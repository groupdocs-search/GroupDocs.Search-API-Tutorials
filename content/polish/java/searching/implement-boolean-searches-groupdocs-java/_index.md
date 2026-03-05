---
date: '2026-01-29'
description: Dowiedz się, jak implementować zapytania boolean AND/OR w języku Java
  przy użyciu GroupDocs.Search for Java, dodawać dokumenty do indeksu i usprawniać
  wyszukiwanie dokumentów.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'java boolean and or: Mistrzowskie wyszukiwania Boolean w GroupDocs.Search
  dla Javy'
type: docs
url: /pl/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: Mistrzowskie wyszukiwania Boolean w GroupDocs.Search dla Java

Wyszukiwanie w ogromnych zbiorach dokumentów może przypominać szukanie igły w stogu siana. Dzięki zapytaniom **java boolean and or** możesz precyzyjnie określić, czego potrzebujesz — dokumentów zawierających *obie* frazy, *dowolną* z nich lub wykluczających niepożądane słowa. W tym przewodniku przeprowadzimy Cię przez konfigurację **GroupDocs.Search for Java**, dodawanie dokumentów do indeksu oraz tworzenie potężnych zapytań Boolean, które przyspieszą Twoje **document retrieval java** procesy.

## Szybkie odpowiedzi
- **Czym jest zapytanie Boolean AND?** Zwraca wyłącznie dokumenty, które zawierają *wszystkie* określone terminy.  
- **Jak różni się OR od AND?** OR dopasowuje dokumenty zawierające *dowolny* z terminów, rozszerzając zestaw wyników.  
- **Kiedy używać NOT?** Użyj NOT, aby odfiltrować dokumenty zawierające niechciane słowa.  
- **Czy potrzebna jest licencja?** Bezpłatna wersja próbna wystarczy do testów; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Jakiej wersji Javy wymaga?** Obsługiwana jest Java 8+; zalecana jest JDK 11+.

## Co to jest **java boolean and or**?
Zapytanie **java boolean and or** łączy operatory logiczne (AND, OR, NOT), aby doprecyzować wyniki wyszukiwania. Strukturyzując zapytania, informujesz GroupDocs.Search, jak terminy mają się do siebie odnosić, uzyskując precyzyjną kontrolę nad procesem pobierania.

## Dlaczego warto używać GroupDocs.Search dla Java?
- **Wysoka wydajność** przy dużych zestawach dokumentów.  
- **Bogate API**, które obsługuje zarówno zapytania tekstowe, jak i oparte na obiektach.  
- **Wbudowane wsparcie językowe** dla stemmingu, słów stop i dopasowań przybliżonych.  
- **Łatwa integracja** z Mavenem lub bezpośrednim pobraniem JAR‑a.

## Wymagania wstępne
Zanim rozpoczniesz, upewnij się, że masz:

- **GroupDocs.Search for Java** (v25.4 lub nowszy) – link do pobrania znajduje się poniżej.  
- Zainstalowaną i skonfigurowaną JDK 8+ w swoim IDE (IntelliJ IDEA, Eclipse itp.).  
- Podstawową znajomość Javy oraz Maven do zarządzania zależnościami.  

## Konfiguracja GroupDocs.Search dla Java

### Konfiguracja Maven
Dodaj repozytorium i zależność do swojego pliku `pom.xml`:

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
Alternatywnie pobierz najnowszy JAR ze strony: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
Rozpocznij od bezpłatnej licencji próbnej, aby przetestować wszystkie funkcje. W środowisku produkcyjnym zakup licencję komercyjną, aby odblokować pełną funkcjonalność.

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

## java boolean and or: Implementacja wyszukiwań Boolean

Poniżej omówimy **AND**, **OR**, **NOT** oraz **złożone** zapytania. Każda sekcja prezentuje zarówno zapytanie w formie tekstowej, jak i równoważne zapytanie oparte na obiektach, dzięki czemu możesz wybrać styl pasujący do Twojego kodu.

### Wyszukiwanie Boolean AND
Połącz terminy przy użyciu **AND**, aby otrzymać wyłącznie dokumenty zawierające *wszystkie* słowa kluczowe.

#### Przegląd
Zapytanie AND zawęża wyniki, zwiększając trafność, gdy potrzebujesz dokumentów spełniających wiele kryteriów.

#### Kroki implementacji

1. **Inicjalizacja indeksu** – jednocześnie pokazuje, jak **add documents to index** w scenariuszu AND.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Indeksowanie dokumentów**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Wykonanie wyszukiwania tekstowego** – przy użyciu składni zwykłego ciągu znaków.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Wykonanie wyszukiwania obiektowego** – przydatne przy budowaniu zapytań programowo (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### Wyszukiwanie Boolean OR
Użyj **OR**, aby poszerzyć wyniki, dopasowując dowolny z podanych terminów.

#### Przegląd
Zapytanie OR jest idealne dla poszukiwań eksploracyjnych, gdy chcesz uchwycić dokumenty zawierające przynajmniej jedno z kilku słów kluczowych (**search with or java**).

#### Kroki implementacji

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

3. **Wykonanie wyszukiwania tekstowego**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Wykonanie wyszukiwania obiektowego**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

### Wyszukiwanie Boolean NOT
Wyklucz niepożądane terminy przy użyciu **NOT**, aby odfiltrować szum w wynikach.

#### Przegląd
Zapytanie NOT pomaga wyeliminować nieistotne dokumenty, np. odfiltrowując nazwę konkurencyjnej marki (**boolean search examples java**).

#### Kroki implementacji

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

3. **Wykonanie wyszukiwania tekstowego**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Wykonanie wyszukiwania obiektowego**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

### Złożone zapytania Boolean
Połącz **AND**, **OR** i **NOT**, aby stworzyć skomplikowaną logikę wyszukiwania dla bardzo precyzyjnych potrzeb.

#### Przegląd
Złożone zapytania pozwalają modelować rzeczywiste scenariusze, np. „znajdź artykuły sportowe, które są pozytywne, ale wyklucz wszelkie wzmianki o konkretnych sportowcach”.

#### Kroki implementacji

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

3. **Wykonanie wyszukiwania tekstowego**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Wykonanie wyszukiwania obiektowego**

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

## Praktyczne zastosowania zapytań java boolean and or
- **Systemy zarządzania dokumentami** – znajdź kontrakty zawierające zarówno „confidential” **AND** „renewal”.  
- **Badania prawne** – filtruj orzecznictwo przy użyciu **AND**/**OR**, jednocześnie wykluczając przestarzałe ustawy za pomocą **NOT**.  
- **Obsługa klienta** – pobierz zgłoszenia, które wspominają „login” **AND** „error”, ale nie „resolved”.  
- **Kuratela treści** – zbierz wpisy blogowe o „cloud” **OR** „serverless” do newslettera.

## Częste pułapki i rozwiązywanie problemów
- **Brak odświeżenia indeksu** – po dodaniu nowych dokumentów wywołaj `index.update()`, aby były dostępne w wyszukiwaniu.  
- **Nieprawidłowe odstępy operatorów** – GroupDocs.Search wymaga spacji wokół operatorów (`AND`, `OR`, `NOT`).  
- **Czułość na wielkość liter** – zapytania są domyślnie niewrażliwe na wielkość liter, ale własne analizatory mogą to zmienić.  
- **Duże zestawy wyników** – używaj paginacji (`search(query, 0, 100)`), aby uniknąć przeciążenia pamięci.

## Najczęściej zadawane pytania

**Q: Czy mogę połączyć więcej niż dwa terminy w zapytaniu AND?**  
A: Oczywiście. Możesz łańcuchowo łączyć wiele obiektów `createWordQuery` przy pomocy `createAndQuery`, lub po prostu napisać `"term1 AND term2 AND term3"` w zapytaniu tekstowym.

**Q: Czy GroupDocs.Search obsługuje wyszukiwania z wildcard lub fuzzy?**  
A: Tak. Dodaj `*` jako wildcard (np. `promot*`) lub użyj `~` dla dopasowania przybliżonego (np. `comfort~`).

**Q: Jak ograniczyć wyszukiwanie do określonych typów plików?**  
A: Skorzystaj z klasy `FileTypeQuery`, aby ograniczyć wyniki do PDF‑ów, DOCX‑ów itp., i połącz ją ze swoim zapytaniem Boolean.

**Q: Jaki jest najlepszy sposób monitorowania wydajności indeksowania?**  
A: Włącz wbudowany logger (`index.getLogger().setLevel(Level.INFO)`) i analizuj metryki czasowe po każdej operacji `add`.

**Q: Czy istnieje możliwość zwiększenia wagi (boost) wybranych terminów?**  
A: Tak. Otocz ważne słowa obiektem `BoostQuery`, aby podnieść ich znaczenie w algorytmie punktacji.

---

**Ostatnia aktualizacja:** 2026-01-29  
**Testowano z:** GroupDocs.Search 25.4 (Java)  
**Autor:** GroupDocs