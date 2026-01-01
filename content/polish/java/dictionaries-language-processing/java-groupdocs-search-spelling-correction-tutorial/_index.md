---
date: '2025-12-20'
description: Dowiedz się, jak włączyć korektę pisowni w Javie przy użyciu GroupDocs.Search,
  dodać dokumenty do indeksu i ustawić maksymalną liczbę błędów, aby zwiększyć dokładność
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

# Jak włączyć korektę pisowni w Javie przy użyciu GroupDocs.Search

Dokładne wyniki wyszukiwania są niezbędne dla każdej nowoczesnej aplikacji. W tym samouczku dowiesz się, **jak włączyć korektę pisowni** w Javie przy użyciu GroupDocs.Search, aby użytkownicy otrzymywali właściwe wyniki nawet przy błędnym wpisaniu zapytań. Przejdziemy przez tworzenie indeksu, **dodawanie dokumentów do indeksu**, konfigurowanie opcji pisowni oraz uruchamianie wyszukiwania, które automatycznie koryguje błędy.

## Quick Answers
- **Co oznacza „how to enable spelling”?** Aktywuje wbudowany sprawdzacz pisowni, który koryguje literówki użytkownika podczas wyszukiwania.  
- **Która biblioteka udostępnia tę funkcję?** GroupDocs.Search for Java.  
- **Czy potrzebna jest licencja?** Licencja próbna działa w trybie ewaluacji; pełna licencja jest wymagana w produkcji.  
- **Czy mogę kontrolować tolerancję?** Tak – użyj `setMaxMistakeCount`, aby określić, ile literówek jest dozwolonych.  
- **Czy jest odpowiednia dla dużych indeksów?** Zdecydowanie – silnik jest zoptymalizowany pod kątem wysokowydajnego indeksowania i wyszukiwania.

## Co oznacza „how to enable spelling” w GroupDocs.Search?
Włączenie korekty pisowni powoduje, że silnik wyszukiwania szuka najbliższych poprawnych terminów, gdy zapytanie zawiera błędy. Ta funkcja znacząco poprawia doświadczenie użytkownika, zwracając istotne wyniki nawet przy błędnie wpisanym zapytaniu.

## Dlaczego włączać korektę pisowni w aplikacjach Java?
- **Zwiększa satysfakcję użytkowników** – użytkownicy nie muszą wpisywać zapytań idealnie.  
- **Obniża współczynnik odrzuceń** – dokładniejsze wyniki utrzymują odwiedzających zaangażowanych.  
- **Działa w różnych domenach** – od katalogów bibliotecznych po wyszukiwanie produktów w e‑commerce.

## Prerequisites
- Zainstalowany Java Development Kit (JDK).
- Podstawowa znajomość Javy i Maven.
- Zrozumienie koncepcji indeksowania.
- Licencja próbna lub pełna klucz GroupDocs.Search.

### Setting Up GroupDocs.Search for Java
Zintegruj bibliotekę w swoim projekcie Maven.

**Maven Setup**  
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

**Direct Download**  
Alternatywnie, pobierz najnowszą wersję z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
Uzyskaj darmową licencję próbną do oceny. W środowisku produkcyjnym zakup pełną licencję lub poproś o tymczasowy klucz na oficjalnej stronie.

## Jak dodać dokumenty do indeksu
Tworzenie indeksu jest podstawą każdej aplikacji z funkcją wyszukiwania. Poniżej znajduje się minimalny przykład, który **dodaje dokumenty do indeksu** z folderu.

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

*Wskazówka:* Sprawdź, czy ścieżki są poprawne i czy aplikacja ma uprawnienia do zapisu w folderze indeksu.

## Jak skonfigurować korektę pisowni (ustaw maksymalną liczbę błędów)
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

*Dlaczego `setMaxMistakeCount` jest ważne:* Określa, ile literówek silnik będzie tolerował. Dostosuj tę wartość w zależności od typowych wzorców błędów w Twojej domenie.

## Jak wykonać wyszukiwanie z korektą pisowni
Gdy indeks jest gotowy i opcje pisowni skonfigurowane, uruchom zapytanie, które może zawierać błędy.

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

Wywołanie `search()` zwraca `SearchResult`, które zawiera poprawione terminy oraz najbardziej istotne dokumenty.

## Praktyczne zastosowania
1. **Systemy biblioteczne:** Koryguj błędnie wpisane tytuły książek lub nazwiska autorów.  
2. **Platformy e‑commerce:** Naprawiaj literówki użytkowników w wyszukiwaniu produktów, aby zwiększyć konwersje.  
3. **Systemy zarządzania treścią:** Popraw wyszukiwanie artykułów dla personelu redakcyjnego.

## Uwagi dotyczące wydajności
- **Utrzymuj indeks aktualny** – regularnie indeksuj nowe lub zmienione pliki.  
- **Dostosuj ustawienia pamięci JVM** – przydziel wystarczającą ilość pamięci heap dla dużych indeksów.  
- **Monitoruj zużycie zasobów** – w razie potrzeby dostosuj flagi garbage‑collectora.

## Najczęściej zadawane pytania

**Q: Czym jest GroupDocs.Search?**  
A: To biblioteka Java, która zapewnia szybkie indeksowanie, zaawansowane funkcje wyszukiwania oraz wbudowaną korektę pisowni.

**Q: Jak uzyskać licencję na GroupDocs.Search?**  
A: Odwiedź oficjalną stronę, aby pobrać darmową wersję próbną lub zakupić pełną licencję.

**Q: Czy mogę zintegrować GroupDocs.Search z innymi frameworkami Java?**  
A: Tak, działa z Spring, Jakarta EE oraz dowolną standardową aplikacją Java.

**Q: Jakie są typowe problemy przy konfigurowaniu indeksu?**  
A: Nieprawidłowe ścieżki folderów, niewystarczające uprawnienia do plików lub brakujące zależności w `pom.xml`.

**Q: Jak korekta pisowni poprawia wyniki wyszukiwania?**  
A: Automatycznie przepisuje błędnie wpisane zapytania na najbliższe poprawne terminy, zwracając bardziej istotne wyniki.

## Dodatkowe zasoby
- [Dokumentacja](https://docs.groupdocs.com/search/java/)
- [Referencja API](https://reference.groupdocs.com/search/java)
- [Pobierz](https://releases.groupdocs.com/search/java/)
- [Repozytorium GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Darmowe Forum Wsparcia](https://forum.groupdocs.com/c/search/10)
- [Tymczasowa Licencja](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2025-12-20  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs