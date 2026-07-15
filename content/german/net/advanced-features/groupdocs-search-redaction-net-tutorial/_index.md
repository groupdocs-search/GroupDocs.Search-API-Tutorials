---
date: '2026-04-04'
description: Erfahren Sie, wie Sie juristische Dokumente durchsuchen und Indizes mit
  GroupDocs.Search verwalten und die Redaktion von medizinischen Aufzeichnungen mit
  GroupDocs.Redaction in .NET integrieren.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: Durchsuchen Sie Rechtsdokumente mit GroupDocs Search & Redaction für .NET
type: docs
url: /de/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Durchsuchen von Rechtsdokumenten mit GroupDocs Search & Redaction in .NET

In der heutigen datengetriebenen Umgebung ist **das Durchsuchen von Rechtsdokumenten** schnell und sicher eine kritische Anforderung für jede Organisation. Egal, ob Sie Verträge, Gerichtsunterlagen oder Compliance‑Berichte bearbeiten, GroupDocs.Search liefert Ihnen einen schnellen, skalierbaren Index, während GroupDocs.Redaction dafür sorgt, dass sensible Informationen verborgen bleiben. Dieses Tutorial führt Sie durch das Einrichten eines durchsuchbaren Index, das Hinzufügen von Dokumenten aus mehreren Ordnern und die Konfiguration der Redaktion, sodass Sie medizinische Aufzeichnungen und andere vertrauliche Dateien sicher durchsuchen können.

## Schnelle Antworten
- **Was macht GroupDocs.Search?** Es erstellt einen volltextdurchsuchbaren Index für eine Vielzahl von Dokumentformaten.  
- **Kann ich Informationen vor dem Suchen redigieren?** Ja – verwenden Sie GroupDocs.Redaction, um sensible Daten zu maskieren oder zu entfernen.  
- **Wie füge ich Dokumente zum Index hinzu?** Rufen Sie `index.Add("folderPath")` für jeden Ordner auf, den Sie einbeziehen möchten.  
- **Welche Dateitypen werden unterstützt?** PDFs, DOCX, PPTX, TXT und viele mehr.  
- **Benötige ich eine Lizenz für die Produktion?** Eine temporäre Testversion ist verfügbar; für die kommerzielle Nutzung ist eine permanente Lizenz erforderlich.

## Voraussetzungen
- .NET Core SDK (3.1 oder höher) installiert.
- Visual Studio Code, Visual Studio oder eine andere IDE, die .NET unterstützt.
- Grundlegende Kenntnisse in C#‑Programmierung.

### Lizenzbeschaffung
Sie können mit einer kostenlosen Testversion beider Bibliotheken beginnen. Für eine erweiterte Nutzung sollten Sie eine temporäre Lizenz erwerben oder eine Lizenz über die [GroupDocs-Website](https://purchase.groupdocs.com/temporary-license/) kaufen.

## Installation der erforderlichen Pakete

**GroupDocs.Search Installation:**  
Using **.NET CLI**, run:
```bash
dotnet add package GroupDocs.Search
```
Alternatively, use the Package Manager Console in Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**GroupDocs.Redaction Installation:**  
- Use .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- Or, through Package Manager:
```powershell
Install-Package GroupDocs.Redaction
```

Visit the NuGet Package Manager UI and search for "GroupDocs.Redaction" to install it if you prefer a GUI.

## Redakteur‑Einstellungen konfigurieren
Before you start redacting, you may want to tweak the redactor behavior (e.g., set the redaction color or define custom patterns). The following snippet shows the basic initialization:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Pro tip:** Adjust `redactorSettings` to match your organization’s compliance policies (e.g., replace text with black boxes, apply OCR before redaction, etc.).

## Implementierungsleitfaden

### Wie durchsucht man Rechtsdokumente?
Creating a searchable index is the foundation for fast retrieval of legal documents. GroupDocs.Search lets you point to any folder, build an index, and then execute complex queries across thousands of files.

### Wie fügt man Dokumente zum Index hinzu
Adding documents is straightforward—simply point the library at the directories that hold your files. You can add multiple folders, which is handy when your legal corpus is spread across different locations.

#### Erstellen und Verwalten eines Index
**Overview:**  
Creating an index is the first step toward efficient document search operations. GroupDocs.Search allows you to create a searchable index in any directory of your choice, enabling quick retrieval of documents.

##### Schritt 1: Index erstellen
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Erklärung:* `Index` initialisiert einen Suchindex im angegebenen Verzeichnis. Stellen Sie sicher, dass der Pfad die Ordnerstruktur Ihres Projekts widerspiegelt.

##### Schritt 2: Dokumente zum Index hinzufügen
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Erklärung:* Die `Add`‑Methode scannt den angegebenen Ordner und fügt jedes unterstützte Dokument dem Index hinzu. Verwenden Sie dies, um **Dokumente zum Index** aus mehreren Quellen hinzuzufügen, z. B. Verträge, Akten oder medizinische Aufzeichnungen.

### Abrufen und Anzeigen von Indexierungsberichten
**Overview:**  
Indexing reports give you insight into how many documents were processed, total term count, and storage size—essential metrics for performance tuning.

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
*Erklärung:* `GetIndexingReports` gibt ein Array von Berichten zurück, die den Indexierungsprozess detailliert beschreiben, und hilft Ihnen, die Leistung zu überwachen und zu optimieren.

## Praktische Anwendungen
1. **Legal Document Management:** Automatisieren Sie die Indexierung von Akten, um sofort auf Gesetze, Schriftsätze und Urteile zugreifen zu können.  
2. **Medical Records System:** Durchsuchen Sie Patientendaten und wahren Sie dabei die Privatsphäre, indem Sie GroupDocs.Redaction verwenden, um PHI zu maskieren.  
3. **Corporate HR Portal:** Kombinieren Sie durchsuchbare Mitarbeiterdateien mit Redaktion, um persönliche Daten zu schützen.

## Leistungsüberlegungen
- **Optimizing Index Size:** Periodisch veraltete Einträge entfernen und den Index neu aufbauen, um ihn schlank zu halten.  
- **Memory Management:** Nutzen Sie den Garbage Collector von .NET; entsorgen Sie `Index`‑Objekte, wenn sie nicht mehr benötigt werden.  
- **Scalability Best Practices:** Speichern Sie den Index auf schnellem SSD‑Speicher und erwägen Sie das Sharding großer Korpora über mehrere Indexe hinweg.

## Häufig gestellte Fragen

**Q: What are the primary uses of GroupDocs.Search?**  
A: Es ist ideal zum Erstellen durchsuchbarer Indexe aus großen Dokumentensammlungen, wodurch ein schneller Zugriff auf Rechts‑ und Medizin‑Dateien ermöglicht wird.

**Q: How does GroupDocs.Redaction ensure data privacy?**  
A: Es erlaubt Ihnen, Redaktionsmuster zu definieren, die sensible Informationen dauerhaft entfernen oder maskieren, bevor das Dokument indexiert oder weitergegeben wird.

**Q: Can I use these libraries in a cloud environment?**  
A: Ja – beide Bibliotheken funktionieren in Azure, AWS oder jeder containerisierten .NET‑Bereitstellung mit entsprechender Lizenzierung.

**Q: What file formats are supported by GroupDocs.Search?**  
A: PDFs, Word, Excel, PowerPoint, TXT, HTML und viele weitere Unternehmensformate.

**Q: How do I troubleshoot indexing errors?**  
A: Überprüfen Sie Ordnerpfade, Dateiberechtigungen und prüfen Sie die Konsolenausgabe von `IndexingReport` auf spezifische Fehlercodes.

## Ressourcen
- **Dokumentation:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **API Reference:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Download:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Free Support:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Zuletzt aktualisiert:** 2026-04-04  
**Getestet mit:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs