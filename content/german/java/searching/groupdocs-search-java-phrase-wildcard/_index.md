---
date: '2026-01-26'
description: Erfahren Sie, wie Sie Phrasen mit Platzhaltermustern in GroupDocs.Search
  für Java suchen. Dieser Leitfaden behandelt das Erstellen eines Suchindexes, das
  Hinzufügen von Dokumenten zum Index und die Durchführung einer Platzhaltersuche
  in Java.
keywords:
- GroupDocs.Search for Java
- phrase searches
- wildcard patterns
title: Wie man Phrasen mit Platzhaltern in GroupDocs.Search Java sucht
type: docs
url: /de/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Wie man Phrasen mit Wildcards in GroupDocs.Search für Java sucht

In der heutigen schnelllebigen Welt des Dokumentenmanagements kann **how to search phrase** effizient zu suchen den Unterschied zwischen Erfolg und Misserfolg der Benutzerfreundlichkeit einer Anwendung ausmachen. Egal, ob Sie ein Content‑Management‑System, einen E‑Commerce‑Katalog oder ein Rechtsdokument‑Repository erstellen, die Fähigkeit, exakte Phrasen – oder flexible Variationen davon – zu finden, ist entscheidend. In diesem Tutorial führen wir Sie durch die Einrichtung von **GroupDocs.Search für Java**, das Erstellen eines Suchindexes, das Hinzufügen von Dokumenten zum Index und das Beherrschen sowohl einfacher Phrasensuchen als auch leistungsstarker Java‑Wildcard‑Suchtechniken.

## Schnelle Antworten
- **Was ist der Hauptvorteil von Phrasensuchen?** Präzise Übereinstimmung von Wortreihenfolge und Nähe.  
- **Können Wildcards innerhalb einer Phrase verwendet werden?** Ja, Sie können Wildcards mit exakten Wörtern für flexible Übereinstimmungen kombinieren.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Testversion reicht für Tests; für die Produktion ist eine Volllizenz erforderlich.  
- **Welche Maven-Version sollte ich verwenden?** Die neueste GroupDocs.Search für Java-Version (z. B. 25.4 zum Zeitpunkt der Erstellung).  
- **Ist dieser Ansatz für große Dokumentenmengen geeignet?** Absolut – halten Sie den Index optimiert und verwenden Sie gezielte Wildcard‑Muster.

## Was ist “how to search phrase”?
Eine Phrase zu suchen bedeutet, nach einer bestimmten Wortsequenz in einem Dokument zu suchen. Wenn Sie Wildcards hinzufügen, ermöglichen Sie der Suchmaschine, Wörter zu überspringen oder zu ersetzen, wodurch Sie die Flexibilität erhalten, Varianten zu finden, ohne die Relevanz zu verlieren.

## Warum GroupDocs.Search für Phrase‑ und Wildcard‑Abfragen verwenden?
- **Hohe Leistung** bei großen Sammlungen dank eines optimierten invertierten Index.  
- **Umfangreiche Abfragesprache**, die exakte Phrasen, einfache Wildcards und erweiterte Muster unterstützt.  
- **Einfache Integration** in jede Java‑basierte Anwendung über Maven oder direkten Download.  

## Voraussetzungen
- Java 8 oder neuer installiert.  
- Maven 3 oder höher (falls Sie die Maven‑Abhängigkeitsverwaltung bevorzugen).  
- Grundlegende Kenntnisse der Java‑Syntax und Projektstruktur.  

## Einrichtung von GroupDocs.Search für Java

### Verwendung von Maven
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
Alternativ laden Sie das neueste JAR von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunter.

### Lizenzbeschaffung
- **Kostenlose Testversion:** Ideal für schnelle Experimente.  
- **Temporäre Lizenz:** Antrag über das GroupDocs‑Portal für erweitertes Testen.  
- **Vollkauf:** Empfohlen für den Produktionseinsatz.

### Grundlegende Initialisierung und Einrichtung
Erstellen Sie einen Ordner für den Index und initialisieren Sie ihn:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

Fügen Sie die Dokumente hinzu, die durchsuchbar sein sollen:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

## Wie man Phrasen mit Wildcards in GroupDocs.Search sucht
Im Folgenden werden drei fortschreitende Szenarien erläutert: exakte Phrasensuche, einfache Wildcard‑Verwendung und erweiterte Wildcard‑Muster.

### Einfache Phrasensuche

#### Überblick
Verwenden Sie dies, wenn Sie eine exakte Übereinstimmung einer Wortsequenz benötigen.

##### Schritt 1: Index erstellen
```java
Index index = new Index(indexFolder);
```

##### Schritt 2: Dokumente zum Index hinzufügen
```java
index.add(documentsFolder);
```

##### Schritt 3: Nach einer bestimmten Phrase suchen (Textform)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Schritt 4: Objektbasierte Abfragen (exakte Phrase suchen)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Phrasensuche mit Wildcards

#### Überblick
Wildcard‑Platzhalter ermöglichen das Überspringen einer variablen Anzahl von Wörtern zwischen exakten Begriffen.

##### Schritt 1: Index erstellen
*(Wie bei den Schritten der einfachen Phrasensuche.)*

##### Schritt 2: Dokumente zum Index hinzufügen
*(Wie oben.)*

##### Schritt 3: Textformsuche mit Wildcards
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Schritt 4: Objektbasierte Abfragen mit Wildcards (Wildcard Search Java)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Erweiterte Wildcard‑Suche

#### Überblick
Kombinieren Sie numerische Bereiche, optionale Zeichen und benutzerdefinierte Muster für anspruchsvolle Übereinstimmungen.

##### Schritt 1: Index erstellen
*(Zur Klarstellung wiederholt.)*

##### Schritt 2: Dokumente zum Index hinzufügen
*(Wiederholt.)*

##### Schritt 3: Textformsuche mit komplexen Wildcard‑Mustern
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

##### Schritt 4: Objektbasierte Abfragen mit erweiterten Wildcards
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

## Praktische Anwendungen
- **Content-Management-Systeme:** Ermöglichen Redakteuren, exakte Klauseln oder flexible Auszüge zu finden.  
- **E‑Commerce-Kataloge:** Lassen Käufer Produkte finden, selbst wenn ihnen ein Wort fehlt oder sie Synonyme verwenden.  
- **Recht & Compliance:** Schnell vertragliche Formulierungen isolieren, die mit kleinen Variationen auftreten können.

## Leistungsüberlegungen
- **Suchindex erstellen** nur einmal pro Dokumentensatz und dann wiederverwenden.  
- **Dokumente zum Index hinzufügen** inkrementell, wenn neue Dateien eintreffen – den gesamten Index nicht jedes Mal neu erstellen.  
- Verwenden Sie **präzise Wildcard‑Muster**, um unnötiges Scannen zu vermeiden; breitere Muster erhöhen die CPU‑Auslastung.  
- Rufen Sie periodisch `index.optimize()` (falls verfügbar) auf, um den Speicherverbrauch gering zu halten.

## Häufige Probleme & Lösungen
| Problem | Lösung |
|-------|----------|
| Keine Ergebnisse für eine Wildcard‑Abfrage zurückgegeben | Überprüfen Sie die Wildcard‑Syntax (`*min~~max`) und stellen Sie sicher, dass die Wörter innerhalb des angegebenen Abstands existieren. |
| Index wird nach Datei‑Updates veraltet | Führen Sie `index.add(updatedFolder)` erneut aus oder verwenden Sie die inkrementelle Update‑API. |
| Hoher Speicherverbrauch bei großen Datensätzen | Erhöhen Sie die JVM‑Heap‑Größe und erwägen Sie, den Index in mehrere Shards aufzuteilen. |

## Häufig gestellte Fragen

**F: Was ist der Unterschied zwischen einer Wildcard‑ und einer Phrasensuche?**  
A: Eine Phrasensuche sucht nach einer exakten Wortreihenfolge, während eine Wildcard es ermöglicht, Wörter innerhalb dieser Reihenfolge zu ersetzen oder zu überspringen.

**F: Kann ich Wildcards mit numerischen Daten in Suchen verwenden?**  
A: Ja, die Wildcard‑Bereichsparameter funktionieren sowohl mit Zahlen als auch mit Wörtern.

**F: Wie sollte ich sehr große Dokumentensammlungen handhaben?**  
A: Halten Sie den Index optimiert, verwenden Sie inkrementelle Updates und gestalten Sie Ihre Wildcard‑Muster so spezifisch wie möglich.

**F: Ist GroupDocs.Search für Echtzeit‑Suchszenarien geeignet?**  
A: Absolut – sobald der Index erstellt ist, werden Abfragen in Millisekunden ausgeführt, was ihn für interaktive Anwendungen geeignet macht.

**F: Kann ich diese Bibliothek in ein bestehendes Java‑Projekt integrieren?**  
A: Ja. Fügen Sie die Maven‑Abhängigkeit oder das JAR hinzu, initialisieren Sie den Index wie gezeigt, und Sie können loslegen.

---

**Zuletzt aktualisiert:** 2026-01-26  
**Getestet mit:** GroupDocs.Search 25.4 für Java  
**Autor:** GroupDocs