---
date: '2026-01-11'
description: Dowiedz się, jak utworzyć niestandardowy indeks wyszukiwania przy użyciu
  GroupDocs.Search dla Javy, konfigurując zwykłe i mieszane znaki dla zaawansowanego
  OCR i wyszukiwania obrazów.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Utwórz niestandardowy indeks wyszukiwania z rozpoznawaniem znaków – GroupDocs.Search
  Java
type: docs
url: /pl/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Tworzenie niestandardowego indeksu wyszukiwania z rozpoznawaniem znaków przy użyciu GroupDocs.Search for Java

W nowoczesnych aplikacjach intensywnie pracujących z dokumentami, **tworzenie niestandardowego indeksu wyszukiwania**, który rozumie niuanse Twojego tekstu — takie jak myślniki, podkreślenia czy symbole specyficzne dla języka — jest niezbędne dla szybkiego i dokładnego wyszukiwania. Ten samouczek przeprowadzi Cię przez konfigurowanie rozpoznawania znaków w **GroupDocs.Search for Java**, obejmując zarówno zwykłe znaki (litery, cyfry, podkreślenia), jak i znaki mieszane (np. myślniki). Po zakończeniu będziesz mógł dostosować indeks do dokładnych potrzeb scenariusza OCR lub wyszukiwania obrazów.

## Szybkie odpowiedzi
- **Co oznacza „create custom search index”?** Oznacza to konfigurowanie indeksu tak, aby traktował określone symbole jako litery lub znaki mieszane, zamiast je ignorować.  
- **Jakiej biblioteki użyto?** GroupDocs.Search for Java (v25.4 w momencie pisania).  
- **Czy potrzebna jest licencja?** Bezpłatna wersja próbna działa w fazie rozwoju; płatna licencja jest wymagana w środowisku produkcyjnym.  
- **Czy mogę indeksować zarówno pliki PDF, jak i obrazy?** Tak — GroupDocs.Search obsługuje OCR na obrazach i plikach PDF po odpowiedniej konfiguracji.  
- **Czy Maven jest wymagany?** Maven jest zalecanym sposobem zarządzania zależnościami, ale można również używać Gradle lub ręcznych plików JAR.  

## Czym jest niestandardowy indeks wyszukiwania?
Niestandardowy indeks wyszukiwania pozwala określić, jak silnik wyszukiwania interpretuje znaki. Domyślnie wiele symboli jest ignorowanych, co może prowadzić do pominięcia dopasowań, np. numerów spraw (`ABC-123`) lub fragmentów kodu (`my_variable`). Dostosowanie słownika alfabetu daje pełną kontrolę nad tym, co silnik traktuje jako tekst podlegający wyszukiwaniu.

## Dlaczego konfigurować znaki zwykłe i mieszane?
- **Znaki zwykłe** (litery, cyfry, podkreślenia) są traktowane jako odrębne tokeny, co poprawia wyszukiwania dokładnych dopasowań.  
- **Znaki mieszane** (myślniki, ukośniki) łączą słowa; ich konfiguracja zapobiega niepożądanemu dzieleniu tokenów, co jest kluczowe dla odniesień prawnych, kodów produktów lub indeksowania kodu źródłowego.  

## Wymagania wstępne
- **JDK 8** lub nowszy zainstalowany.  
- **Maven** do zarządzania zależnościami.  
- Dostęp do biblioteki **GroupDocs.Search for Java** (pobranej przez Maven lub ze strony oficjalnej).  

### Wymagane biblioteki i zależności
Dodaj wpisy repozytorium i zależności do pliku `pom.xml` (jak pokazano poniżej). Blok XML musi pozostać niezmieniony.

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

Możesz także pobrać najnowsze pliki JAR z [Wydania GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/).

### Uzyskanie licencji
- **Bezpłatna wersja próbna** – idealna do wczesnych eksperymentów.  
- **Licencja tymczasowa** – przydatna przy dłuższych cyklach rozwoju.  
- **Licencja produkcyjna** – wymagana przy wdrożeniu komercyjnym.  

Uzyskaj licencję z oficjalnego portalu: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

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

## Konfiguracja GroupDocs.Search for Java

### Instalacja za pomocą Maven
Konfiguracja Maven z sekcji *Wymagania wstępne* to wszystko, czego potrzebujesz. Po jej dodaniu uruchom `mvn clean install`, aby pobrać pliki binarne.

### Wymagania dotyczące konfiguracji środowiska
- Upewnij się, że **folder indeksu** i **folder dokumentów** istnieją na dysku.  
- Używaj ścieżek bezwzględnych lub skonfiguruj IDE tak, aby poprawnie rozwiązywało ścieżki względne.  

## Przewodnik implementacji

Poniżej przeprowadzimy Cię przez dwie odrębne funkcje: **znaki zwykłe** i **znaki mieszane**. Każda funkcja podąża za tym samym schematem — definiowanie ścieżek, tworzenie indeksu, ustawienie słownika znaków i w końcu indeksowanie dokumentów.

### Funkcja 1 – Znaki zwykłe

#### Przegląd
Znaki zwykłe są traktowane jako niezależne tokeny. Jest to idealne, gdy chcesz, aby cyfry, litery i podkreślenia były wyszukiwalne dokładnie tak, jak się pojawiają.

#### Implementacja krok po kroku

**1️⃣ Ustawienie ścieżek**  
Określ, gdzie będzie przechowywany indeks oraz gdzie znajdują się źródłowe dokumenty.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Utworzenie i konfiguracja indeksu**  
Zainicjuj indeks i wyczyść wszelką istniejącą wcześniej konfigurację alfabetu.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Definicja znaków zwykłych**  
Utwórz tablicę znaków, która zawiera cyfry, litery łacińskie oraz podkreślenie.

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

**4️⃣ Indeksowanie dokumentów**  
Dodaj wszystkie pliki z folderu źródłowego do nowo skonfigurowanego indeksu.

```java
index.add(documentFolder);
```

### Funkcja 2 – Znaki mieszane

#### Przegląd
Znaki mieszane (np. myślniki) często łączą dwa słowa. Oznaczenie ich jako *mieszane* informuje silnik, aby podczas indeksowania utrzymał otaczające tokeny razem.

#### Implementacja krok po kroku

**1️⃣ Ustawienie ścieżek**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Utworzenie i konfiguracja indeksu**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Definicja znaków mieszanych**  
Tutaj informujemy słownik, że myślnik powinien być traktowany jako znak mieszany.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Indeksowanie dokumentów**  

```java
index.add(documentFolder);
```

## Praktyczne zastosowania

### Przypadek użycia 1 – Zarządzanie dokumentami prawnymi
Pliki prawne często zawierają numery spraw, np. `2023-AB-456`. Dzięki konfiguracji podkreśleń i myślników, wyszukiwania zwracają dokładne dopasowania bez rozdzielania identyfikatora.

### Przypadek użycia 2 – Repozytoria kodu źródłowego
Programiści muszą przeszukiwać fragmenty kodu, w których podkreślenia (`my_variable`) i myślniki (`my-function`) mają znaczenie. Niestandardowe rozpoznawanie znaków zapewnia, że silnik wyszukiwania respektuje te symbole.

### Przypadek użycia 3 – Zbiory danych wielojęzycznych
Pracując z językami używającymi dodatkowych alfabetów, możesz rozszerzyć zestaw znaków zwykłych o te zakresy Unicode, co zapewnia dokładne wyniki wyszukiwania międzyjęzykowego.

## Rozważania dotyczące wydajności

- **Zarządzanie zasobami** – Monitoruj zużycie pamięci heap; duże indeksy korzystają z przyrostowych commitów.  
- **Garbage Collection** – Zwolnij obiekty `Index` po zakończeniu, aby JVM mogło odzyskać pamięć.  
- **Optymalizacja indeksu** – Okresowo wywołuj `index.optimize()` (jeśli dostępne), aby skompaktować indeks i zwiększyć szybkość zapytań.  

## Zakończenie

Teraz wiesz, jak **tworzyć niestandardowy indeks wyszukiwania**, który rozróżnia znaki zwykłe i mieszane przy użyciu GroupDocs.Search for Java. Ta precyzyjna kontrola umożliwia budowanie rozwiązań wyszukiwania z uwzględnieniem OCR, o wysokiej wydajności, dostosowanych do środowisk prawnych, deweloperskich lub wielojęzycznych.

**Kolejne kroki**  
- Eksperymentuj z dodatkowymi zakresami Unicode dla alfabetów niełacińskich.  
- Połącz konfigurację znaków z innymi funkcjami GroupDocs.Search, takimi jak stemming czy synonimy.  
- Zintegruj indeks z API REST, aby udostępnić możliwości wyszukiwania aplikacjom front‑end.

## Najczęściej zadawane pytania

**P:** *Jaki jest cel `CharacterType.Letter`?*  
**O:** Informuje indeks, aby traktował podane znaki jako zwykłe litery, dzięki czemu są tokenizowane osobno podczas indeksowania.

**P:** *Czy mogę mieszać znaki zwykłe i mieszane w tym samym indeksie?*  
**O:** Tak — po prostu wywołaj `setRange` dla każdego typu; słownik obsłuży obie konfiguracje jednocześnie.

**P:** *Czy muszę przebudować indeks po zmianie alfabetu?*  
**O:** Zdecydowanie tak. Zmiany w słowniku znaków wpływają na tokenizację, więc musisz ponownie zindeksować dokumenty, aby zastosować nowe reguły.

**P:** *Czy istnieje limit liczby niestandardowych znaków, które mogę zdefiniować?*  
**O:** Biblioteka obsługuje pełny zakres Unicode; wydajność może spaść, jeśli dodasz bardzo dużą liczbę znaków, więc ogranicz je do rzeczywiście potrzebnych.

**P:** *Jak to wpływa na dokładność OCR?*  
**O:** Dopasowując zestaw znaków indeksu do wyjścia silnika OCR, zmniejszasz liczbę fałszywych negatywów i poprawiasz ogólną trafność wyników wyszukiwania.

---

**Ostatnia aktualizacja:** 2026-01-11  
**Testowano z:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

---