---
date: '2026-04-04'
description: Dowiedz się, jak przeszukiwać dokumenty prawne i zarządzać indeksami
  przy użyciu GroupDocs.Search oraz integrować redakcję rekordów medycznych z GroupDocs.Redaction
  w .NET.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: Wyszukuj dokumenty prawne za pomocą GroupDocs Search & Redaction dla .NET
type: docs
url: /pl/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Wyszukiwanie dokumentów prawnych przy użyciu GroupDocs Search & Redaction w .NET

W dzisiejszym środowisku opartym na danych, **wyszukiwanie dokumentów prawnych** szybko i bezpiecznie jest kluczowym wymaganiem dla każdej organizacji. Niezależnie od tego, czy obsługujesz umowy, dokumenty sądowe czy raporty zgodności, GroupDocs.Search zapewnia szybki, skalowalny indeks, podczas gdy GroupDocs.Redaction zapewnia, że wrażliwe informacje pozostają ukryte. Ten samouczek przeprowadzi Cię przez konfigurację indeksu wyszukiwalnego, dodawanie dokumentów z wielu folderów oraz konfigurowanie redakcji, abyś mógł bezpiecznie przeszukiwać rekordy medyczne i inne poufne pliki.

## Szybkie odpowiedzi
- **Do czego służy GroupDocs.Search?** Tworzy pełnotekstowy indeks wyszukiwalny dla szerokiego zakresu formatów dokumentów.  
- **Czy mogę zredagować informacje przed wyszukiwaniem?** Tak – użyj GroupDocs.Redaction, aby zamaskować lub usunąć wrażliwe dane.  
- **Jak dodać dokumenty do indeksu?** Wywołaj `index.Add("folderPath")` dla każdego folderu, który chcesz uwzględnić.  
- **Jakie typy plików są obsługiwane?** PDF, DOCX, PPTX, TXT i wiele innych.  
- **Czy potrzebuję licencji do produkcji?** Dostępna jest tymczasowa wersja próbna; stała licencja jest wymagana do użytku komercyjnego.

## Wymagania wstępne
Aby śledzić ten samouczek, upewnij się, że masz:
- .NET Core SDK (3.1 lub nowszy) zainstalowany.
- Visual Studio Code, Visual Studio lub inne IDE obsługujące .NET.
- Podstawową znajomość programowania w C#.

### Uzyskanie licencji
Możesz rozpocząć od darmowej wersji próbnej obu bibliotek. W przypadku dłuższego użytkowania rozważ uzyskanie tymczasowej licencji lub zakup jednej z [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

## Instalacja wymaganych pakietów

**Instalacja GroupDocs.Search:**  
Używając **.NET CLI**, uruchom:
```bash
dotnet add package GroupDocs.Search
```
Alternatywnie, użyj konsoli Package Manager w Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**Instalacja GroupDocs.Redaction:**  
- Użyj .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- Lub przez Package Manager:
```powershell
Install-Package GroupDocs.Redaction
```

Odwiedź interfejs NuGet Package Manager UI i wyszukaj "GroupDocs.Redaction", aby zainstalować go, jeśli wolisz interfejs graficzny.

## Konfiguracja ustawień Redaktora
Zanim rozpoczniesz redakcję, możesz chcieć dostosować zachowanie redaktora (np. ustawić kolor redakcji lub zdefiniować własne wzorce). Poniższy fragment pokazuje podstawową inicjalizację:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Pro tip:** Dostosuj `redactorSettings` do polityk zgodności Twojej organizacji (np. zamień tekst na czarne pola, zastosuj OCR przed redakcją itp.).

## Przewodnik implementacji

### Jak wyszukiwać dokumenty prawne?
Utworzenie indeksu wyszukiwalnego jest podstawą szybkiego odnajdywania dokumentów prawnych. GroupDocs.Search pozwala wskazać dowolny folder, zbudować indeks, a następnie wykonać złożone zapytania wśród tysięcy plików.

### Jak dodać dokumenty do indeksu
Dodawanie dokumentów jest proste — wystarczy skierować bibliotekę na katalogi zawierające Twoje pliki. Możesz dodać wiele folderów, co jest przydatne, gdy Twój korpus prawny jest rozproszony w różnych lokalizacjach.

#### Tworzenie i zarządzanie indeksem
**Przegląd:**  
Utworzenie indeksu jest pierwszym krokiem w kierunku efektywnych operacji wyszukiwania dokumentów. GroupDocs.Search pozwala utworzyć indeks wyszukiwalny w dowolnym wybranym katalogu, umożliwiając szybkie odnajdywanie dokumentów.

##### Krok 1: Utwórz indeks
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Wyjaśnienie:* `Index` inicjalizuje indeks wyszukiwania w określonym katalogu. Upewnij się, że ścieżka odzwierciedla strukturę folderów Twojego projektu.

##### Krok 2: Dodawanie dokumentów do indeksu
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Wyjaśnienie:* Metoda `Add` skanuje podany folder i dołącza każdy obsługiwany dokument do indeksu. Użyj jej, aby **dodać dokumenty do indeksu** z wielu źródeł, takich jak umowy, akta sprawy lub rekordy medyczne.

### Pobieranie i wyświetlanie raportów indeksowania
**Przegląd:**  
Raporty indeksowania dają wgląd w liczbę przetworzonych dokumentów, całkowitą liczbę terminów i rozmiar przechowywania — kluczowe metryki do optymalizacji wydajności.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*Wyjaśnienie:* `GetIndexingReports` zwraca tablicę raportów opisujących proces indeksowania, pomagając monitorować i optymalizować wydajność.

## Praktyczne zastosowania
1. **Zarządzanie dokumentami prawnymi:** Automatyzuj indeksowanie akt spraw, aby natychmiastowo odnajdywać ustawy, krótkie opracowania i wyroki.  
2. **System rekordów medycznych:** Przeszukuj rekordy pacjentów, zachowując prywatność, używając GroupDocs.Redaction do maskowania PHI.  
3. **Portal HR korporacji:** Połącz wyszukiwalne pliki pracowników z redakcją, aby chronić dane osobowe.

## Rozważania dotyczące wydajności
- **Optymalizacja rozmiaru indeksu:** Okresowo usuwać przestarzałe wpisy i przebudowywać indeks, aby był lekki.  
- **Zarządzanie pamięcią:** Wykorzystaj garbage collector .NET; zwalniaj obiekty `Index`, gdy nie są już potrzebne.  
- **Najlepsze praktyki skalowalności:** Przechowuj indeks na szybkim dysku SSD i rozważ podział dużych korpusów na wiele indeksów.

## Najczęściej zadawane pytania

**P: Jakie są główne zastosowania GroupDocs.Search?**  
A: Jest idealny do tworzenia indeksów wyszukiwalnych z dużych zbiorów dokumentów, umożliwiając szybkie odnajdywanie plików prawnych i medycznych.

**P: Jak GroupDocs.Redaction zapewnia prywatność danych?**  
A: Umożliwia definiowanie wzorców redakcji, które trwale usuwają lub maskują wrażliwe informacje przed indeksowaniem lub udostępnieniem dokumentu.

**P: Czy mogę używać tych bibliotek w środowisku chmurowym?**  
A: Tak — obie biblioteki działają w Azure, AWS lub dowolnym konteneryzowanym wdrożeniu .NET przy odpowiedniej licencji.

**P: Jakie formaty plików są obsługiwane przez GroupDocs.Search?**  
A: PDF, Word, Excel, PowerPoint, TXT, HTML i wiele innych formatów korporacyjnych.

**P: Jak rozwiązać problemy z błędami indeksowania?**  
A: Sprawdź ścieżki folderów, uprawnienia do plików oraz przejrzyj wyjście konsoli z `IndexingReport` pod kątem konkretnych kodów błędów.

## Zasoby
- **Dokumentacja:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **Referencja API:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Pobierz:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Bezpłatne wsparcie:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licencja tymczasowa:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Ostatnia aktualizacja:** 2026-04-04  
**Testowano z:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs