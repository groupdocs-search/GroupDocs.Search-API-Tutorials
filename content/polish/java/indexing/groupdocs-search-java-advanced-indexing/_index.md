---
date: '2025-12-29'
description: Dowiedz się, jak optymalizować wydajność wyszukiwania, korzystając z
  zaawansowanych funkcji indeksowania GroupDocs.Search dla Javy, w tym anulowania,
  operacji asynchronicznych, wielowątkowości i dostosowywania metadanych.
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: Optymalizuj wydajność wyszukiwania dzięki zaawansowanym technikom indeksowania
  w GroupDocs.Search dla Javy
type: docs
url: /pl/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Optymalizacja wydajności wyszukiwania przy użyciu zaawansowanych technik indeksowania w GroupDocs.Search dla Javy

W dzisiejszym szybkim środowisku cyfrowym **optymalizacja wydajności wyszukiwania** jest niezbędna do dostarczania natychmiastowych wyników użytkownikom. Niezależnie od tego, czy tworzysz własną wyszukiwarkę, czy ulepszasz istniejący system zarządzania dokumentami, odpowiednia strategia indeksowania może znacząco zmniejszyć opóźnienia i zużycie zasobów. W tym samouczku przeprowadzimy Cię przez najpotężniejsze funkcje GroupDocs.Search dla Javy — anulowanie, asynchroniczne indeksowanie, wielowątkowość i dostosowywanie metadanych — abyś mógł **add documents index** szybciej i wydajniej.

**Czego się nauczysz**

- Jak anulować operację indeksowania po określonym czasie
- Wykonywanie asynchronicznych operacji indeksowania i obsługa zmian statusu
- Konfigurowanie wielowątkowości w celu szybszego indeksowania
- Dostosowywanie opcji indeksowania metadanych

Upewnijmy się, że masz wszystko, czego potrzebujesz, zanim przejdziemy do kodu.

## Prerequisites

- **GroupDocs.Search Library** – wersja 25.4 lub nowsza.  
- **Java Development Environment** – zalecany JDK 8 lub wyższy.  
- Podstawowa znajomość Javy i koncepcji indeksowania.

### Setting Up GroupDocs.Search for Java

#### Maven Installation

Dodaj repozytorium i zależność do pliku `pom.xml`:

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

#### Direct Download

Alternatywnie, pobierz najnowszy plik JAR z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**License Acquisition** – Rozpocznij od darmowej wersji próbnej lub poproś o tymczasową licencję, aby odblokować pełny zestaw funkcji.

### Basic Initialization and Setup

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

## Quick Answers
- **Co robi anulowanie?** Zatrzymuje indeksowanie po określonym czasie, aby zwolnić zasoby.  
- **Czy mogę indeksować dokumenty asynchronicznie?** Tak – ustaw `options.setAsync(true)`.  
- **Ile wątków mogę używać?** Dowolna dodatnia liczba całkowita; typowe wartości to 2‑4 dla większości serwerów.  
- **Czy indeksowanie metadanych jest opcjonalne?** Absolutnie – możesz włączyć je lub dopasować per pole.  
- **Czy potrzebuję licencji na te funkcje?** Wersja próbna działa do testów; pełna licencja jest wymagana w produkcji.

## What Is “Optimize Search Performance” in This Context?

Optymalizacja wydajności wyszukiwania oznacza skonfigurowanie procesu indeksowania tak, aby zużywał odpowiednią ilość CPU, pamięci i czasu, jednocześnie dostarczając natychmiastowo najbardziej istotne wyniki. Kontrolując anulowanie, asynchroniczne wykonywanie, wątkowanie i obsługę metadanych, bezpośrednio wpływasz na to, jak szybko silnik może **add documents index** i odpowiadać na zapytania.

## Why Use Advanced Indexing Features?

- **Zredukowane opóźnienie** – Asynchroniczne i wielowątkowe indeksowanie utrzymuje responsywność aplikacji.  
- **Lepsze zarządzanie zasobami** – Anulowanie zapobiega niekontrolowanym procesom.  
- **Dostosowana trafność wyszukiwania** – Opcje metadanych pozwalają wyświetlać najważniejsze informacje.  

## Implementation Guide

### Cancellation Property

**Przegląd** – Anuluj indeksowanie po określonym czasie, aby uniknąć nadmiernego zużycia zasobów.

#### Step 1: Set Up the Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Create Indexing Options with Cancellation

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

**Key Points**

- `setCancellation()` aktywuje funkcję.  
- `cancelAfter(int milliseconds)` definiuje limit czasu (3 sekundy w tym przykładzie).  

### Asynchronous Property

**Przegląd** – Uruchom indeksowanie w tle i nasłuchuj zmian statusu.

#### Step 1: Set Up the Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Subscribe to Status Changed Event

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

#### Step 3: Configure Asynchronous Options

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Threads Property

**Przegląd** – Przyspiesz indeksowanie, wykorzystując wiele rdzeni CPU.

#### Step 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Configure Multi‑threading

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Metadata Indexing Options Property

**Przegląd** – Dostosuj, które metadane dokumentu są indeksowane i jak są przechowywane.

#### Step 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Configure Metadata Options

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

## Practical Applications

1. **Systemy zarządzania dokumentami** – Użyj asynchronicznego indeksowania, aby interfejs był responsywny, podczas gdy duże partie są przetwarzane w tle.  
2. **Silniki wyszukiwania treści** – Zastosuj anulowanie, aby zapobiec długotrwałym zadaniom pochłaniającym zasoby serwera w szczycie ruchu.  
3. **Duże potoki ingestii** – Wykorzystaj wielowątkowość, aby **add documents index** na dużą skalę, dramatycznie skracając czas przetwarzania.  

## Performance Considerations

- **Zarządzanie wątkami** – Monitoruj użycie CPU; zbyt wiele wątków może powodować narzut przełączania kontekstu.  
- **Ślad pamięci** – Limity metadanych (np. `setMaxBytesToIndexField`) pomagają utrzymać przewidywalne zużycie pamięci.  
- **Garbage Collection** – Używaj odpowiednich flag JVM (`-Xmx`, `-XX:+UseG1GC`) przy indeksowaniu ogromnych korpusów.  

## Common Issues and Solutions

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---------|--------------|-----|
| Indeksowanie nigdy się nie kończy | Anulowanie ustawione zbyt nisko | Zwiększ wartość `cancelAfter` lub usuń anulowanie dla długich zadań |
| Brak aktualizacji statusu w trybie async | Obsługa zdarzenia nie została poprawnie podłączona | Upewnij się, że `index.getEvents().StatusChanged.add(...)` jest wywoływane przed `index.add` |
| Błędy out‑of‑memory | Zbyt wiele wątków lub wysokie limity metadanych | Zmniejsz `options.setThreads` i obniż limity pól metadanych |
| Brak metadanych w wynikach | Indeksowanie metadanych wyłączone | Sprawdź, czy `options.getMetadataIndexingOptions()` jest skonfigurowane i nie ustawione na ignorowanie pól |

## Frequently Asked Questions

**P: Jak uzyskać tymczasową licencję dla GroupDocs.Search?**  
O: Odwiedź [stronę tymczasowej licencji GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**P: Czy mogę anulować operację indeksowania w połowie?**  
O: Tak – użyj właściwości anulowania z `cancelAfter()` lub wywołaj programowo `Cancellation.cancel()`.

**P: Jakie są przykłady zastosowań asynchronicznego indeksowania?**  
O: Pobieranie dokumentów w czasie rzeczywistym, przetwarzanie wsadowe w tle oraz aplikacje z responsywnym UI korzystają z asynchronicznego indeksowania.

**P: Czy bezpiecznie zwiększyć liczbę wątków na współdzielonym serwerze?**  
O: Zwiększaj stopniowo i monitoruj obciążenie CPU; w silnie współdzielonych środowiskach utrzymuj umiarkowaną liczbę wątków (2‑4).

**P: Jak indeksowanie metadanych wpływa na trafność wyszukiwania?**  
O: Poprawnie zaindeksowane metadane (autor, data utworzenia, tagi) mogą mieć wyższą wagę w zapytaniach, zwiększając dokładność wyników.

## Conclusion

Korzystając z tych zaawansowanych funkcji GroupDocs.Search dla Javy, **zoptymalizujesz wydajność wyszukiwania** w różnych scenariuszach — od szybkiej ingestii dokumentów po precyzyjną kontrolę metadanych. Eksperymentuj z różnymi konfiguracjami, monitoruj zużycie zasobów i dostosuj ustawienia do swojego konkretnego obciążenia, aby uzyskać najlepsze wyniki.

---

**Last Updated:** 2025-12-29  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs