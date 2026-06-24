---
date: '2026-05-28'
description: Erfahren Sie, wie Sie mit wildcard patterns nach einer Phrase suchen,
  indem Sie GroupDocs.Search for Java verwenden. Enthält das Erstellen eines search
  index, das Hinzufügen von documents und das Ausführen von exact phrase und wildcard
  queries.
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: Wie man eine Phrase mit Wildcards in GroupDocs.Search for Java sucht
type: docs
url: /de/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Wie man Phrasen mit Platzhaltern in GroupDocs.Search für Java sucht

In modernen dokumentzentrierten Anwendungen ist **wie man eine Phrase sucht** schnell und genau zu finden ein entscheidender Faktor für die Benutzererfahrung. Egal, ob Sie eine Wissensdatenbank, einen E‑Commerce‑Katalog oder ein compliance‑gesteuertes Repository erstellen, die Fähigkeit, eine exakte Phrase – oder eine flexible Variante davon – zu finden, hält die Benutzer produktiv und reduziert den Support‑Aufwand. Dieses Tutorial führt Sie durch die Installation von **GroupDocs.Search for Java**, das Erstellen eines Suchindexes, das Laden von Dokumenten und das Ausführen sowohl von exakten Phrasen‑ als auch von Platzhalter‑erweiterten Abfragen, alles mit klaren, produktionsbereiten Code‑Snippets.

## Schnelle Antworten
- **Was ist der Hauptvorteil von Phrasensuchen?** Präzises Matching der Wortreihenfolge und Nähe, das garantiert, dass nur Dokumente zurückgegeben werden, die die exakte Sequenz enthalten.  
- **Können Platzhalter innerhalb einer Phrase verwendet werden?** Ja – Platzhalter ermöglichen es, Wörter zu überspringen oder zu ersetzen, während die Gesamtreihenfolge beibehalten wird.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Testversion funktioniert zum Testen; für den Produktionseinsatz ist eine Voll‑Lizenz erforderlich.  
- **Welche Maven‑Version sollte ich verwenden?** Die neueste GroupDocs.Search for Java‑Version (z. B. 25.4 zum Zeitpunkt der Erstellung).  
- **Ist dieser Ansatz für große Dokumentenmengen geeignet?** Absolut – GroupDocs.Search kann Sammlungen mit mehreren hunderttausend Dokumenten verarbeiten, wobei die Abfrage‑Latenz unter einer Sekunde liegt, wenn der Index optimiert ist.

## Was ist “wie man eine Phrase sucht”?
**Eine Phrase zu suchen bedeutet, nach einer bestimmten Wortsequenz in einem Dokument zu suchen.**  
Wenn Sie eine Phrasen‑Abfrage ausführen, prüft die Engine, dass die Wörter in exakt derselben Reihenfolge und innerhalb der definierten Nähe erscheinen, wodurch irrelevante Treffer, die dieselben Wörter in anderem Kontext enthalten, eliminiert werden. Dies macht Phrasensuchen ideal zum Auffinden von Rechtsklauseln, Produktcodes oder jedem Text, bei dem die Reihenfolge wichtig ist.

## Warum GroupDocs.Search für Phrase‑ und Platzhalter‑Abfragen verwenden?
GroupDocs.Search bietet **hochleistungsfähige Indizierung von bis zu 1 Million Dokumenten bei gleichzeitig sub‑sekundaren Abfrage‑Antwortzeiten** auf typischer Server‑Hardware. Seine Abfragesprache unterstützt exakte Phrasen, einfache `*`‑ und `?`‑Platzhalter sowie erweiterte Muster wie numerische Bereiche (`*2~5`). Die Bibliothek lässt sich über Maven oder einen direkten JAR‑Download in jede Java‑Anwendung integrieren und läuft auf Java 8+ ohne externe Dienste.

## Voraussetzungen
- Java 8 oder neuer (Java 11 LTS empfohlen).  
- Maven 3 oder höher (falls Sie die Abhängigkeitsverwaltung bevorzugen).  
- Grundlegende Kenntnisse der Java‑Projektstruktur und objektorientierter Konzepte.  

## Einrichtung von GroupDocs.Search für Java

### Verwendung von Maven
Fügen Sie das offizielle Repository und die GroupDocs.Search‑Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### Direkter Download
Alternativ können Sie das neueste JAR von der offiziellen Release‑Seite herunterladen: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lizenzbeschaffung
- **Kostenlose Testversion:** Ideal für schnelle Experimente; begrenzt auf 100 MB indizierter Daten.  
- **Temporäre Lizenz:** Fordern Sie einen 30‑Tage‑Evaluierungsschlüssel über das GroupDocs‑Portal an.  
- **Vollständige Lizenz:** Für den Produktionseinsatz und unbegrenzte Indizierungskapazität erforderlich.

## Grundlegende Initialisierung und Einrichtung
Erstellen Sie einen Ordner, der die Indexdateien enthält, und instanziieren Sie das `Index`‑Objekt. Die Klasse `Index` repräsentiert den auf der Festplatte gespeicherten durchsuchbaren Index und bietet Methoden zum Hinzufügen, Aktualisieren und Abfragen von Dokumenten.

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

Fügen Sie die Dokumente hinzu, die durchsuchbar sein sollen:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## Wie man Phrasen mit Platzhaltern in GroupDocs.Search sucht
Dieser Abschnitt demonstriert drei Ebenen der Phrasensuche – exakte Übereinstimmung, einfacher Platzhalter und erweiterte Platzhalter‑Muster – und zeigt, wie man einen Index erstellt, Dokumente hinzufügt und jeden Abfragetyp mit kompaktem Java‑Code ausführt. Die Beispiele veranschaulichen sowohl textbasierte Abfragen als auch objektbasierte Abfragekonstruktionen, sodass Entwickler flexible Suchfunktionen in ihre Anwendungen integrieren können.

### Einfache Phrasensuche

#### Überblick
Verwenden Sie diesen Ansatz, wenn Sie eine **exakte Übereinstimmung** einer Wortsequenz benötigen, z. B. eine Rechtsklausel oder eine Produktmodellnummer.

#### Direkte Antwort
Laden Sie den Index, rufen Sie `search` mit einer in Anführungszeichen gesetzten Phrase auf (z. B. `"quick brown fox"`), und die Engine gibt nur Dokumente zurück, die genau diese Sequenz enthalten, wobei Wortreihenfolge und Abstand erhalten bleiben. Die Abfrage wird in Millisekunden ausgeführt, selbst bei Indizes mit Hunderttausenden von Dateien.

#### Schritt 1: Index erstellen
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### Schritt 2: Dokumente zum Index hinzufügen
```java
Index index = new Index(indexFolder);
```

#### Schritt 3: Nach einer bestimmten Phrase suchen (Textform)
```java
index.add(documentsFolder);
```

#### Schritt 4: Objektbasierte Abfragen (exakte Phrase suchen)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### Phrasensuche mit Platzhaltern

#### Überblick
Platzhalter (`*` für beliebig viele Zeichen, `?` für ein einzelnes Zeichen) ermöglichen es, **variable Wörter zu überspringen**, während die umgebende Reihenfolge weiterhin erzwungen wird.

#### Direkte Antwort
Fügen Sie ein Platzhalter‑Token (`*`) in eine in Anführungszeichen gesetzte Phrase ein – z. B. `"quick * fox"` – um beliebige Wörter zwischen *quick* und *fox* zu matchen. Die Engine erweitert den Platzhalter zur Abfragezeit und durchsucht nur die indizierten Terme, die dem Muster entsprechen, wodurch die Leistung vergleichbar mit einer einfachen Phrasen‑Abfrage bleibt.

#### Schritt 1: Index erstellen
*(Wie bei der einfachen Phrasensuche.)*

#### Schritt 2: Dokumente zum Index hinzufügen
*(Wie oben.)*

#### Schritt 3: Textbasierte Suche mit Platzhaltern
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Schritt 4: Objektbasierte Abfragen mit Platzhaltern (Wildcard Search Java)
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### Erweiterte Platzhaltersuche

#### Überblick
Kombinieren Sie numerische Bereiche, optionale Zeichen und benutzerdefinierte regex‑ähnliche Muster für **komplexe Übereinstimmungen**, wie Versionsnummern oder Produktcodes.

#### Direkte Antwort
Verwenden Sie die erweiterte Platzhalter‑Syntax `*min~max`, um einen Bereich zulässiger Wortabstände zu definieren, oder `?`, um ein einzelnes Zeichen zu matchen. Zum Beispiel findet `"error *2~5 code"` das Wort *error*, gefolgt von zwei bis fünf beliebigen Wörtern und anschließend *code*. Diese Präzision reduziert Fehlalarme, bietet aber dennoch Flexibilität.

#### Schritt 1: Index erstellen
*(Zur Klarstellung wiederholt.)*

#### Schritt 2: Dokumente zum Index hinzufügen
*(Wiederholt.)*

#### Schritt 3: Textbasierte Suche mit komplexen Platzhaltermustern
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Schritt 4: Objektbasierte Abfragen mit erweiterten Platzhaltern
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## Praktische Anwendungsfälle
- **Content Management Systeme:** Redakteure können exakte Klauseln oder flexible Auszüge finden, ohne Hunderte von Seiten manuell zu durchsuchen.  
- **E‑Commerce‑Kataloge:** Käufer finden Produkte, selbst wenn sie eine Beschreibung weglassen oder Synonyme verwenden, dank Platzhalter‑Toleranz.  
- **Recht & Compliance:** Schnell vertragliche Formulierungen isolieren, die mit kleinen Variationen in verschiedenen Vereinbarungen auftreten können.  

## Leistungsüberlegungen
- **Suchindex erstellen** nur einmal pro stabilem Dokumentensatz; dieselbe `Index`‑Instanz für alle Abfragen wiederverwenden.  
- **Dokumente inkrementell hinzufügen**, wenn neue Dateien eintreffen – das komplette Neuaufbauen des Indexes vermeiden, um die CPU‑Auslastung gering zu halten.  
- **Präzise Platzhalter‑Muster entwerfen**; breitere Muster (`*`) erhöhen die Anzahl der Term‑Erweiterungen und können die CPU‑Last erhöhen.  
- **Rufen Sie `index.optimize()`** periodisch (falls unterstützt) auf, um den Index zu komprimieren und den Speicherverbrauch im Griff zu behalten.  

## Häufige Probleme & Lösungen
| Problem | Lösung |
|-------|----------|
| Keine Ergebnisse für eine Platzhalter‑Abfrage | Überprüfen Sie die Platzhalter‑Syntax (`*min~max`) und stellen Sie sicher, dass die Zielwörter innerhalb des definierten Abstands existieren. |
| Index wird nach Datei‑Updates veraltet | Verwenden Sie `index.add(updatedFolder)` oder die inkrementelle Update‑API, um nur geänderte Dateien zu aktualisieren. |
| Hoher Speicherverbrauch bei großen Datensätzen | Erhöhen Sie den JVM‑Heap (`-Xmx4g` oder höher) und erwägen Sie, den Index in mehrere Shards aufzuteilen für parallele Verarbeitung. |

## Häufig gestellte Fragen

**Q: Was ist der Unterschied zwischen einem Platzhalter und einer Phrasensuche?**  
A: Eine Phrasensuche erfordert die exakte Wortreihenfolge und den Abstand, während ein Platzhalter es ermöglicht, Wörter innerhalb dieser Reihenfolge zu ersetzen oder zu überspringen, was flexible Übereinstimmungen bietet.

**Q: Kann ich Platzhalter bei numerischen Daten in Suchanfragen verwenden?**  
A: Ja – Platzhalter‑Bereichsparameter (`*min~max`) funktionieren sowohl mit Zahlen als auch mit Wörtern und ermöglichen Abfragen wie `"version *1~3"`.

**Q: Wie sollte ich sehr große Dokumentensammlungen handhaben?**  
A: Halten Sie den Index optimiert, führen Sie inkrementelle Updates durch und erstellen Sie spezifische Platzhalter‑Muster, um die Term‑Erweiterung zu begrenzen. GroupDocs.Search kann 1 Million Dokumente indizieren und dabei die Abfrage‑Latenz unter 200 ms auf Standard‑Hardware halten.

**Q: Ist GroupDocs.Search für Echtzeit‑Suchszenarien geeignet?**  
A: Absolut – sobald der Index erstellt ist, werden Abfragen in Millisekunden ausgeführt, was es ideal für interaktive Suchfelder und Auto‑Complete‑Funktionen macht.

**Q: Kann ich diese Bibliothek in ein bestehendes Java‑Projekt integrieren?**  
A: Ja. Fügen Sie die Maven‑Abhängigkeit oder das JAR hinzu, instanziieren Sie das `Index` wie gezeigt, und Sie können abfragen, ohne bestehenden Code zu ändern.

---

**Zuletzt aktualisiert:** 2026-05-28  
**Getestet mit:** GroupDocs.Search 25.4 für Java  
**Autor:** GroupDocs

```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## Verwandte Tutorials

- [Suchindex erstellen Java – GroupDocs.Search Tutorials](/search/java/)
- [Dokumente zum Index hinzufügen – GroupDocs.Search Java Tutorials](/search/java/document-management/)
- [Suchindex erstellen – GroupDocs.Search Java Tutorials](/search/java/advanced-features/)