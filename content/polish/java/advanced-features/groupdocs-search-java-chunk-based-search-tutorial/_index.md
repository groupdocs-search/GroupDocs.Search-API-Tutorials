---
date: '2025-12-19'
description: Dowiedz się, jak dodać dokumenty do indeksu i włączyć wyszukiwanie oparte
  na fragmentach w Javie przy użyciu GroupDocs.Search, zwiększając wydajność przy
  dużych zestawach dokumentów.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Dodaj dokumenty do indeksu z wyszukiwaniem opartym na fragmentach w Javie
type: docs
url: /pl/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Dodawanie dokumentów do indeksu z wyszukiwaniem opartym na fragmentach w Javie

W dzisiejszym świecie napędzanym danymi, możliwość **dodawania dokumentów do indeksu** szybko oraz wykonywania wyszukiwań opartych na fragmentach jest niezbędna dla każdej aplikacji obsługującej duże kolekcje plików. Niezależnie od tego, czy pracujesz z umowami prawnymi, archiwami wsparcia klienta, czy ogromnymi bibliotekami badań, ten samouczek pokaże Ci dokładnie, jak skonfigurować GroupDocs.Search dla Javy, aby efektywnie indeksować dokumenty i pobierać istotne informacje w małych fragmentach.

## Czego się nauczysz
- Jak utworzyć indeks wyszukiwania w określonym folderze.  
- Kroki do **dodawania dokumentów do indeksu** z wielu lokalizacji.  
- Konfigurowanie opcji wyszukiwania, aby włączyć wyszukiwanie oparte na fragmentach.  
- Wykonywanie początkowego i kolejnych wyszukiwań opartych na fragmentach.  
- Przykłady zastosowań, w których wyszukiwanie oparte na fragmentach wyróżnia się w praktyce.

## Szybkie odpowiedzi
- **Jaki jest pierwszy krok?** Utwórz folder indeksu wyszukiwania.  
- **Jak dodać wiele plików?** Użyj `index.add()` dla każdego folderu dokumentów.  
- **Która opcja włącza wyszukiwanie fragmentów?** `options.setChunkSearch(true)`.  
- **Czy mogę kontynuować wyszukiwanie po pierwszym fragmencie?** Tak, wywołaj `index.searchNext()` z tokenem.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna lub tymczasowa licencja wystarczy do rozwoju; pełna licencja jest wymagana w produkcji.

## Wymagania wstępne
Aby skorzystać z tego przewodnika, upewnij się, że masz:

- **Wymagane biblioteki**: GroupDocs.Search dla Javy 25.4 lub nowsza.  
- **Środowisko**: Zainstalowany kompatybilny Java Development Kit (JDK).  
- **Wiedza wstępna**: Podstawowa znajomość programowania w Javie oraz Maven.

## Konfiguracja GroupDocs.Search dla Javy
Aby rozpocząć, zintegrować GroupDocs.Search z projektem przy użyciu Maven:

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

Alternatywnie, pobierz najnowszą wersję z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
Aby wypróbować GroupDocs.Search:

- **Darmowa wersja próbna** – testuj podstawowe funkcje bez zobowiązań.  
- **Tymczasowa licencja** – przedłużony dostęp do rozwoju.  
- **Zakup** – pełna licencja do użytku produkcyjnego.

### Podstawowa inicjalizacja i konfiguracja
Utwórz indeks w folderze, w którym mają znajdować się dane do przeszukiwania:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## Jak dodać dokumenty do indeksu
Teraz, gdy indeks istnieje, następnym logicznym krokiem jest **dodawanie dokumentów do indeksu** z lokalizacji, w których przechowywane są Twoje pliki.

### 1. Tworzenie indeksu
**Przegląd**: Skonfiguruj katalog dla indeksu wyszukiwania.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Dodawanie dokumentów do indeksu
**Przegląd**: Pobierz pliki z kilku folderów źródłowych.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Konfigurowanie opcji wyszukiwania dla fragmentów
Włącz wyszukiwanie oparte na fragmentach, modyfikując obiekt opcji.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Wykonywanie początkowego wyszukiwania opartego na fragmentach
Uruchom pierwsze zapytanie przy użyciu opcji włączających fragmenty.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Kontynuowanie wyszukiwania opartego na fragmentach
Iteruj przez pozostałe fragmenty, aż wyszukiwanie zostanie zakończone.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Dlaczego używać wyszukiwania opartego na fragmentach?
Wyszukiwanie oparte na fragmentach dzieli ogromne kolekcje dokumentów na zarządzalne części, zmniejszając obciążenie pamięci i przyspieszając czasy odpowiedzi. Jest to szczególnie przydatne, gdy:

1. **Zespoły prawne** muszą odnaleźć konkretne klauzule w tysiącach umów.  
2. **Portale wsparcia klienta** muszą natychmiast wyświetlać odpowiednie artykuły bazy wiedzy.  
3. **Badacze** przeszukują rozległe zestawy danych bez ładowania całych plików do pamięci.

## Rozważania dotyczące wydajności
- **Zarządzanie pamięcią** – Przydziel wystarczającą przestrzeń sterty (`-Xmx`) dla dużych indeksów.  
- **Monitorowanie zasobów** – Śledź zużycie CPU podczas indeksowania i operacji wyszukiwania.  
- **Utrzymanie indeksu** – Okresowo przebudowuj lub czyszcz indeks, aby usunąć przestarzałe dane.

## Częste problemy i rozwiązywanie problemów
| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| `OutOfMemoryError` podczas indeksowania | Zbyt mały rozmiar sterty | Zwiększ stertę JVM (`-Xmx2g` lub więcej) |
| Brak wyników | Token fragmentu nie został przetworzony | Upewnij się, że pętla `while` działa aż do `getNextChunkSearchToken()` równego `null` |
| Wolne działanie wyszukiwania | Indeks nie jest zoptymalizowany | Uruchom `index.optimize()` po masowych dodatkach |

## Najczęściej zadawane pytania

**Q: Czym jest wyszukiwanie oparte na fragmentach?**  
A: Wyszukiwanie oparte na fragmentach dzieli zestaw danych na mniejsze części, umożliwiając efektywne zapytania na dużych wolumenach bez ładowania całych dokumentów do pamięci.

**Q: Jak zaktualizować mój indeks o nowe pliki?**  
A: Po prostu wywołaj `index.add()` z ścieżką do nowych dokumentów; indeks automatycznie je uwzględni.

**Q: Czy GroupDocs.Search obsługuje różne formaty plików?**  
A: Tak, obsługuje PDF, DOCX, XLSX, PPTX i wiele innych popularnych formatów.

**Q: Jakie są typowe wąskie gardła wydajności?**  
A: Ograniczenia pamięci i nieoptymalne indeksy są najczęstsze; przydziel wystarczającą stertę i regularnie optymalizuj indeks.

**Q: Gdzie mogę znaleźć bardziej szczegółową dokumentację?**  
A: Odwiedź oficjalną [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) po szczegółowe przewodniki i odniesienia API.

## Zasoby
- **Dokumentacja**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Referencja API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Pobieranie**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Darmowe wsparcie**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Tymczasowa licencja**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Ostatnia aktualizacja:** 2025-12-19  
**Testowano z:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs