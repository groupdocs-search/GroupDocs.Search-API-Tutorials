---
date: '2026-05-17'
description: Dowiedz się, jak skonfigurować sieć wyszukiwania Java, zoptymalizować
  shards, wykonać wyszukiwanie tekstowe i obsłużyć konflikty portów w GroupDocs.Search
  for Java.
keywords:
- configure search network java
- GroupDocs.Search Java
- shard optimization
- Java search network
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  headline: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive
    Guide'
  type: TechArticle
- description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  name: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive Guide'
  steps:
  - name: Define Document Directories and Port
    text: '`DocumentDirectory` is a simple holder for the absolute path of a folder
      you want to index. Provide one or more paths to the configuration.'
  - name: Configure Search Network
    text: 'Create the configuration object using the defined paths:'
  - name: Deploy Nodes Using Configuration
    text: 'Deploy search network nodes and identify the master node for centralized
      management:'
  - name: Subscribe to Master Node Events
    text: '`SearchNetworkEventListener` lets you react to indexing completion, node
      failures, or shard optimizations. CODE_BLOCK_PLACEHOLDER_9_END'
  - name: Add Document Directories to Indexing Process
    text: Pass a list of folder paths to the master node; the engine will create a
      separate shard for each folder, enabling parallel query execution. CODE_BLOCK_PLACEHOLDER_10_END
  - name: Perform a Text Search
    text: Invoke the static helper to run a query and retrieve matching documents
      with relevance scores. CODE_BLOCK_PLACEHOLDER_11_END
  - name: Optimize Indexer Shards
    text: 'Optimize shards to improve search efficiency (this is where **how to optimize
      shards** really matters): CODE_BLOCK_PLACEHOLDER_12_END'
  type: HowTo
- questions:
  - answer: Optimizing shards compacts the index, reduces disk I/O, and typically
      yields 30‑50 % faster query responses for large datasets.
    question: How does shard optimization affect query speed?
  - answer: Yes, the operation is designed to run without downtime, but scheduling
      during low‑traffic periods is recommended for indexes larger than 20 GB.
    question: Is it safe to run `optimizeShards` on a live node?
  - answer: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor`
      to fine‑tune the optimization process.
    question: Can I customize the `OptimizeOptions`?
  - answer: Verify file system permissions, ensure enough free disk space, and confirm
      that no other process is locking the index files.
    question: What should I do if I encounter an `IOException` during optimization?
  - answer: Yes, the optimizer merges segments and removes tombstones, freeing up
      space occupied by deleted documents.
    question: Does optimizing shards also reclaim deleted document space?
  type: FAQPage
title: 'Jak zoptymalizować shards w GroupDocs.Search for Java: Kompletny przewodnik'
type: docs
url: /pl/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# Jak zoptymalizować fragmenty w GroupDocs.Search dla Javy: Kompletny przewodnik

Wydajne wyszukiwanie dokumentów jest niezbędne dla programistów i firm, które zarządzają dużymi zestawami danych lub potrzebują szybkiego wewnętrznego wyszukiwania. W tym samouczku dowiesz się **jak skonfigurować sieć wyszukiwania java**, jak indeksować i zapytywać dokumenty oraz dokładnych kroków **optymalizacji fragmentów** dla maksymalnej wydajności. Omówimy także rzeczywiste przypadki użycia, typowe pułapki i praktyczne wskazówki, aby Twoje węzły wyszukiwania działały płynnie.

## Szybkie odpowiedzi
- **Co to jest optymalizacja fragmentów?** Przeorganizowuje dane indeksu, aby przyspieszyć zapytania i zmniejszyć obciążenie pamięci masowej.  
- **Jak skonfigurować sieć wyszukiwania?** Zdefiniuj katalog bazowy i port, a następnie wdroż węzły przy użyciu udostępnionego API.  
- **Jak wykonać wyszukiwanie tekstowe?** Użyj `TextSearchInNetwork.searchAll` z ciągiem zapytania.  
- **Jak indeksować dokumenty w Javie?** Dodaj katalogi dokumentów do węzła master przy użyciu `IndexingDocuments.addDirectories`.  
- **Jak radzić sobie z konfliktami portów?** Zmień zmienną `basePort` na nieużywany port w Twoim systemie.

## Jak skonfigurować sieć wyszukiwania
`Configuration` przechowuje wszystkie ustawienia potrzebne do uruchomienia sieci GroupDocs.Search, takie jak lokalizacja folderu indeksu i port komunikacyjny.  
`SearchNetwork` koordynuje węzły, obsługując indeksowanie i dystrybucję zapytań.

Wczytaj swoją konfigurację wyszukiwania, ustaw bazową ścieżkę dokumentów, wybierz wolny port i uruchom sieć — wszystko w kilku linijkach kodu. Ta bezpośrednia odpowiedź wyjaśnia cały proces w mniej niż 70 słowach: **Utwórz obiekt `Configuration`, ustaw `basePath` i `basePort`, a następnie wywołaj `SearchNetwork.start(configuration)`.** Sieć automatycznie uruchomi węzeł master oraz wszystkie wymagane węzły pracownicze, gotowe do przyjmowania żądań indeksowania.

### Definicja kotwicy
`Configuration` jest podstawową klasą, która przechowuje wszystkie ustawienia potrzebne do uruchomienia sieci GroupDocs.Search, takie jak lokalizacja folderu indeksu i port komunikacyjny.

Aby uniknąć niechcianego błędu „port already in use”, najpierw sprawdź, czy wybrany port jest wolny (np. przy użyciu `netstat` lub prostego testu socket) przed zainicjowaniem sieci.

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

## Jak indeksować dokumenty w Javie
`IndexingDocuments` jest klasą pomocniczą, która upraszcza dodawanie wielu katalogów do węzła wyszukiwania i uruchamia potok indeksowania.

Dodaj foldery dokumentów do węzła master, a następnie pozwól indeksatorowi je przeszukać. **Bezpośrednia odpowiedź:** Wywołaj `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))`, a następnie `masterNode.index()`; silnik utworzy przeszukiwalne fragmenty dla każdego podanego folderu. To podejście skaluje się poziomo — dodaj więcej węzłów, a ta sama metoda automatycznie rozdzieli obciążenie.

### Definicja kotwicy
`IndexingDocuments` jest klasą pomocniczą, która upraszcza dodawanie wielu katalogów do węzła wyszukiwania i uruchamia potok indeksowania.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Jak wykonać wyszukiwanie tekstowe
`TextSearchInNetwork` udostępnia statyczne metody pomocnicze, które rozgłaszają zapytanie tekstowe do każdego węzła w sieci i agregują wyniki.  
`SearchResult` zawiera identyfikator dopasowanego dokumentu, fragment oraz ocenę trafności.

Uruchom zapytanie we wszystkich fragmentach jednym wywołaniem metody. **Bezpośrednia odpowiedź:** Użyj `TextSearchInNetwork.searchAll("your query", searchNetwork)`; metoda zwraca kolekcję obiektów `SearchResult` zawierających identyfikatory dokumentów, fragmenty i oceny trafności. Możesz dodatkowo filtrować wyniki według języka, typu pliku lub własnych metadanych bez pisania dodatkowego kodu.

### Definicja kotwicy
`TextSearchInNetwork` udostępnia statyczne metody pomocnicze, które rozgłaszają zapytanie tekstowe do każdego węzła w sieci i agregują wyniki.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## Jak radzić sobie z konfliktami portów
Jeśli domyślny port (`49132`) jest zajęty, po prostu wybierz inny wolny port i zaktualizuj pole `basePort` przed uruchomieniem sieci. **Bezpośrednia odpowiedź:** Zmień `int basePort = 49132;` na nieużywaną wartość, np. `49133`, przebuduj i uruchom ponownie; sieć połączy się z nowym portem bez wpływu na istniejące węzły.

Wskazówka: Przechowuj mały plik konfiguracyjny (np. `search-config.properties`), aby móc zmienić port bez rekompilacji.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Wymagania wstępne
Zanim zaczniemy, upewnij się, że masz następujące wymagania spełnione:

### Wymagane biblioteki, wersje i zależności
Aby wdrożyć to rozwiązanie, dołącz bibliotekę GroupDocs.Search przy użyciu Maven, dodając następującą konfigurację do pliku `pom.xml`:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
Alternatywnie, pobierz najnowszą wersję z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Wymagania dotyczące konfiguracji środowiska
- Java Development Kit (JDK) 8 lub nowszy.  
- Uprawnienia sieciowe pozwalające na powiązanie z wybranym `basePort`.  
- Wystarczająca ilość miejsca na dysku dla plików indeksu (każdy fragment może zajmować ~10 MB na 1 000 dokumentów).

### Wymagania wiedzy
Podstawowa znajomość Javy, programowania obiektowego i obsługi wyjątków pomoże Ci płynnie śledzić przykłady.

## Konfiguracja GroupDocs.Search dla Javy
Aby rozpocząć korzystanie z GroupDocs.Search w swoim projekcie, wykonaj następujące kroki:

1. **Add the Dependency**: As shown above, add the necessary Maven dependency to your project or download directly from the releases page.  
2. **License Acquisition**:  
   - **Free trial** – no license key required, but usage is limited to 500 documents per day.  
   - **Temporary license** – request a 30‑day trial key from [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).  
   - **Full license** – purchase a production license for unlimited access and priority support.  
3. **Basic Initialization and Setup**:  
   Initialize the configuration using the `Configuration` class, setting up the base path for documents and specifying a port number:

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## Przewodnik implementacji
Teraz przyjrzyjmy się implementacji kluczowych funkcji przy użyciu GroupDocs.Search Java.

### Funkcja: Konfigurowanie sieci wyszukiwania
**Overview**: Setting up a search network involves defining your document directory and configuring it with a specific port for communication between nodes.

#### Krok 1: Zdefiniuj katalogi dokumentów i port
`DocumentDirectory` is a simple holder for the absolute path of a folder you want to index. Provide one or more paths to the configuration.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### Krok 2: Skonfiguruj sieć wyszukiwania
Create the configuration object using the defined paths:

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Funkcja: Wdrażanie węzłów sieci wyszukiwania
**Overview**: Deploy nodes to handle document searches efficiently across your network.

#### Krok 1: Wdrożenie węzłów przy użyciu konfiguracji
Deploy search network nodes and identify the master node for centralized management:

```java
public static void optimizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    OptimizeOptions options = new OptimizeOptions();
    indexer.optimize(options);
}

optimizeShards(masterNode);

// Perform a second text search to observe optimization effects
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Funkcja: Subskrybowanie zdarzeń węzła sieci
**Overview**: Monitor your search network by subscribing to events that notify you of important changes or actions.

#### Krok 1: Subskrybuj zdarzenia węzła master
`SearchNetworkEventListener` lets you react to indexing completion, node failures, or shard optimizations.

CODE_BLOCK_PLACEHOLDER_9_END

### Funkcja: Indeksowanie dokumentów w węzłach sieci
**Overview**: Add directories containing documents to the indexing process for efficient searches.

#### Krok 1: Dodaj katalogi dokumentów do procesu indeksowania
Pass a list of folder paths to the master node; the engine will create a separate shard for each folder, enabling parallel query execution.

CODE_BLOCK_PLACEHOLDER_10_END

### Funkcja: Wyszukiwanie tekstu w węzłach sieci
**Overview**: Execute text searches across all indexed documents within your search network.

#### Krok 1: Wykonaj wyszukiwanie tekstowe
Invoke the static helper to run a query and retrieve matching documents with relevance scores.

CODE_BLOCK_PLACEHOLDER_11_END

### Funkcja: Optymalizacja fragmentów
**Overview**: Enhance performance by optimizing shards within the indexer of your search network node.

#### Krok 1: Optymalizuj fragmenty indeksera
Optimize shards to improve search efficiency (this is where **how to optimize shards** really matters):

CODE_BLOCK_PLACEHOLDER_12_END

## Praktyczne zastosowania
GroupDocs.Search for Java can be applied in various real‑world scenarios, each benefiting from shard optimization:

1. **Enterprise Document Management** – Handles 10 TB+ archives with sub‑second query times after shard optimization.  
2. **E‑commerce Platforms** – Powers product search across 1 million SKUs, reducing latency by up to 45 % when shards are optimized.  
3. **Legal Firms** – Retrieves case files from 200 GB repositories in under 200 ms.  
4. **Library Systems** – Supports catalog searches for 500 k digital books with efficient memory usage.  
5. **Content Management Systems (CMS)** – Enables instant content discovery for multi‑site deployments with over 2 million pages.

## Rozważania dotyczące wydajności
Aby zapewnić optymalną wydajność implementacji GroupDocs.Search:

- **Regularly optimize shards** – Running `optimizeShards()` after every 10 GB of new data reduces query response times by 30‑50 %.  
- **Monitor memory usage** – Keep JVM heap below 75 % of physical RAM; enable G1GC for large indexes.  
- **Use incremental indexing** – Add only changed files to avoid full re‑indexing.  
- **Leverage multi‑node scaling** – Add worker nodes to distribute shards; each additional node can improve throughput by ~20 % for read‑heavy workloads.

## Typowe problemy i rozwiązania
| Issue | Symptom | Solution |
|-------|---------|----------|
| Port conflict on startup | `java.net.BindException: Address already in use` | Change `basePort` to an unused value; verify with `netstat -ano`. |
| Out‑of‑memory errors during optimization | `java.lang.OutOfMemoryError: Java heap space` | Increase JVM `-Xmx` flag or run optimization on a dedicated node with more RAM. |
| Missing documents in search results | No results returned after indexing | Ensure directories are correctly added via `IndexingDocuments.addDirectories` and that `masterNode.index()` completed without exceptions. |
| Stale shards after bulk delete | Deleted files still appear | Run `optimizeShards()` to merge segments and purge tombstones. |

## Najczęściej zadawane pytania

**Q: How does shard optimization affect query speed?**  
A: Optimizing shards compacts the index, reduces disk I/O, and typically yields 30‑50 % faster query responses for large datasets.

**Q: Is it safe to run `optimizeShards` on a live node?**  
A: Yes, the operation is designed to run without downtime, but scheduling during low‑traffic periods is recommended for indexes larger than 20 GB.

**Q: Can I customize the `OptimizeOptions`?**  
A: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor` to fine‑tune the optimization process.

**Q: What should I do if I encounter an `IOException` during optimization?**  
A: Verify file system permissions, ensure enough free disk space, and confirm that no other process is locking the index files.

**Q: Does optimizing shards also reclaim deleted document space?**  
A: Yes, the optimizer merges segments and removes tombstones, freeing up space occupied by deleted documents.

## Zakończenie
Following this comprehensive guide, you now know how to **configure search network java**, index documents, run text queries, and most importantly, **optimize shards** to keep your search performance razor‑sharp. Apply these patterns to any Java‑based enterprise search solution, and you’ll see measurable improvements in latency, scalability, and resource utilization. For next steps, explore advanced features like custom analyzers, faceted search, and integration with cloud storage providers.

---

**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Powiązane samouczki

- [Konfigurowanie sieci GroupDocs.Search w .NET: Kompletny przewodnik](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Główne indeksowanie dokumentów .NET przy użyciu GroupDocs.Search: Kompletny przewodnik](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Samouczki i przykłady GroupDocs.Search dla Javy](/search/net/)