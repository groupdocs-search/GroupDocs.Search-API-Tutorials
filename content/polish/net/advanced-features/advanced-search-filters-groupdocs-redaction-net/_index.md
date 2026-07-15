---
date: '2026-04-02'
description: Dowiedz się, jak filtrować według rozszerzenia pliku i wyszukiwać tylko
  pliki txt za pomocą GroupDocs.Redaction dla .NET — zwiększ efektywność zarządzania
  dokumentami.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Filtrowanie według rozszerzenia pliku w .NET przy użyciu GroupDocs.Redaction
type: docs
url: /pl/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Filtrowanie według rozszerzenia pliku w .NET przy użyciu GroupDocs.Redaction

Przeglądanie ogromnej kolekcji plików może być przytłaczające, szczególnie gdy potrzebujesz wyników tylko z określonych typów plików. W tym samouczku odkryjesz **jak filtrować według rozszerzenia pliku** przy użyciu GroupDocs.Redaction dla .NET, co pozwoli Ci wyszukiwać tylko pliki txt lub dowolne inne wybrane rozszerzenie. Przeprowadzimy Cię przez konfigurację zarówno filtrów typu pliku, jak i filtrów opartych na ścieżce, abyś mógł szybko zlokalizować dokładnie potrzebne dokumenty.

## Szybkie odpowiedzi
- **Co robi „filter by file extension”?** Ogranicza wyszukiwanie do dokumentów, które mają określone rozszerzenie pliku (np. *.txt).  
- **Dlaczego używać GroupDocs.Redaction do tego?** Dostarcza wbudowane API filtrujące, które są szybkie i łatwe do integracji.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa do testów; płatna licencja jest wymagana w środowisku produkcyjnym.  
- **Jakie wersje .NET są wspierane?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Czy mogę łączyć filtry typu pliku i ścieżki?** Tak — zastosuj wiele filtrów dla bardzo precyzyjnych wyszukiwań.

## Czego się nauczysz
- Jak **filtrować według rozszerzenia pliku**, aby przeszukiwane były tylko pliki tekstowe.  
- Jak skonfigurować **filtry ścieżki pliku**, aby ograniczyć wyniki do konkretnych folderów lub wzorców nazewnictwa.  
- Wskazówki, jak utrzymać indeks szybki i oszczędny pod względem pamięci.

## Wymagania wstępne

Zanim zaczniesz, upewnij się, że masz:

- **GroupDocs.Redaction Library** zainstalowaną i kompatybilną z Twoim projektem .NET.  
- Środowisko programistyczne, takie jak Visual Studio lub VS Code.  
- Podstawową znajomość C# oraz struktury projektów .NET.

## Konfigurowanie GroupDocs.Redaction dla .NET

Najpierw dodaj bibliotekę do swojego projektu.

**Użycie .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Użycie Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

Lub znajdź „GroupDocs.Redaction” w interfejsie NuGet Package Manager i zainstaluj najnowszą wersję.

### Uzyskanie licencji

Możesz rozpocząć od darmowej wersji próbnej lub poprosić o tymczasową licencję. W przypadku długoterminowych projektów zakup licencję na oficjalnej stronie.

### Podstawowa inicjalizacja

Po zainstalowaniu pakietu, utwórz indeks, który będzie przechowywał odwołania do Twoich dokumentów:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Przewodnik po implementacji

### Funkcja 1: Ustawianie filtru dla dokumentów tekstowych (.txt)

#### Jak filtrować według rozszerzenia pliku dla dokumentów tekstowych

1. **Zdefiniuj indeks i foldery dokumentów**  
   Ustaw ścieżki, w których znajdują się Twoje pliki źródłowe:

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Utwórz indeks**  
   Załaduj wszystkie pliki z folderu źródłowego do indeksu:

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Skonfiguruj opcje wyszukiwania z filtrem rozszerzenia pliku**  
   Powiedz silnikowi, aby rozważał tylko pliki *.txt:

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Wykonaj wyszukiwanie**  
   Uruchom zapytanie; filtr zapewnia, że pliki nie‑tekstowe są pomijane:

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Explanation*: Metoda `Search` zwraca dopasowania spełniające filtr, co znacząco redukuje szum i poprawia wydajność.

### Funkcja 2: Filtry ścieżki pliku

#### Dlaczego używać filtrów ścieżki pliku?

Czasami trzeba ograniczyć wyszukiwanie do konkretnego folderu działu lub zestawu plików o wspólnej konwencji nazewnictwa. Filtry ścieżki pozwalają zrobić dokładnie to.

1. **Zdefiniuj indeks i foldery dokumentów**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Utwórz indeks**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Skonfiguruj opcje wyszukiwania z wyrażeniem regularnym opartym na ścieżce**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   To wyrażenie regularne dopasowuje każdy plik, którego pełna ścieżka zawiera słowo „Lorem”, umożliwiając celowanie w konkretne podfoldery.

4. **Wykonaj wyszukiwanie oparte na ścieżce**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Praktyczne zastosowania
- **Zarządzanie dokumentami prawnymi** – Szybko znajdź odpowiednie umowy przechowywane jako pliki tekstowe.  
- **Badania akademickie** – Pobierz tylko notatki badawcze *.txt, które należą do konkretnego folderu projektu.  
- **Raportowanie korporacyjne** – Filtruj wewnętrzne raporty według ścieżki działu (np. `/Finance/2025/`).  

## Rozważania dotyczące wydajności
- Indeksuj tylko typy dokumentów, które naprawdę potrzebujesz; niepotrzebne pliki zwiększają rozmiar indeksu i czas wyszukiwania.  
- Utrzymuj indeks aktualny za pomocą zaplanowanego zadania, które wywołuje `index.Add()` dla nowych lub zmienionych plików.  
- Używaj prostych wyrażeń regularnych; nadmiernie skomplikowane wzorce mogą spowolnić silnik wyszukiwania.  
- Zwolnij obiekty `Index`, gdy nie są już potrzebne, aby zwolnić pamięć.

## Zakończenie
Teraz wiesz, jak **filtrować według rozszerzenia pliku** i stosować **filtry ścieżki pliku** przy użyciu GroupDocs.Redaction dla .NET. Te techniki dają precyzyjną kontrolę nad dużymi zbiorami dokumentów, przyspieszając i zwiększając trafność wyszukiwań. Następnie eksperymentuj z łączeniem wielu filtrów lub integracją wyszukiwania w większy przepływ pracy aplikacji.

## Sekcja FAQ

**Q1: Czy mogę filtrować dokumenty inne niż pliki tekstowe?**  
A1: Tak, GroupDocs.Redaction obsługuje wiele formatów. Zmień argument w `CreateFileExtension` na pożądane rozszerzenie (np. ".pdf").

**Q2: Jak regularnie aktualizować mój indeks wyszukiwania?**  
A2: Zaplanuj usługę w tle lub zadanie cron, które uruchamia `index.Add()` na katalogach, które chcesz utrzymać aktualne.

**Q3: Czy filtrowanie według ścieżki pliku wpływa na wydajność?**  
A3: Odpowiednio zoptymalizowane wyrażenia regularne mają minimalny wpływ, ale zawsze przeprowadzaj testy wydajności na własnym zestawie danych.

**Q4: Czy mogę łączyć wiele filtrów dla bardziej precyzyjnych wyszukiwań?**  
A4: Oczywiście. Możesz łączyć filtry lub tworzyć filtry złożone, aby jednocześnie celować w typ pliku i ścieżkę.

**Q5: Gdzie mogę znaleźć więcej zasobów na temat GroupDocs.Redaction?**  
A5: Odwiedź oficjalną dokumentację pod adresem [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) aby uzyskać szczegółowe przewodniki i odniesienia API.

## Najczęściej zadawane pytania

**Q: Czy `SearchDocumentFilter` działa z zaszyfrowanymi plikami?**  
A: Sam filtr działa na metadanych pliku, więc zaszyfrowane pliki są nadal indeksowane, jeśli podczas indeksowania podasz niezbędne dane uwierzytelniające do odszyfrowania.

**Q: Czy mogę używać znaków wieloznacznych zamiast wyrażenia regularnego do filtrowania ścieżek?**  
A: API obecnie wymaga wyrażenia regularnego, ale możesz symulować proste wieloznaki (np. `.*` dla dowolnych znaków).

**Q: Jak duży może być indeks, zanim będę musiał rozważyć podział (sharding)?**  
A: Indeksy o rozmiarze kilku set gigabajtów mogą skorzystać z podziału na wiele logicznych indeksów; testuj wydajność w miarę wzrostu kolekcji.

**Q: Czy istnieją wbudowane metody usuwania dokumentów z indeksu?**  
A: Tak — wywołaj `index.Delete(documentId)` lub `index.DeleteAll()`, aby zarządzać przestarzałymi wpisami.

**Q: Czy istnieje sposób podglądu wyników wyszukiwania przed załadowaniem pełnego dokumentu?**  
A: Obiekt `SearchResult` zawiera informacje o fragmencie, które możesz wyświetlić w interfejsie użytkownika bez otwierania całego pliku.

## Zasoby
- **Dokumentacja**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **Referencja API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Pobierz**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **Darmowe wsparcie**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Tymczasowa licencja**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Ostatnia aktualizacja:** 2026-04-02  
**Testowano z:** GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs