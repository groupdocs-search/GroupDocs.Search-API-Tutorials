---
date: '2026-02-21'
description: Dowiedz się, jak włączyć korektę pisowni w Javie przy użyciu GroupDocs.Search,
  dodać dokumenty do indeksu i ustawić maksymalną liczbę błędów, aby poprawić dokładność
  wyszukiwania.
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: Jak włączyć sprawdzanie pisowni w Javie z GroupDocs.Search
type: docs
url: /pl/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Jak Włączyć Korektę Pisowni w Javie przy użyciu GroupDocs.Search

Dokładne wyniki wyszukiwania są niezbędne w każdej nowoczesnej aplikacji. W tym samouczku dowiesz się **jak włączyć korektę pisowni** w Javie z GroupDocs.Search, aby użytkownicy otrzymywali właściwe wyniki nawet przy literówkach w zapytaniach. Przejdziemy przez tworzenie indeksu, **dodawanie dokumentów do indeksu**, konfigurowanie opcji pisowni oraz wykonywanie wyszukiwania, które automatycznie koryguje błędy.

## Szybkie odpowiedzi
- **Co oznacza „jak włączyć korektę pisowni”?** Aktywuje wbudowany sprawdzacz pisowni, który koryguje literówki użytkownika podczas wyszukiwania.  
- **Która biblioteka udostępnia tę funkcję?** GroupDocs.Search dla Javy.  
- **Czy potrzebna jest licencja?** Licencja trial działa w trybie ewaluacyjnym; pełna licencja jest wymagana w środowisku produkcyjnym.  
- **Czy mogę kontrolować tolerancję?** Tak – użyj `setMaxMistakeCount`, aby określić, ile literówek jest dopuszczalnych.  
- **Czy nadaje się do dużych indeksów?** Absolutnie – silnik jest zoptymalizowany pod kątem wysokowydajnego indeksowania i wyszukiwania.

## Co to jest „jak włączyć korektę pisowni” w GroupDocs.Search?
Włączenie korekty pisowni informuje silnik wyszukiwania, aby szukał najbliższych poprawnych terminów, gdy zapytanie zawiera błędy. Ta funkcja znacząco poprawia doświadczenie użytkownika, zwracając trafne wyniki nawet przy niepoprawnym wpisie.

## Dlaczego warto włączyć korektę pisowni w aplikacjach Java?
- **Zwiększa satysfakcję użytkowników** – nie muszą wpisywać zapytań idealnie.  
- **Obniża współczynnik odrzuceń** – dokładniejsze wyniki utrzymują odwiedzających dłużej.  
- **Działa w różnych domenach** – od katalogów bibliotecznych po wyszukiwanie produktów w e‑commerce.

## Wymagania wstępne
- Zainstalowany Java Development Kit (JDK).  
- Podstawowa znajomość Javy i Maven.  
- Rozumienie koncepcji indeksowania.  
- Klucz trial lub licencjonowany GroupDocs.Search.

### Konfiguracja GroupDocs.Search dla Javy
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
Uzyskaj darmową licencję trial do oceny. W środowisku produkcyjnym zakup pełną licencję lub poproś o tymczasowy klucz na oficjalnej stronie.

## Jak Dodawać Dokumenty do Indeksu
Tworzenie indeksu to podstawa każdej aplikacji z wyszukiwaniem. Poniżej znajduje się minimalny przykład, który **dodaje dokumenty do indeksu** z folderu.

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

*Wskazówka:* Sprawdź, czy ścieżki są poprawne i czy aplikacja ma uprawnienia zapisu do folderu indeksu.

## Jak Skonfigurować Korektę Pisowni (ustaw maksymalną liczbę błędów)
Możesz precyzyjnie dostroić sprawdzacz pisowni, włączając go i ustawiając tolerancję błędów.

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

*Dlaczego `setMaxMistakeCount` ma znaczenie:* Definiuje, ile literówek silnik będzie tolerował. Dostosuj tę wartość w zależności od typowych wzorców błędów w Twojej domenie.

## Jak Wykonać Wyszukiwanie z Korektą Pisowni
Gdy indeks jest gotowy, a opcje pisowni skonfigurowane, uruchom zapytanie, które może zawierać błędy.

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

Wywołanie `search()` zwraca obiekt `SearchResult`, który zawiera poprawione terminy oraz najistotniejsze dokumenty.

## Praktyczne Zastosowania
1. **Systemy Biblioteczne:** Koryguj błędnie wpisane tytuły książek lub nazwiska autorów.  
2. **Platformy E‑commerce:** Naprawiaj literówki użytkowników w wyszukiwaniu produktów, zwiększając konwersje.  
3. **Systemy Zarządzania Treścią:** Ulepszaj wyszukiwanie artykułów dla redaktorów.

## Rozważania Wydajnościowe
- **Utrzymuj indeks aktualny** – regularnie reindeksuj nowe lub zmienione pliki.  
- **Dostosuj ustawienia pamięci JVM** – przydziel wystarczający heap dla dużych indeksów.  
- **Monitoruj zużycie zasobów** – w razie potrzeby zmień flagi garbage‑collector.

## Typowe Problemy i Rozwiązywanie
| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---------|--------------|-----|
| Brak wyników po włączeniu korekty pisowni | Ścieżka folderu indeksu jest nieprawidłowa lub pusty | Sprawdź, czy `indexFolder` wskazuje na prawidłowy indeks i czy `index.add()` zakończyło się sukcesem |
| Sprawdzacz pisowni nie koryguje oczywistych literówek | `setMaxMistakeCount` jest ustawiony zbyt nisko | Zwiększ liczbę do 2 lub 3, aby uzyskać większą tolerancję |
| Aplikacja się zawiesza przy dużych zestawach dokumentów | Niewystarczający heap JVM | Zwiększ opcję `-Xmx` (np. `-Xmx4g`) |

## Najczęściej Zadawane Pytania

**P: Co to jest GroupDocs.Search?**  
O: To biblioteka Java, która zapewnia szybkie indeksowanie, zaawansowane funkcje wyszukiwania i wbudowaną korektę pisowni.

**P: Jak uzyskać licencję na GroupDocs.Search?**  
O: Odwiedź oficjalną stronę, aby pobrać darmowy trial lub zakupić pełną licencję.

**P: Czy mogę zintegrować GroupDocs.Search z innymi frameworkami Java?**  
O: Tak, działa z Spring, Jakarta EE oraz każdą standardową aplikacją Java.

**P: Jakie są typowe problemy przy konfigurowaniu indeksu?**  
O: Nieprawidłowe ścieżki folderów, niewystarczające uprawnienia do plików lub brak zależności w `pom.xml`.

**P: W jaki sposób korekta pisowni poprawia wyniki wyszukiwania?**  
O: Automatycznie przepisuje błędnie wpisane zapytania na najbliższe poprawne terminy, zwracając bardziej trafne wyniki.

## Dodatkowe Zasoby
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Ostatnia aktualizacja:** 2026-02-21  
**Testowano z:** GroupDocs.Search 25.4  
**Autor:** GroupDocs