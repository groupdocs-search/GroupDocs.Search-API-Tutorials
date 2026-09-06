---
date: '2026-06-12'
description: Erfahren Sie, wie Sie einen Suchindex .NET erstellen und Redaction auf
  PDF anwenden, indem Sie GroupDocs.Search und GroupDocs.Redaction verwenden. Einrichtung,
  Bereitstellung, Indizierung und erweiterte Suche erklärt.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: Erstellen eines Suchindex .NET mit GroupDocs Search und Redaction – Ein umfassender
  Leitfaden
type: docs
url: /de/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Erstelle Suchindex .NET mit GroupDocs Search und Redaction – Ein umfassender Leitfaden

In der heutigen digitalen Landschaft ist **creating a search index .NET**‑Lösung, die sowohl Informationen schnell finden als auch sensible Daten schützen kann, für jede Organisation von höchster Priorität. Dieses Tutorial führt Sie durch die Konfiguration eines skalierbaren GroupDocs.Search‑Netzwerks, das Bereitstellen von Knoten, das Indexieren von Dokumenten und die Verwendung von GroupDocs.Redaction, um **Redaction auf PDF**‑Dateien anzuwenden – alles innerhalb einer .NET‑Umgebung.

## Schnelle Antworten
- **Was ist der erste Schritt, um einen search index .NET zu erstellen?** Definieren Sie einen Basis‑Pfad und Port und stellen Sie dann die Netzwerk‑Knoten bereit.  
- **Wie wende ich Redaction auf PDF mit GroupDocs an?** Initialisieren Sie eine `Redactor`‑Instanz, laden Sie das PDF und rufen Sie `Redact` mit den gewünschten Mustern auf.  
- **Kann ich das Suchnetzwerk auf mehreren Maschinen ausführen?** Ja – stellen Sie Knoten auf separaten Servern bereit und lassen Sie den Master‑Knoten das Indexieren und die Abfragen koordinieren.  
- **Benötige ich eine Lizenz für den Produktionseinsatz?** Eine gültige GroupDocs‑Lizenz ist für die Produktion erforderlich; eine temporäre Testlizenz steht für die Evaluierung zur Verfügung.  
- **Welche .NET‑Versionen werden unterstützt?** .NET Framework 4.7.2+, .NET Core 3.1+ und .NET 5/6/7 werden vollständig unterstützt.

## Was ist „create search index .net“?
*Creating a search index .NET* bezieht sich auf den Aufbau eines durchsuchbaren Repositorys von Dokumenten‑Metadaten und -Inhalten mithilfe von .NET‑Bibliotheken, die Text extrahieren, Begriffe tokenisieren und in einer optimierten Indexstruktur speichern. Dies ermöglicht sofortige Abfrageantworten über verteilte Knoten, unterstützt verschiedene Dateiformate und erlaubt skalierbare, hoch‑leistungsfähige Dokumenten‑Abrufe in Unternehmensanwendungen.

## Warum GroupDocs Search und Redaction zusammen verwenden?
GroupDocs.Search unterstützt **über 50 Dateiformate** – darunter DOCX, PDF, PPTX und HTML – und kann mehrseitige Dokumente indexieren, ohne die gesamte Datei in den Speicher zu laden. In Kombination mit GroupDocs.Redaction, das **Redaction auf PDF** in weniger als 200 ms pro Seite anwenden kann, erhalten Sie eine sichere, hoch‑leistungsfähige Dokumenten‑Management‑Pipeline.

## Voraussetzungen

### Erforderliche Bibliotheken & Abhängigkeiten
Um dieses Tutorial zu folgen, installieren Sie die folgenden Pakete:
- **GroupDocs.Search** für .NET
- **GroupDocs.Redaction** für .NET  

Sie können eine der folgenden Methoden verwenden, um die erforderlichen Bibliotheken zu installieren:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Suchen Sie nach "GroupDocs.Search" und "GroupDocs.Redaction" und installieren Sie die neueste Version.

### Anforderungen an die Umgebung
- .NET Framework 4.7.2 oder höher (oder .NET Core 3.1+)
- Visual Studio IDE (Community, Professional oder Enterprise)

### Vorkenntnisse
- Grundlegende C#‑Programmierung
- Objektorientierte Konzepte
- Vertrautheit mit Netzwerk‑Konfigurationen und Dokumenten‑Management‑Systemen

## Einrichtung von GroupDocs.Redaction für .NET

### Installationsinformationen
Um Redaction‑Funktionen in Ihre Anwendung zu integrieren, beginnen Sie mit dem Hinzufügen der GroupDocs.Redaction‑Bibliothek:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Suchen Sie nach "GroupDocs.Redaction" und installieren Sie sie.

### Lizenzbeschaffung
Um mit einer kostenlosen Testversion oder einer temporären Lizenz zu beginnen, folgen Sie diesen Schritten:
- Besuchen Sie die [GroupDocs-Website](https://purchase.groupdocs.com/temporary-license/), um eine temporäre Lizenz anzufordern.  
- Für Kaufoptionen gehen Sie zu ihrer [Preisseite](https://groupdocs.com/pricing).

Sobald Sie Ihre Lizenzdatei haben, wenden Sie sie in Ihrer Anwendungs‑Konfiguration an:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Grundlegende Initialisierung
Um GroupDocs.Redaction für grundlegende Vorgänge zu initialisieren, verwenden Sie das folgende Code‑Snippet:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Implementierungsleitfaden

### Konfigurationssetup

#### Übersicht
Diese Funktion konfiguriert Ihr Suchnetzwerk mithilfe eines Basis‑Pfads und einer Port‑Nummer und bildet die Grundlage Ihres Dokumenten‑Management‑Systems.

#### Definitionsanker
`SearchNetworkDeployment` ist die Klasse, die die Bereitstellung von Suchknoten im Netzwerk orchestriert.

#### Schritt 1: Basis‑Pfad und Port definieren  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### Schritt 2: Netzwerk konfigurieren
Verwenden Sie die Methode `Configure`, um das Suchnetzwerk mit dem angegebenen Pfad und Port einzurichten:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Bereitstellung von Netzwerk‑Knoten

#### Übersicht
Stellen Sie Knoten innerhalb Ihres konfigurierten Suchnetzwerks für verteilte Dokumentensuche bereit.

#### Definitionsanker
`SearchNetworkNode` repräsentiert einen einzelnen durchsuchbaren Knoten, der mit dem Master‑Knoten kommuniziert.

#### Schritt 1: Bereitstellung initialisieren  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Ereignisabonnierung für Master‑Knoten

#### Übersicht
Abonnieren Sie Ereignisse am Master‑Knoten, um Netzwerk‑Operationen effektiv zu überwachen und zu verwalten.

#### Definitionsanker
`SearchNetworkNodeEvents` bietet Rückrufe für Indexierung, Abfrageausführung und Fehlerbehandlung.

#### Schritt 1: Master‑Knoten identifizieren
Wählen Sie den ersten Knoten als Ihren Master aus:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### Schritt 2: Ereignisse abonnieren
Abonnieren Sie Ereignisse mit:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Dokumente indexieren

#### Übersicht
Indexieren Sie Dokumente für effiziente Suchvorgänge. Dieser Schritt ist entscheidend, damit Ihr Netzwerk die benötigten Daten schnell abrufen kann.

#### Definitionsanker
`SearchIndex` ist das Kernobjekt, das durchsuchbare Token und Metadaten für jede indizierte Datei speichert.

#### Schritt 1: Verzeichnisse zum Index hinzufügen  
```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Suchfunktion – Grundlegende Nutzung

#### Übersicht
Führen Sie grundlegende Suchvorgänge über Knoten im Netzwerk aus.

#### Direkte Antwort
Rufen Sie `SearchNetwork.Query("your term")` auf dem Master‑Knoten auf, um passende Dokumente sofort zu erhalten. Die Methode gibt eine Sammlung von `SearchResult`‑Objekten zurück, die Dateipfade und Relevanzwerte enthalten.  
`SearchNetwork.Query` ist eine Methode, die eine Suchabfrage über das gesamte Netzwerk ausführt und passende Ergebnisse zurückliefert.

#### Schritt 1: Suchparameter definieren  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Erweiterte Suchfunktion

#### Übersicht
Nutzen Sie erweiterte Suchtechniken mit anpassbaren Parametern für präzisere Ergebnisse.

#### Direkte Antwort
Implementieren Sie eine Methode, die ein `SearchOptions`‑Objekt erstellt, die Eigenschaften `UseFuzzySearch`, `Highlight` und `PageSize` setzt und es dann an `SearchNetwork.QueryAdvanced` übergibt. Dies liefert paginierte, hervorgehobene Ergebnisse mit aktivierter unscharfer Suche.  
`SearchNetwork.QueryAdvanced` ist eine Methode, die eine Abfrage mit erweiterten Optionen wie unscharfer Suche und Paginierung ausführt.

#### Schritt 1: Erweiterte Suchmethode implementieren  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### Redaction auf PDF-Dateien anwenden

#### Übersicht
Sichern Sie sensible Informationen, indem Sie PDF‑Inhalte redigieren, bevor sie gespeichert oder geteilt werden.

#### Direkte Antwort
Erstellen Sie eine `Redactor`‑Instanz, laden Sie das Ziel‑PDF, definieren Sie ein `RedactionPattern` (z. B. SSN‑Regex), rufen Sie `redactor.Apply(pattern)` auf und speichern Sie schließlich das redigierte Dokument. Dieser Vorgang stellt sicher, dass persönliche Daten dauerhaft entfernt werden.

#### Definitionsanker
`Redactor` ist die Hauptklasse in GroupDocs.Redaction, die Dokumente verarbeitet und Redaktionsregeln anwendet.

#### Beispielablauf (kein neuer Code‑Block)
1. Initialisieren Sie `Redactor` mit Ihrer Lizenz.  
2. Laden Sie das PDF mit `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` stellt eine Regel dar, die den zu redigierenden Text oder das Muster definiert. Definieren Sie Muster wie `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. Führen Sie `redactor.Apply(pattern)` aus.  
5. Speichern Sie das Ergebnis mit `redactor.Save("sample_redacted.pdf")`.

### Praktische Anwendungen

#### Praxisbeispiele
1. **Legal Document Management** – Verträge effizient durchsuchen und automatisch Kundenkennungen redigieren.  
2. **Healthcare Records** – Patientennotizen finden und gleichzeitig HIPAA‑konforme Redaktion von PHI sicherstellen.  
3. **Corporate Compliance** – Interne Kommunikation nach verbotenen Begriffen scannen und vor der Archivierung redigieren.

## Fazit 
Dieser Leitfaden bietet einen umfassenden Weg für **creating a search index .NET**‑Lösungen, die skalieren, schnell indexieren und Daten durch Redaction schützen. Durch das Konfigurieren von Knoten, das Indexieren von Dokumenten, die Nutzung erweiterter Suchfunktionen und das Anwenden von Redaction können Entwickler die Dokumenten‑Management‑Workflows erheblich verbessern und gleichzeitig strenge Sicherheitsstandards einhalten.

## Häufig gestellte Fragen

**Q: Wie richte ich ein verteiltes Suchnetzwerk in .NET mit GroupDocs ein?**  
A: Definieren Sie einen Basis‑Pfad und Port und rufen Sie `SearchNetworkDeployment.Deploy()` auf, um Master‑ und Worker‑Knoten über mehrere Maschinen zu starten.

**Q: Kann ich erweiterte Suchen mit mehreren Parametern in GroupDocs durchführen?**  
A: Ja – verwenden Sie `SearchOptions`, um unscharfe Suche, Platzhalterunterstützung und Ergebnis‑Highlighting in einer einzigen Abfrage zu kombinieren.

**Q: Ist es möglich, die Netzwerkaktivität am Master‑Knoten zu überwachen?**  
A: Absolut – abonnieren Sie `SearchNetworkNodeEvents` wie `IndexingCompleted` und `QueryExecuted` für Echtzeit‑Einblicke.

**Q: Wie wende ich Redaction auf PDF‑Dateien mit GroupDocs an?**  
A: Initialisieren Sie einen `Redactor`, laden Sie das PDF, definieren Sie `RedactionPattern`‑Objekte (Regex oder Literal‑Strings), rufen Sie `Apply` auf und speichern Sie das bereinigte Dokument.

**Q: Was ist der einfachste Weg, die Suchleistung in einer vernetzten Umgebung zu verbessern?**  
A: Indexieren Sie Ihren gesamten Dokumentensatz vollständig vor den Abfragen, verteilen Sie Knoten, um Parallelverarbeitung zu nutzen, und optimieren Sie `SearchOptions` für Caching und Paging.

**Zuletzt aktualisiert:** 2026-06-12  
**Getestet mit:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Master .NET Dokumenten‑Indexierung mit GroupDocs.Search: Ein umfassender Leitfaden](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Master‑Dokumenten‑Indexierung und erweiterte Suchabfragen mit GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [Meisterung von GroupDocs Search und Redaction in .NET: Fortgeschrittenes Dokumenten‑Management](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)