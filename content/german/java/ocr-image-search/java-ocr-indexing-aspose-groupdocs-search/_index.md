---
date: '2026-01-11'
description: Erfahren Sie, wie Sie die OCR‑Indexierung von GroupDocs für Java mit
  Aspose.OCR nutzen, um leistungsstarke Dokumentensuchfunktionen für PDFs, Bilder
  und gescannte Dateien zu ermöglichen.
keywords:
- Java OCR indexing
- document searchability
- OCR with GroupDocs
title: Wie man GroupDocs für Java OCR-Indexierung mit Aspose verwendet
type: docs
url: /de/java/ocr-image-search/java-ocr-indexing-aspose-groupdocs-search/
weight: 1
---

# So verwenden Sie GroupDocs für Java OCR-Indexierung mit Aspose

In diesem Leitfaden erfahren Sie **wie Sie GroupDocs** verwenden, um OCR‑gestützte Suche zu Ihren Java‑Anwendungen hinzuzufügen. Durch die Kombination von GroupDocs.Search mit Aspose.OCR können Sie bildbasierte Inhalte in durchsuchbaren Text umwandeln, wodurch Dokumentenmanagement‑Systeme deutlich nützlicher werden. Wir führen Sie durch Einrichtung, Indexierung, Suche und benutzerdefinierte OCR‑Integration, alles mit klaren, Schritt‑für‑Schritt‑Beispielen.

## Schnelle Antworten
- **Welche Bibliothek bietet OCR‑Indexierung?** GroupDocs.Search in Kombination mit Aspose.OCR.  
- **Welche Java‑Version wird benötigt?** JDK 8 oder höher.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion ist verfügbar; für den Produktionseinsatz ist eine kostenpflichtige Lizenz erforderlich.  
- **Kann ich sowohl separate als auch eingebettete Bilder indexieren?** Ja, aktivieren Sie beide Optionen in `IndexingOptions`.  
- **Wird Multi‑Threading unterstützt?** Ja, Sie können die Indexierung für große Datenmengen parallelisieren.

## Was ist OCR‑Indexierung mit GroupDocs?
OCR‑Indexierung extrahiert Text aus Bildern (einschließlich gescannter PDFs) und speichert ihn in einem durchsuchbaren Index. GroupDocs.Search übernimmt die Indexierung und die Ausführung von Abfragen, während Aspose.OCR die eigentliche Zeichenerkennung durchführt.

## Warum GroupDocs für Java OCR‑Indexierung verwenden?
- **Hohe Genauigkeit** dank der fortschrittlichen OCR‑Engine von Aspose.  
- **Nahtlose Java‑Integration** über Maven oder direkte JARs.  
- **Flexible Konfiguration** für separate oder eingebettete Bilder.  
- **Skalierbare Leistung** mit Multi‑Threading und Speicheroptimierungen.

## Voraussetzungen
- **GroupDocs.Search** ≥ 25.4  
- **Aspose.OCR** (neueste Version)  
- JDK 8+ und eine IDE (IntelliJ, Eclipse, NetBeans)  
- Grundlegende Java‑Kenntnisse; Maven ist hilfreich, aber nicht zwingend erforderlich

## Einrichtung von GroupDocs.Search für Java
### Verwendung von Maven
Add the repository and dependency to your `pom.xml`:

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
Alternativ können Sie die neueste Version von GroupDocs.Search für Java von [GroupDocs releases](https://releases.groupdocs.com/search/java/) herunterladen.

### Lizenzbeschaffung
- **Kostenlose Testversion** – alle Funktionen ohne Kosten testen.  
- **Temporäre Lizenz** – erweiterter Testzeitraum.  
- **Kauf** – erforderlich für den Produktionseinsatz.

### Grundlegende Initialisierung und Einrichtung
Create an index folder and initialize the `Index` object:

```java
import com.groupdocs.search.Index;
// Specify the directory where the index will be stored.
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
// Create an instance of Index class at the specified location.
Index index = new Index(indexFolder);
```

## So verwenden Sie GroupDocs für OCR‑Indexierung
### Erstellen eines Index
First, set up the folder that will hold the index files:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
Index index = new Index(indexFolder);
```

### OCR‑Indexierungsoptionen festlegen
Enable OCR for both separate and embedded images, and plug in a custom OCR connector:

```java
import com.groupdocs.search.options.IndexingOptions;
IndexingOptions options = new IndexingOptions();
options.getOcrIndexingOptions().setEnabledForSeparateImages(true);
options.getOcrIndexingOptions().setEnabledForEmbeddedImages(true);
// Set a custom OCR connector.
options.getOcrIndexingOptions().setOcrConnector(new OcrConnector());
```

### Dokumente indexieren
Add your source documents (PDFs, Word files, images, etc.) to the index:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder, options);
```

### Suche in einem Index
Run a search query against the indexed content:

```java
import com.groupdocs.search.results.SearchResult;
String query = "water";
SearchResult result = index.search(query);
```

### Implementierung eines OCR‑Connectors
Use Aspose.OCR to recognize text from images. Implement the `IOcrConnector` interface as shown:

```java
import com.groupdocs.search.options.IOcrConnector;
import com.groupdocs.search.options.OcrContext;
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import com.aspose.ocr.AsposeOCR;

public class OcrConnector implements IOcrConnector {
    @Override
    public final String recognize(OcrContext context) {
        if (null == context.getImageLocation()) {
            throw new RuntimeException("The image type is not supported: " + context.getImageLocation());
        }
        
        BufferedImage image = ImageIO.read(context.getImageLocation().toFile());
        AsposeOCR api = new AsposeOCR();
        String text = api.RecognizePage(image);
        return text;
    }
}
```

## Praktische Anwendungen
1. **Dokumentenmanagement‑Systeme** – schnelle Abrufung von Dokumenten mit gescannten Bildern.  
2. **Archivabfrage** – historische Aufzeichnungen in umfangreichen Archiven finden.  
3. **Rechtsdokumenten‑Analyse** – Verträge und Beweismaterialien durchsuchen, die gescannte Unterschriften oder Diagramme enthalten.  
4. **Suche in medizinischen Aufzeichnungen** – Patientenformulare, Laborergebnisse und Röntgen‑Anmerkungen indexieren.

## Leistungsüberlegungen
- **Indexgröße** – unnötige Metadaten ausschließen, um den Index schlank zu halten.  
- **Multi‑Threading** – große Stapel parallel verarbeiten, um die Indexierung zu beschleunigen.  
- **Speichermanagement** – den JVM‑Heap überwachen, wenn hochauflösende Bilder verarbeitet werden.

## Häufige Probleme und Lösungen
- **Lizenzfehler** – stellen Sie sicher, dass die korrekte Lizenzdatei im Arbeitsverzeichnis der Anwendung abgelegt ist.  
- **Fehlende Bilder** – prüfen Sie, ob Bildpfade zugänglich sind und unterstützte Formate (PNG, JPEG, BMP) vorliegen.  
- **Out‑Of‑Memory** – erhöhen Sie den JVM‑Heap (`-Xmx`) oder verarbeiten Sie Dokumente in kleineren Stapeln.

## Häufig gestellte Fragen
**Q: Wie löse ich Lizenzprobleme mit GroupDocs.Search?**  
A: Holen Sie sich eine temporäre Lizenz von der [GroupDocs-Website](https://purchase.groupdocs.com/temporary-license/), um alle Funktionen freizuschalten.

**Q: Was ist der beste Weg, um die Indexierung großer Dokumente zu handhaben?**  
A: Nutzen Sie Multi‑Threading und Batch‑Verarbeitung, um die Leistung zu verbessern und den Speicherbedarf zu reduzieren.

**Q: Kann ich OCR‑Einstellungen in GroupDocs.Search weiter anpassen?**  
A: Ja, `IndexingOptions` ermöglicht das Feintuning des OCR‑Verhaltens, z. B. die Sprachauswahl und Bildvorverarbeitung.

**Q: Was sind häufige Tipps zur Fehlerbehebung bei der Verwendung von GroupDocs.Search?**  
A: Überprüfen Sie die Verzeichnis‑Pfade, stellen Sie sicher, dass alle Abhängigkeiten vorhanden sind, und prüfen Sie die Protokollausgabe auf fehlende Dateien.

**Q: Wie kann ich Aspose.OCR in meine bestehende Java‑Anwendung integrieren?**  
A: Implementieren Sie das `IOcrConnector`‑Interface wie oben gezeigt und stellen Sie sicher, dass Sie die Bildeingabe korrekt verarbeiten.

## Ressourcen
- [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Zuletzt aktualisiert:** 2026-01-11  
**Getestet mit:** GroupDocs.Search 25.4, Aspose.OCR neueste Version  
**Autor:** GroupDocs