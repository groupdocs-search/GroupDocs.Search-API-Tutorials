---
date: '2026-09-06'
description: Dowiedz się, jak filtrować rozszerzenia plików java przy użyciu GroupDocs.Search
  dla Javy, obejmując operatory logiczne AND, OR, NOT, filtry zakresu dat oraz filtry
  ścieżki.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: Filtrowanie rozszerzeń plików java przy użyciu GroupDocs.Search. Dowiedz
  się, jak łączyć filtry rozszerzeń, zakresu dat i ścieżki przy użyciu operatorów
  logicznych w Javie.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: Filtrowanie rozszerzeń plików java za pomocą GroupDocs.Search – Kompletny
  przewodnik
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: Jak filtrować rozszerzenia plików java za pomocą GroupDocs.Search
type: docs
url: /pl/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Filtrowanie rozszerzeń plików java w GroupDocs.Search

W tym obszernej poradniku dowiesz się, jak **filtrować rozszerzenia plików java** podczas indeksowania dokumentów przy użyciu GroupDocs.Search. Po zakończeniu przewodnika będziesz mógł uwzględniać tylko potrzebne typy plików, wykluczać niechciane formaty oraz łączyć te reguły z filtrami zakresu dat i ścieżek przy użyciu operatorów logicznych AND, OR i NOT. Takie podejście utrzymuje indeks lekki, przyspiesza wyszukiwania i pomaga zachować zgodność z zasadami przetwarzania danych.

## Szybkie odpowiedzi
- **Czym jest filtr rozszerzeń plików java?** Jest to reguła, która informuje GroupDocs.Search, które rozszerzenia plików mają być uwzględniane lub wykluczane podczas indeksowania.  
- **Która biblioteka zapewnia tę funkcję?** GroupDocs.Search for Java.  
- **Czy potrzebuję licencji?** Darmowa wersja próbna wystarcza do oceny; pełna licencja jest wymagana w środowisku produkcyjnym.  
- **Czy mogę łączyć filtry?** Tak – możesz łączyć filtry rozszerzeń, dat, rozmiaru i ścieżek przy użyciu logiki AND, OR, NOT.  
- **Czy jest kompatybilny z Maven?** Zdecydowanie – dodaj zależność GroupDocs.Search do swojego `pom.xml`.

## Czym jest filtr rozszerzeń plików java?
**Filtr rozszerzeń plików java** to zestaw reguł, który ocenia rozszerzenie każdego pliku przed jego przekazaniem do silnika indeksującego. Określając rozszerzenia takie jak `.txt`, `.pdf` lub `.epub`, możesz **uwzględniać pliki według rozszerzenia** lub **wykluczać pliki według rozszerzenia**, aby utrzymać indeks skoncentrowany i wyniki wyszukiwania istotne.

## Dlaczego używać filtrowania rozszerzeń plików z GroupDocs.Search?
Filtrowanie rozszerzeń plików poprawia wydajność indeksowania poprzez wykluczanie nieistotnych formatów, zmniejsza wymagania dotyczące przechowywania i pomaga spełniać zasady zgodności, zapobiegając wprowadzaniu niechcianych treści do indeksu. Umożliwia także szybsze odpowiedzi na zapytania, ponieważ silnik wyszukiwania przetwarza mniejszy, bardziej istotny zestaw danych.

- **Performance:** Pomijanie niechcianych plików zmniejsza operacje I/O i przyspiesza indeksowanie nawet o 40 % w dużych repozytoriach.  
- **Storage savings:** Tylko istotne dokumenty są przechowywane w indeksie, co zmniejsza zużycie dysku średnio o 30 %.  
- **Compliance:** Zapobiega przypadkowemu indeksowaniu poufnych lub nieobsługiwanych typów plików.  
- **Flexibility:** Łącz z funkcjami **date range filter java**, aby celować w pliki utworzone lub zmodyfikowane w określonych okresach.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz następujące:

### Wymagane biblioteki i zależności
- **GroupDocs.Search for Java** – wersja 25.4 lub późniejsza (obsługuje ponad 60 formatów wejściowych).  
- **Java Development Kit (JDK)** – dowolna kompatybilna wersja (8 lub nowsza).

### Konfiguracja środowiska
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse lub dowolne środowisko IDE kompatybilne z Maven.

### Wymagania wiedzy
- Podstawowa programowanie w Javie.  
- Znajomość operacji I/O na plikach w Javie.  
- Zrozumienie wyrażeń regularnych oraz obsługi dat i czasu.

## Konfigurowanie GroupDocs.Search dla Java
Aby rozpocząć korzystanie z GroupDocs.Search, musisz dodać go jako zależność w swoim projekcie.

### Konfiguracja Maven
Dodaj poniższą konfigurację repozytorium i zależności do pliku `pom.xml`:

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

### Bezpośrednie pobranie
Alternatywnie, pobierz najnowszą wersję bezpośrednio z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Uzyskanie licencji
1. **Free trial** – przetestuj funkcje bez kosztów.  
2. **Temporary license** – uzyskaj pełną funkcjonalność na ograniczony czas.  
3. **Purchase** – zdobądź stałą licencję do użytku produkcyjnego.

### Podstawowa inicjalizacja i konfiguracja
Po dodaniu biblioteki, zainicjalizuj środowisko indeksowania. Klasa `IndexSettings` zawiera wszystkie opcje konfiguracji, w tym filtry.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Przewodnik implementacji
Poniżej zagłębiamy się w każdy typ filtru, wyjaśniając **dlaczego ma to znaczenie** i podając instrukcje krok po kroku, które możesz skopiować do swojego projektu.

### Filtrowanie rozszerzeń plików
Filtruj pliki według ich rozszerzeń podczas indeksowania. To idealne rozwiązanie, gdy chcesz przetwarzać jedynie e‑książki (`.fb2`, `.epub`) oraz pliki tekstowe (`.txt`).

#### Przegląd
`DocumentFilter.createFileExtension` tworzy białą listę rozszerzeń.

#### Kroki implementacji
1. **Create filter** – określ rozszerzenia, które chcesz zachować.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize index and add documents** – zastosuj filtr przy tworzeniu `IndexSettings`.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtr logiczny NOT
Wyklucz określone rozszerzenia, takie jak strony internetowe i pliki PDF, gdy nie są potrzebne w twoim scenariuszu wyszukiwania.

#### Kroki implementacji
1. **Create exclusion filter** – określ rozszerzenia do odrzucenia.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to index settings** – połącz filtr NOT z innymi regułami.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add documents** – indeksowane są tylko pliki, które przejdą połączony filtr.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtr logiczny AND
Połącz kilka warunków — datę utworzenia, rozszerzenie i rozmiar pliku — tak aby **tylko pliki spełniające wszystkie kryteria** były indeksowane.

#### Przegląd
`DocumentFilter.createAnd` łączy wiele filtrów w jedną regułę.

#### Kroki implementacji
1. **Define filters** – utwórz osobne filtry dla każdego warunku.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine filters** – użyj operatora AND, aby wymagać spełnienia wszystkich warunków.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index documents** – przekaż połączony filtr do potoku indeksowania.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtr logiczny OR
Uwzględnij pliki, które spełniają **dowolny** z określonych warunków — przydatne, gdy chcesz objąć zarówno małe pliki tekstowe, jak i większe pliki nienależące do tekstu.

#### Kroki implementacji
1. **Define filters** – utwórz oddzielne filtry dla każdej alternatywnej sytuacji.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine filters with logical conditions** – użyj operatora OR.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR filter** – dołącz połączony filtr do konfiguracji indeksu.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtry czasu utworzenia
Celuj w pliki utworzone w określonym przedziale czasu — klasyczny scenariusz **date range filter java**.

#### Kroki implementacji
1. **Define date‑range filter** – określ daty początkową i końcową.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index documents** – indeksowane są tylko pliki, których znaczniki czasu utworzenia mieszczą się w podanym przedziale.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtry czasu modyfikacji
Wyklucz pliki, które zostały zmodyfikowane po określonej dacie granicznej.

#### Kroki implementacji
1. **Define filter** – ustaw maksymalny znacznik czasu modyfikacji.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index documents** – pliki nowsze niż data graniczna są pomijane.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtrowanie ścieżki pliku
Ogranicz indeksowanie do plików znajdujących się w określonych folderach lub pasujących do wzorca — idealne dla **include files by extension** w konkretnej hierarchii katalogów.

#### Kroki implementacji
1. **Define file‑path filter** – użyj wzorców glob lub regex do dopasowania katalogów.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize index and add documents** – zastosuj filtr ścieżki razem z innymi regułami.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Częste pułapki i wskazówki
- **Nigdy nie mieszaj ścieżek bezwzględnych i względnych** w tej samej konfiguracji filtru – może to prowadzić do nieoczekiwanych wykluczeń.  
- **Reset the `IndexSettings`** przy zmianie zestawów filtrów; w przeciwnym razie poprzednie filtry mogą pozostać.  
- **Combine a length upper bound with an extension filter** dla dużych kolekcji, aby utrzymać niskie zużycie pamięci.  
- **LoggingOptions** kontroluje konfigurację logowania dla GroupDocs.Search.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) aby zobaczyć, dlaczego plik został odrzucony.  

## Najczęściej zadawane pytania

**Q: Czy mogę zmienić kryteria filtru po utworzeniu indeksu?**  
A: Tak. Przebuduj indeks z nowym `DocumentFilter` lub użyj indeksowania przyrostowego z zaktualizowanymi ustawieniami.

**Q: Czy filtr rozszerzeń plików java działa na skompresowanych archiwach (np. ZIP)?**  
A: GroupDocs.Search może indeksować obsługiwane formaty archiwów, ale filtr rozszerzeń odnosi się do samego archiwum, a nie do plików wewnątrz. Użyj zagnieżdżonych filtrów, aby uzyskać głębszą kontrolę.

**Q: Jak debugować, dlaczego konkretny plik został wykluczony?**  
A: Włącz logowanie biblioteki (`LoggingOptions.setEnabled(true)`) i przejrzyj log – informuje, który filtr odrzucił każdy plik.

**Q: Czy można połączyć filtr rozszerzeń plików java z własnymi filtrami regex?**  
A: Zdecydowanie. Umieść filtr regex wewnątrz `DocumentFilter.createAnd()` razem z filtrem rozszerzeń.

**Q: Jaki wpływ na wydajność ma dodanie wielu filtrów?**  
A: Każdy filtr wprowadza niewielki narzut podczas indeksowania, ale redukcja danych w indeksie zazwyczaj przewyższa koszt. Przetestuj na reprezentatywnej próbce, aby znaleźć optymalny balans.

---

**Ostatnia aktualizacja:** 2026-09-06  
**Testowano z:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Powiązane tutoriale

- [Niestandardowy format daty Java | Wyszukiwanie zakresu dat z GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean i or: Mistrzowskie wyszukiwania logiczne z GroupDocs.Search dla Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Optymalizacja wydajności wyszukiwania dzięki zaawansowanym technikom indeksowania w GroupDocs.Search dla Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}