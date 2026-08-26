---
date: '2026-08-26'
description: Erfahren Sie, wie boolean operators Java es Ihnen ermöglichen, einen
  schnellen search index zu erstellen, content search Java durchzuführen und faceted
  queries mit GroupDocs.Search auszuführen.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: Erfahren Sie, wie boolean operators Java es Ihnen ermöglichen, einen
  schnellen search index zu erstellen, content search Java durchzuführen und faceted
  queries mit GroupDocs.Search auszuführen.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – search index erstellen und faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – search index erstellen & faceted search
type: docs
url: /de/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolesche Operatoren Java – Suchindex erstellen & facettierte Suche

Implementieren einer leistungsstarken **Sucherlebnis** in Java kann überwältigend wirken, besonders wenn Sie einen **Suchindex erstellen Java** benötigen, der **boolesche Operatoren Java** für facettierte und komplexe Abfragen unterstützt. In diesem Tutorial führen wir Sie durch die Einrichtung von **GroupDocs.Search for Java**, das Erstellen eines Index, das Hinzufügen von Dokumenten und das Erstellen sowohl einfacher facettierter Suchen als auch anspruchsvoller Multi‑Kriterien‑Abfragen, die boolesche Logik verwenden. Am Ende verstehen Sie, wie Sie **Inhaltssuche Java**, **Dateinamen‑Suche Java** und sogar **Index aktualisieren Java**‑Operationen nutzen können, um Ihre Daten aktuell zu halten.

## Schnelle Antworten
- **Was ist eine facettierte Suche?** Eine Möglichkeit, Ergebnisse nach vordefinierten Kategorien wie Dateityp oder Datum zu filtern.  
- **Wie erstelle ich einen Suchindex Java?** Initialisieren Sie ein `Index`‑Objekt, das auf einen Ordner zeigt, und fügen Sie Dokumente hinzu.  
- **Kann ich mehrere Kriterien mit booleschen Operatoren kombinieren?** Ja – verwenden Sie objektbasierte Abfragen oder boolesche Operatoren in einer Textabfrage.  
- **Brauche ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; eine kommerzielle Lizenz entfernt Beschränkungen.  
- **Welche IDE ist am besten geeignet?** Jede Java‑IDE (IntelliJ IDEA, Eclipse, NetBeans) funktioniert fine.

## Was bedeutet „Suchindex erstellen Java“?

Ein Suchindex Java zu erstellen bedeutet, eine festplattenbasierte Struktur zu konstruieren, die Dokumenttext und Metadaten speichert und eine sofortige Abrufung passender Dokumente über Abfragen ermöglicht. Der Index ordnet Begriffe Dokumenten‑IDs zu, unterstützt schnelle Lookups und kann inkrementell aktualisiert werden, wenn sich Dateien ändern, und bildet die Grundlage für leistungsstarke Suchfunktionen.

## Warum GroupDocs.Search für facettierte und komplexe Abfragen verwenden?

GroupDocs.Search für Java bietet integrierte Facettierung, Unterstützung für boolesche Abfragen und Hochleistungs‑Indexierung, die bis zu 10 Millionen Dokumente verarbeiten kann, während die Abfrage‑Latenz auf typischer Server‑Hardware unter 200 ms bleibt. Es stellt sofort einsatzbereite Feldfilter, eine umfangreiche Abfragesprache und reine Java‑Kompatibilität bereit, was es ideal für unternehmensweite Suchszenarien macht.

## Voraussetzungen

- **JDK 8 oder neuer** installiert und in Ihrer IDE konfiguriert.  
- **Maven** (oder Gradle) für die Abhängigkeitsverwaltung.  
- **GroupDocs.Search für Java** ≥ 25.4.  
- Grundlegende Kenntnisse der Java‑OOP‑Konzepte und der Maven‑Projektstruktur.

## Einrichtung von GroupDocs.Search für Java

### Maven‑Einrichtung
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
Alternativ können Sie das neueste JAR von der offiziellen Release‑Seite herunterladen:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Lizenzbeschaffung
Um die volle Funktionalität freizuschalten:

1. **Kostenlose Testversion** – ideal für Entwicklung und Tests.  
2. **Temporäre Evaluierungslizenz** – erweitert die Testlimits.  
3. **Kommerzielle Lizenz** – entfernt alle Beschränkungen für den Produktionseinsatz.

### Grundlegende Initialisierung und Einrichtung
Die Klasse `Index` ist die Kernkomponente, die einen auf der Festplatte gespeicherten durchsuchbaren Index darstellt. Das folgende Snippet zeigt, wie man einen **Suchindex erstellen Java** erzeugt, indem man die Klasse `Index` instanziiert:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

Mit dem bereitstehenden Index können wir zu realen facettierten und komplexen Abfragen übergehen.

## Wie man boolesche Operatoren Java verwendet – Einfache facettierte Suche

Laden Sie Ihren Index, fügen Sie Dokumente hinzu und führen Sie eine Feldabfrage aus; das Zwei‑Schritt‑Muster ermöglicht es, Facetten‑Zähler und gefilterte Ergebnisse in einem einzigen Aufruf abzurufen. Dieser Ansatz bietet Benutzern eine intuitive Möglichkeit, Ergebnisse nach Kategorien wie Dateityp, Autor oder benutzerdefinierten Metadaten einzugrenzen.

### Schritt 1: Index erstellen
Zuerst zeigen Sie den `Index` auf einen Ordner, in dem die Indexdateien gespeichert werden.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Schritt 2: Dokumente zum Index hinzufügen
Teilen Sie GroupDocs.Search mit, wo sich Ihre Quelldokumente befinden. Alle unterstützten Dateitypen (PDF, DOCX, TXT usw.) werden automatisch indiziert.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Schritt 3: Suche im Inhaltsfeld mit einer Textabfrage durchführen
Eine schnelle Textabfrage filtert nach dem Feld `content`. Die Syntax `content: Pellentesque` begrenzt die Ergebnisse auf Dokumente, die das Wort *Pellentesque* im Fließtext enthalten.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Schritt 4: Suche mit einer Objekt‑Abfrage durchführen
Objektbasierte Abfragen geben Ihnen feinkörnige Kontrolle. Hier erstellen wir eine Wortabfrage, verpacken sie in eine Feldabfrage und führen sie aus.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Wie man boolesche Operatoren Java verwendet – Komplexe Abfragesuche

Um eine komplexe Abfrage auszuführen, kombinieren Sie mehrere Feldbedingungen mit AND/OR/NOT‑Operatoren und fügen optional Phrasensuchen hinzu. Sie können jede Bedingung mittels Feldabfragen angeben, sie mit booleschen Operatoren verschachteln und die Relevanz durch Boosting steuern, sodass Sie nur die relevantesten Dokumente erhalten, die alle erforderlichen Kriterien erfüllen.

### Schritt 1: Index für komplexe Abfragen erstellen
Verwenden Sie dieselbe Ordnerstruktur erneut; Sie können den Index sowohl für einfache als auch für komplexe Szenarien gemeinsam nutzen.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Schritt 2: Suche mit einer Textabfrage durchführen
Die folgende Abfrage sucht nach Dateien mit dem Namen *lorem* **und** *ipsum* **oder** nach Inhalten, die eine von zwei genauen Phrasen enthalten.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Schritt 3: Suche mit einer Objekt‑Abfrage durchführen
Objektbasierte Konstruktion spiegelt die Textabfrage wider, bietet jedoch Typsicherheit und IDE‑Unterstützung.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Praktische Anwendungen von facettierten & komplexen Suchen

| Szenario | Wie Facettierung hilft | Beispielabfrage |
|----------|------------------------|-----------------|
| **E‑Commerce-Katalog** | Nach Kategorie, Preis, Marke filtern | `category: Electronics AND price:[100 TO 500]` |
| **Rechtsdokumenten‑Repository** | Nach Aktenzeichen, Gerichtsbarkeit eingrenzen | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Forschungsarchive** | Autor, Publikationsjahr, Schlüsselwörter kombinieren | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Unternehmens‑Intranet** | Nach Dateityp und Abteilung suchen | `filetype: pdf AND department: HR` |

## Häufige Fallstricke & Fehlerbehebung

Das Objekt `SearchResult` enthält die Dokumente, die einer Abfrage entsprechen, und bietet Zugriff auf deren Relevanz‑Scores und hervorgehobene Fragmente.  
Die Klasse `CommonFieldNames` definiert Standardfeldnamen wie `Content` und `FileName`, die in der gesamten API verwendet werden.

- **Leere Ergebnisse** – Überprüfen Sie, ob die Dokumente erfolgreich hinzugefügt wurden (`index.getDocumentCount()` kann helfen).  
- **Veralteter Index** – Nach dem Hinzufügen oder Entfernen von Dateien rufen Sie `index.update()` auf, um **Index aktualisieren Java** durchzuführen und den Index synchron zu halten.  
- **Falsche Feldnamen** – Verwenden Sie die Konstanten `CommonFieldNames` (`Content`, `FileName` usw.), um Tippfehler zu vermeiden.  
- **Leistungsengpässe** – Bei riesigen Sammlungen sollten Sie das Aktivieren von `index.setCacheSize()` oder die Verwendung einer dedizierten SSD für den Indexordner in Betracht ziehen.  
- **Fehlende Hervorhebungen** – Um **Suchergebnisse hervorheben Java** zu erreichen, rufen Sie die passenden Fragmente über `SearchResult.getFragments()` ab (hier nicht gezeigt, aber in der API verfügbar).

## Häufig gestellte Fragen

**F: Kann ich GroupDocs.Search mit Spring Boot verwenden?**  
**A:** Absolut. Fügen Sie die Maven‑Abhängigkeit hinzu, konfigurieren Sie den Index als Spring‑Bean und injizieren Sie ihn dort, wo Sie Suchfunktionen benötigen.

**F: Unterstützt die Bibliothek benutzerdefinierte Metadatenfelder?**  
**A:** Ja – Sie können während der Indexierung benutzerdefinierte Felder hinzufügen und anschließend darauf facettieren.

**F: Wie groß kann der Index werden?**  
**A:** Der festplattenbasierte Index kann bis zu 10 Millionen Dokumente verarbeiten; stellen Sie lediglich ausreichenden Speicher sicher und überwachen Sie die Cache‑Einstellungen.

**F: Gibt es eine Möglichkeit, Ergebnisse nach Relevanz zu ranken?**  
**A:** GroupDocs.Search bewertet Treffer automatisch; Sie können den Score über `SearchResult.getDocument(i).getScore()` abrufen.

**F: Was passiert, wenn ich verschlüsselte PDFs indiziere?**  
**A:** Geben Sie beim Hinzufügen des Dokuments das Passwort an: `index.add(filePath, password)`.

## Fazit

Jetzt sollten Sie sich sicher fühlen, **Suchindex erstellen Java** mit GroupDocs.Search zu nutzen, Dokumente hinzuzufügen und sowohl einfache facettierte Abfragen als auch anspruchsvolle boolesche Suchen mit **booleschen Operatoren Java** zu erstellen. Diese Fähigkeiten ermöglichen es Ihnen, schnelle, präzise und benutzerfreundliche Sucherlebnisse in einer Vielzahl von Anwendungen bereitzustellen – von E‑Commerce‑Plattformen bis hin zu Unternehmens‑Wissensdatenbanken.

Bereit für den nächsten Schritt? Erkunden Sie die erweiterten Funktionen von **GroupDocs.Search**, wie **Hervorhebung**, **Vorschläge** und **Echtzeit‑Indexierung**, um die Suchkraft Ihrer Anwendung weiter zu steigern.

---

**Last Updated:** 2026-08-26  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Verwandte Tutorials

- [Wildcard-Suche Java mit GroupDocs.Search – Erweiterte Funktionen](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Wie man Index Java mit GroupDocs.Search aktualisiert – Ein umfassender Leitfaden](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Wie man Java-Volltextsuche implementiert: Indexverzeichnis mit GroupDocs.Search erstellen](/search/java/indexing/groupdocs-search-java-create-index/)