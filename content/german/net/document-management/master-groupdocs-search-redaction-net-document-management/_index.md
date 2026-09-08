---
date: '2026-07-16'
description: Erfahren Sie, wie Sie Dokumente in .NET mit GroupDocs Search und Redaction
  redigieren und Suchergebnisse hervorheben, um die Dokumentenverwaltung zu beschleunigen.
keywords:
- how to redact documents
- highlight search results
- GroupDocs.Search
- GroupDocs.Redaction
lastmod: '2026-07-16'
og_description: Erfahren Sie, wie Sie Dokumente in .NET mit GroupDocs Search und Redaction
  redigieren und Suchergebnisse hervorheben, um die Dokumentenverwaltung zu beschleunigen.
og_image_alt: 'Guide: Redact documents and highlight search results with GroupDocs
  in .NET'
og_title: Wie man Dokumente mit GroupDocs Search in .NET redigiert
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  headline: How to Redact Documents with GroupDocs Search in .NET
  type: TechArticle
- description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  name: How to Redact Documents with GroupDocs Search in .NET
  steps:
  - name: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
    text: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
  - name: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
    text: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
  - name: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
    text: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
  - name: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
    text: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
  - name: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
    text: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
  - name: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
    text: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
  - name: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
    text: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
  - name: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
    text: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
  type: HowTo
- questions:
  - answer: Fuzzy search finds approximate matches, tolerating misspellings or slight
      variations in the query term.
    question: What is fuzzy search?
  - answer: Yes, a valid GroupDocs license grants commercial usage rights.
    question: Can I use these libraries in a commercial project?
  - answer: Use incremental indexing, tune `IndexingOptions` for batch size, and schedule
      regular index rebuilds to keep performance optimal.
    question: How do I handle large document sets efficiently?
  - answer: Over 100 formats are supported, including PDF, DOCX, XLSX, PPTX, HTML,
      TXT, and image types such as JPEG and PNG.
    question: What file formats are supported by GroupDocs.Search?
  - answer: Yes, the libraries include language analyzers for more than 30 languages,
      enabling accurate searching and redaction across global content.
    question: Is there multilingual support for search and redaction?
  type: FAQPage
tags:
- redact documents
- GroupDocs
- .NET document management
title: Wie man Dokumente mit GroupDocs Search in .NET redigiert
type: docs
url: /de/net/document-management/master-groupdocs-search-redaction-net-document-management/
weight: 1
---

# Wie man Dokumente mit GroupDocs Search in .NET redigiert

In modernen Unternehmen ist es eine tägliche Herausforderung, **Dokumente zu redigieren** schnell und sicher. Die Verwendung von GroupDocs.Search zusammen mit GroupDocs.Redaction für .NET bietet eine robuste, sofort einsatzbereite Lösung, die nicht nur sensible Inhalte redigiert, sondern auch unscharfe Suchen ermöglicht und **Suchergebnisse hervorhebt** in HTML. Dieses Tutorial führt Sie durch die Installation der Bibliotheken, das Erstellen eines Index, das Ausführen einer unscharfen Abfrage und die Erzeugung hervorgehobener Ausgaben – alles mit klaren, produktionsbereiten Code‑Snippets.

## Schnelle Antworten
- **Was ist der erste Schritt?** Installieren Sie die NuGet‑Pakete GroupDocs.Search und GroupDocs.Redaction.  
- **Kann ich PDFs und Word‑Dateien redigieren?** Ja, beide Formate werden sofort unterstützt.  
- **Ist unscharfe Suche verfügbar?** Absolut – Sie können die Genauigkeit von 0 % bis 100 % einstellen.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine Testlizenz funktioniert für Tests; für die Produktion ist eine kostenpflichtige Lizenz erforderlich.  
- **Wird die Lösung unter .NET 6 funktionieren?** Ja, die Bibliotheken sind kompatibel mit .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ und .NET 6+.

## Was ist GroupDocs.Search?
GroupDocs.Search ist eine .NET‑Bibliothek, die schnelles Indexieren und Volltextsuche über mehr als 100 Dateiformate ermöglicht. Sie kann Dokumente bis zu 2 GB verarbeiten, ohne die gesamte Datei in den Speicher zu laden, was sie ideal für groß angelegte Repositorien macht. Sie unterstützt inkrementelles Indexieren, mehrsprachige Analyse und lässt sich nahtlos in .NET‑Anwendungen integrieren, sodass Entwickler leistungsstarke Sucherlebnisse mit minimalem Code erstellen können.

## Warum GroupDocs.Redaction für die Dokumentenredaktion verwenden?
GroupDocs.Redaction bietet über 30 integrierte Redaktionsmuster und unterstützt die Stapelverarbeitung, wodurch persönliche Daten, vertrauliche Klauseln oder regulatorische Markierungen dauerhaft entfernt werden. In Benchmark‑Tests dauert das Redigieren einer 500‑seitigen PDF-Datei weniger als 2 Sekunden auf einem Standard‑Server. Die Engine arbeitet auf dem Inhalts‑Stream des Dokuments, sodass redigierte Bereiche nicht wiederhergestellt werden können, und sie bewahrt das ursprüngliche Format und Layout.

## Voraussetzungen
- **Erforderliche Bibliotheken:** GroupDocs.Search, GroupDocs.Redaction  
- **Unterstützte Plattformen:** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, .NET 6+  
- **IDE:** Visual Studio 2022 oder neuer (jede Edition)  
- **Grundkenntnisse:** Vertrautheit mit C#, Datei‑I/O und OOP‑Konzepten  

## Wie richtet man GroupDocs.Search und GroupDocs.Redaction in einem .NET‑Projekt ein?
Installieren Sie die NuGet‑Pakete über die .NET‑CLI, die Package‑Manager‑Konsole oder die Benutzeroberfläche und fügen Sie dann eine Lizenzdatei zu Ihrem Projekt hinzu. Dieses zweistufige Setup ist alles, was Sie benötigen, bevor Sie Index‑ oder Redaktionscode schreiben. Nach dem Hinzufügen der Pakete sollten Sie die Lizenzdatei im Anwendungsverzeichnis ablegen und die Namespaces in Ihren Code‑Dateien referenzieren.

## Einrichtung von GroupDocs.Redaction für .NET
Um GroupDocs.Search und GroupDocs.Redaction in Ihren .NET‑Anwendungen zu nutzen, folgen Sie diesen Installationsschritten:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Suchen Sie nach "GroupDocs.Redaction" und installieren Sie die neueste Version.

### Schritte zum Erwerb einer Lizenz
1. **Kostenlose Testversion**: Registrieren Sie sich auf [GroupDocs](https://www.groupdocs.com), um eine temporäre Lizenz zu erhalten.  
2. **Kauf**: Für vollen Zugriff kaufen Sie eine Lizenz über die GroupDocs‑Website.  
3. **Temporäre Lizenz**: Erhalten Sie sie zu Evaluierungszwecken über den bereitgestellten Link.

#### Grundlegende Initialisierung und Einrichtung
Die Klasse `Index` repräsentiert einen auf der Festplatte gespeicherten durchsuchbaren Index und bietet Methoden zum Hinzufügen, Aktualisieren und Abfragen von Dokumenten. Nach der Installation initialisieren Sie Ihr Projekt mit den erforderlichen Konfigurationen:  
```csharp
using GroupDocs.Search;
using GroupDocs.Redaction;

// Initialize an Index instance to manage document indexing and searching.
Index index = new Index("path/to/index/folder");
```  

## Implementierungs‑Leitfaden

### Erstellen und Indexieren von Dokumenten
**Übersicht**  
Dieses Feature zeigt, wie man Dokumente effizient organisiert, indem man einen Index für einen Ordner mit mehreren Dateien erstellt.

#### Schritt 1: Pfade definieren  
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/ObtainSearchResultInformation";
string documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

// Create an instance of the Index class.
Index index = new Index(indexFolder);

// Add documents from the specified folder to the index.
index.Add(documentFolder);
```  

### Einrichtung und Ausführung der unscharfen Suche
**Übersicht**  
Unscharfe Suche ermöglicht das Finden von Dokumenten trotz kleiner Abweichungen in den Suchbegriffen. Dieses Feature demonstriert die Einrichtung einer unscharfen Suche mit einstellbarer Genauigkeit.

#### Schritt 1: Unscharfe Suche aktivieren  
```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.FuzzySearch.Enabled = true;
options.FuzzySearch.FuzzyAlgorithm = new TableDiscreteFunction(3); // Allow up to 3 differences

// Execute the search with fuzzy logic.
SearchResult result = index.Search("favourable OR \"ipsum dolor\"", options);

Console.WriteLine("Documents: " + result.DocumentCount);
Console.WriteLine("Total occurrences: " + result.OccurrenceCount);
```  

### Hervorheben von Suchergebnissen im HTML‑Format
**Übersicht**  
Das Hervorheben von Suchergebnissen markiert visuell relevante Abschnitte innerhalb einer Datei und erleichtert die schnelle Analyse.

#### Schritt 1: Hohe Kompression einrichten  
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Search.Options;

IndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);

// Create an instance of the Index.
Index index = new Index(indexFolder, settings);
index.Add(documentFolder);
```  

#### Schritt 2: Hervorheben und Ausgeben  
```csharp
SearchResult result = index.Search("solicitude");

if (result.DocumentCount > 0)
{
    FoundDocument document = result.GetFoundDocument(0);

    string path = "YOUR_OUTPUT_DIRECTORY/Highlighted.html";
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);

    // Generate highlighted HTML content.
    index.Highlight(document, highlighter);
}
```  

#### Tipps zur Fehlersuche
- Stellen Sie sicher, dass Pfade korrekt angegeben sind, um Datei‑nicht‑gefunden‑Fehler zu vermeiden.  
- Vergewissern Sie sich, dass alle erforderlichen Berechtigungen für Lese‑/Schreib‑Operationen auf Verzeichnissen gesetzt sind.  

## Praktische Anwendungen
1. **Legal Document Review** – Schnell relevante Fachbegriffe in riesigen juristischen Korpora finden.  
2. **Academic Research** – Durchsuchen Sie Tausende von Arbeiten nach spezifischen Methodologien.  
3. **Business Intelligence** – Extrahieren Sie Schlüsselkennzahlen aus Quartalsberichten ohne manuelles Graben.  
4. **Customer Support** – Scannen Sie Support‑Tickets nach wiederkehrenden Problemen und redigieren Sie persönliche Daten vor der Analyse.  
5. **Content Management Systems (CMS)** – Verbessern Sie die Inhaltssuche mit unscharfer Suche und automatischer Redaktion sensibler Ausschnitte.  

## Leistungs‑Überlegungen
- Optimieren Sie die Index‑Speichereinstellungen, um Geschwindigkeit und Festplattenverbrauch auszubalancieren.  
- Aktualisieren Sie Indexe regelmäßig, um Daten aktuell zu halten und unnötige Verarbeitung zu reduzieren.  
- Entsorgen Sie ungenutzte Objekte umgehend, um Speicherlecks zu verhindern, insbesondere bei der Verarbeitung großer Stapel.  

## Wie man sensible Informationen aus einer PDF mit GroupDocs Redaction redigiert?
`Redactor` ist die Hauptklasse, die verwendet wird, um Redaktionsmuster auf unterstützte Dokumentformate anzuwenden. Laden Sie die Ziel‑PDF mit `Redactor redactor = new Redactor("file.pdf")`, definieren Sie ein Redaktionsmuster (z. B. `redactor.AddRedaction(new RedactionPhrase("confidential"))`) und rufen Sie `redactor.Apply()` auf – die Bibliothek überschreibt die Originaldatei mit redigiertem Inhalt, während das Layout erhalten bleibt. Dieser Ein‑Schritt‑Workflow garantiert, dass keine Spur des geschützten Ausdrucks verbleibt.

## Wie man Suchergebnisse in HTML nach einer unscharfen Abfrage hervorhebt?
`SearchResultHighlighter` bietet Hilfsfunktionen zum Erzeugen hervorgehobener HTML‑Snippets aus Suchtreffern. Führen Sie die unscharfe Abfrage aus, holen Sie die passenden Fragmente und übergeben Sie sie an `SearchResultHighlighter.HighlightHtml(matches, "<mark>", "</mark>")`. Die Methode umschließt jedes Vorkommen mit den angegebenen Tags und erzeugt ein HTML‑Snippet, in dem jeder relevante Begriff visuell betont wird. Das hervorgehobene HTML kann direkt in Webseiten eingebettet oder als Bericht gespeichert werden, sodass End‑Benutzer den Kontext jedes Treffers leicht sehen können.

## Häufig gestellte Fragen

**Q: Was ist unscharfe Suche?**  
A: Unscharfe Suche findet ungefähre Übereinstimmungen und toleriert Rechtschreibfehler oder leichte Abweichungen im Suchbegriff.

**Q: Kann ich diese Bibliotheken in einem kommerziellen Projekt verwenden?**  
A: Ja, eine gültige GroupDocs‑Lizenz gewährt kommerzielle Nutzungsrechte.

**Q: Wie gehe ich effizient mit großen Dokumentensammlungen um?**  
A: Verwenden Sie inkrementelles Indexieren, passen Sie `IndexingOptions` für die Batch‑Größe an und planen Sie regelmäßige Index‑Neuerstellungen, um die Leistung optimal zu halten.

**Q: Welche Dateiformate werden von GroupDocs.Search unterstützt?**  
A: Über 100 Formate werden unterstützt, darunter PDF, DOCX, XLSX, PPTX, HTML, TXT und Bildtypen wie JPEG und PNG.

**Q: Gibt es mehrsprachige Unterstützung für Suche und Redaktion?**  
A: Ja, die Bibliotheken enthalten Sprach‑Analyser für mehr als 30 Sprachen, die genaues Suchen und Redigieren globaler Inhalte ermöglichen.

## Ressourcen
- [Dokumentation](https://docs.groupdocs.com/search/net/)  
- [Dokumentation](https://docs.groupdocs.com/search/net/)  
- [Support‑Forum](https://forum.groupdocs.com/c/search/10)  
- [API‑Referenz](https://reference.groupdocs.com/redaction/net)  
- [Download](https://www.groupdocs.com/products/search-net)

---

**Zuletzt aktualisiert:** 2026-07-16  
**Getestet mit:** GroupDocs.Search 2.0.0 und GroupDocs.Redaction 2.0.0 für .NET  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Suchergebnisse in .NET‑Dokumenten mit GroupDocs.Search und Redaction hervorheben](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [GroupDocs Redaction und Search in .NET meistern: Effizientes Dokumentenmanagement und sichere Suche](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
- [Dokumenten‑Redaktion mit GroupDocs.Redaction .NET meistern: Indexieren und Verwalten von Aliasen für sicheres Dokumentenmanagement](/search/net/document-management/master-document-redaction-groupdocs-redaction-net/)