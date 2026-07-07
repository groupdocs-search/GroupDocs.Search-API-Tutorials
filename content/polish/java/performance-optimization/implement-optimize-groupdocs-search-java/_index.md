---
date: '2026-07-07'
description: Dowiedz się, jak usunąć index, wykonać full text search Java oraz zoptymalizować
  search performance przy użyciu GroupDocs.Search for Java. Przewodnik krok po kroku
  z network setup i indexing.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: Jak usunąć index i wykonać full text search Java przy użyciu GroupDocs.Search.
  Postępuj zgodnie z tym przewodnikiem, aby skonfigurować search network, utworzyć
  searchable index i zoptymalizować search performance.
og_title: Jak usunąć index i wykonać text search z GroupDocs.Search for Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: Jak usunąć index i wykonać text search z GroupDocs.Search for Java
type: docs
url: /pl/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Jak usunąć indeks i wykonywać wyszukiwanie tekstu przy użyciu GroupDocs.Search dla Javy

W dzisiejszym świecie napędzanym danymi, **how to delete index** szybko, jednocześnie zapewniając błyskawiczne możliwości pełnotekstowego wyszukiwania w Javie, jest przewagą konkurencyjną. Niezależnie od tego, czy budujesz wewnętrzną bazę wiedzy, repozytorium spraw prawnych, czy katalog produktów e‑commerce, dobrze dostrojona sieć wyszukiwania może znacząco poprawić satysfakcję użytkowników. W tym przewodniku dowiesz się, jak **set up a search network**, **create a searchable index**, **optimize search performance** oraz **delete documents from the index** w razie potrzeby — wszystko przy użyciu GroupDocs.Search dla Javy.

## Szybkie odpowiedzi
- **What is the main purpose of GroupDocs.Search for Java?** Zapewnia pełnotekstowe wyszukiwanie w ponad 50 formatach dokumentów, umożliwiając szybkie wyszukiwanie słów kluczowych.  
- **How do I perform text search in a distributed environment?** Uruchom sieć wyszukiwania, indeksuj dokumenty na węźle głównym, a następnie zapytaj dowolny węzeł.  
- **Can I delete documents from the index without rebuilding it?** Tak, użyj Delete API, aby usunąć wybrane pliki, skutecznie *how to delete index* bez pełnego ponownego indeksowania.  
- **What Java version is required?** JDK 8 lub wyższy.  
- **Is a license needed for production?** Wymagana jest ważna licencja GroupDocs.Search; dostępna jest darmowa wersja próbna.

## Co to jest „perform text search”?
Wykonywanie wyszukiwania tekstu oznacza zapytanie pełnotekstowego indeksu w celu odnalezienia dokumentów zawierających określone słowa kluczowe lub frazy. GroupDocs.Search buduje odwrócony indeks, który umożliwia te wyszukiwania niezwykle szybko, nawet wśród tysięcy plików.

## Dlaczego warto skonfigurować sieć wyszukiwania?
Sieć wyszukiwania rozdziela obciążenia indeksowania i zapytań na wiele węzłów, umożliwiając **optimize search performance**, skalowanie w poziomie i utrzymanie wysokiej dostępności. Ta architektura jest idealna dla repozytoriów dokumentów na poziomie przedsiębiorstwa, gdzie istotne są opóźnienia i przepustowość.

## Jak wdrożyć i zoptymalizować sieć wyszukiwania przy użyciu GroupDocs.Search dla Javy
Wczytaj swoją konfigurację, uruchom węzeł główny, a następnie dodaj węzły robocze, które współdzielą tę samą ścieżkę bazową i port. Takie wdrożenie sieci pozwala dowolnemu węzłowi obsługiwać żądania indeksowania lub zapytań, zapewniając spójne czasy odpowiedzi nawet przy rosnącej liczbie dokumentów sięgającej setek tysięcy.

### Przegląd krok po kroku
1. **Define a base configuration** która zawiera współdzielony katalog i port TCP.  
2. **Start the master node** aby zarządzać indeksem i koordynować węzły robocze.  
3. **Add worker nodes** które łączą się z węzłem głównym, umożliwiając równoległe indeksowanie i wyszukiwanie.  
4. **Monitor resource usage** i dostosuj ustawienia sterty JVM, aby utrzymać niskie opóźnienia.

## Jak usunąć indeks w GroupDocs.Search dla Javy
`SearchNode` reprezentuje węzeł w sieci GroupDocs.Search, który zarządza operacjami indeksowania i zapytań. Metoda `delete` usuwa określone dokumenty z indeksu.

### Bezpośrednie kroki usuwania
- Wywołaj metodę `delete` na instancji `SearchNode`.  
- Podaj tablicę względnych ścieżek plików.  
- Zatwierdź zmiany; indeks zostaje natychmiast odświeżony i kolejne wyszukiwania nie zwracają usuniętych plików.

## Co to jest sieć wyszukiwania?
Sieć **search network** to klaster połączonych ze sobą węzłów, które współdzielą wspólne repozytorium indeksu, umożliwiając rozproszone indeksowanie i wykonywanie zapytań. Zapewnia skalowanie w poziomie oraz odporność na awarie dla dużych zbiorów dokumentów.

## Jak utworzyć indeks przeszukiwalny (index documents java)
Metoda `add` indeksuje dokument w indeksie wyszukiwania. Dodaj dokumenty do węzła głównego przy użyciu metody `add`; sieć propaguje zmiany do wszystkich węzłów roboczych. To podejście zapewnia, że każdy węzeł może obsługiwać zapytania względem najnowszego indeksu bez dodatkowych kroków synchronizacji.

### Kluczowe działania
- Wskaż węzeł główny na folder zawierający pliki źródłowe.  
- Uruchom procedurę indeksowania; sieć przetwarza każdy plik i aktualizuje odwrócony indeks.  
- Sprawdź, czy pliki indeksu pojawiają się w wyznaczonym katalogu przechowywania.

## Jak usunąć zindeksowane pliki (remove indexed files)
Gdy dokument staje się przestarzały, wywołaj API `delete` z jego ścieżką. System usuwa wpisy pliku z odwróconego indeksu, zwalniając miejsce i zapobiegając przestarzałym wynikom.

## Konfiguracja GroupDocs.Search dla Javy
Aby rozpocząć, zintegrować GroupDocs.Search z projektem Java, korzystając z poniższej konfiguracji:

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
Alternatively, you can [download the latest version directly from GroupDocs](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
GroupDocs oferuje darmową wersję próbną, która pozwala ocenić funkcje przed zakupem. Tymczasową licencję można uzyskać, postępując zgodnie z instrukcjami na ich [purchase page](https://purchase.groupdocs.com/temporary-license/). To umożliwi pełną funkcjonalność w trakcie fazy testowej.

### Podstawowa inicjalizacja i konfiguracja
Zainicjalizuj GroupDocs.Search w aplikacji Java przy użyciu:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## Przewodnik implementacji

### Konfigurowanie sieci wyszukiwania
**Overview:** Ustal ścieżkę bazową i port dla sieci wyszukiwania, umożliwiając węzłom skuteczną komunikację.

#### Krok 1: Zdefiniuj konfigurację bazową
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parameters:**  
  - `basePath`: Ścieżka katalogu dla operacji sieciowych.  
  - `basePort`: Numer portu używanego przez sieć wyszukiwania.

#### Krok 2: Rozwiązywanie problemów
Upewnij się, że wybrany port nie jest zablokowany przez ustawienia zapory lub używany przez inną aplikację. Dostosuj w razie potrzeby, aby uniknąć konfliktów.

### Wdrażanie węzłów sieci wyszukiwania
**Overview:** Korzystając z konfiguracji, wdrażaj węzły w sieci w celu rozproszonego indeksowania i wyszukiwania.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Key Configuration Options:**  
  - **Base Path & Port:** Te wartości powinny odpowiadać tym użytym w początkowej konfiguracji, aby zapewnić spójność.

### Indeksowanie dokumentów (`create searchable index`)
**Overview:** Dodaj dokumenty do indeksu wyszukiwania efektywnie przy użyciu węzła głównego.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Purpose:**  
  - `masterNode`: Główny węzeł zarządzający indeksowaniem dokumentów.  
  - `documentsPath`: Ścieżka do katalogu zawierającego dokumenty.

#### Wskazówki rozwiązywania problemów
Sprawdź, czy ścieżki do dokumentów są poprawne i dostępne. Upewnij się, że uprawnienia pozwalają na odczyt z tych katalogów.

### Wyszukiwanie tekstu w sieci (`perform text search`)
**Overview:** Wykonaj kompleksowe wyszukiwania tekstu w całej zindeksowanej sieci.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parameters:**  
  - `query`: Tekst, którego szukasz.  
  - `masterNode`: Węzeł przeprowadzający wyszukiwanie.

### Usuwanie dokumentów z indeksu (`delete documents index`)
**Overview:** Usuń określone dokumenty z indeksu, podając ich ścieżki plików.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Method Purpose:**  
  - `node`: Docelowy węzeł dla operacji usuwania.  
  - `filePaths`: Ścieżki dokumentów do usunięcia z indeksu.

#### Rozwiązywanie problemów
Upewnij się, że ścieżki plików są dokładne i że pliki istnieją w katalogu. Jeśli problemy będą się utrzymywać, sprawdź uprawnienia sieciowe i łączność.

## Praktyczne zastosowania
1. **Enterprise Document Management:** Usprawnij wewnętrzne wyszukiwanie wiedzy.  
2. **Legal Case Analysis:** Szybko znajdź odpowiednie akta spraw w wielu repozytoriach.  
3. **E‑commerce Platforms:** Zwiększ szybkość wyszukiwania produktów poprzez indeksowanie opisów i recenzji.  
4. **Academic Research:** Efektywnie przeszukuj duże cyfrowe biblioteki prac i rozpraw.  
5. **Customer Support Systems:** Skróć czas odpowiedzi, umożliwiając agentom natychmiastowe przeszukiwanie wcześniejszych zgłoszeń.

## Rozważania dotyczące wydajności
- **Optimize Indexing Speed:** Dodawaj nowe dokumenty stopniowo w godzinach poza szczytem, aby utrzymać niskie opóźnienia.  
- **Resource Usage Guidelines:** Monitoruj CPU i pamięć, szczególnie przy skalowaniu liczby węzłów.  
- **Java Memory Management:** Dostosuj ustawienia sterty JVM w zależności od obciążenia (np. `-Xmx2g` dla indeksów średniej wielkości).

## Zakończenie
Korzystając z tego przewodnika, nauczyłeś się, jak **set up a search network**, **create a searchable index**, **perform text search** oraz **delete documents index** przy użyciu GroupDocs.Search dla Javy. Te możliwości umożliwiają szybkie i niezawodne wyszukiwanie dokumentów w środowiskach rozproszonych.

**Next Steps**
- Eksperymentuj z różnymi konfiguracjami węzłów, aby znaleźć optymalny balans dla swojego obciążenia.  
- Zgłębiaj zaawansowane opcje indeksowania, takie jak niestandardowe analizatory i dostrajanie trafności.  
- Zbadaj integrację z innymi produktami GroupDocs w celu kompleksowego przetwarzania dokumentów.

## Najczęściej zadawane pytania

**Q: What is the primary use case for GroupDocs.Search for Java?**  
A: Zapewnia pełnotekstowe wyszukiwanie w wielu formatach dokumentów, umożliwiając **perform text search** w dużych repozytoriach.

**Q: How can I improve search speed in a large network?**  
A: Wdrażaj dodatkowe węzły, dostosuj stertę JVM i planuj indeksowanie w okresach niskiego ruchu, aby **optimize search performance**.

**Q: Is it possible to delete a single document without re‑indexing the whole collection?**  
A: Tak, użyj API **delete documents index**, jak pokazano w przykładzie kodu, aby usunąć określone pliki.

**Q: Do I need a license for development?**  
A: Licencja próbna jest wystarczająca do testów; licencja komercyjna jest wymagana przy wdrożeniach produkcyjnych.

**Q: Can I index PDFs, Word files, and emails together?**  
A: Oczywiście — GroupDocs.Search obsługuje szeroką gamę formatów od razu po instalacji.

---

**Ostatnia aktualizacja:** 2026-07-07  
**Testowano z:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs

## Powiązane samouczki

- [How to Index Text in Java with GroupDocs.Search Guide](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [Optimize Search Performance with Advanced Indexing Techniques in GroupDocs.Search for Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [Improve Query Performance with GroupDocs.Search Java: Optimize Index & Search](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)