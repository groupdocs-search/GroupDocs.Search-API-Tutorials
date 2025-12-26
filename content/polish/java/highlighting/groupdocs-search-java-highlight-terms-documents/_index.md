---
date: '2025-12-26'
description: Dowiedz się, jak wyszukiwać i podświetlać tekst w dokumentach przy użyciu
  GroupDocs.Search dla Javy. Poznaj techniki podświetlania całych dokumentów i fragmentów.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Wyszukiwanie i podświetlanie tekstu z GroupDocs.Search dla Javy
type: docs
url: /pl/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Wyszukiwanie i podświetlanie tekstu w dokumentach przy użyciu GroupDocs.Search dla Javy

W dzisiejszej erze cyfrowej **wyszukiwanie i podświetlanie tekstu** w ogromnych zbiorach dokumentów jest powszechnym wymaganiem. Niezależnie od tego, czy tworzysz narzędzie do przeglądu prawnego, portal badań akademickich, czy pulpit wsparcia klienta, możliwość natychmiastowego zlokalizowania i podkreślenia kluczowych terminów znacząco poprawia użyteczność. W tym kompleksowym przewodniku dowiesz się, jak zaimplementować **wyszukiwanie i podświetlanie tekstu** przy użyciu GroupDocs.Search dla Javy — obejmując zarówno podświetlanie całego dokumentu, jak i podświetlanie na poziomie fragmentów dla skoncentrowanego kontekstu.

## Szybkie odpowiedzi
- **Co oznacza „wyszukiwanie i podświetlanie tekstu”?** Odnosi się do znajdowania terminów zapytania w dokumencie i wizualnego podkreślania ich (np. za pomocą koloru tła).  
- **Która biblioteka zapewnia tę funkcjonalność?** GroupDocs.Search for Java.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna wystarcza do oceny; pełna licencja jest wymagana w środowisku produkcyjnym.  
- **Czy mogę dostosować kolory podświetlenia?** Tak — dowolny kolor RGB można ustawić za pomocą `HighlightOptions`.  
- **Czy obsługiwane jest podświetlanie fragmentów?** Absolutnie; możesz określić liczbę terminów przed i po dopasowaniu, aby utworzyć zwięzłe fragmenty.

## Co to jest wyszukiwanie i podświetlanie tekstu?
Wyszukiwanie i podświetlanie tekstu to proces skanowania indeksu dokumentów pod kątem określonego zapytania, pobierania pasujących dokumentów oraz oznaczania każdego wystąpienia terminu zapytania w wyjściu dokumentu (HTML, PDF itp.). Ten wizualny sygnał pomaga użytkownikom szybko zauważyć istotne informacje.

## Dlaczego warto używać GroupDocs.Search dla Javy?
- **Wysokowydajne indeksowanie** z konfigurowalną kompresją.  
- **Bogate API podświetlania** działające na całych dokumentach oraz na niestandardowych fragmentach.  
- **Obsługa wielu formatów** (DOCX, PDF, PPTX, TXT i inne).  
- **Łatwa integracja z Maven** oraz przejrzyste API skoncentrowane na Javie.

## Wymagania wstępne
- Java Development Kit (JDK) 8 lub nowszy.  
- Maven do zarządzania zależnościami.  
- IDE, takie jak IntelliJ IDEA lub Eclipse.  
- Podstawowa znajomość składni Javy.

## Konfiguracja GroupDocs.Search dla Javy

Dodaj repozytorium GroupDocs i zależność do swojego `pom.xml`:

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

Możesz także pobrać najnowszy plik JAR bezpośrednio z oficjalnej strony: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
Rozpocznij od wersji próbnej lub uzyskaj tymczasową licencję do oceny. W przypadku wdrożeń produkcyjnych zakup pełnej licencji, aby odblokować wszystkie funkcje.

## Przewodnik implementacji

Implementacja podzielona jest na dwie praktyczne sekcje: **podświetlanie w całych dokumentach** oraz **podświetlanie w fragmentach**. Obie sekcje zawierają niezbędne kroki, jak **podświetlać dokumenty Java** przy użyciu GroupDocs.Search.

### Konfigurowanie ustawień indeksu
Przed indeksowaniem skonfiguruj magazyn, aby używał wysokiej kompresji — zmniejsza to zużycie dysku przy zachowaniu szybkości wyszukiwania.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Podświetlanie w całych dokumentach

#### Krok 1: Utwórz i wypełnij indeks
Utwórz folder indeksu i dodaj wszystkie pliki źródłowe, które chcesz przeszukiwać.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Krok 2: Wykonaj wyszukiwanie i zastosuj podświetlanie
Wyszukaj termin (np. `ipsum`) i wygeneruj plik HTML z podświetlonymi dopasowaniami.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Wyjaśnienie kluczowych opcji**
- **Compression** – wysoka kompresja oszczędza miejsce na dysku.  
- **HighlightColor** – ustaw dowolną wartość RGB, aby dopasować do palety UI.  
- **UseInlineStyles** – `false` generuje czysty HTML, który można stylować globalnie przy użyciu CSS.

### Podświetlanie w fragmentach

#### Krok 1: Indeksowanie i wyszukiwanie (takie same jak powyżej)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Krok 2: Zdefiniuj kontekst fragmentu i podświetl
Określ, ile terminów przed i po dopasowaniu ma się pojawić w każdym fragmencie.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### Krok 3: Pobierz i zapisz podświetlone fragmenty
Zbierz wygenerowane fragmenty i zapisz je do pliku HTML.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Praktyczne zastosowania
1. **Legal Document Review** – natychmiastowe podświetlanie ustaw, klauzul lub odniesień do spraw.  
2. **Academic Research** – wyświetlanie kluczowej terminologii wśród dziesiątek plików PDF i Word.  
3. **Customer Support** – wskazywanie numerów zamówień lub kodów błędów w historii zgłoszeń.

## Rozważania dotyczące wydajności
- **Index Size** – wysoka kompresja (`Compression.High`) zmniejsza rozmiar na dysku.  
- **Fragment Context** – większe wartości `termsBefore/After` zwiększają dokładność, ale mogą wpływać na szybkość.  
- **Memory Management** – monitoruj pamięć JVM podczas indeksowania dużych korpusów; rozważ indeksowanie przyrostowe dla bardzo dużych zestawów.

## Typowe problemy i rozwiązania
- **Indexing Errors** – sprawdź ścieżki plików i upewnij się, że aplikacja ma uprawnienia do odczytu/zapisu.  
- **No Highlights Appear** – potwierdź, że `UseInlineStyles` odpowiada formatowi wyjściowemu (HTML vs. PDF).  
- **Color Not Applied** – upewnij się, że wartości RGB mieszczą się w zakresie 0‑255 i że przeglądarka HTML obsługuje styl.

## Najczęściej zadawane pytania

**Q: Jakie są korzyści z używania GroupDocs.Search dla Javy?**  
A: Oferuje szybkie, skalowalne indeksowanie, konfigurowalne podświetlanie oraz obsługę wielu formatów dokumentów.

**Q: Jak mogę zintegrować GroupDocs.Search z API REST?**  
A: Udostępnij metody wyszukiwania i podświetlania poprzez kontrolery Spring Boot, zwracając ładunki HTML lub JSON.

**Q: Czy biblioteka obsługuje pliki zabezpieczone hasłem?**  
A: Tak — podaj hasło przy dodawaniu dokumentu do indeksu.

**Q: Czy mogę dostosować znacznik podświetlenia poza kolorem?**  
A: Oczywiście; możesz wstrzyknąć klasy CSS za pomocą `HighlightOptions` lub zmodyfikować HTML po wygenerowaniu.

**Q: Jaką wersję testowano w tym przewodniku?**  
A: Kod został zweryfikowany pod kątem GroupDocs.Search 25.4.

---

**Ostatnia aktualizacja:** 2025-12-26  
**Testowano z:** GroupDocs.Search 25.4  
**Autor:** GroupDocs