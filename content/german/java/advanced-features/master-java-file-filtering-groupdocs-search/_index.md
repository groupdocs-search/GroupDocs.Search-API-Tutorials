---
date: '2026-09-06'
description: Erfahren Sie, wie Sie Dateierweiterungen java mit GroupDocs.Search für
  Java filtern, einschließlich logischer AND-, OR- und NOT-Operatoren, Datumsbereichsfilter
  und Pfadfilter.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: Dateierweiterungen java mit GroupDocs.Search filtern. Erfahren Sie,
  wie Sie Erweiterungs-, Datumsbereichs- und Pfadfilter mit logischen Operatoren in
  Java kombinieren.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: Dateierweiterungen java mit GroupDocs.Search filtern – Komplettanleitung
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: Wie man Dateierweiterungen java mit GroupDocs.Search filtert
type: docs
url: /de/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Filterdateierweiterungen java mit GroupDocs.Search

In diesem umfassenden Tutorial lernen Sie, wie Sie **filter file extensions java** beim Indizieren von Dokumenten mit GroupDocs.Search vorgehen. Am Ende des Leitfadens können Sie nur die benötigten Dateitypen einbeziehen, unerwünschte Formate ausschließen und diese Regeln mit Datums‑ und Pfadfiltern unter Verwendung der logischen Operatoren AND, OR und NOT kombinieren. Dieser Ansatz hält Ihren Index schlank, beschleunigt die Suche und hilft Ihnen, die Richtlinien zur Datenverarbeitung einzuhalten.

## Schnelle Antworten
- **Was ist der java file extension filter?** Es ist eine Regel, die GroupDocs.Search mitteilt, welche Dateierweiterungen während des Indexierens ein- oder ausgeschlossen werden sollen.  
- **Welche Bibliothek stellt diese Funktion bereit?** GroupDocs.Search für Java.  
- **Brauche ich eine Lizenz?** Eine kostenlose Testversion ist für die Evaluierung ausreichend; für den Produktionseinsatz ist eine Voll‑Lizenz erforderlich.  
- **Kann ich Filter kombinieren?** Ja – Sie können Erweiterungs‑, Datums‑, Größen‑ und Pfadfilter mit AND‑, OR‑ und NOT‑Logik verketten.  
- **Ist es Maven‑kompatibel?** Absolut – fügen Sie die GroupDocs.Search‑Abhängigkeit zu Ihrer `pom.xml` hinzu.

## Was ist ein java file extension filter?
Ein **java file extension filter** ist ein Regelwerk, das die Erweiterung jeder Datei prüft, bevor sie an die Indexierungs‑Engine übergeben wird. Durch Angabe von Erweiterungen wie `.txt`, `.pdf` oder `.epub` können Sie **include files by extension** oder **exclude files by extension** verwenden, um Ihren Index fokussiert und die Suchergebnisse relevant zu halten.

## Warum Dateierweiterungsfilterung mit GroupDocs.Search verwenden?
Die Filterung nach Dateierweiterungen verbessert die Indexierungseffizienz, indem irrelevante Formate ausgeschlossen werden, reduziert den Speicherbedarf und unterstützt die Einhaltung von Compliance‑Regeln, indem unerwünschte Inhalte nicht in den Index gelangen. Außerdem ermöglicht sie schnellere Abfrageantworten, da die Suchmaschine einen kleineren, relevanteren Datensatz verarbeitet.

- **Performance:** Das Überspringen unerwünschter Dateien reduziert I/O und beschleunigt die Indexierung um bis zu 40 % bei großen Repositorien.  
- **Speicherersparnis:** Nur relevante Dokumente werden im Index gespeichert, wodurch die Festplattennutzung im Durchschnitt um 30 % reduziert wird.  
- **Compliance:** Verhindert das versehentliche Indexieren vertraulicher oder nicht unterstützter Dateitypen.  
- **Flexibilität:** Kombinieren Sie mit **date range filter java**-Funktionen, um Dateien zu adressieren, die in bestimmten Zeiträumen erstellt oder geändert wurden.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:

### Erforderliche Bibliotheken und Abhängigkeiten
- **GroupDocs.Search for Java** – Version 25.4 oder neuer (unterstützt über 60 Eingabeformate).  
- **Java Development Kit (JDK)** – jede kompatible Version (8 oder neuer).

### Umgebung einrichten
- Integrierte Entwicklungsumgebung (IDE): IntelliJ IDEA, Eclipse oder jede Maven‑kompatible IDE.

### Wissensvoraussetzungen
- Grundkenntnisse in Java-Programmierung.  
- Vertrautheit mit Datei‑I/O in Java.  
- Verständnis von regulären Ausdrücken und Datum‑Zeit‑Verarbeitung.

## Einrichtung von GroupDocs.Search für Java
Um GroupDocs.Search zu verwenden, müssen Sie es als Abhängigkeit in Ihr Projekt einbinden.

### Maven‑Konfiguration
Fügen Sie die folgende Repository‑ und Abhängigkeitskonfiguration zu Ihrer `pom.xml`‑Datei hinzu:

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
Alternativ können Sie die neueste Version direkt von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunterladen.

#### Lizenzbeschaffung
1. **Free trial** – Erkunden Sie die Funktionen kostenlos.  
2. **Temporary license** – Erhalten Sie die volle Funktionalität für einen begrenzten Zeitraum.  
3. **Purchase** – Erwerben Sie eine permanente Lizenz für den Produktionseinsatz.

### Grundlegende Initialisierung und Einrichtung
Sobald die Bibliothek hinzugefügt ist, initialisieren Sie Ihre Indexierungsumgebung. Die Klasse `IndexSettings` enthält alle Konfigurationsoptionen, einschließlich Filter.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Implementierungsanleitung
Im Folgenden gehen wir auf jeden Filtertyp ein, erklären **warum er wichtig ist** und geben Schritt‑für‑Schritt‑Anleitungen, die Sie in Ihr Projekt übernehmen können.

### Filterung von Dateierweiterungen
Filtern Sie Dateien während der Indexierung nach ihren Erweiterungen. Das ist ideal, wenn Sie nur e‑Books (`.fb2`, `.epub`) und Klartextdateien (`.txt`) verarbeiten möchten.

#### Überblick
`DocumentFilter.createFileExtension` erstellt eine Whitelist von Erweiterungen.

#### Implementierungsschritte
1. **Create filter** – Definieren Sie die Erweiterungen, die Sie behalten möchten.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize index and add documents** – Wenden Sie den Filter beim Erstellen der `IndexSettings` an.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logischer NOT‑Filter
Schließen Sie bestimmte Erweiterungen aus, wie Webseiten und PDFs, wenn sie für Ihr Suchszenario nicht benötigt werden.

#### Implementierungsschritte
1. **Create exclusion filter** – Geben Sie die zu verwerfenden Erweiterungen an.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to index settings** – Kombinieren Sie den NOT‑Filter mit anderen Regeln.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add documents** – Nur Dateien, die den kombinierten Filter bestehen, werden indexiert.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logischer AND‑Filter
Kombinieren Sie mehrere Bedingungen – Erstellungsdatum, Erweiterung und Dateigröße – sodass **nur Dateien, die alle Kriterien erfüllen**, indexiert werden.

#### Überblick
`DocumentFilter.createAnd` fasst mehrere Filter zu einer einzigen Regel zusammen.

#### Implementierungsschritte
1. **Define filters** – Erstellen Sie einzelne Filter für jede Bedingung.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine filters** – Verwenden Sie den AND‑Operator, um alle Bedingungen zu verlangen.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index documents** – Geben Sie den kombinierten Filter an die Indexierungspipeline weiter.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logischer OR‑Filter
Schließen Sie Dateien ein, die **irgendeine** der angegebenen Bedingungen erfüllen – nützlich, wenn Sie sowohl kleine Textdateien als auch größere Nicht‑Text‑Dateien erfassen möchten.

#### Implementierungsschritte
1. **Define filters** – Erstellen Sie separate Filter für jede alternative Bedingung.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine filters with logical conditions** – Verwenden Sie den OR‑Operator.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR filter** – Hängen Sie den kombinierten Filter an die Indexkonfiguration an.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Erstellungszeit‑Filter
Zielen Sie auf Dateien, die innerhalb eines bestimmten Zeitraums erstellt wurden – ein klassisches **date range filter java**‑Szenario.

#### Implementierungsschritte
1. **Define date‑range filter** – Geben Sie Start‑ und Enddatum an.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index documents** – Nur Dateien, deren Erstellungszeitstempel innerhalb des Bereichs liegen, werden indexiert.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Änderungszeit‑Filter
Schließen Sie Dateien aus, die nach einem bestimmten Stichtag geändert wurden.

#### Implementierungsschritte
1. **Define filter** – Legen Sie den maximalen Änderungszeitstempel fest.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index documents** – Dateien, die neuer als der Stichtag sind, werden ignoriert.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Dateipfad‑Filterung
Beschränken Sie die Indexierung auf Dateien in bestimmten Ordnern oder solche, die einem Muster entsprechen – ideal für **include files by extension** innerhalb einer bestimmten Verzeichnisstruktur.

#### Implementierungsschritte
1. **Define file‑path filter** – Verwenden Sie Glob‑ oder Regex‑Muster, um Verzeichnisse zu matchen.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize index and add documents** – Wenden Sie den Pfadfilter zusammen mit anderen Regeln an.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Häufige Fallstricke & Tipps

- **Mischen Sie niemals absolute und relative Pfade** in derselben Filterkonfiguration – das kann zu unerwarteten Ausschlüssen führen.  
- **Setzen Sie die `IndexSettings` zurück**, wenn Sie Filtersets wechseln; sonst können vorherige Filter bestehen bleiben.  
- **Kombinieren Sie eine maximale Länge mit einem Erweiterungsfilter** für große Sammlungen, um den Speicherverbrauch gering zu halten.  
- LoggingOptions steuert die Protokollierungskonfiguration für GroupDocs.Search.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) um zu sehen, warum eine Datei abgelehnt wurde.  

## Häufig gestellte Fragen

**Q: Kann ich die Filterkriterien ändern, nachdem der Index erstellt wurde?**  
A: Ja. Erstellen Sie den Index mit einem neuen `DocumentFilter` neu oder verwenden Sie inkrementelles Indexieren mit aktualisierten Einstellungen.

**Q: Funktioniert der java file extension filter für komprimierte Archive (z. B. ZIP)?**  
A: GroupDocs.Search kann unterstützte Archivformate indexieren, jedoch gilt der Erweiterungsfilter für das Archiv selbst, nicht für die inneren Dateien. Verwenden Sie verschachtelte Filter für eine tiefere Kontrolle.

**Q: Wie kann ich debuggen, warum eine bestimmte Datei ausgeschlossen wurde?**  
A: Aktivieren Sie das Logging der Bibliothek (`LoggingOptions.setEnabled(true)`) und prüfen Sie das Protokoll – es gibt an, welcher Filter jede Datei abgelehnt hat.

**Q: Ist es möglich, den java file extension filter mit benutzerdefinierten Regex‑Filtern zu kombinieren?**  
A: Absolut. Verpacken Sie einen Regex‑Filter innerhalb von `DocumentFilter.createAnd()` zusammen mit dem Erweiterungsfilter.

**Q: Welche Auswirkungen hat das Hinzufügen vieler Filter auf die Performance?**  
A: Jeder Filter verursacht einen geringen Overhead während der Indexierung, aber die Reduzierung der indexierten Daten überwiegt in der Regel die Kosten. Testen Sie mit einer repräsentativen Stichprobe, um das optimale Gleichgewicht zu finden.

**Zuletzt aktualisiert:** 2026-09-06  
**Getestet mit:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Benutzerdefiniertes Datumsformat Java | Datum‑Bereichsuche mit GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: Master Boolean Searches mit GroupDocs.Search für Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Suchleistung optimieren mit fortgeschrittenen Indexierungstechniken in GroupDocs.Search für Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)

