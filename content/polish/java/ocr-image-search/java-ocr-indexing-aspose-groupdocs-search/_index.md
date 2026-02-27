---
date: '2026-01-11'
description: Dowiedz się, jak używać GroupDocs for Java OCR do indeksowania z Aspose.OCR,
  umożliwiając potężne możliwości wyszukiwania dokumentów w plikach PDF, obrazach
  i zeskanowanych dokumentach.
keywords:
- Java OCR indexing
- document searchability
- OCR with GroupDocs
title: Jak używać GroupDocs for Java do indeksowania OCR z Aspose
type: docs
url: /pl/java/ocr-image-search/java-ocr-indexing-aspose-groupdocs-search/
weight: 1
---

# Jak używać GroupDocs do indeksowania OCR w Javie z Aspose

W tym przewodniku dowiesz się **jak używać GroupDocs**, aby dodać wyszukiwanie oparte na OCR do swoich aplikacji Java. Łącząc GroupDocs.Search z Aspose.OCR, możesz przekształcić zawartość opartą na obrazach w tekst przeszukiwalny, co sprawia, że systemy zarządzania dokumentami są znacznie bardziej użyteczne. Przejdziemy przez konfigurację, indeksowanie, wyszukiwanie i własną integrację OCR, wszystko z jasnymi, krok po kroku przykładami.

## Szybkie odpowiedzi
- **Jaka biblioteka zapewnia indeksowanie OCR?** GroupDocs.Search w połączeniu z Aspose.OCR.  
- **Jakiej wersji Java wymaga?** JDK 8 lub wyższa.  
- **Czy potrzebna jest licencja?** Dostępna jest bezpłatna wersja próbna; płatna licencja jest wymagana w środowisku produkcyjnym.  
- **Czy mogę indeksować zarówno osobne, jak i osadzone obrazy?** Tak, włącz obie opcje w `IndexingOptions`.  
- **Czy obsługiwane jest wielowątkowość?** Tak, możesz równolegle indeksować duże zestawy danych.

## Czym jest indeksowanie OCR w GroupDocs?
Indeksowanie OCR wyodrębnia tekst z obrazów (w tym zeskanowanych plików PDF) i zapisuje go w przeszukiwalnym indeksie. GroupDocs.Search obsługuje indeksowanie i wykonywanie zapytań, natomiast Aspose.OCR wykonuje rzeczywiste rozpoznawanie znaków.

## Dlaczego używać GroupDocs do indeksowania OCR w Javie?
- **Wysoka dokładność** dzięki zaawansowanemu silnikowi OCR od Aspose.  
- **Bezproblemowa integracja z Javą** poprzez Maven lub bezpośrednie pliki JAR.  
- **Elastyczna konfiguracja** dla osobnych lub osadzonych obrazów.  
- **Skalowalna wydajność** dzięki wielowątkowości i optymalizacji pamięci.

## Prerequisites
- **GroupDocs.Search** ≥ 25.4  
- **Aspose.OCR** (latest version)  
- JDK 8+ and an IDE (IntelliJ, Eclipse, NetBeans)  
- Podstawowa znajomość Java; Maven jest pomocny, ale nieobowiązkowy

## Konfiguracja GroupDocs.Search dla Java
### Using Maven
Dodaj repozytorium i zależność do swojego `pom.xml`:

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

### Bezpośrednie pobieranie
Alternatywnie, pobierz najnowszą wersję GroupDocs.Search dla Java z [wydania GroupDocs](https://releases.groupdocs.com/search/java/).

### Nabycie licencji
- **Bezpłatna wersja próbna** – przetestuj wszystkie funkcje bez kosztów.
- **Licencja tymczasowa** – wydłużony okres testowy.
- **Zakup** – wymagany przy stosowaniu produkcji.

### Podstawowa inicjalizacja i konfiguracja
Utwórz folder indeksu i zainicjalizuj obiekt `Index`:

```java
import com.groupdocs.search.Index;
// Specify the directory where the index will be stored.
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
// Create an instance of Index class at the specified location.
Index index = new Index(indexFolder);
```

## Jak używać GroupDocs do indeksowania OCR
### Creating an Index
Najpierw skonfiguruj folder, w którym będą przechowywane pliki indeksu:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
Index index = new Index(indexFolder);
```

### Ustawianie opcji indeksowania OCR
Włącz OCR zarówno dla osobnych, jak i osadzonych obrazów oraz podłącz własny łącznik OCR:

```java
import com.groupdocs.search.options.IndexingOptions;
IndexingOptions options = new IndexingOptions();
options.getOcrIndexingOptions().setEnabledForSeparateImages(true);
options.getOcrIndexingOptions().setEnabledForEmbeddedImages(true);
// Set a custom OCR connector.
options.getOcrIndexingOptions().setOcrConnector(new OcrConnector());
```

### Indeksowanie dokumentów
Dodaj swoje dokumenty źródłowe (PDF, pliki Word, obrazy itp.) do indeksu:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder, options);
```

### Wyszukiwanie w indeksie
Uruchom zapytanie wyszukiwania na zindeksowanej zawartości:

```java
import com.groupdocs.search.results.SearchResult;
String query = "water";
SearchResult result = index.search(query);
```

### Implementacja łącznika OCR
Użyj Aspose.OCR do rozpoznawania tekstu z obrazów. Zaimplementuj interfejs `IOcrConnector` jak pokazano:

```java
import com.groupdocs.search.options.IOcrConnector;
import com.groupdocs.search.options.OcrContext;
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import com.aspose.ocr.AsposeOCR;

public class OcrConnector implements IOcrConnector {
    @Override
    public final String recognize(OcrContext context) {
        if (null == context.getImageLocation()) {
            throw new RuntimeException("The image type is not supported: " + context.getImageLocation());
        }
        
        BufferedImage image = ImageIO.read(context.getImageLocation().toFile());
        AsposeOCR api = new AsposeOCR();
        String text = api.RecognizePage(image);
        return text;
    }
}
```

## Praktyczne zastosowania
1. **Systemy zarządzania dokumentami** – szybkie wyszukiwanie dokumentów zawierających zeskanowane obrazy.  
2. **Wyszukiwanie w archiwach** – odnajdywanie historycznych rekordów w ogromnych archiwach.  
3. **Analiza dokumentów prawnych** – przeszukiwanie umów i dowodów zawierających zeskanowane podpisy lub diagramy.  
4. **Wyszukiwanie w dokumentacji medycznej** – indeksowanie formularzy pacjentów, wyników laboratoriów i adnotacji z rentgenów.

## Uwagi dotyczące wydajności
- **Rozmiar indeksu** – wyklucz niepotrzebne metadane, aby utrzymać indeks w lekkiej formie.  
- **Wielowątkowość** – przetwarzaj duże partie równolegle, aby przyspieszyć indeksowanie.  
- **Zarządzanie pamięcią** – monitoruj stertę JVM przy obsłudze obrazów wysokiej rozdzielczości.

## Typowe problemy i rozwiązania
- **Błędy licencji** – upewnij się, że prawidłowy plik licencji znajduje się w katalogu roboczym aplikacji.  
- **Brakujące obrazy** – sprawdź, czy ścieżki do obrazów są dostępne i czy formaty są obsługiwane (PNG, JPEG, BMP).  
- **Out‑Of‑Memory** – zwiększ stertę JVM (`-Xmx`) lub przetwarzaj dokumenty w mniejszych partiach.

## Najczęściej zadawane pytania
**P: Jak rozwiązać problemy z licencjonowaniem w GroupDocs.Search?**  
A: Uzyskaj tymczasową licencję ze [strony GroupDocs](https://purchase.groupdocs.com/temporary-license/), aby odblokować wszystkie funkcje.

**P: Jaki jest najlepszy sposób obsługi indeksowania dużych dokumentów?**  
A: Wykorzystaj wielowątkowość i przetwarzanie wsadowe, aby poprawić wydajność i zmniejszyć obciążenie pamięci.

**P: Czy mogę dalej dostosować ustawienia OCR w GroupDocs.Search?**  
A: Tak, `IndexingOptions` pozwala precyzyjnie dostroić zachowanie OCR, np. wybór języka i wstępne przetwarzanie obrazu.

**P: Jakie są typowe wskazówki rozwiązywania problemów przy używaniu GroupDocs.Search?**  
A: Sprawdź dokładnie ścieżki katalogów, upewnij się, że wszystkie zależności są dostępne, oraz przejrzyj logi pod kątem brakujących plików.

**P: Jak mogę zintegrować Aspose.OCR z istniejącą aplikacją Java?**  
A: Zaimplementuj interfejs `IOcrConnector` jak pokazano powyżej, zapewniając prawidłowe obsłużenie wejścia obrazu.

## Zasoby
- [Dokumentacja GroupDocs.Search](https://docs.groupdocs.com/search/java/)
- [Referencja API](https://reference.groupdocs.com/search/java/)

---

**Ostatnia aktualizacja:** 2026-01-11  
**Testowano z:** GroupDocs.Search 25.4, Aspose.OCR najnowsza wersja  
**Author:** GroupDocs