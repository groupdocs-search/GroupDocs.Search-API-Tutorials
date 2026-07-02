---
date: '2026-01-16'
description: Erfahren Sie, wie Sie das GroupDocs‑Suchnetzwerk in Java konfigurieren
  und Synonyme zum Index hinzufügen, um die Sucheffizienz zu verbessern.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Konfigurieren Sie GroupDocs.Search Network in Java – Boost Search
type: docs
url: /de/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Konfigurieren des GroupDocs.Search Netzwerks in Java – Suche beschleunigen

In heutigen datengetriebenen Anwendungen ist **configure groupdocs search network** der entscheidende Schritt, um schnelle, genaue Ergebnisse über massive Dokumentensammlungen zu liefern. Egal, ob Sie ein unternehmensweites Suchportal aufbauen oder eine bestehende Lösung erweitern, ein gut konfiguriertes GroupDocs.Search Netzwerk ermöglicht horizontales Skalieren, das Hinzufügen von Synonymunterstützung und niedrige Latenz. In diesem Tutorial lernen Sie, wie Sie ein GroupDocs.Search Netzwerk mit Java einrichten, bereitstellen und feinabstimmen, sowie praktische Tipps zum Hinzufügen von Synonymen zum Index und zur Verwaltung von Node‑Lebenszyklen.

## Quick Answers
- **Was ist der Hauptvorteil der Konfiguration eines GroupDocs.Search Netzwerks?** Sie ermöglicht verteiltes Indexieren und Abfragen, was Leistung und Skalierbarkeit verbessert.  
- **Benötige ich eine Lizenz, um die Beispiele auszuführen?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Können Synonyme hinzugefügt werden, ohne den Index neu aufzubauen?** Ja – verwenden Sie das Synonym‑Wörterbuch zur Laufzeit, um **add synonyms to index**.  
- **Wie viele Nodes kann ich bereitstellen?** Sie können so viele Nodes bereitstellen, wie Ihre Infrastruktur zulässt; jeder Node läuft auf einem eigenen Port.  

## Was bedeutet die Konfiguration eines GroupDocs.Search Netzwerks?
Die Konfiguration eines GroupDocs.Search Netzwerks bedeutet, die Ordnerstruktur, Ports und Node‑Einstellungen zu definieren, die mehreren JVM‑Instanzen die Zusammenarbeit beim Indexieren und Suchen ermöglichen. Diese Einrichtung erstellt einen Master‑Node, der Worker (Shards) koordiniert und sicherstellt, dass Abfragen über den gesamten Datensatz ausgeführt werden.

## Warum ein GroupDocs.Search Netzwerk konfigurieren?
- **Skalierbarkeit** – Verteilung der Indexierungslast auf mehrere Maschinen.  
- **Zuverlässigkeit** – Nodes können hinzugefügt oder entfernt werden, ohne Ausfallzeiten.  
- **Suchrelevanz** – Synonyme zum Index hinzufügen für reichhaltigere Ergebnisse.  
- **Performance** – Parallele Abfrageausführung reduziert die Antwortzeit.

## Voraussetzungen
- Java Development Kit (JDK) 8 oder neuer  
- Maven zum Erstellen des Projekts  
- Grundlegende Kenntnisse der Java‑Syntax  
- Zugriff auf die GroupDocs.Search für Java Bibliothek (heruntergeladen über Maven oder die offizielle Release‑Seite)

## Einrichtung von GroupDocs.Search für Java

Fügen Sie das Repository und die Abhängigkeit zu Ihrer Maven **pom.xml** hinzu:

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

Alternativ können Sie die neueste Version direkt von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunterladen.

### Lizenzbeschaffung
- **Kostenlose Testversion** – Kernfunktionen ohne Kosten erkunden.  
- **Temporäre Lizenz** – Vollständige Funktionen für kurzfristige Tests freischalten.  
- **Kommerzielle Lizenz** – Für Produktionsbereitstellungen erforderlich.

### Grundlegende Initialisierung und Einrichtung
Erstellen Sie eine einfache Java‑Klasse, um zu überprüfen, ob die Bibliothek korrekt geladen wird:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Schritt‑für‑Schritt‑Anleitung zur Konfiguration des GroupDocs.Search Netzwerks

### 1. Konfiguration des Suchnetzwerks
Definieren Sie den Basis‑Dokumentenordner und den Start‑Port für die Node‑Kommunikation.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Ort, an dem Wörterbücher (z. B. Synonymdateien) liegen.  
- **basePort** – Der erste Port; nachfolgende Nodes erhöhen diesen Wert.

### 2. Bereitstellung von Suchnetzwerk‑Nodes
Starten Sie mehrere Worker‑Nodes, die dieselbe Konfiguration teilen.

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Jeder Node läuft auf einem eigenen Port (basePort + index) und hält einen Shard des Gesamindex.

### 3. Abonnieren von Node‑Ereignissen
Überwachen Sie Gesundheit, Indexierungsfortschritt und Fehlersituationen, indem Sie einen Ereignis‑Listener am Master‑Node anhängen.

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Ereignis‑Callbacks ermöglichen es Ihnen, auf Node‑Start/‑Stopp, Abschluss der Indexierung und unerwartete Fehler zu reagieren.

### 4. Hinzufügen von Synonymen zum Indexer eines Nodes
Verbessern Sie die Relevanz, indem Sie zur Laufzeit **add synonyms to index**.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Array von Begriffen, die als gleichwertig behandelt werden sollen.  
- **clearBeforeAdding** – Auf `true` setzen, wenn vorhandene Einträge ersetzt werden sollen.

### 5. Hinzufügen von Verzeichnissen für die Indexierung
Teilen Sie dem Master‑Node mit, welche Ordner die Dokumente enthalten, die durchsuchbar sein sollen.

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

Die Methode scannt das Verzeichnis rekursiv und verteilt Dateien über die Shards.

### 6. Durchführen einer Textsuche im Netzwerk
Führen Sie eine Abfrage über alle Nodes aus, optional mit erzwungenem exakten Trefferverhalten.

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Setzen Sie `exactMatchOnly` auf `true`, wenn Sie eine strikte Begriffsuche ohne Stemming benötigen.

### 7. Schließen von Netzwerk‑Nodes
Geben Sie Ressourcen nach Abschluss der Verarbeitung sauber frei.

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Ein korrektes Herunterfahren verhindert Speicherlecks und hält die JVM gesund.

## Praktische Anwendungen
| Szenario | Wie das Netzwerk hilft |
|----------|------------------------|
| **Enterprise Search** | Verteilen Sie die Indexierung über Rechenzentrums‑Server für Petabyte‑große Korpora. |
| **Document Management** | Fügen Sie Synonyme zum Index hinzu, damit Benutzer Dokumente auch bei unterschiedlicher Terminologie finden. |
| **E‑Commerce Katalog** | Stellen Sie region‑spezifische Nodes bereit, um lokalisierte Produktsuchen schnell zu bedienen. |
| **Content Management** | Halten Sie Inhalte durchsuchbar, während Redakteure neue Dateien in bestimmten Verzeichnissen hinzufügen. |

## Häufige Probleme & Lösungen
- **Portkonflikte** – Stellen Sie sicher, dass jeder Node‑Port (basePort + index) frei ist; passen Sie `basePort` bei Bedarf an.  
- **Synonym nicht angewendet** – Vergewissern Sie sich, dass Sie `indexer.setDictionary(dictionary)` nach dem Hinzufügen von Begriffen aufgerufen haben.  
- **Node reagiert nicht** – Abonnieren Sie Ereignisse; suchen Sie nach `NodeFailed` Callbacks, um Netzwerkprobleme zu diagnostizieren.  
- **Speicherleck beim Schließen** – Rufen Sie stets `node.close()` für jeden bereitgestellten Node auf.

## Häufig gestellte Fragen

**F: Wie verbessert das Bereitstellen mehrerer Nodes die Suchleistung?**  
A: Jeder Node indexiert einen Shard der Daten, wodurch parallele Verarbeitung ermöglicht wird und die Abfrage‑Latenz reduziert wird, da die Arbeitslast geteilt wird.

**F: Kann ich Synonyme hinzufügen, ohne vorhandene Dokumente neu zu indexieren?**  
A: Ja, Sie können zur Laufzeit über das Synonym‑Wörterbuch **add synonyms to index**; die Änderungen wirken sich sofort auf neue Abfragen aus.

**F: Ist das Abonnieren von Node‑Ereignissen zwingend erforderlich?**  
A: Obwohl es für den Grundbetrieb nicht nötig ist, bietet das Abonnieren von Ereignissen Einblick in die Node‑Gesundheit und hilft, bei Fehlern schnell zu reagieren.

**F: Was sind bewährte Methoden zur Verwaltung von Node‑Ressourcen?**  
A: Schließen Sie regelmäßig inaktive Nodes, überwachen Sie den JVM‑Speicherverbrauch und recyceln Sie Nodes während der Nebenzeiten, um den Ressourcenverbrauch optimal zu halten.

**F: Unterstützt GroupDocs.Search nicht‑Text‑Formate wie PDFs oder Bilder?**  
A: Absolut. Die Bibliothek extrahiert Text aus PDFs, Office‑Dateien und führt sogar OCR auf Bildern durch, sodass diese sofort durchsuchbar sind.

**Zuletzt aktualisiert:** 2026-01-16  
**Getestet mit:** GroupDocs.Search 25.4 für Java  
**Autor:** GroupDocs