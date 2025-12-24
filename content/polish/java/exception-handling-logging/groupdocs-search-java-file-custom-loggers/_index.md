---
date: '2025-12-24'
description: Dowiedz się, jak ograniczyć rozmiar pliku dziennika i używać loggera
  konsoli w Javie z GroupDocs.Search dla Javy. Ten przewodnik obejmuje konfiguracje
  logowania, wskazówki dotyczące rozwiązywania problemów oraz optymalizację wydajności.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Ogranicz rozmiar pliku logu przy użyciu loggerów GroupDocs.Search w Javie
type: docs
url: /pl/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Ogranicz rozmiar pliku dziennika przy użyciu loggerów GroupDocs.Search Java

Efektywne logowanie jest niezbędne przy zarządzaniu dużymi zbiorami dokumentów, szczególnie gdy trzeba **ograniczyć rozmiar pliku dziennika**, aby utrzymać kontrolę nad zużyciem pamięci. **GroupDocs.Search for Java** oferuje solidne rozwiązania do obsługi dzienników dzięki swoim potężnym możliwościom wyszukiwania. Ten samouczek prowadzi Cię przez implementację loggerów plikowych i własnych przy użyciu GroupDocs.Search, zwiększając zdolność Twojej aplikacji do śledzenia zdarzeń i debugowania problemów.

## Szybkie odpowiedzi
- **Co oznacza „limit log file size”?** Ogranicza maksymalny rozmiar pliku dziennika, zapobiegając niekontrolowanemu wzrostowi na dysku.  
- **Który logger pozwala ograniczyć rozmiar pliku dziennika?** Wbudowany `FileLogger` przyjmuje parametr maksymalnego rozmiaru.  
- **Jak używać console logger java?** Utwórz instancję `ConsoleLogger` i ustaw ją w `IndexSettings`.  
- **Czy potrzebna jest licencja na GroupDocs.Search?** Wersja próbna działa do oceny; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Jaki jest pierwszy krok?** Dodaj zależność GroupDocs.Search do swojego projektu Maven.

## Co to jest limit rozmiaru pliku dziennika?
Ograniczenie rozmiaru pliku dziennika oznacza skonfigurowanie loggera tak, aby po osiągnięciu określonego progu (np. 4 MB) przestał rosnąć lub został przełączony. Dzięki temu zużycie pamięci przez aplikację jest przewidywalne i unika się degradacji wydajności.

## Dlaczego używać loggerów plikowych i własnych z GroupDocs.Search?
- **Auditability:** Zachowaj trwały zapis zdarzeń indeksowania i wyszukiwania.  
- **Debugging:** Szybko zidentyfikuj problemy, przeglądając zwięzłe dzienniki.  
- **Flexibility:** Wybierz pomiędzy trwałymi dziennikami plikowymi a natychmiastowym wyjściem w konsoli (`use console logger java`).  

## Wymagania wstępne
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 lub nowszy, IDE (IntelliJ IDEA, Eclipse, itp.).  
- Podstawowa znajomość Java i Maven.  

## Konfiguracja GroupDocs.Search dla Java

Dodaj bibliotekę do swojego projektu, używając jednej z poniższych metod.

**Konfiguracja Maven:**

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

**Bezpośrednie pobranie:**  
Pobierz najnowszy plik JAR z oficjalnej strony: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
Uzyskaj wersję próbną lub zakup licencję poprzez [stronę licencjonowania](https://purchase.groupdocs.com/temporary-license/).

## Jak ograniczyć rozmiar pliku dziennika przy użyciu File Logger
Poniżej znajduje się przewodnik krok po kroku, który pokazuje, jak skonfigurować `FileLogger`, aby plik dziennika nigdy nie przekraczał określonego rozmiaru.

### 1️⃣ Importuj niezbędne pakiety
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Skonfiguruj Index Settings z File Logger
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

**Kluczowy punkt:** Konstruktor `FileLogger` przyjmuje drugi argument (`4.0`), który definiuje maksymalny rozmiar pliku dziennika w megabajtach, bezpośrednio spełniając wymaganie **limit log file size**.

## Jak używać console logger java
Jeśli wolisz natychmiastową informację zwrotną w terminalu, zamień logger plikowy na logger konsoli.

### 1️⃣ Importuj Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Skonfiguruj Index Settings z Console Logger
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

**Wskazówka:** Logger konsoli jest idealny podczas rozwoju, ponieważ natychmiast wypisuje każdy wpis dziennika, pomagając zweryfikować, że indeksowanie i wyszukiwanie działają zgodnie z oczekiwaniami.

## Praktyczne zastosowania
1. **Document Management Systems:** Zachowuj ścieżki audytu każdego zindeksowanego dokumentu.  
2. **Enterprise Search Engines:** Monitoruj wydajność zapytań i wskaźniki błędów w czasie rzeczywistym.  
3. **Legal & Compliance Software:** Rejestruj terminy wyszukiwania do raportowania regulacyjnego.

## Rozważania dotyczące wydajności
- **Log Size:** Ograniczając rozmiar pliku dziennika, unikasz nadmiernego zużycia dysku, które mogłoby spowolnić aplikację.  
- **Asynchronous Logging:** Jeśli potrzebujesz większej przepustowości, rozważ opakowanie loggera w asynchroniczną kolejkę (poza zakresem tego przewodnika).  
- **Memory Management:** Zwolnij duże obiekty `Index`, gdy nie są już potrzebne, aby utrzymać niski rozmiar pamięci JVM.

## Typowe problemy i rozwiązania
- **Log path not accessible:** Sprawdź, czy katalog istnieje i aplikacja ma uprawnienia do zapisu.  
- **Logger not firing:** Upewnij się, że wywołujesz `settings.setLogger(...)` *przed* utworzeniem obiektu `Index`.  
- **Console output missing:** Potwierdź, że uruchamiasz aplikację w terminalu, który wyświetla `System.out`.

## Najczęściej zadawane pytania

**Q: Co kontroluje drugi parametr `FileLogger`?**  
A: Ustawia maksymalny rozmiar pliku dziennika w megabajtach, umożliwiając ograniczenie rozmiaru pliku dziennika.

**Q: Czy mogę połączyć loggery plikowy i konsolowy?**  
A: Tak, poprzez stworzenie własnego loggera, który przekazuje wiadomości do obu miejsc docelowych.

**Q: Jak dodać dokumenty do indeksu po początkowym utworzeniu?**  
A: Wywołaj `index.add(pathToNewDocs)` w dowolnym momencie; logger zarejestruje operację.

**Q: Czy `ConsoleLogger` jest wątkowo‑bezpieczny?**  
A: Zapisuje bezpośrednio do `System.out`, które jest synchronizowane przez JVM, co czyni go bezpiecznym w większości przypadków.

**Q: Czy ograniczenie rozmiaru pliku dziennika wpłynie na ilość przechowywanych informacji?**  
A: Po osiągnięciu limitu rozmiaru nowe wpisy mogą być odrzucane lub plik może zostać przełączony, w zależności od implementacji loggera.

## Zasoby
- [Dokumentacja](https://docs.groupdocs.com/search/java/)
- [Referencja API](https://reference.groupdocs.com/search/java/)

---

**Ostatnia aktualizacja:** 2025-12-24  
**Testowano z:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs