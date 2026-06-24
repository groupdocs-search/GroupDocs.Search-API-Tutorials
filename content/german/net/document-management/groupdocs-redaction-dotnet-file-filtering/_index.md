---
date: '2026-04-21'
description: Erfahren Sie, wie Sie Dateien mit GroupDocs.Redaction für .NET filtern,
  einschließlich Filter nach Erstellungsdatum, Dateigröße, Änderungsdatum und wie
  Sie NOT‑Filter anwenden.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Wie man Dateien mit GroupDocs.Redaction für .NET filtert
type: docs
url: /de/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Wie man Dateien mit GroupDocs.Redaction für .NET filtert

In der heutigen schnelllebigen digitalen Umgebung kann **wie man Dateien filtert** effizient den Unterschied zwischen Produktivität und Frust ausmachen. Ob Sie Dokumente nach Erweiterung, Erstellungsdatum, Größe oder Änderungsdatum isolieren müssen, eine solide Filterstrategie spart Zeit, senkt Speicherkosten und hält Ihren Suchindex übersichtlich. In diesem Tutorial führen wir Sie durch praxisnahe Beispiele mit GroupDocs.Redaction für .NET und zeigen Ihnen genau, wie Sie Dateien filtern, um gängige Geschäftsanforderungen zu erfüllen.

## Schnelle Antworten
- **Welche Bibliothek benötige ich?** GroupDocs.Redaction für .NET (Installation über NuGet).  
- **Kann ich nach Erstellungsdatum filtern?** Ja – verwenden Sie `CreateCreationTimeRange`.  
- **Wie schließe ich bestimmte Typen aus?** Wenden Sie einen NOT-Filter mit `DocumentFilter.CreateNot` an.  
- **Wird das Filtern nach Dateigröße unterstützt?** Absolut, über `CreateFileLengthRange` oder obere/untere Grenzen.  
- **Benötige ich eine Lizenz?** Für den Produktionseinsatz ist eine Test- oder Volllizenz erforderlich.

## Was ist Dateifilterung mit GroupDocs.Redaction?
Dateifilterung ermöglicht es Ihnen, der Indexierungs-Engine mitzuteilen, welche Dokumente basierend auf Metadaten wie Erweiterung, Daten, Pfadmuster oder Größe einbezogen oder ignoriert werden sollen. Durch die Definition präziser `DocumentFilter`‑Regeln halten Sie Ihren Index schlank und Ihre Suchvorgänge schnell.

## Warum GroupDocs.Redaction für .NET verwenden?
- **Eingebaute Filterhilfen** – kein Bedarf, benutzerdefinierten Dateisystemcode zu schreiben.  
- **Logische Operatoren** – mehrere Kriterien mit AND, OR und NOT kombinieren.  
- **Leistungsoptimiert** – Filter werden während der Indexierung angewendet, nicht danach.  
- **Plattformübergreifend** – funktioniert mit .NET Framework, .NET Core und .NET 5/6+.

## Voraussetzungen
- .NET Framework 4.6+ oder .NET Core 3.1+ installiert.  
- Visual Studio oder Ihre bevorzugte C#‑IDE.  
- Grundkenntnisse in C#.

### Erforderliche Bibliotheken & Einrichtung
Installieren Sie das NuGet‑Paket mit Ihrer bevorzugten Methode:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Profi‑Tipp:** Nach der Installation fügen Sie Ihre Lizenzdatei dem Projektstamm hinzu und rufen `License.SetLicense("license-file-path")` auf, bevor Sie irgendein Redactor‑ oder Index‑Objekt erstellen.

## Einrichtung von GroupDocs.Redaction für .NET

Zuerst erstellen Sie eine `Redactor`‑Instanz, die auf das Dokument verweist, mit dem Sie arbeiten möchten:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Warum das wichtig ist:** Das Initialisieren des Redactors stellt sicher, dass die Bibliothek bereit ist, später im Workflow Filter und Redaktionsregeln anzuwenden.

## Wie man Dateien nach Erweiterung filtert

Das Filtern nach Dateierweiterung ist die gängigste Methode, um einen Dokumentensatz einzugrenzen. Im Folgenden behalten wir nur FB2-, EPUB- und TXT‑Dateien.

### Nach Dateierweiterung filtern

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

## Wie man einen NOT‑Filter anwendet, um unerwünschte Typen auszuschließen

Wenn Sie **einen NOT‑Filter** anwenden müssen – zum Beispiel HTML‑ und PDF‑Dateien ausschließen – verwenden Sie `CreateNot`.

### HTM-, HTML- und PDF‑Dateien ausschließen

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

## Wie man Dateien nach Erstellungsdatum filtert

Wenn Sie **nach Erstellungsdatum filtern** müssen, geben Sie ein Start‑ und End‑`DateTime` an.

### Nach Erstellungsdatumsbereich filtern

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

## Wie man Dateien nach Änderungsdatum filtert

Ähnlich wie bei Erstellungsdaten können Sie die Ergebnisse auf Dateien beschränken, die vor einem bestimmten Zeitpunkt geändert wurden.

### Nach Änderungsdatum filtern

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

## Wie man Dateien nach Pfad mit regulären Ausdrücken filtert

Wenn Ihre Ordnerstruktur Namenskonventionen folgt, kann ein Regex bestimmte Pfade anvisieren.

### Nach Dateipfad‑Muster filtern

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

## Wie man Dateien nach Größe filtert

Die Kontrolle der Dokumentgröße ist entscheidend, wenn es um Bandbreiten- oder Speichergrenzen geht.

### Nach Dateigröße filtern (50 KB – 100 KB)

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

## Wie man mehrere Bedingungen mit AND kombiniert

Wenn Sie **wie man Dateien filtert** mit mehreren Kriterien gleichzeitig benötigen, kombinieren Sie sie mit `CreateAnd`.

### Beispiel für logisches AND

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

## Wie man mehrere Bedingungen mit OR kombiniert

Verwenden Sie `CreateOr`, wenn eine von mehreren Regeln erfüllt sein soll.

### Beispiel für logisches OR

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

## Häufige Probleme und Lösungen
- **Filter nicht angewendet:** Stellen Sie sicher, dass Sie `settings.DocumentFilter` **vor** dem Erstellen der `Index`‑Instanz zuweisen.  
- **Unerwartete Dateien erscheinen:** Überprüfen Sie, ob die Dateierweiterungen den führenden Punkt (`.txt`) enthalten.  
- **Leistungsverlust:** Kombinieren Sie Filter mit AND, um die Anzahl der früh im Indexierungspipeline gescannten Dateien zu reduzieren.  
- **Regex‑Fehler:** Escape‑Zeichen für Sonderzeichen in Ihrem Pfadmuster oder verwenden Sie `RegexOptions.IgnoreCase` für case‑insensitive Vergleiche.

## Häufig gestellte Fragen

**Q: Kann ich einen NOT‑Filter mit einem AND‑Filter kombinieren?**  
A: Ja. Erstellen Sie zuerst den NOT‑Filter (`DocumentFilter.CreateNot`) und fügen Sie ihn dann als eines der Argumente zu `DocumentFilter.CreateAnd` hinzu.

**Q: Wie filtere ich Dateien, die größer als 10 MB sind?**  
A: Verwenden Sie `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)`, um nur Dateien einzuschließen, die diese Größe überschreiten.

**Q: Ist es möglich, gleichzeitig nach Erstellungs- und Änderungsdaten zu filtern?**  
A: Absolut. Erstellen Sie jeden Filter separat und kombinieren Sie sie mit `CreateAnd`.

**Q: Funktionieren diese Filter mit Cloud‑Speicherpfaden?**  
A: Die Filter arbeiten auf dem lokalen Dateisystem. Für Cloud‑Quellen laden Sie die Dateien zunächst in einen temporären Ordner herunter und wenden dann dieselben Filter an.

**Q: Erfordert das Ändern des Filters eine Neu‑Indexierung?**  
A: Ja. Filter werden ausgewertet, wenn Sie `index.Add` aufrufen. Das Ändern eines Filters bedeutet, dass Sie den Index neu erstellen müssen, um die neuen Kriterien zu berücksichtigen.

## Fazit

Durch das Beherrschen von **wie man Dateien filtert** mit GroupDocs.Redaction für .NET – sei es nach Erweiterung, Erstellungsdatum, Änderungsdatum, Dateigröße oder mit NOT‑Logik – können Sie das Dokumentenmanagement optimieren, Indexe leistungsfähig halten und sich auf den wirklich wichtigen Inhalt konzentrieren. Experimentieren Sie mit den logischen Operatoren, um die Filterung exakt an Ihre Geschäftsregeln anzupassen, und Sie werden sofortige Verbesserungen in Geschwindigkeit und Speichereffizienz feststellen.

---

**Zuletzt aktualisiert:** 2026-04-21  
**Getestet mit:** GroupDocs.Redaction 24.11 for .NET  
**Autor:** GroupDocs  

---