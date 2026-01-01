---
date: '2025-12-19'
description: Dowiedz się, jak zaimplementować filtr rozszerzeń plików Java przy użyciu
  GroupDocs.Search dla Javy, obejmujący operatory logiczne, daty utworzenia/modyfikacji
  oraz filtry ścieżek.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: Filtr rozszerzeń plików Java z GroupDocs.Search – Poradnik
type: docs
url: /pl/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Opanowanie filtru rozszerzenia plików java w GroupDocs.Search

Zarządzanie rosnącym repozytorium dokumentów może szybko stać się przytłaczające. Niezależnie od tego, czy musisz indeksować tylko określone typy dokumentów, czy wykluczyć nieistotne pliki, **java file extension filter** zapewnia precyzyjną kontrolę nad tym, co jest przetwarzane. W tym przewodniku pokażemy, jak skonfigurować GroupDocs.Search dla Java oraz jak łączyć filtrowanie rozszerzeń plików z operatorami logicznymi AND, OR i NOT, a także z filtrami zakresu dat i ścieżek.

## Szybkie odpowiedzi
- **Czym jest java file extension filter?** Konfiguracja, która informuje GroupDocs.Search, które rozszerzenia plików mają być uwzględnione lub wykluczone podczas indeksowania.  
- **Która biblioteka zapewnia tę funkcję?** GroupDocs.Search for Java.  
- **Czy potrzebuję licencji?** Tak. Darmowa wersja próbna działa do oceny; pełna licencja jest wymagana w środowisku produkcyjnym.  
- **Czy mogę łączyć filtry?** Tak – możesz łączyć filtry rozszerzeń, dat, rozmiaru i ścieżek przy użyciu logiki AND, OR, NOT.  
- **Czy jest kompatybilny z Maven?** Oczywiście – dodaj zależność GroupDocs.Search do swojego `pom.xml`.

## Wprowadzenie

Masz problem z efektywnym zarządzaniem rosnącym repozytorium plików? Niezależnie od tego, czy musisz organizować dokumenty według typu, czy odfiltrować niepotrzebne pliki podczas indeksowania, zadanie może być przytłaczające bez odpowiednich narzędzi. **GroupDocs.Search for Java** to zaawansowana biblioteka wyszukiwania, która upraszcza te wyzwania dzięki potężnym możliwościom filtrowania plików. Ten samouczek poprowadzi Cię przez implementację technik filtrowania plików .NET przy użyciu GroupDocs.Search, koncentrując się na filtrach logicznych AND, OR i NOT.

### Czego się nauczysz
- Konfigurowanie GroupDocs.Search w środowisku Java  
- Implementacja różnych filtrów: rozszerzenie pliku, operatory logiczne (AND, OR, NOT), czas utworzenia, czas modyfikacji, ścieżka pliku i długość  
- Praktyczne zastosowania tych filtrów w efektywnym zarządzaniu dokumentami  
- Wskazówki optymalizacji wydajności dla dużych zadań indeksowania  

Gotowy, aby odblokować pełny potencjał filtrowania plików w Java? Zanurzmy się najpierw w wymagania wstępne.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz następujące:

### Wymagane biblioteki i zależności
- **GroupDocs.Search for Java**: Version 25.4 or later  
- **Java Development Kit (JDK)**: Upewnij się, że masz zainstalowaną kompatybilną wersję na swoim systemie  

### Konfiguracja środowiska
- Zintegrowane środowisko programistyczne (IDE): Użyj IntelliJ IDEA, Eclipse lub dowolnego preferowanego IDE obsługującego projekty Maven.

### Wymagania wiedzy
- Podstawowa znajomość programowania w języku Java  
- Znajomość operacji I/O na plikach w Java  
- Zrozumienie wyrażeń regularnych i manipulacji datą‑czasem  

## Konfiguracja GroupDocs.Search dla Java
Aby rozpocząć korzystanie z GroupDocs.Search, musisz dodać go jako zależność w swoim projekcie. Oto jak:

### Konfiguracja Maven
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

### Bezpośrednie pobranie
Alternatywnie, pobierz najnowszą wersję bezpośrednio z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Uzyskanie licencji
1. **Free Trial**: Rozpocznij od darmowej wersji próbnej, aby poznać funkcje GroupDocs.Search.  
2. **Temporary License**: Złóż wniosek o tymczasową licencję, aby uzyskać pełną funkcjonalność bez ograniczeń.  
3. **Purchase**: W przypadku długoterminowego użytkowania zakup subskrypcję.  

### Podstawowa inicjalizacja i konfiguracja
Po dodaniu biblioteki, zainicjalizuj środowisko indeksowania:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Przewodnik implementacji
Teraz przyjrzyjmy się, jak zaimplementować różne funkcje filtrowania plików przy użyciu GroupDocs.Search.

### Filtrowanie rozszerzeń plików
Filtruj pliki według ich rozszerzeń podczas indeksowania. Ta funkcja jest przydatna do przetwarzania tylko określonych typów dokumentów, takich jak FB2, EPUB i TXT.

#### Przegląd
Filtruj dokumenty na podstawie rozszerzenia pliku przy użyciu własnej konfiguracji filtru.

#### Kroki implementacji
1. **Utwórz filtr**:
    
    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Zainicjalizuj indeks i dodaj dokumenty**:
    
    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtrowanie logiczne NOT
Wyklucz określone rozszerzenia plików podczas indeksowania, takie jak HTM, HTML i PDF.

#### Kroki implementacji
1. **Utwórz filtr wykluczający**:
    
    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Zastosuj do ustawień indeksu**:
    
    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Dodaj dokumenty**:
    
    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtrowanie logiczne AND
Połącz wiele kryteriów, aby uwzględnić tylko pliki spełniające wszystkie określone warunki.

#### Przegląd
Użyj operacji logicznego AND, aby filtrować pliki na podstawie czasu utworzenia, rozszerzenia pliku i długości.

#### Kroki implementacji
1. **Zdefiniuj filtry**:
    
    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Połącz filtry**:
    
    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Indeksuj dokumenty**:
    
    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtrowanie logiczne OR
Uwzględnij pliki spełniające dowolne z określonych kryteriów, używając operacji logicznego OR.

#### Kroki implementacji
1. **Zdefiniuj filtry**:
    
    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Połącz filtry z warunkami logicznymi**:
    
    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Zakończ filtr OR**:
    
    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtry czasu utworzenia
Filtruj pliki na podstawie ich czasu utworzenia, aby uwzględnić tylko te mieszczące się w określonym przedziale dat.

#### Kroki implementacji
1. **Zdefiniuj filtr zakresu dat**:
    
    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Indeksuj dokumenty**:
    
    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtry czasu modyfikacji
Wyklucz pliki zmodyfikowane po określonej dacie.

#### Kroki implementacji
1. **Zdefiniuj filtr**:
    
    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Indeksuj dokumenty**:
    
    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtrowanie ścieżki pliku
Filtruj pliki na podstawie ich ścieżek, aby uwzględnić tylko te znajdujące się w określonych katalogach.

#### Kroki implementacji
1. **Zdefiniuj filtr ścieżki pliku**:
    
    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Zainicjalizuj indeks i dodaj dokumenty**:
    
    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Częste pułapki i wskazówki
- **Nigdy nie mieszaj ścieżek bezwzględnych i względnych** w tej samej konfiguracji filtru – może to prowadzić do nieoczekiwanych wykluczeń.  
- **Pamiętaj, aby zresetować `IndexSettings`** przy przełączaniu z jednego zestawu filtrów na inny; w przeciwnym razie poprzednie filtry mogą pozostać.  
- **Duże kolekcje plików** korzystają z łączenia górnego limitu długości z filtrem rozszerzenia, aby utrzymać niskie zużycie pamięci.  

## Najczęściej zadawane pytania

**Q: Czy mogę zmienić kryteria filtru po utworzeniu indeksu?**  
A: Tak. Możesz odbudować indeks z nowym `DocumentFilter` lub użyć indeksowania przyrostowego z zaktualizowanymi ustawieniami.

**Q: Czy filtr rozszerzenia plików java działa na skompresowanych archiwach (np. ZIP)?**  
A: GroupDocs.Search może indeksować obsługiwane formaty archiwów, ale filtr rozszerzenia odnosi się do samego archiwum, a nie do plików wewnętrznych. W razie potrzeby użyj zagnieżdżonych filtrów.

**Q: Jak mogę debugować, dlaczego konkretny plik został wykluczony?**  
A: Włącz logowanie biblioteki (ustaw `LoggingOptions.setEnabled(true)`) i przeanalizuj wygenerowany log – raportuje, który filtr odrzucił dany plik.

**Q: Czy można połączyć filtr rozszerzenia plików java z własnymi filtrami regex?**  
A: Absolutnie. Możesz opakować filtr regex wewnątrz `DocumentFilter.createAnd()` razem z filtrem rozszerzenia.

**Q: Jaki wpływ na wydajność ma dodanie wielu filtrów?**  
A: Każdy dodatkowy filtr wprowadza niewielki narzut podczas indeksowania, ale korzyść z mniejszego rozmiaru indeksu zazwyczaj przewyższa koszty. Przetestuj na próbce, aby znaleźć optymalny balans.

---

**Ostatnia aktualizacja:** 2025-12-19  
**Testowano z:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs