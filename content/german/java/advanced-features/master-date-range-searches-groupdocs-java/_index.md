---
date: '2026-10-07'
description: Erfahren Sie, wie Sie custom date format java‑Suchen mit GroupDocs implementieren,
  einschließlich date range queries, custom patterns und performance tips.
keywords:
- custom date format java
- search documents by date
- date range query example
- optimize search performance
- configure custom date pattern
lastmod: '2026-10-07'
og_description: Custom date format java tutorial zeigt, wie man GroupDocs.Search für
  Java konfiguriert, date range queries ausführt und die performance steigert. Folgen
  Sie step‑by‑step examples.
og_image_alt: Guide illustrating custom date format java usage in GroupDocs Search
og_title: Custom date format java – guide to date range search mit GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-07'
  description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  headline: Custom date format java | date range search with GroupDocs
  type: TechArticle
- description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  name: Custom date format java | date range search with GroupDocs
  steps:
  - name: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
    text: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
  - name: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
    text: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
  - name: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
    text: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
  type: HowTo
- questions:
  - answer: Text form is quick and easy but limited to the default ISO format; object‑based
      queries let you supply `Date` objects and custom formats for greater flexibility.
    question: What is the difference between text form and object‑based date queries?
  - answer: Yes, combine `daterange` clauses with logical operators like `AND` or
      `OR` to build complex queries.
    question: Can I search for multiple date ranges in a single query?
  - answer: There is a minor overhead for additional parsing, but the impact is negligible
      for typical workloads and is outweighed by the accuracy gains.
    question: Will custom date formats slow down the search?
  - answer: Absolutely. With proper indexing strategies and JVM tuning, it scales
      to millions of documents while maintaining sub‑second query response times.
    question: Is GroupDocs.Search suitable for large‑scale deployments?
  - answer: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
      for additional samples and use‑case implementations.
    question: Where can I find more Java examples?
  type: FAQPage
tags:
- custom date format
- GroupDocs.Search
- Java date handling
- document indexing
- search optimization
title: Custom date format java | date range search mit GroupDocs
type: docs
url: /de/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Benutzerdefiniertes Datumsformat java | Datumsspanne‑Suche mit GroupDocs

Die Suche nach Dokumenten nach Datum ist ein häufiges Anforderung—egal, ob Sie ein Archivsystem, ein Finanzberichts‑Tool oder ein Content‑Management‑Portal erstellen. In diesem Tutorial lernen Sie Techniken für **custom date format java** mit GroupDocs.Search, einschließlich Datumsspanne‑Abfragen, benutzerdefinierter MusterdDefinitionen und Tipps zur **optimize search performance**. Am Ende können Sie Benutzern ermöglichen, Datensätze abzurufen, die in einem beliebigen Datumsintervall liegen, unabhängig vom verwendeten Format.

## Schnelle Antworten
- **Was ist die primäre Klasse für die Indizierung?** `Index` aus dem Paket `com.groupdocs.search`.  
- **Wie definieren Sie ein benutzerdefiniertes Datums‑Muster?** Verwenden Sie `DateFormat` mit `DateFormatElement`‑Objekten und einem Trennzeichen.  
- **Kann ich mit einer Textabfrage suchen?** Ja, die Syntax `daterange(start ~~ end)` funktioniert direkt im Abfrage‑String.  
- **Welche Maven‑Koordinaten werden benötigt?** `com.groupdocs:groupdocs-search:25.4` (oder neuer).  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Test‑ oder temporäre Lizenz reicht für Tests aus; für die Produktion ist eine kommerzielle Lizenz erforderlich.

## Was ist custom date format java?
Custom date format java teilt GroupDocs.Search mit, wie Datumszeichenketten zu interpretieren sind, die nicht dem Standard‑ISO‑Muster (YYYY‑MM‑DD) entsprechen. Durch die Definition eines eigenen Musters—wie `MM/dd/yyyy` oder `dd‑MM‑yyyy`—ermöglichen Sie der Engine, Datumsangaben in Dokumenten zu erkennen, die regionale oder veraltete Formate verwenden. Diese Fähigkeit erlaubt es, Datumsangaben konsistent über heterogene Quellen zu indizieren und abzufragen, wodurch sowohl Recall als auch Präzision bei datumszentrierten Suchen verbessert werden.

## Warum GroupDocs.Search für Datumsspanne‑Abfragen verwenden?
GroupDocs.Search kombiniert Hochgeschwindigkeits‑Indexierung mit flexibler Abfragekonstruktion und ist damit ideal für Datumsspanne‑Szenarien. Die Engine kann schnell Dokumente finden, die Datumsangaben innerhalb eines angegebenen Intervalls enthalten, selbst wenn diese Daten im Freitext oder in Metadatenfeldern erscheinen. Die integrierte Unterstützung mehrerer Dateiformate und anpassbarer Datumsparser ermöglicht es, unterschiedliche Dokumentsammlungen zu verarbeiten, ohne format­spezifischen Code zu schreiben, und dennoch Sub‑Sekunden‑Antwortzeiten bei großen Indizes zu erreichen.

## Wie man Dokumente nach Datum mit GroupDocs.Search sucht
Sie richten die Bibliothek ein, indexieren einen Beispielordner und führen dann sowohl einfache Text‑Form‑Abfragen als auch umfangreichere objektbasierte Abfragen aus. Der Prozess beginnt mit der Erstellung einer `Index`‑Instanz, der Konfiguration aller benötigten benutzerdefinierten Datumsformate und anschließend dem Aufruf der Such‑API entweder mit einem einfachen String oder einer strukturierten `SearchQuery`. Dieser Ansatz ermöglicht es Ihnen, das Kontrollniveau zu wählen, das den Anforderungen Ihrer Anwendung entspricht.

### Voraussetzungen
- Java 8 oder neuer installiert.  
- Maven für die Abhängigkeitsverwaltung.  
- Zugriff auf eine GroupDocs.Search‑Lizenz (Test‑ oder temporäre Lizenz funktioniert für die Entwicklung).  

### Einrichtung von GroupDocs.Search für Java

#### Installation mit Maven
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

#### Direkter Download
Alternativ können Sie die neueste Version direkt von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunterladen.

#### Grundlegende Initialisierung und Einrichtung
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

**Definition anchor:** Die `Index`‑Klasse ist der Kerncontainer, der durchsuchbare Metadaten für jede hinzugefügte Datei speichert und schnelle Look‑ups über große Sammlungen ermöglicht.

## Feature 1: Erstellen von Datumsspanne‑Suchabfragen

### Verwendung von Text‑Form‑Abfrage
Der einfachste Weg ist, die Datumsspanne direkt in den Abfrage‑String einzubetten:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Direct answer:** Laden Sie Ihren Index und rufen Sie dann `search("daterange(2022-01-01 ~~ 2022-12-31)")` auf, um jedes Dokument abzurufen, dessen indiziertes Datum zwischen dem 1. Januar 2022 und dem 31. Dezember 2022 liegt. Diese Ein‑Zeilen‑Abfrage funktioniert sofort und liefert nach Relevanz sortierte Ergebnisse.

**Explanation:** Die `daterange`‑Syntax erwartet Datumsangaben im Format `YYYY‑MM‑DD`. Sie gibt alle Dokumente zurück, deren indizierte Daten innerhalb des Intervalls liegen.

### Verwendung von Abfrage‑Objekt
Für programmatische Kontrolle und benutzerdefiniertes Parsen erstellen Sie ein `SearchQuery`‑Objekt. Die Klasse `SearchQuery` repräsentiert eine strukturierte Abfrage, die mehrere Kriterien wie Schlüsselwörter, Filter und Datumsspannen kombinieren kann.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Direct answer:** Erstellen Sie ein `SearchQuery` mit `createDateRangeQuery(startDate, endDate)`, wobei `startDate` und `endDate` Instanzen von `java.util.Date` sind; übergeben Sie dann die Abfrage an `index.search(query)`, um präzise Ergebnisse zu erhalten, die Zeitzonen‑Offsets und lokalspezifische Kalender berücksichtigen.

**Definition anchor:** Die Klasse `SearchQuery` fasst alle Suchkriterien zusammen und ermöglicht es, Datumsspannen mit Schlüsselwort‑Filtern, Booleschen Operatoren und Boost‑Regeln zu kombinieren.

**Explanation:** `createDateRangeQuery` erlaubt die Angabe von `java.util.Date`‑Objekten und bietet volle Flexibilität bezüglich Zeitzonen und lokalspezifischer Handhabung.

## Feature 2: Angeben von custom date format java Mustern

### Festlegen benutzerdefinierter Datumsformate
Die Klasse `DateFormat` teilt der Engine mit, wie ein Datumsstring basierend auf der Reihenfolge der Elemente und Trennzeichenzeichen zu zerlegen und zu interpretieren ist. Definieren Sie ein `DateFormat`, das der Datumsdarstellung Ihres Dokuments entspricht:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Direct answer:** Löschen Sie die Standardformate mit `dateFormat.clear()`, fügen Sie dann ein neues `DateFormat` hinzu, das aus `DateFormatElement`‑Objekten (Monat, Tag, Jahr) aufgebaut ist, und setzen Sie das Trennzeichen auf `/`. Danach wird die Engine Datumsangaben im Format `MM/dd/yyyy` sowohl beim Indexieren als auch bei Abfragen korrekt parsen.

**Definition anchor:** `DateFormat` ist ein Konfigurationsobjekt, das GroupDocs.Search mitteilt, wie ein Datumsstring basierend auf der Reihenfolge der Elemente und Trennzeichen zu zerlegen und zu interpretieren ist.

**Explanation:** Durch das Löschen der Standardformate und das Hinzufügen eines `DateFormat`, das `/` als Trennzeichen verwendet, versteht die Engine nun Datumsangaben im Format `MM/dd/yyyy`. Dies ist entscheidend für **search documents by date** in Regionen, die die Monat‑zuerst‑Notation bevorzugen.

## Tipps zur Optimierung der Suchleistung
- **Index inkrementell:** Fügen Sie neue Dateien dem bestehenden Index hinzu, anstatt ihn von Grund auf neu zu erstellen; dies reduziert die CPU‑Auslastung um bis zu 70 % bei täglichen Updates.  
- **Veraltete Daten entfernen:** Entfernen Sie regelmäßig Dokumente, die nicht mehr benötigt werden; ein schlanker Index verbessert die Cache‑Trefferquote und reduziert die Abfrage‑Latenz.  
- **Speichereinstellungen anpassen:** Erhöhen Sie den JVM‑Heap (`-Xmx4g` oder höher), wenn Sie mit Indizes größer als 5 GB arbeiten, um Out‑of‑Memory‑Fehler zu vermeiden.  
- **Mehr‑Thread‑Indexierung aktivieren:** Verwenden Sie `IndexingOptions.setThreadCount(Runtime.getRuntime().availableProcessors())`, um die Dokumentenverarbeitung zu parallelisieren und die Indexierungszeit um etwa die Anzahl der CPU‑Kerne zu verkürzen.

## Häufige Probleme und Lösungen
- **Datums‑Parsing‑Fehler:** Stellen Sie sicher, dass die Datumszeichenketten im Dokument exakt dem von Ihnen definierten benutzerdefinierten Muster entsprechen; nicht passende Trennzeichen oder fehlende führende Nullen führen zu Fehlern.  
- **Fehlende Ergebnisse:** Vergewissern Sie sich, dass die indizierten Felder Datums‑Metadaten enthalten; hat ein Dokument Datumsangaben nur in Freitext‑Absätzen, aktivieren Sie die Option `ExtractDateMetadata` während der Indexierung.  
- **Index‑Zugriffs‑Ausnahmen:** Stellen Sie sicher, dass der Pfad `indexFolder` beschreibbar und nicht von einem anderen Prozess gesperrt ist; verwenden Sie für jede Umgebung (dev, test, prod) einen eigenen Ordner, um Konflikte zu vermeiden.

## Praktische Anwendungen
1. **Archivsysteme** – Abrufen von Datensätzen aus einem bestimmten historischen Zeitraum, ohne Datumsangaben manuell zu normalisieren.  
2. **Content‑Management** – Unterstützung regionaler Datumsformate wie `dd/MM/yyyy` für europäische Nutzer, was die Benutzerzufriedenheit erhöht.  
3. **Finanzsoftware** – Schnell Transaktionen nach Finanzquartal oder Jahr filtern, wodurch Echtzeit‑Reporting‑Dashboards ermöglicht werden.

## Warum das wichtig ist
Die Implementierung von **custom date format java**‑Verarbeitung beseitigt die Hürden beim Umgang mit inkonsistenten Datumsdarstellungen in Dokumenten. Sie ermöglicht es Ihnen, **handle multiple date formats** in einem einzigen Index zu unterstützen, sodass End‑Benutzer genaue Ergebnisse erhalten, unabhängig davon, wie die Daten ursprünglich erfasst wurden. Diese Flexibilität verbessert die Suchrelevanz, reduziert den Vorverarbeitungsaufwand und verkürzt die Time‑to‑Value für datumszentrierte Anwendungen.

## Nächste Schritte
- Erkunden Sie weiterführende Abfrage‑Kombinationen mit den Operatoren `AND`, `OR` und `NOT`.  
- Experimentieren Sie mit benutzerdefinierten Analyzer‑Klassen, falls Sie zusätzliche zeitliche Metadaten wie in XML‑Tags eingebettete Zeitstempel indexieren müssen.  
- Überprüfen Sie den Performance‑Tuning‑Leitfaden in der offiziellen Dokumentation, um Ihre Lösung für Millionen von Dokumenten und Multi‑Tenant‑Umgebungen zu skalieren.

## Häufig gestellte Fragen

**Q: Was ist der Unterschied zwischen Text‑Form‑ und objektbasierten Datumsabfragen?**  
A: Die Text‑Form ist schnell und einfach, aber auf das Standard‑ISO‑Format beschränkt; objektbasierte Abfragen ermöglichen die Angabe von `Date`‑Objekten und benutzerdefinierten Formaten für mehr Flexibilität.

**Q: Kann ich in einer einzigen Abfrage nach mehreren Datumsspannen suchen?**  
A: Ja, kombinieren Sie `daterange`‑Klauseln mit logischen Operatoren wie `AND` oder `OR`, um komplexe Abfragen zu erstellen.

**Q: Verlangsamen benutzerdefinierte Datumsformate die Suche?**  
A: Es gibt einen geringen Overhead für zusätzliches Parsen, aber die Auswirkung ist bei typischen Workloads vernachlässigbar und wird durch die Genauigkeitsgewinne übertroffen.

**Q: Ist GroupDocs.Search für groß angelegte Deployments geeignet?**  
A: Absolut. Mit geeigneten Indexierungsstrategien und JVM‑Optimierung skaliert es auf Millionen von Dokumenten und liefert Sub‑Sekunden‑Antwortzeiten bei Abfragen.

**Q: Wo finde ich weitere Java‑Beispiele?**  
A: Erkunden Sie das [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) für weitere Beispiele und Anwendungsfall‑Implementierungen.

---

**Ressourcen**
- **Dokumentation:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API-Referenz:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **GitHub-Repository:** [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Ansicht auf GitHub:** [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Kostenloses Support‑Forum:** [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Temporäre Lizenz:** [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

**Zuletzt aktualisiert:** 2026-10-07  
**Getestet mit:** GroupDocs.Search Java 25.4  
**Autor:** GroupDocs  

## Verwandte Tutorials

- [Groupdocs Search Java Erweiterte Suchfunktionen](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Java Volltext‑Suchbibliothek – Index optimieren mit GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Wie man Dokumente mit Metadaten‑Indexierung in Java zu einem Index hinzufügt, mit GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)