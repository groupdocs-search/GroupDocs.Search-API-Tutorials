---
date: '2026-04-21'
description: Dowiedz się, jak filtrować pliki przy użyciu GroupDocs.Redaction dla
  .NET, w tym filtrować według daty utworzenia, rozmiaru pliku, daty modyfikacji oraz
  jak stosować filtry NOT.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Jak filtrować pliki przy użyciu GroupDocs.Redaction dla .NET
type: docs
url: /pl/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Jak filtrować pliki za pomocą GroupDocs.Redaction dla .NET

W dzisiejszym szybkim środowisku cyfrowym, **jak filtrować pliki** efektywnie może decydować o Twojej wydajności. Niezależnie od tego, czy musisz wyodrębnić dokumenty według rozszerzenia, daty utworzenia, rozmiaru lub daty modyfikacji, solidna strategia filtrowania oszczędza czas, zmniejsza koszty przechowywania i utrzymuje porządek w indeksie wyszukiwania. W tym samouczku przeprowadzimy Cię przez praktyczne przykłady z użyciem GroupDocs.Redaction dla .NET, pokazując dokładnie, jak filtrować pliki, aby spełnić typowe potrzeby biznesowe.

## Szybkie odpowiedzi
- **Jakiej biblioteki potrzebuję?** GroupDocs.Redaction for .NET (zainstaluj przez NuGet).  
- **Czy mogę filtrować według daty utworzenia?** Tak – użyj `CreateCreationTimeRange`.  
- **Jak wykluczyć określone typy?** Zastosuj filtr NOT za pomocą `DocumentFilter.CreateNot`.  
- **Czy filtrowanie według rozmiaru pliku jest obsługiwane?** Absolutnie, za pomocą `CreateFileLengthRange` lub górnych/dolnych granic.  
- **Czy potrzebna jest licencja?** Wymagana jest licencja próbna lub pełna do użytku produkcyjnego.

## Czym jest filtrowanie plików w GroupDocs.Redaction?
Filtrowanie plików pozwala określić silnikowi indeksującemu, które dokumenty mają być uwzględnione lub pominięte na podstawie metadanych, takich jak rozszerzenie, daty, wzorce ścieżek lub rozmiar. Definiując precyzyjne reguły `DocumentFilter`, utrzymujesz indeks lekki, a wyszukiwania szybkie.

## Dlaczego warto używać GroupDocs.Redaction dla .NET?
- **Wbudowane pomocniki filtrów** – nie ma potrzeby pisać własnego kodu systemu plików.  
- **Operatory logiczne** – łącz wiele kryteriów za pomocą AND, OR i NOT.  
- **Optymalizacja wydajności** – filtry są stosowane podczas indeksowania, a nie po nim.  
- **Wieloplatformowy** – działa z .NET Framework, .NET Core oraz .NET 5/6+.

## Wymagania wstępne
- .NET Framework 4.6+ lub .NET Core 3.1+ zainstalowany.  
- Visual Studio lub ulubione IDE C#.  
- Podstawowa znajomość C#.

### Wymagane biblioteki i konfiguracja
Zainstaluj pakiet NuGet, używając preferowanej metody:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Wskazówka:** Po instalacji dodaj plik licencji do katalogu głównego projektu i wywołaj `License.SetLicense("license-file-path")` przed utworzeniem jakichkolwiek obiektów Redactor lub Index.

## Konfiguracja GroupDocs.Redaction dla .NET

Najpierw utwórz instancję `Redactor`, która wskazuje dokument, z którym chcesz pracować:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Dlaczego to ważne:** Inicjalizacja Redactor zapewnia, że biblioteka jest gotowa do zastosowania filtrów i reguł redakcji później w przepływie pracy.

## Jak filtrować pliki według rozszerzenia

Filtrowanie według rozszerzenia pliku jest najczęstszym sposobem zawężenia zestawu dokumentów. Poniżej zachowujemy tylko pliki FB2, EPUB i TXT.

### Filtrowanie według rozszerzenia pliku

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Jak zastosować filtr NOT, aby wykluczyć niepożądane typy

Jeśli potrzebujesz **zastosować logikę filtru NOT** — na przykład wykluczyć pliki HTML i PDF — użyj `CreateNot`.

### Wyklucz pliki HTM, HTML i PDF

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Jak filtrować pliki według daty utworzenia

Gdy potrzebujesz **filtrować według daty utworzenia**, określ początkowy i końcowy `DateTime`.

### Filtrowanie według zakresu dat utworzenia

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Jak filtrować pliki według daty modyfikacji

Podobnie jak w przypadku dat utworzenia, możesz ograniczyć wyniki do plików zmodyfikowanych przed określonym momentem.

### Filtrowanie według daty modyfikacji

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Jak filtrować pliki według ścieżki przy użyciu wyrażeń regularnych

Jeśli struktura folderów podąża za konwencjami nazewniczymi, wyrażenie regularne może celować w określone ścieżki.

### Filtrowanie według wzorca ścieżki pliku

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Jak filtrować pliki według rozmiaru

Kontrola rozmiaru dokumentu jest niezbędna przy ograniczeniach przepustowości lub pojemności pamięci.

### Filtrowanie według rozmiaru pliku (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Jak połączyć wiele warunków za pomocą AND

Gdy potrzebujesz **jak filtrować pliki** przy użyciu kilku kryteriów jednocześnie, połącz je za pomocą `CreateAnd`.

### Przykład logicznego AND

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Jak połączyć wiele warunków za pomocą OR

Użyj `CreateOr`, gdy dowolna z kilku reguł powinna zostać spełniona.

### Przykład logicznego OR

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Częste problemy i rozwiązania
- **Filtr nie zastosowany:** Upewnij się, że przypisujesz `settings.DocumentFilter` **przed** utworzeniem instancji `Index`.  
- **Pojawiają się nieoczekiwane pliki:** Sprawdź, czy rozszerzenia plików zawierają początkową kropkę (`.txt`).  
- **Spowolnienie wydajności:** Połącz filtry za pomocą AND, aby zmniejszyć liczbę plików skanowanych na wczesnym etapie potoku indeksowania.  
- **Błędy wyrażeń regularnych:** Użyj znaków ucieczki dla specjalnych znaków w wzorcu ścieżki lub użyj `RegexOptions.IgnoreCase` dla dopasowań bez rozróżniania wielkości liter.

## Najczęściej zadawane pytania

**Q: Czy mogę połączyć filtr NOT z filtrem AND?**  
A: Tak. Najpierw zbuduj filtr NOT (`DocumentFilter.CreateNot`), a następnie użyj go jako jednego z argumentów w `DocumentFilter.CreateAnd`.

**Q: Jak filtrować pliki większe niż 10 MB?**  
A: Użyj `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)`, aby uwzględnić tylko pliki przekraczające ten rozmiar.

**Q: Czy można filtrować jednocześnie według daty utworzenia i modyfikacji?**  
A: Absolutnie. Utwórz każdy filtr osobno i połącz je za pomocą `CreateAnd`.

**Q: Czy te filtry działają ze ścieżkami w chmurze?**  
A: Filtry działają na lokalnym systemie plików. W przypadku źródeł w chmurze najpierw pobierz pliki do tymczasowego folderu, a następnie zastosuj te same filtry.

**Q: Czy zmiana filtru wymaga ponownego indeksowania?**  
A: Tak. Filtry są oceniane podczas wywoływania `index.Add`. Zmiana filtru oznacza konieczność przebudowy indeksu, aby odzwierciedlić nowe kryteria.

## Zakończenie

Opanowując **jak filtrować pliki** za pomocą GroupDocs.Redaction dla .NET — niezależnie od tego, czy chodzi o rozszerzenie, datę utworzenia, datę modyfikacji, rozmiar pliku czy logikę NOT — możesz usprawnić zarządzanie dokumentami, utrzymać wydajne indeksy i skupić się na treściach, które naprawdę mają znaczenie. Eksperymentuj z operatorami logicznymi, aby dostosować filtrowanie do swoich precyzyjnych reguł biznesowych, a zauważysz natychmiastowe korzyści w szybkości i efektywności przechowywania.

---

**Ostatnia aktualizacja:** 2026-04-21  
**Testowano z:** GroupDocs.Redaction 24.11 dla .NET  
**Autor:** GroupDocs  

---