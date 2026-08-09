---
date: '2026-07-02'
description: Dowiedz się, jak uzyskać tymczasową licencję dla GroupDocs.Search, dodać
  katalogi do indeksu oraz dodać niestandardowe atrybuty dokumentów, zarządzając Java
  search network nodes.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Uzyskaj tymczasową licencję GroupDocs – Master Search Nodes (Java)
type: docs
url: /pl/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Uzyskaj tymczasową licencję GroupDocs – Główne węzły wyszukiwania (Java)

W tym kompleksowym przewodniku **uzyskasz tymczasową licencję dla GroupDocs.Search**, skonfigurujesz wielowęzłową sieć wyszukiwania i nauczysz się **dodawać katalogi do indeksu** oraz **dodawać niestandardowe atrybuty dokumentów** przy użyciu Javy. Niezależnie od tego, czy budujesz system zarządzania dokumentami w przedsiębiorstwie, czy przeszukiwalny katalog produktów, opanowanie tych kroków pozwoli Ci ocenić platformę bez ograniczeń i szybko skalować możliwości wyszukiwania.

## Szybkie odpowiedzi
- **Jaki jest pierwszy krok, aby rozpocząć korzystanie z GroupDocs.Search?** Uzyskaj tymczasową licencję z portalu GroupDocs.  
- **Które repozytorium Maven zawiera bibliotekę?** `https://releases.groupdocs.com/search/java/`.  
- **Jak dodać katalogi do indeksu?** Wywołaj pomocniczą metodę `addDirectoriesToIndex` na węźle głównym.  
- **Czy mogę dodać niestandardowe atrybuty dokumentów?** Tak — wywołaj `addAttribute` z kluczem dokumentu i nazwą atrybutu.  
- **Jak prawidłowo zamknąć węzły?** Wywołaj `closeNodes`, aby zwolnić zasoby.

## Czym jest tymczasowa licencja i dlaczego jej potrzebuję?
Tymczasowa licencja pozwala ocenić GroupDocs.Search bez żadnych ograniczeń ewaluacyjnych. Jest idealna do projektów rozwojowych, testowych lub proof‑of‑concept przed podjęciem decyzji o pełnym zakupie. Licencja zapewnia pełny dostęp do funkcji przez ograniczony czas, umożliwiając benchmarkowanie wydajności, testowanie punktów integracji i zapewnienie, że rozwiązanie spełnia Twoje wymagania bez zobowiązań finansowych.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że spełniasz następujące wymagania:

### Wymagane biblioteki i zależności
Aby pracować z GroupDocs.Search dla Javy, dołącz niezbędne zależności Maven:
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
Możesz również pobrać najnowszą wersję bezpośrednio z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Konfiguracja środowiska
- Upewnij się, że masz zainstalowane kompatybilne JDK (Java 8 lub nowsze).  
- Skonfiguruj swoje IDE, aby obsługiwało projekty Maven.

### Wymagania wiedzy
Podstawowa znajomość programowania w Javie oraz doświadczenie w zarządzaniu projektami Maven będą przydatne. Jeśli jesteś nowy w tych koncepcjach, rozważ zapoznanie się z materiałami wprowadzającymi, aby rozpocząć.

## Jak uzyskać tymczasową licencję
Tymczasową licencję uzyskuje się, odwiedzając portal GroupDocs, wypełniając krótki formularz zgłoszeniowy i umieszczając otrzymany plik `.lic` w folderze `resources` projektu. Następnie zainicjalizuj licencję kilkoma liniami kodu (zobacz fragment poniżej). Do formularza użyj oficjalnej strony: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## Konfiguracja GroupDocs.Search dla Javy

### Informacje o instalacji
Aby rozpocząć korzystanie z GroupDocs.Search dla Javy w swoim projekcie, postępuj zgodnie z powyższymi krokami Maven lub pobierz najnowszą wersję bezpośrednio ze strony oficjalnych wydań.

#### Kroki uzyskania licencji
1. **Free Trial** – Przeglądaj funkcje bez zobowiązań.  
2. **Temporary License** – Uzyskaj krótkoterminowy klucz do testów (zobacz sekcję powyżej).  
3. **Purchase** – Do użytku produkcyjnego kup pełną licencję na **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)**.

### Podstawowa inicjalizacja i konfiguracja
Zainicjalizuj swój projekt z GroupDocs.Search w następujący sposób:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Ten krok inicjalizacji jest kluczowy, aby zapewnić płynne działanie wszystkich komponentów w sieci wyszukiwania.

## Przewodnik implementacji
Teraz podzielmy proces na przystępne sekcje, z których każda koncentruje się na konkretnej funkcji wdrażania i zarządzania węzłami sieci wyszukiwania.

### Funkcja 1: Konfiguracja ustawień
**Przegląd:** Konfiguracja sieci wyszukiwania jest pierwszym krokiem przy wdrażaniu węzłów. Ustawienie to obejmuje określenie ścieżek i portów niezbędnych do wdrożenia węzła.

#### Kroki implementacji:
##### Krok 1: Zdefiniuj bazową ścieżkę i port
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Krok 2: Skonfiguruj sieć wyszukiwania
Funkcja `configureSearchNetwork` przygotowuje obiekt konfiguracji niezbędny do wdrażania węzłów.  
`Configuration` to klasa przechowująca wszystkie ustawienia, takie jak folder indeksu, porty sieciowe i role węzłów.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parametry:** Bazowa ścieżka i port są używane do lokalizacji zasobów i ustanawiania kanałów komunikacji.  
- **Wartość zwracana:** Skonfigurowany obiekt `Configuration` dostosowany do potrzeb wdrożenia.

### Funkcja 2: Wdrożenie sieci wyszukiwania
**Przegląd:** Wdrażanie węzłów jest niezbędne do skalowania możliwości wyszukiwania w różnych środowiskach lub segmentach danych.

#### Kroki implementacji:
##### Krok 1: Wdrożenie węzłów
Funkcja `deploySearchNetwork` inicjalizuje i zwraca tablicę węzłów sieci wyszukiwania.  
`SearchNetworkNodes` reprezentuje każdą instancję węzła uczestniczącego w rozproszonym klastrze wyszukiwania.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parametry:** Bazowa ścieżka, port i konfiguracja są używane do określenia środowiska wdrożenia.  
- **Wartość zwracana:** Tablica zawierająca zainicjalizowane `SearchNetworkNodes`.

### Funkcja 3: Subskrypcja zdarzeń sieci
**Przegląd:** Monitorowanie działań sieci wyszukiwania jest kluczowe dla utrzymania optymalnej wydajności i niezawodności.

#### Kroki implementacji:
##### Krok 1: Subskrybuj zdarzenia węzła głównego
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Cel:** Ten krok zapewnia powiadomienia o istotnych zdarzeniach lub zmianach w sieci wyszukiwania.

### Funkcja 4: Indeksowanie dokumentów
**Przegląd:** Dodawanie katalogów zawierających dokumenty do indeksowania umożliwia efektywne wyszukiwanie danych w całej sieci.

#### Jak dodać katalogi do indeksu
`addDirectoriesToIndex` to metoda pomocnicza rejestrująca ścieżki folderów do indeksowania na węźle głównym.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Cel:** Umożliwia szybki dostęp i możliwość przeszukiwania wszystkich dokumentów w określonych katalogach.

### Funkcja 5: Dodawanie atrybutów do dokumentów
**Przegląd:** Niestandardowe atrybuty wzbogacają metadane dokumentów, czyniąc wyszukiwania bardziej elastycznymi i informacyjnymi.

#### Jak dodać niestandardowe atrybuty dokumentów
`addAttribute` dodaje niestandardowy atrybut metadanych do określonego dokumentu w indeksie.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parametry:** Określ węzeł, klucz dokumentu oraz atrybut do dodania.  
- **Cel:** Rozszerza funkcjonalność wyszukiwania poprzez wzbogacenie dokumentów o dodatkowe metadane.

### Funkcja 6: Pobieranie zindeksowanych dokumentów
**Przegląd:** Efektywne pobieranie i wyświetlanie zindeksowanych dokumentów zapewnia dokładność i kompletność danych.

#### Kroki implementacji:
##### Krok 1: Pobierz zindeksowane dokumenty
```java
getIndexedDocuments(nodes[0]);
```  
- **Cel:** Weryfikuje pomyślne indeksowanie wszystkich niezbędnych dokumentów w sieci wyszukiwania.

### Funkcja 7: Zamykanie węzłów sieci
**Przegląd:** Prawidłowe zamykanie węzłów jest kluczowe dla zarządzania zasobami i zapobiegania wyciekom pamięci.

#### Kroki implementacji:
##### Krok 1: Zamknij wszystkie węzły
`closeNodes` wyłącza wszystkie aktywne węzły wyszukiwania i zwalnia przydzielone zasoby.  
```java
closeNodes(nodes);
```  
- **Cel:** Zwalnia zasoby zajęte przez każdy węzeł, zapewniając czysty proces zamykania.

## Dlaczego warto używać tymczasowej licencji dla GroupDocs.Search?
Tymczasowa licencja zapewnia **pełny dostęp do funkcji przez 30 dni** i obsługuje do **50 000 zindeksowanych dokumentów** bez ograniczeń wydajności. Pozwala to na benchmarkowanie szybkości indeksowania, opóźnień zapytań i skalowalności na rzeczywistych danych przed zakupem licencji produkcyjnej. Usuwa również znaki wodne ewaluacji, dając prawdziwy obraz możliwości końcowego produktu.

## Typowe przypadki użycia
1. **Enterprise Document Management** – Indeksuj miliony wewnętrznych plików w różnych działach, umożliwiając natychmiastowe wyszukiwanie pełnotekstowe.  
2. **E‑commerce Platforms** – Zbuduj przeszukiwalny katalog produktów obejmujący wiele magazynów i zewnętrzne źródła danych.  
3. **Legal Firms** – Organizuj akta spraw, umowy i dowody z niestandardowymi metadanymi dla szybkiego odnajdywania.

Możliwości integracji z innymi systemami obejmują platformy CRM, systemy zarządzania treścią (CMS) oraz narzędzia analityki danych, wykorzystując solidne funkcje indeksowania i wyszukiwania oferowane przez GroupDocs.Search dla Javy.

## Wskazówki dotyczące wydajności
Aby zoptymalizować wydajność przy użyciu GroupDocs.Search dla Javy:
- **Optymalizacja konfiguracji** – Dostosuj ustawienia konfiguracji do konkretnego środowiska wdrożeniowego.  
- **Monitorowanie zużycia zasobów** – Regularnie sprawdzaj CPU, pamięć i I/O, aby zapobiegać wąskim gardłom lub wyciekom pamięci.  
- **Stosowanie najlepszych praktyk** – Przestrzegaj wytycznych dotyczących zarządzania pamięcią w Javie, zapewniając efektywne wykorzystanie zasobów systemowych.

## Najczęściej zadawane pytania

**P: Jak długo obowiązuje tymczasowa licencja?**  
O: Tymczasowe licencje zazwyczaj są ważne przez 30 dni, dając wystarczająco dużo czasu na ocenę produktu.

**P: Czy mogę przejść z tymczasowej licencji na pełną bez ponownej instalacji?**  
O: Tak — zamień plik tymczasowej licencji na plik pełnej licencji i uruchom ponownie aplikację.

**P: Czy po zastosowaniu nowej licencji muszę ponownie indeksować dokumenty?**  
O: Nie, indeks pozostaje nienaruszony; licencja reguluje jedynie prawa użytkowania.

**P: Co się stanie, jeśli zapomnę zamknąć węzły?**  
O: Niezwolnione zasoby mogą prowadzić do wycieków pamięci; zawsze wywołuj `closeNodes` podczas zamykania.

**P: Czy można dodać więcej niż jeden niestandardowy atrybut do dokumentu?**  
O: Oczywiście — wywołaj `addAttribute` wielokrotnie z różnymi nazwami atrybutów.

**Ostatnia aktualizacja:** 2026-07-02  
**Testowano z:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs

## Powiązane samouczki

- [Wdrożenie węzła sieci wyszukiwania w .NET przy użyciu GroupDocs dla efektywnego indeksowania i pobierania dokumentów](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Jak zaimplementować sieć wyszukiwania z GroupDocs.Search w .NET dla systemów zarządzania dokumentami](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Konfiguracja sieci Aspose.Search i dodawanie atrybutów dokumentów z GroupDocs.Redaction dla .NET: Kompletny przewodnik](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)