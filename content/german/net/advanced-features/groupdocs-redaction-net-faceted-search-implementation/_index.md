---
date: '2026-04-02'
description: Erfahren Sie, wie Sie einen Suchindex mit GroupDocs erstellen und Dokumente
  zum Index hinzufügen, während Sie facettierte Suche mit GroupDocs.Search und GroupDocs.Redaction
  in .NET implementieren.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Suchindex mit GroupDocs und Redaction .NET Faceted Search erstellen
type: docs
url: /de/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Erstellen eines Suchindex mit GroupDocs Redaction .NET Faceted Search

In modernen Anwendungen ist **die Erstellung eines Suchindex mit GroupDocs** entscheidend für eine schnelle, genaue Dokumentenabfrage. Egal, ob Sie rechtliche Verträge, Produktkataloge oder große Wissensdatenbanken verwalten, ein gut gebauter Index ermöglicht es Ihnen, **Dokumente zum Index hinzuzufügen** und leistungsstarke facettierte Suchen in Sekunden durchzuführen. Dieses Tutorial führt Sie durch den gesamten Prozess – von der Einrichtung von GroupDocs.Redaction bis hin zur Erstellung einfacher und komplexer facettierter Abfragen – damit Sie ein reaktionsschnelles Sucherlebnis in Ihren .NET-Projekten bereitstellen können.

## Schnelle Antworten
- **Was ist der Hauptzweck?** Einen Suchindex mit GroupDocs zu erstellen und facettierte Suche zu ermöglichen.  
- **Welche Bibliotheken werden benötigt?** GroupDocs.Redaction und GroupDocs.Search für .NET.  
- **Wie füge ich Dokumente zum Index hinzu?** Verwenden Sie `index.Add(documentsFolder)` nach der Initialisierung des Index.  
- **Kann ich komplexe Abfragen ausführen?** Ja, kombinieren Sie Objektabfragen mit logischen Operatoren für erweiterte Filterungen.  
- **Wird eine Lizenz benötigt?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine kommerzielle Lizenz erforderlich.

## Was ist facettierte Suche und warum mit GroupDocs verwenden?
Facettierte Suche ermöglicht es Benutzern, Ergebnisse durch gleichzeitiges Anwenden mehrerer Filter – wie Kategorie, Datum oder Autor – zu verfeinern. In Kombination mit **GroupDocs.Redaction** erhalten Sie sichere, durchsuchbare Inhalte, die Redaktionsregeln respektieren, was sie ideal für stark regulierte Umgebungen macht.

## Voraussetzungen

### Erforderliche Bibliotheken, Versionen und Abhängigkeiten
- **GroupDocs.Redaction .NET** – neueste stabile Version.  
- **GroupDocs.Search .NET** – arbeitet Hand in Hand mit Redaction für die Indexierung.

### Anforderungen an die Umgebungseinrichtung
- **IDE**: Visual Studio 2019 oder neuer.  
- **Framework**: .NET Core 3.1, .NET 5 oder .NET 6.  
- **OS-Kompatibilität**: Windows, Linux, macOS.

### Wissensvoraussetzungen
Grundlegende C#‑Kenntnisse und ein grundlegendes Verständnis von facettierten Suchkonzepten sind hilfreich, aber die Schritt‑für‑Schritt‑Anleitung ist auch für Einsteiger geeignet.

## Einrichtung von GroupDocs.Redaction für .NET

### Installationsinformationen
Sie können das GroupDocs.Redaction‑Paket mit einer der folgenden Methoden hinzufügen:

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Suchen Sie nach "GroupDocs.Redaction" und installieren Sie die neueste Version.

### Schritte zum Erwerb einer Lizenz
Um alle Funktionen freizuschalten, beginnen Sie mit einer kostenlosen Testversion oder erhalten Sie eine permanente Lizenz:

1. Besuchen Sie [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/), um Lizenzoptionen zu erkunden.  
2. Folgen Sie den Anweisungen auf dem Bildschirm, um Ihre Test- oder gekaufte Lizenzdatei zu erhalten.

### Grundlegende Initialisierung und Einrichtung
Nachdem das Paket installiert ist, initialisieren Sie den Redactor in Ihrer Anwendung:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Wie man einen Suchindex mit GroupDocs erstellt

Im Folgenden teilen wir die Implementierung in zwei Teile: **Einfache facettierte Suche** und **Komplexe Abfrage**. Jeder Teil zeigt, wie man **einen Suchindex mit GroupDocs erstellt**, Dokumente hinzufügt und Abfragen ausführt.

### Feature 1: Einfache facettierte Suche

**Übersicht**  
Facettierte Suche ermöglicht es Benutzern, Ergebnisse durch Auswahl mehrerer Kriterien einzugrenzen. Dieser Abschnitt demonstriert einen einfachen Ansatz mit GroupDocs.Search.

#### Schritt 1: Index- und Dokumentordner definieren
Richten Sie die Ordnerpfade ein, in denen der Index gespeichert wird und in denen sich Ihre Quelldokumente befinden.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Schritt 2: Index erstellen
```csharp
Index index = new Index(indexFolder);
```

#### Schritt 3: Dokumente zum Index hinzufügen
```csharp
index.Add(documentsFolder);
```

#### Schritt 4: Textabfrage durchführen
Führen Sie eine einfache Textabfrage gegen das Feld **content** aus.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Schritt 5: Objektabfrage ausführen
Verwenden Sie objektorientierte Abfragen für feinere Kontrolle.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Feature 2: Komplexe Abfrage

**Übersicht**  
Wenn Sie mehrere Filter kombinieren müssen – z. B. Dateinamensmuster und Phrasenübereinstimmungen – können Sie eine komplexe Abfrage mit logischen Operatoren erstellen.

#### Schritt 1: Index- und Dokumentordner definieren
Verwenden Sie dieselbe Ordnerstruktur für ein fortgeschritteneres Szenario erneut.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Schritt 2: Index erstellen und Dokumente hinzufügen
(Siehe Schritte 2‑3 aus dem einfachen Beispiel; sie bleiben unverändert.)

#### Schritt 3: Textabfrage ausführen
Führen Sie eine zusammengesetzte Textabfrage aus, die Dateinamen- und Inhaltskriterien kombiniert.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Schritt 4: Objektabfragen erstellen und ausführen
Erstellen Sie dieselbe Logik programmgesteuert.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Fahren Sie fort, Phrasen, Bereiche und boolesche Operatoren zu kombinieren, um Ihre genauen Geschäftsregeln zu erfüllen.

## Praktische Anwendungen

1. **E‑Commerce-Plattformen** – Produkte nach Kategorie, Preis und Bewertung filtern.  
2. **Dokumentenmanagementsysteme** – Verträge nach Autor, Datum oder Vertraulichkeitsstufe finden.  
3. **Content-Portale** – Lesern ermöglichen, nach Tags, Themen und Veröffentlichungsdaten zu filtern.

## Leistungsüberlegungen

- **Index-Aktualisierung**: Regelmäßig neue oder aktualisierte Dateien neu indexieren, um die Suche schnell zu halten.  
- **Speicherverwaltung**: Entsorgen Sie `Index`‑Objekte, wenn sie nicht mehr benötigt werden, insbesondere bei großen Datenmengen.  
- **Asynchrones Indexieren**: Verwenden Sie `Task.Run` oder Hintergrunddienste, um UI‑Einbrüche während intensiven Indexierens zu vermeiden.

## Häufige Probleme und Lösungen

| Problem | Lösung |
|---------|--------|
| **Index nicht gefunden** | Überprüfen Sie den Pfad `indexFolder` und stellen Sie sicher, dass der Ordner Schreibrechte hat. |
| **Keine Ergebnisse zurückgegeben** | Stellen Sie sicher, dass die Felder, die Sie abfragen (z. B. `Content`, `Filename`), indexiert sind. |
| **Out‑of‑Memory‑Fehler** | Verarbeiten Sie Dokumente in Batches und erwägen Sie, die .NET‑GC‑Heap‑Größe zu erhöhen. |

## Häufig gestellte Fragen

**Q: Was ist facettierte Suche?**  
A: Facettierte Suche ermöglicht es Benutzern, Ergebnisse mithilfe mehrerer unabhängiger Filter wie Kategorie, Datum oder Autor zu verfeinern.

**Q: Wie gehe ich mit großen Datensätzen in GroupDocs.Search um?**  
A: Verwenden Sie inkrementelles Indexieren, Batch‑Verarbeitung und asynchrone Vorgänge, um den Speicherverbrauch niedrig und die Leistung hoch zu halten.

**Q: Kann ich GroupDocs‑Funktionalitäten in bestehende .NET‑Anwendungen integrieren?**  
A: Ja, die Bibliotheken sind für die nahtlose Integration in jedes .NET‑Projekt konzipiert.

**Q: Was sind häufige Probleme bei facettierter Suche?**  
A: Komplexe Abfragesyntax und die Sicherstellung, dass alle relevanten Felder indexiert sind, sind typische Herausforderungen; gründliche Tests und Indexwartung mindern diese.

**Q: Wie erhalte ich eine temporäre Lizenz für GroupDocs?**  
A: Besuchen Sie die [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/), um eine Testlizenz zu beantragen, die während der Evaluierung die volle Funktionalität freischaltet.

## Ressourcen
- **Dokumentation**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API‑Referenz**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Zuletzt aktualisiert:** 2026-04-02  
**Getestet mit:** GroupDocs.Redaction 23.12 für .NET, GroupDocs.Search 23.12 für .NET  
**Autor:** GroupDocs