---
date: '2025-12-20'
description: Erfahren Sie, wie Sie einen Wortformen‑Provider in Java mit GroupDocs.Search
  erstellen. Generieren Sie Singular‑ und Pluralformen für die Suche, Textanalyse
  und mehr.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Word-Formularanbieter in Java mit der GroupDocs.Search-API erstellen
type: docs
url: /de/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Word Forms Provider in Java mit der GroupDocs.Search API erstellen

Wörter vom Singular in den Plural – oder umgekehrt – zu transformieren, ist ein häufiges Hindernis beim Aufbau sprachbewusster Anwendungen. In diesem Leitfaden werden Sie **create word forms provider** mit der GroupDocs.Search Java API erstellen, wodurch Ihre Suchmaschine oder Ihr Textanalyse‑Tool die Fähigkeit erhält, verschiedene Wortvarianten automatisch zu verstehen und zuzuordnen.

Egal, ob Sie eine Suchmaschine, ein Content‑Management‑System oder irgendeine Java‑Anwendung entwickeln, die natürliche Sprache verarbeitet, das Beherrschen der Wort‑Form‑Generierung macht Ihre Ergebnisse genauer und Ihre Nutzer zufriedener. Lassen Sie uns die Voraussetzungen untersuchen, die vor dem Start nötig sind.

## Schnelle Antworten
- **What does a word forms provider do?** Es erzeugt alternative Formen (Singular, Plural usw.) eines gegebenen Wortes, sodass Suchvorgänge alle Varianten abdecken können.  
- **Which library is required?** GroupDocs.Search for Java (Version 25.4 oder neuer).  
- **Do I need a license?** Eine kostenlose Testversion reicht für die Evaluierung; für die Produktion ist eine permanente Lizenz erforderlich.  
- **What Java version is supported?** JDK 8 oder höher.  
- **How many lines of code are needed?** Etwa 30 Zeilen für eine einfache Provider‑Implementierung.

## Was ist das Feature “Create Word Forms Provider”?
Eine **create word forms provider**‑Komponente ist eine benutzerdefinierte Klasse, die `IWordFormsProvider` implementiert. Sie erhält ein Wort und gibt ein Array möglicher Formen – Singular, Plural oder andere linguistische Variationen – basierend auf von Ihnen definierten Regeln zurück. Dadurch kann der Suchindex „cat“ und „cats“ als äquivalent behandeln, was den Recall erhöht, ohne die Präzision zu beeinträchtigen.

## Warum GroupDocs.Search für die Wort‑Form‑Generierung verwenden?
- **Built‑in extensibility:** Sie können Ihren eigenen Provider direkt in die Indexierungspipeline einbinden.  
- **Performance‑optimized:** Die Bibliothek verarbeitet große Indexe effizient, und Sie können Ergebnisse für zusätzliche Geschwindigkeit zwischenspeichern.  
- **Cross‑language support:** Obwohl dieses Tutorial sich auf Java konzentriert, gelten die gleichen Konzepte für .NET und andere Plattformen.

## Voraussetzungen

Bevor Sie den **create word forms provider** implementieren, stellen Sie sicher, dass Sie Folgendes haben:

- **Maven** installiert und ein JDK 8 oder neuer auf Ihrem Rechner eingerichtet.  
- Grundlegende Kenntnisse in Java‑Entwicklung und der `pom.xml`‑Konfiguration von Maven.  
- Zugriff auf die GroupDocs.Search Java‑Bibliothek (Version 25.4 oder später).

## Einrichtung von GroupDocs.Search für Java

### Maven-Konfiguration

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

Um GroupDocs.Search ohne Einschränkungen zu nutzen:

1. **Free Trial:** Melden Sie sich für eine Testversion an, um die Kernfunktionen zu erkunden.  
2. **Temporary License:** Fordern Sie einen temporären Schlüssel für erweiterte Tests an.  
3. **Purchase:** Erwerben Sie eine kommerzielle Lizenz für uneingeschränkten Produktionseinsatz.

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

Im Folgenden gehen wir die Schritte durch, um einen **create word forms provider** zu erstellen, der einfache Singular‑zu‑Plural‑ und Plural‑zu‑Singular‑Transformationen verarbeitet.

### Implementierung des SimpleWordFormsProvider

#### Überblick

Unser benutzerdefinierter Provider wird:

- Entfernt das abschließende „es“ oder „s“, um eine Singularform zu schätzen.  
- Ändert ein abschließendes „y“ zu „is“, um eine Pluralform zu erzeugen (z. B. „city“ → „citis“).  
- Fügt „s“ und „es“ hinzu, um grundlegende Pluralkandidaten zu erzeugen.

#### Schritt 1 – Erstellen des Klassengerüsts

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

- **Singularization:** Erkennt gängige Plural‑Suffixe (`es`, `s`) und entfernt sie, um das Grundwort zu approximieren.  
- **Pluralization:** Behandelt Substantive, die auf `y` enden, indem es durch `is` ersetzt, eine einfache Regel, die für viele englische Wörter funktioniert.  
- **Suffix Appending:** Fügt `s` und `es` hinzu, um reguläre Pluralformen abzudecken, die von den vorherigen Prüfungen nicht erfasst werden.

#### Fehlersuche‑Tipps

- **Case Sensitivity:** Die Methode verwendet `toLowerCase()` für den Vergleich, sodass „Cats“ und „cats“ gleich behandelt werden.  
- **Edge Cases:** Wörter, die kürzer als die Suffix‑Länge sind, werden ignoriert, um leere Zeichenketten zu vermeiden.  
- **Performance:** Bei großen Vokabularen sollten Sie das Zwischenspeichern der Ergebnisse in einer `ConcurrentHashMap` in Betracht ziehen.

## Praktische Anwendungen

Die Implementierung eines **create word forms provider** kann mehrere reale Anwendungsfälle verbessern:

1. **Search Engines:** Nutzer, die „mouse“ eingeben, sollten auch Dokumente mit „mice“ finden. Ein Provider kann solche unregelmäßigen Formen erzeugen.  
2. **Text Analysis Tools:** Sentiment‑ oder Entity‑Extraktion wird zuverlässiger, wenn alle Wortvarianten erkannt werden.  
3. **Content Management Systems:** Automatische Tag‑Generierung kann Plural‑Synonyme einbeziehen, was SEO und interne Verlinkungen verbessert.

## Leistungs‑Überlegungen

Wenn Sie den Provider in ein Produktionssystem einbinden, beachten Sie diese Tipps:

- **Cache Frequently Used Forms:** Speichern Sie Ergebnisse im Speicher, um dieselbe Wortverarbeitung nicht wiederholt zu berechnen.  
- **Monitor JVM Heap:** Große Indexe können den Speicherverbrauch erhöhen; passen Sie `-Xmx` entsprechend an.  
- **Use Efficient Collections:** `ArrayList` funktioniert für kleine Mengen, aber bei Tausenden von Formen sollten Sie `HashSet` in Betracht ziehen, um Duplikate schnell zu entfernen.

**Best Practices**

- Halten Sie die Bibliothek auf dem neuesten Stand, um von Performance‑Patches zu profitieren.  
- Profilieren Sie den Provider mit realistischen Abfrage‑Lasten, um Engpässe frühzeitig zu erkennen.  

## Fazit

Sie haben nun gelernt, wie man mit GroupDocs.Search für Java einen **create word forms provider** erstellt. Diese leichte Komponente kann die Relevanz von Suchergebnissen und die Genauigkeit der linguistischen Analyse in vielen Anwendungen erheblich verbessern.

**Nächste Schritte:**  
- Experimentieren Sie mit anspruchsvolleren linguistischen Regeln (unregelmäßige Plurale, Stemming).  
- Integrieren Sie den Provider in eine Indexierungspipeline und messen Sie Verbesserungen des Recalls.  
- Erkunden Sie weitere GroupDocs.Search‑Funktionen wie Synonym‑Wörterbücher und benutzerdefinierte Analyzer.

**Call to Action:** Versuchen Sie noch heute, den `SimpleWordFormsProvider` zu Ihrem eigenen Projekt hinzuzufügen, und sehen Sie, wie er Ihre Suche verbessert!

## FAQ‑Abschnitt

**1. What is GroupDocs.Search for Java?**  
Es ist eine leistungsstarke Bibliothek, die Volltextsuche, Indexierung und linguistische Funktionen bietet – einschließlich der Möglichkeit, benutzerdefinierte word‑form‑Provider einzubinden.

**2. How does the SimpleWordFormsProvider work?**  
Es erzeugt alternative Formen, indem es einfache suffixbasierte Regeln anwendet (Entfernen von „s/es“, Umwandlung von „y“ zu „is“ und Anhängen von „s/es“).

**3. Can I customize the word form generation rules?**  
Absolut. Ändern Sie die `getWordForms`‑Methode, um unregelmäßige Formen, länderspezifische Regeln oder die Integration externer Wörterbücher einzubeziehen.

**4. What are some common applications for this feature?**  
Suchmaschinen, Text‑Analyse‑Pipelines und CMS‑Plattformen profitieren davon, Singular‑/Plural‑Varianten zu erkennen.

**5. Do I need a commercial license for production use?**  
Ja – während eine Testversion Ihnen das Erkunden der API ermöglicht, entfernt eine gekaufte Lizenz Nutzungslimits und gewährt Support.

---

**Last Updated:** 2025-12-20  
**Tested With:** GroupDocs.Search 25.4 (Java)  
**Author:** GroupDocs  

---