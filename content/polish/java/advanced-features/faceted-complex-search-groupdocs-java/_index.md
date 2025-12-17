---
date: '2025-12-16'
description: Naucz się tworzyć indeksy wyszukiwania w Javie i implementować wyszukiwania
  fasetowe oraz złożone przy użyciu GroupDocs.Search, zwiększając wydajność wyszukiwania
  i doświadczenie użytkownika.
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: Utwórz indeks wyszukiwania w Javie – Wyszukiwania fasetowe i złożone
type: docs
url: /pl/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Utwórz indeks wyszukiwania Java – Wyszukiwania fasetowane i złożone

Implementacja potężnego **search experience** w Javie może wydawać się przytłaczająca, szczególnie gdy musisz **create search index Java** projekty obsługujące duże kolekcje dokumentów. Na szczęście **GroupDocs.Search for Java** udostępnia bogate API, które pozwala budować zapytania fasetowane i złożone przy użyciu zaledwie kilku linii kodu. W tym samouczku dowiesz się, jak skonfigurować bibliotekę, **create a search index Java**, dodać dokumenty i uruchomić zarówno proste wyszukiwania fasetowane, jak i zaawansowane zapytania wielokryterialne.

## Szybkie odpowiedzi
- **What is a faceted search?** Sposób filtrowania wyników według predefiniowanych kategorii (np. typ pliku, data).  
- **How do I create a search index Java?** Zainicjalizuj obiekt `Index` wskazujący na folder i dodaj dokumenty.  
- **Can I combine multiple criteria?** Tak — użyj zapytań opartych na obiektach lub operatorów Boolean w zapytaniu tekstowym.  
- **Do I need a license?** Bezpłatna wersja próbna działa w środowisku deweloperskim; licencja komercyjna usuwa ograniczenia.  
- **Which IDE works best?** Dowolne IDE Java (IntelliJ IDEA, Eclipse, NetBeans) działa bez problemu.

## Co to jest „create search index java”?
Tworzenie indeksu wyszukiwania w Javie oznacza budowanie struktury danych umożliwiającej przeszukiwanie, która przechowuje metadane i treść dokumentów, zapewniając szybkie odnajdywanie na podstawie zapytań użytkownika. Dzięki GroupDocs.Search indeks znajduje się na dysku, może być aktualizowany przyrostowo i obsługuje zaawansowane funkcje, takie jak faceting i złożona logika Boolean.

## Dlaczego używać GroupDocs.Search do zapytań fasetowanych i złożonych?
- **Out‑of‑the‑box faceting** – filtrowanie po polach, takich jak nazwa pliku, rozmiar lub własne metadane.  
- **Rich query language** – łączenie zapytań tekstowych, frazowych i polowych przy użyciu operatorów AND/OR/NOT.  
- **Scalable performance** – indeksuje miliony dokumentów, utrzymując niskie opóźnienia wyszukiwania.  
- **Pure Java** – brak zależności natywnych, działa na każdej platformie z JDK 8+.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz następujące elementy:

- **JDK 8 or newer** zainstalowane i skonfigurowane w IDE.  
- **Maven** (lub Gradle) do zarządzania zależnościami.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Podstawową znajomość koncepcji OOP w Javie oraz struktury projektu Maven.

## Konfiguracja GroupDocs.Search dla Java

### Konfiguracja Maven
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

### Bezpośrednie pobranie
Alternatywnie pobierz najnowszy plik JAR ze strony oficjalnych wydań:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Uzyskanie licencji
Aby odblokować pełną funkcjonalność:

1. **Free trial** – idealny do rozwoju i testów.  
2. **Temporary evaluation license** – wydłuża limity wersji próbnej.  
3. **Commercial license** – usuwa wszystkie ograniczenia w środowisku produkcyjnym.

### Podstawowa inicjalizacja i konfiguracja
Poniższy fragment kodu pokazuje, jak **create a search index Java** poprzez utworzenie obiektu `Index`:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## Jak utworzyć search index java – Proste wyszukiwanie fasetowane

Wyszukiwanie fasetowane pozwala użytkownikom końcowym zawęzić wyniki, wybierając wartości z predefiniowanych kategorii (facetów). Poniżej znajdziesz krok po kroku instrukcję.

### Krok 1: Utwórz indeks
Najpierw wskaż `Index` na folder, w którym będą przechowywane pliki indeksu.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Krok 2: Dodaj dokumenty do indeksu
Powiedz GroupDocs.Search, gdzie znajdują się Twoje dokumenty źródłowe. Wszystkie obsługiwane typy plików (PDF, DOCX, TXT itp.) zostaną automatycznie zaindeksowane.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Krok 3: Wykonaj wyszukiwanie w polu Content przy użyciu zapytania tekstowego
Szybkie zapytanie tekstowe filtruje po polu `content`. Składnia `content: Pellentesque` ogranicza wyniki do dokumentów zawierających słowo *Pellentesque* w treści.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Krok 4: Wykonaj wyszukiwanie przy użyciu zapytania obiektowego
Zapytania oparte na obiektach dają precyzyjną kontrolę. Tutaj budujemy zapytanie słowne, otaczamy je zapytaniem pola i wykonujemy je.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Jak utworzyć search index java – Złożone zapytanie wyszukiwania

Złożone zapytania łączą wiele pól, operatory Boolean i wyszukiwanie frazowe. Są idealne w scenariuszach, takich jak filtry e‑commerce czy badania dokumentów prawnych.

### Krok 1: Utwórz indeks dla zapytań złożonych
Użyj tej samej struktury folderów; możesz współdzielić indeks zarówno w prostych, jak i złożonych scenariuszach.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Krok 2: Wykonaj wyszukiwanie przy użyciu zapytania tekstowego
Poniższe zapytanie wyszukuje pliki o nazwie *lorem* **and** *ipsum* **or** zawartość zawierającą jedną z dwóch dokładnych fraz.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Krok 3: Wykonaj wyszukiwanie przy użyciu zapytania obiektowego
Budowa oparta na obiektach odzwierciedla zapytanie tekstowe, ale zapewnia bezpieczeństwo typów i wsparcie IDE.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Praktyczne zastosowania wyszukiwań fasetowanych i złożonych

| Scenariusz | Jak faceting pomaga | Przykładowe zapytanie |
|------------|----------------------|-----------------------|
| **Katalog e‑commerce** | Filtrowanie po kategorii, cenie, marce | `category: Electronics AND price:[100 TO 500]` |
| **Repozytorium dokumentów prawnych** | Zawężanie po numerze sprawy, jurysdykcji | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Archiwa badawcze** | Łączenie autora, roku publikacji, słów kluczowych | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Intranet przedsiębiorstwa** | Wyszukiwanie po typie pliku i dziale | `filetype: pdf AND department: HR` |

## Typowe pułapki i rozwiązywanie problemów
- **Empty results** – Sprawdź, czy dokumenty zostały pomyślnie dodane (`index.getDocumentCount()` może pomóc).  
- **Stale index** – Po dodaniu lub usunięciu plików wywołaj `index.update()`, aby utrzymać indeks w synchronizacji.  
- **Incorrect field names** – Używaj stałych `CommonFieldNames` (`Content`, `FileName` itp.), aby uniknąć literówek.  
- **Performance bottlenecks** – W przypadku bardzo dużych kolekcji rozważ włączenie `index.setCacheSize()` lub użycie dedykowanego SSD dla folderu indeksu.

## Najczęściej zadawane pytania

**Q: Czy mogę używać GroupDocs.Search z Spring Boot?**  
A: Oczywiście. Wystarczy dodać zależność Maven, skonfigurować indeks jako bean Spring i wstrzyknąć go tam, gdzie jest potrzebny.

**Q: Czy biblioteka obsługuje własne pola metadanych?**  
A: Tak – możesz dodać pola definiowane przez użytkownika podczas indeksowania, a następnie facetingować je.

**Q: Jak duży może być indeks?**  
A: Indeks jest oparty na dysku i może obsługiwać miliony dokumentów; wystarczy zapewnić odpowiednią pojemność i monitorować ustawienia pamięci podręcznej.

**Q: Czy istnieje sposób na ranking wyników według trafności?**  
A: GroupDocs.Search automatycznie ocenia dopasowania; wynik można pobrać za pomocą `SearchResult.getDocument(i).getScore()`.

**Q: Co się stanie, jeśli zaindeksuję zaszyfrowane pliki PDF?**  
A: Podaj hasło podczas dodawania dokumentu: `index.add(filePath, password)`.

## Zakończenie

Do tej pory powinieneś czuć się pewnie **creating a search index Java** przy użyciu GroupDocs.Search, dodawać dokumenty i tworzyć zarówno proste zapytania fasetowane, jak i zaawansowane wyszukiwania Boolean. Te możliwości pozwalają dostarczać szybkie, dokładne i przyjazne dla użytkownika doświadczenia wyszukiwania w szerokim zakresie aplikacji — od platform e‑commerce po korporacyjne bazy wiedzy.

Gotowy na kolejny krok? Poznaj zaawansowane funkcje **GroupDocs.Search**, takie jak **highlighting**, **suggestions** i **real‑time indexing**, aby jeszcze bardziej wzmocnić możliwości wyszukiwania w Twojej aplikacji.

---

**Ostatnia aktualizacja:** 2025-12-16  
**Testowano z:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs