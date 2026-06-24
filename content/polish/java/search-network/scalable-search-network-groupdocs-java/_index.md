---
date: '2026-05-17'
description: Dowiedz się, jak skonfigurować base port groupdocs dla skalowalnej sieci
  GroupDocs.Search Java, zoptymalizować retrieval speed i skonfigurować multi‑node
  systems.
keywords:
- configure base port groupdocs
- GroupDocs.Search Java setup
- multi‑node search configuration
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure base port groupdocs for a scalable GroupDocs.Search
    Java network, optimize retrieval speed, and set up multi‑node systems.
  headline: Configure base port groupdocs in Java Search Network
  type: TechArticle
- questions:
  - answer: Disabling stop words can improve search accuracy by retaining common terms
      that might be crucial in specialized domains.
    question: What is the purpose of disabling stop words in indexing?
  - answer: Start with a high `basePort` (e.g., 49100) and increment it for each subsequent
      node, ensuring every node has a unique TCP endpoint.
    question: How do I handle port conflicts when adding multiple nodes?
  - answer: Yes—just make sure the chosen ports are open in your cloud security groups
      and replace `127.0.0.1` with the appropriate public or private IP.
    question: Can I use this setup for cloud‑based applications?
  - answer: '`NormalIndex` offers a balanced trade‑off between speed and memory usage,
      while specialized indexes (e.g., `FastIndex`) target niche performance scenarios.'
    question: What is the difference between NormalIndex and other index types?
  - answer: Technically no; the limit is dictated by your hardware resources and network
      bandwidth.
    question: Is there a limit to the number of nodes I can add?
  type: FAQPage
title: Skonfiguruj base port groupdocs w Java Search Network
type: docs
url: /pl/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Skonfiguruj bazowy port groupdocs w sieci wyszukiwania Java

W nowoczesnych, danych‑intensywnych aplikacjach, **configure base port groupdocs** jest pierwszym krokiem do budowania szybkiej, niezawodnej infrastruktury wyszukiwania. Niezależnie od tego, czy indeksujesz tysiące plików PDF, czy rozbudowujesz się na kilka serwerów, przydzielanie unikalnych portów i katalogów zapobiega konfliktom między węzłami i utrzymuje klaster w dobrej kondycji. Ten samouczek przeprowadzi Cię przez wymagania wstępne, instalację oraz kompletną konfigurację wielowęzłową przy użyciu GroupDocs.Search dla Javy, abyś mógł uruchomić naprawdę skalowalną sieć wyszukiwania już dziś.

## Szybkie odpowiedzi
- **Jaki jest główny cel?** Przydzielenie unikalnych portów i podstawowych katalogów dla każdego węzła wyszukiwania, eliminując konflikty.  
- **Czy potrzebuję licencji?** Tak – wymagana jest licencja próbna lub pełna do wdrożeń produkcyjnych.  
- **Która wersja Javy jest wspierana?** Java 8 lub wyższa (zalecane Java 11+).  
- **Czy mogę uruchomić to na serwerach w chmurze?** Absolutnie – wystarczy otworzyć wybrane porty w grupach zabezpieczeń chmury.  
- **Ile węzłów mogę dodać?** Brak sztywnego limitu; ograniczenia wynikają jedynie z zasobów sprzętowych i przepustowości sieci.

## Czym jest „configure base port groupdocs”?

**Configure base port groupdocs** to proces przydzielania początkowego portu TCP, którego będzie używać każdy węzeł wyszukiwania i zwiększania go dla kolejnych węzłów. Ten prosty krok eliminuje niechciane błędy „port już w użyciu” i tworzy podstawy czystego, poziomo‑skalowalnego klastra wyszukiwania, zapewniając, że każdy węzeł komunikuje się przez odrębny punkt końcowy.

## Dlaczego używać GroupDocs.Search w skalowalnej sieci?

GroupDocs.Search zapewnia **wysoką wydajność indeksowania** (do 50 GB/min na standardowym serwerze 8‑rdzeniowym) i obsługuje **ponad 50 formatów plików** w tym PDF, DOCX, PPTX i HTML. Jego modularna architektura pozwala mieszać indeksatory, wyszukiwarki, fragmenty i ekstraktory między węzłami, zapewniając liniową skalowalność w miarę dodawania sprzętu. Biblioteka oferuje również wbudowane opcje kompresji, które zmniejszają zużycie dysku nawet o 70 %, jednocześnie utrzymując opóźnienie zapytań poniżej 200 ms przy typowych obciążeniach.

## Wymagania wstępne
- **Java Development Kit (JDK)** 8 lub nowszy (zalecane Java 11+ dla lepszej kolekcji śmieci).  
- **IDE** takie jak IntelliJ IDEA lub Eclipse.  
- **GroupDocs.Search for Java** library (wersja 25.4 lub późniejsza) zainstalowana przez Maven lub ręczne pobranie.  
- Podstawowa wiedza o sieciach (porty TCP, localhost vs. zdalne hosty).  
- Ważna licencja **GroupDocs.Search** (próbna lub pełna).

## Konfiguracja GroupDocs.Search dla Javy

### Instrukcje instalacji

**Ustawienia Maven:**

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

**Bezpośrednie pobranie:**  
Alternatywnie, pobierz najnowszą wersję z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji

- **Free Trial** – rozpocznij testowanie od razu.  
- **Temporary License** – uzyskaj wydłużony okres próbny pod adresem [Temporary License](https://purchase.groupdocs.com/temporary-license).  
- **Full Purchase** – wymagane do wdrożeń produkcyjnych.

### Podstawowa inicjalizacja i konfiguracja

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## Przewodnik wdrożeniowy

### Jak skonfigurować bazowy port groupdocs?

Aby skonfigurować bazowy port, edytuj plik konfiguracji sieci lub programowo ustaw właściwość `basePort` na wysoką, niewykorzystaną wartość, np. 49100. Dla każdego kolejnego węzła zwiększaj numer portu o jeden (lub o stały offset), aby każdy węzeł wiązał się z własnym odrębnym punktem końcowym TCP, eliminując błędy kolizji portów i upraszczając reguły zapory.

#### Konfiguracja ścieżek bazowych

Zanim napiszesz jakikolwiek kod, zdecyduj o spójnym układzie folderów. Na przykład, utwórz osobne katalogi dla indeksatorów (`Indexer0`), wyszukiwarek (`Searcher0`) i ekstraktorów (`Extractor0`). Taka struktura pozwala każdemu węzłowi szybko odnajdywać swoje pliki.

- **Dlaczego**: Przewidywalna hierarchia katalogów zapobiega błędom „plik nie znaleziony” podczas uruchamiania węzłów na różnych maszynach.

#### Konfiguracja bazowego portu

Wybierz wysoki port początkowy, aby uniknąć konfliktów ze standardowymi usługami (HTTP 80, SSH 22 itp.). Zwiększaj numer portu dla każdego nowego węzła, który dodajesz.

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Dlaczego**: Rozpoczęcie od wysokiego portu (np. 49100) zmniejsza ryzyko kolizji z istniejącymi usługami i upraszcza tworzenie reguł zapory.

#### Definiowanie adresu hosta

Podczas rozwoju, `localhost` działa poprawnie. W produkcji zastąp go adresem IP serwera lub nazwą DNS, aby zdalne węzły mogły się ze sobą komunikować.

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Dlaczego**: Użycie rzeczywistego adresu hosta umożliwia komunikację między maszynami, co jest niezbędne w klastrach w chmurze lub on‑premise.

#### Tworzenie konfiguracji sieciowej

Klasa `NetworkConfig` łączy wszystkie opcje sieciowe — bazowy port, host oraz opcjonalne ustawienia SSL — w jeden obiekt, który jest wykorzystywany przez silnik wyszukiwania.

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Dlaczego**: Centralizacja tych opcji sprawia, że konfiguracja jest wielokrotnego użytku i łatwiejsza w utrzymaniu na wielu węzłach.

#### Dodawanie węzłów

`SearchNode` reprezentuje pojedynczy węzeł w klastrze GroupDocs.Search, który wykonuje określoną funkcję, taką jak indeksowanie lub wyszukiwanie. Utwórz instancję `SearchNode` dla każdej roli (indeksator, wyszukiwarka, ekstraktor) i zarejestruj ją w `SearchEngine`. Rozdzielenie obowiązków między węzłami zwiększa równoległość i odporność na awarie.

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Dlaczego**: Rozdzielenie pracy na dedykowane węzły zmniejsza rywalizację o zasoby i pozwala każdej maszynie specjalizować się w jednej czynności, zwiększając ogólną przepustowość.

#### Finalizacja konfiguracji

Po dodaniu wszystkich węzłów, wywołaj `engine.start()`, aby uruchomić sieć. Silnik automatycznie przypisze każdy węzeł do przydzielonego portu i zweryfikuje łączność.

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Typowe problemy i rozwiązania

- **Konflikty portów** – Zawsze zwiększaj `basePort` dla każdego nowego węzła. Sprawdzaj otwarte porty przy użyciu `netstat` lub monitoru sieciowego systemu operacyjnego.  
- **Brakujące katalogi** – Upewnij się, że każdy folder (`Indexer0`, `Searcher0` itp.) istnieje i proces Java ma uprawnienia odczytu/zapisu.  
- **Dostępność sieci** – Przechodząc do konfiguracji wielomaszynowej, zamień `127.0.0.1` na rzeczywisty adres IP hosta i otwórz wybrane porty w zaporach.  

## Praktyczne zastosowania

| Scenariusz | Korzyść z konfiguracji bazowego portu groupdocs |
|------------|-------------------------------------------------|
| Zarządzanie dokumentami w przedsiębiorstwie | Bezproblemowe skalowanie w całych działach bez przestojów |
| Duże platformy CMS | Szybsze pobieranie treści dzięki rozproszeniu indeksu |
| Zarządzanie sprawami prawnymi | Równoległe wyodrębnianie PDF‑ów zmniejsza opóźnienia wyszukiwania |

## Rozważania dotyczące wydajności

- **Monitorowanie CPU/pamięci** – Użyj JMX Javy lub narzędzia profilującego, aby obserwować zużycie wątków.  
- **Dostosowanie kompresji** – `Compression.High` oszczędza miejsce na dysku, ale może zwiększyć obciążenie CPU; przetestuj zarówno `High`, jak i `Normal`, aby znaleźć optymalne ustawienie.  
- **Regularne aktualizacje** – Nowe wydania GroupDocs.Search często zawierają poprawki wydajności; utrzymuj bibliotekę w aktualnej wersji.

## Zakończenie

Teraz wiesz, jak **configure base port groupdocs** i skonfigurować wielowęzłową sieć wyszukiwania przy użyciu GroupDocs.Search dla Javy. Eksperymentuj z dodatkowymi węzłami, dopasuj ustawienia indeksu i zintegrować sieć z istniejącymi aplikacjami, aby uzyskać naprawdę skalowalne rozwiązanie wyszukiwania.

## Najczęściej zadawane pytania

**Q: Jaki jest cel wyłączania słów stop w indeksowaniu?**  
A: Wyłączenie słów stop może poprawić dokładność wyszukiwania, zachowując powszechne terminy, które mogą być kluczowe w specjalistycznych dziedzinach.

**Q: Jak radzić sobie z konfliktami portów przy dodawaniu wielu węzłów?**  
A: Rozpocznij od wysokiego `basePort` (np. 49100) i zwiększaj go dla każdego kolejnego węzła, zapewniając, że każdy węzeł ma unikalny punkt końcowy TCP.

**Q: Czy mogę używać tej konfiguracji w aplikacjach opartych na chmurze?**  
A: Tak — upewnij się, że wybrane porty są otwarte w grupach zabezpieczeń chmury i zamień `127.0.0.1` na odpowiedni publiczny lub prywatny adres IP.

**Q: Jaka jest różnica między NormalIndex a innymi typami indeksów?**  
A: `NormalIndex` zapewnia zrównoważony kompromis między szybkością a zużyciem pamięci, podczas gdy specjalistyczne indeksy (np. `FastIndex`) są przeznaczone do specyficznych scenariuszy wydajnościowych.

**Q: Czy istnieje limit liczby węzłów, które mogę dodać?**  
A: Technicznie nie; limit zależy od zasobów sprzętowych i przepustowości sieci.

---

**Ostatnia aktualizacja:** 2026-05-17  
**Testowano z:** GroupDocs.Search Java 25.4  
**Autor:** GroupDocs

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

## Powiązane samouczki

- [Jak skonfigurować sieć wyszukiwania .NET przy użyciu GroupDocs.Search i Redaction](/search/net/search-network/configure-net-search-network-groupdocs/)
- [Jak wdrożyć sieć wyszukiwania z GroupDocs.Search w .NET dla systemów zarządzania dokumentami](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Wdrożenie węzła sieci wyszukiwania w .NET przy użyciu GroupDocs dla efektywnego indeksowania i wyszukiwania dokumentów](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)