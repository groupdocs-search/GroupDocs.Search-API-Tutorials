---
date: '2026-04-02'
description: Dowiedz się, jak utworzyć indeks wyszukiwania w GroupDocs i dodać dokumenty
  do indeksu, jednocześnie implementując wyszukiwanie fasetowe przy użyciu GroupDocs.Search
  i GroupDocs.Redaction w .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Utwórz indeks wyszukiwania GroupDocs z redakcją .NET – wyszukiwanie fasetowe
type: docs
url: /pl/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Utwórz indeks wyszukiwania GroupDocs z Redaction .NET Wyszukiwanie fasetowe

## Szybkie odpowiedzi
- **Jaki jest główny cel?** Aby utworzyć indeks wyszukiwania z GroupDocs i włączyć wyszukiwanie fasetowe.  
- **Jakie biblioteki są wymagane?** GroupDocs.Redaction i GroupDocs.Search dla .NET.  
- **Jak dodać dokumenty do indeksu?** Użyj `index.Add(documentsFolder)` po zainicjowaniu indeksu.  
- **Czy mogę uruchamiać złożone zapytania?** Tak, łącz zapytania obiektowe z operatorami logicznymi w celu zaawansowanego filtrowania.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w produkcji.

## Czym jest wyszukiwanie fasetowe i dlaczego używać go z GroupDocs?
Wyszukiwanie fasetowe pozwala użytkownikom precyzować wyniki, stosując jednocześnie wiele filtrów — takich jak kategoria, data czy autor. W połączeniu z **GroupDocs.Redaction** uzyskujesz bezpieczną, przeszukiwalną treść, która respektuje zasady redakcji, co czyni ją idealną dla środowisk o wysokich wymaganiach zgodności.

## Prerequisites

### Wymagane biblioteki, wersje i zależności
- **GroupDocs.Redaction .NET** – najnowsze stabilne wydanie.  
- **GroupDocs.Search .NET** – współpracuje z Redaction przy indeksowaniu.

### Wymagania dotyczące konfiguracji środowiska
- **IDE**: Visual Studio 2019 lub nowszy.  
- **Framework**: .NET Core 3.1, .NET 5 lub .NET 6.  
- **Kompatybilność systemu operacyjnego**: Windows, Linux, macOS.

### Wymagania wiedzy
Podstawowe umiejętności C# oraz ogólne zrozumienie koncepcji wyszukiwania fasetowego będą pomocne, ale przewodnik krok po kroku jest przyjazny także dla początkujących.

## Konfiguracja GroupDocs.Redaction dla .NET

### Informacje o instalacji
Możesz dodać pakiet GroupDocs.Redaction za pomocą jednej z następujących metod:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Wyszukaj "GroupDocs.Redaction" i zainstaluj najnowszą wersję.

### Kroki uzyskania licencji
Aby odblokować wszystkie funkcje, rozpocznij od wersji próbnej lub uzyskaj stałą licencję:

1. Odwiedź [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/), aby zapoznać się z opcjami licencjonowania.  
2. Postępuj zgodnie z instrukcjami wyświetlanymi na ekranie, aby otrzymać plik licencji próbnej lub zakupionej.

### Podstawowa inicjalizacja i konfiguracja
Po zainstalowaniu pakietu, zainicjalizuj Redactor w swojej aplikacji:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Jak utworzyć indeks wyszukiwania groupdocs

Poniżej dzielimy implementację na dwie części: **Simple Faceted Search** i **Complex Query**. Każda część pokazuje, jak **utworzyć indeks wyszukiwania groupdocs**, dodać dokumenty i uruchomić zapytania.

### Funkcja 1: Proste wyszukiwanie fasetowe

**Przegląd**  
Wyszukiwanie fasetowe pozwala użytkownikom zawęzić wyniki, wybierając wiele kryteriów. Ta sekcja demonstruje prostą metodę przy użyciu GroupDocs.Search.

#### Krok 1: Zdefiniuj foldery indeksu i dokumentów
Ustaw ścieżki folderów, w których będzie przechowywany indeks oraz w których znajdują się dokumenty źródłowe.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Krok 2: Utwórz indeks
Zainicjalizuj indeks wyszukiwania w zdefiniowanym folderze.

```csharp
Index index = new Index(indexFolder);
```

#### Krok 3: Dodaj dokumenty do indeksu
Załaduj dokumenty, aby stały się przeszukiwalne.

```csharp
index.Add(documentsFolder);
```

#### Krok 4: Wykonaj wyszukiwanie zapytania tekstowego
Uruchom podstawowe zapytanie tekstowe względem pola **content**.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Krok 5: Wykonaj wyszukiwanie zapytania obiektowego
Użyj zapytań obiektowych dla większej kontroli.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Funkcja 2: Złożone zapytanie

**Przegląd**  
Gdy potrzebujesz połączyć wiele filtrów — takich jak wzorce nazw plików i dopasowania fraz — możesz zbudować złożone zapytanie przy użyciu operatorów logicznych.

#### Krok 1: Zdefiniuj foldery indeksu i dokumentów
Użyj tej samej struktury folderów w bardziej zaawansowanym scenariuszu.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Krok 2: Utwórz indeks i dodaj dokumenty
(Zobacz kroki 2‑3 z prostego przykładu; pozostają takie same.)

#### Krok 3: Wykonaj wyszukiwanie zapytania tekstowego
Uruchom złożone zapytanie tekstowe, które łączy kryteria nazwy pliku i zawartości.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Krok 4: Zbuduj i wykonaj zapytania obiektowe
Zbuduj tę samą logikę programowo.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Kontynuuj łączenie fraz, zakresów i operatorów logicznych, aby dopasować dokładne reguły biznesowe.

## Praktyczne zastosowania

1. **Platformy e‑commerce** – Filtruj produkty według kategorii, ceny i oceny.  
2. **Systemy zarządzania dokumentami** – Znajdź umowy według autora, daty lub poziomu poufności.  
3. **Portale treści** – Pozwól czytelnikom zagłębiać się w treść według tagów, tematów i dat publikacji.

## Uwagi dotyczące wydajności

- **Odświeżanie indeksu**: Regularnie indeksuj ponownie nowe lub zaktualizowane pliki, aby utrzymać szybkie wyszukiwanie.  
- **Zarządzanie pamięcią**: Zwolnij obiekty `Index` po zakończeniu, szczególnie przy dużych zestawach danych.  
- **Indeksowanie asynchroniczne**: Użyj `Task.Run` lub usług w tle, aby uniknąć zacięć interfejsu podczas intensywnego indeksowania.

## Częste problemy i rozwiązania

| Problem | Rozwiązanie |
|---------|-------------|
| **Indeks nie znaleziony** | Sprawdź ścieżkę `indexFolder` i upewnij się, że folder ma uprawnienia do zapisu. |
| **Brak wyników** | Sprawdź, czy pola, które zapytujesz (np. `Content`, `Filename`), są zaindeksowane. |
| **Błędy braku pamięci** | Przetwarzaj dokumenty w partiach i rozważ zwiększenie rozmiaru sterty .NET GC. |

## Najczęściej zadawane pytania

**Q: Czym jest wyszukiwanie fasetowe?**  
A: Wyszukiwanie fasetowe pozwala użytkownikom precyzować wyniki przy użyciu wielu niezależnych filtrów, takich jak kategoria, data czy autor.

**Q: Jak obsługiwać duże zestawy danych z GroupDocs.Search?**  
A: Używaj indeksowania przyrostowego, przetwarzania w partiach i operacji asynchronicznych, aby utrzymać niskie zużycie pamięci i wysoką wydajność.

**Q: Czy mogę zintegrować funkcjonalności GroupDocs z istniejącymi aplikacjami .NET?**  
A: Tak, biblioteki są zaprojektowane do płynnej integracji z dowolnym projektem .NET.

**Q: Jakie są typowe problemy z wyszukiwaniem fasetowym?**  
A: Złożona składnia zapytań oraz zapewnienie, że wszystkie istotne pola są zaindeksowane, to typowe wyzwania; odpowiednie testowanie i utrzymanie indeksu je łagodzą.

**Q: Jak uzyskać tymczasową licencję dla GroupDocs?**  
A: Odwiedź [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/), aby ubiegać się o licencję próbną, która odblokowuje pełną funkcjonalność podczas oceny.

## Zasoby
- **Dokumentacja**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **Referencja API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Ostatnia aktualizacja:** 2026-04-02  
**Testowano z:** GroupDocs.Redaction 23.12 for .NET, GroupDocs.Search 23.12 for .NET  
**Autor:** GroupDocs