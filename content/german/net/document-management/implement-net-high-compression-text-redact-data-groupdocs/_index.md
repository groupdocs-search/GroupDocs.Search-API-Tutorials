---
date: '2026-06-07'
description: Erfahren Sie, wie Sie hochkomprimiertes .NET für die Textspeicherung
  implementieren und vertrauliche Daten mit GroupDocs.Search und GroupDocs.Redaction
  in .NET-Anwendungen redigieren.
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
title: 'Implementieren Sie hochkomprimiertes .NET mit GroupDocs: Leitfaden für Text
  & Redaktion'
type: docs
url: /de/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Implementierung von High Compression .NET mit GroupDocs: Text‑ und Redaktions‑Leitfaden

In modernen .NET‑Lösungen ist **implement high compression .net** unerlässlich, wenn Sie massive Textsammlungen speichern müssen, ohne den Festplattenspeicher zu sprengen. Gleichzeitig erfordert der Schutz sensibler Informationen – wie persönliche Kennungen oder Finanzdaten – eine zuverlässige Redaktion. Dieses Tutorial zeigt Ihnen Schritt für Schritt, wie Sie die hochkomprimierte Textspeicherung mit **GroupDocs.Search** konfigurieren und vertrauliche Daten sicher mit **GroupDocs.Redaction** redigieren. Am Ende können Sie indizierten Text um bis zu 90 % komprimieren und private Inhalte aus PDFs, Word‑Dateien und vielen anderen Formaten entfernen.

## Schnelle Antworten
- **Welche Bibliothek bietet hochkomprimierte Indizierung?** GroupDocs.Search für .NET.  
- **Welches Tool redigiert sensible Daten?** GroupDocs.Redaction für .NET.  
- **Kann ich Dokumente automatisch zum Index hinzufügen?** Ja – verwenden Sie die `AddDocument`‑API innerhalb einer Ordnerscan‑Schleife.  
- **Ist die Kompression verlustfrei für die Suche?** Ja, der Text bleibt nach der Kompression vollständig durchsuchbar.  
- **Benötige ich eine Lizenz für die Produktion?** Eine permanente GroupDocs‑Lizenz ist für die kommerzielle Nutzung erforderlich.

## Was bedeutet „implement high compression .net“?
Implement high compression .net bedeutet, die Indexierungs‑Engine von GroupDocs.Search so zu konfigurieren, dass extrahierte Textinhalte in komprimierter Form gespeichert werden. Dadurch wird die Größe des Indexes auf der Festplatte drastisch reduziert, während der Text vollständig durchsuchbar bleibt. Die Kompression ist verlustfrei, sodass die Relevanz von Abfragen und die Extraktion von Textauszügen genau wie bei einem unkomprimierten Index funktionieren.

## Warum GroupDocs für Kompression und Redaktion verwenden?
GroupDocs.Search unterstützt mehr als fünfzig Eingabeformate und kann indizierten Text um bis zu neunzig Prozent komprimieren, sodass große Dokumentensammlungen nur einen Bruchteil ihrer ursprünglichen Größe einnehmen. GroupDocs.Redaction ergänzt dies, indem es sensible Informationen in über dreißig Dateitypen dauerhaft löscht oder maskiert und Ihnen hilft, strenge Compliance‑Vorschriften wie GDPR und HIPAA ohne zusätzliche Werkzeuge zu erfüllen.

## Voraussetzungen
- **Entwicklungsumgebung:** Visual Studio 2022 oder neuer, .NET 6+ (oder .NET Framework 4.7.2).  
- **Bibliotheken:** NuGet‑Pakete `GroupDocs.Search` und `GroupDocs.Redaction`.  
- **Berechtigungen:** Lese‑/Schreibzugriff auf die Ordner, die Quelldokumente und den Zielort des Indexes enthalten.  
- **Grundkenntnisse:** C#‑Syntax, Datei‑I/O und Vertrautheit mit der .NET‑Projektstruktur.

## Wie implementiert man High Compression .NET mit GroupDocs?
Um High Compression .NET mit GroupDocs zu implementieren, erstellen Sie zunächst eine Instanz von `TextStorageSettings` und setzen deren `CompressionLevel` auf `High`. Anschließend instanziieren Sie ein `Index`‑Objekt, übergeben die Einstellungen und den Ordner, in dem der Index gespeichert werden soll. Nachdem der Index bereit ist, fügen Sie Dokumente mit `AddDocument` hinzu und führen schließlich Suchvorgänge mit der `Search`‑Methode aus, wobei die Engine die Kompression und Dekompression transparent handhabt.

### Schritt 1: Installieren der erforderlichen NuGet‑Pakete
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
- Suche nach „GroupDocs.Search“ und klicke **Install**.  

### Schritt 2: Installieren von GroupDocs.Redaction (für Datenredaktion)
- Öffnen Sie den **NuGet Package Manager**.  
- Suchen Sie nach **GroupDocs.Redaction** und installieren Sie die neueste stabile Version.  

### Schritt 3: Lizenz erhalten und anwenden
- **Kostenlose Testversion:** Registrieren Sie sich im GroupDocs‑Portal für einen 30‑Tage‑Testschlüssel.  
- **Temporäre Lizenz:** Fordern Sie einen temporären Schlüssel für Entwicklungsumgebungen an.  
- **Permanente Lizenz:** Kaufen Sie eine Produktionslizenz, um Evaluationsbeschränkungen zu entfernen.

### Schritt 4: Grundlegende Initialisierung beider Bibliotheken
Die `Search`‑ und `Redaction`‑Engines teilen ein gemeinsames Lizenzmodell. Initialisieren Sie sie beim Anwendungsstart:

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

## Feature 1: Einstellungen für hochkomprimierte Textspeicherung

### Konfiguration der Indexierung einrichten
`TextStorageSettings` ist die Klasse, die GroupDocs.Search mitteilt, wie der extrahierte Text gespeichert werden soll. Das Aktivieren hoher Kompression reduziert die Indexgröße um bis zu **10×**, ohne die Suchgeschwindigkeit zu beeinträchtigen.

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

**Erklärung:**  
- `CompressionLevel.High` aktiviert einen ZSTD‑basierten Algorithmus, der Textblöcke effizient komprimiert.  
- `UseMemoryCache = false` zwingt die Engine, Daten vom Datenträger zu streamen, was für groß angelegte Deployments ideal ist.

### Erstellen und Verwalten des Indexes
Das `Index`‑Objekt repräsentiert das durchsuchbare Repository auf dem Datenträger. Sie geben den Ordner an, in dem die Indexdateien gespeichert werden, und übergeben die oben definierten Kompressionseinstellungen.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Erklärung:**  
- `indexFolder` bestimmt, wo die komprimierten Indexdateien abgelegt werden.  
- `settings` fügt die Hochkompressions‑Konfiguration ein und stellt sicher, dass jedes hinzugefügte Dokument davon profitiert.

## Feature 2: Dokumente zum Index hinzufügen

### Dokumente zu Ihrem Index hinzufügen
`AddDocument` fügt eine einzelne Datei dem Index hinzu, extrahiert deren Text, komprimiert ihn gemäß den konfigurierten Einstellungen und speichert das Ergebnis. GroupDocs.Search kann Dateien aus einem Verzeichnisbaum einlesen. Die folgende Schleife durchläuft `documentsFolder`, fügt jede Datei hinzu und protokolliert den Fortschritt.

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

**Erklärung:**  
- `AddDocument` analysiert die Datei, extrahiert durchsuchbaren Text, komprimiert ihn gemäß `TextStorageSettings` und speichert ihn im Index.  
- Dieser Ansatz funktioniert für **PDF, DOCX, TXT, HTML** und mehr als **30** weitere Formate.

## Feature 3: Ausführen einer Suchabfrage

### Suche ausführen
`Search` führt eine Abfrage gegen den komprimierten Index aus und gibt eine Sammlung passender `DocumentResult`‑Objekte mit Relevanzwerten und hervorgehobenen Ausschnitten zurück. Sobald der Index gefüllt ist, können Sie schnelle Abfragen ausführen. Die `Search`‑Methode liefert eine Sammlung von `DocumentResult`‑Objekten, die Dateipfade und hervorgehobene Ausschnitte enthalten.

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

**Erklärung:**  
- Die Suchmaschine scannt den komprimierten Text direkt, sodass die Abfrageverzögerung selbst bei Indizes mit **Millionen von Seiten** niedrig bleibt.  
- `Score` gibt die Relevanz an; höhere Werte bedeuten ein besseres Ergebnis.

## Wie redigiert man vertrauliche Daten mit GroupDocs.Redaction?
Das Redigieren vertraulicher Daten mit GroupDocs.Redaction beginnt mit dem Erstellen einer `Redactor`‑Instanz für die Zieldatei. Definieren Sie ein oder mehrere `SearchPattern`‑Objekte, die den zu entfernenden Text beschreiben, z. B. reguläre Ausdrücke für Sozialversicherungsnummern. Wenden Sie jedes Muster mit `Redact` an, wobei Sie einen `RedactionType` wie `BlackOut` angeben, und speichern Sie das Ergebnis als neues Dokument, sodass das Original unverändert bleibt.

`Redactor` ist die Hauptklasse in GroupDocs.Redaction, die zum Laden eines Dokuments und zum Durchführen von Redaktions‑Operationen verwendet wird.  
`SearchPattern` definiert einen regulären Ausdruck, der den zu redigierenden Text identifiziert.

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

**Erklärung:**  
- `SearchPattern` verwendet einen regulären Ausdruck, um Sozialversicherungsnummern zu finden.  
- `RedactionType.BlackOut` ersetzt den gefundenen Text durch ein durchgängiges schwarzes Rechteck, sodass die Daten nicht wiederhergestellt werden können.

## Praktische Anwendungen
1. **Rechtsdokumenten‑Management:** Automatisches Komprimieren massiver Falldateien und Redigieren von Kundenkennungen vor der Archivierung.  
2. **Gesundheitsakten:** Jahre von Patientennotizen in einem komprimierten Index speichern und PHI (Protected Health Information) entfernen, bevor sie mit Forschungspartnern geteilt werden.  
3. **Finanzberichte:** Quartalsberichte sichern, indem Kontonummern redigiert werden, während der durchsuchbare Text für Prüfungsabfragen erhalten bleibt.

## Leistungsüberlegungen
- **Auswirkungen der Kompression:** Hohe Kompression reduziert die Indexgröße um bis zu **90 %**, was die SSD‑Abnutzung verringert und Sicherungs‑Vorgänge beschleunigt.  
- **Speichernutzung:** Deaktivieren Sie das In‑Memory‑Caching für sehr große Indizes, um den Prozess‑Footprint unter **500 MB** zu halten.  
- **I/O‑Optimierung:** Dokumente stapelweise in Gruppen von 100 hinzufügen, um Festplatten‑Thrashing zu minimieren.  
- **Asynchrone Verarbeitung:** Wickeln Sie `AddDocument`‑Aufrufe in `Task.Run` ein, um UI‑Threads in Desktop‑Apps reaktionsfähig zu halten.

## Häufige Fallstricke & Fehlersuche
- **Falsche Dateipfade:** Stellen Sie sicher, dass `documentsFolder` und `indexFolder` absolute Pfade sind und die Anwendung Lese‑/Schreibrechte hat.  
- **Lizenzfehler:** Stellen Sie sicher, dass die `.lic`‑Dateien zusammen mit der ausführbaren Datei bereitgestellt oder als Ressourcen eingebettet sind.  
- **Suche liefert keine Ergebnisse:** Prüfen Sie, ob das Kompressionslevel von `TextStorageSettings` dem während der Indexierung verwendeten entspricht; nicht übereinstimmende Einstellungen können Deserialisierungsfehler verursachen.

## Häufig gestellte Fragen

**Q: Kann ich nach dem initialen Aufbau Dokumente zum Index hinzufügen?**  
A: Ja – rufen Sie einfach `index.AddDocument` für neue Dateien auf; die Engine aktualisiert den komprimierten Index inkrementell.

**Q: Verändert die Redaktion die Originaldatei?**  
A: Nein – die Originaldatei bleibt unverändert; die redigierte Version wird als neue Datei gespeichert, wodurch die Dokumentenintegrität erhalten bleibt.

**Q: Welche Formate unterstützt GroupDocs.Redaction?**  
A: Über **30** Formate, darunter PDF, DOCX, PPTX, XLSX, Bilder (PNG, JPEG) und Klartext.

**Q: Wie wirkt sich hohe Kompression auf die Suchrelevanz aus?**  
A: Nicht. Die Kompression ist für Text verlustfrei, sodass die Relevanzwerte identisch mit einem unkomprimierten Index sind.

**Q: Gibt es ein Limit für die Größe der Dokumente, die ich indexieren kann?**  
A: GroupDocs.Search kann Multi‑Gigabyte‑Dateien durch Streaming verarbeiten; stellen Sie jedoch sicher, dass ausreichend Festplattenspeicher für den komprimierten Index vorhanden ist (etwa 10 % der Originalgröße).

## Ressourcen
- [Dokumentation](https://docs.groupdocs.com/search/net/)
- [API‑Referenz](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction für .NET](https://releases.groupdocs.com/search/net/)
- [Kostenloses Support‑Forum](https://forum.groupdocs.com/c/search/10)
- [Erwerb einer temporären Lizenz](https://purchase.groupdocs.com/temporary-license/)

---

**Zuletzt aktualisiert:** 2026-06-07  
**Getestet mit:** GroupDocs.Search 23.12 und GroupDocs.Redaction 23.12 für .NET  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Implementierung von GroupDocs.Search und Redaction in .NET für Dokumentenmanagement](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Wie man GroupDocs.Redaction für .NET optimiert: Leitfaden für effizientes Index‑ und Rechtschreib‑Management](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Meistern von GroupDocs Redaction und Search in .NET: Effizientes Dokumentenmanagement und sichere Suche](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)