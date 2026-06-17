---
date: '2026-02-21'
description: Dowiedz się, jak dodawać dokumenty do indeksu i zwiększyć wydajność wyszukiwania
  przy użyciu wyszukiwania opartego na fragmentach w Javie z GroupDocs.Search, optymalizując
  pamięć indeksu wyszukiwania w Javie dla dużych zestawów dokumentów.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Dodaj dokumenty do indeksu z wyszukiwaniem opartym na fragmentach w Javie
type: docs
url: /pl/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

_BLOCK_0-10 all present.

Make sure to keep all formatting.

Let's craft final output.# Dodawanie dokumentów do indeksu z wyszukiwaniem opartym na fragmentach w Javie

W nowoczesnych aplikacjach, które muszą szybko **add documents to index** i następnie wykonywać szybkie zapytania oparte na fragmentach, potrzebne jest rozwiązanie, które skaluje się bez nadmiernego zużycia pamięci. Ten samouczek przeprowadzi Cię przez konfigurację GroupDocs.Search dla Javy, dodawanie wielu folderów z dokumentami oraz konfigurowanie silnika w celu **increase search performance**, jednocześnie utrzymując zużycie **java search index memory** pod kontrolą. Niezależnie od tego, czy indeksujesz umowy prawne, zgłoszenia wsparcia, czy prace naukowe, poniższe kroki zapewnią gotową do produkcji implementację.

## Szybkie odpowiedzi
- **Jaki jest pierwszy krok?** Utwórz folder indeksu wyszukiwania.  
- **Jak dodać wiele plików?** Użyj `index.add()` dla każdego folderu z dokumentami.  
- **Która opcja włącza wyszukiwanie fragmentów?** `options.setChunkSearch(true)`.  
- **Czy mogę kontynuować wyszukiwanie po pierwszym fragmencie?** Tak, wywołaj `index.searchNext()` z tokenem.  
- **Czy potrzebuję licencji?** Darmowa wersja próbna lub tymczasowa licencja działa w środowisku deweloperskim; pełna licencja jest wymagana w produkcji.  

## Czego się nauczysz
- Jak utworzyć indeks wyszukiwania w określonym folderze.  
- Kroki do **add documents to index** z wielu lokalizacji.  
- Konfigurowanie opcji wyszukiwania w celu włączenia wyszukiwania opartego na fragmentach.  
- Wykonywanie początkowych i kolejnych wyszukiwań opartych na fragmentach.  
- Przykłady zastosowań, w których wyszukiwanie dokumentów oparte na fragmentach wyróżnia się.  

## Wymagania wstępne
- **Wymagane biblioteki**: GroupDocs.Search for Java 25.4 or later.  
- **Konfiguracja środowiska**: Zainstalowany kompatybilny Java Development Kit (JDK).  
- **Wymagania wiedzy**: Podstawowa znajomość programowania w Javie oraz Maven.  

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
- **Free Trial** – przetestuj podstawowe funkcje bez zobowiązań.  
- **Temporary License** – rozszerzony dostęp dla deweloperów.  
- **Purchase** – pełna licencja do użytku produkcyjnego.  

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
Teraz, gdy indeks istnieje, następnym logicznym krokiem jest **add documents to index** z lokalizacji, w których przechowywane są Twoje pliki.

### 1. Tworzenie indeksu
**Przegląd**: Utwórz katalog dla indeksu wyszukiwania.

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

### 3. Konfigurowanie opcji wyszukiwania dla wyszukiwania fragmentów
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
Wyszukiwanie oparte na fragmentach dzieli ogromne kolekcje dokumentów na zarządzalne części, zmniejszając obciążenie pamięci i przyspieszając czasy odpowiedzi. Jest szczególnie korzystne, gdy:
1. **Legal teams** muszą znaleźć konkretne klauzule w tysiącach umów.  
2. **Customer support portals** muszą natychmiast wyświetlać odpowiednie artykuły bazy wiedzy.  
3. **Researchers** przeszukują obszerne zestawy danych bez ładowania całych plików do pamięci.  

## Jak to podejście **increases search performance**
Wyszukując mniejsze fragmenty zamiast całych plików, silnik może:
- Pominąć nieistotne sekcje na wczesnym etapie, oszczędzając cykle CPU.  
- Utrzymywać w pamięci tylko aktywny fragment, co bezpośrednio zmniejsza zużycie **java search index memory**.  
- Równolegle przetwarzać fragmenty na maszynach wielordzeniowych, uzyskując szybsze wyniki.

## Zarządzanie **java search index memory**
Choć wyszukiwanie oparte na fragmentach już zmniejsza zużycie pamięci, możesz dodatkowo dostroić JVM:
- Przydziel wystarczającą ilość pamięci heap (`-Xmx2g` lub więcej) w zależności od rozmiaru indeksu.  
- Użyj `index.optimize()` po masowych dodaniach, aby skompresować strukturę indeksu.  
- Monitoruj przerwy GC przy użyciu narzędzi takich jak VisualVM, aby uniknąć skoków opóźnień.

## Uwagi dotyczące wydajności
- **Memory Management** – Przydziel wystarczającą przestrzeń heap (`-Xmx`) dla dużych indeksów.  
- **Resource Monitoring** – Monitoruj zużycie CPU podczas operacji indeksowania i wyszukiwania.  
- **Index Maintenance** – Okresowo przebudowuj lub czyszcz indeks, aby usunąć przestarzałe dane.  

## Częste pułapki i rozwiązywanie problemów
| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `OutOfMemoryError` podczas indeksowania | Rozmiar sterty jest zbyt mały | Zwiększ stertę JVM (`-Xmx2g` lub więcej) |
| Brak zwróconych wyników | Token fragmentu nie został przetworzony | Upewnij się, że pętla `while` działa aż `getNextChunkSearchToken()` będzie `null` |
| Wolna wydajność wyszukiwania | Indeks nie jest zoptymalizowany | Uruchom `index.optimize()` po masowych dodaniach |

## Najczęściej zadawane pytania

**Q: Czym jest wyszukiwanie oparte na fragmentach?**  
A: Wyszukiwanie oparte na fragmentach dzieli zestaw danych na mniejsze części, umożliwiając efektywne zapytania na dużych wolumenach danych bez ładowania całych dokumentów do pamięci.

**Q: Jak zaktualizować mój indeks o nowe pliki?**  
A: Po prostu wywołaj `index.add()` z ścieżką do nowych dokumentów; indeks automatycznie je uwzględni.

**Q: Czy GroupDocs.Search obsługuje różne formaty plików?**  
A: Tak, obsługuje PDF‑y, DOCX, XLSX, PPTX oraz wiele innych popularnych formatów.

**Q: Jakie są typowe wąskie gardła wydajności?**  
A: Ograniczenia pamięci i nieoptymalne indeksy są najczęstsze; przydziel wystarczającą pamięć heap i regularnie optymalizuj indeks.

**Q: Gdzie mogę znaleźć bardziej szczegółową dokumentację?**  
A: Odwiedź oficjalną [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) aby uzyskać szczegółowe przewodniki i odniesienia API.

**Q: Czy wyszukiwanie oparte na fragmentach działa z zaszyfrowanymi PDF‑ami?**  
A: Tak, pod warunkiem podania hasła za pomocą odpowiedniego przeciążenia API.

**Q: Jak mogę monitorować postęp indeksowania?**  
A: Użyj przeciążenia `Index.add()`, które zwraca obiekt `Progress`, lub podłącz się do wywołań zwrotnych logowania.

## Zasoby
- **Dokumentacja**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Referencja API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Pobierz**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Bezpłatne wsparcie**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Tymczasowa licencja**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Ostatnia aktualizacja:** 2026-02-21  
**Testowano z:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

---