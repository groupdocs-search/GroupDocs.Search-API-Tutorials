---
date: '2026-07-31'
description: Dowiedz się, jak wdrożyć case insensitive search java, dodając dokumenty
  do indeksu przy użyciu GroupDocs.Search oraz wykorzystując zamianę znaków do normalizacji
  tekstu podczas indeksowania.
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: Case insensitive search java umożliwia dodawanie dokumentów do indeksu
  i ich wyszukiwanie bez martwienia się o wielkość liter. Ten przewodnik pokazuje,
  jak GroupDocs.Search normalizuje tekst podczas indeksowania, zapewniając szybkie
  i niezawodne wyniki.
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Case Insensitive Search Java – indeksowanie dokumentów z GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: Dodaj dokumenty do indeksu dla wyszukiwania bez rozróżniania wielkości liter
  w Javie
type: docs
url: /pl/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# Dodaj dokumenty do indeksu dla wyszukiwania bez uwzględniania wielkości liter w Javie

Kiedy potrzebujesz **case insensitive search java**, które niezawodnie znajduje informacje niezależnie od tego, jak użytkownicy je wpisują, kluczem jest dodanie dokumentów do indeksu przy jednoczesnym normalizowaniu tekstu. W tym samouczku przeprowadzimy konfigurację GroupDocs.Search dla Javy, tak aby każdy dokument, który indeksujesz, był automatycznie zamieniany na małe litery (lub w inny sposób przetwarzany) podczas indeksowania, co zapewnia wyniki bez uwzględniania wielkości liter bez dodatkowej logiki w czasie zapytania.

## Szybkie odpowiedzi
- **Co oznacza „add documents to index”?** Oznacza to ładowanie plików źródłowych do struktury danych umożliwiającej wyszukiwanie, tak aby można je było później zapytać.  
- **Dlaczego używać zamiany znaków?** Normalizuje każdy znak — zazwyczaj do małych liter — tak aby wyszukiwania automatycznie ignorowały różnice w wielkości liter.  
- **Czy potrzebna jest licencja?** Bezpłatna wersja próbna działa w środowisku deweloperskim; pełna licencja jest wymagana w wdrożeniach produkcyjnych.  
- **Jaka wersja Javy jest wymagana?** Java 8 lub nowsza; biblioteka jest przeznaczona dla Java 11+ w celu uzyskania optymalnej wydajności.  
- **Czy mogę przełączyć się na wyszukiwanie uwzględniające wielkość liter w razie potrzeby?** Tak — opcje wyszukiwania pozwalają przełączać uwzględnianie wielkości liter dla poszczególnych zapytań.

## Co oznacza „add documents to index” w GroupDocs.Search?
Załaduj swoje pliki źródłowe (PDF, DOCX, TXT itp.) do indeksu umożliwiającego wyszukiwanie, aby silnik mógł je szybko odnaleźć. Dodawanie dokumentów do indeksu analizuje każdy plik, wyodrębnia zwykły tekst i przechowuje go w zoptymalizowanej strukturze danych, co umożliwia szybkie wyszukiwanie.

## Dlaczego włączyć zamianę znaków podczas indeksowania?
Zamiana znaków konwertuje każdy znak na zdefiniowany wcześniej odpowiednik — najczęściej na małe litery — w trakcie budowania indeksu. Dzięki temu różnice w kapitalizacji, znakach diakrytycznych czy symbolach specyficznych dla lokalizacji nie wpływają na wyniki wyszukiwania. Normalizując tekst w czasie indeksowania, silnik może dopasowywać zapytania do spójnego zestawu tokenów, zapewniając szybkie, niezawodne zachowanie bez uwzględniania wielkości liter bez dodatkowego przetwarzania przy każdym wyszukiwaniu.

## Wymagania wstępne
- **GroupDocs.Search for Java** wersja 25.4 lub nowsza (biblioteka obsługuje ponad 30 formatów plików i może indeksować dokumenty wielostronicowe bez ładowania całego pliku do pamięci).  
- **Java Development Kit (JDK)** 8 lub nowszy zainstalowany.  
- Podstawowa znajomość **Maven** (lub możliwość ręcznego dodania plików JAR).  

## Konfiguracja GroupDocs.Search dla Javy

### Konfiguracja Maven
Dodaj repozytorium GroupDocs oraz zależność do pliku `pom.xml`:

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
Jeśli wolisz nie używać Maven, pobierz najnowszy plik JAR z oficjalnej strony: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
- **Free Trial** – pobierz licencję próbną, aby rozpocząć eksperymenty.  
- **Temporary License** – poproś o przedłużoną licencję testową w portalu GroupDocs.  
- **Full License** – zakup licencję produkcyjną, gdy będziesz gotowy do uruchomienia.

### Podstawowa inicjalizacja (Utworzenie indeksu)
Poniższy fragment tworzy folder indeksu i włącza zamianę znaków:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Przewodnik implementacji

### Włączenie zamiany znaków w ustawieniach indeksu
Aktywacja tej funkcji instruuje silnik, aby zamieniał znaki podczas indeksowania, co jest kluczowym krokiem do zachowania bez uwzględniania wielkości liter.

#### Krok 1: Skonfiguruj `IndexSettings`
`IndexSettings` jest obiektem konfiguracyjnym, który kontroluje sposób przechowywania i przetwarzania tekstu w indeksie. Ustawiając `useCharacterReplacements` na **true**, włączasz automatyczne zamienianie na małe litery (lub dowolne własne mapowanie).

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### Konfiguracja zamiany znaków
Mapuj każdy znak na jego odpowiednik w małych literach (lub dowolne własne mapowanie, które jest potrzebne).

#### Krok 2: Zdefiniuj i dodaj pary zamiany
Słownik zamian przechowuje pary takie jak `'A' → 'a'`, `'É' → 'e'` itd. Dodanie tych par przed indeksowaniem zapewnia, że każdy token jest znormalizowany.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Indeksowanie dokumentów
Teraz, gdy indeks jest gotowy, możesz **add documents to index** z dowolnego folderu.

#### Krok 3: Dodaj dokumenty do indeksowania
GroupDocs.Search skanuje docelowy katalog, wyodrębnia tekst z każdego obsługiwanego typu pliku, stosuje mapę zamian i zapisuje tokeny w magazynie indeksu.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Wykonaj wyszukiwanie uwzględniające wielkość liter (opcjonalnie)

#### Krok 4: Wykonaj wyszukiwania uwzględniające wielkość liter
`SearchOptions` konfiguruje zachowanie zapytania, takie jak przełączanie uwzględniania wielkości liter, umożliwiając precyzyjną kontrolę nad sposobem wykonywania wyszukiwań.  
`SearchOptions.setUseCaseSensitiveSearch(true)` wymusza, aby silnik traktował znaki wielkie i małe jako odrębne podczas konkretnego zapytania, nadpisując domyślne zachowanie bez uwzględniania wielkości liter.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## Praktyczne zastosowania
1. **Kampanie marketingowe** – Normalizuj nazwy produktów, aby zespoły sprzedaży mogły znaleźć zasoby bez martwienia się o wielkość liter.  
2. **Obsługa klienta** – Zasilaj pola wyszukiwania w help desku, które zwracają właściwy artykuł, niezależnie od tego, czy użytkownik wpisze „login”, czy „Login”.  
3. **Katalogi e‑commerce** – Zapewnij, że klienci znajdą produkty niezależnie od tego, jak wpisują tytuły produktów, co zwiększa współczynnik konwersji.

## Względy wydajnościowe
- **Organizuj pliki źródłowe** – Przejrzysta hierarchia folderów skraca czas skanowania podczas kroku **add documents to index**.  
- **Monitoruj pamięć** – Indeksowanie dużych korpusów może zużywać znaczną ilość RAM; przetwarzanie plików w partiach po 500 – 1 000 elementów utrzymuje zużycie sterty pod kontrolą.  
- **Asynchroniczne indeksowanie** – Gdy jest wspierane, uruchamiaj indeksowanie w wątku w tle, aby interfejs był responsywny i uniknąć blokowania operacji użytkownika.

## Typowe problemy i rozwiązywanie

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|-------|--------------------------|-------------|
| Brak wyników dla znanego terminu | Zamiana znaków nie jest włączona | Sprawdź, czy `settings.setUseCharacterReplacements(true)` oraz czy słownik zamian zawiera potrzebne znaki. |
| Błąd braku pamięci podczas indeksowania | Indeksowanie zbyt wielu dużych plików jednocześnie | Indeksuj w mniejszych partiach lub zwiększ pamięć sterty JVM (`-Xmx4g`). |
| Wyszukiwanie zwraca wyniki uwzględniające wielkość liter nieoczekiwanie | `SearchOptions.setUseCaseSensitiveSearch(true)` został ustawiony | Usuń lub ustaw na `false`, aby przywrócić domyślne zachowanie bez uwzględniania wielkości liter. |
| Czas ładowania indeksu przekracza oczekiwania | Niewydajna struktura folderów lub brak użycia SSD | Zorganizuj ponownie pliki, usuń nieużywane dokumenty i przechowuj indeks na szybkim SSD. |
| Znaki specjalne są ignorowane | W słowniku zamian brak wpisów Unicode | Dodaj mapowania dla znaków takich jak “é”, “ß”, “ø” do ich pożądanych odpowiedników. |

## Najczęściej zadawane pytania

**Q: Jak obsłużyć znaki specjalne (np. „é”, „ß”) podczas indeksowania?**  
A: Umieść te znaki w słowniku zamian, mapując je na ich odpowiedniki ASCII lub pozostawiając niezmienione w zależności od wymagań wyszukiwania.

**Q: Czy mogę ograniczyć zamianę znaków do konkretnego języka?**  
A: Tak. Zbuduj własną tablicę zamian, która zawiera tylko znaki dla docelowego języka, przed dodaniem jej do słownika.

**Q: Co zrobić, gdy indeks ładuje się długo?**  
A: Optymalizuj strukturę folderów, usuń niepotrzebne pliki i przechowuj indeks na szybkim SSD. Indeksowanie przyrostowe również zmniejsza obciążenie przy ładowaniu.

**Q: Czy można odwrócić zamianę znaków po indeksowaniu?**  
A: Nie. Zamiany są trwale zapisane w danych indeksu; aby je zmienić, trzeba przebudować indeks z nowymi ustawieniami.

**Q: Gdzie mogę znaleźć bardziej szczegółową dokumentację API?**  
A: Oficjalna dokumentacja i odniesienie API zawierają wyczerpujące informacje (zobacz zasoby poniżej).

## Zasoby
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/) 

---

**Ostatnia aktualizacja:** 2026-07-31  
**Testowano z:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

## Powiązane samouczki

- [Zamiana znaków w GroupDocs.Search Java: Kompletny przewodnik po ulepszaniu wyszukiwania tekstu i indeksowania](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [Dodaj dokumenty do indeksu: wyszukiwanie uwzględniające wielkość liter w Javie z GroupDocs](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [Jak dodać dokumenty do indeksu przy użyciu GroupDocs.Search dla Javy](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)