---
date: '2026-02-06'
description: Dowiedz się, jak dodać dokumenty do indeksu i włączyć wyszukiwanie uwzględniające
  wielkość liter w Javie przy użyciu GroupDocs.Search, zwiększając dokładność swojej
  aplikacji.
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 'Dodaj dokumenty do indeksu: wyszukiwanie w Javie rozróżniające wielkość liter
  z GroupDocs'
type: docs
url: /pl/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Dodawanie dokumentów do indeksu: Opanowanie wyszukiwań rozróżniających wielkość liter w Javie z GroupDocs

Uzyskanie właściwej informacji z ogromnej kolekcji dokumentów jest kluczowym wymogiem współczesnych aplikacji. W tym przewodniku dowiesz się **jak dodać dokumenty do indeksu** oraz wykonać **wyszukiwania rozróżniające wielkość liter** przy użyciu GroupDocs.Search dla Javy. Niezależnie od tego, czy tworzysz repozytorium dokumentów prawnych, katalog e‑commerce, czy system zarządzania treścią, precyzyjne wyniki wyszukiwania zadowalają użytkowników i zapewniają wiarygodność danych.

## Szybkie odpowiedzi
- **Jaki jest podstawowy krok, aby rozpocząć wyszukiwanie?** Dodaj dokumenty do indeksu za pomocą `index.add(...)`.
- **Jak włączyć wyszukiwanie rozróżniające wielkość liter?** Ustaw `options.setUseCaseSensitiveSearch(true)`.
- **Czy mogę wyszukiwać w wielu katalogach?** Tak – wywołaj `index.add()` dla każdego folderu, który chcesz uwzględnić.
- **Która metoda pozwala na wyszukiwanie przy użyciu obiektów?** Użyj `SearchQuery.createWordQuery(...)`.
- **Czy potrzebuję licencji do testów?** Dostępna jest tymczasowa licencja do celów próbnych.

## Co oznacza „dodawanie dokumentów do indeksu”?
Dodawanie dokumentów do indeksu oznacza wprowadzenie Twoich plików źródłowych (PDF, dokumenty Word, zwykły tekst itp.) do GroupDocs.Search, aby mógł zbudować strukturę danych umożliwiającą wyszukiwanie. Po zindeksowaniu silnik może wykonywać szybkie zapytania, w tym rozróżniające wielkość liter.

## Dlaczego włączyć wyszukiwanie rozróżniające wielkość liter w Javie?
- **Dokładne dopasowanie terminu** – rozróżnia „Apple” (firma) od „apple” (owoc).  
- **Zgodność z regulacjami** – niektóre branże wymagają dokładnego dopasowania fraz.  
- **Zwiększona trafność** – użytkownicy często oczekują wyników uwzględniających wielkość liter w kontekstach technicznych lub prawnych.

## Wymagania wstępne
- JDK (zalecane Java 17 lub nowsza)  
- Maven do zarządzania zależnościami  
- IDE, takie jak IntelliJ IDEA lub Eclipse  
- Podstawowa znajomość programowania w Javie  

## Konfiguracja GroupDocs.Search dla Javy
Najpierw dodaj repozytorium GroupDocs oraz zależność do swojego `pom.xml`:

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

Alternatywnie możesz pobrać najnowszą wersję bezpośrednio z [wydania GroupDocs.Search dla Java](https://releases.groupdocs.com/search/java/).

### Licencjonowanie
Aby rozpocząć wersję próbną, odwiedź stronę GroupDocs i zdobądź tymczasową licencję. Pozwoli to przetestować wszystkie funkcje bez żadnych ograniczeń.

## Jak dodać dokumenty do indeksu – Wyszukiwanie zapytaniem tekstowym

### Krok 1: Utwórz indeks i dodaj swoje dokumenty
Utwórz folder, w którym będą przechowywane pliki indeksu, a następnie dodaj katalog źródłowy zawierający dokumenty, które chcesz przeszukiwać.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Wskazówka:** Możesz wywołać `index.add()` wielokrotnie, aby **wyszukiwać w wielu katalogach** w jednym indeksie.

### Krok 2: Włącz wyszukiwanie rozróżniające wielkość liter
Skonfiguruj opcje wyszukiwania, aby uwzględniały wielkość liter.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Krok 3: Wykonaj zapytanie tekstowe rozróżniające wielkość liter
Uruchom zapytanie, które rozróżnia „Advantages” od „advantages”.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Pętla wypisuje pełną ścieżkę każdego dokumentu, który zawiera dokładnie dopasowany pod względem wielkości liter termin.

## Jak dodać dokumenty do indeksu – Wyszukiwanie zapytaniem obiektowym

Zapytania obiektowe dają większą elastyczność, szczególnie gdy trzeba połączyć wiele kryteriów.

### Krok 1: Zainicjuj drugi indeks (opcjonalnie)
Jeśli wolisz trzymać wyszukiwania oparte na obiektach oddzielnie, utwórz kolejny folder indeksu.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Krok 2: Ponownie użyj opcji rozróżniania wielkości liter
Ta sama instancja `SearchOptions` działa również dla zapytań obiektowych.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Krok 3: Zbuduj i uruchom zapytanie obiektowe
Utwórz obiekt zapytania słownego i przekaż go do silnika wyszukiwania.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Użycie `createWordQuery` pozwala później połączyć je z zapytaniami frazowymi, wieloznacznymi lub logicznymi w bardziej złożonych scenariuszach.

## Praktyczne zastosowania
- **Zarządzanie dokumentami prawnymi:** Pobieraj przepisy specyficzne dla sprawy, gdzie istotna jest wielkość liter.  
- **Platformy e‑commerce:** Rozróżniaj SKU produktów, np. „PRO‑X” vs. „pro‑x”.  
- **Systemy zarządzania treścią (CMS):** Zapewnij autorom możliwość znajdowania dokładnych nagłówków lub tagów.

## Uwagi dotyczące wydajności
- **Utrzymuj indeks aktualny** – przeprowadzaj ponowne indeksowanie, gdy dodane zostaną nowe pliki lub istniejące zostaną zmienione.  
- **Monitoruj zużycie pamięci** – duże korpusy skorzystają z indeksowania przyrostowego i odpowiedniego przydziału pamięci JVM.  
- **Wykorzystaj garbage collector Javy** – zwalniaj obiekty `Index`, gdy nie są już potrzebne.

## Typowe problemy i rozwiązania
| Issue | Solution |
|-------|----------|
| `useCaseSensitiveSearch` appears ignored | Sprawdź, czy używasz najnowszej wersji GroupDocs.Search oraz czy indeks został przebudowany po zmianie tej opcji. |
| No results returned for a known term | Upewnij się, że wielkość liter terminu jest dokładnie dopasowana oraz że dokument został pomyślnie dodany do indeksu. |
| Searching many folders slows down | Dodawaj każdy folder osobno za pomocą `index.add()` i rozważ podzielenie indeksu na fragmenty (shards) przy bardzo dużych zbiorach danych. |

## Najczęściej zadawane pytania

**Q:** Jak radzić sobie z dużymi zestawami danych przy użyciu GroupDocs.Search?  
**A:** Wykorzystaj partycjonowanie indeksu, dostosuj ustawienia pamięci JVM oraz okresowo kompaktuj indeks, aby utrzymać optymalną wydajność.

**Q:** Czy mogę wyszukiwać jednocześnie w wielu katalogach?  
**A:** Tak – wywołaj `index.add()` dla każdego katalogu, który chcesz uwzględnić, a następnie uruchom pojedyncze zapytanie przeciwko połączonemu indeksowi.

**Q:** Jakie są typowe pułapki przy konfigurowaniu wyszukiwań rozróżniających wielkość liter?  
**A:** Zapomnienie o przebudowaniu indeksu po włączeniu `useCaseSensitiveSearch` lub użycie niewłaściwej wielkości liter w ciągu zapytania.

**Q:** Jak mogę rozwiązać problemy z błędami wyszukiwania?  
**A:** Sprawdź pliki logów generowane przez GroupDocs.Search pod kątem śladów stosu oraz potwierdź, że wszystkie zależności Maven zostały poprawnie rozwiązane.

**Q:** Czy GroupDocs.Search jest odpowiedni dla aplikacji czasu rzeczywistego?  
**A:** Przy odpowiednich strategiach indeksowania (aktualizacje przyrostowe i buforowanie w pamięci) może dostarczać wyniki wyszukiwania zbliżone do czasu rzeczywistego.

## Zasoby
- **Dokumentacja:** [Dokumentacja GroupDocs.Search Java](https://docs.groupdocs.com/search/java/)
- **Referencja API:** [Referencja API Java](https://reference.groupdocs.com/search/java)
- **Pobieranie:** [Najnowsze wydania](https://releases.groupdocs.com/search/java/)
- **Repozytorium GitHub:** [GroupDocs.Search dla Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum wsparcia:** [Bezpłatne wsparcie GroupDocs](https://forum.groupdocs.com/c/search/10)
- **Tymczasowa licencja:** [Uzyskaj tymczasową licencję](https://purchase.groupdocs.com/temporary-license/)

---

**Ostatnia aktualizacja:** 2026-02-06  
**Testowano z:** GroupDocs.Search 25.4  
**Autor:** GroupDocs