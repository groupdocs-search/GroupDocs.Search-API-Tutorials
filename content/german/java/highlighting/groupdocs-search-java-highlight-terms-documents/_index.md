---
date: '2025-12-26'
description: Erfahren Sie, wie Sie mit GroupDocs.Search für Java Text in Dokumenten
  suchen und hervorheben. Entdecken Sie Techniken zur Hervorhebung von gesamten Dokumenten
  und Fragmenten.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Suche und Hervorhebung von Text mit GroupDocs.Search für Java
type: docs
url: /de/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Suche und Hervorhebung von Text in Dokumenten mit GroupDocs.Search für Java

Im heutigen digitalen Zeitalter ist **search and highlight text** über massive Dokumentensammlungen hinweg eine gängige Anforderung. Egal, ob Sie ein Tool zur juristischen Überprüfung, ein akademisches Forschungsportal oder ein Kunden‑Support‑Dashboard erstellen, die Möglichkeit, Schlüsselbegriffe sofort zu finden und hervorzuheben, verbessert die Benutzerfreundlichkeit erheblich. In diesem umfassenden Leitfaden erfahren Sie, wie Sie **search and highlight text** mit GroupDocs.Search für Java implementieren – sowohl die Hervorhebung des gesamten Dokuments als auch die fragmentbasierte Hervorhebung für fokussierten Kontext.

## Schnelle Antworten
- **Was bedeutet “search and highlight text”?** Es bezieht sich auf das Auffinden von Suchbegriffen in einem Dokument und deren visuelle Hervorhebung (z. B. mit Hintergrundfarbe).  
- **Welche Bibliothek bietet diese Fähigkeit?** GroupDocs.Search für Java.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion ist für die Evaluierung ausreichend; für die Produktion ist eine Voll‑Lizenz erforderlich.  
- **Kann ich die Hervorhebungsfarben anpassen?** Ja – jede RGB‑Farbe kann über `HighlightOptions` festgelegt werden.  
- **Wird fragmentbasierte Hervorhebung unterstützt?** Absolut; Sie können Begriffe vor/nach dem Treffer definieren, um prägnante Ausschnitte zu erzeugen.

## Was ist search and highlight text?
search and highlight text ist der Vorgang, einen Dokumenten‑Index nach einer bestimmten Abfrage zu durchsuchen, passende Dokumente abzurufen und dann jedes Vorkommen des Suchbegriffs im Dokumentausgabeformat (HTML, PDF usw.) zu markieren. Dieser visuelle Hinweis hilft End‑Benutzern, relevante Informationen sofort zu erkennen.

## Warum GroupDocs.Search für Java verwenden?
- **High‑performance indexing** mit konfigurierbarer Kompression.  
- **Rich highlighting API**, die sowohl für ganze Dokumente als auch für benutzerdefinierte Fragmente funktioniert.  
- **Cross‑format support** (DOCX, PDF, PPTX, TXT und mehr).  
- **Einfache Maven‑Integration** und klare Java‑zentrierte API.

## Voraussetzungen
- Java Development Kit (JDK) 8 oder neuer.  
- Maven für das Abhängigkeitsmanagement.  
- Eine IDE wie IntelliJ IDEA oder Eclipse.  
- Grundlegende Kenntnisse der Java‑Syntax.

## Einrichtung von GroupDocs.Search für Java

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

Sie können das neueste JAR auch direkt von der offiziellen Seite herunterladen: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lizenzbeschaffung
Beginnen Sie mit einer kostenlosen Testversion oder erhalten Sie eine temporäre Lizenz für die Evaluierung. Für Produktionsumgebungen erwerben Sie eine Voll‑Lizenz, um alle Funktionen freizuschalten.

## Implementierungs‑Leitfaden

Die Implementierung ist in zwei praktische Abschnitte unterteilt: **highlighting in entire documents** und **highlighting in fragments**. Beide Abschnitte enthalten die wesentlichen Schritte, um **how to highlight Java** Dokumente mit GroupDocs.Search zu markieren.

### Konfiguration der Indexeinstellungen
Vor dem Indexieren konfigurieren Sie den Speicher, um hohe Kompression zu verwenden – dies reduziert den Festplattenverbrauch bei gleichzeitigem Erhalt der Suchgeschwindigkeit.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Hervorhebung in gesamten Dokumenten

#### Schritt 1: Index erstellen und befüllen
Erstellen Sie einen Indexordner und fügen Sie alle Quelldateien hinzu, die Sie durchsuchen möchten.

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
- **HighlightColor** – setzen Sie jeden RGB‑Wert, um Ihrer UI‑Palette zu entsprechen.  
- **UseInlineStyles** – `false` erzeugt sauberes HTML, das global mit CSS gestaltet werden kann.

### Hervorhebung in Fragmenten

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

## Praktische Anwendungen
1. **Legal Document Review** – sofort Gesetze, Klauseln oder Fallreferenzen hervorheben.  
2. **Academic Research** – Schlüsselterminologie in Dutzenden von PDFs und Word‑Dateien sichtbar machen.  
3. **Customer Support** – Bestellnummern oder Fehlercodes in Ticket‑Verläufen pinpointen.

## Leistungsüberlegungen
- **Index Size** – hohe Kompression (`Compression.High`) reduziert den Festplattenverbrauch.  
- **Fragment Context** – größere `termsBefore/After`‑Werte erhöhen die Genauigkeit, können jedoch die Geschwindigkeit beeinflussen.  
- **Memory Management** – überwachen Sie den JVM‑Heap beim Indexieren großer Korpora; erwägen Sie inkrementelles Indexieren für sehr große Mengen.

## Häufige Probleme und Lösungen
- **Indexing Errors** – prüfen Sie die Dateipfade und stellen Sie sicher, dass die Anwendung Lese‑/Schreibrechte hat.  
- **No Highlights Appear** – bestätigen Sie, dass `UseInlineStyles` zu Ihrem Ausgabeformat passt (HTML vs. PDF).  
- **Color Not Applied** – stellen Sie sicher, dass die RGB‑Werte im Bereich 0‑255 liegen und dass der HTML‑Viewer den Stil unterstützt.

## Häufig gestellte Fragen

**Q: What are the benefits of using GroupDocs.Search for Java?**  
A: Es bietet schnelle, skalierbare Indexierung, anpassbare Hervorhebung und Unterstützung für viele Dokumentformate.

**Q: How can I integrate GroupDocs.Search with a REST API?**  
A: Stellen Sie die Such‑ und Hervorhebungs‑Methoden über Spring‑Boot‑Controller bereit und geben Sie HTML‑ oder JSON‑Payloads zurück.

**Q: Does the library handle password‑protected files?**  
A: Ja – geben Sie das Passwort beim Hinzufügen des Dokuments zum Index an.

**Q: Can I customize the highlight markup beyond color?**  
A: Absolut; Sie können CSS‑Klassen über `HighlightOptions` einfügen oder das HTML nach der Erzeugung anpassen.

**Q: What version was tested for this guide?**  
A: Der Code wurde gegen GroupDocs.Search 25.4 validiert.

---

**Zuletzt aktualisiert:** 2025-12-26  
**Getestet mit:** GroupDocs.Search 25.4  
**Autor:** GroupDocs