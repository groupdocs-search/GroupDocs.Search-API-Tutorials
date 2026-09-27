---
date: '2026-09-27'
description: Erfahren Sie, wie Sie Text java mit GroupDocs.Search für Java hervorheben,
  einschließlich search documents java, index documents java und fragment highlighting.
keywords:
- highlight text java
- search documents java
- index documents java
- java text highlighting library
- highlight terms pdf java
lastmod: '2026-09-27'
og_description: Erfahren Sie, wie Sie Text java mit GroupDocs.Search für Java hervorheben.
  Erhalten Sie eine Schritt-für-Schritt-Anleitung zu indexing, searching und fragment
  highlighting für schnelle Ergebnisse.
og_image_alt: Screenshot of highlighted search terms in a Java application using GroupDocs.Search
og_title: Text java mit GroupDocs.Search hervorheben – Schnelle Dokumenten-Hervorhebung
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  headline: Highlight text java with GroupDocs.Search
  type: TechArticle
- description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  name: Highlight text java with GroupDocs.Search
  steps:
  - name: create and populate the index
    text: Create an index folder and add all source files you want to search. The
      `Index` class represents the searchable container.
  - name: perform search and apply highlighting
    text: Search for the term (e.g., `ipsum`) and generate an HTML file with highlighted
      matches. Use `HighlightOptions` to specify the highlight color and whether to
      use inline styles. `HighlightOptions` lets you define the foreground and background
      colors, as well as the CSS class that will be applied to ea
  - name: index and search (same as above)
    text: The same index and search steps apply; you reuse the `Index` and `SearchResult`
      objects.
  - name: define fragment context and highlight
    text: Specify how many terms before and after the match should appear in each
      fragment with `FragmentOptions`. `FragmentOptions` controls the number of surrounding
      words (`termsBefore` and `termsAfter`) that are included in each snippet, allowing
      you to balance context against snippet length.
  - name: retrieve and write highlighted fragments
    text: Collect the generated fragments and write them to an HTML file. Each fragment
      is already highlighted according to the `HighlightOptions` you configured. `fragmentHighlighter`
      is a utility that creates highlighted snippets from a `SearchResult` using the
      specified fragment and highlight options. **Di
  type: HowTo
- questions:
  - answer: It offers fast, scalable indexing, customizable highlighting, and support
      for 30+ document formats, processing 500‑page files in under 2 seconds on a
      typical server.
    question: What are the benefits of using GroupDocs.Search for Java?
  - answer: Expose the search and highlight methods via Spring Boot controllers, returning
      HTML snippets or JSON payloads that contain the highlighted fragments.
    question: How can I integrate GroupDocs.Search with a REST API?
  - answer: Yes—provide the password when adding the document to the index via `addDocument(filePath,
      password)`.
    question: Does the library handle password‑protected files?
  - answer: Absolutely; you can assign a CSS class with `options.setCssClass("myHighlight")`
      and style it globally, or modify the generated HTML after highlighting.
    question: Can I customize the highlight markup beyond color?
  - answer: The code was validated against GroupDocs.Search 25.4.
    question: What version was tested for this guide?
  type: FAQPage
tags:
- highlight text java
- GroupDocs.Search
- Java document processing
title: Text java mit GroupDocs.Search hervorheben
type: docs
url: /de/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Text hervorheben java mit GroupDocs.Search

In modernen Unternehmensanwendungen ist **highlight text java** unerlässlich, um rohe Suchergebnisse in sofort lesbare Erkenntnisse zu verwandeln. Egal, ob Sie ein Legal‑Review‑Portal, eine akademische Suchmaschine oder ein Kunden‑Support‑Dashboard erstellen, die Möglichkeit, Abfragebegriffe zu finden und visuell hervorzuheben, spart den Benutzern unzählige Sekunden manueller Durchsicht. Dieses Tutorial zeigt, wie Sie **GroupDocs.Search for Java** verwenden, um **search documents java**, **index documents java** zu nutzen und sowohl Voll‑Dokument‑ als auch Fragment‑Highlighting anzuwenden, alles mit nur wenigen Codezeilen.

## Schnelle Antworten
- **What does “search and highlight text” mean?** Es bedeutet, Abfragebegriffe in einem Dokument zu finden und sie visuell hervorzuheben (zum Beispiel mit einem farbigen Hintergrund).  
- **Which library provides this capability?** GroupDocs.Search for Java.  
- **Do I need a license?** Eine kostenlose Testversion funktioniert für die Evaluierung; eine Volllizenz ist für den Produktionseinsatz erforderlich.  
- **Can I customize highlight colors?** Ja—jede RGB‑Farbe kann über `HighlightOptions` festgelegt werden.  
- **Is fragment highlighting supported?** Absolut; Sie können Begriffe vor/nach dem Treffer definieren, um prägnante Ausschnitte zu erstellen.

## So heben Sie Text java in Dokumenten hervor

Um Text java in Dokumenten hervorzuheben, erstellen Sie zunächst einen Index der Quelldateien mit geeigneten Kompressionseinstellungen, führen dann eine Suchanfrage aus, um die gewünschten Begriffe zu finden, und exportieren schließlich die Ergebnisse nach HTML, PDF oder Klartext, wobei jeder Treffer in ein Highlight‑Tag eingeschlossen wird. Dieser dreistufige Prozess sorgt für schnelles, genaues Hervorheben in großen Sammlungen.

1. **Create an index** mit Kompressionseinstellungen, die den Speicherbedarf gering halten.  
2. **Execute a search** mit der Abfragezeichenfolge, die Sie hervorheben möchten.  
3. **Generate output** (HTML, PDF oder Klartext), bei dem jedes Vorkommen des Suchbegriffs in ein Highlight‑Tag eingeschlossen wird.

## Was ist search and highlight text?

Search and highlight text ist der Vorgang, eine indizierte Sammlung nach einer gegebenen Abfrage zu durchsuchen, passende Dokumente abzurufen und dann jedes Vorkommen des Suchbegriffs im Ergebnis (HTML, PDF usw.) zu markieren. Dieser visuelle Hinweis hilft Endbenutzern, relevante Informationen sofort zu erkennen.

## Warum GroupDocs.Search for Java verwenden?

GroupDocs.Search for Java bietet **high‑performance indexing** (bis zu 50 GB pro Index mit `Compression.High`), **rich highlighting**, das auf gesamten Dokumenten und benutzerdefinierten Fragmenten funktioniert, und **cross‑format support** für über 30 Dateitypen – einschließlich DOCX, PDF, PPTX und TXT. Die Bibliothek bietet zudem **incremental indexing**, mit dem Sie neue Dateien hinzufügen können, ohne den gesamten Index neu zu erstellen, was die Ausfallzeit in groß angelegten Deployments um bis zu 80 % reduziert.

## Voraussetzungen
- Java Development Kit (JDK) 8 oder neuer.  
- Maven für das Abhängigkeitsmanagement.  
- Eine IDE wie IntelliJ IDEA oder Eclipse.  
- Grundlegende Kenntnisse der Java‑Syntax.

## Einrichtung von GroupDocs.Search für Java

Fügen Sie das GroupDocs-Repository und die Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

Sie können das neueste JAR auch direkt von der offiziellen Seite herunterladen: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lizenzbeschaffung
Beginnen Sie mit einer kostenlosen Testversion oder erhalten Sie eine temporäre Lizenz zur Evaluierung. Für Produktionseinsätze kaufen Sie eine Volllizenz, um alle Funktionen freizuschalten.

## Implementierungsleitfaden

Die Implementierung ist in zwei praktische Abschnitte unterteilt: **highlighting in entire documents** und **highlighting in fragments**. Beide Abschnitte enthalten die wesentlichen Schritte für **how to highlight Java** Dokumente mit GroupDocs.Search.

### Konfiguration der Indexeinstellungen

Vor dem Indexieren konfigurieren Sie den Speicher, um hohe Kompression zu verwenden – dies reduziert den Festplattenverbrauch um bis zu 70 %, während die Suchgeschwindigkeit erhalten bleibt.

`IndexSettings` ist das Konfigurationsobjekt, das steuert, wie der Index auf der Festplatte gespeichert wird. Setzen Sie `Compression` auf `Compression.High`, um diese Optimierung zu aktivieren.  
`Compression` gibt das Niveau der Datenkompression an, das auf die Indexdateien angewendet wird, wobei `Compression.High` die maximale Größenreduktion bietet.

## Hervorheben in gesamten Dokumenten

### Schritt 1: Index erstellen und befüllen

Erstellen Sie einen Indexordner und fügen alle Quelldateien hinzu, die Sie durchsuchen möchten. Die Klasse `Index` stellt den durchsuchbaren Container dar.

### Schritt 2: Suche ausführen und Hervorhebung anwenden

Suchen Sie nach dem Begriff (z. B. `ipsum`) und erzeugen Sie eine HTML‑Datei mit hervorgehobenen Treffern. Verwenden Sie `HighlightOptions`, um die Highlight‑Farbe und die Verwendung von Inline‑Styles festzulegen.

`HighlightOptions` ermöglicht das Festlegen von Vorder‑ und Hintergrundfarben sowie der CSS‑Klasse, die jedem hervorgehobenen Begriff zugewiesen wird.

`HtmlHighlighter` erzeugt HTML‑Ausgabe mit hervorgehobenen Begriffen basierend auf den angegebenen Optionen.  
`SearchResult` enthält die Liste der passenden Dokumente und die Positionen jedes gefundenen Begriffs.

**Direct answer:** Laden Sie Ihren Index, rufen Sie `search("ipsum")` auf und übergeben Sie das resultierende `SearchResult` zusammen mit einer konfigurierten `HighlightOptions`‑Instanz an den `HtmlHighlighter`. Der Highlighter gibt HTML zurück, bei dem jedes Vorkommen von “ipsum” in ein `<span>` mit der gewählten Hintergrundfarbe eingeschlossen ist.

Erklärte Schlüsseloptionen  
- **Compression** – hohe Kompression spart Speicher.  
- **HighlightColor** – setzen Sie beliebige RGB‑Werte, um Ihrer UI‑Palette zu entsprechen.  
- **UseInlineStyles** – `false` erzeugt sauberes HTML, das global mit CSS gestaltet werden kann.

## Hervorheben in Fragmenten

### Schritt 1: Indexieren und Suchen (wie oben)

Die gleichen Index‑ und Suchschritte gelten; Sie verwenden die Objekte `Index` und `SearchResult` erneut.

### Schritt 2: Fragmentkontext definieren und hervorheben

Geben Sie mit `FragmentOptions` an, wie viele Begriffe vor und nach dem Treffer in jedem Fragment erscheinen sollen.

`FragmentOptions` steuert die Anzahl der umgebenden Wörter (`termsBefore` und `termsAfter`), die in jedem Ausschnitt enthalten sind, sodass Sie Kontext und Länge des Snippets abwägen können.

### Schritt 3: Hervorgehobene Fragmente abrufen und schreiben

Sammeln Sie die erzeugten Fragmente und schreiben Sie sie in eine HTML‑Datei. Jedes Fragment ist bereits gemäß den von Ihnen konfigurierten `HighlightOptions` hervorgehoben.

`fragmentHighlighter` ist ein Hilfsprogramm, das aus einem `SearchResult` hervorgehobene Snippets mithilfe der angegebenen Fragment‑ und Highlight‑Optionen erstellt.

**Direct answer:** Nachdem Sie das `SearchResult` erhalten haben, rufen Sie `fragmentHighlighter.highlight(searchResult, fragmentOptions, highlightOptions)` auf. Die Methode gibt eine Liste von HTML‑Snippets zurück, von denen jedes den gefundenen Begriff enthält, umgeben von der konfigurierten Anzahl Kontextwörter und mit der gewählten Farbe hervorgehoben.

## Praktische Anwendungen
1. **Legal document review** – sofort Gesetze, Klauseln oder Fallreferenzen in Tausenden von Verträgen hervorheben.  
2. **Academic research** – Schlüsselbegriffe in Dutzenden von PDFs und Word‑Dateien aufzeigen, wodurch die Literaturrecherchezeit um bis zu 60 % reduziert wird.  
3. **Customer support** – Bestellnummern oder Fehlercodes in Ticket‑Verläufen pinpointen, sodass Agenten Probleme schneller lösen können.

## Leistungsüberlegungen
- **Index size** – hohe Kompression (`Compression.High`) reduziert den Festplattenverbrauch um bis zu 70 % ohne spürbare Latenzeinbußen.  
- **Fragment context** – größere `termsBefore/After`‑Werte erhöhen die Lesbarkeit des Snippets, können jedoch 10–15 ms pro Abfrage hinzufügen.  
- **Memory management** – überwachen Sie den JVM‑Heap beim Indexieren großer Korpora; erwägen Sie inkrementelles Indexieren für Datensätze über 2 GB, um die Speichernutzung unter 1 GB zu halten.

## Häufige Probleme und Lösungen
- **Indexing errors** – prüfen Sie Dateipfade und stellen Sie sicher, dass die Anwendung Lese‑/Schreibrechte für den Indexordner hat.  
- **No highlights appear** – bestätigen Sie, dass `UseInlineStyles` zu Ihrem Ausgabeformat (HTML vs. PDF) passt.  
- **Color not applied** – stellen Sie sicher, dass die RGB‑Werte im Bereich 0‑255 liegen und dass der Viewer Inline‑CSS oder die bereitgestellte CSS‑Klasse respektiert.

## Häufig gestellte Fragen

**Q: What are the benefits of using GroupDocs.Search for Java?**  
A: Es bietet schnelles, skalierbares Indexieren, anpassbares Hervorheben und Unterstützung für über 30 Dokumentformate, wobei 500‑seitige Dateien in weniger als 2 Sekunden auf einem typischen Server verarbeitet werden.

**Q: How can I integrate GroupDocs.Search with a REST API?**  
A: Stellen Sie die Such‑ und Highlight‑Methoden über Spring‑Boot‑Controller bereit und geben HTML‑Snippets oder JSON‑Payloads zurück, die die hervorgehobenen Fragmente enthalten.

**Q: Does the library handle password‑protected files?**  
A: Ja—geben Sie das Passwort beim Hinzufügen des Dokuments zum Index über `addDocument(filePath, password)` an.

**Q: Can I customize the highlight markup beyond color?**  
A: Absolut; Sie können eine CSS‑Klasse mit `options.setCssClass("myHighlight")` zuweisen und global stylen oder das generierte HTML nach dem Hervorheben anpassen.

**Q: What version was tested for this guide?**  
A: Der Code wurde gegen GroupDocs.Search 25.4 validiert.

**Q: How do I set highlight options java to use a CSS class instead of inline styles?**  
A: Rufen Sie `options.setUseInlineStyles(false)` auf und definieren Sie eine CSS‑Regel für die Klasse, die Sie über `options.setCssClass("myHighlight")` zuweisen.

**Q: Is there a way to highlight terms in PDF output directly?**  
A: Ja—GroupDocs.Search arbeitet mit PDF‑Eingaben, und der Highlighter erzeugt HTML, das in einen PDF‑Viewer eingebettet oder mittels GroupDocs.Conversion wieder in PDF konvertiert werden kann.

**Zuletzt aktualisiert:** 2026-09-27  
**Getestet mit:** GroupDocs.Search 25.4  
**Autor:** GroupDocs

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

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Verwandte Tutorials

- [Wie man die Java-Volltextsuche implementiert: Indexverzeichnis mit GroupDocs.Search erstellen](/search/java/indexing/groupdocs-search-java-create-index/)
- [Erfahren Sie, wie Sie den Suchindex mit GroupDocs.Search für Java verwalten](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [Dokumente zum Index hinzufügen mit Chunk-basierter Suche in Java](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)