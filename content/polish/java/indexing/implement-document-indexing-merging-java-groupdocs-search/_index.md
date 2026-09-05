---
date: '2026-05-12'
description: 'Poznaj java full text search z GroupDocs.Search: dodaj dokumenty do
  indeksu, skonfiguruj opcje scalania i anuluj operację scalania. Idealne dla rozwiązań
  java do zarządzania dokumentami.'
keywords:
- java full text search
- document management java
- GroupDocs.Search merging
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: 'Learn java full text search with GroupDocs.Search: add documents to
    index, configure merge options, and cancel merge operation. Ideal for document
    management java solutions.'
  headline: java full text search – add docs & merge with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It tells GroupDocs.Search to scan a folder, extract searchable tokens,
      and store metadata for each file.
    question: What does “add documents to index” mean?
  - answer: Yes—use the `Cancellation` object to abort a merge after a configurable
      timeout.
    question: Can I stop a long merge?
  - answer: A free trial or temporary license works for testing; a commercial license
      unlocks full features.
    question: Do I need a license?
  - answer: JDK 8 or newer.
    question: Which Java version is required?
  - answer: Absolutely—GroupDocs.Search can handle multi‑hundred‑page documents with
      incremental indexing.
    question: Is this suitable for large datasets?
  type: FAQPage
title: java full text search – dodaj dokumenty i scal z GroupDocs.Search
type: docs
url: /pl/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# java full text search – dodawanie dokumentów i scalanie z GroupDocs.Search

## Szybkie odpowiedzi
- **Co oznacza „add documents to index”?** Informuje GroupDocs.Search, aby zeskanował folder, wyodrębnił tokeny do wyszukiwania i zapisał metadane dla każdego pliku.  
- **Czy mogę zatrzymać długie scalanie?** Tak — użyj obiektu `Cancellation`, aby przerwać scalanie po skonfigurowanym czasie oczekiwania.  
- **Czy potrzebuję licencji?** Darmowa wersja próbna lub tymczasowa licencja działa w testach; licencja komercyjna odblokowuje pełne funkcje.  
- **Jakiej wersji Javy wymaga?** JDK 8 lub nowszy.  
- **Czy to nadaje się do dużych zestawów danych?** Zdecydowanie — GroupDocs.Search radzi sobie z dokumentami liczącymi setki stron przy indeksowaniu przyrostowym.

## Co oznacza „add documents to index” w GroupDocs.Search?
**Dodawanie dokumentów do indeksu oznacza wprowadzenie kolekcji plików do GroupDocs.Search, aby biblioteka mogła analizować ich zawartość, wyodrębniać tokeny i budować strukturę danych umożliwiającą wyszukiwanie.** Proces tworzy zwartą reprezentację, która umożliwia błyskawiczne zapytania pełnotekstowe we wszystkich zaindeksowanych plikach.

## Dlaczego używać GroupDocs.Search do zarządzania dokumentami w Javie?
GroupDocs.Search zapewnia **skalowalne indeksowanie dla ponad 50 formatów wejściowych** (PDF, DOCX, XLSX, PPTX, HTML, obrazy itp.) i może przetwarzać **dokumenty do 2 GB bez ładowania całego pliku do pamięci**. Jego API daje precyzyjną kontrolę nad indeksowaniem, scalaniem i anulowaniem, co czyni go najlepszym wyborem dla rozwiązań klasy enterprise w zakresie java full text search.

## Wymagania wstępne
- **GroupDocs.Search for Java** wersja 25.4 lub nowsza.  
- Maven (lub ręczne pobranie JAR).  
- Podstawowa znajomość Javy oraz środowisko JDK 8+.

## Konfiguracja GroupDocs.Search dla Javy

### Instalacja Maven
Jeśli zarządzasz zależnościami przy użyciu Maven, dodaj repozytorium i zależność do swojego `pom.xml`:

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
- **Free Trial:** Zarejestruj się na stronie GroupDocs, aby uzyskać licencję próbną.  
- **Temporary License:** Złóż wniosek o tymczasowy klucz, jeśli potrzebujesz dłuższej oceny.  
- **Commercial License:** Kup licencję do użytku produkcyjnego.

Po uzyskaniu pliku licencji umieść go w projekcie i zainicjalizuj bibliotekę, jak pokazano później.

## Przewodnik implementacji

### Jak dodać dokumenty do indeksu – Tworzenie pierwszego indeksu
**Załaduj lub utwórz pusty indeks, tworząc instancję klasy `Index`, która reprezentuje kontener wyszukiwalny na dysku.** Ten krok przygotowuje miejsce przechowywania wszystkich tokenów, które zostaną wygenerowane z Twoich dokumentów.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **Dlaczego:** Ten krok tworzy kontener przechowywania, w którym zostaną zapisane zaindeksowane tokeny.

#### Dodawanie dokumentów do indeksu
**Wywołaj `index.add` z ścieżką do folderu; metoda skanuje każdy plik, wyodrębnia tekst i zapisuje metadane wyszukiwalne w indeksie.** Operacja odbywa się w jednym przebiegu i respektuje skonfigurowane `IndexSettings`.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **Dlaczego:** Biblioteka odczytuje każdy plik, wyodrębnia tekst i zapisuje go w `index1`.

### Tworzenie drugiego indeksu dla elastycznych przepływów pracy
**Utwórz kolejną instancję `Index`, aby przechowywać oddzielny zestaw dokumentów, umożliwiając izolowane przetwarzanie przed scaleniem.** Ten wzorzec jest przydatny w scenariuszach multi‑tenant lub indeksowaniu etapowym.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Dlaczego:** Wiele indeksów pozwala zarządzać odrębnymi zestawami dokumentów i później je łączyć.

### Jak skonfigurować opcje scalania i anulować operację scalania
**Utwórz instancję `MergeOptions`, ustaw żądane parametry i dołącz token `Cancellation`, który przerywa scalanie po określonym czasie.** Daje to pełną kontrolę nad zużyciem zasobów podczas dużych scaleni.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **Dlaczego:** `Cancellation` daje możliwość **automatycznego anulowania operacji scalania**, zapobiegając niekontrolowanym zadaniom.

### Scalanie indeksów
**Wywołaj `index1.merge(index2, mergeOptions)`; główny indeks wchłania wszystkie dokumenty z indeksu drugiego, zachowując integralność tokenów.** Po scaleniu posiadasz jednolite repozytorium wyszukiwalne.

```java
index1.merge(index2, options);
```

- **Dlaczego:** Po tym wywołaniu `index1` zawiera wszystkie dokumenty z obu źródeł, zapewniając jednolite doświadczenie wyszukiwania.

## Praktyczne zastosowania w zarządzaniu dokumentami w Javie
- **Legal firms:** Konsoliduj akta spraw z wielu biur w jeden wyszukiwalny indeks.  
- **Financial institutions:** Scal kwartalne raporty w jednolite repozytorium dla szybkich zapytań audytowych.  
- **Enterprises:** Połącz polityki HR, podręczniki zgodności i wewnętrzne przewodniki dla wyszukiwania w całej firmie.

## Rozważania dotyczące wydajności
- **Incremental indexing:** Dodawaj nowe pliki okresowo zamiast przebudowywać cały indeks.  
- **Memory monitoring:** Duże partie mogą zużywać pamięć RAM; przetwarzaj pliki w mniejszych partiach lub włącz tryb strumieniowy.  
- **Garbage collection:** Zwolnij nieużywane obiekty `Index` niezwłocznie, aby uwolnić zasoby.  
- **SSD storage:** Przechowywanie plików indeksu na SSD może przyspieszyć scalanie nawet dwukrotnie.

## Typowe problemy i rozwiązania
| Problem | Rozwiązanie |
|-------|----------|
| **Nieprawidłowa ścieżka folderu** | Sprawdź ścieżkę bezwzględną i upewnij się, że aplikacja ma uprawnienia do odczytu. |
| **Niewystarczająca pamięć** | Zwiększ przydział pamięci JVM (`-Xmx`) lub indeksuj pliki w partiach. |
| **Anulowanie nie zostało wywołane** | Upewnij się, że `cancelAfter` jest ustawione przed wywołaniem `merge`. |
| **Nieobsługiwany format pliku** | Zainstaluj dodatkowe wtyczki formatów z GroupDocs, jeśli to konieczne. |

## Najczęściej zadawane pytania

**Q:** *Dlaczego miałbym tworzyć wiele indeksów zamiast jednego?*  
**A:** Oddzielne indeksy pozwalają izolować domeny danych, stosować odrębne polityki bezpieczeństwa i scalać je tylko w razie potrzeby, co poprawia wydajność i organizację.

**Q:** *Czy mogę anulować operację indeksowania tak samo jak anuluję scalanie?*  
**A:** Tak — użyj obiektu `Cancellation` z metodą `add`, aby zatrzymać długotrwałe zadania indeksowania.

**Q:** *Jak zapewnić optymalną wydajność przy bardzo dużych zbiorach dokumentów?*  
**A:** Wykonuj indeksowanie przyrostowe, monitoruj pamięć JVM i przechowuj indeks na SSD. Rozważ użycie ustawienia `BatchSize`, aby ograniczyć liczbę dokumentów w pamięci.

**Q:** *Co zrobić, gdy otrzymuję błąd „Access denied”?*  
**A:** Sprawdź uprawnienia folderu dla użytkownika uruchamiającego proces Java i upewnij się, że plik licencji jest czytelny.

**Q:** *Czy GroupDocs.Search jest kompatybilny z innymi bibliotekami GroupDocs?*  
**A:** Zdecydowanie — możesz zintegrować go z GroupDocs.Viewer, GroupDocs.Conversion i innymi, aby zbudować pełne rozwiązanie dokumentacyjne.

## Zakończenie
Korzystając z tego przewodnika, wiesz już, jak **dodawać dokumenty do indeksu**, konfigurować zachowanie scalania i bezpiecznie **anulować operację scalania** w razie potrzeby — wszystko w ramach solidnego **java full text search**. Eksperymentuj z większymi zestawami danych, odkrywaj własne tokenizatory lub łącz GroupDocs.Search z innymi produktami GroupDocs, aby stworzyć rozwiązanie klasy enterprise.

## Zasoby
- **Documentation:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License Application:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**Last Updated:** 2026-05-12  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Powiązane tutoriale

- [Jak dodać dokumenty do indeksu z indeksowaniem metadanych w Javie przy użyciu GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Dodaj dokumenty do indeksu i wyłącz słowa stop w GroupDocs.Search Java dla zwiększonej dokładności wyszukiwania](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)
- [Dodaj dokumenty do indeksu – tutoriale GroupDocs.Search Java](/search/java/document-management/)