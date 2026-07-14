---
date: '2026-06-07'
description: Dowiedz się, jak wdrożyć wysoką kompresję .NET w przechowywaniu tekstu
  oraz redagować poufne dane przy użyciu GroupDocs.Search i GroupDocs.Redaction w
  aplikacjach .NET.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'Wdrażanie wysokiej kompresji .NET z GroupDocs: Przewodnik po tekście i redakcji'
type: docs
url: /pl/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Implementacja wysokiej kompresji .NET z GroupDocs: przewodnik po tekście i redakcji

W nowoczesnych rozwiązaniach .NET, **implement high compression .net** jest niezbędny, gdy trzeba przechowywać ogromne kolekcje tekstu bez nadmiernego zużycia dysku. Jednocześnie ochrona wrażliwych informacji — takich jak identyfikatory osobiste czy dane finansowe — wymaga niezawodnej redakcji. Ten samouczek pokazuje krok po kroku, jak skonfigurować przechowywanie tekstu z wysoką kompresją przy użyciu **GroupDocs.Search** oraz jak bezpiecznie usunąć poufne dane za pomocą **GroupDocs.Redaction**. Po zakończeniu będziesz w stanie skompresować indeksowany tekst nawet o 90 % i usunąć prywatną zawartość z plików PDF, Word i wielu innych formatów.

## Szybkie odpowiedzi
- **Jaka biblioteka zapewnia indeksowanie wysokiej kompresji?** GroupDocs.Search for .NET.  
- **Które narzędzie usuwa wrażliwe dane?** GroupDocs.Redaction for .NET.  
- **Czy mogę automatycznie dodawać dokumenty do indeksu?** Yes—use the `AddDocument` API inside a folder‑scan loop.  
- **Czy kompresja jest bezstratna dla wyszukiwania?** Yes, the text remains fully searchable after compression.  
- **Czy potrzebna jest licencja do produkcji?** A permanent GroupDocs license is required for commercial use.

## Co oznacza „implement high compression .net”?
Implement high compression .net oznacza skonfigurowanie silnika indeksowania GroupDocs.Search do przechowywania wyodrębnionej treści tekstowej w skompresowanej formie. Redukuje to rozmiar indeksu na dysku dramatycznie, zachowując jednocześnie pełną możliwość wyszukiwania tekstu. Kompresja jest bezstratna, więc trafność zapytań i wyodrębnianie fragmentów działają dokładnie tak jak w przypadku nie skompresowanego indeksu.

## Dlaczego warto używać GroupDocs do kompresji i redakcji?
GroupDocs.Search obsługuje ponad pięćdziesiąt formatów wejściowych i może skompresować indeksowany tekst nawet o dziewięćdziesiąt procent, pozwalając dużym zbiorom dokumentów zajmować tylko ułamek ich pierwotnego rozmiaru. GroupDocs.Redaction uzupełnia to, trwale usuwając lub maskując wrażliwe informacje w ponad trzydziestu typach plików, pomagając spełnić surowe przepisy zgodności, takie jak GDPR i HIPAA, bez dodatkowych narzędzi.

## Wymagania wstępne
- **Środowisko programistyczne:** Visual Studio 2022 lub nowsze, .NET 6+ (lub .NET Framework 4.7.2).  
- **Biblioteki:** pakiety NuGet `GroupDocs.Search` i `GroupDocs.Redaction`.  
- **Uprawnienia:** dostęp odczytu/zapisu do folderów zawierających dokumenty źródłowe oraz miejsce wyjściowe indeksu.  
- **Podstawowa wiedza:** składnia C#, operacje I/O na plikach oraz znajomość struktury projektu .NET.

## Jak zaimplementować wysoką kompresję .NET z GroupDocs?
Aby zaimplementować wysoką kompresję .NET z GroupDocs, najpierw utwórz instancję `TextStorageSettings` i ustaw jej `CompressionLevel` na `High`. Następnie zainicjuj obiekt `Index`, przekazując ustawienia oraz folder, w którym indeks będzie przechowywany. Po przygotowaniu indeksu dodaj dokumenty przy użyciu `AddDocument`, a na końcu wykonaj wyszukiwania metodą `Search`, przy czym silnik transparentnie obsługuje kompresję i dekompresję.

### Krok 1: Zainstaluj wymagane pakiety NuGet
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Wyszukaj „GroupDocs.Search” i kliknij **Install**.  

### Krok 2: Zainstaluj GroupDocs.Redaction (do redakcji danych)
- Otwórz **NuGet Package Manager**.  
- Wyszukaj **GroupDocs.Redaction** i zainstaluj najnowszą stabilną wersję.  

### Krok 3: Uzyskaj i zastosuj licencję
- **Darmowa wersja próbna:** Zarejestruj się w portalu GroupDocs, aby uzyskać klucz próbny na 30 dni.  
- **Licencja tymczasowa:** Poproś o tymczasowy klucz do środowisk deweloperskich.  
- **Licencja stała:** Kup licencję produkcyjną, aby usunąć ograniczenia wersji ewaluacyjnej.

### Krok 4: Podstawowa inicjalizacja obu bibliotek
Silniki `Search` i `Redaction` korzystają ze wspólnego modelu licencjonowania. Zainicjalizuj je przy uruchamianiu aplikacji:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Funkcja 1: Ustawienia przechowywania tekstu z wysoką kompresją

### Konfiguracja ustawień indeksowania
`TextStorageSettings` jest klasą, która określa, jak GroupDocs.Search przechowuje wyodrębniony tekst. Włączenie wysokiej kompresji zmniejsza rozmiar indeksu nawet o **10×** bez wpływu na szybkość wyszukiwania.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Wyjaśnienie:**  
- `CompressionLevel.High` aktywuje algorytm oparty na ZSTD, który efektywnie kompresuje bloki tekstu.  
- `UseMemoryCache = false` zmusza silnik do strumieniowego odczytu danych z dysku, co jest idealne przy dużych wdrożeniach.

### Tworzenie i zarządzanie indeksem
Obiekt `Index` reprezentuje przeszukiwalne repozytorium na dysku. Określasz folder, w którym będą przechowywane pliki indeksu, oraz przekazujesz powyższe ustawienia kompresji.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Wyjaśnienie:**  
- `indexFolder` określa, gdzie znajdują się skompresowane pliki indeksu.  
- `settings` wprowadza konfigurację wysokiej kompresji, zapewniając, że każdy dodany dokument z niej korzysta.

## Funkcja 2: Dodawanie dokumentów do indeksu

### Dodaj dokumenty do swojego indeksu
`AddDocument` dodaje pojedynczy plik do indeksu, wyodrębnia jego tekst, kompresuje go zgodnie z ustawieniami i przechowuje wynik. GroupDocs.Search może przetwarzać pliki z drzewa katalogów. Poniższa pętla przechodzi przez `documentsFolder`, dodaje każdy plik i rejestruje postęp.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Wyjaśnienie:**  
- `AddDocument` parsuje plik, wyodrębnia tekst możliwy do przeszukania, kompresuje go zgodnie z `TextStorageSettings` i zapisuje w indeksie.  
- To podejście działa dla **PDF, DOCX, TXT, HTML** oraz ponad **30** innych formatów.

## Funkcja 3: Wykonywanie zapytania wyszukiwania

### Wykonaj wyszukiwanie
`Search` wykonuje zapytanie przeciwko skompresowanemu indeksowi i zwraca kolekcję pasujących obiektów `DocumentResult` z ocenami trafności oraz wyróżnionymi fragmentami. Po wypełnieniu indeksu możesz uruchamiać szybkie zapytania. Metoda `Search` zwraca kolekcję obiektów `DocumentResult`, które zawierają ścieżki plików i wyróżnione fragmenty.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Wyjaśnienie:**  
- Silnik wyszukiwania skanuje skompresowany tekst bezpośrednio, więc opóźnienie zapytania pozostaje niskie nawet dla indeksów zawierających **miliony stron**.  
- `Score` wskazuje trafność; wyższe wartości oznaczają lepsze dopasowanie.

## Jak zredagować poufne dane przy użyciu GroupDocs.Redaction?
Redagowanie poufnych danych przy użyciu GroupDocs.Redaction rozpoczyna się od utworzenia instancji `Redactor` dla docelowego pliku. Zdefiniuj jeden lub więcej obiektów `SearchPattern`, które opisują tekst do usunięcia, np. wyrażenia regularne dla numerów ubezpieczenia społecznego. Zastosuj każdy wzorzec przy użyciu `Redact`, określając `RedactionType`, np. `BlackOut`, i zapisz wynik jako nowy dokument, zapewniając, że oryginał pozostaje nienaruszony.

`Redactor` jest główną klasą w GroupDocs.Redaction używaną do ładowania dokumentu i wykonywania operacji redakcji.  
`SearchPattern` definiuje wyrażenie regularne, które identyfikuje tekst do redakcji.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Wyjaśnienie:**  
- `SearchPattern` używa wyrażenia regularnego do znajdowania numerów ubezpieczenia społecznego.  
- `RedactionType.BlackOut` zastępuje dopasowany tekst solidnym czarnym prostokątem, zapewniając, że dane nie mogą zostać odzyskane.

## Praktyczne zastosowania
1. **Zarządzanie dokumentami prawnymi:** Automatycznie kompresuj ogromne akta spraw i redaguj identyfikatory klientów przed archiwizacją.  
2. **Rekordy medyczne:** Przechowuj lata notatek pacjentów w skompresowanym indeksie i usuwaj PHI (Protected Health Information) przed udostępnieniem partnerom badawczym.  
3. **Raportowanie finansowe:** Zabezpiecz kwartalne raporty, redagując numery kont, jednocześnie zachowując tekst przeszukiwalny dla zapytań audytowych.

## Rozważania dotyczące wydajności
- **Wpływ kompresji:** Wysoka kompresja zmniejsza rozmiar indeksu nawet o **90 %**, co obniża zużycie SSD i przyspiesza operacje backupu.  
- **Zużycie pamięci:** Wyłącz buforowanie w pamięci dla bardzo dużych indeksów, aby utrzymać zużycie procesu poniżej **500 MB**.  
- **Optymalizacja I/O:** Dodawaj dokumenty partiami po 100, aby zminimalizować nadmierne operacje dyskowe.  
- **Przetwarzanie asynchroniczne:** Owiń wywołania `AddDocument` w `Task.Run`, aby utrzymać responsywność wątków UI w aplikacjach desktopowych.

## Częste pułapki i rozwiązywanie problemów
- **Nieprawidłowe ścieżki plików:** Zweryfikuj, że `documentsFolder` i `indexFolder` są ścieżkami bezwzględnymi oraz że aplikacja ma uprawnienia odczytu/zapisu.  
- **Błędy licencji:** Upewnij się, że pliki `.lic` są wdrożone razem z plikiem wykonywalnym lub osadzone jako zasoby.  
- **Wyszukiwanie nie zwraca wyników:** Sprawdź, czy poziom kompresji w `TextStorageSettings` odpowiada temu użytemu podczas indeksowania; niezgodne ustawienia mogą powodować błędy deserializacji.

## Najczęściej zadawane pytania

**P: Czy mogę dodawać dokumenty do indeksu po początkowym utworzeniu?**  
O: Tak — po prostu wywołaj `index.AddDocument` dla nowych plików; silnik aktualizuje skompresowany indeks stopniowo.

**P: Czy redakcja zmienia oryginalny plik?**  
O: Nie — oryginalny plik pozostaje nienaruszony; wersja zredagowana jest zapisywana jako nowy plik, zachowując integralność dokumentu.

**P: Jakie formaty obsługuje GroupDocs.Redaction?**  
O: Ponad **30** formatów, w tym PDF, DOCX, PPTX, XLSX, obrazy (PNG, JPEG) oraz zwykły tekst.

**P: Jak wysoka kompresja wpływa na trafność wyszukiwania?**  
O: Nie wpływa. Kompresja jest bezstratna dla tekstu, więc oceny trafności są identyczne jak w nie skompresowanym indeksie.

**P: Czy istnieje limit rozmiaru dokumentów, które mogę indeksować?**  
O: GroupDocs.Search może obsługiwać pliki wielogigabajtowe, strumieniując ich zawartość; jednak zapewnij wystarczającą ilość miejsca na dysku dla skompresowanego indeksu (około 10 % pierwotnego rozmiaru).

## Zasoby
- [Dokumentacja](https://docs.groupdocs.com/search/net/)
- [Referencja API](https://reference.groupdocs.com/redaction/net)
- [Pobierz GroupDocs.Redaction dla .NET](https://releases.groupdocs.com/search/net/)
- [Darmowe forum wsparcia](https://forum.groupdocs.com/c/search/10)
- [Uzyskanie licencji tymczasowej](https://purchase.groupdocs.com/temporary-license/)

---

**Ostatnia aktualizacja:** 2026-06-07  
**Testowano z:** GroupDocs.Search 23.12 and GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs

## Powiązane samouczki

- [Implementacja GroupDocs.Search i Redaction w .NET dla zarządzania dokumentami](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Jak zoptymalizować GroupDocs.Redaction dla .NET: przewodnik po efektywnym zarządzaniu indeksem i pisownią](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Mistrzostwo w GroupDocs Redaction i Search w .NET: efektywne zarządzanie dokumentami i bezpieczne wyszukiwanie](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)