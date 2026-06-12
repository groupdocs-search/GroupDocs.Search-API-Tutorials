---
date: '2026-06-12'
description: Erfahren Sie, wie Sie Dokumente in .NET mit GroupDocs.Search und GroupDocs.Redaction
  suchen und redigieren, die Suchleistung optimieren und Indexierungsfehler behandeln.
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Wie man Dokumente in .NET mit GroupDocs.Search und GroupDocs.Redaction sucht
  und redigiert
type: docs
url: /de/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# Dokumente in .NET mit GroupDocs.Search & GroupDocs.Redaction suchen und redigieren

In modernen Unternehmensumgebungen sind **search and redact**‑Funktionen unerlässlich, um sensible Informationen zu schützen und gleichzeitig Dokumente leicht auffindbar zu halten. Dieses Tutorial führt Sie durch den Aufbau einer robusten .NET‑Lösung, die GroupDocs.Search für schnelle Volltextsuche mit GroupDocs.Redaction kombiniert, um vertrauliche Daten sicher zu entfernen. Am Ende wissen Sie, wie Sie die Bibliotheken einrichten, einen benutzerdefinierten Textsegmentierer erstellen, Hochleistungssuchen ausführen und Redaktionen sicher anwenden.

## Schnelle Antworten
- **Was bedeutet „search and redact“?** Es bedeutet, Text in Dokumenten zu finden und dauerhaft zu maskieren.  
- **Welche Bibliotheken werden benötigt?** GroupDocs.Search und GroupDocs.Redaction für .NET.  
- **Kann ich mehrsprachige Inhalte verarbeiten?** Ja – verwenden Sie einen benutzerdefinierten Textsegmentierer, um Wörter korrekt zu teilen.  
- **Wie verbessere ich die Suchgeschwindigkeit?** Index einmal erstellen, den Index wiederverwenden und die Einstellung `optimize search performance` aktivieren.  
- **Was ist, wenn die Indizierung fehlschlägt?** Befolgen Sie die Richtlinien „handle indexing errors“ im Abschnitt zur Fehlerbehebung.  

## Was ist „search and redact“?

Search and redact ist der Prozess, bei dem spezifische Begriffe in einer Dokumentensammlung gefunden und dann dauerhaft verdeckt oder entfernt werden, um die Privatsphäre zu schützen oder regulatorische Vorgaben zu erfüllen. Es kombiniert Volltextsuche, um sensible Informationen zu finden, mit Redaktionswerkzeugen, die den Inhalt ersetzen und dabei das ursprüngliche Layout des Dokuments beibehalten.

## Warum GroupDocs.Search und GroupDocs.Redaction zusammen verwenden?

GroupDocs.Search unterstützt **mehr als 50 Dateiformate** und kann **über 100.000 Dokumente** in weniger als einer Minute auf typischer Serverhardware indizieren, während GroupDocs.Redaction Redaktionen auf **PDF, DOCX, PPTX und mehr** anwenden kann, ohne das ursprüngliche Layout zu verändern. Die Kombination bietet Ihnen eine einheitliche Lösung, die **die Suchleistung optimiert** und **Indexierungsfehler** elegant handhabt.

## Voraussetzungen

- Visual Studio 2022 oder neuer mit .NET 6+ Unterstützung.  
- NuGet‑Pakete: **GroupDocs.Search** und **GroupDocs.Redaction** (neueste stabile Versionen).  
- Eine gültige GroupDocs‑Lizenz (Testversion oder gekauft).  

### Erforderliche Bibliotheken
- **GroupDocs.Search** – Bietet Indizierung, Abfragen und benutzerdefinierte Segmentierung.  
- **GroupDocs.Redaction** – Bietet Text-, Bild‑ und Metadaten‑Redaktion für unterstützte Formate.

### Anforderungen an die Umgebungseinrichtung
Stellen Sie sicher, dass Ihr Entwicklungsrechner Schreibberechtigungen für den Ordner hat, in dem der Index gespeichert wird.

### Wissensvoraussetzungen
- Vertrautheit mit C# und .NET‑Projektstrukturen.  
- Grundlegendes Verständnis von Dokumentenverarbeitungs‑Konzepten (optional, aber hilfreich).

## Wie installiere ich GroupDocs.Redaction für .NET?

Sie können das Redaction‑Paket zu Ihrem Projekt hinzufügen, entweder über die .NET‑CLI oder den NuGet‑Paket‑Manager. Der Befehl lädt die neueste stabile Version herunter und registriert sie in Ihrer Projektdatei, sodass die API sofort verfügbar ist.  

```bash
dotnet add package GroupDocs.Redaction
```  

## Wie erhalte ich eine Lizenz für GroupDocs?

GroupDocs bietet drei Lizenzierungsoptionen: eine kostenlose Testversion zur Evaluierung, eine temporäre Lizenz für erweiterte Entwicklungstests und eine vollständige kommerzielle Lizenz für den Produktionseinsatz. Die Testversion bietet eingeschränkte Funktionalität, während der temporäre Schlüssel den Evaluierungszeitraum verlängert und die gekaufte Lizenz alle Funktionen sowie Prioritäts‑Support freischaltet.

## Wie initialisiere ich GroupDocs.Redaction in meiner Anwendung?

Die Klasse `Redaction` ist der primäre Einstiegspunkt zum Anwenden von Redaktionen auf unterstützte Dokumente. Sie lädt eine Datei, bereitet Redaktionsobjekte vor und führt den Redaktionsprozess aus, wobei ein modifiziertes Dokument zurückgegeben wird, das das ursprüngliche Layout beibehält. Sie können außerdem Redaktionsoptionen wie Farbe, Overlay und Metadaten‑Entfernung konfigurieren, um spezifische Compliance‑Anforderungen zu erfüllen.  

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## Wie richte ich einen Index mit GroupDocs.Search ein?

Die Klasse `Index` stellt ein durchsuchbares Repository dar, das auf der Festplatte gespeichert ist. Sie verwaltet das Erstellen, Aktualisieren und Abfragen des Index, sodass Sie Dokumente hinzufügen, den Index neu aufbauen und schnelle Suchen über große Sammlungen ausführen können. Der Indexordner kann auf lokalem oder Netzwerk‑Speicher liegen, und Sie können Komprimierungs‑ und Verschlüsselungseinstellungen konfigurieren, um die indizierten Daten zu schützen.  

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## Was ist ein benutzerdefinierter Textsegmentierer und warum sollte ich ihn verwenden?

Ein benutzerdefinierter Textsegmentierer bestimmt, wie Rohtext in durchsuchbare Token aufgeteilt wird. Durch Anpassen der Segmentierungsregeln für bestimmte Sprachen oder Domänen verbessern Sie die Tokenisierungsgenauigkeit, was zu höherer Trefferquote und Relevanz in den Suchergebnissen führt. Dies ist besonders nützlich für Sprachen mit komplexen Wortgrenzen, wie Japanisch oder Arabisch, bei denen Standard‑Tokenizer Wörter fehlerhaft aufteilen können.  

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## Wie führe ich eine Volltextsuche mit dem benutzerdefinierten Segmentierer durch?

Das Objekt `SearchQuery` fasst die Benutzeranfrage zusammen und arbeitet mit dem benutzerdefinierten Segmentierer, um Treffer zu finden. Es unterstützt unscharfe Übereinstimmungen, Phrasenabfragen und Gewichtungen und gibt ein Ergebnis‑Set mit Dokument‑IDs, Trefferpositionen und Relevanzwerten zurück. Sie können außerdem Filter wie Dateityp oder Datumsbereich anwenden, um die Ergebnisse für eine präzisere Zielsetzung einzugrenzen.  

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## Wie wende ich Redaktionen an, nachdem sensibler Text gefunden wurde?

Die `Redaction`‑API ermöglicht das Ersetzen oder Entfernen von Text, Bildern und Metadaten in unterstützten Dokumenten. Nachdem Sie sensible Begriffe identifiziert haben, erstellen Sie Redaktionsobjekte, wenden sie an und speichern die redigierte Datei, sodass vertrauliche Informationen dauerhaft verborgen bleiben. Redaktionsoptionen umfassen das Überlagern mit schwarzen Kästchen, das Anwenden benutzerdefinierter Farben oder das Entfernen ganzer Objekte bei gleichzeitiger Beibehaltung der Dokumentstruktur.  

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## Häufige Probleme und wie Indexierungsfehler zu behandeln sind

- **Index Not Found:** Überprüfen Sie, ob der Indexpfad existiert und die Anwendung Lese‑/Schreibrechte hat.  
- **Search Returns No Results:** Führen Sie den Indexierungsprozess erneut aus und stellen Sie sicher, dass der benutzerdefinierte Segmentierer korrekt registriert ist.  
- **Redaction Fails on Certain Formats:** Stellen Sie sicher, dass der Dateityp unterstützt wird; für PDFs verwenden Sie die neueste Redaction‑Version, um PDF 2.0‑Funktionen zu handhaben.  

## Praktische Anwendungen

1. **Rechtsdokumentenverwaltung:** Durchsuchen Sie Verträge nach „non‑disclosure“ und redigieren Sie Klauseln automatisch, bevor sie extern geteilt werden.  
2. **Akademische Forschung:** Finden Sie unveröffentlichte Daten in Manuskripten und verbergen Sie sie für Peer‑Review‑Prozesse.  
3. **Geschäftsverträge:** Verarbeiten Sie Tausende von Vereinbarungen im Batch‑Verfahren, indem Sie persönliche Kennungen redigieren und gleichzeitig die rechtliche Sprache beibehalten.  

## Wie kann ich die Suchleistung für große Dokumentensammlungen optimieren?

Um die Leistung zu maximieren, indizieren Sie Dokumente einmal und verwenden denselben Index für nachfolgende Abfragen wieder. Aktivieren Sie die Parallelverarbeitung, konfigurieren Sie Caching und optimieren Sie die Indexeinstellungen, um Latenz zu reduzieren und den Durchsatz auf Mehrkern‑Servern zu erhöhen. Zusätzlich setzen Sie das Flag `EnableMemoryMapping`, um den Index speicher‑gemappt zu ermöglichen, was Lesevorgänge für große Datensätze beschleunigt.

## Wie verwalte ich .NET‑Speicher beim Arbeiten mit großen Dateien?

Effizientes Speichermanagement ist entscheidend beim Umgang mit großen Dokumenten. Verpacken Sie `Index`‑ und `Redaction`‑Objekte in `using`‑Anweisungen, um eine deterministische Entsorgung sicherzustellen, und verarbeiten Sie Dateien als Streams, anstatt ganze Dokumente in den Speicher zu laden. Das Überwachen von Leistungs‑Counters hilft, Speicher‑Spikes frühzeitig zu erkennen, sodass Sie Batch‑Größen anpassen oder das Garbage‑Collection‑Tuning aktivieren können.

## Häufig gestellte Fragen

**Q: Kann ich GroupDocs.Search mit nicht‑textuellen Metadaten verwenden?**  
A: Ja – Metadatenfelder können zusammen mit dem Dokumentinhalt indiziert werden, wodurch Suchanfragen wie „author:JohnDoe“ möglich sind.

**Q: Unterstützt GroupDocs.Redaction Echtzeit‑Redaktion in einer Web‑API?**  
A: Ja; Sie können die Redaction‑API synchron für kleine Dateien aufrufen oder größere Aufträge für die asynchrone Verarbeitung in eine Warteschlange stellen.

**Q: Was soll ich tun, wenn der Index beschädigt wird?**  
A: Löschen Sie den beschädigten Indexordner und bauen Sie ihn mit derselben Indexierungsroutine neu auf; die Bibliothek protokolliert detaillierte Fehlermeldungen, um Ihnen zu helfen, die Ursache zu ermitteln.

**Q: Ist es möglich, redigierte Dokumente vor dem Speichern vorzusehen?**  
A: Absolut – rufen Sie `redaction.Apply()` mit dem `preview`‑Flag auf, um eine temporäre Version zur Überprüfung zu erzeugen.

**Q: Welche .NET‑Versionen werden offiziell unterstützt?**  
A: GroupDocs.Search und GroupDocs.Redaction unterstützen .NET 6, .NET 5, .NET Core 3.1 und .NET Framework 4.6.2+.

## Ressourcen

- **Dokumentation:** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API‑Referenz:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Download:** [GroupDocs Releases](https://releases.groupdocs.com/search/net/)
- **Kostenloser Support:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporäre Lizenz:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Zuletzt aktualisiert:** 2026-06-12  
**Getestet mit:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**Autor:** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## Verwandte Tutorials

- [Meistern von GroupDocs Search und Redaction in .NET: Fortgeschrittenes Dokumentenmanagement](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
- [Implementierung von GroupDocs.Search & Redaction: Aktualisieren und Verwalten von Dokumenten‑Indizes in .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [Optimieren der Dokumentenindizierung in .NET mit GroupDocs.Redaction: Abbruch, Async und Threads](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)