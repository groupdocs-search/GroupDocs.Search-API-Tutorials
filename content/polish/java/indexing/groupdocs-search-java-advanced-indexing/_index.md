---
date: '2026-08-15'
description: Dowiedz się, jak poprawić opóźnienie wyszukiwania, korzystając z advanced
  indexing features GroupDocs.Search dla Java, w tym cancellation, async operations,
  multithreading i metadata customization.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: Popraw opóźnienie wyszukiwania w GroupDocs.Search dla Java, używając
  cancellation, async operations, multithreading i metadata customization. Zwiększ
  wydajność i zmniejsz zużycie zasobów.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: Popraw opóźnienie wyszukiwania dzięki advanced indexing w GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: Popraw opóźnienie wyszukiwania dzięki advanced indexing w GroupDocs
type: docs
url: /pl/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Popraw opóźnienie wyszukiwania dzięki zaawansowanemu indeksowaniu w GroupDocs

W dzisiejszym szybkim środowisku cyfrowym, **poprawa opóźnienia wyszukiwania** jest niezbędna do dostarczania natychmiastowych wyników użytkownikom. Niezależnie od tego, czy budujesz własną wyszukiwarkę, czy ulepszasz istniejący system zarządzania dokumentami, odpowiednia strategia indeksowania może dramatycznie skrócić opóźnienie, zmniejszyć zużycie zasobów i **poprawić opóźnienie wyszukiwania** we wszystkich obszarach. W tym samouczku przeprowadzimy Cię przez najpotężniejsze funkcje GroupDocs.Search dla Javy — anulowanie, asynchroniczne indeksowanie, wielowątkowość i dostosowywanie metadanych — abyś mógł **dodawać dokumenty do indeksu** szybciej i bardziej efektywnie.

**Co się nauczysz**

- Jak anulować operację indeksowania po określonym czasie
- Wykonywanie asynchronicznych operacji indeksowania i obsługa zmian statusu
- Konfigurowanie wielowątkowości w celu szybszego indeksowania
- Dostosowywanie opcji indeksowania metadanych, aby **dostosować metadane wyszukiwania**

Upewnijmy się, że masz wszystko, czego potrzebujesz, zanim zanurkujemy w kod.

## Szybkie odpowiedzi
- **Co robi anulowanie?** Zatrzymuje indeksowanie po określonym czasie, zwalniając CPU i pamięć dla innych zadań.  
- **Czy mogę indeksować dokumenty asynchronicznie?** Tak – włącz to za pomocą `options.setAsync(true)`.  
- **Ile wątków mogę używać?** Dowolna dodatnia liczba całkowita; 2‑4 wątki są typowe dla większości serwerów.  
- **Czy indeksowanie metadanych jest opcjonalne?** Absolutnie – możesz je włączyć lub dopasować per pole.  
- **Czy potrzebuję licencji na te funkcje?** Wersja próbna działa w testach; pełna licencja jest wymagana w produkcji.

## Wymagania wstępne

- **Biblioteka GroupDocs.Search** – wersja 25.4 lub późniejsza.  
- **Środowisko programistyczne Java** – zalecany JDK 8 lub wyższy.  
- Podstawowa znajomość Javy i koncepcji indeksowania.

### Konfiguracja GroupDocs.Search dla Javy

#### Instalacja Maven

Dodaj repozytorium i zależność do pliku `pom.xml`:

Konfiguracja `pom.xml` informuje Maven, które artefakty GroupDocs.Search pobrać i uwzględnić w projekcie.

```xml
<repositories>
    <repository>
        <id>repository.groupdocs.com</id>
        <name>GroupDocs Repository</name>
        <url>https://releases.groupdocs.com/search/java/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>com.groupdocs</groupId>
        <artifactId>groupdocs-search</artifactId>
        <version>25.4</version>
    </dependency>
</dependencies>
```

#### Bezpośrednie pobranie

Alternatywnie, pobierz najnowszy plik JAR z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**Pozyskanie licencji** – Rozpocznij od darmowej wersji próbnej lub poproś o tymczasową licencję, aby odblokować pełny zestaw funkcji.

### Podstawowa inicjalizacja i konfiguracja

Klasa `SearchIndex` jest punktem wejścia, który reprezentuje indeks przeszukiwalny przechowywany na dysku lub w pamięci.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## Co oznacza „optymalizacja wydajności wyszukiwania” w tym kontekście?

Optymalizacja wydajności wyszukiwania oznacza skonfigurowanie procesu indeksowania tak, aby zużywał odpowiednią ilość CPU, pamięci i czasu, jednocześnie dostarczając najistotniejsze wyniki natychmiast. Kontrolując anulowanie, asynchroniczne wykonywanie, wątkowanie i obsługę metadanych, bezpośrednio wpływasz na to, jak szybko silnik może **dodawać dokumenty do indeksu** i odpowiadać na zapytania.

## Dlaczego używać zaawansowanych funkcji indeksowania?

Asynchroniczne i wielowątkowe indeksowanie utrzymuje responsywność aplikacji, podczas gdy anulowanie zapobiega niekontrolowanym procesom. Dobrze dopasowane opcje metadanych pozwalają wyświetlać najważniejsze informacje, co bezpośrednio **poprawia opóźnienie wyszukiwania** dla użytkowników końcowych. Dodatkowo, te funkcje redukują skoki CPU, zmniejszają obciążenie pamięci i umożliwiają płynniejsze skalowanie przy obsłudze dużych wolumenów dokumentów.

## Jak poprawić opóźnienie wyszukiwania dzięki zaawansowanemu indeksowaniu?

Załaduj swoją instancję `SearchIndex`, skonfiguruj `IndexingOptions` z ustawieniami anulowania, async i wątków, a następnie wywołaj `index.add(document)` — ta kombinacja skraca całkowity czas indeksowania nawet o 60 % przy typowych obciążeniach i gwarantuje, że długotrwałe zadania nie będą blokować innych operacji. Możesz także dostosować limity indeksowania metadanych i monitorować postęp poprzez zdarzenia zmiany statusu, aby zapewnić, że pipeline mieści się w budżetach wydajności.

## Przewodnik implementacji

### Właściwość anulowania

**Przegląd** – Anuluj indeksowanie po określonym czasie, aby uniknąć nadmiernego zużycia zasobów.

#### Krok 1: przygotuj środowisko

Utwórz instancję `SearchIndex` wskazującą na folder indeksu.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Krok 2: utwórz opcje indeksowania z anulowaniem

`IndexingOptions` pozwala określić, jak zachowuje się silnik indeksujący.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Kluczowe punkty**

- `setCancellation()` aktywuje funkcję.  
- `cancelAfter(int milliseconds)` definiuje limit czasu (3 sekundy w tym przykładzie).

### Właściwość asynchroniczna

**Przegląd** – Uruchom indeksowanie w tle i nasłuchuj zmian statusu.

#### Krok 1: przygotuj środowisko

Zainicjuj indeks i przygotuj kolekcję dokumentów.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Krok 2: subskrybuj zdarzenie zmiany statusu

Zdarzenie `StatusChanged` powiadamia Cię, gdy zadanie indeksowania przechodzi pomiędzy stanami.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Krok 3: skonfiguruj opcje asynchroniczne

Włącz tryb async, aby wywołanie zwracało się natychmiast, a przetwarzanie kontynuowało w tle.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Właściwość wątków

**Przegląd** – Przyspiesz indeksowanie, wykorzystując wiele rdzeni CPU.

#### Krok 1: przygotuj środowisko

Przygotuj indeks i upewnij się, że JVM ma wystarczającą pamięć heap.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Krok 2: skonfiguruj wielowątkowość

Ustaw liczbę wątków roboczych; każdy wątek przetwarza podzbiór dokumentów.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Właściwość opcji indeksowania metadanych

**Przegląd** – Dostosuj, które metadane dokumentu są indeksowane i jak są przechowywane.

#### Krok 1: przygotuj środowisko

Wczytaj dokument zawierający pola metadanych, takie jak autor, tytuł i niestandardowe tagi.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Krok 2: skonfiguruj opcje metadanych

`MetadataIndexingOptions` pozwala włączać lub wyłączać poszczególne pola metadanych oraz definiować limity rozmiaru.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Praktyczne zastosowania

1. **Systemy zarządzania dokumentami** – Użyj asynchronicznego indeksowania, aby UI pozostawało responsywne, podczas gdy duże partie są przetwarzane w tle.  
2. **Wyszukiwarki treści** – Zastosuj anulowanie, aby zapobiec zajmowaniu zasobów serwera przez długotrwałe zadania w szczycie ruchu.  
3. **Duże pipeline’y ingestii** – Wykorzystaj wielowątkowość, aby **dodawać dokumenty do indeksu** na dużą skalę, dramatycznie skracając czas przetwarzania.  

## Rozważania dotyczące wydajności

- **Zarządzanie wątkami** – Monitoruj użycie CPU; zbyt wiele wątków może powodować narzut przełączania kontekstów.  
- **Ślad pamięci** – Limity metadanych (np. `setMaxBytesToIndexField`) utrzymują przewidywalne zużycie pamięci.  
- **Garbage collection** – Używaj odpowiednich flag JVM (`-Xmx`, `-XX:+UseG1GC`) przy indeksowaniu ogromnych korpusów.  

## Typowe problemy i rozwiązania

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---------|--------------|-----|
| Indeksowanie nigdy się nie kończy | Anulowanie ustawione zbyt nisko | Zwiększ wartość `cancelAfter` lub usuń anulowanie dla długich zadań |
| Brak aktualizacji statusu w trybie async | Obsługa zdarzeń nie podłączona prawidłowo | Upewnij się, że `index.getEvents().StatusChanged.add(...)` jest wywoływane przed `index.add` |
| Błędy Out‑of‑memory | Zbyt wiele wątków lub wysokie limity metadanych | Zmniejsz `options.setThreads` i obniż limity pól metadanych |
| Brak metadanych w wynikach | Indeksowanie metadanych wyłączone | Zweryfikuj, że `options.getMetadataIndexingOptions()` jest skonfigurowane i nie ustawione na ignorowanie pól |

## Najczęściej zadawane pytania

**Q: Jak uzyskać tymczasową licencję dla GroupDocs.Search?**  
A: Odwiedź [stronę tymczasowej licencji GroupDocs](https://purchase.groupdocs.com/temporary-license/) i postępuj zgodnie z instrukcjami wyświetlanymi na ekranie.

**Q: Czy mogę anulować operację indeksowania w połowie?**  
A: Tak – użyj właściwości anulowania z `cancelAfter()` lub wywołaj programowo `Cancellation.cancel()`.

**Q: Jakie są przykłady zastosowań asynchronicznego indeksowania?**  
A: Pobieranie dokumentów w czasie rzeczywistym, przetwarzanie wsadowe w tle oraz aplikacje z responsywnym UI korzystają z asynchronicznego indeksowania.

**Q: Czy bezpiecznie zwiększyć liczbę wątków na współdzielonym serwerze?**  
A: Zwiększaj stopniowo i monitoruj obciążenie CPU; w silnie współdzielonych środowiskach utrzymuj liczbę wątków na umiarkowanym poziomie (2‑4).

**Q: Jak indeksowanie metadanych wpływa na trafność wyszukiwania?**  
A: Poprawnie zaindeksowane metadane (autor, data utworzenia, tagi) mogą mieć wyższą wagę w zapytaniach, zwiększając dokładność wyników.

## Podsumowanie

Korzystając z tych zaawansowanych funkcji GroupDocs.Search dla Javy, **poprawisz opóźnienie wyszukiwania** w różnych scenariuszach — od szybkiego wprowadzania dokumentów po precyzyjną kontrolę metadanych. Eksperymentuj z różnymi konfiguracjami, monitoruj zużycie zasobów i dostosuj ustawienia do konkretnego obciążenia, aby uzyskać najlepsze wyniki.

---

**Ostatnia aktualizacja:** 2026-08-15  
**Testowano z:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Powiązane samouczki

- [Popraw wydajność zapytań w GroupDocs.Search Java: optymalizacja indeksu i wyszukiwania](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Jak dodać dokumenty do indeksu przy użyciu indeksowania metadanych w Javie z GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Jak dodać wiele aliasów i dodać dokumenty do indeksu w GroupDocs.Search dla Javy](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)