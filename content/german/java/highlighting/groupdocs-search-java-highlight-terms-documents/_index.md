---
date: '2026-02-27'
description: Erfahren Sie, wie Sie Text in Java mit GroupDocs.Search für Java hervorheben,
  einschließlich der Suche nach Dokumenten in Java, der Indexierung von Dokumenten
  in Java und der Fragmenthervorhebung.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Text in Java mit GroupDocs.Search hervorheben
type: docs
url: /de/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

 final content.

# Text in Java hervorheben mit GroupDocs.Search

In der heutigen schnelllebigen digitalen Umgebung ist es ein Muss, **Text in Java hervorzuheben** über große Dateisammlungen hinweg. Egal, ob Sie eine Plattform für juristische Prüfungen, eine akademische Recherche‑Engine oder eine Kunden‑Support‑Konsole bauen – das sofortige Erkennen der gesuchten Begriffe macht das Erlebnis deutlich effizienter. Dieses Tutorial führt Sie durch die Nutzung von **GroupDocs.Search for Java**, um **Dokumente java zu durchsuchen**, **Dokumente java zu indexieren** und reichhaltiges Hervorheben anzuwenden – sowohl für ganze Dokumente als auch für fokussierte Fragmente.

## Schnellantworten
- **Was bedeutet „Suche und Hervorhebung von Text“?** Es bezeichnet das Auffinden von Suchbegriffen in einem Dokument und deren visuelle Betonung (z. B. mit Hintergrundfarbe).  
- **Welche Bibliothek bietet diese Fähigkeit?** GroupDocs.Search for Java.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion reicht für die Evaluierung; für den Produktionseinsatz ist eine Voll‑Lizenz erforderlich.  
- **Kann ich die Hervorhebungsfarben anpassen?** Ja – jede RGB‑Farbe kann über `HighlightOptions` festgelegt werden.  
- **Wird Fragment‑Highlighting unterstützt?** Absolut; Sie können Begriffe vor und nach dem Treffer definieren, um kompakte Snippets zu erzeugen.

## Wie man Text in Java in Dokumenten hervorhebt
Das Hervorheben von Text in Java umfasst drei Kernschritte:

1. **Indexieren Sie die Quelldateien**, damit sie schnell durchsucht werden können.  
2. **Führen Sie eine Abfrage** gegen den Index aus, um passende Dokumente zu finden.  
3. **Rendern Sie die Ergebnisse mit visuellen Hinweisen** mithilfe der Highlighter‑API.

Im Folgenden betrachten wir jeden Schritt im Detail, zuerst für die Ausgabe des gesamten Dokuments und anschließend für Snippets auf Fragment‑Ebene.

## Was ist Suche und Hervorhebung von Text?
Suche und Hervorhebung von Text ist der Prozess, einen Dokumenten‑Index nach einer vorgegebenen Abfrage zu durchsuchen, passende Dokumente abzurufen und anschließend jedes Vorkommen des Suchbegriffs im Dokumentenausgabeformat (HTML, PDF usw.) zu markieren. Dieser visuelle Hinweis hilft End‑Benutzern, relevante Informationen sofort zu erkennen.

## Warum GroupDocs.Search for Java verwenden?
- **Hoch‑leistungsfähiges Indexieren** mit konfigurierbarer Kompression (`index documents java`).  
- **Umfangreiche Highlight‑API**, die sowohl auf ganze Dokumente als auch auf benutzerdefinierte Fragmente (`highlight search terms java`) angewendet werden kann.  
- **Cross‑Format‑Unterstützung** (DOCX, PDF, PPTX, TXT und mehr).  
- **Einfache Maven‑Integration** und ein klares, Java‑zentriertes Design.

## Voraussetzungen
- Java Development Kit (JDK) 8 oder neuer.  
- Maven für das Dependency‑Management.  
- Eine IDE wie IntelliJ IDEA oder Eclipse.  
- Grundlegende Vertrautheit mit Java‑Syntax.

## GroupDocs.Search for Java einrichten

Fügen Sie das GroupDocs‑Repository und die Abhängigkeit zu Ihrer `pom.xml` hinzu:

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

Sie können das aktuelle JAR auch direkt von der offiziellen Seite herunterladen: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lizenzbeschaffung
Beginnen Sie mit einer kostenlosen Testversion oder erhalten Sie eine temporäre Lizenz für die Evaluierung. Für Produktions‑Deployments erwerben Sie eine Voll‑Lizenz, um alle Funktionen freizuschalten.

## Implementierungs‑Leitfaden

Die Implementierung ist in zwei praktische Abschnitte unterteilt: **Hervorheben in gesamten Dokumenten** und **Hervorheben in Fragmenten**. Beide Abschnitte enthalten die wesentlichen Schritte, **wie man Java‑Dokumente** mit GroupDocs.Search hervorhebt.

### Konfiguration der Index‑Einstellungen
Vor dem Indexieren konfigurieren Sie den Speicher, um hohe Kompression zu nutzen – das reduziert den Festplattenverbrauch bei gleichbleibender Suchgeschwindigkeit.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Hervorheben in gesamten Dokumenten

#### Schritt 1: Index erstellen und befüllen
Erzeugen Sie einen Index‑Ordner und fügen Sie alle Quell‑Dateien hinzu, die Sie durchsuchen möchten.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Schritt 2: Suche ausführen und Hervorhebung anwenden
Suchen Sie nach dem Begriff (z. B. `ipsum`) und erzeugen Sie eine HTML‑Datei mit hervorgehobenen Treffern.

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

**Wichtige Optionen erklärt**  
- **Compression** – hohe Kompression spart Speicherplatz.  
- **HighlightColor** – setzen Sie jeden RGB‑Wert, der zu Ihrer UI‑Palette passt.  
- **UseInlineStyles** – `false` erzeugt sauberes HTML, das global per CSS gestaltet werden kann.  

### Hervorheben in Fragmenten

#### Schritt 1: Indexieren und Suchen (wie oben)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Schritt 2: Fragment‑Kontext definieren und hervorheben
Geben Sie an, wie viele Begriffe vor und nach dem Treffer in jedem Fragment erscheinen sollen.

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

#### Schritt 3: Hervorgehobene Fragmente abrufen und schreiben
Sammeln Sie die erzeugten Fragmente und schreiben Sie sie in eine HTML‑Datei.

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

## Praktische Anwendungsfälle
1. **Juristische Dokumentenprüfung** – sofortige Hervorhebung von Gesetzen, Klauseln oder Fallreferenzen.  
2. **Akademische Forschung** – Schlüsselbegriffe über Dutzende PDFs und Word‑Dateien hinweg sichtbar machen.  
3. **Kunden‑Support** – Bestellnummern oder Fehlercodes innerhalb von Ticket‑Verläufen schnell finden.

## Leistungs‑Überlegungen
- **Indexgröße** – hohe Kompression (`Compression.High`) reduziert den Festplatten‑Footprint.  
- **Fragment‑Kontext** – größere Werte für `termsBefore/After` erhöhen die Genauigkeit, können jedoch die Geschwindigkeit beeinflussen.  
- **Speicherverwaltung** – überwachen Sie den JVM‑Heap beim Indexieren großer Korpora; erwägen Sie inkrementelles Indexieren für sehr große Mengen.

## Häufige Probleme und Lösungen
- **Indexierungsfehler** – prüfen Sie Dateipfade und stellen Sie sicher, dass die Anwendung Lese‑/Schreibrechte hat.  
- **Keine Hervorhebungen sichtbar** – vergewissern Sie sich, dass `UseInlineStyles` zu Ihrem Ausgabeformat (HTML vs. PDF) passt.  
- **Farbe wird nicht angewendet** – stellen Sie sicher, dass die RGB‑Werte im Bereich 0‑255 liegen und dass der HTML‑Viewer den Stil unterstützt.

## Häufig gestellte Fragen

**F: Welche Vorteile bietet GroupDocs.Search for Java?**  
A: Es liefert schnelles, skalierbares Indexieren, anpassbare Hervorhebung und Unterstützung für zahlreiche Dokumentformate.

**F: Wie kann ich GroupDocs.Search in eine REST‑API integrieren?**  
A: Stellen Sie die Such‑ und Hervorhebungs‑Methoden über Spring‑Boot‑Controller bereit und geben Sie HTML‑ oder JSON‑Payloads zurück.

**F: Unterstützt die Bibliothek passwortgeschützte Dateien?**  
A: Ja – übergeben Sie das Passwort beim Hinzufügen des Dokuments zum Index.

**F: Kann ich das Hervorhebungs‑Markup über die Farbe hinaus anpassen?**  
A: Absolut; Sie können CSS‑Klassen über `HighlightOptions` einfügen oder das HTML nach der Generierung modifizieren.

**F: Welche Version wurde für diesen Leitfaden getestet?**  
A: Der Code wurde gegen GroupDocs.Search 25.4 validiert.

**F: Wie setze ich Highlight‑Optionen in Java, um eine CSS‑Klasse statt Inline‑Styles zu verwenden?**  
A: Setzen Sie `options.setUseInlineStyles(false)` und fügen Sie eine CSS‑Regel für die Klasse hinzu, die Sie über `options.setCssClass("myHighlight")` zuweisen.

**F: Gibt es eine Möglichkeit, Begriffe in PDF‑Dateien direkt in Java hervorzuheben?**  
A: Ja – GroupDocs.Search arbeitet mit PDF‑Eingaben, und der Highlighter erzeugt HTML, das Sie in einem PDF‑Viewer einbetten oder mit GroupDocs.Conversion zurück in PDF konvertieren können.

---

**Zuletzt aktualisiert:** 2026-02-27  
**Getestet mit:** GroupDocs.Search 25.4  
**Autor:** GroupDocs