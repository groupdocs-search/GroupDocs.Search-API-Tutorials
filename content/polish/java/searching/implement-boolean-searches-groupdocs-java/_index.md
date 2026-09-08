---
date: '2026-07-21'
description: Samouczek Tworzenie zapytania Boolean w Javie pokazuje, jak wdrożyć wyszukiwania
  boolean AND, OR, NOT przy użyciu GroupDocs.Search dla Javy, dodać dokumenty do indeksu
  i zwiększyć skuteczność wyszukiwania dokumentów.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Samouczek Tworzenie zapytania Boolean w Javie wyjaśnia krok po kroku,
  jak tworzyć zapytania AND, OR, NOT przy użyciu GroupDocs.Search dla Javy, dodać
  dokumenty do indeksu i poprawić wydajność wyszukiwania.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Tworzenie zapytania Boolean w Javie – Opanuj wyszukiwania Boolean z GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Tworzenie zapytania Boolean w Javie: Opanuj wyszukiwania Boolean z GroupDocs.Search
  dla Javy'
type: docs
url: /pl/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Utwórz zapytanie Boolean w Javie: Opanuj wyszukiwania Boolean z GroupDocs.Search dla Javy

Wyszukiwanie ogromnych zbiorów dokumentów może przypominać szukanie igły w stogu siana. **Create Boolean Query Java** pozwala precyzyjnie określić, czego potrzebujesz — dokumentów zawierających *obie* terminy, *dowolny* z nich lub *wykluczających* niechciane słowa. W tym przewodniku przeprowadzimy Cię przez konfigurację **GroupDocs.Search for Java**, dodawanie dokumentów do indeksu oraz tworzenie potężnych zapytań Boolean, które usprawnią Twoje procesy **document retrieval java**. Po zakończeniu będziesz w stanie napisać czysty, łatwy w utrzymaniu kod, który tworzy zapytania Boolean w Javie w kilku linijkach.

## Szybkie odpowiedzi
- **Czym jest zapytanie boolean AND?** Zwraca tylko dokumenty, które zawierają *wszystkie* określone terminy.  
- **Jak różni się OR od AND?** OR dopasowuje dokumenty zawierające *dowolny* z terminów, rozszerzając zestaw wyników.  
- **Kiedy używać NOT?** Użyj NOT, aby odfiltrować dokumenty zawierające niechciane słowa.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna wystarcza do testów; licencja komercyjna jest wymagana w produkcji.  
- **Jaka wersja Javy jest wymagana?** Obsługiwana jest Java 8+; zalecany jest JDK 11+.

## Co to jest **create boolean query java**?
`create boolean query java` odnosi się do konstruowania zapytania wyszukiwania w Javie, które łączy operatory logiczne takie jak AND, OR i NOT przy użyciu API GroupDocs.Search. Poprzez składanie tych operatorów możesz precyzyjnie kontrolować, które dokumenty pasują, umożliwiając zaawansowane filtrowanie, dostrajanie trafności oraz złożone scenariusze wyszukiwania.

## Dlaczego warto używać GroupDocs.Search dla Javy?
- **Wysoka wydajność** przy dużych zestawach dokumentów – potrafi indeksować i przeszukiwać 500 GB tekstu w mniej niż minutę na standardowym serwerze.  
- **Bogate API**, które obsługuje zarówno zapytania oparte na tekście, jak i oparte na obiektach, pozwalając wybrać styl pasujący do Twojej architektury.  
- **Wbudowane wsparcie językowe** dla stemmingu, słów stop i dopasowań przybliżonych w ponad 30 językach.  
- **Łatwa integracja** z Mavenem lub bezpośrednim pobraniem JAR, wymagająca tylko kilku linii kodu, aby rozpocząć.

## Wymagania wstępne
Zanim zanurzysz się w temat, upewnij się, że masz:
- **GroupDocs.Search for Java** (v25.4 lub nowszy) – zobacz link do pobrania poniżej.  
- Zainstalowany JDK 8+ i skonfigurowany w IDE (IntelliJ IDEA, Eclipse itp.).  
- Podstawową znajomość Javy oraz Maven do zarządzania zależnościami.  

## Konfiguracja GroupDocs.Search dla Javy

### Konfiguracja Maven
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

### Bezpośrednie pobranie
Alternatywnie, pobierz najnowszy JAR z oficjalnej strony: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
Rozpocznij od darmowej licencji próbnej, aby wypróbować wszystkie funkcje. W środowisku produkcyjnym zakup licencję komercyjną, aby odblokować pełną funkcjonalność.

### Podstawowa inicjalizacja i konfiguracja
Utwórz folder indeksu i zainicjalizuj obiekt `Index`:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## Jak utworzyć zapytanie boolean w Javie?
`Index` reprezentuje kolekcję dokumentów przechowywaną na dysku, którą można przeszukiwać. `BooleanQuery` łączy wiele podzapytń przy użyciu operatorów logicznych. `createAndQuery`, `createOrQuery` i `createNotQuery` tworzą odpowiednio podzapytania AND, OR i NOT. Załaduj lub utwórz instancję `Index`, dodaj dokumenty, a następnie zbuduj obiekt `BooleanQuery` używając `createAndQuery`, `createOrQuery` lub `createNotQuery`. Wywołaj `index.search(query)`, aby uzyskać pasujące dokumenty. Ten wzorzec działa zarówno w prostych, jak i złożonych scenariuszach i wymaga tylko trzech logicznych kroków: inicjalizacji indeksu, dodania dokumentów i wykonania zapytania.

## Wyszukiwanie Boolean AND

### Przegląd
Zapytanie AND zawęża wyniki, zwiększając trafność, gdy potrzebujesz dokumentów spełniających wiele kryteriów.

### Kroki implementacji
1. **Inicjalizacja indeksu** – to także demonstruje **dodawanie dokumentów do indeksu** w scenariuszu AND.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Indeksowanie dokumentów**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Wykonaj wyszukiwanie zapytaniem tekstowym** – używając składni zwykłego ciągu znaków.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Wykonaj wyszukiwanie zapytaniem obiektowym** – przydatne przy programowym budowaniu zapytań (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Wyszukiwanie Boolean OR

### Przegląd
Zapytanie OR jest idealne dla poszukiwań eksploracyjnych, gdy chcesz uchwycić dokumenty zawierające przynajmniej jedno z kilku słów kluczowych (**search with or java**).

### Kroki implementacji
1. **Inicjalizacja indeksu**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Indeksowanie dokumentów**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Wykonaj wyszukiwanie zapytaniem tekstowym**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Wykonaj wyszukiwanie zapytaniem obiektowym**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Wyszukiwanie Boolean NOT

### Przegląd
Zapytanie NOT pomaga wyeliminować nieistotne dokumenty, np. odfiltrować nazwę marki konkurenta (**boolean search examples java**).

### Kroki implementacji
1. **Inicjalizacja indeksu**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Indeksowanie dokumentów**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Wykonaj wyszukiwanie zapytaniem tekstowym**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Wykonaj wyszukiwanie zapytaniem obiektowym**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## Złożone zapytania Boolean

### Przegląd
Złożone zapytania pozwalają modelować rzeczywiste scenariusze wyszukiwania, takie jak „znajdź artykuły sportowe, które są pozytywne, ale wyklucz wszelkie wzmianki o konkretnych sportowcach”.

### Kroki implementacji
1. **Inicjalizacja indeksu**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Indeksowanie dokumentów**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Wykonaj wyszukiwanie zapytaniem tekstowym**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Wykonaj wyszukiwanie zapytaniem obiektowym**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## Praktyczne zastosowania zapytań **java boolean and or**
- **Systemy zarządzania dokumentami** – znajdź umowy zawierające zarówno „confidential” **AND** „renewal”.  
- **Badania prawne** – filtruj orzecznictwo przy użyciu **AND**/**OR**, jednocześnie wykluczając przestarzałe ustawy za pomocą **NOT**.  
- **Wsparcie klienta** – pobierz zgłoszenia, które wspominają „login” **AND** „error”, ale nie „resolved”.  
- **Kuratela treści** – zbierz wpisy na blogu o „cloud” **OR** „serverless” do newslettera.

## Częste pułapki i rozwiązywanie problemów
- **Brak odświeżenia indeksu** – po dodaniu nowych dokumentów wywołaj `index.update()`, aby zapewnić ich możliwość przeszukiwania.  
- **Nieprawidłowe odstępy operatorów** – GroupDocs.Search oczekuje spacji wokół operatorów (`AND`, `OR`, `NOT`).  
- **Rozróżnianie wielkości liter** – zapytania są domyślnie niewrażliwe na wielkość liter, ale własne analizatory mogą to zmienić.  
- **Duże zestawy wyników** – używaj paginacji (`search(query, 0, 100)`), aby uniknąć przeciążenia pamięci.  

## Najczęściej zadawane pytania

**Q: Czy mogę połączyć więcej niż dwa terminy w zapytaniu AND?**  
A: Oczywiście. Możesz łańcuchowo połączyć wiele obiektów `createWordQuery` przy użyciu `createAndQuery`, lub po prostu napisać `"term1 AND term2 AND term3"` w zapytaniu tekstowym.

**Q: Czy GroupDocs.Search obsługuje wyszukiwania z wildcardami lub przybliżone?**  
A: Tak. Dodaj `*` jako wildcard (np. `promot*`) lub użyj `~` dla dopasowania przybliżonego (np. `comfort~`).

**Q: Jak ograniczyć wyszukiwanie do określonych typów plików?**  
`FileTypeQuery` ogranicza wyniki wyszukiwania do konkretnych formatów plików, takich jak PDF lub DOCX.  
A: Użyj klasy `FileTypeQuery`, aby ograniczyć wyniki do PDF, DOCX itp., i połącz ją ze swoim zapytaniem Boolean.

**Q: Jaki jest najlepszy sposób monitorowania wydajności indeksowania?**  
A: Włącz wbudowany logger (`index.getLogger().setLevel(Level.INFO)`) i przejrzyj metryki czasowe po każdej operacji `add`.

**Q: Czy istnieje sposób na zwiększenie istotności niektórych terminów?**  
`BoostQuery` podnosi wynik trafności określonych terminów w zapytaniu wyszukiwania.  
A: Tak. Otocz ważne słowa klasą `BoostQuery`, aby zwiększyć ich wagę w algorytmie punktacji.

---

**Ostatnia aktualizacja:** 2026-07-21  
**Testowano z:** GroupDocs.Search 25.4 (Java)  
**Autor:** GroupDocs

## Powiązane samouczki

- [Boolean Operators Java – Create Search Index & Faceted Search](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Master GroupDocs.Search Java&#58; Efficient Document Search and Index Management](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - Mastering GroupDocs.Search Java – Create and Manage a Search Index](/search/java/indexing/groupdocs-search-java-create-index-guide/)