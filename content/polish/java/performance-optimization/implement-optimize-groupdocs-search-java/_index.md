---
date: '2026-01-16'
description: Dowiedz się, jak przeprowadzać wyszukiwanie tekstu i optymalizować wydajność
  wyszukiwania przy użyciu GroupDocs.Search dla Javy. Zawiera kroki konfiguracji sieci
  wyszukiwania, tworzenia indeksu przeszukiwalnego oraz usuwania indeksu dokumentów.
keywords:
- GroupDocs.Search for Java
- search network optimization
- document indexing with GroupDocs
title: Wykonaj wyszukiwanie tekstu za pomocą GroupDocs.Search dla Javy
type: docs
url: /pl/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Wykonaj wyszukiwanie tekstu przy użyciu GroupDocs.Search dla Javy
## Optymalizacja wydajności

## Jak wdrożyć i zoptymalizować sieć wyszukiwania przy użyciu GroupDocs.Search dla Javy

### Wprowadzenie
W dzisiejszym świecie napędzanym danymi zdolność do **wykonywania wyszukiwania tekstowego** szybko w ogromnych kolekcjach dokumentów stanowi przewagę konkurencyjną. Niezależnie od tego, czy tworzysz wewnętrzną bazę wiedzy, repozytorium spraw prawnych, czy katalog produktów e‑commerce, dobrze dopasowana sieć wyszukiwania może znacząco poprawić satysfakcję użytkowników. W tym przewodniku dowiesz się, jak **skonfigurować sieć wyszukiwania**, **utworzyć indeks przeszukiwalny**, **optymalizować wydajność wyszukiwania**, a nawet **usunąć indeks dokumentów**, gdy zajdzie taka potrzeba — wszystko przy użyciu GroupDocs.Search dla Javy.

**Czego się nauczysz**
- Konfigurowanie sieci wyszukiwania z GroupDocs.Search  
- Wdrażanie węzłów w sieci  
- Efektywne indeksowanie dokumentów (`index documents java`)  
- Wykonywanie wyszukiwań tekstowych w sieci (`perform text search`)  
- Usuwanie wybranych dokumentów z indeksu (`delete documents index`)  

Zanurzmy się w to, jak możesz wykorzystać te funkcje, aby stworzyć zoptymalizowane doświadczenie wyszukiwania.

## Szybkie odpowiedzi
- **Jaki jest główny cel GroupDocs.Search dla Javy?** Zapewnia pełnotekstowe wyszukiwanie w wielu formatach dokumentów.  
- **Jak wykonać wyszukiwanie tekstowe w środowisku rozproszonym?** Wdrożenie sieci wyszukiwania, indeksowanie dokumentów na węźle głównym, a następnie zapytania do dowolnego węzła.  
- **Czy mogę usuwać dokumenty z indeksu bez jego ponownego budowania?** Tak, użyj API Delete, aby usunąć wybrane pliki.  
- **Jakiej wersji Javy wymaga biblioteka?** JDK 8 lub wyższa.  
- **Czy potrzebna jest licencja do produkcji?** Wymagana jest ważna licencja GroupDocs.Search; dostępna jest bezpłatna wersja próbna.

## Co to jest „perform text search”?
Wykonywanie wyszukiwania tekstowego oznacza zapytanie do pełnotekstowego indeksu w celu odnalezienia dokumentów zawierających określone słowa kluczowe lub frazy. GroupDocs.Search buduje odwrócony indeks, który umożliwia te wyszukiwania niezwykle szybko, nawet wśród tysięcy plików.

## Dlaczego warto skonfigurować sieć wyszukiwania?
Sieć wyszukiwania rozdziela zadania indeksowania i zapytań na wiele węzłów, co pozwala **optymalizować wydajność wyszukiwania**, skalować horyzontalnie i utrzymywać wysoką dostępność. Taka architektura jest idealna dla repozytoriów dokumentów na poziomie przedsiębiorstwa, gdzie istotne są opóźnienia i przepustowość.

### Wymagania wstępne
- **Wymagane biblioteki:** GroupDocs.Search dla Javy w wersji 25.4 (najnowsza).  
- **Środowisko:** Java JDK 8+, Maven.  
- **Wiedza:** Podstawowa znajomość Javy oraz koncepcji sieciowych.

### Konfiguracja GroupDocs.Search dla Javy
Aby rozpocząć, zintegrować GroupDocs.Search z projektem Java, używając poniższej konfiguracji:

#### Konfiguracja Maven
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

#### Bezpośrednie pobranie
Alternatywnie możesz [pobrać najnowszą wersję bezpośrednio z GroupDocs](https://releases.groupdocs.com/search/java/).

#### Uzyskanie licencji
GroupDocs oferuje bezpłatną wersję próbną, która pozwala ocenić funkcje przed zakupem. Tymczasową licencję możesz uzyskać, postępując zgodnie z instrukcjami na ich [stronie zakupu](https://purchase.groupdocs.com/temporary-license/). Umożliwi to pełną funkcjonalność w fazie testowej.

#### Podstawowa inicjalizacja i konfiguracja
Zainicjuj GroupDocs.Search w aplikacji Java za pomocą:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

### Przewodnik implementacji

#### Konfigurowanie sieci wyszukiwania
**Przegląd:** Ustal ścieżkę bazową i port dla sieci wyszukiwania, aby węzły mogły skutecznie się komunikować.

##### Krok 1: Definicja podstawowej konfiguracji

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parametry:**  
  - `basePath`: Ścieżka katalogu dla operacji sieciowych.  
  - `basePort`: Numer portu używanego przez sieć wyszukiwania.

##### Krok 2: Rozwiązywanie problemów
Upewnij się, że wybrany port nie jest zablokowany przez zaporę sieciową ani używany przez inną aplikację. Dostosuj go w razie potrzeby, aby uniknąć konfliktów.

#### Wdrażanie węzłów sieci wyszukiwania
**Przegląd:** Korzystając z konfiguracji, wdrażaj węzły w sieci w celu rozproszonego indeksowania i wyszukiwania.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Kluczowe opcje konfiguracji:**  
  - **Ścieżka bazowa i port:** Te wartości powinny być zgodne z tymi użytymi w początkowej konfiguracji, aby zapewnić spójność.

#### Indeksowanie dokumentów (`create searchable index`)
**Przegląd:** Dodawaj dokumenty do indeksu wyszukiwania efektywnie, używając węzła głównego.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Cel:**  
  - `masterNode`: Główny węzeł zarządzający indeksowaniem dokumentów.  
  - `documentsPath`: Ścieżka do katalogu zawierającego dokumenty.

##### Wskazówki dotyczące rozwiązywania problemów
Sprawdź, czy ścieżki do dokumentów są poprawne i dostępne. Upewnij się, że uprawnienia pozwalają na odczyt z tych katalogów.

#### Wyszukiwanie tekstu w sieci (`perform text search`)
**Przegląd:** Wykonuj kompleksowe wyszukiwania tekstowe w całej zaindeksowanej sieci.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parametry:**  
  - `query`: Tekst, którego szukasz.  
  - `masterNode`: Węzeł przeprowadzający wyszukiwanie.

#### Usuwanie dokumentów z indeksu (`delete documents index`)
**Przegląd:** Usuwaj wybrane dokumenty z indeksu, podając ich ścieżki plików.

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

- **Cel metody:**  
  - `node`: Docelowy węzeł operacji usuwania.  
  - `filePaths`: Ścieżki dokumentów do usunięcia z indeksu.

##### Rozwiązywanie problemów
Upewnij się, że ścieżki plików są dokładne i że pliki istnieją w katalogu. Jeśli problemy będą się utrzymywać, sprawdź uprawnienia sieciowe i łączność.

### Praktyczne zastosowania
1. **Zarządzanie dokumentami w przedsiębiorstwie:** Usprawnienie wewnętrznego wyszukiwania wiedzy.  
2. **Analiza spraw prawnych:** Szybkie odnajdywanie istotnych aktów w wielu repozytoriach.  
3. **Platformy e‑commerce:** Przyspieszenie wyszukiwania produktów poprzez indeksowanie opisów i recenzji.  
4. **Badania akademickie:** Efektywne przeszukiwanie dużych cyfrowych bibliotek artykułów i prac dyplomowych.  
5. **Systemy wsparcia klienta:** Skrócenie czasu odpowiedzi dzięki natychmiastowemu przeszukiwaniu poprzednich zgłoszeń.

### Wskazówki dotyczące wydajności
- **Optymalizacja szybkości indeksowania:** Dodawaj nowe dokumenty partiami w godzinach o niskim obciążeniu, aby utrzymać niskie opóźnienia.  
- **Wytyczne dotyczące zużycia zasobów:** Monitoruj CPU i pamięć, szczególnie przy zwiększaniu liczby węzłów.  
- **Zarządzanie pamięcią w Javie:** Dostosuj ustawienia sterty JVM w zależności od obciążenia (np. `-Xmx2g` dla indeksów średniej wielkości).

### Podsumowanie
Korzystając z tego przewodnika, nauczyłeś się, jak **skonfigurować sieć wyszukiwania**, **utworzyć indeks przeszukiwalny**, **wykonywać wyszukiwanie tekstowe** oraz **usuwać dokumenty z indeksu** przy użyciu GroupDocs.Search dla Javy. Te możliwości zapewniają szybkie i niezawodne wyszukiwanie dokumentów w środowiskach rozproszonych.

**Kolejne kroki**
- Eksperymentuj z różnymi konfiguracjami węzłów, aby znaleźć optymalny balans dla swojego obciążenia.  
- Zagłęb się w zaawansowane opcje indeksowania, takie jak własne analizatory i dostrajanie trafności.  
- Zbadaj integrację z innymi produktami GroupDocs w celu kompleksowego przetwarzania dokumentów.

## Najczęściej zadawane pytania

**P: Jaki jest podstawowy przypadek użycia GroupDocs.Search dla Javy?**  
O: Zapewnia pełnotekstowe wyszukiwanie w wielu formatach dokumentów, umożliwiając **wykonywanie wyszukiwania tekstowego** w dużych repozytoriach.

**P: Jak mogę zwiększyć prędkość wyszukiwania w dużej sieci?**  
O: Dodaj dodatkowe węzły, dostrój stertę JVM i zaplanuj indeksowanie w okresach niskiego ruchu, aby **optymalizować wydajność wyszukiwania**.

**P: Czy można usunąć pojedynczy dokument bez ponownego indeksowania całej kolekcji?**  
O: Tak, użyj API **delete documents index**, jak pokazano w przykładzie kodu, aby usunąć wybrane pliki.

**P: Czy potrzebna jest licencja do celów deweloperskich?**  
O: Licencja próbna wystarczy do testów; licencja komercyjna jest wymagana przy wdrożeniach produkcyjnych.

**P: Czy mogę indeksować jednocześnie PDF‑y, pliki Word i e‑maile?**  
O: Oczywiście — GroupDocs.Search obsługuje szeroką gamę formatów od razu po instalacji.

---

**Ostatnia aktualizacja:** 2026-01-16  
**Testowano z:** GroupDocs.Search dla Javy 25.4  
**Autor:** GroupDocs