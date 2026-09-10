---
date: '2026-09-02'
description: Dowiedz się, jak utworzyć search index java i włączyć spelling correction
  przy użyciu GroupDocs.Search. Postępuj zgodnie z instrukcjami krok po kroku, aby
  dodać dokumenty, skonfigurować max mistake count i poprawić dokładność wyszukiwania.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: Dowiedz się, jak utworzyć search index java i włączyć spelling correction
  przy użyciu GroupDocs.Search. Postępuj zgodnie z instrukcjami krok po kroku, aby
  dodać dokumenty, skonfigurować max mistake count i poprawić dokładność wyszukiwania.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: Jak utworzyć search index java i włączyć spelling correction
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: Jak utworzyć search index java i włączyć spelling correction
type: docs
url: /pl/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Jak utworzyć indeks wyszukiwania java i włączyć korektę pisowni

W nowoczesnych aplikacjach Java dostarczanie dokładnych wyników wyszukiwania jest niezbędną funkcją. Ten samouczek pokazuje **jak utworzyć indeks wyszukiwania java** i włączyć korektę pisowni przy użyciu GroupDocs.Search, aby użytkownicy otrzymywali trafne wyniki nawet przy błędnym wpisaniu zapytań. Zobaczysz, jak skonfigurować bibliotekę, dodać dokumenty, ustawić maksymalną liczbę błędów oraz wykonać wyszukiwanie tolerujące literówki — wszystko bez pisania dodatkowego kodu konfiguracyjnego.

## Szybkie odpowiedzi
- **Co robi „enable spelling”?** Aktywuje wbudowany sprawdzacz pisowni, który przepisuje błędnie napisane terminy na ich najbliższe poprawne formy podczas wyszukiwania.  
- **Która biblioteka zapewnia tę funkcję?** GroupDocs.Search for Java.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna wystarcza do oceny; pełna licencja jest wymagana w środowisku produkcyjnym.  
- **Czy mogę kontrolować tolerancję?** Tak – użyj `setMaxMistakeCount`, aby określić, ile literówek dopuszczonych jest w zapytaniu.  
- **Czy nadaje się do dużych indeksów?** Zdecydowanie – silnik obsługuje indeksy z milionami rekordów, utrzymując opóźnienie zapytań poniżej 100 ms na typowym sprzęcie serwerowym.

## Czym jest GroupDocs.Search?
GroupDocs.Search to biblioteka Java, która zapewnia szybkie indeksowanie pełnotekstowe i zaawansowane funkcje wyszukiwania, w tym wbudowaną korektę pisowni. Obsługuje ponad 50 formatów wejściowych i może przetwarzać dokumenty wielostronicowe bez ładowania całego pliku do pamięci.

## Dlaczego włączyć korektę pisowni w aplikacjach Java?
- **Zwiększa satysfakcję użytkowników** – odwiedzający otrzymują poprawne wyniki nawet przy niedoskonałym pisaniu.  
- **Zmniejsza współczynnik odrzuceń** – trafne wyniki utrzymują użytkowników dłużej.  
- **Działa w różnych domenach** – od katalogów bibliotecznych po wyszukiwanie produktów w e‑commerce, korekta pisowni poprawia trafność wszędzie.

## Wymagania wstępne
- Zainstalowany Java Development Kit (JDK).  
- Podstawowa znajomość Java i Maven.  
- Zrozumienie koncepcji indeksowania.  
- Licencja próbna lub klucz licencyjny GroupDocs.Search.

### Konfiguracja GroupDocs.Search dla Java
Zintegruj bibliotekę w swoim projekcie Maven.

**Konfiguracja Maven**  
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

**Bezpośrednie pobranie**  
Alternatywnie pobierz najnowszą wersję z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
Uzyskaj darmową licencję próbną do oceny. Do użytku produkcyjnego zakup pełną licencję lub poproś o tymczasowy klucz na oficjalnej stronie.

## Jak utworzyć indeks wyszukiwania w Java?
`SearchIndex` jest główną klasą reprezentującą indeks wyszukiwalny przechowywany na dysku.  
Utwórz instancję `SearchIndex` wskazującą na folder na dysku, a następnie dodaj dokumenty ze źródłowego katalogu. Silnik buduje odwrócony indeks, który umożliwia szybkie wyszukiwania. Możesz wywołać `index.add()` dla każdego pliku; biblioteka automatycznie wyodrębnia tekst w zależności od typu pliku.

## Jak włączyć korektę pisowni?
`getSpellingOptions()` zwraca obiekt konfiguracji pisowni dla indeksu, umożliwiając włączenie lub dostosowanie funkcji sprawdzania pisowni.  
Włącz korektę, wywołując `index.getSpellingOptions().setEnabled(true)`. Powoduje to, że silnik analizuje terminy zapytania i sugeruje poprawione alternatywy, gdy wykryte zostaną niezgodności. Funkcja działa od razu dla wszystkich języków indeksowanych obsługiwanych przez bibliotekę.

## Co to jest ustawienie maksymalnej liczby błędów?
`setMaxMistakeCount` konfiguruje maksymalną liczbę edycji znaków, które sprawdzacz pisowni toleruje na termin.  
`setMaxMistakeCount(int)` definiuje maksymalną liczbę edycji znaków (wstawienia, usunięcia, zamiany), które sprawdzacz pisowni toleruje na termin. Ustawienie na **2** pozwala silnikowi naprawić typowe dwuznakowe literówki, unikając jednocześnie zbyt agresywnych poprawek, które mogłyby zwrócić niepowiązane wyniki.

## Jak wykonać wyszukiwanie z korektą pisowni
`search()` wykonuje zapytanie przeciwko indeksowi i zwraca obiekt `SearchResult` zawierający dopasowania oraz ewentualne poprawione terminy.  
Uruchom zapytanie wyszukiwania przy użyciu metody `search()`. Jeśli zapytanie zawiera błędnie napisane słowa, silnik zwróci `SearchResult`, który zawiera poprawione terminy oraz listę najbardziej istotnych dokumentów. Możesz wyświetlić zarówno oryginalne zapytanie, jak i poprawioną wersję użytkownikowi dla przejrzystości.  
`SearchResult` przechowuje listę pasujących dokumentów i informacje o korektach zapytania.

## Praktyczne zastosowania
1. **Systemy biblioteczne** – automatycznie naprawiają błędnie napisane tytuły książek lub nazwiska autorów.  
2. **Platformy e‑commerce** – korygują literówki w nazwach produktów, aby zwiększyć współczynnik konwersji.  
3. **Zarządzanie treścią** – pomagają redaktorom znaleźć artykuły nawet przy niedoskonałych słowach kluczowych.

## Uwagi dotyczące wydajności
- **Utrzymuj indeks aktualny** – regularnie indeksuj nowe lub zmienione pliki.  
- **Dostosuj ustawienia pamięci JVM** – przydziel wystarczający stos dla dużych indeksów (np. `-Xmx4g`).  
- **Monitoruj zużycie zasobów** – dostosuj flagi garbage‑collectora, jeśli zauważysz przerwy podczas masowego indeksowania.

## Typowe problemy i rozwiązywanie
| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|-------|--------------------------|-------------|
| Brak wyników po włączeniu korekty pisowni | Ścieżka folderu indeksu jest nieprawidłowa lub pusta | Sprawdź, czy `indexFolder` wskazuje prawidłowy indeks i czy `index.add()` zakończyło się sukcesem |
| Sprawdzacz pisowni nie koryguje oczywistych literówek | `setMaxMistakeCount` jest ustawione zbyt nisko | Zwiększ liczbę do 2 lub 3, aby uzyskać bardziej tolerancyjną korektę |
| Aplikacja się zawiesza przy dużych zestawach dokumentów | Niewystarczająca pamięć JVM | Zwiększ opcję `-Xmx` (np. `-Xmx4g`) |

## Najczęściej zadawane pytania

**Q: Czym jest GroupDocs.Search?**  
A: GroupDocs.Search to biblioteka Java, która zapewnia szybkie indeksowanie, zaawansowane możliwości zapytań oraz wbudowaną korektę pisowni dla każdej aplikacji Java.

**Q: Jak uzyskać licencję na GroupDocs.Search?**  
A: Odwiedź oficjalną stronę, aby pobrać darmową wersję próbną lub zakupić pełną licencję; tymczasowy klucz jest również dostępny do krótkoterminowego testowania.

**Q: Czy mogę zintegrować GroupDocs.Search z innymi frameworkami Java?**  
A: Tak, działa bezproblemowo ze Spring, Jakarta EE oraz każdą standardową aplikacją Java.

**Q: Jakie są typowe problemy przy konfigurowaniu indeksu?**  
A: Nieprawidłowe ścieżki folderów, brak uprawnień do plików lub brakujące zależności Maven są typowymi przyczynami.

**Q: W jaki sposób korekta pisowni poprawia wyniki wyszukiwania?**  
A: Automatycznie przepisuje błędnie wpisane zapytania na ich najbliższe poprawne formy, zwracając bardziej trafne wyniki i zmniejszając frustrację użytkowników.

## Dodatkowe zasoby
- [Dokumentacja](https://docs.groupdocs.com/search/java/)
- [Referencja API](https://reference.groupdocs.com/search/java)
- [Pobierz](https://releases.groupdocs.com/search/java/)
- [Repozytorium GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Darmowe forum wsparcia](https://forum.groupdocs.com/c/search/10)
- [Licencja tymczasowa](https://purchase.groupdocs.com/temporary-license/)

---

**Ostatnia aktualizacja:** 2026-09-02  
**Testowano z:** GroupDocs.Search 25.4  
**Autor:** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## Powiązane samouczki

- [Jak utworzyć indeks dokumentów i dodać dokumenty przy użyciu API GroupDocs.Search dla Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Przetwarzanie języka Java – Utwórz słownik synonimów z GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Słowa stop w wyszukiwaniu: Dodaj dokumenty do indeksu z GroupDocs.Search Java](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)