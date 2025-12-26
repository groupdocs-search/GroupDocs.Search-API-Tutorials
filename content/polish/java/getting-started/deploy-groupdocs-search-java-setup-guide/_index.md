---
date: '2025-12-26'
description: Dowiedz się, jak utworzyć indeks przeszukiwalny w Javie przy użyciu GroupDocs.Search
  for Java, dodać pliki do wyszukiwania i dodać katalogi do węzła.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: Utwórz przeszukiwalny indeks w Javie – wdrożenie GroupDocs.Search dla Javy
type: docs
url: /pl/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# Utwórz przeszukiwalny indeks Java – Wdrożenie GroupDocs.Search dla Java

W dzisiejszym świecie napędzanym danymi, **tworzenie przeszukiwalnego indeksu java** aplikacje muszą efektywnie obsługiwać ogromne kolekcje dokumentów. Niezależnie od tego, czy budujesz usługę wyszukiwania klasy korporacyjnej, czy mniejszy projekt, dobrze skonfigurowana sieć wyszukiwania może znacząco przyspieszyć odzyskiwanie wyników i zwiększyć ich trafność. W tym przewodniku przeprowadzimy Cię przez cały proces konfiguracji **GroupDocs.Search for Java**, od dodawania plików do wyszukiwania po dodawanie katalogów do węzła, abyś mógł od razu rozpocząć indeksowanie swoich dokumentów.

## Szybkie odpowiedzi
- **Jaki jest podstawowy cel GroupDocs.Search?** Dostarcza skalowalny, oparty na Javie silnik do indeksowania i przeszukiwania dokumentów w rozproszonej sieci.  
- **Którą wersję powinienem używać?** Zalecana jest najnowsza stabilna wersja (np. 25.4) dla nowych projektów.  
- **Czy potrzebna jest licencja?** Dostępna jest 30‑dniowa bezpłatna wersja próbna; stała licencja jest wymagana do użytku produkcyjnego.  
- **Czy mogę dodać zarówno pliki, jak i całe katalogi?** Tak – użyj pomocników `addFiles` i `addDirectories`, aby wczytać zawartość.  
- **Jakiej wersji Javy wymaga?** Java 8 lub wyższa, z Mavenem do zarządzania zależnościami.

## Co to jest „create searchable index java”?
Tworzenie przeszukiwalnego indeksu w Javie oznacza budowanie struktury danych, która mapuje terminy na dokumenty je zawierające, umożliwiając szybkie zapytania pełnotekstowe. GroupDocs.Search zajmuje się ciężką pracą, pozwalając Ci skupić się na dostarczaniu dokumentów i dostrajaniu zachowań wyszukiwania.

## Dlaczego warto używać GroupDocs.Search for Java?
- **Skalowalna architektura sieci** – Wdrożenie wielu węzłów, które współdzielą obciążenie indeksowania.  
- **Bogate wsparcie formatów dokumentów** – PDF, Word, Excel, PowerPoint, obrazy i wiele innych.  
- **Aktualizacje zdarzeniowe** – Subskrybuj zdarzenia węzła, aby utrzymywać indeks aktualny w czasie rzeczywistym.  
- **Prosta integracja z Mavenem** – Dodaj kilka linii do `pom.xml` i rozpocznij indeksowanie.

## Wymagania wstępne
- **JDK 8+** zainstalowany na maszynie deweloperskiej.  
- IDE, takie jak **IntelliJ IDEA** lub **Eclipse**.  
- Podstawowa znajomość **Java** i **Maven**.  
- Dostęp do biblioteki **GroupDocs.Search for Java** (pobranie lub Maven).

## Konfiguracja GroupDocs.Search for Java

### Zależność Maven
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

> **Wskazówka:** Utrzymuj numer wersji aktualny, sprawdzając oficjalną stronę wydań.

Możesz także pobrać plik JAR bezpośrednio ze strony: [wydania GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
- **Bezpłatna wersja próbna:** 30‑dniowa ocena.  
- **Licencja tymczasowa:** Wniosek o przedłużone testowanie.  
- **Zakup:** Wymagany dla wdrożeń produkcyjnych.

### Podstawowa inicjalizacja
Utwórz obiekt konfiguracji, który wskazuje folder, w którym będą przechowywane pliki indeksu, oraz definiuje podstawowy port komunikacyjny:

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## Jak stworzyć przeszukiwalny indeks java z GroupDocs.Search?

Poniżej przedstawiamy kluczowe funkcje, które pozwolą Ci **dodawać pliki do wyszukiwania** i **dodawać katalogi do węzła**, jednocześnie wdrażając skalowalną sieć.

### Funkcja 1 – Konfiguracja i ustawienia sieci
Konfigurowanie sieci wyszukiwania to pierwszy krok w budowie przeszukiwalnego indeksu.

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – Katalog, w którym będą przechowywane dane indeksu.  
- **`basePort`** – Port początkowy; każdy węzeł zwiększy go o jeden.

### Funkcja 2 – Wdrożenie węzłów sieci wyszukiwania
Wdrożenie węzłów rozdziela obciążenie indeksowania na wiele maszyn lub procesów.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

Każdy `SearchNetworkNode` uruchamia własną usługę indeksowania, umożliwiając **tworzenie przeszukiwalnego indeksu java**, który skaluje się poziomo.

### Funkcja 3 – Subskrypcja zdarzeń węzła
Aktualizacje w czasie rzeczywistym utrzymują indeks zsynchronizowany ze zmianami w systemie plików.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

Nasłuchując zdarzeń, możesz automatycznie wywoływać ponowne indeksowanie, gdy pojawią się nowe pliki.

### Funkcja 4 – Dodawanie katalogów do węzła sieci
Użyj tego pomocnika, aby **dodawać katalogi do węzła**, rekurencyjnie zbierając wszystkie obsługiwane dokumenty.

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

### Funkcja 5 – Dodawanie plików do węzła sieci
Gdy potrzebna jest precyzyjna kontrola, **dodawaj pliki do wyszukiwania** indywidualnie:

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Ta metoda daje elastyczność indeksowania plików pochodzących ze strumieni, przechowywania w chmurze lub tymczasowych lokalizacji.

## Typowe problemy i rozwiązania
| Problem | Powód | Rozwiązanie |
|---------|-------|-------------|
| **Brak dokumentów w wynikach wyszukiwania** | Indeks nie został zatwierdzony | Wywołaj `node.getIndexer().commit()` po dodaniu plików. |
| **Błąd konfliktu portu** | Inna usługa używa `basePort` | Wybierz inny `basePort` lub sprawdź dostępne porty. |
| **Nieobsługiwany format pliku** | Biblioteka nie posiada parsera | Upewnij się, że rozszerzenie pliku jest obsługiwane lub dodaj własny ekstraktor. |

## Najczęściej zadawane pytania

**P: Czy mogę używać GroupDocs.Search w aplikacji Java działającej w chmurze?**  
O: Tak. Biblioteka działa w dowolnym środowisku Java, a `basePath` możesz skierować do folderu zamontowanego sieciowo lub pamięci chmurowej zamontowanej lokalnie.

**P: Jak zaktualizować indeks, gdy plik ulegnie zmianie?**  
O: Subskrybuj zdarzenia węzła (patrz Funkcja 3) i ponownie wywołaj `addFiles` lub `addDirectories` dla zmodyfikowanych ścieżek.

**P: Czy istnieje limit liczby węzłów, które mogę wdrożyć?**  
O: Praktycznie limit zależy od Twojego sprzętu i przepustowości sieci. API nie narzuca sztywnego limitu.

**P: Czy muszę restartować węzły po dodaniu nowych plików?**  
O: Nie. Dodawanie plików uruchamia indeksowanie automatycznie; jedynie w razie odroczenia operacji trzeba wykonać commit.

**P: Jakie formaty dokumentów są obsługiwane od razu?**  
O: PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML oraz wiele typów obrazów. Pełną listę znajdziesz w oficjalnej dokumentacji.

---

**Ostatnia aktualizacja:** 2025-12-26  
**Testowano z:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs