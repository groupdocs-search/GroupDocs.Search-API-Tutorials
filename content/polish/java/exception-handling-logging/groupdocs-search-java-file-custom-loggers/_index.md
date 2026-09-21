---
date: '2026-09-21'
description: Dowiedz się, jak utworzyć logger, ustawić maksymalny rozmiar logu i używać
  loggera konsolowego w GroupDocs.Search dla Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Dowiedz się, jak utworzyć logger, ustawić maksymalny rozmiar logu
  i używać loggera konsolowego w GroupDocs.Search dla Java. Postępuj zgodnie z instrukcjami
  krok po kroku i wskazówkami najlepszych praktyk.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Jak utworzyć logger i ograniczyć rozmiar logu w GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: Jak utworzyć logger i ograniczyć rozmiar logu w GroupDocs.Search dla Java
type: docs
url: /pl/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Jak utworzyć logger i ograniczyć rozmiar pliku dziennika w GroupDocs.Search dla Javy

W tym samouczku dowiesz się, **jak tworzyć logger** implementacje dla GroupDocs.Search, skonfigurować maksymalny rozmiar pliku dziennika oraz przełączać się między logowaniem do pliku a konsolą. Odpowiednie zarządzanie dziennikami zapobiega zapełnianiu dysków podczas dużych zadań indeksowania, ułatwia rozwiązywanie problemów i zapewnia natychmiastową informację zwrotną podczas programowania. Rozpoczniemy od konfiguracji Maven, przejdziemy przez ustawienia loggera i zakończymy prostym zapytaniem wyszukiwania, które pokaże logger w działaniu.

## Szybkie odpowiedzi
- **Co oznacza „limit log file size”?** Ogranicza maksymalny rozmiar pliku dziennika, zapobiegając niekontrolowanemu wzrostowi na dysku.  
- **Który logger pozwala ograniczyć rozmiar pliku dziennika?** Wbudowany `FileLogger` przyjmuje parametr maksymalnego rozmiaru.  
- **Jak używać console logger java?** Utwórz instancję `ConsoleLogger` i ustaw ją w `IndexSettings`.  
- **Czy potrzebna jest licencja na GroupDocs.Search?** Wersja próbna działa do oceny; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Jaki jest pierwszy krok?** Dodaj zależność GroupDocs.Search do swojego projektu Maven.  

## Co to jest limit rozmiaru pliku dziennika?
Ustawienie **limit log file size** informuje logger, aby przestał zapisywać nowe wpisy, gdy plik osiągnie określony próg (na przykład 4 MB). Gdy limit zostanie osiągnięty, logger albo odrzuca dalsze komunikaty, albo przełącza się na nowy plik, utrzymując przewidywalne zużycie dysku.

## Dlaczego używać loggerów plikowych i niestandardowych z GroupDocs.Search?
Loggery plikowe i niestandardowe zapewniają możliwość audytu, wgląd w debugowanie oraz elastyczność. W środowiskach produkcyjnych logi plikowe dostarczają trwały zapis każdej operacji indeksowania i wyszukiwania, podczas gdy logi konsolowe zapewniają natychmiastową informację zwrotną w trakcie rozwoju. Te logi pomagają zespołom monitorować wydajność, śledzić błędy i spełniać wymogi zgodności, zachowując szczegółowy ślad aktywności.

## Wymagania wstępne
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 lub nowszy, z IDE takim jak IntelliJ IDEA lub Eclipse.  
- Podstawowa znajomość Maven i programowania w Javie.  

## Konfiguracja GroupDocs.Search dla Javy

Dodaj bibliotekę do swojego projektu, używając jednej z poniższych metod.

**Konfiguracja Maven:**  

```text
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
```

**Bezpośrednie pobranie:**  
Pobierz najnowszy plik JAR z oficjalnej strony: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
Uzyskaj wersję próbną lub zakup licencję poprzez [stronę licencjonowania](https://purchase.groupdocs.com/temporary-license/).

## Jak utworzyć niestandardowy logger dla GroupDocs.Search
Tworzenie niestandardowego loggera jest proste, ponieważ GroupDocs.Search opiera się na interfejsie `ILogger`. Implementując ten interfejs — lub rozszerzając dostarczone `FileLogger` lub `ConsoleLogger` — możesz wstrzyknąć dodatkowe zachowanie, takie jak zdalne przekazywanie lub rotacja logów. Możesz także dodać logikę inicjalizacji, np. otwieranie połączeń sieciowych, i zapewnić zamknięcie zasobów w metodzie zamknięcia loggera. Takie podejście pozwala integrować się z platformami monitorującymi, takimi jak ELK lub Splunk.

### Definicja kotwicy
`ILogger` jest podstawowym kontraktem logowania w GroupDocs.Search; każda klasa implementująca jego metodę `log(Level, String)` może stać się loggerem.

### Przykładowe podejście (bez bloku kodu)
1. Utwórz klasę implementującą `ILogger`.  
2. Nadpisz metodę `log`, aby zapisywać komunikaty do wybranego miejsca (plik, baza danych, endpoint HTTP).  
3. W konfiguracji indeksu wywołaj `settings.setLogger(new YourCustomLogger())`.  

## Jak ograniczyć rozmiar pliku dziennika przy użyciu File Logger
`FileLogger` zapisuje wpisy dziennika do pliku na dysku i przyjmuje argument maksymalnego rozmiaru. Określając limit rozmiaru, logger automatycznie przestaje dodawać nowe wpisy lub tworzy nowy plik, gdy próg zostanie osiągnięty, zapobiegając niekontrolowanemu wzrostowi dysku. Takie zachowanie zapewnia, że logowanie nie wpływa na wydajność indeksowania, jednocześnie utrzymując zwięzły zapis zdarzeń.

### Definicja kotwicy
`FileLogger` jest wbudowanym loggerem, który zapisuje komunikaty do pliku tekstowego i obsługuje konfigurowalny maksymalny rozmiar pliku.

### Przewodnik krok po kroku
1️⃣ **Importuj niezbędne pakiety**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Skonfiguruj ustawienia indeksu z File Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **Utwórz lub załaduj indeks**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Dodaj dokumenty do indeksu**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Wykonaj zapytanie wyszukiwania**  
```text
```java
SearchResult result = index.search(query);
```
```

**Kluczowy punkt:** Drugi argument konstruktora `FileLogger` (`4.0`) określa **set max log size** w megabajtach, bezpośrednio spełniając wymóg **limit log file size**.

## Jak używać console logger java
Gdy potrzebna jest natychmiastowa widoczność zdarzeń logowania, `ConsoleLogger` zapisuje każdą wiadomość do `System.out`. Ten logger jest lekki i bezpieczny wątkowo, co czyni go odpowiednim do sesji rozwojowych i debugowania. Dostarcza natychmiastową informację zwrotną o postępie indeksowania, zapytaniach wyszukiwania i warunkach błędów, nie wymagając operacji I/O na plikach, co może przyspieszyć iteracyjne testowanie.

### Definicja kotwicy
`ConsoleLogger` jest lekkim loggerem, który wypisuje wpisy dziennika na standardowy strumień konsoli, co czyni go idealnym do sesji debugowania.

### Kroki konfiguracji
1️⃣ **Importuj logger konsoli**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Skonfiguruj ustawienia indeksu z Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Utwórz lub załaduj indeks**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Dodaj dokumenty i wykonaj wyszukiwanie**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Wskazówka:** Logger konsoli jest idealny podczas rozwoju, ponieważ natychmiast wypisuje każdy wpis dziennika, pomagając zweryfikować, że indeksowanie i wyszukiwanie działają zgodnie z oczekiwaniami.

## Praktyczne zastosowania
1. **Systemy zarządzania dokumentami:** Zachowuj ścieżki audytu każdego zindeksowanego dokumentu, spełniając wymogi zgodności.  
2. **Wyszukiwarki korporacyjne:** Monitoruj wydajność zapytań i wskaźniki błędów w czasie rzeczywistym, umożliwiając szybkie kontrole zgodności z SLA.  
3. **Oprogramowanie prawne i zgodności:** Rejestruj terminy wyszukiwania i znaczniki czasu do raportowania regulacyjnego, z logami przechowywanymi przez wymagany okres retencji.  

## Uwagi dotyczące wydajności
- **Rozmiar logu:** Dzięki **set max log size** unikasz nadmiernego zużycia dysku, które mogłoby spowolnić działanie garbage collectora JVM.  
- **Logowanie asynchroniczne:** W scenariuszach o wysokiej przepustowości, otocz logger kolejką asynchroniczną, aby odłączyć I/O od wątku indeksowania (implementacja poza zakresem tego przewodnika).  
- **Zarządzanie pamięcią:** Zwolnij duże obiekty `Index` wywołując `index.close()`, gdy nie są już potrzebne, aby utrzymać niski ślad pamięci JVM.  

## Typowe problemy i rozwiązania
- **Ścieżka logu niedostępna:** Sprawdź, czy katalog istnieje i czy aplikacja ma uprawnienia zapisu dla konta użytkownika uruchamiającego JVM.  
- **Logger nie działa:** Upewnij się, że wywołujesz `settings.setLogger(...)` *przed* utworzeniem obiektu `Index`; w przeciwnym razie używany jest domyślny logger.  
- **Brak wyjścia konsoli:** Upewnij się, że uruchamiasz aplikację w terminalu wyświetlającym `System.out` i że żaden framework logowania (np. SLF4J) nie przechwytuje wyjścia.  

## Najczęściej zadawane pytania

**Q: Co kontroluje drugi parametr `FileLogger`?**  
A: Ustawia maksymalny rozmiar pliku dziennika w megabajtach, pozwalając na **set max log size** i zapobiegając niekontrolowanemu wzrostowi.

**Q: Czy mogę połączyć loggery plikowy i konsolowy?**  
A: Tak. Utwórz niestandardowy logger, który przekazuje każde wywołanie `log` zarówno do `FileLogger`, jak i `ConsoleLogger`, a następnie zarejestruj ten logger złożony w `IndexSettings`.

**Q: Jak dodać dokumenty do indeksu po początkowym utworzeniu?**  
A: Wywołaj `index.add(pathToNewDocs)` w dowolnym momencie; skonfigurowany logger automatycznie zarejestruje dodanie.

**Q: Czy `ConsoleLogger` jest bezpieczny wątkowo?**  
A: Zapisuje bezpośrednio do `System.out`, które JVM synchronizuje wewnętrznie, co czyni go bezpiecznym w typowych scenariuszach wielowątkowych.

**Q: Czy ograniczenie rozmiaru pliku dziennika wpłynie na ilość przechowywanych informacji?**  
A: Gdy limit rozmiaru zostanie osiągnięty, nowe wpisy są albo odrzucane, albo logger przełącza się na nowy plik, w zależności od wybranej implementacji.

## Zasoby
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Ostatnia aktualizacja:** 2026-09-21  
**Testowano z:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs  

## Powiązane samouczki

- [Jak wdrożyć logowanie - Samouczki obsługi wyjątków i logowania dla GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Implementacja asynchronicznego logowania w Javie z GroupDocs.Search – Przewodnik po niestandardowym loggerze](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Tworzenie indeksu wyszukiwania w Javie – Samouczki GroupDocs.Search](/search/java/indexing/)