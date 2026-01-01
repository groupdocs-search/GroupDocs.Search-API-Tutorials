---
date: '2025-12-18'
description: Dowiedz się, jak wdrożyć niestandardowy format dat w wyszukiwaniach Java
  przy użyciu GroupDocs.Search, w tym zapytania zakresu dat, własne wzorce i wskazówki
  dotyczące wydajności.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: 'Niestandardowy format daty w Javie | wyszukiwanie zakresu dat z GroupDocs'
type: docs
url: /pl/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Custom Date Format Java | Date Range Search with GroupDocs

Wyszukiwanie dokumentów według daty jest częstym wymaganiem — niezależnie od tego, czy tworzysz system archiwizacji, narzędzie do raportowania finansowego, czy portal zarządzania treścią. W tym samouczku poznasz techniki **custom date format java** przy użyciu GroupDocs.Search, obejmujące zapytania zakresu dat, definicje własnych wzorców oraz wskazówki, jak **optimize search performance**. Po zakończeniu będziesz mógł umożliwić użytkownikom pobieranie rekordów mieszczących się w dowolnym przedziale dat, niezależnie od używanego formatu.

## Szybkie odpowiedzi
- **Jaka jest podstawowa klasa do indeksowania?** `Index` from the `com.groupdocs.search` package.  
- **Jak zdefiniować własny wzorzec daty?** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **Czy mogę wyszukiwać przy użyciu zapytania tekstowego?** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **Jakie współrzędne Maven są wymagane?** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **Czy potrzebuję licencji do rozwoju?** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## Co to jest **custom date format java**?
**custom date format java** informuje GroupDocs.Search, jak interpretować ciągi dat, które nie podążają za domyślnym wzorcem ISO (YYYY‑MM‑DD). Definiując własny wzorzec — na przykład `MM/dd/yyyy` lub `dd‑MM‑yyyy` — umożliwiasz silnikowi rozpoznawanie dat osadzonych w dokumentach używających regionalnych lub starszych formatów.

## Dlaczego używać GroupDocs.Search do zapytań zakresu dat?
- **Speed:** Wbudowane indeksowanie zapewnia wyszukiwania O(log n).  
- **Flexibility:** Obsługuje zarówno tworzenie zapytań tekstowych, jak i obiektowych.  
- **Multi‑format support:** Obsługuje PDF‑y, Word, Excel, zwykły tekst i inne bez dodatkowego kodu.  

## Jak **search documents by date** z GroupDocs.Search
Poniżej znajdziesz przewodnik krok po kroku, który przeprowadzi Cię przez konfigurację biblioteki, indeksowanie plików oraz wykonywanie zarówno prostych, jak i zaawansowanych wyszukiwań zakresu dat.

### Wymagania wstępne
- Java 8 lub nowszy zainstalowany.  
- Maven do zarządzania zależnościami.  
- Dostęp do licencji GroupDocs.Search (wersja próbna lub tymczasowa działa w fazie rozwoju).  

### Konfiguracja GroupDocs.Search dla Java

#### Instalacja przy użyciu Maven
Dodaj repozytorium i zależność do swojego `pom.xml`:

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
Alternatywnie możesz pobrać najnowszą wersję bezpośrednio z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Podstawowa inicjalizacja i konfiguracja
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## Funkcja 1: Tworzenie zapytań wyszukiwania zakresu dat

### Użycie zapytania w formie tekstowej
The simplest way is to embed the date range directly in the query string:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Explanation**: Składnia `daterange` oczekuje dat w formacie `YYYY‑MM‑DD`. Zwraca wszystkie dokumenty, których zindeksowane daty mieszczą się w podanym przedziale.

### Użycie obiektu zapytania
For programmatic control and custom parsing, build a `SearchQuery` object:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Explanation**: `createDateRangeQuery` pozwala podać obiekty `java.util.Date`, dając pełną elastyczność w zakresie stref czasowych i obsługi specyficznej dla lokalizacji.

## Funkcja 2: Określanie wzorców **custom date format java**

### Ustawianie własnych formatów dat
Define a `DateFormat` that matches your document’s date representation:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Explanation**: Po wyczyszczeniu domyślnych formatów i dodaniu `DateFormat` używającego `/` jako separatora, silnik rozumie daty zapisane jako `MM/dd/yyyy`. Jest to niezbędne do **search documents by date** w regionach, które preferują notację miesiąc‑dzień‑rok.

## Wskazówki, jak **optimize search performance**
- **Index Incrementally**: Dodawaj nowe pliki do istniejącego indeksu zamiast przebudowywać go od zera.  
- **Prune Stale Data**: Okresowo usuwaj dokumenty, które nie są już potrzebne.  
- **Adjust Memory Settings**: Zwiększ przydział pamięci JVM (`-Xmx`) przy pracy z dużymi indeksami.  

## Częste problemy i rozwiązania
- **Date Parsing Errors**: Sprawdź, czy ciągi dat w dokumencie dokładnie pasują do zdefiniowanego własnego wzorca.  
- **Missing Results**: Upewnij się, że zindeksowane pola zawierają metadane dat; w przeciwnym razie silnik nie będzie mógł dopasować zapytań datowych.  
- **Index Access Exceptions**: Potwierdź, że ścieżka `indexFolder` jest zapisywalna i nie jest zablokowana przez inny proces.  

## Praktyczne zastosowania
1. **Archival Systems** – Pobieranie rekordów z określonego okresu historycznego.  
2. **Content Management** – Obsługa regionalnych formatów dat, takich jak `dd/MM/yyyy`, dla europejskich odbiorców.  
3. **Financial Software** – Szybkie filtrowanie transakcji według kwartału fiskalnego lub roku.  

## Zakończenie
Masz teraz kompletny zestaw narzędzi **custom date format java** do budowania potężnych wyszukiwań zakresu dat z GroupDocs.Search. Zaimplementuj te wzorce, dopracuj wydajność, a Twoja aplikacja dostarczy szybkie i dokładne wyniki dla dowolnego zapytania czasowego.

## Najczęściej zadawane pytania

**Q: What is the difference between text form and object‑based date queries?**  
A: Forma tekstowa jest szybka i prosta, ale ograniczona do domyślnego formatu ISO; zapytania oparte na obiektach pozwalają podać obiekty `Date` i własne formaty, zapewniając większą elastyczność.

**Q: Can I search for multiple date ranges in a single query?**  
A: Tak, połącz klauzule `daterange` przy użyciu operatorów logicznych takich jak `AND` lub `OR`, aby zbudować złożone zapytania.

**Q: Will custom date formats slow down the search?**  
A: Istnieje niewielki narzut związany z dodatkowymi operacjami parsowania, ale wpływ jest pomijalny przy typowych obciążeniach i jest rekompensowany przez zwiększoną dokładność.

**Q: Is GroupDocs.Search suitable for large‑scale deployments?**  
A: Zdecydowanie tak. Przy odpowiednich strategiach indeksowania i dostrojeniu JVM, skaluje się do milionów dokumentów.

**Q: Where can I find more Java examples?**  
A: Przeglądaj [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) w poszukiwaniu dodatkowych przykładów i implementacji przypadków użycia.

---

**Resources**
- **Documentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [Get the latest version here](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum**: [Join the discussion](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)  

---

**Ostatnia aktualizacja:** 2025-12-18  
**Testowano z:** GroupDocs.Search Java 25.4  
**Autor:** GroupDocs