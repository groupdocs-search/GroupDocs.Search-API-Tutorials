---
date: '2026-01-11'
description: Erfahren Sie, wie Sie mit GroupDocs.Search für Java einen benutzerdefinierten
  Suchindex erstellen und reguläre sowie gemischte Zeichen für fortgeschrittene OCR‑
  und Bildsuche konfigurieren.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Erstellen eines benutzerdefinierten Suchindex mit Zeichenerkennung – GroupDocs.Search
  Java
type: docs
url: /de/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Erstellen eines benutzerdefinierten Suchindexes mit Zeichenerkennung mithilfe von GroupDocs.Search für Java

In modernen, dokumentintensiven Anwendungen ist **das Erstellen eines benutzerdefinierten Suchindexes**, der die Nuancen Ihres Textes versteht – wie Bindestriche, Unterstriche oder sprachspezifische Symbole – für schnelle, genaue Abrufe unerlässlich. Dieses Tutorial führt Sie durch die Konfiguration der Zeichenerkennung in **GroupDocs.Search für Java**, wobei sowohl reguläre Zeichen (Buchstaben, Ziffern, Unterstriche) als auch kombinierte Zeichen (z. B. Bindestriche) behandelt werden. Am Ende können Sie einen Index anpassen, der exakt den Anforderungen Ihres OCR‑ oder Bildsuch‑Szenarios entspricht.

## Schnelle Antworten
- **Was bedeutet „create custom search index“?** Es bedeutet, einen Index so zu konfigurieren, dass bestimmte Symbole als Buchstaben oder kombinierte Zeichen behandelt werden, anstatt sie zu ignorieren.  
- **Welche Bibliothek wird verwendet?** GroupDocs.Search für Java (v25.4 zum Zeitpunkt der Erstellung).  
- **Brauche ich eine Lizenz?** Eine kostenlose Testversion reicht für die Entwicklung; für die Produktion ist eine kostenpflichtige Lizenz erforderlich.  
- **Kann ich sowohl PDFs als auch Bilder indexieren?** Ja – GroupDocs.Search unterstützt OCR für Bilder und PDFs, wenn es korrekt konfiguriert ist.  
- **Ist Maven erforderlich?** Maven ist der empfohlene Weg zur Verwaltung von Abhängigkeiten, aber Sie können auch Gradle oder manuelle JARs verwenden.  

## Was ist ein benutzerdefinierter Suchindex?
Ein benutzerdefinierter Suchindex ermöglicht es Ihnen festzulegen, wie die Suchmaschine Zeichen interpretiert. Standardmäßig werden viele Symbole ignoriert, was zu verpassten Treffern bei z. B. Aktenzeichen (`ABC-123`) oder Code‑Snippets (`my_variable`) führen kann. Durch Anpassen des Alphabet‑Wörterbuchs erhalten Sie die volle Kontrolle darüber, was die Engine als durchsuchbaren Text behandelt.

## Warum reguläre und kombinierte Zeichen konfigurieren?
- **Reguläre Zeichen** (Buchstaben, Ziffern, Unterstriche) werden als eigenständige Token behandelt, was exakte Übereinstimmungen verbessert.  
- **Kombinierte Zeichen** (Bindestriche, Schrägstriche) verbinden Wörter; ihre Konfiguration verhindert ein unerwünschtes Aufteilen von Token, was für Rechtsreferenzen, Produktcodes oder die Indexierung von Quellcode entscheidend ist.  

## Voraussetzungen
- **JDK 8** oder höher installiert.  
- **Maven** für das Abhängigkeitsmanagement.  
- Zugriff auf die **GroupDocs.Search für Java**‑Bibliothek (heruntergeladen über Maven oder die offizielle Seite).  

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

Sie können die neuesten JARs auch von [GroupDocs.Search für Java Releases](https://releases.groupdocs.com/search/java/) herunterladen.

### Lizenzbeschaffung
- **Kostenlose Testversion** – ideal für frühe Experimente.  
- **Temporäre Lizenz** – nützlich für längere Entwicklungszyklen.  
- **Produktionslizenz** – für den kommerziellen Einsatz erforderlich.  

Erhalten Sie eine Lizenz über das offizielle Portal: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Grundlegende Initialisierung
Das untenstehende Snippet zeigt den minimalen Code, der benötigt wird, um einen leeren Index zu erstellen. Belassen Sie es unverändert; wir werden später darauf aufbauen.

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
- Stellen Sie sicher, dass der **Index‑Ordner** und der **Dokumenten‑Ordner** auf dem Datenträger existieren.  
- Verwenden Sie absolute Pfade oder konfigurieren Sie Ihre IDE so, dass relative Pfade korrekt aufgelöst werden.  

## Implementierungs‑Leitfaden

Im Folgenden gehen wir die beiden unterschiedlichen Funktionen durch: **reguläre Zeichen** und **kombinierte Zeichen**. Jede Funktion folgt demselben Muster – Pfade definieren, Index erstellen, das Zeichendictionary festlegen und schließlich die Dokumente indexieren.

### Feature 1 – Reguläre Zeichen

#### Überblick
Reguläre Zeichen werden als unabhängige Token behandelt. Das ist ideal, wenn Ziffern, Buchstaben und Unterstriche exakt so durchsuchbar sein sollen, wie sie erscheinen.

#### Schritt‑für‑Schritt‑Implementierung

**1️⃣ Pfade festlegen**  
Definieren Sie, wo der Index gespeichert wird und wo Ihre Quelldokumente liegen.

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

**4️⃣ Dokumente indexieren**  
Fügen Sie alle Dateien aus dem Quellordner dem neu konfigurierten Index hinzu.

```java
index.add(documentFolder);
```

### Feature 2 – Kombinierte Zeichen

#### Überblick
Kombinierte Zeichen (wie Bindestriche) verbinden häufig zwei Wörter. Wenn sie als *blended* markiert werden, weist das die Engine an, die umgebenden Token beim Indexieren zusammenzuhalten.

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

**4️⃣ Dokumente indexieren**  

```java
index.add(documentFolder);
```

## Praktische Anwendungen

### Anwendungsfall 1 – Verwaltung juristischer Dokumente
Juristische Dateien enthalten häufig Aktenzeichen wie `2023-AB-456`. Durch die Konfiguration von Unterstrichen und Bindestrichen liefern Suchvorgänge exakte Treffer, ohne den Bezeichner zu splitten.

### Anwendungsfall 2 – Quellcode‑Repositories
Entwickler müssen Code‑Snippets durchsuchen, bei denen Unterstriche (`my_variable`) und Bindestriche (`my-function`) bedeutungsvoll sind. Benutzerdefinierte Zeichenerkennung stellt sicher, dass die Suchmaschine diese Symbole respektiert.

### Anwendungsfall 3 – Mehrsprachige Datensätze
Wenn Sie mit Sprachen arbeiten, die zusätzliche Alphabete verwenden, können Sie das reguläre Zeichen‑Set erweitern, um diese Unicode‑Bereiche einzuschließen, und so genaue Suchergebnisse über Sprachgrenzen hinweg garantieren.

## Leistungs‑Überlegungen

- **Ressourcen‑Management** – Behalten Sie die Heap‑Nutzung im Auge; große Indexe profitieren von inkrementellen Commits.  
- **Garbage Collection** – Geben Sie `Index`‑Objekte frei, wenn sie nicht mehr benötigt werden, damit die JVM den Speicher zurückgewinnt.  
- **Index‑Optimierung** – Rufen Sie periodisch `index.optimize()` (falls verfügbar) auf, um den Index zu komprimieren und die Abfragegeschwindigkeit zu verbessern.  

## Fazit

Sie wissen jetzt, wie Sie **einen benutzerdefinierten Suchindex** erstellen, der zwischen regulären und kombinierten Zeichen mithilfe von GroupDocs.Search für Java unterscheidet. Diese feinkörnige Kontrolle ermöglicht es Ihnen, OCR‑bewusste, leistungsstarke Suchlösungen zu bauen, die auf juristische, Entwicklungs‑ oder mehrsprachige Umgebungen zugeschnitten sind.

**Nächste Schritte**
- Experimentieren Sie mit zusätzlichen Unicode‑Bereichen für nicht‑lateinische Alphabete.  
- Kombinieren Sie die Zeichenkonfiguration mit anderen GroupDocs.Search‑Funktionen wie Stemming oder Synonymen.  
- Integrieren Sie den Index in eine REST‑API, um Suchfunktionen Front‑End‑Anwendungen bereitzustellen.

## Häufig gestellte Fragen

**F:** *Was ist der Zweck von `CharacterType.Letter`?*  
**A:** Es weist den Index an, die angegebenen Zeichen als reguläre Buchstaben zu behandeln, sodass sie beim Indexieren separat tokenisiert werden.

**F:** *Kann ich reguläre und kombinierte Zeichen im selben Index mischen?*  
**A:** Ja – rufen Sie einfach `setRange` für jeden Typ auf; das Wörterbuch verarbeitet beide Konfigurationen gleichzeitig.

**F:** *Muss ich den Index neu aufbauen, nachdem ich das Alphabet geändert habe?*  
**A:** Auf jeden Fall. Änderungen am Zeichenwörterbuch beeinflussen die Tokenisierung, daher müssen Sie die Dokumente neu indexieren, um die neuen Regeln anzuwenden.

**F:** *Gibt es ein Limit für die Anzahl benutzerdefinierter Zeichen, die ich definieren kann?*  
**A:** Die Bibliothek unterstützt den gesamten Unicode‑Bereich; die Leistung kann sinken, wenn Sie ein extrem großes Set hinzufügen, daher sollten Sie es auf die tatsächlich benötigten Zeichen beschränken.

**F:** *Wie wirkt sich das auf die OCR‑Genauigkeit aus?*  
**A:** Durch die Abstimmung des Zeichen‑Sets des Index auf die Ausgabe der OCR‑Engine reduzieren Sie Fehlnegative und verbessern die Gesamtrelevanz der Suche.

---

**Zuletzt aktualisiert:** 2026-01-11  
**Getestet mit:** GroupDocs.Search 25.4 für Java  
**Autor:** GroupDocs  

---