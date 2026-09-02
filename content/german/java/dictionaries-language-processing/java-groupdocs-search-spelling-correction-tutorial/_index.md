---
date: '2026-09-02'
description: Erfahren Sie, wie Sie mit GroupDocs.Search einen Suchindex in Java erstellen
  und die Rechtschreibkorrektur aktivieren. Befolgen Sie Schritt‑für‑Schritt‑Anleitungen,
  um Dokumente hinzuzufügen, max mistake count zu konfigurieren und die search accuracy
  zu verbessern.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: Erfahren Sie, wie Sie mit GroupDocs.Search einen Suchindex in Java
  erstellen und die Rechtschreibkorrektur aktivieren. Befolgen Sie Schritt‑für‑Schritt‑Anleitungen,
  um Dokumente hinzuzufügen, max mistake count zu konfigurieren und die search accuracy
  zu verbessern.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: Wie man einen Suchindex in Java erstellt und die Rechtschreibkorrektur aktiviert
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: Wie man einen Suchindex in Java erstellt und die Rechtschreibkorrektur aktiviert
type: docs
url: /de/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Wie man einen Suchindex in Java erstellt und Rechtschreibprüfung aktiviert

In modernen Java‑Anwendungen ist die Bereitstellung genauer Suchergebnisse ein unverzichtbares Merkmal. Dieses Tutorial zeigt **wie man einen Suchindex in Java erstellt** und die Rechtschreibkorrektur mit GroupDocs.Search aktiviert, sodass Benutzer relevante Treffer erhalten, selbst wenn sie Anfragen falsch tippen. Sie sehen, wie Sie die Bibliothek einrichten, Dokumente hinzufügen, die maximale Fehleranzahl konfigurieren und eine tipptolerante Suche durchführen – alles ohne eine einzige Zeile zusätzlicher Konfigurations‑Code.

## Schnelle Antworten
- **Was bewirkt „enable spelling“?** Es aktiviert den integrierten Rechtschreibprüfer, der falsch geschriebene Begriffe während einer Suche in ihre nächstgelegenen korrekten Formen umschreibt.  
- **Welche Bibliothek stellt diese Funktion bereit?** GroupDocs.Search für Java.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion reicht für die Evaluierung; für den Produktionseinsatz ist eine Voll‑Lizenz erforderlich.  
- **Kann ich die Toleranz steuern?** Ja – verwenden Sie `setMaxMistakeCount`, um festzulegen, wie viele Tippfehler pro Abfrage erlaubt sind.  
- **Ist es für große Indizes geeignet?** Absolut – die Engine verarbeitet Indizes mit Millionen von Datensätzen und hält die Abfrage‑Latenz unter 100 ms auf typischer Server‑Hardware.

## Was ist GroupDocs.Search?
GroupDocs.Search ist eine Java‑Bibliothek, die schnelles Volltext‑Indexieren und erweiterte Suchfunktionen, einschließlich integrierter Rechtschreibkorrektur, bereitstellt. Sie unterstützt mehr als 50 Eingabeformate und kann mehrseitige Dokumente verarbeiten, ohne die gesamte Datei in den Speicher zu laden.

## Warum Rechtschreibkorrektur in Java‑Anwendungen aktivieren?
- **Steigert die Benutzerzufriedenheit** – Besucher erhalten korrekte Ergebnisse selbst bei unvollständiger Eingabe.  
- **Reduziert Absprungraten** – genaue Treffer halten Benutzer länger auf der Seite.  
- **Funktioniert in allen Bereichen** – von Bibliothekskatalogen bis zu E‑Commerce‑Produktsuchen verbessert die Rechtschreibkorrektur überall die Relevanz.

## Voraussetzungen
- Java Development Kit (JDK) installiert.  
- Grundkenntnisse in Java und Maven.  
- Verständnis von Indexierungskonzepten.  
- Eine GroupDocs.Search‑Testversion oder ein Lizenzschlüssel.

### Einrichtung von GroupDocs.Search für Java
Integrieren Sie die Bibliothek in Ihr Maven‑Projekt.

**Maven‑Einrichtung**  
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

**Direkter Download**  
Alternativ können Sie die neueste Version von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunterladen.

### Lizenzbeschaffung
Erhalten Sie eine kostenlose Testlizenz für die Evaluierung. Für den Produktionseinsatz kaufen Sie eine Voll‑Lizenz oder fordern Sie einen temporären Schlüssel von der offiziellen Website an.

## Wie erstelle ich einen Suchindex in Java?
`SearchIndex` ist die Hauptklasse, die einen auf der Festplatte gespeicherten durchsuchbaren Index repräsentiert.  
Erstellen Sie eine `SearchIndex`‑Instanz, die auf einen Ordner auf der Festplatte zeigt, und fügen Sie dann Dokumente aus einem Quellverzeichnis hinzu. Die Engine baut einen invertierten Index auf, der schnelle Look‑ups ermöglicht. Sie können `index.add()` für jede Datei aufrufen; die Bibliothek extrahiert den Text automatisch basierend auf dem Dateityp.

## Wie kann ich die Rechtschreibkorrektur aktivieren?
`getSpellingOptions()` gibt das Rechtschreib‑Konfigurationsobjekt für den Index zurück, sodass Sie die Rechtschreibprüfung aktivieren oder anpassen können.  
Aktivieren Sie die Rechtschreibung, indem Sie `index.getSpellingOptions().setEnabled(true)` aufrufen. Dadurch wird die Engine angewiesen, Abfragebegriffe zu analysieren und korrigierte Alternativen vorzuschlagen, wenn Unstimmigkeiten erkannt werden. Die Funktion funktioniert sofort für alle vom Index unterstützten Sprachen.

## Was ist die Einstellung für die maximale Fehleranzahl?
`setMaxMistakeCount` konfiguriert die maximale Anzahl von Zeichenänderungen, die der Rechtschreibprüfer pro Begriff toleriert.  
`setMaxMistakeCount(int)` definiert die maximale Anzahl von Zeichenänderungen (Einfügungen, Löschungen, Ersetzungen), die der Rechtschreibprüfer pro Begriff toleriert. Wird sie auf **2** gesetzt, kann die Engine gängige Tippfehler mit zwei Zeichen korrigieren, ohne zu aggressive Korrekturen vorzunehmen, die zu irrelevanten Ergebnissen führen könnten.

## Wie führt man eine rechtschreibkorrigierte Suche durch
`search()` führt eine Abfrage gegen den Index aus und gibt ein `SearchResult`‑Objekt zurück, das Treffer und etwaige korrigierte Begriffe enthält.  
Führen Sie eine Suchabfrage mit der Methode `search()` aus. Enthält die Abfrage falsch geschriebene Wörter, gibt die Engine ein `SearchResult` zurück, das die korrigierten Begriffe und eine Liste der relevantesten Dokumente enthält. Sie können dem Benutzer sowohl die ursprüngliche Abfrage als auch die korrigierte Version anzeigen, um Transparenz zu gewährleisten.  
`SearchResult` enthält die Liste der passenden Dokumente und Informationen zu den Abfragekorrekturen.

## Praktische Anwendungen
1. **Bibliothekssysteme** – korrigieren automatisch falsch geschriebene Buchtitel oder Autorennamen.  
2. **E‑Commerce‑Plattformen** – korrigieren Tippfehler in Produktnamen, um die Konversionsrate zu erhöhen.  
3. **Content‑Management** – unterstützt Redakteure dabei, Artikel auch bei unvollständigen Schlüsselwörtern zu finden.

## Leistungsüberlegungen
- **Den Index aktuell halten** – neue oder geänderte Dateien regelmäßig neu indexieren.  
- **JVM‑Speichereinstellungen anpassen** – ausreichend Heap für große Indizes reservieren (z. B. `-Xmx4g`).  
- **Ressourcennutzung überwachen** – Garbage‑Collector‑Parameter anpassen, wenn Sie Pausen beim Mass‑Indexieren bemerken.

## Häufige Probleme & Fehlersuche
| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Keine Ergebnisse nach Aktivierung der Rechtschreibung | Der Pfad zum Indexordner ist falsch oder leer | Stellen Sie sicher, dass `indexFolder` auf einen gültigen Index zeigt und dass `index.add()` erfolgreich war |
| Rechtschreibprüfung korrigiert offensichtliche Tippfehler nicht | `setMaxMistakeCount` ist zu niedrig eingestellt | Erhöhen Sie den Wert auf 2 oder 3 für eine tolerantere Korrektur |
| Anwendung stürzt bei großen Dokumentenmengen ab | Unzureichender JVM‑Heap | Erhöhen Sie die `-Xmx`‑Option (z. B. `-Xmx4g`) |

## Häufig gestellte Fragen

**Q: Was ist GroupDocs.Search?**  
A: GroupDocs.Search ist eine Java‑Bibliothek, die schnelles Indexieren, erweiterte Abfragefunktionen und integrierte Rechtschreibkorrektur für jede Java‑Anwendung bereitstellt.

**Q: Wie erhalte ich eine Lizenz für GroupDocs.Search?**  
A: Besuchen Sie die offizielle Website, um eine kostenlose Testversion herunterzuladen oder eine Voll‑Lizenz zu erwerben; ein temporärer Schlüssel ist ebenfalls für kurzfristige Tests verfügbar.

**Q: Kann ich GroupDocs.Search in andere Java‑Frameworks integrieren?**  
A: Ja, es funktioniert nahtlos mit Spring, Jakarta EE und jeder Standard‑Java‑Anwendung.

**Q: Was sind häufige Probleme beim Einrichten eines Index?**  
A: Falsche Ordnerpfade, fehlende Dateiberechtigungen oder fehlende Maven‑Abhängigkeiten sind die typischen Ursachen.

**Q: Wie verbessert die Rechtschreibkorrektur die Suchergebnisse?**  
A: Sie schreibt falsch geschriebene Anfragen automatisch in die nächstgelegenen korrekten Begriffe um, liefert relevantere Treffer und reduziert die Frustration der Benutzer.

## Zusätzliche Ressourcen
- [Dokumentation](https://docs.groupdocs.com/search/java/)
- [API‑Referenz](https://reference.groupdocs.com/search/java)
- [Download](https://releases.groupdocs.com/search/java/)
- [GitHub‑Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Kostenloses Support‑Forum](https://forum.groupdocs.com/c/search/10)
- [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)

---

**Zuletzt aktualisiert:** 2026-09-02  
**Getestet mit:** GroupDocs.Search 25.4  
**Autor:** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## Verwandte Tutorials

- [Wie man einen Dokumentenindex erstellt und Dokumente mit der GroupDocs.Search‑API für Java hinzufügt](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Sprachverarbeitung Java – Synonymwörterbuch mit GroupDocs.Search erstellen](/search/java/dictionaries-language-processing/)
- [Stoppwörter in der Suche: Dokumente zum Index mit GroupDocs.Search Java hinzufügen](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)