---
date: '2026-03-17'
description: Erfahren Sie, wie Sie mit GroupDocs.Search für Java einen Index erstellen,
  reguläre und gemischte Zeichen konfigurieren und die Suche nach juristischen Aktenzeichen
  und OCR‑Bildern optimieren.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Wie man einen Index mit Zeichenerkennung in Java erstellt
type: docs
url: /de/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

für‑Schritt‑Implementierung". Good.

Similarly for Feature 2.

We used "## Praktische Anwendungen". Good.

We used "### Anwendungsfall 1 – Verwaltung juristischer Dokumente". Good.

... etc.

Now produce final markdown.# Wie man einen Index mit Zeichenerkennung mit GroupDocs.Search für Java erstellt

In modernen, dokumentintensiven Anwendungen ist es entscheidend, **wie man einen Index erstellt**, der die Nuancen Ihres Textes berücksichtigt – wie Bindestriche, Unterstriche oder sprachspezifische Symbole – um eine schnelle, genaue Suche zu ermöglichen. In diesem Tutorial führen wir Sie durch die Konfiguration der Zeichenerkennung in **GroupDocs.Search for Java**, wobei sowohl reguläre Zeichen (Buchstaben, Ziffern, Unterstriche) als auch kombinierte Zeichen (z. B. Bindestriche) behandelt werden. Am Ende können Sie einen Index erstellen, der exakt auf die Anforderungen Ihres OCR‑ oder Bildsuch‑Szenarios zugeschnitten ist, egal ob Sie juristische Aktenzeichen, Quellcode‑Repositorys oder mehrsprachige PDFs indizieren.

## Schnellantworten
- **Was bedeutet „create custom search index“?** Es bedeutet, einen Index so zu konfigurieren, dass bestimmte Symbole als Buchstaben oder kombinierte Zeichen behandelt werden, anstatt sie zu ignorieren.  
- **Welche Bibliothek wird verwendet?** GroupDocs.Search for Java (v25.4 zum Zeitpunkt der Erstellung).  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine kostenpflichtige Lizenz erforderlich.  
- **Kann ich sowohl PDFs als auch Bilder indizieren?** Ja – GroupDocs.Search unterstützt OCR für Bilder und PDFs, wenn es korrekt konfiguriert ist.  
- **Ist Maven erforderlich?** Maven ist der empfohlene Weg zur Verwaltung von Abhängigkeiten, aber Sie können auch Gradle oder manuelle JARs verwenden.

## Was ist ein benutzerdefinierter Suchindex?
Ein benutzerdefinierter Suchindex ermöglicht es Ihnen festzulegen, wie die Suchmaschine Zeichen interpretiert. Standardmäßig werden viele Symbole ignoriert, was zu verpassten Treffern bei z. B. Aktenzeichen (`2023-AB-456`) oder Code‑Snippets (`my_variable`) führen kann. Durch Anpassen des Alphabet‑Wörterbuchs erhalten Sie die volle Kontrolle darüber, was die Engine als durchsuchbaren Text behandelt.

## Warum reguläre und kombinierte Zeichen für juristische Aktenzahlen konfigurieren?
- **Reguläre Zeichen** (Buchstaben, Ziffern, Unterstriche) werden separat tokenisiert, was exakte Übereinstimmungssuchen für Kennungen ermöglicht.  
- **Kombinierte Zeichen** (Bindestriche, Schrägstriche) halten zusammengehörige Token zusammen und verhindern ein unerwünschtes Aufteilen von Aktenzahlen, Produktcodes oder Dateipfaden.  
- Diese Konfiguration **optimiert die Leistung des Suchindexes**, indem sie Token‑Fragmentierung reduziert und die Relevanz für OCR‑generierten Inhalt verbessert.

## Voraussetzungen
- **JDK 8** oder höher installiert.  
- **Maven** zur Verwaltung von Abhängigkeiten.  
- Zugriff auf die **GroupDocs.Search for Java**‑Bibliothek (über Maven oder die offizielle Website heruntergeladen).  

### Erforderliche Bibliotheken und Abhängigkeiten
Fügen Sie die Repository‑ und Abhängigkeits‑Einträge zu Ihrer `pom.xml` hinzu (wie unten gezeigt). Der XML‑Block muss unverändert bleiben.

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

Sie können die neuesten JARs auch von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunterladen.

### Lizenzbeschaffung
- **Free Trial** – ideal für frühe Experimente.  
- **Temporary License** – nützlich für längere Entwicklungszyklen.  
- **Production License** – erforderlich für den kommerziellen Einsatz.  

Erhalten Sie eine Lizenz über das offizielle Portal: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Grundlegende Initialisierung
Das nachstehende Snippet zeigt den minimalen Code, der benötigt wird, um einen leeren Index zu erstellen. Belassen Sie es unverändert; wir werden später darauf aufbauen.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Einrichtung von GroupDocs.Search für Java

### Installation über Maven
Die Maven‑Konfiguration aus dem Abschnitt *Voraussetzungen* ist alles, was Sie benötigen. Nach dem Hinzufügen führen Sie `mvn clean install` aus, um die Binärdateien zu holen.

### Anforderungen an die Umgebung
- Stellen Sie sicher, dass der **Index‑Ordner** und der **Dokument‑Ordner** auf der Festplatte existieren.  
- Verwenden Sie absolute Pfade oder konfigurieren Sie Ihre IDE so, dass relative Pfade korrekt aufgelöst werden.  

## Implementierungs‑Leitfaden

Im Folgenden gehen wir die beiden unterschiedlichen Funktionen durch: **reguläre Zeichen** und **kombinierte Zeichen**. Jede Funktion folgt dem gleichen Muster – Pfade definieren, den Index erstellen, das Zeichen‑Wörterbuch festlegen und schließlich Ihre Dokumente indizieren.

### Feature 1 – Reguläre Zeichen

#### Übersicht
Reguläre Zeichen werden als unabhängige Token behandelt. Das ist ideal, wenn Sie Ziffern, Buchstaben und Unterstriche exakt so durchsuchbar haben möchten, wie sie erscheinen.

#### Schritt‑für‑Schritt‑Implementierung

**1️⃣ Pfade festlegen**  
Definieren Sie, wo der Index gespeichert wird und wo sich Ihre Quelldokumente befinden.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Index erstellen und konfigurieren**  
Instanziieren Sie den Index und löschen Sie jede bereits vorhandene Alphabet‑Konfiguration.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Reguläre Zeichen definieren**  
Erstellen Sie ein Zeichen‑Array, das Ziffern, lateinische Buchstaben und den Unterstrich enthält.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Dokumente indizieren**  
Fügen Sie alle Dateien aus dem Quellordner dem neu konfigurierten Index hinzu.

```java
index.add(documentFolder);
```

### Feature 2 – Kombinierte Zeichen

#### Übersicht
Kombinierte Zeichen (wie Bindestriche) verbinden häufig zwei Wörter. Wenn sie als *blended* markiert werden, weist das die Engine an, die umgebenden Token während des Indexierens zusammenzuhalten.

#### Schritt‑für‑Schritt‑Implementierung

**1️⃣ Pfade festlegen**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Index erstellen und konfigurieren**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Kombinierte Zeichen definieren**  
Hier teilen wir dem Wörterbuch mit, dass der Bindestrich als kombiniertes Zeichen behandelt werden soll.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Dokumente indizieren**  

```java
index.add(documentFolder);
```

## Praktische Anwendungen

### Anwendungsfall 1 – Verwaltung juristischer Dokumente
Juristische Dateien enthalten oft Aktenzahlen wie `2023-AB-456`. Durch die Konfiguration von Unterstrichen und Bindestrichen liefern Suchvorgänge exakte Treffer, ohne die Kennung zu splitten, und unterstützen Sie dabei, **juristische Aktenzahlen** effizient zu durchsuchen.

### Anwendungsfall 2 – Quellcode‑Repositorys
Entwickler müssen Code‑Snippets durchsuchen, bei denen Unterstriche (`my_variable`) und Bindestriche (`my-function`) bedeutungsvoll sind. Benutzerdefinierte Zeichenerkennung stellt sicher, dass die Suchmaschine diese Symbole respektiert.

### Anwendungsfall 3 – Mehrsprachige Datensätze
Bei der Arbeit mit Sprachen, die zusätzliche Alphabete verwenden, können Sie den **Unicode‑Zeichensatz erweitern**, um diese Bereiche einzuschließen, und so genaue Suchergebnisse über Sprachgrenzen hinweg gewährleisten.

### Anwendungsfall 4 – PDF‑Bilder indizieren
Wenn Sie gescannte PDFs oder Bilddateien indizieren, enthält die OCR‑Ausgabe häufig gemischte Zeichen. Durch die korrekte Konfiguration von regulären und kombinierten Zeichen **optimieren Sie die Leistung des Suchindexes** für bildbasierte Inhalte.

## Leistungsüberlegungen

- **Ressourcenverwaltung** – Behalten Sie die Heap‑Nutzung im Auge; große Indexe profitieren von inkrementellen Commits.  
- **Garbage Collection** – Geben Sie `Index`‑Objekte frei, wenn sie nicht mehr benötigt werden, damit die JVM den Speicher zurückgewinnt.  
- **Index‑Optimierung** – Rufen Sie periodisch `index.optimize()` (falls verfügbar) auf, um den Index zu komprimieren und die Abfragegeschwindigkeit zu erhöhen.  

## Fazit

Sie wissen jetzt, **wie man einen Index erstellt**, der zwischen regulären und kombinierten Zeichen mit GroupDocs.Search for Java unterscheidet. Diese feinkörnige Kontrolle ermöglicht es Ihnen, OCR‑bewusste, leistungsstarke Suchlösungen zu bauen, die auf juristische, Entwicklungs‑ oder mehrsprachige Umgebungen zugeschnitten sind.

### Nächste Schritte
- Experimentieren Sie mit zusätzlichen Unicode‑Bereichen für nicht‑lateinische Alphabete.  
- Kombinieren Sie die Zeichenkonfiguration mit anderen GroupDocs.Search‑Funktionen wie Stemming oder Synonymen.  
- Integrieren Sie den Index in eine REST‑API, um Suchfunktionen Front‑End‑Anwendungen bereitzustellen.

## Häufig gestellte Fragen

**Q:** *Was ist der Zweck von `CharacterType.Letter`?*  
**A:** Es weist den Index an, die bereitgestellten Zeichen als reguläre Buchstaben zu behandeln, sodass sie beim Indexieren separat tokenisiert werden.

**Q:** *Kann ich reguläre und kombinierte Zeichen im selben Index mischen?*  
**A:** Ja – rufen Sie einfach `setRange` für jeden Typ auf; das Wörterbuch verarbeitet beide Konfigurationen gleichzeitig.

**Q:** *Muss ich den Index nach einer Änderung des Alphabets neu erstellen?*  
**A:** Auf jeden Fall. Änderungen am Zeichen‑Wörterbuch beeinflussen die Tokenisierung, daher müssen Sie die Dokumente neu indizieren, um die neuen Regeln anzuwenden.

**Q:** *Gibt es ein Limit für die Anzahl benutzerdefinierter Zeichen, die ich definieren kann?*  
**A:** Die Bibliothek unterstützt den gesamten Unicode‑Bereich; die Leistung kann sinken, wenn Sie ein extrem großes Set hinzufügen, daher sollten Sie es auf die tatsächlich benötigten Zeichen beschränken.

**Q:** *Wie wirkt sich das auf die OCR‑Genauigkeit aus?*  
**A:** Durch die Angleichung des Zeichen‑Sets des Index an die Ausgabe der OCR‑Engine reduzieren Sie Fehlnegative und verbessern die Gesamtrelevanz der Suche.

---

**Zuletzt aktualisiert:** 2026-03-17  
**Getestet mit:** GroupDocs.Search 25.4 für Java  
**Autor:** GroupDocs  

---