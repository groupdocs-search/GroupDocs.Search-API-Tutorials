---
date: '2026-07-21'
description: Das Create Boolean Query Java‑Tutorial zeigt, wie man boolesche AND-,
  OR‑ und NOT‑Suchen mit GroupDocs.Search for Java implementiert, Dokumente zu einem
  Index hinzufügt und die Dokumentenabfrage verbessert.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Das Create Boolean Query Java‑Tutorial erklärt Schritt für Schritt,
  wie man AND‑, OR‑ und NOT‑Abfragen mit GroupDocs.Search for Java erstellt, Dokumente
  zu einem Index hinzufügt und die Abrufleistung verbessert.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Create Boolean Query Java – Beherrsche Boolesche Suchen mit GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Erstelle Boolesche Abfrage Java: Beherrsche Boolesche Suchen mit GroupDocs.Search
  for Java'
type: docs
url: /de/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Boolesche Abfrage in Java erstellen: Boolesche Suchen mit GroupDocs.Search für Java

Das Durchsuchen riesiger Dokumentensammlungen kann sich anfühlen, als würde man eine Nadel im Heuhaufen suchen. **Create Boolean Query Java** ermöglicht es Ihnen, der Engine genau mitzuteilen, was Sie benötigen – Dokumente, die *beide* Begriffe enthalten, *einen* der Begriffe oder *unerwünschte* Wörter auszuschließen. In diesem Leitfaden zeigen wir Ihnen, wie Sie **GroupDocs.Search for Java** einrichten, Dokumente zu einem Index hinzufügen und leistungsstarke boolesche Abfragen erstellen, die Ihre **document retrieval java** Arbeitsabläufe verbessern. Am Ende können Sie sauberen, wartbaren Code schreiben, der boolesche Abfragen in Java mit nur wenigen Zeilen erstellt.

## Schnelle Antworten
- **Was ist eine boolesche AND‑Abfrage?** Gibt nur Dokumente zurück, die *alle* angegebenen Begriffe enthalten.  
- **Wie unterscheidet sich OR von AND?** OR findet Dokumente mit *irgendeinem* der Begriffe und erweitert damit die Ergebnismenge.  
- **Wann sollte ich NOT verwenden?** Verwenden Sie NOT, um Dokumente mit unerwünschten Wörtern herauszufiltern.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion reicht für Tests; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Welche Java‑Version wird benötigt?** Java 8+ wird unterstützt; JDK 11+ wird empfohlen.

## Was ist **create boolean query java**?
`create boolean query java` bezieht sich auf das Erstellen einer Suchabfrage in Java, die logische Operatoren wie AND, OR und NOT mithilfe der GroupDocs.Search‑API kombiniert. Durch das Zusammenstellen dieser Operatoren können Sie genau steuern, welche Dokumente übereinstimmen, was erweiterte Filterung, Relevanz‑Feinabstimmung und komplexe Suchszenarien ermöglicht.

## Warum GroupDocs.Search für Java verwenden?
- **Hohe Leistung** bei großen Dokumentenmengen – es kann 500 GB Text in weniger als einer Minute auf einem Standard‑Server indexieren und durchsuchen.  
- **Umfangreiche API**, die sowohl textbasierte als auch objektbasierte Abfragen unterstützt und Ihnen ermöglicht, den Stil zu wählen, der zu Ihrer Architektur passt.  
- **Integrierte Sprachunterstützung** für Stemming, Stoppwörter und unscharfe Suche in über 30 Sprachen.  
- **Einfache Integration** mit Maven oder direktem JAR‑Download, erfordert nur wenige Code‑Zeilen zum Starten.

## Voraussetzungen
Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:
- **GroupDocs.Search for Java** (v25.4 oder neuer) – siehe den Download‑Link unten.  
- JDK 8+ installiert und in Ihrer IDE (IntelliJ IDEA, Eclipse usw.) konfiguriert.  
- Grundkenntnisse in Java und Maven für das Abhängigkeits‑Management.  

## Einrichtung von GroupDocs.Search für Java

### Maven‑Einrichtung
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
Alternativ laden Sie das neueste JAR von der offiziellen Seite herunter: [GroupDocs.Search für Java Releases](https://releases.groupdocs.com/search/java/).

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

## Wie erstelle ich boolean query java?
Die Klasse `Index` repräsentiert eine durchsuchbare Sammlung von Dokumenten, die auf der Festplatte gespeichert ist. Ein `BooleanQuery` kombiniert mehrere Unterabfragen mit logischen Operatoren. `createAndQuery`, `createOrQuery` und `createNotQuery` erstellen AND-, OR- bzw. NOT‑Unterabfragen. Laden oder erstellen Sie eine `Index`‑Instanz, fügen Sie Dokumente hinzu und bauen Sie anschließend ein `BooleanQuery`‑Objekt mit `createAndQuery`, `createOrQuery` oder `createNotQuery` auf. Rufen Sie `index.search(query)` auf, um passende Dokumente zu erhalten. Dieses Muster funktioniert sowohl für einfache als auch komplexe Szenarien und erfordert nur drei logische Schritte: Indexinitialisierung, Dokumenten‑Hinzufügen und Abfrageausführung.

## Boolesche AND‑Suche

### Übersicht
Eine AND‑Abfrage reduziert die Ergebnisse und verbessert die Relevanz, wenn Sie Dokumente benötigen, die mehrere Kriterien erfüllen.

### Implementierungsschritte

1. **Index initialisieren** – dies demonstriert außerdem **Dokumente zum Index hinzufügen** für das AND‑Szenario.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Dokumente indexieren**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Textabfrage‑Suche ausführen** – unter Verwendung der einfachen String‑Syntax.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Objektabfrage‑Suche ausführen** – nützlich beim programmatischen Aufbau von Abfragen (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Boolesche OR‑Suche

### Übersicht
Eine OR‑Abfrage ist ideal für explorative Suchen, bei denen Sie Dokumente erfassen möchten, die mindestens eines mehrerer Schlüsselwörter enthalten (**search with or java**).

### Implementierungsschritte

1. **Index initialisieren**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Dokumente indexieren**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Textabfrage‑Suche ausführen**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Objektabfrage‑Suche ausführen**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Boolesche NOT‑Suche

### Übersicht
Eine NOT‑Abfrage hilft Ihnen, irrelevante Dokumente zu entfernen, z. B. das Filtern des Markennamens eines Konkurrenten (**boolean search examples java**).

### Implementierungsschritte

1. **Index initialisieren**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Dokumente indexieren**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Textabfrage‑Suche ausführen**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Objektabfrage‑Suche ausführen**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## Komplexe boolesche Abfragen

### Übersicht
Komplexe Abfragen ermöglichen es, reale Suchszenarien abzubilden, z. B. „Finde Sportartikel, die positiv sind, aber jede Erwähnung bestimmter Athleten ausschließen“.

### Implementierungsschritte

1. **Index initialisieren**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Dokumente indexieren**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Textabfrage‑Suche ausführen**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Objektabfrage‑Suche ausführen**

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

## Praktische Anwendungen von **java boolean and or** Abfragen
- **Document Management Systems** – finden Sie Verträge, die sowohl „confidential“ **AND** „renewal“ enthalten.  
- **Legal Research** – filtern Sie Rechtsprechung mit **AND**/**OR**, während Sie veraltete Gesetze mit **NOT** ausschließen.  
- **Customer Support** – rufen Sie Tickets ab, die „login“ **AND** „error“ erwähnen, aber nicht „resolved“.  
- **Content Curation** – sammeln Sie Blog‑Posts über „cloud“ **OR** „serverless“ für einen Newsletter.

## Häufige Fallstricke & Fehlersuche
- **Fehlende Index‑Aktualisierung** – nach dem Hinzufügen neuer Dokumente rufen Sie `index.update()` auf, um sicherzustellen, dass sie durchsuchbar sind.  
- **Falsche Operator‑Abstände** – GroupDocs.Search erwartet Leerzeichen um die Operatoren (`AND`, `OR`, `NOT`).  
- **Groß‑/Kleinschreibung** – Abfragen sind standardmäßig case‑insensitive, aber benutzerdefinierte Analyzer können dies beeinflussen.  
- **Große Ergebnismengen** – verwenden Sie Paginierung (`search(query, 0, 100)`), um Speicherüberlastungen zu vermeiden.  

## Häufig gestellte Fragen

**F: Kann ich mehr als zwei Begriffe in einer AND‑Abfrage kombinieren?**  
A: Absolut. Sie können mehrere `createWordQuery`‑Objekte mit `createAndQuery` verketten oder einfach `"term1 AND term2 AND term3"` in der Textabfrage schreiben.

**F: Unterstützt GroupDocs.Search Platzhalter‑ oder unscharfe Suchen?**  
A: Ja. Hängen Sie `*` für einen Platzhalter an (z. B. `promot*`) oder verwenden Sie `~` für unscharfe Übereinstimmung (z. B. `comfort~`).

**F: Wie begrenze ich die Suche auf bestimmte Dateitypen?**  
`FileTypeQuery` begrenzt die Suchergebnisse auf bestimmte Dateiformate wie PDF oder DOCX.  
A: Verwenden Sie die Klasse `FileTypeQuery`, um Ergebnisse auf PDFs, DOCX usw. zu beschränken und kombinieren Sie sie mit Ihrer booleschen Abfrage.

**F: Was ist der beste Weg, die Indexierungs‑Performance zu überwachen?**  
A: Aktivieren Sie den integrierten Logger (`index.getLogger().setLevel(Level.INFO)`) und prüfen Sie die Zeitmessungen nach jedem `add`‑Vorgang.

**F: Gibt es eine Möglichkeit, die Relevanz bestimmter Begriffe zu erhöhen?**  
`BoostQuery` erhöht den Relevanz‑Score der angegebenen Begriffe in einer Suchabfrage.  
A: Ja. Umschließen Sie wichtige Wörter mit `BoostQuery`, um ihr Gewicht im Scoring‑Algorithmus zu erhöhen.

---

**Zuletzt aktualisiert:** 2026-07-21  
**Getestet mit:** GroupDocs.Search 25.4 (Java)  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Boolesche Operatoren Java – Suchindex erstellen & facettierte Suche](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Master GroupDocs.Search Java: Effiziente Dokumentensuche und Indexverwaltung](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java – GroupDocs.Search Java meistern – Suchindex erstellen und verwalten](/search/java/indexing/groupdocs-search-java-create-index-guide/)