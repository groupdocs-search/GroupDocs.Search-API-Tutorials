---
date: '2026-04-02'
description: Erfahren Sie, wie Sie nach Dateierweiterung filtern und nur txt‑Dateien
  mit GroupDocs.Redaction für .NET durchsuchen – steigern Sie die Effizienz der Dokumentenverwaltung.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Filtern nach Dateierweiterung in .NET mit GroupDocs.Redaction
type: docs
url: /de/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Filter nach Dateierweiterung in .NET mit GroupDocs.Redaction

Das Durchsuchen einer riesigen Dateisammlung kann überwältigend wirken, besonders wenn Sie nur Ergebnisse aus bestimmten Dateitypen benötigen. In diesem Tutorial erfahren Sie **wie man nach Dateierweiterung filtert** mit GroupDocs.Redaction für .NET, sodass Sie nur txt‑Dateien oder jede andere von Ihnen gewählte Erweiterung durchsuchen können. Wir zeigen, wie sowohl dateityp‑ als auch pfadbasierten Filter eingerichtet werden, damit Sie die gewünschten Dokumente schnell finden.

## Schnelle Antworten
- **Was bewirkt „filter by file extension“?** Es begrenzt eine Suche auf Dokumente, die einer angegebenen Dateierweiterung entsprechen (z. B. *.txt).  
- **Warum GroupDocs.Redaction dafür verwenden?** Es bietet integrierte Filter‑APIs, die schnell und einfach zu integrieren sind.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion reicht für Tests; für den Produktionseinsatz ist eine kostenpflichtige Lizenz erforderlich.  
- **Welche .NET‑Versionen werden unterstützt?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Kann ich Dateityp‑ und Pfad‑Filter kombinieren?** Ja – mehrere Filter können angewendet werden für hochpräzise Suchen.

## Was Sie lernen werden
- Wie man **nach Dateierweiterung filtert**, sodass nur Textdateien durchsucht werden.  
- Wie man **Dateipfad‑Filter** einrichtet, um Ergebnisse auf bestimmte Ordner oder Namensmuster zu beschränken.  
- Tipps, um Ihren Index schnell und speichereffizient zu halten.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie:

- **GroupDocs.Redaction Bibliothek** installiert und kompatibel mit Ihrem .NET‑Projekt.  
- Eine Entwicklungsumgebung wie Visual Studio oder VS Code.  
- Grundkenntnisse in C# und Vertrautheit mit der .NET‑Projektstruktur.

## Einrichtung von GroupDocs.Redaction für .NET

Zuerst fügen Sie die Bibliothek zu Ihrem Projekt hinzu.

**Using .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Using Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

Oder suchen Sie “GroupDocs.Redaction” im NuGet Package Manager UI und installieren Sie die neueste Version.

### Lizenzbeschaffung

Sie können mit einer kostenlosen Testversion starten oder eine temporäre Lizenz anfordern. Für langfristige Projekte kaufen Sie eine Lizenz auf der offiziellen Website.

### Grundlegende Initialisierung

Nachdem das Paket installiert ist, erstellen Sie einen Index, der Referenzen zu Ihren Dokumenten hält:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Implementierungs‑Leitfaden

### Feature 1: Einen Filter für Textdokumente (.txt) festlegen

#### Wie man nach Dateierweiterung für Textdokumente filtert

1. **Definieren Sie den Index und die Dokumentenordner**  
   Legen Sie die Pfade fest, in denen Ihre Quelldateien liegen:

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Erstellen Sie einen Index**  
   Laden Sie alle Dateien aus dem Quellordner in den Index:

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Konfigurieren Sie die Suchoptionen mit einem Dateierweiterungs‑Filter**  
   Teilen Sie der Engine mit, nur *.txt‑Dateien zu berücksichtigen:

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Führen Sie die Suche aus**  
   Starten Sie eine Abfrage; der Filter sorgt dafür, dass Nicht‑Textdateien ignoriert werden:

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Erklärung*: Die Methode `Search` gibt Treffer zurück, die den Filter erfüllen, wodurch Rauschen stark reduziert und die Leistung verbessert wird.

### Feature 2: Dateipfad‑Filter

#### Warum Dateipfad‑Filter verwenden?

Manchmal müssen Sie Suchen auf einen bestimmten Abteilungsordner oder eine Gruppe von Dateien mit gemeinsamer Namenskonvention beschränken. Pfad‑Filter ermöglichen genau das.

1. **Definieren Sie den Index und die Dokumentenordner**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Erstellen Sie einen Index**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Konfigurieren Sie die Suchoptionen mit einem pfadbasierten regulären Ausdruck**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Dieser reguläre Ausdruck trifft auf jede Datei zu, deren voller Pfad das Wort “Lorem” enthält, sodass Sie gezielt bestimmte Unterordner ansteuern können.

4. **Führen Sie die pfadbasierten Suche aus**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Praktische Anwendungen
- **Rechtsdokumenten‑Management** – Schnell relevante Verträge finden, die als Klartextdateien gespeichert sind.  
- **Akademische Forschung** – Nur *.txt‑Forschungsnotizen abrufen, die zu einem bestimmten Projektordner gehören.  
- **Unternehmensberichte** – Interne Berichte nach Abteilungs‑Pfad filtern (z. B. `/Finance/2025/`).  

## Leistungs‑Überlegungen
- Indexieren Sie nur die Dokumenttypen, die Sie tatsächlich benötigen; unnötige Dateien erhöhen die Indexgröße und Suchzeit.  
- Halten Sie Ihren Index mit einem geplanten Job, der `index.Add()` für neue oder geänderte Dateien aufruft, aktuell.  
- Verwenden Sie einfache reguläre Ausdrücke; zu komplexe Muster können die Suchmaschine verlangsamen.  
- Entsorgen Sie `Index`‑Objekte, wenn sie nicht mehr benötigt werden, um Speicher freizugeben.

## Fazit
Sie wissen jetzt, wie man **nach Dateierweiterung filtert** und **Dateipfad‑Filter** mit GroupDocs.Redaction für .NET anwendet. Diese Techniken geben Ihnen feinkörnige Kontrolle über große Dokumentensammlungen, wodurch Suchen schneller und relevanter werden. Als Nächstes experimentieren Sie mit der Kombination mehrerer Filter oder integrieren die Suche in einen größeren Anwendungs‑Workflow.

## FAQ‑Abschnitt

**Q1: Kann ich Dokumente filtern, die keine Textdateien sind?**  
A1: Ja, GroupDocs.Redaction unterstützt viele Formate. Ändern Sie das Argument in `CreateFileExtension` auf die gewünschte Erweiterung (z. B. ".pdf").

**Q2: Wie aktualisiere ich meinen Suchindex regelmäßig?**  
A2: Planen Sie einen Hintergrunddienst oder einen Cron‑Job, der `index.Add()` in den Verzeichnissen ausführt, die Sie aktuell halten möchten.

**Q3: Gibt es Leistungseinbußen beim Filtern nach Dateipfad?**  
A3: Optimierte reguläre Ausdrücke haben nur minimale Auswirkungen, aber testen Sie stets mit Ihrem eigenen Datensatz.

**Q4: Kann ich mehrere Filter kombinieren für verfeinerte Suchen?**  
A4: Absolut. Sie können Filter verketten oder zusammengesetzte Filter erstellen, um sowohl Dateityp als auch Pfad gleichzeitig zu berücksichtigen.

**Q5: Wo finde ich weitere Ressourcen zu GroupDocs.Redaction?**  
A5: Besuchen Sie die offizielle Dokumentation unter [GroupDocs Dokumentation](https://docs.groupdocs.com/search/net/) für ausführliche Anleitungen und API‑Referenzen.

## Häufig gestellte Fragen

**Q: Funktioniert der `SearchDocumentFilter` mit verschlüsselten Dateien?**  
A: Der Filter arbeitet auf Dateimetadaten, sodass verschlüsselte Dateien weiterhin indexiert werden, sofern Sie während des Indexierens die erforderlichen Entschlüsselungs‑Credentials bereitstellen.

**Q: Kann ich Platzhalter anstelle eines regulären Ausdrucks für die Pfad‑Filterung verwenden?**  
A: Die API erfordert derzeit einen regulären Ausdruck, aber Sie können einfache Platzhalter simulieren (z. B. `.*` für beliebige Zeichen).

**Q: Wie groß darf der Index werden, bevor ich über Sharding nachdenken muss?**  
A: Indizes von mehreren hundert Gigabyte können von einer Aufteilung in mehrere logische Indizes profitieren; testen Sie die Leistung, wenn Ihre Sammlung wächst.

**Q: Gibt es integrierte Methoden, um Dokumente aus dem Index zu entfernen?**  
A: Ja – rufen Sie `index.Delete(documentId)` oder `index.DeleteAll()` auf, um veraltete Einträge zu verwalten.

**Q: Gibt es eine Möglichkeit, Suchergebnisse vorzusehen, bevor das gesamte Dokument geladen wird?**  
A: Das `SearchResult`‑Objekt enthält Snippet‑Informationen, die Sie in der UI anzeigen können, ohne die gesamte Datei zu öffnen.

## Ressourcen
- **Dokumentation**: [GroupDocs Dokumentation](https://docs.groupdocs.com/search/net/)
- **API‑Referenz**: [GroupDocs API Referenz](https://reference.groupdocs.com/redaction/net)
- **Download**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **Kostenloser Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporäre Lizenz**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Letzte Aktualisierung:** 2026-04-02  
**Getestet mit:** GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs