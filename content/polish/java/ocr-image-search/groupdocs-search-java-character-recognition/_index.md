---
date: '2026-03-17'
description: Dowiedz się, jak utworzyć indeks przy użyciu GroupDocs.Search dla Javy,
  skonfigurować zwykłe i mieszane znaki oraz zoptymalizować wyszukiwanie numerów spraw
  sądowych i obrazów OCR.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Jak utworzyć indeks z rozpoznawaniem znaków w Javie
type: docs
url: /pl/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Jak utworzyć indeks z rozpoznawaniem znaków przy użyciu GroupDocs.Search dla Javy

W nowoczesnych aplikacjach intensywnie pracujących z dokumentami, **jak utworzyć indeks**, który uwzględnia niuanse Twojego tekstu — takie jak myślniki, podkreślenia czy symbole specyficzne dla języka — jest niezbędny do szybkiego i dokładnego wyszukiwania. W tym samouczku przeprowadzimy konfigurację rozpoznawania znaków w **GroupDocs.Search for Java**, obejmując zarówno zwykłe znaki (litery, cyfry, podkreślenia), jak i znaki mieszane (np. myślniki). Po zakończeniu będziesz w stanie dostosować indeks do dokładnych potrzeb scenariusza OCR lub wyszukiwania obrazów, niezależnie od tego, czy indeksujesz numery spraw prawnych, repozytoria kodu źródłowego czy wielojęzyczne pliki PDF.

## Szybkie odpowiedzi
- **Co oznacza „create custom search index”?** Oznacza to konfigurację indeksu tak, aby traktował określone symbole jako litery lub znaki mieszane, zamiast je ignorować.  
- **Jakiej biblioteki użyto?** GroupDocs.Search for Java (v25.4 w momencie pisania).  
- **Czy potrzebna jest licencja?** Bezpłatna wersja próbna działa w środowisku deweloperskim; płatna licencja jest wymagana w produkcji.  
- **Czy mogę indeksować zarówno PDF‑y, jak i obrazy?** Tak — GroupDocs.Search obsługuje OCR na obrazach i PDF‑ach po odpowiedniej konfiguracji.  
- **Czy Maven jest wymagany?** Maven jest zalecaną metodą zarządzania zależnościami, ale możesz również użyć Gradle lub ręcznych plików JAR.

## Czym jest niestandardowy indeks wyszukiwania?
Niestandardowy indeks wyszukiwania pozwala określić, jak silnik wyszukiwania interpretuje znaki. Domyślnie wiele symboli jest ignorowanych, co może prowadzić do pominiętych dopasowań, np. numerów spraw (`2023-AB-456`) lub fragmentów kodu (`my_variable`). Dostosowanie słownika alfabetu daje pełną kontrolę nad tym, co silnik traktuje jako tekst przeszukiwalny.

## Dlaczego konfigurować zwykłe i mieszane znaki dla numerów spraw prawnych?
- **Zwykłe znaki** (litery, cyfry, podkreślenia) są tokenizowane osobno, umożliwiając dokładne wyszukiwanie identyfikatorów.  
- **Mieszane znaki** (myślniki, ukośniki) utrzymują powiązane tokeny razem, zapobiegając niepożądanemu rozdzielaniu numerów spraw, kodów produktów czy ścieżek plików.  
- Ta konfiguracja **optymalizuje wydajność indeksu wyszukiwania** poprzez zmniejszenie fragmentacji tokenów i poprawę trafności wyników dla treści generowanych przez OCR.

## Wymagania wstępne
- **JDK 8** lub nowszy zainstalowany.  
- **Maven** do zarządzania zależnościami.  
- Dostęp do biblioteki **GroupDocs.Search for Java** (pobranej przez Maven lub ze strony oficjalnej).  

### Wymagane biblioteki i zależności
Dodaj repozytorium i wpisy zależności do swojego `pom.xml` (jak pokazano poniżej). Blok XML musi pozostać niezmieniony.

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

Możesz także pobrać najnowsze pliki JAR z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
- **Free Trial** – idealna do wczesnych eksperymentów.  
- **Temporary License** – przydatna przy dłuższych cyklach rozwojowych.  
- **Production License** – wymagana przy wdrożeniach komercyjnych.  

Uzyskaj licencję w oficjalnym portalu: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Podstawowa inicjalizacja
Poniższy fragment kodu pokazuje minimalny kod potrzebny do uruchomienia pustego indeksu. Zachowaj go w niezmienionej formie; później rozbudujemy go.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Konfiguracja GroupDocs.Search dla Javy

### Instalacja za pomocą Maven
Konfiguracja Maven z sekcji *Wymagania wstępne* to wszystko, czego potrzebujesz. Po jej dodaniu uruchom `mvn clean install`, aby pobrać binaria.

### Wymagania dotyczące konfiguracji środowiska
- Upewnij się, że **folder indeksu** i **folder dokumentów** istnieją na dysku.  
- Używaj ścieżek bezwzględnych lub skonfiguruj IDE tak, aby poprawnie rozwiązywało ścieżki względne.  

## Przewodnik implementacji

Poniżej przechodzimy przez dwie odrębne funkcje: **zwykłe znaki** i **mieszane znaki**. Każda funkcja podąża za tym samym schematem — definiuj ścieżki, twórz indeks, ustaw słownik znaków i na końcu indeksuj dokumenty.

### Funkcja 1 – Zwykłe znaki

#### Przegląd
Zwykłe znaki są traktowane jako niezależne tokeny. Jest to idealne rozwiązanie, gdy chcesz, aby cyfry, litery i podkreślenia były wyszukiwalne dokładnie tak, jak się pojawiają.

#### Implementacja krok po kroku

**1️⃣ Set Up Paths**  
Zdefiniuj, gdzie indeks będzie przechowywany oraz gdzie znajdują się źródłowe dokumenty.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  
Zainicjuj indeks i wyczyść wszelkie istniejące wcześniej konfiguracje alfabetu.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Define Regular Characters**  
Zbuduj tablicę znaków, która zawiera cyfry, litery łacińskie oraz podkreślenie.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Index Documents**  
Dodaj wszystkie pliki z folderu źródłowego do nowo skonfigurowanego indeksu.

```java
index.add(documentFolder);
```

### Funkcja 2 – Mieszane znaki

#### Przegląd
Mieszane znaki (np. myślniki) często łączą dwa wyrazy. Oznaczenie ich jako *mieszane* informuje silnik, aby podczas indeksowania utrzymał otaczające tokeny razem.

#### Implementacja krok po kroku

**1️⃣ Set Up Paths**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Define Blended Characters**  
Tutaj informujemy słownik, że myślnik powinien być traktowany jako znak mieszany.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index Documents**  

```java
index.add(documentFolder);
```

## Praktyczne zastosowania

### Przypadek użycia 1 – Zarządzanie dokumentami prawnymi
Pliki prawne często zawierają numery spraw, np. `2023-AB-456`. Konfigurując podkreślenia i myślniki, wyszukiwania zwracają dokładne dopasowania bez rozdzielania identyfikatora, co pomaga **wyszukiwać numery spraw prawnych** efektywnie.

### Przypadek użycia 2 – Repozytoria kodu źródłowego
Programiści muszą przeszukiwać fragmenty kodu, w których podkreślenia (`my_variable`) i myślniki (`my-function`) mają znaczenie. Niestandardowe rozpoznawanie znaków zapewnia, że silnik wyszukiwania respektuje te symbole.

### Przypadek użycia 3 – Zestawy danych wielojęzycznych
Pracując z językami używającymi dodatkowych alfabetów, możesz **rozszerzyć zestaw znaków Unicode**, aby obejmował te zakresy, gwarantując dokładne wyniki wyszukiwania międzyjęzykowego.

### Przypadek użycia 4 – Indeksowanie obrazów PDF
Jeśli indeksujesz zeskanowane PDF‑y lub pliki graficzne, wynik OCR często zawiera mieszane znaki. Poprawna konfiguracja zwykłych i mieszanych znaków **optymalizuje wydajność indeksu wyszukiwania** dla treści opartych na obrazach.

## Rozważania dotyczące wydajności

- **Resource Management** – Monitoruj zużycie pamięci heap; duże indeksy korzystają z przyrostowych commitów.  
- **Garbage Collection** – Zwolnij obiekty `Index`, gdy nie są już potrzebne, aby JVM mógł odzyskać pamięć.  
- **Index Optimization** – Okresowo wywołuj `index.optimize()` (jeśli dostępne), aby skompaktować indeks i przyspieszyć zapytania.  

## Zakończenie

Teraz wiesz **jak utworzyć indeks**, który rozróżnia zwykłe i mieszane znaki przy użyciu GroupDocs.Search dla Javy. Ta precyzyjna kontrola umożliwia budowanie rozwiązań wyszukiwania świadomych OCR, o wysokiej wydajności, dopasowanych do środowisk prawnych, deweloperskich czy wielojęzycznych.

### Kolejne kroki
- Eksperymentuj z dodatkowymi zakresami Unicode dla alfabetów nie‑łacińskich.  
- Połącz konfigurację znaków z innymi funkcjami GroupDocs.Search, takimi jak stemming czy synonimy.  
- Zintegruj indeks z API REST, aby udostępnić możliwości wyszukiwania aplikacjom front‑endowym.

## Najczęściej zadawane pytania

**Q:** *Jaki jest cel `CharacterType.Letter`?*  
**A:** Informuje indeks, aby traktował podane znaki jako zwykłe litery, więc są one tokenizowane osobno podczas indeksowania.

**Q:** *Czy mogę mieszać zwykłe i mieszane znaki w tym samym indeksie?*  
**A:** Tak — po prostu wywołaj `setRange` dla każdego typu; słownik obsłuży obie konfiguracje jednocześnie.

**Q:** *Czy muszę przebudować indeks po zmianie alfabetu?*  
**A:** Zdecydowanie. Zmiany w słowniku znaków wpływają na tokenizację, więc musisz ponownie zindeksować dokumenty, aby zastosować nowe zasady.

**Q:** *Czy istnieje limit liczby niestandardowych znaków, które mogę zdefiniować?*  
**A:** Biblioteka obsługuje pełny zakres Unicode; wydajność może spaść, jeśli dodasz niezwykle dużą liczbę znaków, dlatego ogranicz je do rzeczywiście potrzebnych.

**Q:** *Jak to wpływa na dokładność OCR?*  
**A:** Dzięki dopasowaniu zestawu znaków indeksu do wyjścia silnika OCR zmniejszasz liczbę fałszywych negatywów i poprawiasz ogólną trafność wyników wyszukiwania.

---

**Last Updated:** 2026-03-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---