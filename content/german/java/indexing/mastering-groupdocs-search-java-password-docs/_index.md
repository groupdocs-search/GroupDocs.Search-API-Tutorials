---
date: '2026-10-28'
description: Erfahren Sie, wie Sie mehrere Dateitypen durchsuchen und mit GroupDocs.Search
  in Java einen durchsuchbaren Index für passwortgeschützte Dokumente erstellen. Schritt‑für‑Schritt-Anleitung
  mit Code, Tipps und Performance‑Tricks.
keywords:
- search multiple file types
- build searchable index
- password protected document indexing java
- groupdocs.search java api
lastmod: '2026-10-28'
og_description: Erfahren Sie, wie Sie mehrere Dateitypen durchsuchen und mit GroupDocs.Search
  in Java einen durchsuchbaren Index für passwortgeschützte Dokumente erstellen. Schritt‑für‑Schritt-Anleitung
  mit Code, Tipps und Performance‑Tricks.
og_image_alt: Guide showing Java code to search multiple file types and index password‑protected
  documents with GroupDocs.Search
og_title: Wie man mehrere Dateitypen sucht und Dokumente in Java indexiert
schemas:
- author: GroupDocs
  dateModified: '2026-10-28'
  description: Learn how to search multiple file types and build a searchable index
    for password‑protected documents in Java using GroupDocs.Search. Step‑by‑step
    guide with code, tips, and performance tricks.
  headline: How to search multiple file types and index docs in Java
  type: TechArticle
- questions:
  - answer: GroupDocs.Search supports 120+ formats including PDF, DOCX, XLSX, PPTX,
      and common image types. Install format plugins if required.
    question: How do I handle different file formats?
  - answer: The document is skipped and a warning is logged; verify your password
      dictionary or event handler.
    question: What happens if a password is wrong?
  - answer: Yes, but they must be downloaded to a local temporary folder first because
      the engine works with file‑system paths.
    question: Can I index files stored in the cloud?
  - answer: Adjust scoring with `IndexOptions`, add synonyms, and use advanced query
      syntax such as `field:term~` for fuzzy matching. `IndexOptions` is a configuration
      object that controls scoring and indexing behavior.
    question: How can I improve search relevance?
  - answer: Review the log output; common causes are missing passwords, corrupted
      files, or unsupported formats.
    question: What should I do if indexing fails for some files?
  type: FAQPage
tags:
- search multiple file types
- GroupDocs.Search
- Java indexing
- password‑protected docs
- document search
title: Wie man mehrere Dateitypen sucht und Dokumente in Java indexiert
type: docs
url: /de/java/indexing/mastering-groupdocs-search-java-password-docs/
weight: 1
---

# Wie man mehrere Dateitypen sucht und Dokumente in Java indexiert

In modernen Unternehmen muss man häufig **mehrere Dateitypen durchsuchen**, während vertrauliche Dateien hinter Passwörtern gesperrt bleiben. Dieses Tutorial zeigt, wie man in Java mit GroupDocs.Search einen durchsuchbaren Index für passwortgeschützte Dokumente erstellt. Sie sehen, wie man ein Passwort‑Wörterbuch konfiguriert, Passwort‑erforderliche Ereignisse behandelt und die Leistung für große Stapel optimiert – alles ohne eigene Entschlüsselungslogik zu schreiben.

## Schnelle Antworten
- **Worum geht es in diesem Tutorial?** Indexierung passwortgeschützter Dokumente mit einem Passwort‑Wörterbuch und einem Ereignis‑Listener.  
- **Welche Bibliothek wird benötigt?** GroupDocs.Search for Java (neueste Version).  
- **Benötige ich eine Lizenz?** Eine temporäre kostenlose Testlizenz steht für die Evaluierung zur Verfügung.  
- **Kann ich andere Dateitypen indexieren?** Ja, GroupDocs.Search unterstützt mehr als 120 Formate, darunter PDF, DOCX, XLSX, PPTX und Bilder.  
- **Welche Java‑Version wird benötigt?** JDK 8 oder höher.  

## Was ist „create document index java“?
`create document index java` bezieht sich auf den Prozess, eine durchsuchbare Datenstruktur zu erstellen, die Begriffe den Speicherorten von Java‑verwalteten Dateien zuordnet. Mit GroupDocs.Search extrahiert die Engine automatisch Text aus unterstützten Formaten – einschließlich verschlüsselter PDFs, Office‑Dokumente und Bilder – sodass Sie Volltextsuche durchführen können, ohne eigene Entschlüsselungscode zu schreiben. Dieser Ansatz vereinfacht die Implementierung der Suche und bewahrt die Dokumentensicherheit.

## Warum GroupDocs.Search für passwortgeschützte Dateien verwenden?
GroupDocs.Search bietet einen Zero‑Touch‑Entsperrmechanismus, der Passwörter aus einem Wörterbuch oder einem Ereignis‑Handler anwendet und Ihnen ermöglicht, verschlüsselte Dateien in einem Durchlauf zu indexieren. Es verarbeitet bis zu 2 Millionen Dokumente pro Stunde auf einem Standard‑8‑Kern‑Server, unterstützt mehr als 120 Dateitypen und bietet eine umfangreiche Abfragesprache mit Booleschen, Platzhalter‑ und Fuzzy‑Operatoren – alles entscheidend für den Aufbau eines durchsuchbaren Index, der vielfältige Inhalte abdeckt.

## Voraussetzungen
- Java Development Kit (JDK) 8+ installiert und zu Ihrem `PATH` hinzugefügt.  
- Eine IDE wie IntelliJ IDEA oder Eclipse.  
- Maven für das Abhängigkeitsmanagement.  
- GroupDocs.Search für Java – Bibliothek über Maven hinzufügen (siehe den Einrichtungsabschnitt).  

## Einrichtung von GroupDocs.Search für Java

### Verwendung von Maven
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

### Direkter Download
Alternativ können Sie die neueste Version direkt von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunterladen.

Um mit einer Testlizenz zu beginnen, besuchen Sie die [temporäre Lizenzseite von GroupDocs](https://purchase.groupdocs.com/temporary-license/) und folgen Sie den Anweisungen, um Ihre kostenlose Testversion zu erhalten.

## Wie man Dokumente mit einem Passwort‑Wörterbuch indexiert

Sie können einen **durchsuchbaren Index** erstellen, indem Sie ein Wörterbuch bereitstellen, das Dateipfade ihren Passwörtern zuordnet. Die Engine ruft während des Indexierens automatisch das richtige Passwort ab.

### Überblick
Speichern Sie Dokumentenpasswörter in einer einfachen Schlüssel‑Wert‑Map, damit die Indexierungs‑Engine Dateien bei Bedarf entsperren kann.

### Schritt 1: Index und Dokumenten‑Ordner definieren
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordDictionary";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Schritt 2: Index erstellen
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Schritt 3: Dokumenten‑Passwörter hinzufügen
```java
// Add passwords for specific files using their absolute paths
String path1 = new File(documentsFolder + "/English.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path1, "123456");

String path2 = new File(documentsFolder + "/SampleDocument.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path2, "123456");
```

### Schritt 4: Dokumente indexieren
```java
// Automatically retrieve passwords from the dictionary during indexing
index.add(documentsFolder);
```

### Schritt 5: Im Index suchen
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

**Tipp:** Für Produktionsszenarien laden Sie Passwörter aus einem sicheren Tresor (z. B. Azure Key Vault oder AWS Secrets Manager) statt sie hart zu codieren.

#### Fehlersuche
- Stellen Sie sicher, dass jedes Passwort dem tatsächlichen Schutzpasswort der Datei entspricht.  
- Überprüfen Sie die Dateipfade; ein falscher Pfad löst `FileNotFoundException` aus.

## Wie man Dokumente mit einem Ereignis‑Listener für Passwortanforderungen indexiert?

Sie können Passwörter nur bereitstellen, wenn die Engine ein Passwort‑erforderliches Ereignis auslöst, wodurch Anmeldeinformationen aus dem Speicher gehalten und eine dynamische Passwortauflösung ermöglicht werden.

Wenn die Indexierungs‑Engine auf eine verschlüsselte Datei stößt, löst sie einen Callback aus, in dem Sie das Passwort aus einem sicheren Speicher abrufen oder es on‑the‑fly berechnen können. Diese Methode reduziert die Angriffsfläche im Vergleich zur Speicherung aller Passwörter in einem Wörterbuch.

### Überblick
Stellen Sie Passwörter on‑the‑fly über einen Ereignis‑Callback bereit und halten Sie Ihren Anmeldeinformations‑Store isoliert.

### Schritt 1: Index und Dokumenten‑Ordner definieren
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordEvent";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Schritt 2: Index erstellen
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Schritt 3: Auf das Passwort‑erforderliche Ereignis abonnieren
```java
index.getEvents().PasswordRequired.add(new EventHandler<PasswordRequiredEventArgs>() {
    @Override
    public void invoke(Object sender, PasswordRequiredEventArgs args) {
        // Provide password for DOCX files when needed
        if (args.getDocumentFullPath().endsWith(".docx")) {
            args.setPassword("123456");
        }
    }
});
```

### Schritt 4: Dokumente indexieren
```java
// The event handler will supply passwords as required during indexing
index.add(documentsFolder);
```

### Schritt 5: Im Index suchen
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

#### Fehlersuche
- Stellen Sie sicher, dass der Ereignis‑Handler alle Dateierweiterungen abdeckt, die Sie indexieren müssen.  
- Testen Sie zunächst mit einigen Beispieldateien, um zu bestätigen, dass das Passwort angewendet wird.

## Praktische Anwendungen

1. **Enterprise-Dokumentenmanagement** – automatisieren Sie die Indexierung vertraulicher Verträge, HR‑Dateien und Finanzberichte, während sie im Ruhezustand verschlüsselt bleiben.  
2. **Rechtliche Archive** – rufen Sie Fallakten schnell ab, ohne sensible Inhalte offenzulegen.  
3. **Gesundheitsakten** – indexieren Sie Patienten‑PDFs und Word‑Dokumente und erfüllen Sie dabei die HIPAA‑Anforderungen.

## Leistungsüberlegungen

- **Speicherzuweisung** – weisen Sie ausreichend Heap‑Speicher zu (`-Xmx2g` oder höher) für große Stapel zu.  
- **Parallele Indexierung** – verwenden Sie `index.addAsync(...)` oder führen Sie mehrere Indexierungs‑Threads aus, um bis zu **2 Millionen Dokumente pro Stunde** auf einer 8‑Kern‑Maschine zu erreichen. `index.addAsync(...)` ist eine Methode, die Dokumente für die asynchrone Indexierung in die Warteschlange stellt.  
- **Indexwartung** – rufen Sie periodisch `index.optimize()` auf, um den Index zu komprimieren und die Abfragegeschwindigkeit zu verbessern.

## Häufige Probleme und Lösungen

- **Falsches Passwort** – das Dokument wird übersprungen und eine Warnung wird protokolliert. Überprüfen Sie Ihre Passwortquelle.  
- **Nicht unterstütztes Format** – installieren Sie die erforderlichen Format‑Plugins oder konvertieren Sie Dateien vor der Indexierung in einen unterstützten Typ.  
- **Große Dateien** – erhöhen Sie die Heap‑Größe und erwägen Sie, sie in kleineren Stapeln zu indexieren, um `OutOfMemoryError` zu vermeiden.

## Häufig gestellte Fragen

**Q: Wie gehe ich mit verschiedenen Dateiformaten um?**  
A: GroupDocs.Search unterstützt mehr als 120 Formate, darunter PDF, DOCX, XLSX, PPTX und gängige Bildtypen. Installieren Sie bei Bedarf Format‑Plugins.

**Q: Was passiert, wenn ein Passwort falsch ist?**  
A: Das Dokument wird übersprungen und eine Warnung wird protokolliert; überprüfen Sie Ihr Passwort‑Wörterbuch oder den Ereignis‑Handler.

**Q: Kann ich Dateien, die in der Cloud gespeichert sind, indexieren?**  
A: Ja, aber sie müssen zuerst in einen lokalen temporären Ordner heruntergeladen werden, da die Engine mit Dateisystem‑Pfaden arbeitet.

**Q: Wie kann ich die Suchrelevanz verbessern?**  
A: Passen Sie das Scoring mit `IndexOptions` an, fügen Sie Synonyme hinzu und verwenden Sie erweiterte Abfragesyntax wie `field:term~` für Fuzzy‑Matching. `IndexOptions` ist ein Konfigurationsobjekt, das das Scoring und das Indexierungsverhalten steuert.

**Q: Was soll ich tun, wenn die Indexierung bei einigen Dateien fehlschlägt?**  
A: Überprüfen Sie die Protokollausgabe; häufige Ursachen sind fehlende Passwörter, beschädigte Dateien oder nicht unterstützte Formate.

## Ressourcen
- [GroupDocs.Search Dokumentation](https://docs.groupdocs.com/search/java/)
- [API‑Referenz](https://reference.groupdocs.com/search/java)
- [GroupDocs.Search herunterladen](https://releases.groupdocs.com/search/java/)
- [GitHub‑Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Kostenloses Support‑Forum](https://forum.groupdocs.com/c/search/10)
- [Informationen zur temporären Lizenz](https://purchase.groupdocs.com/temporary-license/)

Durch Befolgen dieser Anleitung wissen Sie jetzt, **wie man mehrere Dateitypen durchsucht** und **passwortgeschützte Dokumente** in Java indexiert, wodurch sowohl Sicherheit als auch Auffindbarkeit in Ihren Anwendungen gesteigert werden.

---

**Zuletzt aktualisiert:** 2026-10-28  
**Getestet mit:** GroupDocs.Search 25.4 für Java  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Wie man passwortgeschützte Dokumente in Java mit GroupDocs.Search indexiert](/search/java/indexing/mastering-groupdocs-search-java-password-docs/)
- [Abfrageleistung mit GroupDocs.Search Java verbessern: Index & Suche optimieren](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)