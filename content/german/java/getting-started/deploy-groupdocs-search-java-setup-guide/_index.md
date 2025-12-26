---
date: '2025-12-26'
description: Erfahren Sie, wie Sie mit GroupDocs.Search für Java einen durchsuchbaren
  Index in Java erstellen, Dateien zur Suche hinzufügen und Verzeichnisse zum Knoten
  hinzufügen.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: Durchsuchbaren Index in Java erstellen – GroupDocs.Search für Java bereitstellen
type: docs
url: /de/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# Erstellen eines durchsuchbaren Index in Java – Bereitstellung von GroupDocs.Search für Java

In der heutigen datengetriebenen Welt müssen Anwendungen, die **einen durchsuchbaren Index in Java erstellen**, massive Dokumentensammlungen effizient verarbeiten. Egal, ob Sie einen unternehmensweiten Suchdienst oder ein kleineres Projekt bauen, ein gut konfiguriertes Suchnetzwerk kann die Abrufgeschwindigkeit und Relevanz erheblich verbessern. In diesem Leitfaden führen wir Sie durch den gesamten Prozess der Einrichtung von **GroupDocs.Search für Java**, vom Hinzufügen von Dateien zur Suche bis zum Hinzufügen von Verzeichnissen zu einem Knoten, sodass Sie sofort mit der Indizierung Ihrer Dokumente beginnen können.

## Schnelle Antworten
- **Was ist der Hauptzweck von GroupDocs.Search?** Es bietet eine skalierbare, Java‑basierte Engine zum Indizieren und Durchsuchen von Dokumenten in einem verteilten Netzwerk.  
- **Welche Version sollte ich verwenden?** Die neueste stabile Version (z. B. 25.4) wird für neue Projekte empfohlen.  
- **Benötige ich eine Lizenz?** Eine 30‑tägige kostenlose Testversion ist verfügbar; für den Produktionseinsatz ist eine permanente Lizenz erforderlich.  
- **Kann ich sowohl Dateien als auch ganze Verzeichnisse hinzufügen?** Ja – verwenden Sie die Hilfsfunktionen `addFiles` und `addDirectories`, um Inhalte zu importieren.  
- **Welche Java‑Version wird benötigt?** Java 8 oder höher, mit Maven für das Abhängigkeitsmanagement.

## Was bedeutet „einen durchsuchbaren Index in Java erstellen“?
Einen durchsuchbaren Index in Java zu erstellen bedeutet, eine Datenstruktur aufzubauen, die Begriffe den Dokumenten zuordnet, die sie enthalten, und so schnelle Volltextabfragen ermöglicht. GroupDocs.Search übernimmt die aufwändige Arbeit, sodass Sie sich darauf konzentrieren können, Dokumente bereitzustellen und das Suchverhalten zu optimieren.

## Warum GroupDocs.Search für Java verwenden?
- **Skalierbare Netzwerkarchitektur** – Setzen Sie mehrere Knoten ein, die die Indexierungslast teilen.  
- **Umfangreiche Unterstützung von Dokumentformaten** – PDFs, Word, Excel, PowerPoint, Bilder und mehr.  
- **Ereignisgesteuerte Updates** – Abonnieren Sie Knoten‑Events, um den Index in Echtzeit aktuell zu halten.  
- **Einfache Maven‑Integration** – Fügen Sie ein paar Zeilen zu `pom.xml` hinzu und beginnen Sie mit der Indizierung.

## Voraussetzungen
- **JDK 8+** auf Ihrer Entwicklungsmaschine installiert.  
- Eine IDE wie **IntelliJ IDEA** oder **Eclipse**.  
- Grundkenntnisse in **Java** und **Maven**.  
- Zugriff auf die **GroupDocs.Search für Java**‑Bibliothek (Download oder Maven).

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

> **Pro‑Tipp:** Halten Sie die Versionsnummer aktuell, indem Sie die offizielle Release‑Seite prüfen.

Sie können das JAR auch direkt von der offiziellen Seite herunterladen: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lizenzbeschaffung
- **Kostenlose Testversion:** 30‑tägige Evaluierung.  
- **Temporäre Lizenz:** Anfrage für erweitertes Testen.  
- **Kauf:** Für Produktionseinsätze erforderlich.

### Grundlegende Initialisierung
Erstellen Sie ein Konfigurationsobjekt, das auf einen Ordner verweist, in dem Indexdateien gespeichert werden, und den Basis‑Kommunikationsport definiert:

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## Wie erstelle ich einen durchsuchbaren Index in Java mit GroupDocs.Search?

Im Folgenden erläutern wir die Kernfunktionen, die Sie benötigen, um **Dateien zur Suche hinzuzufügen** und **Verzeichnisse zu einem Knoten hinzuzufügen**, und gleichzeitig ein skalierbares Netzwerk bereitzustellen.

### Feature 1 – Konfiguration und Netzwerk‑Setup
Die Konfiguration des Suchnetzwerks ist der erste Schritt zum Aufbau eines durchsuchbaren Index.

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – Verzeichnis, in dem die Indexdaten gespeichert werden.  
- **`basePort`** – Startport; jeder Knoten erhöht diesen Wert.

### Feature 2 – Bereitstellung von Suchnetzwerk‑Knoten
Das Bereitstellen von Knoten verteilt die Indexierungslast auf mehrere Maschinen oder Prozesse.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

Jeder `SearchNetworkNode` betreibt seinen eigenen Indexierungsservice, sodass Sie **einen durchsuchbaren Index in Java erstellen** können, der horizontal skaliert.

### Feature 3 – Abonnieren von Knoten‑Events
Echtzeit‑Updates halten den Index synchron mit Änderungen im Dateisystem.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

Durch das Abhören von Events können Sie automatisch eine erneute Indexierung auslösen, wenn neue Dateien eintreffen.

### Feature 4 – Hinzufügen von Verzeichnissen zu einem Netzwerk‑Knoten
Verwenden Sie diese Hilfsfunktion, um **Verzeichnisse zu einem Knoten hinzuzufügen**, wobei alle unterstützten Dokumente rekursiv gesammelt werden.

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

### Feature 5 – Hinzufügen von Dateien zu einem Netzwerk‑Knoten
Wenn Sie eine feinkörnige Kontrolle benötigen, **fügen Sie Dateien einzeln zur Suche hinzu**:

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Diese Methode bietet Ihnen die Flexibilität, Dateien aus Streams, Cloud‑Speicher oder temporären Speicherorten zu indexieren.

## Häufige Probleme & Lösungen
| Problem | Ursache | Lösung |
|---------|---------|--------|
| **Keine Dokumente erscheinen in den Suchergebnissen** | Index nicht bestätigt | Rufen Sie `node.getIndexer().commit()` nach dem Hinzufügen von Dateien auf. |
| **Portkonflikt‑Fehler** | Ein anderer Dienst verwendet `basePort` | Wählen Sie einen anderen `basePort` oder prüfen Sie freie Ports. |
| **Nicht unterstütztes Dateiformat** | Bibliothek fehlt ein Parser | Stellen Sie sicher, dass die Dateierweiterung unterstützt wird, oder fügen Sie einen benutzerdefinierten Extraktor hinzu. |

## Häufig gestellte Fragen

**F: Kann ich GroupDocs.Search in einer cloud‑basierten Java‑Anwendung verwenden?**  
A: Ja. Die Bibliothek funktioniert mit jeder Java‑Runtime, und Sie können `basePath` auf einen netzwerkgemounteten Ordner oder Cloud‑Speicher, der lokal gemountet ist, verweisen.

**F: Wie aktualisiere ich den Index, wenn sich eine Datei ändert?**  
A: Abonnieren Sie Knoten‑Events (siehe Feature 3) und rufen Sie `addFiles` oder `addDirectories` erneut für die geänderten Pfade auf.

**F: Gibt es ein Limit für die Anzahl der Knoten, die ich bereitstellen kann?**  
A: Praktisch wird das Limit durch Ihre Hardware und Netzwerkbandbreite definiert. Die API selbst legt keine feste Obergrenze fest.

**F: Muss ich Knoten nach dem Hinzufügen neuer Dateien neu starten?**  
A: Nein. Das Hinzufügen von Dateien löst die Indexierung automatisch aus; Sie müssen nur committen, wenn Sie den Vorgang verzögern.

**F: Welche Dokumentformate werden standardmäßig unterstützt?**  
A: PDFs, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML und viele Bildtypen. Siehe die offizielle Dokumentation für die vollständige Liste.

---

**Zuletzt aktualisiert:** 2025-12-26  
**Getestet mit:** GroupDocs.Search für Java 25.4  
**Autor:** GroupDocs