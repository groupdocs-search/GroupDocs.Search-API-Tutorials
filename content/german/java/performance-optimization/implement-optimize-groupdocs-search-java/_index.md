---
date: '2026-07-07'
description: Erfahren Sie, wie Sie den Index löschen, Full Text Search in Java durchführen
  und die Search Performance mit GroupDocs.Search for Java optimieren. Schritt‑für‑Schritt‑Anleitung
  mit Network Setup und Indexing.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: Wie man den Index löscht und Full Text Search in Java mit GroupDocs.Search
  verwendet. Folgen Sie dieser Anleitung, um ein Search Network einzurichten, einen
  durchsuchbaren Index zu erstellen und die Search Performance zu optimieren.
og_title: Wie man den Index löscht und Text Search mit GroupDocs.Search for Java durchführt
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: Wie man den Index löscht und Text Search mit GroupDocs.Search for Java durchführt
type: docs
url: /de/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Wie man Index löscht und Textsuche mit GroupDocs.Search für Java durchführt

In der heutigen datengetriebenen Welt ist **how to delete index** schnell zu erledigen, während gleichzeitig blitzschnelle Volltextsuche‑Funktionen für Java bereitgestellt werden, ein Wettbewerbsvorteil. Egal, ob Sie ein internes Wissensbasis, ein Rechtsfall‑Repository oder einen E‑Commerce‑Produktkatalog aufbauen, ein gut abgestimmtes Suchnetzwerk kann die Benutzerzufriedenheit dramatisch steigern. In diesem Leitfaden lernen Sie, wie Sie **set up a search network**, **create a searchable index**, **optimize search performance** und **delete documents from the index** bei Bedarf – alles mit GroupDocs.Search für Java.

## Schnelle Antworten
- **Was ist der Hauptzweck von GroupDocs.Search für Java?** Es bietet Volltextsuche über mehr als 50 Dokumentformate und ermöglicht schnelle Schlüsselwortabfragen.  
- **Wie führe ich eine Textsuche in einer verteilten Umgebung durch?** Stellen Sie ein Suchnetzwerk bereit, indexieren Sie Dokumente auf einem Master‑Knoten und führen Sie dann Abfragen an jedem Knoten aus.  
- **Kann ich Dokumente aus dem Index löschen, ohne ihn neu aufzubauen?** Ja, verwenden Sie die Delete‑API, um ausgewählte Dateien zu entfernen, wodurch *how to delete index* ohne vollständiges Re‑Indexieren erreicht wird.  
- **Welche Java‑Version wird benötigt?** JDK 8 oder höher.  
- **Wird für die Produktion eine Lizenz benötigt?** Eine gültige GroupDocs.Search‑Lizenz ist erforderlich; eine kostenlose Testversion ist verfügbar.

## Was bedeutet „perform text search“?
Eine Textsuche bedeutet, einen Volltext‑Index abzufragen, um Dokumente zu finden, die die angegebenen Schlüsselwörter oder Phrasen enthalten. GroupDocs.Search erstellt einen invertierten Index, der diese Look‑ups extrem schnell macht, selbst bei Tausenden von Dateien.

## Warum ein Suchnetzwerk einrichten?
Ein Suchnetzwerk verteilt Indexierungs‑ und Abfrage‑Workloads über mehrere Knoten, sodass Sie **optimize search performance**, horizontal skalieren und hohe Verfügbarkeit gewährleisten können. Diese Architektur ist ideal für Unternehmens‑Dokumenten‑Repositorien, bei denen Latenz und Durchsatz entscheidend sind.

## Wie man ein Suchnetzwerk mit GroupDocs.Search für Java implementiert und optimiert
Laden Sie Ihre Konfiguration, starten Sie einen Master‑Knoten und fügen Sie dann Worker‑Knoten hinzu, die denselben Basis‑Pfad und Port teilen. Durch die Bereitstellung des Netzwerks auf diese Weise kann jeder Knoten Indexierungs‑ oder Abfrage‑Anfragen bearbeiten und konsistente Antwortzeiten liefern, selbst wenn die Dokumentenzahl in die Hunderttausende steigt.

### Schritt‑für‑Schritt‑Übersicht
1. **Definieren Sie eine Basiskonfiguration**, die ein gemeinsames Verzeichnis und einen TCP‑Port enthält.  
2. **Starten Sie den Master‑Knoten**, um den Index zu verwalten und die Worker‑Knoten zu koordinieren.  
3. **Fügen Sie Worker‑Knoten hinzu**, die sich mit dem Master verbinden und paralleles Indexieren sowie Suchen ermöglichen.  
4. **Überwachen Sie die Ressourcennutzung** und passen Sie die JVM‑Heap‑Einstellungen an, um die Latenz gering zu halten.

## Wie man den Index in GroupDocs.Search für Java löscht
`SearchNode` stellt einen Knoten im GroupDocs.Search‑Netzwerk dar, das Indexierungs‑ und Abfrage‑Operationen verwaltet. Die Methode `delete` entfernt angegebene Dokumente aus dem Index.

### Direkte Löschschritte
- Rufen Sie die Methode `delete` auf der `SearchNode`‑Instanz auf.  
- Geben Sie ein Array mit relativen Dateipfaden an.  
- Übernehmen Sie die Änderungen; der Index wird sofort aktualisiert und nachfolgende Suchvorgänge geben die entfernten Dateien nicht mehr zurück.

## Was ist ein Suchnetzwerk?
Ein **search network** ist ein Cluster miteinander verbundener Knoten, die ein gemeinsames Index‑Repository teilen und verteilte Indexierung sowie Abfrageausführung ermöglichen. Es erlaubt horizontales Skalieren und Fehlertoleranz für großflächige Dokumentensammlungen.

## Wie man einen durchsuchbaren Index erstellt (index documents java)
Die `add`‑Methode indexiert ein Dokument in den Such‑Index. Fügen Sie Dokumente dem Master‑Knoten mit der `add`‑Methode hinzu; das Netzwerk propagiert die Änderungen an alle Worker‑Knoten. Dieser Ansatz stellt sicher, dass jeder Knoten Abfragen gegen den neuesten Index ohne zusätzliche Synchronisationsschritte ausführen kann.

### Schlüsselaktionen
- Zeigen Sie den Master‑Knoten auf den Ordner, der die Quelldateien enthält.  
- Rufen Sie die Indexierungsroutine auf; das Netzwerk verarbeitet jede Datei und aktualisiert den invertierten Index.  
- Vergewissern Sie sich, dass die Indexdateien im vorgesehenen Speicherverzeichnis erscheinen.

## Wie man indizierte Dateien entfernt (remove indexed files)
Wenn ein Dokument veraltet ist, rufen Sie die `delete`‑API mit seinem Pfad auf. Das System entfernt die Einträge der Datei aus dem invertierten Index, spart Speicherplatz und verhindert veraltete Ergebnisse.

## Einrichtung von GroupDocs.Search für Java
Um zu beginnen, integrieren Sie GroupDocs.Search in Ihr Java‑Projekt mit der folgenden Einrichtung:

### Maven‑Setup
Fügen Sie das Repository und die Abhängigkeit zu Ihrer `pom.xml`‑Datei hinzu:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

### Direkter Download
Alternativ können Sie [die neueste Version direkt von GroupDocs herunterladen](https://releases.groupdocs.com/search/java/).

### Lizenzbeschaffung
GroupDocs bietet eine kostenlose Testversion, mit der Sie die Funktionen vor dem Kauf evaluieren können. Sie können eine temporäre Lizenz erhalten, indem Sie den Schritten auf ihrer [Kaufseite](https://purchase.groupdocs.com/temporary-license/) folgen. Dadurch wird die volle Funktionalität während Ihrer Testphase aktiviert.

### Grundlegende Initialisierung und Einrichtung
Initialisieren Sie GroupDocs.Search in Ihrer Java‑Anwendung mit:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## Implementierungsleitfaden

### Konfiguration des Suchnetzwerks
**Übersicht:** Legen Sie einen Basis‑Pfad und einen Port für Ihr Suchnetzwerk fest, damit die Knoten effektiv kommunizieren können.

#### Schritt 1: Basis-Konfiguration definieren
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parameter:**  
  - `basePath`: Verzeichnispfad für Netzwerkoperationen.  
  - `basePort`: Port‑Nummer, die vom Suchnetzwerk verwendet wird.

#### Schritt 2: Fehlerbehebung
Stellen Sie sicher, dass Ihr angegebener Port nicht durch Firewall‑Einstellungen blockiert ist oder bereits von einer anderen Anwendung verwendet wird. Passen Sie ihn bei Bedarf an, um Konflikte zu vermeiden.

### Bereitstellung von Suchnetzwerk‑Knoten
**Übersicht:** Verwenden Sie Ihre Konfiguration, um Knoten über Ihr Netzwerk für verteilte Indexierung und Suche bereitzustellen.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Wichtige Konfigurationsoptionen:**  
  - **Base Path & Port:** Diese Werte sollten mit denen Ihrer anfänglichen Konfiguration übereinstimmen, um Konsistenz zu gewährleisten.

### Dokumente indexieren (`create searchable index`)
**Übersicht:** Fügen Sie Dokumente effizient über einen Master‑Knoten zum Such‑Index hinzu.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Zweck:**  
  - `masterNode`: Der primäre Knoten, der die Dokumenten‑Indexierung verwaltet.  
  - `documentsPath`: Pfad zum Verzeichnis, das die Dokumente enthält.

#### Tipps zur Fehlerbehebung
Stellen Sie sicher, dass Ihre Dokumenten‑Pfade korrekt und zugänglich sind. Vergewissern Sie sich, dass die Berechtigungen das Lesen aus diesen Verzeichnissen erlauben.

### Textsuche im Netzwerk (`perform text search`)
**Übersicht:** Führen Sie umfassende Textsuchen über Ihr indiziertes Netzwerk durch.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parameter:**  
  - `query`: Der Text, nach dem Sie suchen.  
  - `masterNode`: Knoten, der die Suche durchführt.

### Dokumente aus dem Index löschen (`delete documents index`)
**Übersicht:** Entfernen Sie bestimmte Dokumente aus Ihrem Index anhand ihrer Dateipfade.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Methodenzweck:**  
  - `node`: Der Zielknoten für Löschoperationen.  
  - `filePaths`: Pfade der Dokumente, die aus dem Index entfernt werden sollen.

#### Fehlerbehebung
Stellen Sie sicher, dass die Dateipfade exakt sind und die Dateien im Verzeichnis existieren. Bei anhaltenden Problemen prüfen Sie Netzwerkberechtigungen und Konnektivität.

## Praktische Anwendungen
1. **Enterprise Document Management:** Interne Wissensabfrage optimieren.  
2. **Legal Case Analysis:** Schnell relevante Fallakten über mehrere Repositorien hinweg finden.  
3. **E‑Commerce Platforms:** Produktsuchgeschwindigkeit steigern, indem Beschreibungen und Bewertungen indexiert werden.  
4. **Academic Research:** Große digitale Bibliotheken von Artikeln und Abschlussarbeiten effizient durchsuchen.  
5. **Customer Support Systems:** Reaktionszeit reduzieren, indem Agenten vergangene Tickets sofort durchsuchen können.

## Leistungsüberlegungen
- **Indexierungsgeschwindigkeit optimieren:** Fügen Sie neue Dokumente schrittweise während Nebenzeiten hinzu, um die Latenz gering zu halten.  
- **Richtlinien zur Ressourcennutzung:** Überwachen Sie CPU und Speicher, insbesondere beim Skalieren der Knotenanzahl.  
- **Java‑Speicherverwaltung:** Passen Sie die JVM‑Heap‑Einstellungen basierend auf Ihrer Arbeitslast an (z. B. `-Xmx2g` für mittelgroße Indizes).

## Fazit
Durch Befolgen dieses Leitfadens haben Sie gelernt, wie Sie **set up a search network**, **create a searchable index**, **perform text search** und **delete documents index** mit GroupDocs.Search für Java nutzen. Diese Fähigkeiten ermöglichen eine schnelle, zuverlässige Dokumentenabfrage in verteilten Umgebungen.

**Nächste Schritte**
- Experimentieren Sie mit verschiedenen Knoten‑Konfigurationen, um das optimale Gleichgewicht für Ihre Arbeitslast zu finden.  
- Vertiefen Sie sich in erweiterte Indexierungsoptionen wie benutzerdefinierte Analyzer und Relevanz‑Tuning.  
- Erkunden Sie die Integration mit anderen GroupDocs‑Produkten für eine End‑zu‑End‑Dokumentenverarbeitung.

## Häufig gestellte Fragen

**Q: Was ist der primäre Anwendungsfall für GroupDocs.Search für Java?**  
A: Es bietet Volltextsuche über viele Dokumentformate, sodass Sie **perform text search** in großen Repositorien durchführen können.

**Q: Wie kann ich die Suchgeschwindigkeit in einem großen Netzwerk verbessern?**  
A: Stellen Sie zusätzliche Knoten bereit, passen Sie den JVM‑Heap an und planen Sie die Indexierung während Niedrigverkehrszeiten, um **optimize search performance** zu erreichen.

**Q: Ist es möglich, ein einzelnes Dokument zu löschen, ohne die gesamte Sammlung neu zu indexieren?**  
A: Ja, verwenden Sie die **delete documents index**‑API wie im Code‑Beispiel gezeigt, um bestimmte Dateien zu entfernen.

**Q: Benötige ich eine Lizenz für die Entwicklung?**  
A: Eine kostenlose Testlizenz reicht für Tests aus; für Produktionsumgebungen ist eine kommerzielle Lizenz erforderlich.

**Q: Kann ich PDFs, Word‑Dateien und E‑Mails zusammen indexieren?**  
A: Absolut – GroupDocs.Search unterstützt von Haus aus ein breites Spektrum an Formaten.

**Zuletzt aktualisiert:** 2026-07-07  
**Getestet mit:** GroupDocs.Search für Java 25.4  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Wie man Text in Java mit dem GroupDocs.Search‑Leitfaden indexiert](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [Suchleistung mit fortgeschrittenen Indexierungstechniken in GroupDocs.Search für Java optimieren](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [Abfrageleistung mit GroupDocs.Search Java verbessern: Index & Suche optimieren](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)