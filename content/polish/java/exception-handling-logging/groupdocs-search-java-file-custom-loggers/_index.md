---
date: '2026-02-24'
description: Dowiedz się, jak utworzyć własny logger, ustawić maksymalny rozmiar logu
  i skonfigurować logger konsoli lub pliku w GroupDocs.Search dla Javy.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Jak stworzyć własny logger i ograniczyć rozmiar pliku logu w GroupDocs.Search
  Java
type: docs
url: /pl/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Ogranicz rozmiar pliku logu przy użyciu loggerów GroupDocs.Search Java

W tym przewodniku **tworzyć własny logger** i dowiesz się, jak **ograniczyć rozmiar pliku logu** podczas korzystania z GroupDocs.Search dla Javy. Kontrola wzrostu logów jest kluczowa przy indeksowaniu dokumentów na dużą skalę, a wbudowane loggery pozwalają **ustawić maksymalny rozmiar logu**, **przewijać plik logu**, lub przełączyć się na **używać loggera konsoli** dla natychmiastowej informacji zwrotnej. Przejdźmy przez pełną konfigurację, od ustawień Maven po uruchomienie zapytania wyszukiwania, i zobaczmy, jak **dodawać indeks dokumentów** z włączonym loggerem.

## Szybkie odpowiedzi
- **Co oznacza „ograniczenie rozmiaru pliku logu”?** Ogranicza maksymalny rozmiar pliku logu, zapobiegając niekontrolowanemu wzrostowi na dysku.  
- **Który logger pozwala ograniczyć rozmiar pliku logu?** Wbudowany `FileLogger` przyjmuje parametr maksymalnego rozmiaru.  
- **Jak używać loggera konsoli w Javie?** Utwórz instancję `ConsoleLogger` i ustaw ją w `IndexSettings`.  
- **Czy potrzebna jest licencja na GroupDocs.Search?** Wersja próbna działa do oceny; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Jaki jest pierwszy krok?** Dodaj zależność GroupDocs.Search do swojego projektu Maven.  

## Co to jest ograniczenie rozmiaru pliku logu?
Ograniczenie rozmiaru pliku logu oznacza skonfigurowanie loggera tak, aby po osiągnięciu określonego progu (np. 4 MB) przestał rosnąć lub został przewinięty. Zapewnia to przewidywalny rozmiar pamięci aplikacji i zapobiega degradacji wydajności.

## Dlaczego używać plikowych i własnych loggerów z GroupDocs.Search?
- **Audytowalność:** Zachowaj trwały zapis zdarzeń indeksowania i wyszukiwania.  
- **Debugowanie:** Szybko zidentyfikuj problemy, przeglądając zwięzłe logi.  
- **Elastyczność:** Wybierz pomiędzy trwałymi logami w pliku a natychmiastowym wyjściem konsoli (`use console logger`).  

## Wymagania wstępne
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 lub nowszy, IDE (IntelliJ IDEA, Eclipse, itp.).  
- Podstawowa znajomość Javy i Maven.

## Konfiguracja GroupDocs.Search dla Java

Dodaj bibliotekę do swojego projektu, używając jednej z poniższych metod.

**Maven Setup:**

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

**Direct Download:**  
Pobierz najnowszy plik JAR z oficjalnej strony: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
Uzyskaj wersję próbną lub zakup licencję poprzez [stronę licencjonowania](https://purchase.groupdocs.com/temporary-license/).

## Jak utworzyć własny logger dla GroupDocs.Search
GroupDocs.Search pozwala podłączyć dowolną implementację interfejsu `ILogger`. Rozszerzając `FileLogger` lub `ConsoleLogger`, możesz dodać dodatkowe zachowanie — takie jak przewijanie pliku logu lub przekazywanie wiadomości do zdalnej usługi monitorującej. Ta elastyczność jest powodem, dla którego wiele zespołów **tworzy własny logger** rozwiązania dopasowane do ich potrzeb operacyjnych.

## Jak ograniczyć rozmiar pliku logu przy użyciu File Logger
Poniżej znajduje się przewodnik krok po kroku, który pokazuje, jak **skonfigurować logger plikowy**, aby plik logu nigdy nie przekraczał określonego rozmiaru.

### 1️⃣ Importuj niezbędne pakiety
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Skonfiguruj ustawienia indeksu z loggerem plikowym
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Utwórz lub załaduj indeks
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Dodaj dokumenty do indeksu
```java
index.add(documentsFolder);
```

### 5️⃣ Wykonaj zapytanie wyszukiwania
```java
SearchResult result = index.search(query);
```

**Kluczowy punkt:** Drugi argument konstruktora `FileLogger` (`4.0`) definiuje **ustaw maksymalny rozmiar logu** w megabajtach, bezpośrednio spełniając wymaganie **ograniczenia rozmiaru pliku logu**.

## Jak używać loggera konsoli w Javie
Jeśli wolisz natychmiastową informację zwrotną w terminalu, zamień logger plikowy na logger konsoli.

### 1️⃣ Importuj logger konsoli
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Skonfiguruj ustawienia indeksu z loggerem konsoli
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Utwórz lub załaduj indeks
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Dodaj dokumenty i wykonaj wyszukiwanie
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Wskazówka:** Logger konsoli jest idealny podczas rozwoju, ponieważ natychmiast drukuje każdy wpis logu, pomagając zweryfikować, że indeksowanie i wyszukiwanie działają zgodnie z oczekiwaniami.

## Praktyczne zastosowania
1. **Systemy zarządzania dokumentami:** Zachowuj ścieżki audytu każdego zindeksowanego dokumentu.  
2. **Przedsiębiorcze silniki wyszukiwania:** Monitoruj wydajność zapytań i wskaźniki błędów w czasie rzeczywistym.  
3. **Oprogramowanie prawne i zgodności:** Rejestruj terminy wyszukiwania do raportowania regulacyjnego.

## Rozważania dotyczące wydajności
- **Rozmiar logu:** Dzięki **ustaw maksymalny rozmiar logu**, unikasz nadmiernego zużycia dysku, które mogłoby spowolnić aplikację.  
- **Asynchroniczne logowanie:** Jeśli potrzebujesz większej przepustowości, rozważ opakowanie loggera w kolejkę asynchroniczną (poza zakresem tego przewodnika).  
- **Zarządzanie pamięcią:** Zwolnij duże obiekty `Index`, gdy nie są już potrzebne, aby utrzymać niski ślad pamięci JVM.

## Częste problemy i rozwiązania
- **Ścieżka logu jest niedostępna:** Sprawdź, czy katalog istnieje i aplikacja ma uprawnienia do zapisu.  
- **Logger nie działa:** Upewnij się, że wywołujesz `settings.setLogger(...)` *przed* utworzeniem obiektu `Index`.  
- **Brak wyjścia konsoli:** Upewnij się, że uruchamiasz aplikację w terminalu, który wyświetla `System.out`.

## Najczęściej zadawane pytania

**P: Co kontroluje drugi parametr `FileLogger`?**  
O: Ustawia maksymalny rozmiar pliku logu w megabajtach, pozwalając na **ustaw maksymalny rozmiar logu**.

**P: Czy mogę połączyć logger plikowy i konsolowy?**  
O: Tak, tworząc własny logger, który przekazuje wiadomości do obu miejsc.

**P: Jak dodać dokumenty do indeksu po początkowym utworzeniu?**  
O: Wywołaj `index.add(pathToNewDocs)` w dowolnym momencie; logger zarejestruje operację.

**P: Czy `ConsoleLogger` jest wątkowo‑bezpieczny?**  
O: Zapisuje bezpośrednio do `System.out`, które jest synchronizowane przez JVM, co czyni go bezpiecznym w większości przypadków użycia.

**P: Czy ograniczenie rozmiaru pliku logu wpłynie na ilość przechowywanych informacji?**  
O: Po osiągnięciu limitu rozmiaru nowe wpisy mogą być odrzucane lub plik może **przewijać plik logu**, w zależności od implementacji loggera.

## Zasoby
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](httpshttps://reference.groupdocs.com/search/java/)

---

**Ostatnia aktualizacja:** 2026-02-24  
**Testowano z:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs