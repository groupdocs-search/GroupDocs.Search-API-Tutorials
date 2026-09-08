---
date: '2026-07-26'
description: Erfahren Sie, wie Sie einen Index in .NET mit GroupDocs.Search erstellen
  und die Redaktion mit GroupDocs.Redaction integrieren, um eine schnelle Dokumentensuche
  und Datenverarbeitung zu ermöglichen.
keywords:
- how to create index
- how to add documents
- how to delete document
- search index .net
lastmod: '2026-07-26'
og_description: Erfahren Sie, wie Sie einen Index in .NET mit GroupDocs.Search erstellen
  und die Redaktion mit GroupDocs.Redaction integrieren, um eine schnelle Dokumentensuche
  und Datenverarbeitung zu ermöglichen.
og_image_alt: Guide showing GroupDocs Search index creation and Redaction integration
  in .NET
og_title: Wie man einen Index in .NET mit der GroupDocs Search API erstellt
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  headline: How to Create Index in .NET with GroupDocs Search API
  type: TechArticle
- description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  name: How to Create Index in .NET with GroupDocs Search API
  steps:
  - name: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
    text: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
  - name: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
    text: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
  - name: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
    text: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
  - name: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
    text: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
  - name: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
    text: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search can index over 150 formats—including PDFs, DOCX,
      PPTX, XLSX, and image types—by extracting embedded text via OCR where necessary.
    question: Can I index non‑text files with GroupDocs?
  - answer: Use `AddFolder` with a configurable batch size, run indexing in a background
      service, and periodically call `Optimize()` to merge small index segments.
    question: How do I handle large volumes of documents?
  - answer: Redaction removes personally identifiable information before it ever reaches
      the index, guaranteeing that search results never expose protected data.
    question: What are the benefits of using redaction with indexing?
  - answer: GroupDocs.Search provides synonym dictionaries, custom tokenizers, and
      regular‑expression filters, allowing you to fine‑tune relevance scoring.
    question: Is it possible to customize search algorithms?
  - answer: Verify folder permissions, ensure the .NET runtime matches the library’s
      target, and check the log file generated in the index folder for detailed error
      messages.
    question: How do I troubleshoot common indexing issues?
  type: FAQPage
tags:
- index management
- GroupDocs.Search
- GroupDocs.Redaction
- C# document indexing
- document redaction .NET
title: Wie man einen Index in .NET mit der GroupDocs Search API erstellt
type: docs
url: /de/net/document-management/master-net-index-management-groupdocs-search-redaction/
weight: 1
---

# Wie man einen Index in .NET mit der GroupDocs Search API erstellt

In diesem Tutorial erfahren Sie **how to create index** für Ihre .NET‑Anwendungen mit GroupDocs.Search und schützen anschließend sensible Inhalte mit GroupDocs.Redaction. Am Ende des Leitfadens können Sie einen durchsuchbaren Index erstellen, aktualisieren und bereinigen und verstehen, warum die Kombination von Suche und Redaktion eine bewährte Praxis für sicheres Dokumentenmanagement ist.

## Schnelle Antworten
- **What does “how to create index” mean?** Es bedeutet, eine durchsuchbare Datenstruktur zu erstellen, die Dokumentinhalte auf schnelle Suchschlüssel abbildet.  
- **Which libraries are required?** GroupDocs.Search und GroupDocs.Redaction für .NET (NuGet‑Pakete).  
- **Can I index PDFs, Word, and images?** Ja – über 150 Formate werden standardmäßig unterstützt.  
- **How do I delete a document from the index?** Rufen Sie die `Delete`‑Methode mit dem Pfad oder der ID des Dokuments auf.  
- **Is redaction performed before or after indexing?** Die Redaktion sollte zuerst erfolgen, damit geschützte Daten niemals in den Index gelangen.

## Was bedeutet “how to create index”?
Der Ausdruck **how to create index** bezieht sich auf den Prozess, eine durchsuchbare Datenstruktur zu erzeugen, die Begriff‑zu‑Dokument‑Zuordnungen für schnelle Abrufe speichert. In GroupDocs befindet sich diese Struktur auf der Festplatte und kann inkrementell aktualisiert werden, ohne die gesamte Sammlung neu aufzubauen.

## Warum GroupDocs.Search und GroupDocs.Redaction zusammen verwenden?
GroupDocs.Search unterstützt die Indizierung von **150+ Dateiformaten** und kann Indizes größer als **10 GB** verarbeiten, während der Speicherverbrauch unter 200 MB bleibt, da Dateien gestreamt statt vollständig geladen werden. Durch die Hinzufügung von GroupDocs.Redaction wird sichergestellt, dass vertrauliche Texte, Bilder oder Metadaten entfernt werden, bevor der Inhalt jemals den Index erreicht, was die Einhaltung von GDPR, HIPAA und anderen Vorschriften garantiert.

## Voraussetzungen

- **Libraries & Versions** – Installieren Sie die neuesten **GroupDocs.Search**‑ und **GroupDocs.Redaction**‑NuGet‑Pakete, die mit .NET 6 oder höher kompatibel sind.  
- **IDE** – Visual Studio 2022 (oder jede IDE, die .NET 6 unterstützt).  
- **Knowledge** – Grundlegende C#‑Kenntnisse, Vertrautheit mit Datei‑I/O und ein Verständnis von Indexierungskonzepten.

## Einrichtung von GroupDocs.Redaction für .NET

### Installation

**Verwendung der .NET‑CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Verwendung der Package‑Manager‑Konsole in Visual Studio:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Sie können auch “GroupDocs.Redaction” im NuGet‑Package‑Manager‑UI finden und die neueste stabile Version installieren.

### Lizenzbeschaffung

Sie können eine kostenlose Testversion erhalten oder eine temporäre Lizenz anfordern, um alle Funktionen uneingeschränkt zu testen. Besuchen Sie die [GroupDocs Kaufseite](https://purchase.groupdocs.com/temporary-license/) für weitere Details zur Lizenzbeschaffung.

### Grundlegende Initialisierung

Redactor ist die Hauptklasse, die Redaktionsvorgänge an einem Dokument durchführt.  
Das folgende Snippet zeigt den minimalen Code, der erforderlich ist, um GroupDocs.Redaction zu verwenden:  
```csharp
// Initialize the Redactor with a file path or stream
using (Redactor redactor = new Redactor("input.docx"))
{
    // Your redaction code here
}
```  

Dieses einfache Setup ist alles, was Sie benötigen, um mit GroupDocs.Redaction zu beginnen.

## Implementierungsleitfaden

### Wie erstellt man einen Index?

`Index` stellt den durchsuchbaren Container dar, der Begriffsdictionaries und Dokumenten‑Metadaten enthält.  
Laden oder erstellen Sie ein `Index`‑Objekt, verweisen Sie auf einen Ordner, in dem die Indexdateien gespeichert werden, und rufen Sie `Create` auf. Der Vorgang schreibt die erforderlichen Metadatendateien und bereitet die Engine für die Dokumentaufnahme vor.  
```text
// Direct answer (40‑70 words):
Create a new `Index` instance by specifying the folder path where the index will reside, then invoke `Create()` to initialise the storage structures. The method writes index headers, term dictionaries, and a lock file, making the folder ready for document addition. This step is required only once per index location.
```

#### Schritt 1: Index erstellen
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/DeleteIndexedPaths";
Index index = new Index(indexFolder);
// This line initializes an index at the provided folder path.
```  

### Wie fügt man Dokumente dem Index hinzu?

`Add` fügt ein einzelnes Dokument dem Index hinzu, während `AddFolder` alle Dateien in einem Verzeichnis verarbeitet.  
Sie fügen Dateien hinzu, indem Sie `Add` oder `AddFolder` aufrufen. Die Engine liest jede unterstützte Datei, extrahiert den Text und aktualisiert das Begriffsdictionary.  
```text
// Direct answer (40‑70 words):
Use `index.AddFolder("C:\\Docs")` or `index.Add("C:\\Docs\\file.pdf")` to feed documents into the index. The API streams each file, extracts searchable text, and stores term‑frequency data without loading the entire file into memory, which lets you index thousands of large PDFs efficiently.
```

#### Schritt 2: Dokumentordner hinzufügen
```csharp
string documentsFolder1 = @"YOUR_DOCUMENT_DIRECTORY";
string documentsFolder2 = @"YOUR_DOCUMENT_DIRECTORY2";

index.Add(documentsFolder1);  // Adding the first folder of documents to the index
index.Add(documentsFolder2);  // Adding the second folder of documents to the index
```  

### Wie ruft man indizierte Pfade ab?

`GetIndexedPaths` gibt eine Sammlung aller Dokumentpfade zurück, die im Index gespeichert sind.  
Das Abrufen der Liste der indizierten Dateipfade ermöglicht es Ihnen zu überprüfen, welche Dokumente derzeit durchsuchbar sind.  
```text
// Direct answer (40‑70 words):
Call `index.GetIndexedDocuments()` to obtain a collection of `IndexedDocumentInfo` objects, each containing the original file path, document ID, and indexing timestamp. Loop through the collection and output the `FilePath` property to confirm that every expected file has been successfully added.
```

#### Schritt 3: Indizierte Pfade anzeigen
```csharp
string[] indexedPaths1 = index.GetIndexedPaths();
foreach (string path in indexedPaths1)
{
    Console.WriteLine(path); // Outputs the document paths
}
```  

### Wie löscht man ein Dokument aus dem Index?

`Delete` entfernt ein Dokument aus dem Index anhand seines Pfads oder seiner Kennung.  
Wenn eine Datei entfernt oder veraltet ist, sollten Sie ihren Eintrag löschen, um die Genauigkeit der Suchergebnisse zu gewährleisten.  
```text
// Direct answer (40‑70 words):
Invoke `index.Delete("C:\\Docs\\obsolete.pdf")` or `index.Delete(documentId)` to purge a specific document from the index. The method removes all term entries linked to that file, updates the term dictionary, and frees the space on disk, ensuring that future queries no longer return the deleted content.
```

#### Schritt 4: Bestimmte Pfade löschen
```csharp
using GroupDocs.Search.Options;

string[] pathsToDelete = { @"YOUR_DOCUMENT_DIRECTORY" };
DeleteResult deleteResult = index.Delete(pathsToDelete, new UpdateOptions());
// This deletes specified document paths from the index.
```  

### Wie prüft man die verbleibenden indizierten Pfade nach dem Löschen?

Nach dem Entfernen können Sie die Abrufmethode erneut ausführen, um sicherzustellen, dass der Index den aktuellen Zustand widerspiegelt.  
```text
// Direct answer (40‑70 words):
Run `index.GetIndexedDocuments()` again and compare the resulting list with the pre‑deletion list. The missing file path confirms successful deletion, while the remaining entries confirm the index’s integrity. This verification step is especially important in automated pipelines.
```

#### Schritt 5: Verbleibende Pfade überprüfen
```csharp
string[] indexedPaths2 = index.GetIndexedPaths();
foreach (string path in indexedPaths2)
{
    Console.WriteLine(path); // Displays remaining paths after deletion
}
```  

## Praktische Anwendungen

1. **Document Management Systems** – Verträge, Rechnungen oder Handbücher schnell in Millionen von Dateien finden.  
2. **Legal Document Review** – Vor der Indizierung vertrauliche Informationen redigieren, um versehentliche Offenlegung zu vermeiden.  
3. **Archival Solutions** – Durchsuchbare Metadaten für historische Aufzeichnungen bewahren, ohne gesamte Archive in den Speicher zu laden.  
4. **Content Management Platforms** – Site‑weite Suche für Blogs, Wissensdatenbanken und Multimedia‑Bibliotheken ermöglichen.  
5. **Data Compliance Audits** – Sicherstellen, dass nur bereinigte Inhalte durchsuchbar sind, um regulatorische Anforderungen zu erfüllen.

## Leistungsüberlegungen

- **Optimize Indexing** – Planen Sie nächtliche inkrementelle Indizierung; verwenden Sie `AddFolder` mit einer Batch‑Größe von 100 Dateien, um I/O‑Spitzen zu reduzieren.  
- **Resource Management** – Überwachen Sie CPU und RAM; GroupDocs.Search verarbeitet Dateien gestreamt und hält den Spitzenverbrauch unter 200 MB, selbst bei 10 GB‑Indizes.  
- **Best Practices** – Speichern Sie den Index auf SSDs für sub‑sekunden‑Antwortzeiten und aktivieren Sie die Kompression (`index.Compression = true`), um den Festplattenverbrauch zu halbieren.

## Häufig gestellte Fragen

**Q: Kann ich nicht‑Textdateien mit GroupDocs indizieren?**  
A: Ja, GroupDocs.Search kann über 150 Formate indizieren – einschließlich PDFs, DOCX, PPTX, XLSX und Bildtypen – indem bei Bedarf eingebetteter Text mittels OCR extrahiert wird.

**Q: Wie gehe ich mit großen Mengen von Dokumenten um?**  
A: Verwenden Sie `AddFolder` mit einer konfigurierbaren Batch‑Größe, führen Sie die Indizierung in einem Hintergrunddienst aus und rufen Sie periodisch `Optimize()` auf, um kleine Indexsegmente zusammenzuführen.

**Q: Was sind die Vorteile der Verwendung von Redaktion zusammen mit Indizierung?**  
A: Die Redaktion entfernt personenbezogene Daten, bevor sie jemals den Index erreichen, und garantiert, dass Suchergebnisse niemals geschützte Daten preisgeben.

**Q: Ist es möglich, Suchalgorithmen anzupassen?**  
A: GroupDocs.Search bietet Synonym‑Dictionaries, benutzerdefinierte Tokenizer und reguläre‑Ausdruck‑Filter, mit denen Sie die Relevanzbewertung feinabstimmen können.

**Q: Wie behebe ich häufige Indexierungsprobleme?**  
A: Überprüfen Sie die Ordnerberechtigungen, stellen Sie sicher, dass die .NET‑Runtime mit dem Ziel der Bibliothek übereinstimmt, und prüfen Sie die im Indexordner erzeugte Protokolldatei auf detaillierte Fehlermeldungen.

## Ressourcen

- **Documentation**: [GroupDocs Redaction .NET Dokumentation](https://docs.groupdocs.com/search/net/)  
- **API Reference**: [GroupDocs Redaction .NET API](https://reference.groupdocs.com/redaction/net)  
- **Download**: [Neueste GroupDocs-Versionen](https://releases.groupdocs.com/search/net/)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Temporäre Lizenz anfordern](https://purchase.groupdocs.com/temporary-license/)  

Erkunden Sie diese Ressourcen, um Ihr Verständnis zu vertiefen und Ihre Implementierung von GroupDocs.Search und Redaction in .NET zu verbessern. Viel Spaß beim Programmieren!

---

**Zuletzt aktualisiert:** 2026-07-26  
**Getestet mit:** GroupDocs.Search 23.10, GroupDocs.Redaction 23.10 for .NET  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Master Index Creation and Merging with GroupDocs.Redaction .NET for Efficient Document Management](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)  
- [Mastering GroupDocs.Redaction .NET: Efficient Index Creation and Alias Management for Advanced Document Search](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)  
- [Master GroupDocs Search and Redaction in .NET: A Comprehensive Guide for Document Management](/search/net/document-management/groupdocs-search-redaction-net-tutorial/)