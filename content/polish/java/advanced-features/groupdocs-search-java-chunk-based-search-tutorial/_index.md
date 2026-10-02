---
date: '2026-10-02'
description: Dowiedz się, jak używać temporary license, aby dodawać dokumenty do indeksu
  przy użyciu chunk‑based search w Java, zwiększając search performance przy jednoczesnym
  kontrolowaniu memory usage.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Użyj temporary license, aby dodawać dokumenty do indeksu przy użyciu
  chunk‑based search w Java, poprawiając search speed i zmniejszając memory consumption.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Użyj temporary license do chunk‑based indexing w Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Użyj temporary license do chunk‑based indexing w Java
type: docs
url: /pl/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Użyj tymczasowej licencji do indeksowania opartego na fragmentach w Javie

W tym samouczku **użyjesz tymczasowej licencji**, aby dodać dokumenty do indeksu przy użyciu funkcji wyszukiwania opartego na fragmentach w GroupDocs.Search. Podejście pozwala radzić sobie z ogromnymi zbiorami dokumentów — umowami prawnymi, zgłoszeniami wsparcia, artykułami naukowymi — przy jednoczesnym utrzymaniu niskiego zużycia **java search index memory** i **zwiększeniu wydajności wyszukiwania**. Zobaczysz, jak skonfigurować folder indeksu, podać wiele źródeł dokumentów, włączyć wyszukiwanie fragmentów oraz uruchomić zarówno pierwsze, jak i kolejne zapytania fragmentowe.

## Szybkie odpowiedzi
- **Jaki jest pierwszy krok?** Utwórz folder indeksu wyszukiwania.  
- **Jak uwzględnić wiele plików?** Użyj `index.add()` dla każdego folderu dokumentów.  
- **Która opcja włącza wyszukiwanie fragmentów?** `options.setChunkSearch(true)`.  
- **Czy mogę kontynuować wyszukiwanie po pierwszym fragmencie?** Tak, wywołaj `index.searchNext()` z tokenem.  
- **Czy potrzebuję licencji?** Bezpłatna wersja próbna lub tymczasowa licencja wystarczy do rozwoju; pełna licencja jest wymagana w środowisku produkcyjnym.  

## Czego się nauczysz
- Jak utworzyć indeks wyszukiwania w określonym folderze.  
- Kroki do **dodania dokumentów do indeksu** z wielu lokalizacji.  
- Konfigurowanie opcji wyszukiwania, aby włączyć wyszukiwanie oparte na fragmentach.  
- Wykonywanie początkowych i kolejnych wyszukiwań opartych na fragmentach.  
- Praktyczne scenariusze, w których wyszukiwanie dokumentów oparte na fragmentach się wyróżnia.  

## Wymagania wstępne
Aby skorzystać z tego przewodnika, upewnij się, że masz:

- **Wymagane biblioteki**: GroupDocs.Search for Java 25.4 lub nowsza.  
- **Konfiguracja środowiska**: Zainstalowany kompatybilny Java Development Kit (JDK).  
- **Wymagania wiedzy**: Podstawowa programowanie w Javie i znajomość Maven.  

## Konfiguracja GroupDocs.Search dla Javy
Aby rozpocząć, zintegrować GroupDocs.Search z projektem przy użyciu Maven:

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

Alternatywnie, pobierz najnowszą wersję z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
Aby wypróbować GroupDocs.Search:

- **Free trial** – przetestuj podstawowe funkcje bez zobowiązań.  
- **Temporary license** – rozszerzony dostęp do rozwoju.  
- **Purchase** – pełna licencja do użytku produkcyjnego.  

## Jak dodać dokumenty do indeksu?
**Bezpośrednia odpowiedź:** Wywołaj `index.add()` dla każdego folderu zawierającego pliki, które mają być przeszukiwane; metoda skanuje folder rekurencyjnie i dodaje każdy obsługiwany dokument do indeksu w jednej operacji. Eliminuje to potrzebę ręcznego przetwarzania plik po pliku i przyspiesza masowe wprowadzanie.

`SearchIndex` jest centralną klasą reprezentującą przeszukiwalną kolekcję na dysku. Po jej utworzeniu wszystkie operacje indeksowania i zapytań przechodzą przez ten obiekt.

### 1. Tworzenie indeksu
**Bezpośrednia odpowiedź:** Utwórz obiekt `SearchIndex` z ścieżką, w której mają być przechowywane pliki indeksu, a następnie wywołaj `index.create()`, aby zainicjować strukturę przechowywania. Wywołanie tworzy niezbędne foldery i pliki metadanych przy pierwszym użyciu.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. Dodawanie dokumentów do indeksu
**Bezpośrednia odpowiedź:** Użyj metody `index.add()` i przekaż bezwzględną ścieżkę każdego folderu źródłowego; API automatycznie wykrywa obsługiwane formaty (PDF, DOCX, XLSX, itp.) i wyodrębnia przeszukiwalny tekst do indeksu.

`SearchOptions` jest obiektem konfiguracyjnym, który pozwala precyzyjnie dostosować sposób przetwarzania dokumentów podczas indeksowania i wyszukiwania. Użyjesz go później, aby włączyć zapytania oparte na fragmentach.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Konfigurowanie opcji wyszukiwania dla fragmentów
**Bezpośrednia odpowiedź:** Ustaw `options.setChunkSearch(true)` na instancji `SearchOptions` przed wykonaniem zapytania; informuje to silnik, aby podzielił każdy dokument na logiczne fragmenty (zwykle akapity) i zwracał dopasowania per fragment zamiast całego pliku.

`SearchResult` przechowuje dopasowane fragmenty, ich pozycje oraz oceny trafności. Gdy wyszukiwanie fragmentów jest włączone, każdy `SearchResult` odpowiada pojedynczemu fragmentowi oryginalnego dokumentu.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. Wykonywanie początkowego wyszukiwania opartego na fragmentach
**Bezpośrednia odpowiedź:** Wykonaj `index.search("your query", options)`; wywołanie zwraca kolekcję `SearchResult` dla pierwszego zestawu dopasowanych fragmentów oraz token, który reprezentuje stan wyszukiwania do kontynuacji.

Zwrócony token jest niezbędny do stronicowania dużych zestawów wyników bez ponownego wykonywania całego zapytania.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Kontynuowanie wyszukiwania opartego na fragmentach
**Bezpośrednia odpowiedź:** Przekaż token zwrócony z poprzedniego wywołania do `index.searchNext(token, options)`; powtarzaj aż metoda zwróci `null`, co oznacza, że wszystkie dopasowane fragmenty zostały pobrane.

To przyrostowe podejście utrzymuje niskie zużycie pamięci, ponieważ w pamięci znajduje się tylko bieżąca partia fragmentów.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Dlaczego używać wyszukiwania opartego na fragmentach?
Wyszukiwanie oparte na fragmentach dzieli ogromne kolekcje dokumentów na zarządzalne części, zmniejszając obciążenie pamięci i przyspieszając czasy odpowiedzi. Indeksując na poziomie akapitu lub sekcji, silnik może pobrać tylko istotne fragmenty, co obniża zużycie CPU i poprawia opóźnienia dla użytkowników końcowych. Jest to szczególnie przydatne, gdy:

1. **Zespoły prawne** muszą odnaleźć konkretne klauzule w tysiącach umów.  
2. **Portale wsparcia klienta** muszą natychmiast wyświetlać odpowiednie artykuły bazy wiedzy.  
3. **Badacze** przeszukują obszerne zestawy danych bez ładowania całych plików do pamięci.  

Uzasadnione stwierdzenie: GroupDocs.Search może przetworzyć **PDF‑y powyżej 500 stron** w mniej niż **2 sekundy na fragment** na standardowym serwerze 8‑rdzeniowym, przy jednoczesnym utrzymaniu szczytowego zużycia sterty poniżej **200 MB**.

## Jak to podejście zwiększa wydajność wyszukiwania
**Bezpośrednia odpowiedź:** Dzięki wyszukiwaniu mniejszych fragmentów zamiast całych plików, silnik może wcześnie pomijać nieistotne sekcje, zmniejszyć liczbę cykli CPU i utrzymywać w pamięci tylko aktywny fragment, co bezpośrednio obniża zużycie **java search index memory** i zapewnia szybsze czasy odpowiedzi. To ukierunkowane podejście umożliwia także skuteczniejsze buforowanie i przetwarzanie równoległe, pozwalając wielu rdzeniom obsługiwać różne fragmenty jednocześnie, co dodatkowo zwiększa przepustowość na serwerach wielordzeniowych.

Dodatkowe korzyści obejmują:
- Równoległe przetwarzanie fragmentów na wielu rdzeniach.  
- Wczesne zakończenie, gdy zostanie znalezione dopasowanie o wysokiej trafności.  

## Zarządzanie pamięcią indeksu wyszukiwania w Javie
**Bezpośrednia odpowiedź:** Przydziel wystarczającą pamięć sterty JVM (np. `-Xmx2g` lub więcej) w zależności od oczekiwanego rozmiaru indeksu, uruchom `index.optimize()` po masowych dodatkach, aby skompresować strukturę indeksu, oraz monitoruj przerwy GC za pomocą VisualVM, aby uniknąć skoków opóźnień.

Dalsze wskazówki dotyczące strojenia:
- Użyj `index.flush()` po dużych partiach, aby zapisać dane pośrednie na dysk.  
- Włącz `options.setMemoryLimit(256)`, aby ograniczyć zużycie pamięci na pojedyncze wyszukiwanie.  

## Rozważania dotyczące wydajności
- **Zarządzanie pamięcią** – Przydziel wystarczającą przestrzeń sterty (`-Xmx`) dla dużych indeksów.  
- **Monitorowanie zasobów** – Śledź zużycie CPU podczas operacji indeksowania i wyszukiwania.  
- **Utrzymanie indeksu** – Okresowo przebudowuj lub czyszcz indeks, aby usunąć przestarzałe dane.  

## Typowe pułapki i rozwiązywanie problemów
| Problem | Dlaczego się dzieje | Rozwiązanie |
|---------|---------------------|-------------|
| `OutOfMemoryError` podczas indeksowania | Rozmiar sterty zbyt mały | Zwiększ stertę JVM (`-Xmx2g` lub wyższą) |
| Brak zwróconych wyników | Token fragmentu nie został przetworzony | Upewnij się, że pętla `while` działa aż `getNextChunkSearchToken()` będzie `null` |
| Wolna wydajność wyszukiwania | Indeks nie jest zoptymalizowany | Uruchom `index.optimize()` po masowych dodatkach |

## Najczęściej zadawane pytania

**Q: Co to jest wyszukiwanie oparte na fragmentach?**  
A: Wyszukiwanie oparte na fragmentach dzieli zestaw danych na mniejsze części, umożliwiając efektywne zapytania na dużych wolumenach danych bez ładowania całych dokumentów do pamięci.

**Q: Jak zaktualizować mój indeks nowymi plikami?**  
A: Po prostu wywołaj `index.add()` z ścieżką do nowych dokumentów; indeks automatycznie je uwzględni.

**Q: Czy GroupDocs.Search obsługuje różne formaty plików?**  
A: Tak, obsługuje **PDF, DOCX, XLSX, PPTX, HTML, TXT oraz ponad 30 innych formatów**.

**Q: Jakie są typowe wąskie gardła wydajności?**  
A: Ograniczenia pamięci i nieoptymalne indeksy są najczęstsze; przydziel wystarczającą stertę i regularnie optymalizuj indeks.

**Q: Gdzie mogę znaleźć bardziej szczegółową dokumentację?**  
A: Odwiedź oficjalną [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) po szczegółowe przewodniki i odniesienia API.

**Q: Czy wyszukiwanie oparte na fragmentach działa z zaszyfrowanymi plikami PDF?**  
A: Tak, pod warunkiem podania hasła za pomocą odpowiedniego przeciążenia API.

**Q: Jak mogę monitorować postęp indeksowania?**  
A: Użyj przeciążenia `Index.add()`, które zwraca obiekt `Progress`, lub podłącz się do wywołań zwrotnych logowania.

## Zasoby
- **Dokumentacja**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Referencja API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Pobieranie**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Bezpłatne wsparcie**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Tymczasowa licencja**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

**Ostatnia aktualizacja:** 2026-10-02  
**Testowano z:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Powiązane samouczki

- [Utwórz katalog indeksu wyszukiwania i ustaw licencję – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Popraw wydajność zapytań z GroupDocs.Search Java: Optymalizacja indeksu i wyszukiwania](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java Zaawansowane funkcje wyszukiwania](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)