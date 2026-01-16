---
date: '2026-01-16'
description: Dowiedz się, jak skonfigurować sieć wyszukiwania GroupDocs w Javie i
  dodać synonimy do indeksu, aby zwiększyć wydajność wyszukiwania.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Skonfiguruj GroupDocs.Search Network w Javie – przyspiesz wyszukiwanie
type: docs
url: /pl/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Konfiguracja sieci GroupDocs.Search w Javie – przyspieszenie wyszukiwania

W dzisiejszych aplikacjach opartych na danych, **configure groupdocs search network** jest kluczowym krokiem do dostarczania szybkich, dokładnych wyników w ogromnych zbiorach dokumentów. Niezależnie od tego, czy budujesz portal wyszukiwania na poziomie przedsiębiorstwa, czy rozszerzasz istniejące rozwiązanie, dobrze skonfigurowana sieć GroupDocs.Search pozwala na skalowanie w poziomie, dodawanie obsługi synonimów i utrzymanie niskiej latencji. W tym samouczku nauczysz się, jak skonfigurować, wdrożyć i dopasować sieć GroupDocs.Search przy użyciu Javy, a także praktyczne wskazówki dotyczące dodawania synonimów do indeksu i zarządzania cyklem życia węzłów.

## Szybkie odpowiedzi
- **Jaka jest główna korzyść z konfiguracji sieci GroupDocs.Search?** Umożliwia rozproszone indeksowanie i zapytania, poprawiając wydajność i skalowalność.  
- **Czy potrzebuję licencji, aby uruchomić przykłady?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w produkcji.  
- **Czy można dodać synonimy bez przebudowy indeksu?** Tak — użyj słownika synonimów w czasie wykonywania, aby **add synonyms to index**.  
- **Ile węzłów mogę wdrożyć?** Możesz wdrożyć dowolną liczbę węzłów, zależnie od możliwości Twojej infrastruktury; każdy węzeł działa na własnym porcie.  

## Co to jest konfigurowanie sieci GroupDocs.Search?
Konfigurowanie sieci GroupDocs.Search oznacza definiowanie struktury folderów, portów i ustawień węzłów, które pozwalają wielu instancjom JVM współpracować przy indeksowaniu i wyszukiwaniu. To ustawienie tworzy węzeł główny (master‑node), który koordynuje pracowników (shards) i zapewnia wykonywanie zapytań na całym zestawie danych.

## Dlaczego konfigurować sieć GroupDocs.Search?
- **Scalability** – Rozdziel obciążenie indeksowania na kilka maszyn.  
- **Reliability** – Węzły mogą być dodawane lub usuwane bez przestoju.  
- **Search relevance** – Dodaj synonimy do indeksu, aby uzyskać bogatsze wyniki.  
- **Performance** – Równoległe wykonywanie zapytań skraca czas odpowiedzi.  

## Wymagania wstępne
- Java Development Kit (JDK) 8 lub nowszy  
- Maven do budowania projektu  
- Podstawowa znajomość składni Javy  
- Dostęp do biblioteki GroupDocs.Search for Java (pobieranej przez Maven lub ze strony oficjalnych wydań)

## Konfiguracja GroupDocs.Search dla Javy

Dodaj repozytorium i zależność do swojego pliku Maven **pom.xml**:

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

Alternatywnie, pobierz najnowszą wersję bezpośrednio z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskiwanie licencji
- **Free Trial** – Poznaj podstawowe funkcje bez kosztów.  
- **Temporary License** – Odblokuj pełne możliwości na krótkoterminowe testy.  
- **Commercial License** – Wymagana przy wdrożeniach produkcyjnych.

### Podstawowa inicjalizacja i konfiguracja
Utwórz prostą klasę Java, aby zweryfikować prawidłowe ładowanie biblioteki:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Przewodnik krok po kroku po konfiguracji sieci GroupDocs.Search

### 1. Konfigurowanie sieci wyszukiwania
Zdefiniuj podstawowy folder dokumentów oraz początkowy port do komunikacji węzłów.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Gdzie znajdują się słowniki (np. pliki synonimów).  
- **basePort** – Pierwszy port; kolejne węzły zwiększają go o tę wartość.

### 2. Wdrażanie węzłów sieci wyszukiwania
Uruchom wiele węzłów roboczych, które współdzielą tę samą konfigurację.

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Każdy węzeł działa na własnym porcie (basePort + index) i przechowuje fragment (shard) całego indeksu.

### 3. Subskrybowanie zdarzeń węzła
Monitoruj stan, postęp indeksowania i warunki błędów, podłączając nasłuchiwacz zdarzeń do węzła głównego.

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Wywołania zwrotne zdarzeń pozwalają reagować na uruchomienie/wyłączenie węzła, zakończenie indeksowania oraz nieoczekiwane awarie.

### 4. Dodawanie synonimów do indeksatora węzła  
Zwiększ trafność, używając **add synonyms to index** w czasie wykonywania.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Tablica terminów, które powinny być traktowane jako równoważne.  
- **clearBeforeAdding** – Ustaw na `true`, jeśli chcesz zastąpić istniejące wpisy.

### 5. Dodawanie katalogów do indeksowania
Powiedz węzłowi głównemu, które foldery zawierają dokumenty, które mają być przeszukiwalne.

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

Metoda skanuje katalog rekurencyjnie i rozdziela pliki pomiędzy fragmenty (shards).

### 6. Wykonywanie wyszukiwania tekstowego w sieci
Wykonaj zapytanie we wszystkich węzłach, opcjonalnie wymuszając zachowanie dopasowania dokładnego.

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Ustaw `exactMatchOnly` na `true`, gdy potrzebne jest ścisłe dopasowanie terminu bez stemmingu.

### 7. Zamykanie węzłów sieci
Zwolnij zasoby w sposób kontrolowany po zakończeniu przetwarzania.

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Poprawne zamknięcie zapobiega wyciekom pamięci i utrzymuje JVM w dobrej kondycji.

## Praktyczne zastosowania
| Scenario | How the network helps |
|----------|-----------------------|
| **Enterprise Search** | Rozdziel indeksowanie na serwery w centrum danych, aby obsłużyć korpusy o skali petabajtów. |
| **Document Management** | Dodaj synonimy do indeksu, aby użytkownicy znajdowali dokumenty nawet przy różnej terminologii. |
| **E‑commerce Catalog** | Wdrażaj węzły specyficzne dla regionu, aby szybko obsługiwać lokalne wyszukiwania produktów. |
| **Content Management** | Utrzymuj treść przeszukiwalną, gdy redaktorzy dodają nowe pliki do określonych katalogów. |

## Częste problemy i rozwiązania
- **Port Conflicts** – Upewnij się, że port każdego węzła (basePort + index) jest wolny; w razie potrzeby dostosuj `basePort`.  
- **Synonym Not Applied** – Sprawdź, czy po dodaniu terminów wywołałeś `indexer.setDictionary(dictionary)`.  
- **Node Not Responding** – Subskrybuj zdarzenia; szukaj wywołań zwrotnych `NodeFailed`, aby zdiagnozować problemy sieciowe.  
- **Memory Leak on Close** – Zawsze wywołuj `node.close()` dla każdego wdrożonego węzła.  

## Najczęściej zadawane pytania

**Q: Jak wdrożenie wielu węzłów poprawia wydajność wyszukiwania?**  
A: Każdy węzeł indeksuje fragment danych, co umożliwia równoległe przetwarzanie i zmniejsza opóźnienie zapytań, ponieważ obciążenie jest rozdzielane.

**Q: Czy mogę dodać synonimy bez ponownego indeksowania istniejących dokumentów?**  
A: Tak, możesz **add synonyms to index** w czasie wykonywania za pomocą słownika synonimów; zmiany wchodzą w życie od razu dla nowych zapytań.

**Q: Czy subskrybowanie zdarzeń węzła jest obowiązkowe?**  
A: Choć nie jest wymagane do podstawowej pracy, subskrypcja zdarzeń zapewnia wgląd w stan węzła i pomaga szybko reagować na awarie.

**Q: Jakie są najlepsze praktyki zarządzania zasobami węzłów?**  
A: Regularnie zamykaj nieużywane węzły, monitoruj zużycie pamięci JVM i odnawiaj węzły w godzinach poza szczytem, aby utrzymać optymalne zużycie zasobów.

**Q: Czy GroupDocs.Search obsługuje formaty nienależące do tekstu, takie jak PDF‑y lub obrazy?**  
A: Zdecydowanie tak. Biblioteka wyodrębnia tekst z plików PDF, Office oraz wykonuje OCR na obrazach, co czyni je przeszukiwalnymi od razu po instalacji.

---

**Ostatnia aktualizacja:** 2026-01-16  
**Testowano z:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs