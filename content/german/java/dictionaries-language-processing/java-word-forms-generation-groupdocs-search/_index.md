---
date: '2026-02-21'
description: Lernen Sie, wie Sie Singular‑Plural‑Formen in Java mit der GroupDocs.Search‑API
  erzeugen. Erstellen Sie einen benutzerdefinierten Wortformen‑Provider für genaue
  Suche und Textanalyse.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Singular‑ und Pluralformen in Java mit GroupDocs.Search generieren
type: docs
url: /de/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Generieren von Singular‑Plural‑Formen in Java mit GroupDocs.Search

Wenn Sie **Singular‑Plural‑Formen in Java generieren** müssen, ist ein benutzerdefinierter Word‑Forms‑Provider der Schlüssel, damit Ihre Such‑ oder Textanalyse‑Engine jede Variation eines Begriffs versteht. In diesem Tutorial führen wir Sie Schritt für Schritt durch den Aufbau eines solchen Providers mit der GroupDocs.Search Java API, sodass Ihre Anwendung automatisch „cat“, „cats“, „city“ und „citis“ ohne zusätzlichen Aufwand abgleichen kann.

## Schnelle Antworten
- **Was macht ein Word‑Forms‑Provider?** Er erzeugt alternative Formen (Singular, Plural usw.) eines gegebenen Wortes, sodass Suchvorgänge alle Varianten abgleichen können.  
- **Welche Bibliothek wird benötigt?** GroupDocs.Search für Java (Version 25.4 oder neuer).  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion reicht für die Evaluierung; für den Produktionseinsatz ist eine permanente Lizenz erforderlich.  
- **Welche Java‑Version wird unterstützt?** JDK 8 oder höher.  
- **Wie viele Code‑Zeilen werden benötigt?** Etwa 30 Zeilen für eine einfache Provider‑Implementierung.

## Was ist das Feature „Create Word Forms Provider“?

Ein **create word forms provider**‑Komponente ist eine benutzerdefinierte Klasse, die `IWordFormsProvider` implementiert. Sie erhält ein Wort und gibt ein Array möglicher Formen zurück – Singular, Plural oder andere linguistische Varianten – basierend auf von Ihnen definierten Regeln. Dadurch kann der Suchindex „cat“ und „cats“ als äquivalent behandeln, was den Recall erhöht, ohne die Präzision zu beeinträchtigen.

## Warum GroupDocs.Search für die Wort‑Form‑Generierung verwenden?

- **Eingebaute Erweiterbarkeit:** Binden Sie Ihren eigenen Provider direkt in die Indexierungspipeline ein.  
- **Leistungsoptimiert:** Verarbeitet große Indexe effizient und Sie können Ergebnisse für zusätzliche Geschwindigkeit zwischenspeichern.  
- **Plattformübergreifende Unterstützung:** Die Konzepte gelten auch für .NET und andere Plattformen.

## Voraussetzungen

Bevor Sie den **create word forms provider** implementieren, stellen Sie sicher, dass Sie Folgendes haben:

- **Maven** installiert und ein JDK 8 oder neuer auf Ihrem Rechner eingerichtet.  
- Grundlegende Kenntnisse in der Java‑Entwicklung und der `pom.xml`‑Konfiguration von Maven.  
- Zugriff auf die GroupDocs.Search Java‑Bibliothek (Version 25.4 oder neuer).

## Einrichtung von GroupDocs.Search für Java

### Maven‑Konfiguration

Fügen Sie das Repository und die Abhängigkeit zu Ihrer `pom.xml`‑Datei genau wie unten gezeigt hinzu:

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

Alternativ können Sie das neueste JAR von der offiziellen Release‑Seite herunterladen: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Schritte zum Erwerb einer Lizenz

1. **Kostenlose Testversion:** Registrieren Sie sich für eine Testversion, um die Kernfunktionen zu erkunden.  
2. **Temporäre Lizenz:** Fordern Sie einen temporären Schlüssel für erweiterte Tests an.  
3. **Kauf:** Erwerben Sie eine kommerzielle Lizenz für uneingeschränkten Produktionseinsatz.

### Grundlegende Initialisierung und Einrichtung

Das folgende Snippet zeigt, wie ein Index erstellt wird – Ihr Ausgangspunkt zum Hinzufügen von Dokumenten und Wort‑Form‑Logik:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Implementierungs‑Leitfaden

Im Folgenden führen wir die Schritte zum **create word forms provider** aus, der einfache Singular‑zu‑Plural‑ und Plural‑zu‑Singular‑Transformationen verarbeitet.

### Implementierung des SimpleWordFormsProvider

#### Überblick
Unser benutzerdefinierter Provider wird:

- Entfernt das abschließende „es“ oder „s“, um eine Singularform zu schätzen.  
- Ändert ein abschließendes „y“ zu „is“, um eine Pluralform zu erzeugen (z. B. „city“ → „citis“).  
- Fügt „s“ und „es“ hinzu, um grundlegende Pluralkandidaten zu erzeugen.

#### Schritt 1 – Klassen‑Skelett erstellen

Beginnen Sie damit, eine Klasse zu definieren, die `IWordFormsProvider` implementiert. Lassen Sie die Import‑Anweisungen unverändert:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Schritt 2 – Implementierung von `getWordForms`

Fügen Sie die Methode hinzu, die die Liste möglicher Formen erstellt. Dieser Block enthält die Kernlogik; Sie können ihn später erweitern, um komplexere Regeln abzudecken.

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### Erklärung der Logik
- **Singularisierung:** Erkennt gängige Plural‑Suffixe (`es`, `s`) und entfernt sie, um das Grundwort zu approximieren.  
- **Pluralisierung:** Behandelt Substantive, die auf `y` enden, indem es es durch `is` ersetzt – eine einfache Regel, die für viele englische Wörter funktioniert.  
- **Suffix‑Anfügung:** Fügt `s` und `es` hinzu, um reguläre Pluralformen abzudecken, die durch die vorherigen Prüfungen möglicherweise nicht erfasst werden.

#### Fehlersuche‑Tipps
- **Groß‑/Kleinschreibung:** Die Methode verwendet `toLowerCase()` für den Vergleich, sodass „Cats“ und „cats“ gleich behandelt werden.  
- **Randfälle:** Wörter, die kürzer als die Suffix‑Länge sind, werden ignoriert, um die Rückgabe leerer Zeichenketten zu vermeiden.  
- **Performance:** Bei großen Vokabularen sollten Sie das Zwischenspeichern der Ergebnisse in einer `ConcurrentHashMap` in Betracht ziehen.

## Praktische Anwendungsfälle

Die Implementierung eines **create word forms provider** kann mehrere reale Szenarien verbessern:

1. **Suchmaschinen:** Benutzer, die „mouse“ eingeben, sollten auch Dokumente mit „mice“ finden. Ein Provider kann solche unregelmäßigen Formen erzeugen.  
2. **Textanalyse‑Tools:** Sentiment‑ oder Entity‑Extraktion wird zuverlässiger, wenn alle Wortvarianten erkannt werden.  
3. **Content‑Management‑Systeme:** Die automatische Tag‑Generierung kann Plural‑Synonyme einbeziehen, was SEO und interne Verlinkungen verbessert.

## Leistungs‑Überlegungen

Wenn Sie den Provider in ein Produktionssystem einbinden, beachten Sie folgende Tipps:

- **Häufig genutzte Formen zwischenspeichern:** Ergebnisse im Speicher ablegen, um dieselben Wörter nicht wiederholt neu zu berechnen.  
- **JVM‑Heap überwachen:** Große Indexe können den Speicherverbrauch erhöhen; passen Sie `-Xmx` entsprechend an.  
- **Effiziente Collections verwenden:** `ArrayList` funktioniert für kleine Mengen, aber bei Tausenden von Formen sollten Sie `HashSet` in Betracht ziehen, um Duplikate schnell zu entfernen.

**Best Practices**
- Halten Sie die Bibliothek aktuell, um von Performance‑Patches zu profitieren.  
- Profilieren Sie den Provider mit realistischen Abfrage‑Lasten, um Engpässe früh zu erkennen.

## Fazit

Sie haben nun gelernt, wie man **Singular‑Plural‑Formen in Java generiert** mithilfe eines benutzerdefinierten `SimpleWordFormsProvider` mit GroupDocs.Search. Diese leichte Komponente kann die Relevanz von Suchergebnissen und die Genauigkeit der linguistischen Analyse in vielen Anwendungen dramatisch verbessern.

**Nächste Schritte:**  
- Experimentieren Sie mit anspruchsvolleren linguistischen Regeln (unregelmäßige Plurale, Stemming).  
- Integrieren Sie den Provider in eine Indexierungspipeline und messen Sie Verbesserungen beim Recall.  
- Erkunden Sie weitere GroupDocs.Search‑Funktionen wie Synonym‑Wörterbücher und benutzerdefinierte Analyzer.

**Aufruf zum Handeln:** Versuchen Sie noch heute, den `SimpleWordFormsProvider` zu Ihrem eigenen Projekt hinzuzufügen und sehen Sie, wie er Ihr Sucherlebnis bereichert!

## FAQ‑Abschnitt

**1. Was ist GroupDocs.Search für Java?**  
Es ist eine leistungsstarke Bibliothek, die Volltextsuche, Indexierung und linguistische Funktionen bietet – einschließlich der Möglichkeit, benutzerdefinierte Word‑Form‑Provider einzubinden.

**2. Wie funktioniert der SimpleWordFormsProvider?**  
Er erzeugt alternative Formen, indem er einfache suffixbasierte Regeln anwendet (Entfernen von „s/es“, Umwandlung von „y“ zu „is“ und Anfügen von „s/es“).

**3. Kann ich die Regeln zur Wort‑Form‑Generierung anpassen?**  
Ja. Ändern Sie die `getWordForms`‑Methode, um unregelmäßige Formen, lokalspezifische Regeln oder die Integration externer Wörterbücher einzubeziehen.

**4. Welche gängigen Anwendungsfälle gibt es für dieses Feature?**  
Suchmaschinen, Textanalyse‑Pipelines und CMS‑Plattformen profitieren davon, Singular‑/Plural‑Varianten zu erkennen.

**5. Benötige ich eine kommerzielle Lizenz für den Produktionseinsatz?**  
Ja – während eine Testversion Ihnen das Erkunden der API ermöglicht, entfernt eine gekaufte Lizenz Nutzungslimits und gewährt Support.

---

**Zuletzt aktualisiert:** 2026-02-21  
**Getestet mit:** GroupDocs.Search 25.4 (Java)  
**Autor:** GroupDocs