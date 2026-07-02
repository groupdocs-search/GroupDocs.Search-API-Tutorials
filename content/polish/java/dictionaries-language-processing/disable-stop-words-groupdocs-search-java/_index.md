---
date: '2026-02-19'
description: Dowiedz się, jak wyłączyć słowa stop w wyszukiwaniu i dodać dokumenty
  do indeksu za pomocą GroupDocs.Search dla Javy, zwiększając dokładność zapytań.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 'Słowa stop w wyszukiwaniu: dodawanie dokumentów do indeksu przy użyciu GroupDocs.Search
  Java'
type: docs
url: /pl/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Słowa stop w wyszukiwaniu: Dodawanie dokumentów do indeksu przy użyciu GroupDocs.Search Java

Jeśli potrzebujesz **dodawać dokumenty do indeksu**, jednocześnie upewniając się, że żadne ważne pojęcie — szczególnie te powszechne — nie jest pomijane, trafiłeś we właściwe miejsce. W tym przewodniku pokażemy, jak **wyłączyć słowa stop w wyszukiwaniu** przy użyciu GroupDocs.Search for Java, tak aby każdy token (nawet „on”, „by” lub „the”) stał się przeszukiwalny i wyniki były znacznie dokładniejsze.

## Szybkie odpowiedzi
- **Co oznacza „add documents to index”?** Oznacza to ładowanie plików źródłowych do przeszukiwalnego indeksu, aby można było je efektywnie zapytać.  
- **Dlaczego miałbym wyłączyć słowa stop?** Aby uwzględnić powszechne słowa (np. „on”, „the”) w wyszukiwaniach, gdy są one istotne dla Twojej domeny.  
- **Jakiej wersji biblioteki potrzebuję?** GroupDocs.Search for Java 25.4 lub nowsza.  
- **Czy potrzebuję licencji?** Bezpłatna wersja próbna działa do oceny; stała licencja jest wymagana w środowisku produkcyjnym.  
- **Czy mogę używać tego w projekcie Maven?** Tak — wystarczy dodać repozytorium i zależność pokazane poniżej.

## Czym są słowa stop w wyszukiwaniu i dlaczego możesz chcieć je wyłączyć?
Słowa stop to częste terminy, które wiele silników wyszukiwania automatycznie filtruje, aby przyspieszyć zapytania. Choć poprawia to wydajność w ogólnych wyszukiwaniach internetowych, może obniżać precyzję w specjalistycznych dziedzinach — umowach prawnych, katalogach e‑commerce czy podręcznikach technicznych — gdzie słowa takie jak „on”, „by” czy „as” mają rzeczywiste znaczenie. Wyłączenie słów stop pozwala traktować każde słowo jako istotne, zapewniając, że żaden istotny dokument nie zostanie pominięty.

## Jak działa dodawanie dokumentów do indeksu w GroupDocs.Search?
Gdy dodajesz dokumenty, biblioteka odczytuje każdy plik, tokenizuje jego zawartość i przechowuje tokeny w zoptymalizowanej strukturze danych (indeksie). Po zaindeksowaniu silnik może w milisekundach pobrać pasujące dokumenty, nawet w dużych zbiorach.

## Wymagania wstępne

- **Wymagane biblioteki**: GroupDocs.Search for Java 25.4 (lub nowsza).  
- **Środowisko programistyczne**: IntelliJ IDEA, Eclipse lub dowolne IDE Java, które preferujesz.  
- **Podstawowa wiedza**: Znajomość składni Java oraz koncepcji indeksowania.

## Konfiguracja GroupDocs.Search for Java

### Instalacja Maven

Jeśli używasz Maven, dodaj poniższy fragment do swojego `pom.xml`:

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

Alternatywnie pobierz najnowszą wersję z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Kroki uzyskania licencji
- **Bezpłatna wersja próbna** – rozpocznij testowanie od razu.  
- **Licencja tymczasowa** – uzyskaj klucz ograniczony czasowo, aby uzyskać pełną funkcjonalność.  
- **Zakup** – zapewnij stałą licencję do użytku produkcyjnego.

## Podstawowa inicjalizacja i konfiguracja

Utwórz instancję `IndexSettings`, aby kontrolować zachowanie indeksu:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Jak wyłączyć słowa stop w wyszukiwaniu (Java)

Poniższa linia wyłącza wbudowany filtr słów stop:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Parametry*: `setUseStopWords` przyjmuje wartość boolean.  
*Cel*: Gwarantuje, że każde słowo — w tym powszechne słowa stop — jest indeksowane i przeszukiwalne.

## Jak dodać dokumenty do indeksu

### Definiowanie katalogu wyjściowego

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Określanie katalogu dokumentów

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Teraz każdy plik w `YOUR_DOCUMENT_DIRECTORY` jest **dodawany do indeksu** i gotowy do zapytań.

## Wykonywanie zapytania wyszukiwania

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Ponieważ słowa stop są wyłączone, termin `"on"` będzie brany pod uwagę podczas wyszukiwania, zwracając dopasowania, które w przeciwnym razie zostałyby pominięte.

## Praktyczne zastosowania

1. **Enterprise Document Search** – Zapewnij, że kluczowa terminologia nie jest filtrowana.  
2. **E‑commerce Platforms** – Popraw wykrywalność produktów, indeksując każde słowo w opisach produktów.  
3. **Legal Research Tools** – Uchwyć każdy termin prawny, nawet te zwykle traktowane jako słowa stop.

## Rozważania dotyczące wydajności

- **Wskazówki optymalizacyjne**: Regularnie aktualizuj i przycinaj indeks, aby utrzymać wysoką prędkość wyszukiwania.  
- **Zużycie zasobów**: Monitoruj rozmiar sterty JVM; duże indeksy mogą wymagać dostrojenia ustawień garbage collection.  
- **Zarządzanie pamięcią w Javie**: Używaj wydajnych struktur danych i rozważ przechowywanie off‑heap dla bardzo dużych korpusów.

## Typowe problemy i rozwiązania

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---|---|---|
| Brak wyników dla powszechnych słów | `setUseStopWords(true)` (domyślnie) | Wywołaj `setUseStopWords(false)` jak pokazano powyżej. |
| Błędy Out‑of‑memory podczas indeksowania | Indeksowanie zbyt wielu dużych plików jednocześnie | Indeksuj pliki partiami; zwiększ opcję JVM `-Xmx`. |
| Wyniki wyszukiwania są nieaktualne | Indeks nie został odświeżony po dodaniu nowych plików | Wywołaj `index.update()` lub ponownie dodaj zmienione dokumenty. |

## Najczęściej zadawane pytania

**Q: Czym są słowa stop?**  
A: Słowa stop to powszechne terminy (np. „the”, „is”, „on”), które wiele silników wyszukiwania ignoruje, aby przyspieszyć zapytania. Wyłączenie ich pozwala traktować każdy token jako przeszukiwalny.

**Q: Dlaczego wyłączać słowa stop w indeksach wyszukiwania?**  
A: Gdy wymagana jest dokładna zgodność fraz — np. w dokumentach prawnych lub technicznych — każde słowo ma znaczenie, więc trzeba uwzględnić słowa stop.

**Q: Jak GroupDocs.Search radzi sobie z dużymi zestawami danych?**  
A: Biblioteka używa zoptymalizowanych struktur danych i indeksowania przyrostowego, aby utrzymać niskie zużycie pamięci, nawet przy milionach dokumentów.

**Q: Czy mogę zintegrować GroupDocs.Search z innymi aplikacjami Java?**  
A: Tak, API jest zaprojektowane tak, aby łatwo wbudować je w dowolny system oparty na Javie, od usług webowych po aplikacje desktopowe.

**Q: Co zrobić, jeśli wyniki wyszukiwania nie są dokładne?**  
A: Zweryfikuj, czy indeks zawiera wszystkie wymagane dokumenty (`add documents to index`), upewnij się, że filtrowanie słów stop jest wyłączone w razie potrzeby i rozważ ponowne zbudowanie indeksu po większych zmianach.

## Dodatkowe zasoby

- **Dokumentacja**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Referencja API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Pobieranie**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **Repozytorium GitHub**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Bezpłatne wsparcie**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Licencja tymczasowa**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Korzystając z tego przewodnika, teraz wiesz, jak **dodawać dokumenty do indeksu** i **wyłączać słowa stop w wyszukiwaniu**, aby dostarczać dokładniejsze wyniki w swoich aplikacjach Java.

---

**Ostatnia aktualizacja:** 2026-02-19  
**Testowano z:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs  

---