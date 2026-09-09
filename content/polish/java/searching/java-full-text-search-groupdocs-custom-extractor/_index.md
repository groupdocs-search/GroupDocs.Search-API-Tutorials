---
date: '2026-08-05'
description: Dowiedz się, jak stworzyć ekstraktor plików dziennika do pełnotekstowego
  wyszukiwania w Javie przy użyciu GroupDocs.Search. Dodaj dokumenty do indeksu, zoptymalizuj
  wydajność wyszukiwania i efektywnie obsługuj duże pliki dziennika.
keywords:
- full text search java
- optimize search performance
- add documents to index
- java full text search
lastmod: '2026-08-05'
og_description: Poradnik Full text search java pokazuje, jak zbudować własny ekstraktor
  plików dziennika przy użyciu GroupDocs.Search, dodać dokumenty do indeksu i zoptymalizować
  wydajność wyszukiwania dla ogromnych archiwów dzienników.
og_image_alt: Diagram of log file extractor workflow in Java using GroupDocs.Search
og_title: 'Full text search java: ekstraktor plików dziennika z GroupDocs'
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  headline: 'Full text search java: log file extractor with GroupDocs'
  type: TechArticle
- description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  name: 'Full text search java: log file extractor with GroupDocs'
  steps:
  - name: define the custom extractor
    text: '`TextExtractorBase` is the abstract base class you extend to create a custom
      extractor. It declares which file extensions the extractor supports and contains
      the core extraction logic. **Key points** - `getFileExtensions()` registers
      the extractor for `.log` files. - `extractText` is where you can s'
  - name: configure index settings with the extractor
    text: Add your extractor to the `IndexSettings` and enable `autoReindex` so new
      logs are indexed automatically without manual intervention. `IndexSettings`
      configures index behavior such as memory limits and custom extractors. `autoReindex`
      automatically updates the index when source files change.
  - name: add documents to the index
    text: Now that the index recognises log files, you can **add documents to index**
      just like any other supported format.
  - name: search the index
    text: Perform plain‑text queries. The custom extractor guarantees that every log
      entry is searchable.
  type: HowTo
- questions:
  - answer: The default extractor handles common formats (PDF, DOCX, etc.). A custom
      log file extractor lets you define exactly how plain‑text log entries are parsed
      and indexed.
    question: How does a log file extractor differ from the default extractor?
  - answer: Yes, by adding a pre‑processing step that extracts files from the archive
      before feeding them to the index.
    question: Can I index compressed log archives (e.g., .zip)?
  - answer: Enable `autoReindex` and schedule a background watcher that calls `index.add(newLogFile)`
      whenever a new file appears.
    question: What’s the best way to keep the index up‑to‑date with continuously generated
      logs?
  - answer: Practically, the limit is bound by available memory. Splitting very large
      logs into smaller chunks before indexing is recommended.
    question: Is there a limit to the size of a single log file that can be indexed?
  - answer: Yes, the search API includes fuzzy matching, wildcards, and proximity
      queries to improve result relevance.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs
- Java search
- log file extractor
- indexing
title: 'Full text search java: ekstraktor plików dziennika z GroupDocs'
type: docs
url: /pl/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# Pełnotekstowe wyszukiwanie java: ekstraktor plików dziennika z GroupDocs

Pełnotekstowe wyszukiwanie java jest fundamentem każdego systemu, który musi szybko odnajdywać informacje w ogromnych zbiorach dokumentów. W tym samouczku dowiesz się, jak skonfigurować GroupDocs.Search, stworzyć własny ekstraktor plików dziennika, dodać dokumenty do indeksu oraz zoptymalizować wydajność wyszukiwania przy pracy z gigabajtami danych dziennika.

## Czego się nauczysz
- Skonfigurować i uruchomić GroupDocs.Search dla Java.  
- Zaimplementować **ekstraktor plików dziennika**, który parsuje pliki tekstowe zgodnie z Twoimi potrzebami.  
- **Dodawać dokumenty do indeksu** obok PDF‑ów, DOCX‑ów i innych formatów.  
- Praktyczne scenariusze, w których **ekstraktor plików dziennika** przynosi wymierne korzyści.  
- Sprawdzone wskazówki, jak **optymalizować wydajność wyszukiwania** dla archiwów dzienników o rozmiarze wielu gigabajtów.

## Szybkie odpowiedzi
- **Czym jest ekstraktor plików dziennika?** Niestandardowy komponent, który instruuje GroupDocs.Search, jak odczytywać i indeksować pliki tekstowe dziennika.  
- **Dlaczego warto używać GroupDocs.Search?** Obsługuje indeksowanie ponad 50 formatów, zapewnia automatyczne ponowne indeksowanie i radzi sobie z indeksami do 10 GB przy zużyciu pamięci poniżej 2 GB RAM.  
- **Czy potrzebna jest licencja?** Tak – wymagana jest licencja próbna lub pełna, aby włączyć bibliotekę.  
- **Czy mogę jednocześnie indeksować inne typy plików?** Oczywiście; możesz mieszać PDF‑y, DOCX‑y i własne pliki dziennika w jednym indeksie.  
- **Jak poprawić wydajność?** Używaj przyrostowego indeksowania, dostosuj `IndexSettings` i włącz flagę `autoReindex`.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz następujące elementy:

### Wymagane biblioteki
Dodaj zależność Maven GroupDocs.Search do swojego `pom.xml`. Użyj najnowszej wersji zgodnej z poziomem Java w Twoim projekcie.

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

Alternatywnie, pobierz najnowszą wersję bezpośrednio z [GroupDocs.Search dla Java – wydania](https://releases.groupdocs.com/search/java/).

### Konfiguracja środowiska
- JDK 8 lub wyższy.  
- Znajomość programowania w Javie oraz podstawowych koncepcji obsługi plików.

### Uzyskiwanie licencji
Rozpocznij od pobrania darmowej licencji próbnej, aby wypróbować funkcje GroupDocs.Search. W środowisku produkcyjnym zakup pełną licencję lub poproś o tymczasową poprzez [stronę GroupDocs](https://purchase.groupdocs.com/temporary-license/).

## Konfiguracja GroupDocs.Search dla Java

Aby rozpocząć, zainicjalizuj bibliotekę i zastosuj plik licencyjny:

1. **Konfiguracja Maven** – upewnij się, że zależność z poprzedniego kroku jest obecna.  
2. **Inicjalizacja licencji** – załaduj plik licencji przed jakimikolwiek wywołaniami API.

```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

Po przygotowaniu środowiska możesz przejść do budowy własnego **ekstraktora plików dziennika**.

## Czym jest ekstraktor plików dziennika?

Ekstraktor plików dziennika to fragment kodu, który instruuje GroupDocs.Search, jak odczytywać surowe pliki dziennika (zwykle `.log`) i przekształca ich zawartość w tekst możliwy do przeszukania. Dostarczając własny ekstraktor, zyskujesz pełną kontrolę nad regułami parsowania, filtrowaniem szumu i wyodrębnianiem wyłącznie informacji istotnych dla Twojego scenariusza wyszukiwania.

## Tworzenie ekstraktora plików dziennika

GroupDocs.Search umożliwia podłączanie własnych ekstraktorów tekstu dla dowolnego typu pliku. Postępuj zgodnie z poniższymi krokami, aby stworzyć ekstraktor dla plików dziennika.

### Krok 1: zdefiniuj własny ekstraktor
`TextExtractorBase` to abstrakcyjna klasa bazowa, którą rozszerzasz, aby stworzyć własny ekstraktor. Deklaruje ona, które rozszerzenia plików obsługuje ekstraktor oraz zawiera podstawową logikę ekstrakcji.

```java
import com.groupdocs.search.extractors.TextExtractorBase;

public class LogExtractor extends TextExtractorBase {
    @Override
    public String[] getFileExtensions() {
        return new String[]{"log"};
    }

    @Override
    public String extractText(String documentContent) {
        // Custom logic for extracting text from log files.
        return documentContent; // Implement your custom extraction here.
    }
}
```

**Kluczowe punkty**  
- `getFileExtensions()` rejestruje ekstraktor dla plików `.log`.  
- `extractText` to miejsce, w którym możesz usuwać znaczniki czasu, filtrować linie debugowania lub zastosować dowolne przetwarzanie wstępne niezbędne do **wyszukiwania w dużych plikach dziennika**.

### Krok 2: skonfiguruj ustawienia indeksu z ekstraktorem
Dodaj swój ekstraktor do `IndexSettings` i włącz `autoReindex`, aby nowe dzienniki były indeksowane automatycznie, bez ręcznej interwencji.

`IndexSettings` konfiguruje zachowanie indeksu, takie jak limity pamięci i własne ekstraktory.  
`autoReindex` automatycznie aktualizuje indeks, gdy zmieniają się pliki źródłowe.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

public class CustomTextExtractorFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        IndexSettings settings = new IndexSettings();
        
        // Adding the custom text extractor to the settings.
        settings.getCustomExtractors().addItem(new LogExtractor());
        
        // Creating or loading an index with specified settings and enabling auto-reindexing.
        Index index = new Index(indexFolder, settings, true);
    }
}
```

### Krok 3: dodaj dokumenty do indeksu
Teraz, gdy indeks rozpoznaje pliki dziennika, możesz **dodawać dokumenty do indeksu** tak samo, jak każdy inny obsługiwany format.

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Loading or creating an index in the specified directory.
        Index index = new Index(indexFolder);
        
        // Adding documents from the folder to the index.
        index.add(documentsFolder);
    }
}
```

### Krok 4: przeszukaj indeks
Wykonuj zapytania tekstowe. Niestandardowy ekstraktor zapewnia, że każdy wpis dziennika jest przeszukiwalny.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchDocumentsFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        
        // Loading the existing index.
        Index index = new Index(indexFolder);
        
        // Define search queries
        String query1 = "objection";
        String query2 = "log";
        
        // Performing searches and retrieving results.
        SearchResult result1 = index.search(query1);
        SearchResult result2 = index.search(query2);
    }
}
```

## Wskazówki optymalizacji wydajności wyszukiwania

- **Indeksowanie przyrostowe** – dodawaj tylko nowe lub zmienione pliki dziennika zamiast przebudowywać cały indeks.  
- **Zarządzanie pamięcią** – flaga `autoReindex` utrzymuje niskie zużycie RAM, zapisując dane pośrednie na dysk.  
- **Ustawienia indeksu** – dostosuj `setMaxMemoryUsage` do pojemności serwera; typowa wartość to 1 GB dla indeksu o rozmiarze 10 GB.  
- **Optymalizacja zapytań** – używaj zapytań frazowych, znaków wieloznacznych lub filtrów, aby zawęzić wyniki przy przeszukiwaniu ogromnych archiwów dzienników.

## Praktyczne zastosowania

GroupDocs.Search może być wykorzystywany w wielu rzeczywistych scenariuszach, takich jak:

- **Zarządzanie dziennikami** – znajdowanie komunikatów o błędach, działań użytkowników lub konkretnych znaczników czasu w gigabajtach danych dziennika w ciągu kilku sekund.  
- **Systemy wyszukiwania dokumentów** – utrzymanie jednego przeszukiwalnego repozytorium, które obejmuje PDF‑y, dokumenty Word, arkusze kalkulacyjne i własne pliki dziennika.  
- **Analiza treści** – generowanie raportów częstotliwości słów kluczowych lub wykrywanie anomalii w strumieniowych danych dziennika.

## Rozważania dotyczące wydajności

Podczas wdrażania GroupDocs.Search w dużej skali pamiętaj o następujących najlepszych praktykach:

- Przechowuj indeksy na szybkich dyskach SSD, aby zminimalizować opóźnienia odczytu/zapisu.  
- Monitoruj zużycie sterty JVM; rozważ przeniesienie dużych indeksów do osobnego procesu, jeśli pamięć stanie się wąskim gardłem.  
- Włącz `autoReindex` (jak pokazano), aby utrzymać indeks aktualny bez ręcznego przebudowywania.

## Zakończenie

Do tej pory zbudowałeś **ekstraktor plików dziennika**, nauczyłeś się **dodawać dokumenty do indeksu** oraz odkryłeś sposoby **optymalizacji wydajności wyszukiwania** dla dużych archiwów dzienników. To połączenie pozwala Twoim aplikacjom Java zapewniać szybkie, dokładne pełnotekstowe wyszukiwanie we wszystkich typach dokumentów.

Po dalsze zgłębienie tematu zapoznaj się z oficjalną [dokumentacją GroupDocs](https://docs.groupdocs.com/search/java/) lub eksperymentuj z różnymi implementacjami ekstraktorów, aby dopasować je do swojego unikalnego przypadku użycia.

## Sekcja FAQ
1. **Jakie typy plików mogę indeksować przy użyciu GroupDocs.Search?**  
   - Możesz indeksować PDF‑y, dokumenty Word, arkusze kalkulacyjne i wiele innych formatów, a także własne pliki dziennika za pomocą ekstraktorów tekstu.  
2. **Jak efektywnie obsługiwać duże kolekcje dokumentów?**  
   - Korzystaj z aktualizacji przyrostowych, partycjonuj indeksy i dostosuj `IndexSettings`, aby skutecznie zarządzać zasobami.  
3. **Czy GroupDocs.Search można zintegrować z innymi systemami?**  
   - Tak, oferuje czyste API Java, które może być osadzone w istniejących usługach, mikro‑serwisach lub aplikacjach webowych.  
4. **Czym jest licencja tymczasowa i jak ją uzyskać?**  
   - Licencja tymczasowa zapewnia pełną funkcjonalność do oceny bez ograniczeń czasowych. Złóż wniosek poprzez [stronę GroupDocs](https://purchase.groupdocs.com/temporary-license/).

## Najczęściej zadawane pytania

**Q: Jak ekstraktor plików dziennika różni się od domyślnego ekstraktora?**  
A: Domyślny ekstraktor obsługuje popularne formaty (PDF, DOCX itp.). Niestandardowy ekstraktor plików dziennika pozwala precyzyjnie określić, w jaki sposób parsowane i indeksowane są wpisy tekstowe dziennika.

**Q: Czy mogę indeksować skompresowane archiwa dzienników (np. .zip)?**  
A: Tak, poprzez dodanie kroku wstępnego przetwarzania, który wyodrębnia pliki z archiwum przed przekazaniem ich do indeksu.

**Q: Jaki jest najlepszy sposób, aby utrzymać indeks aktualny przy ciągle generowanych dziennikach?**  
A: Włącz `autoReindex` i zaplanuj obserwatora w tle, który wywołuje `index.add(newLogFile)` za każdym razem, gdy pojawi się nowy plik.

**Q: Czy istnieje limit rozmiaru pojedynczego pliku dziennika, który można indeksować?**  
A: Praktycznie limit zależy od dostępnej pamięci. Zaleca się podzielenie bardzo dużych dzienników na mniejsze fragmenty przed indeksowaniem.

**Q: Czy GroupDocs.Search obsługuje wyszukiwania rozmyte lub z użyciem znaków wieloznacznych?**  
A: Tak, API wyszukiwania zawiera dopasowanie rozmyte, znaki wieloznaczne oraz zapytania zbliżeniowe, aby poprawić trafność wyników.

---

**Last Updated:** 2026-08-05  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Powiązane samouczki

- [Java Pełnotekstowe Wyszukiwanie: Tworzenie indeksu z GroupDocs.Search](/search/java/dictionaries-language-processing/master-alphabet-dictionary-indexing-groupdocs-search-java/)
- [Jak dodać dokumenty do indeksu z GroupDocs.Search dla Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Popraw wydajność zapytań z GroupDocs.Search Java: Optymalizacja indeksu i wyszukiwania](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)