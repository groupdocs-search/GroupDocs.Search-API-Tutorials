---
date: '2026-02-21'
description: Erfahren Sie, wie Sie die Rechtschreibkorrektur in Java mit GroupDocs.Search
  aktivieren, Dokumente zum Index hinzufügen und die maximale Fehlermenge festlegen,
  um die Suchgenauigkeit zu verbessern.
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: Wie man die Rechtschreibung in Java mit GroupDocs.Search aktiviert
type: docs
url: /de/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Wie man Rechtschreibkorrektur in Java mit GroupDocs.Search aktiviert

Genauere Suchergebnisse sind für jede moderne Anwendung unerlässlich. In diesem Tutorial lernen Sie **wie man Rechtschreibkorrektur** in Java mit GroupDocs.Search aktiviert, sodass Benutzer die richtigen Ergebnisse erhalten, selbst wenn sie Suchanfragen falsch eingeben. Wir führen Sie durch das Erstellen eines Index, **Hinzufügen von Dokumenten zum Index**, das Konfigurieren von Rechtschreiboptionen und das Ausführen einer Suche, die Fehler automatisch korrigiert.

## Schnelle Antworten
- **Was bedeutet „how to enable spelling“?** Es aktiviert den integrierten Rechtschreibprüfer, der Tippfehler der Benutzer während einer Suche korrigiert.  
- **Welche Bibliothek stellt diese Funktion bereit?** GroupDocs.Search for Java.  
- **Brauche ich eine Lizenz?** Eine kostenlose Testlizenz funktioniert für die Evaluierung; für die Produktion ist eine Volllizenz erforderlich.  
- **Kann ich die Toleranz steuern?** Ja – verwenden Sie `setMaxMistakeCount`, um festzulegen, wie viele Tippfehler erlaubt sind.  
- **Ist es für große Indexe geeignet?** Absolut – die Engine ist für hochperformante Indexierung und Suche optimiert.

## Was bedeutet „how to enable spelling“ in GroupDocs.Search?
Das Aktivieren der Rechtschreibkorrektur veranlasst die Suchmaschine, nach den nächstgelegenen korrekten Begriffen zu suchen, wenn eine Anfrage Fehler enthält. Diese Funktion verbessert die Benutzererfahrung erheblich, indem sie relevante Ergebnisse selbst bei falsch geschriebenen Eingaben zurückgibt.

## Warum Rechtschreibkorrektur in Java‑Anwendungen aktivieren?
- **Steigert die Benutzerzufriedenheit** – Benutzer müssen nicht perfekt tippen.  
- **Reduziert Absprungraten** – genauere Ergebnisse halten Besucher engagiert.  
- **Funktioniert in verschiedenen Bereichen** – von Bibliothekskatalogen bis zu E‑Commerce‑Produktsuchen.

## Voraussetzungen
- Java Development Kit (JDK) installiert.  
- Grundkenntnisse in Java und Maven.  
- Verständnis von Indexierungskonzepten.  
- Ein GroupDocs.Search‑Test oder ein lizenzierter Schlüssel.

### Einrichtung von GroupDocs.Search für Java
Integrieren Sie die Bibliothek in Ihr Maven‑Projekt.

**Maven‑Setup**  
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

**Direkter Download**  
Alternativ laden Sie die neueste Version von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunter.

### Lizenzbeschaffung
Erhalten Sie eine kostenlose Testlizenz für die Evaluierung. Für den Produktionseinsatz kaufen Sie eine Volllizenz oder fordern Sie einen temporären Schlüssel von der offiziellen Website an.

## Wie man Dokumente zum Index hinzufügt
Das Erstellen eines Index ist die Grundlage jeder suchfähigen Anwendung. Nachfolgend ein minimales Beispiel, das **Dokumente zum Index hinzufügt** aus einem Ordner.

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

*Tipp:* Stellen Sie sicher, dass die Pfade korrekt sind und die Anwendung Schreibrechte für den Indexordner hat.

## Wie man Rechtschreibkorrektur konfiguriert (maximale Fehleranzahl festlegen)
Sie können den Rechtschreibprüfer feinabstimmen, indem Sie ihn aktivieren und die Toleranz für Fehler festlegen.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

*Warum `setMaxMistakeCount` wichtig ist:* Sie definiert, wie viele Tippfehler die Engine toleriert. Passen Sie diesen Wert basierend auf den typischen Fehlermustern Ihrer Domäne an.

## Wie man eine rechtschreibkorrektur‑unterstützte Suche durchführt
Mit dem vorbereiteten Index und den konfigurierten Rechtschreiboptionen führen Sie eine Abfrage aus, die Fehler enthalten kann.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

Der Aufruf `search()` liefert ein `SearchResult`, das korrigierte Begriffe und die relevantesten Dokumente enthält.

## Praktische Anwendungen
1. **Bibliothekssysteme:** Korrigieren Sie falsch geschriebene Buchtitel oder Autorennamen.  
2. **E‑Commerce‑Plattformen:** Beheben Sie Tippfehler von Benutzern in Produktsuchen, um die Konversionsrate zu steigern.  
3. **Content‑Management‑Systeme:** Verbessern Sie die Artikelsuche für Redakteure.

## Leistungsüberlegungen
- **Den Index aktuell halten** – neue oder geänderte Dateien regelmäßig neu indexieren.  
- **JVM‑Speichereinstellungen anpassen** – ausreichend Heap für große Indexe bereitstellen.  
- **Ressourcennutzung überwachen** – bei Bedarf Garbage‑Collector‑Parameter anpassen.

## Häufige Probleme & Fehlerbehebung
| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Keine Ergebnisse nach Aktivierung der Rechtschreibkorrektur | Pfad zum Indexordner ist falsch oder leer | Stellen Sie sicher, dass `indexFolder` auf einen gültigen Index zeigt und dass `index.add()` erfolgreich war |
| Rechtschreibprüfer korrigiert offensichtliche Tippfehler nicht | `setMaxMistakeCount` ist zu niedrig eingestellt | Erhöhen Sie den Wert auf 2 oder 3 für eine tolerantere Korrektur |
| Anwendung stürzt bei großen Dokumentensätzen ab | Unzureichender JVM‑Heap | Erhöhen Sie die `-Xmx`‑Option (z. B. `-Xmx4g`) |

## Häufig gestellte Fragen

**Q: Was ist GroupDocs.Search?**  
A: Es ist eine Java‑Bibliothek, die schnelles Indexieren, erweiterte Suchfunktionen und integrierte Rechtschreibkorrektur bietet.

**Q: Wie erhalte ich eine Lizenz für GroupDocs.Search?**  
A: Besuchen Sie die offizielle Website, um eine kostenlose Testversion herunterzuladen oder eine Volllizenz zu erwerben.

**Q: Kann ich GroupDocs.Search in andere Java‑Frameworks integrieren?**  
A: Ja, es funktioniert mit Spring, Jakarta EE und jeder Standard‑Java‑Anwendung.

**Q: Was sind häufige Probleme beim Einrichten eines Index?**  
A: Falsche Ordnerpfade, unzureichende Dateiberechtigungen oder fehlende Abhängigkeiten in `pom.xml`.

**Q: Wie verbessert Rechtschreibkorrektur die Suchergebnisse?**  
A: Sie schreibt falsch geschriebene Anfragen automatisch in die nächstgelegenen korrekten Begriffe um und liefert relevantere Treffer.

## Weitere Ressourcen
- [Dokumentation](https://docs.groupdocs.com/search/java/)
- [API‑Referenz](https://reference.groupdocs.com/search/java)
- [Download](https://releases.groupdocs.com/search/java/)
- [GitHub‑Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Kostenloses Support‑Forum](https://forum.groupdocs.com/c/search/10)
- [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)

---

**Zuletzt aktualisiert:** 2026-02-21  
**Getestet mit:** GroupDocs.Search 25.4  
**Autor:** GroupDocs