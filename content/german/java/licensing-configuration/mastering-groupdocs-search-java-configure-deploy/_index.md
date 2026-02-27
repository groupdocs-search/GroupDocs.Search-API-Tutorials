---
date: '2026-01-08'
description: Erfahren Sie, wie Sie die Suche konfigurieren und Echtzeit‑Suchupdates
  mit GroupDocs.Search für Java aktivieren. Schritt‑für‑Schritt‑Anleitung zur Netzwerkeinrichtung,
  Knotenbereitstellung und Indizierung.
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 'So konfigurieren Sie die Suche mit GroupDocs.Search in Java - Konfigurations‑
  und Bereitstellungsleitfaden'
type: docs
url: /de/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# Wie man die Suche mit GroupDocs.Search in Java konfiguriert

In der heutigen schnelllebigen digitalen Welt kann **wie man die Suche konfiguriert** effizient den Erfolg eines Projekts ausmachen oder verhindern. Ob Sie tausende von Verträgen, Forschungsarbeiten oder internen Berichten bearbeiten, ein gut gestaltetes Suchnetzwerk ermöglicht es, das richtige Dokument in Sekunden zu finden. Dieses Tutorial führt Sie durch die Konfiguration eines Suchnetzwerks, das Bereitstellen von Knoten und das Aktivieren von **Echtzeit‑Suchupdates** mit GroupDocs.Search für Java.

## Schnelle Antworten
- **Was ist der Hauptzweck eines Suchnetzwerks?** Um die Indexierung und Abfrageverarbeitung über mehrere Knoten zu verteilen, um Skalierbarkeit und Geschwindigkeit zu erreichen.  
- **Welche Bibliotheksversion ist erforderlich?** GroupDocs.Search für Java v25.4 oder neuer.  
- **Brauche ich eine Lizenz?** Eine kostenlose Testversion reicht für die Evaluierung; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Wie werden Echtzeit‑Updates gehandhabt?** Durch das Abonnieren von Knoten‑Events, die bei Änderungen der Indexierung ausgelöst werden.  
- **Kann ich neue Dokumentordner unterwegs hinzufügen?** Ja — verwenden Sie die Methode `addDirectories` des Indexers.

## Was bedeutet „wie man die Suche konfiguriert“ im GroupDocs‑Kontext?
Die Konfiguration der Suche bedeutet, ein **Suchnetzwerk** einzurichten, das weiß, wo Ihre Dokumente gespeichert sind, wie Knoten kommunizieren und wie die Indexierung koordiniert wird. Sobald das Netzwerk konfiguriert ist, können Sie Knoten hinzufügen oder entfernen, ohne Ausfallzeiten, und gewährleisten so kontinuierlichen Zugriff auf aktuelle Suchergebnisse.

## Warum GroupDocs.Search für Java verwenden?
- **Skalierbarkeit:** Arbeitslasten über mehrere Maschinen verteilen.  
- **Echtzeit‑Updates:** Neu indizierte Dateien sofort im gesamten Netzwerk widerspiegeln.  
- **Einfache Integration:** Einfache Maven‑Einrichtung und klare Java‑APIs.  
- **Enterprise‑bereit:** Bewältigt große Korpora und komplexe Abfrageszenarien.

## Voraussetzungen
- **Java Development Kit (JDK) 8+** installiert.  
- **Maven** für das Abhängigkeitsmanagement.  
- Grundlegende Kenntnisse in Java, Maven und Suchkonzepten.

## Einrichtung von GroupDocs.Search für Java

### Maven‑Abhängigkeit
Fügen Sie das Repository und die Abhängigkeit zu Ihrer `pom.xml` hinzu:

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

**Direkter Download:** Sie können die Bibliothek auch von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) beziehen.

### Lizenzbeschaffung
- **Kostenlose Testversion:** Holen Sie sich eine Testlizenz, um alle Funktionen zu erkunden.  
- **Temporäre Lizenz:** Beantragen Sie eine erweiterte Evaluierungsdauer.  
- **Kommerzielle Lizenz:** Für Produktionseinsätze erforderlich.

### Grundlegende Initialisierung
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Wie man ein Suchnetzwerk in Java konfiguriert

### Schritt 1: Erforderliche Pakete importieren
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### Schritt 2: Netzwerk konfigurieren
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Parameter:** `basePath` verweist auf Ihren Dokumentordner; `basePort` ist der TCP‑Port, der für die Knotenkommunikation verwendet wird.

## Bereitstellung von Suchnetzwerk‑Knoten

### Schritt 1: Bereitstellungspaket importieren
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### Schritt 2: Knoten bereitstellen
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Master‑Knoten:** Koordiniert Suchen und Indexierung über alle Knoten.

## Abonnieren von Knoten‑Events für Echtzeit‑Suchupdates

### Schritt 1: Ereignis‑Paket importieren
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### Schritt 2: Master‑Knoten‑Events abonnieren
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Ereignisbehandlung:** Ermöglicht **Echtzeit‑Suchupdates**, wann immer Dokumente hinzugefügt, aktualisiert oder entfernt werden.

## Hinzufügen von Verzeichnissen für die Indexierung

### Schritt 1: Indexer‑Paket importieren
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### Schritt 2: Dokumentverzeichnisse hinzufügen
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Dynamische Indexierung:** Fügen Sie beliebig viele Ordner hinzu; das Netzwerk indexiert sie automatisch.

## Abrufen indizierter Dokumente

### Schritt 1: Searcher‑Paket importieren
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### Schritt 2: Dokumentinformationen abrufen
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **Shard‑Verwaltung:** Handhabt große Datensätze effizient, indem Dokumente über Shards verteilt werden.

## Praktische Anwendungsfälle
1. **Enterprise‑Dokumentenmanagement:** Suche über Millionen von Dateien zentralisieren.  
2. **Rechtsanwaltskanzleien:** Schnell Fallakten, Verträge und Beweismaterial finden.  
3. **Akademische Forschung:** Zeitschriften und Arbeiten indexieren für sofortige Abrufe.

## Leistungsüberlegungen
- **Indexierung optimieren:** Regelmäßige Index‑Aktualisierungen planen und veraltete Daten entfernen.  
- **Speicherverwaltung:** JVM‑Heap überwachen, besonders beim Umgang mit großen Shards.  
- **Skalierbarkeitsplanung:** Knoten hinzufügen, wenn Ihr Korpus wächst; das Netzwerk balanciert die Last automatisch.

## Häufige Probleme & Lösungen

| Problem | Ursache | Lösung |
|---------|---------|--------|
| Knoten können nicht verbinden | Portkonflikt oder Firewall | Stellen Sie sicher, dass `basePort` offen ist und nicht von anderen Diensten verwendet wird |
| Index wird nicht aktualisiert | Ereignis‑Abonnement fehlt | Rufen Sie `SearchNetworkNodeEvents.subscribe(masterNode)` nach der Bereitstellung auf |
| Out‑of‑Memory‑Fehler | Zu viele große Shards geladen | Reduzieren Sie die Shard‑Größe oder erhöhen Sie den JVM‑Heap (`-Xmx`‑Flag) |

## Häufig gestellte Fragen

**Q: Kann ich neue Verzeichnisse hinzufügen, nachdem das Netzwerk läuft?**  
A: Ja — verwenden Sie die Methode `indexer.addDirectories()`; abonnierte Events propagieren Updates in Echtzeit.

**Q: Wie überwache ich die Knoten‑Gesundheit?**  
A: Jeder `SearchNetworkNode` stellt Status‑APIs bereit; integrieren Sie diese in Ihr bevorzugtes Überwachungstool.

**Q: Ist es möglich, den Master‑Knoten auf einer separaten Maschine zu betreiben?**  
A: Absolut. Stellen Sie lediglich sicher, dass alle Knoten denselben `basePort` verwenden und sich über das Netzwerk erreichen können.

**Q: Welche Dateiformate werden unterstützt?**  
A: GroupDocs.Search unterstützt PDFs, Word, Excel, PowerPoint, Klartext und viele weitere Formate sofort.

**Q: Muss ich das Netzwerk nach dem Hinzufügen eines neuen Knotens neu starten?**  
A: Nein — Knoten können dynamisch hinzugefügt oder entfernt werden; der Master‑Knoten wird die Shards automatisch neu ausbalancieren.

## Fazit
Sie haben nun ein vollständiges, Schritt‑für‑Schritt‑Verständnis von **wie man die Suche konfiguriert** mit GroupDocs.Search für Java, von der ersten Einrichtung bis zu Echtzeit‑Updates und verteilter Indexierung. Wenden Sie diese Muster an, um schnelle, skalierbare und zuverlässige Dokumentsuch‑Lösungen für jede Branche zu bauen.

---

**Zuletzt aktualisiert:** 2026-01-08  
**Getestet mit:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs