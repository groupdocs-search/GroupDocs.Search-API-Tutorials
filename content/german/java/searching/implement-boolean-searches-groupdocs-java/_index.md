---
date: '2026-01-29'
description: Erfahren Sie, wie Sie Java‑Boolean‑ und OR‑Abfragen mit GroupDocs.Search
  für Java implementieren, Dokumente zum Index hinzufügen und die Dokumentenabfrage
  verbessern.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'Java Boolean und/oder: Beherrsche Boolesche Suchen mit GroupDocs.Search für
  Java'
type: docs
url: /de/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: Beherrschung von Booleschen Suchvorgängen mit GroupDocs.Search für Java

Die Suche in riesigen Dokumentensammlungen kann sich anfühlen, als würde man eine Nadel im Heuhaufen suchen. Mit **java boolean and or**‑Abfragen können Sie der Engine genau mitteilen, was Sie benötigen – Dokumente, die *beide* Begriffe enthalten, *einen* der Begriffe oder *unerwünschte* Wörter ausschließen. In diesem Leitfaden zeigen wir, wie Sie **GroupDocs.Search for Java** einrichten, Dokumente zu einem Index hinzufügen und leistungsstarke Boolesche Abfragen erstellen, die Ihre **document retrieval java**‑Arbeitsabläufe verbessern.

## Schnelle Antworten
- **Was ist eine boolesche AND‑Abfrage?** Gibt nur Dokumente zurück, die *alle* angegebenen Begriffe enthalten.  
- **Wie unterscheidet sich OR von AND?** OR findet Dokumente mit *irgendeinem* der Begriffe und erweitert damit die Ergebnismenge.  
- **Wann sollte ich NOT verwenden?** Verwenden Sie NOT, um Dokumente mit unerwünschten Wörtern herauszufiltern.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für Tests; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Welche Java-Version wird benötigt?** Java 8+ wird unterstützt; JDK 11+ wird empfohlen.

## Was ist **java boolean and or**?
Eine **java boolean and or**‑Abfrage kombiniert logische Operatoren (AND, OR, NOT), um Suchergebnisse zu verfeinern. Durch die Strukturierung von Abfragen teilen Sie GroupDocs.Search genau mit, wie die Begriffe zueinander stehen, und erhalten so eine präzise Kontrolle über den Abrufprozess.

## Warum GroupDocs.Search für Java verwenden?
- **High performance** bei großen Dokumentenmengen.  
- **Rich API** die sowohl textbasierte als auch objektbasierte Abfragen unterstützt.  
- **Built‑in language support** für Stemming, Stoppwörter und Fuzzy‑Matching.  
- **Easy integration** mit Maven oder direktem JAR‑Download.

## Voraussetzungen
Bevor Sie starten, stellen Sie sicher, dass Sie Folgendes haben:

- **GroupDocs.Search for Java** (v25.4 oder neuer) – siehe den Download‑Link unten.  
- JDK 8+ installiert und in Ihrer IDE (IntelliJ IDEA, Eclipse usw.) konfiguriert.  
- Grundkenntnisse in Java und Maven für das Abhängigkeitsmanagement.  

## Einrichtung von GroupDocs.Search für Java

### Maven-Konfiguration
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

### Direkter Download
Alternativ können Sie das neueste JAR von der offiziellen Seite herunterladen: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lizenzbeschaffung
Beginnen Sie mit einer kostenlosen Testlizenz, um alle Funktionen zu erkunden. Für den Produktionseinsatz erwerben Sie eine kommerzielle Lizenz, um die volle Funktionalität freizuschalten.

### Grundlegende Initialisierung und Einrichtung
Erstellen Sie einen Index‑Ordner und instanziieren Sie das `Index`‑Objekt:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## java boolean and or: Implementierung Boolescher Suchvorgänge

Im Folgenden behandeln wir **AND**, **OR**, **NOT** und **complex**‑Abfragen. Jeder Abschnitt zeigt sowohl eine reine Textabfrage als auch die äquivalente objektbasierte Abfrage, sodass Sie den Stil wählen können, der zu Ihrem Codebasis passt.

### Boolesche AND‑Suche
Kombinieren Sie Begriffe mit **AND**, um nur Dokumente abzurufen, die *alle* Schlüsselwörter enthalten.

#### Überblick
Eine AND‑Abfrage verengt die Ergebnisse und verbessert die Relevanz, wenn Sie Dokumente benötigen, die mehrere Kriterien erfüllen.

#### Implementierungsschritte

1. **Initialize Index** – dies demonstriert ebenfalls **add documents to index** für das AND‑Szenario.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – unter Verwendung der reinen Zeichenketten‑Syntax.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – nützlich beim programmatischen Aufbau von Abfragen (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### Boolesche OR‑Suche
Verwenden Sie **OR**, um die Ergebnisse zu erweitern und jedes der angegebenen Stichwörter zu treffen.

#### Überblick
Eine OR‑Abfrage ist ideal für explorative Suchen, bei denen Sie Dokumente erfassen möchten, die mindestens eines mehrerer Schlüsselwörter enthalten (**search with or java**).

#### Implementierungsschritte

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

### Boolesche NOT‑Suche
Schließen Sie unerwünschte Begriffe mit **NOT** aus, um Rauschen aus Ihren Ergebnissen zu filtern.

#### Überblick
Eine NOT‑Abfrage hilft Ihnen, irrelevante Dokumente zu eliminieren, z. B. das Herausfiltern des Markennamens eines Konkurrenten (**boolean search examples java**).

#### Implementierungsschritte

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

### Komplexe Boolesche Abfragen
Kombinieren Sie **AND**, **OR** und **NOT**, um komplexe Suchlogik für hochspezifische Abrufanforderungen zu erstellen.

#### Überblick
Komplexe Abfragen ermöglichen es, reale Suchszenarien zu modellieren, z. B. „Finden Sie Sportartikel, die positiv sind, aber jede Erwähnung bestimmter Athleten ausschließen“.

#### Implementierungsschritte

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## Praktische Anwendungen von java boolean and or‑Abfragen
- **Document Management Systems** – finden Sie Verträge, die sowohl „confidential“ **AND** „renewal“ enthalten.  
- **Legal Research** – filtern Sie Rechtsprechung mit **AND**/**OR**, während Sie veraltete Gesetze mit **NOT** ausschließen.  
- **Customer Support** – rufen Sie Tickets ab, die „login“ **AND** „error“ erwähnen, aber nicht „resolved“.  
- **Content Curation** – sammeln Sie Blogbeiträge über „cloud“ **OR** „serverless“ für einen Newsletter.  

## Häufige Fallstricke & Fehlersuche
- **Missing Index Refresh** – nach dem Hinzufügen neuer Dokumente rufen Sie `index.update()` auf, um sicherzustellen, dass sie durchsuchbar sind.  
- **Incorrect Operator Spacing** – GroupDocs.Search erwartet Leerzeichen um die Operatoren (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – Abfragen sind standardmäßig nicht case‑sensitive, aber benutzerdefinierte Analyzer können dies beeinflussen.  
- **Large Result Sets** – verwenden Sie Paginierung (`search(query, 0, 100)`), um Speicherüberlastungen zu vermeiden.  

## Häufig gestellte Fragen

**Q: Kann ich mehr als zwei Begriffe in einer AND‑Abfrage kombinieren?**  
A: Absolut. Sie können mehrere `createWordQuery`‑Objekte mit `createAndQuery` verketten oder einfach `"term1 AND term2 AND term3"` in der Textabfrage schreiben.

**Q: Unterstützt GroupDocs.Search Platzhalter‑ oder Fuzzy‑Suchen?**  
A: Ja. Hängen Sie `*` für einen Platzhalter an (z. B. `promot*`) oder verwenden Sie `~` für Fuzzy‑Matching (z. B. `comfort~`).

**Q: Wie begrenze ich die Suche auf bestimmte Dateitypen?**  
A: Verwenden Sie die Klasse `FileTypeQuery`, um die Ergebnisse auf PDFs, DOCX usw. zu beschränken, und kombinieren Sie sie mit Ihrer Booleschen Abfrage.

**Q: Was ist der beste Weg, die Indexierungs‑Performance zu überwachen?**  
A: Aktivieren Sie den integrierten Logger (`index.getLogger().setLevel(Level.INFO)`) und prüfen Sie die Zeitmessungen nach jeder `add`‑Operation.

**Q: Gibt es eine Möglichkeit, die Relevanz bestimmter Begriffe zu erhöhen?**  
A: Ja. Umhüllen Sie wichtige Wörter mit `BoostQuery`, um ihr Gewicht im Scoring‑Algorithmus zu erhöhen.

---

**Last Updated:** 2026-01-29  
**Tested With:** GroupDocs.Search 25.4 (Java)  
**Author:** GroupDocs