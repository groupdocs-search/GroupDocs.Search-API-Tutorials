---
date: '2026-02-21'
description: Dowiedz się, jak zaimplementować filtr rozszerzeń plików Java przy użyciu
  GroupDocs.Search dla Javy, obejmujący operatory logiczne, daty utworzenia/modyfikacji
  oraz filtry ścieżek.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: Filtr rozszerzeń plików Java z GroupDocs.Search – przewodnik
type: docs
url: /pl/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

 is "---". Keep as is.

Then "**Last Updated:** 2026-02-21" -> "**Last Updated:** 2026-02-21" (date unchanged)

"**Tested With:** GroupDocs.Search 25.4 for Java" -> "**Tested With:** GroupDocs.Search 25.4 for Java"

"**Author:** GroupDocs" -> "**Author:** GroupDocs"

Then final "---"? Already there.

Make sure all markdown formatting preserved.

Now produce final content.# Opanowanie filtru rozszerzeń plików java w GroupDocs.Search

Zarządzanie rosnącym repozytorium dokumentów może szybko stać się przytłaczające, szczególnie gdy trzeba indeksować tylko określone typy plików. **The java file extension filter** pozwala powiedzieć GroupDocs.Search dokładnie, które rozszerzenia uwzględnić lub wykluczyć, dając precyzyjną kontrolę nad potokiem indeksowania. W tym przewodniku przeprowadzimy konfigurację GroupDocs.Search dla Javy i pokażemy, jak łączyć filtrowanie rozszerzeń plików z operatorami logicznymi AND, OR i NOT, a także z filtrami zakresu dat i ścieżek.

## Szybkie odpowiedzi
- **What is the java file extension filter?** Konfiguracja, która informuje GroupDocs.Search, które rozszerzenia plików uwzględnić lub wykluczyć podczas indeksowania.  
- **Which library provides this feature?** GroupDocs.Search for Java.  
- **Do I need a license?** Darmowa wersja próbna działa w ocenie; pełna licencja jest wymagana w produkcji.  
- **Can I combine filters?** Tak – możesz łączyć filtry rozszerzeń, dat, rozmiaru i ścieżek przy użyciu logiki AND, OR, NOT.  
- **Is it Maven‑compatible?** Absolutnie – dodaj zależność GroupDocs.Search do swojego `pom.xml`.

## Co to jest java file extension filter?
**java file extension filter** to zestaw reguł, który ocenia rozszerzenie każdego pliku przed jego przekazaniem do silnika indeksującego. Określając rozszerzenia takie jak `.txt`, `.pdf` lub `.epub`, możesz **include files by extension** lub **exclude files by extension**, aby utrzymać indeks skupiony i wyniki wyszukiwania istotne.

## Dlaczego używać filtrowania rozszerzeń plików z GroupDocs.Search?
- **Performance:** Pomijanie niepotrzebnych plików zmniejsza I/O i przyspiesza indeksowanie.  
- **Storage savings:** Tylko istotne dokumenty są przechowywane w indeksie, co zmniejsza zużycie dysku.  
- **Compliance:** Zapobiega przypadkowemu indeksowaniu poufnych lub nieobsługiwanych typów plików.  
- **Flexibility:** Połącz z funkcjami **date range filter java**, aby celować w pliki utworzone lub zmodyfikowane w określonych okresach.

## Prerequisites

Zanim zaczniemy, upewnij się, że masz następujące elementy:

### Required Libraries and Dependencies
- **GroupDocs.Search for Java**: Wersja 25.4 lub nowsza  
- **Java Development Kit (JDK)**: Zainstalowana kompatybilna wersja  

### Environment Setup
- Zintegrowane środowisko programistyczne (IDE): IntelliJ IDEA, Eclipse lub dowolne IDE kompatybilne z Maven.

### Knowledge Prerequisites
- Podstawowe programowanie w Javie  
- Znajomość operacji I/O na plikach w Javie  
- Zrozumienie wyrażeń regularnych i obsługi dat/czasu  

## Setting Up GroupDocs.Search for Java
Aby rozpocząć korzystanie z GroupDocs.Search, musisz dodać go jako zależność w swoim projekcie.

### Maven Configuration
Dodaj następującą konfigurację repozytorium i zależności do pliku `pom.xml`:

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

### Direct Download
Alternatywnie, pobierz najnowszą wersję bezpośrednio z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### License Acquisition
1. **Free Trial** – przetestuj funkcje bez kosztów.  
2. **Temporary License** – uzyskaj pełną funkcjonalność na ograniczony czas.  
3. **Purchase** – zdobądź stałą licencję do użytku produkcyjnego.  

### Basic Initialization and Setup
Po dodaniu biblioteki, zainicjalizuj środowisko indeksowania:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Przewodnik implementacji
Poniżej zagłębiamy się w każdy typ filtru, wyjaśniając **why it matters** i dostarczając kod krok po kroku, który możesz skopiować do swojego projektu.

### File Extension Filtering
Filtruj pliki według ich rozszerzeń podczas indeksowania. To idealne rozwiązanie, gdy chcesz przetwarzać tylko e‑książki (`.fb2`, `.epub`) oraz pliki tekstowe (`.txt`).

#### Overview
Użyj `DocumentFilter.createFileExtension`, aby utworzyć białą listę rozszerzeń.

#### Implementation Steps
1. **Create Filter**:

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logical NOT Filter
Wyklucz określone rozszerzenia, takie jak strony internetowe i PDF, gdy nie są potrzebne w twoim scenariuszu wyszukiwania.

#### Implementation Steps
1. **Create Exclusion Filter**:

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to Index Settings**:

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add Documents**:

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logical AND Filter
Połącz kilka warunków — datę utworzenia, rozszerzenie i rozmiar pliku — tak, aby **only files that meet all criteria** były indeksowane.

#### Overview
`DocumentFilter.createAnd` łączy wiele filtrów w jedną regułę.

#### Implementation Steps
1. **Define Filters**:

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine Filters**:

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index Documents**:

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logical OR Filter
Uwzględnij pliki, które spełniają **any** z określonych warunków — przydatne, gdy chcesz objąć zarówno małe pliki tekstowe, jak i większe pliki nienależące do tekstu.

#### Implementation Steps
1. **Define Filters**:

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine Filters with Logical Conditions**:

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR Filter**:

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Creation Time Filters
Celuj w pliki utworzone w określonym okresie — klasyczny scenariusz **date range filter java**.

#### Implementation Steps
1. **Define Date Range Filter**:

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index Documents**:

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Modification Time Filters
Wyklucz pliki, które zostały zmodyfikowane po określonej dacie granicznej.

#### Implementation Steps
1. **Define Filter**:

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index Documents**:

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### File Path Filtering
Ogranicz indeksowanie do plików znajdujących się w określonych folderach lub pasujących do wzorca — idealne dla **include files by extension** w konkretnej hierarchii katalogów.

#### Implementation Steps
1. **Define File Path Filter**:

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Common Pitfalls & Tips

- **Never mix absolute and relative paths** w tej samej konfiguracji filtru – może to prowadzić do nieoczekiwanych wykluczeń.  
- **Reset the `IndexSettings`** przy przełączaniu zestawów filtrów; w przeciwnym razie poprzednie filtry mogą pozostać.  
- **Combine a length upper bound with an extension filter** dla dużych kolekcji, aby utrzymać niskie zużycie pamięci.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) aby zobaczyć, dlaczego plik został odrzucony.  

## Frequently Asked Questions

**Q: Czy mogę zmienić kryteria filtru po utworzeniu indeksu?**  
A: Tak. Przebuduj indeks z nowym `DocumentFilter` lub użyj indeksowania przyrostowego z zaktualizowanymi ustawieniami.

**Q: Czy filtr rozszerzeń plików java działa na skompresowanych archiwach (np. ZIP)?**  
A: GroupDocs.Search może indeksować obsługiwane formaty archiwów, ale filtr rozszerzeń dotyczy samego archiwum, a nie plików wewnątrz. Użyj zagnieżdżonych filtrów dla głębszej kontroli.

**Q: Jak debugować, dlaczego konkretny plik został wykluczony?**  
A: Włącz logowanie biblioteki (`LoggingOptions.setEnabled(true)`) i przejrzyj log – raportuje, który filtr odrzucił każdy plik.

**Q: Czy można połączyć filtr rozszerzeń plików java z własnymi filtrami regex?**  
A: Absolutnie. Owiń filtr regex wewnątrz `DocumentFilter.createAnd()` razem z filtrem rozszerzeń.

**Q: Jaki wpływ na wydajność ma dodanie wielu filtrów?**  
A: Każdy filtr dodaje niewielki narzut podczas indeksowania, ale redukcja danych indeksowanych zazwyczaj przewyższa koszt. Przetestuj na reprezentatywnej próbce, aby znaleźć optymalny balans.

---

**Last Updated:** 2026-02-21  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---