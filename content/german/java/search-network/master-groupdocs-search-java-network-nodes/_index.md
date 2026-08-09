---
date: '2026-07-02'
description: Erfahren Sie, wie Sie eine temporäre Lizenz für GroupDocs.Search erhalten,
  Verzeichnisse zum Index hinzufügen und benutzerdefinierte Dokumentattribute hinzufügen,
  während Sie Java search network nodes verwalten.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Temporäre Lizenz für GroupDocs – Master Search Nodes (Java)
type: docs
url: /de/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Temporäre Lizenz für GroupDocs – Master Search Nodes (Java) erhalten

In diesem umfassenden Leitfaden **erhalten Sie eine temporäre Lizenz für GroupDocs.Search**, konfigurieren ein Multi‑Node‑Suchnetzwerk und lernen, wie Sie **Verzeichnisse zum Index hinzufügen** und **benutzerdefinierte Dokumentattribute** mit Java hinzufügen. Egal, ob Sie ein Enterprise‑Dokumentenmanagement‑System oder einen durchsuchbaren Produktkatalog bauen, das Beherrschen dieser Schritte ermöglicht Ihnen, die Plattform ohne Einschränkungen zu evaluieren und Ihre Suchfähigkeiten schnell zu skalieren.

## Schnelle Antworten
- **Was ist der erste Schritt, um GroupDocs.Search zu nutzen?** Eine temporäre Lizenz vom GroupDocs‑Portal erhalten.  
- **Welches Maven‑Repository hostet die Bibliothek?** `https://releases.groupdocs.com/search/java/`.  
- **Wie füge ich Verzeichnisse zum Index hinzu?** Rufen Sie die `addDirectoriesToIndex`‑Hilfsfunktion auf dem Master‑Knoten auf.  
- **Kann ich benutzerdefinierte Dokumentattribute hinzufügen?** Ja – rufen Sie `addAttribute` mit dem Dokumentenschlüssel und dem Attributnamen auf.  
- **Wie schließe ich Knoten sauber herunter?** Rufen Sie `closeNodes` auf, um Ressourcen freizugeben.

## Was ist eine temporäre Lizenz und warum brauche ich sie?
Eine temporäre Lizenz ermöglicht Ihnen die Evaluation von GroupDocs.Search ohne Bewertungseinschränkungen. Sie ist ideal für Entwicklung, Tests oder Proof‑of‑Concept‑Projekte, bevor Sie einen vollständigen Kauf tätigen. Die Lizenz gewährt vollen Funktionszugriff für einen begrenzten Zeitraum, sodass Sie Leistung benchmarken, Integrationspunkte testen und sicherstellen können, dass die Lösung Ihren Anforderungen entspricht, ohne finanzielle Verpflichtungen.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

### Erforderliche Bibliotheken und Abhängigkeiten
Um mit GroupDocs.Search für Java zu arbeiten, fügen Sie die notwendigen Maven‑Abhängigkeiten hinzu:
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
Sie können die neueste Version auch direkt von [GroupDocs.Search für Java Releases](https://releases.groupdocs.com/search/java/) herunterladen.

### Umgebung einrichten
- Stellen Sie sicher, dass ein kompatibles JDK installiert ist (Java 8 oder höher).  
- Richten Sie Ihre IDE ein, um Maven‑Projekte zu unterstützen.

### Wissensvoraussetzungen
Ein grundlegendes Verständnis von Java‑Programmierung und Vertrautheit mit Maven‑Projektmanagement sind vorteilhaft. Wenn Sie neu in diesen Konzepten sind, sollten Sie einführende Ressourcen erkunden, um loszulegen.

## So erhalten Sie eine temporäre Lizenz
Eine temporäre Lizenz erhalten Sie, indem Sie das GroupDocs‑Portal besuchen, ein kurzes Antragsformular ausfüllen und die erhaltene `.lic`‑Datei in den `resources`‑Ordner Ihres Projekts legen. Anschließend initialisieren Sie die Lizenz mit wenigen Codezeilen (siehe das Snippet unten). Für das Antragsformular nutzen Sie die offizielle Seite: [GroupDocs Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/).

## Einrichtung von GroupDocs.Search für Java

### Installationsinformationen
Um GroupDocs.Search für Java in Ihrem Projekt zu verwenden, folgen Sie den oben genannten Maven‑Schritten oder laden die neueste Version direkt von der offiziellen Release‑Seite herunter.

#### Schritte zum Erwerb einer Lizenz
1. **Kostenlose Testversion** – Erkunden Sie die Funktionen ohne Verpflichtung.  
2. **Temporäre Lizenz** – Einen kurzzeitigen Schlüssel für Tests erhalten (siehe Abschnitt oben).  
3. **Kauf** – Für den Produktionseinsatz kaufen Sie eine Voll‑Lizenz über die **[GroupDocs Kaufseite](https://purchase.groupdocs.com/)**.

### Grundlegende Initialisierung und Einrichtung
Initialisieren Sie Ihr Projekt mit GroupDocs.Search wie folgt:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Dieser Initialisierungsschritt ist entscheidend, damit alle Komponenten nahtlos innerhalb Ihres Suchnetzwerks funktionieren.

## Implementierungsleitfaden
Nun teilen wir den Prozess in handhabbare Abschnitte, die sich jeweils auf ein spezifisches Feature der Bereitstellung und Verwaltung von Suchnetzwerk‑Knoten konzentrieren.

### Feature 1: Konfigurationssetup
**Übersicht:** Das Einrichten der Konfiguration für Ihr Suchnetzwerk ist der erste Schritt beim Deployen von Knoten. Dieses Setup beinhaltet das Festlegen von Pfaden und Ports, die für die Knotenbereitstellung kritisch sind.

#### Implementierungsschritte:
##### Schritt 1: Basis‑Pfad und Port definieren
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Schritt 2: Suchnetzwerk konfigurieren
Die Funktion `configureSearchNetwork` bereitet das Konfigurationsobjekt vor, das für das Bereitstellen von Knoten erforderlich ist.  
`Configuration` ist eine Klasse, die alle Einstellungen wie Indexordner, Netzwerkports und Knotenrollen enthält.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parameter:** Der Basis‑Pfad und der Port werden verwendet, um Ressourcen zu finden und Kommunikationskanäle aufzubauen.  
- **Rückgabewert:** Ein konfiguriertes `Configuration`‑Objekt, das auf Ihre Bereitstellungsanforderungen zugeschnitten ist.

### Feature 2: Bereitstellung des Suchnetzwerks
**Übersicht:** Das Deployen von Knoten ist essenziell, um Ihre Suchfähigkeiten über verschiedene Umgebungen oder Datensegmente hinweg zu skalieren.

#### Implementierungsschritte:
##### Schritt 1: Knoten bereitstellen
Die Funktion `deploySearchNetwork` initialisiert und gibt ein Array von Suchnetzwerk‑Knoten zurück.  
`SearchNetworkNodes` repräsentiert jede Knoteninstanz, die am verteilten Such‑Cluster teilnimmt.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parameter:** Basis‑Pfad, Port und Konfiguration werden verwendet, um die Bereitstellungsumgebung zu bestimmen.  
- **Rückgabewert:** Ein Array, das initialisierte `SearchNetworkNodes` enthält.

### Feature 3: Abonnieren von Netzwerkereignissen
**Übersicht:** Das Überwachen der Aktivitäten Ihres Suchnetzwerks ist entscheidend, um optimale Leistung und Zuverlässigkeit zu gewährleisten.

#### Implementierungsschritte:
##### Schritt 1: Ereignisse des Master‑Knotens abonnieren
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Zweck:** Dieser Schritt stellt sicher, dass Sie über wichtige Ereignisse oder Änderungen in Ihrem Suchnetzwerk benachrichtigt werden.

### Feature 4: Dokumente indexieren
**Übersicht:** Das Hinzufügen von Verzeichnissen, die zu indexierende Dokumente enthalten, ermöglicht eine effiziente Datenabfrage über Ihr Netzwerk hinweg.

#### So fügen Sie Verzeichnisse zum Index hinzu
`addDirectoriesToIndex` ist eine Hilfsmethode, die Ordnerpfade für das Indexieren auf dem Master‑Knoten registriert.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Zweck:** Erleichtert den schnellen Zugriff und die Durchsuchbarkeit aller Dokumente in den angegebenen Verzeichnissen.

### Feature 5: Attribute zu Dokumenten hinzufügen
**Übersicht:** Benutzerdefinierte Attribute erweitern die Metadaten von Dokumenten und machen Suchen flexibler und informativer.

#### So fügen Sie benutzerdefinierte Dokumentattribute hinzu
`addAttribute` fügt einem angegebenen Dokument im Index ein benutzerdefiniertes Metadaten‑Attribut hinzu.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parameter:** Geben Sie den Knoten, den Dokumentenschlüssel und das hinzuzufügende Attribut an.  
- **Zweck:** Erweitert die Suchfunktionalität, indem Dokumente mit zusätzlichen Metadaten angereichert werden.

### Feature 6: Indexierte Dokumente abrufen
**Übersicht:** Effizientes Abrufen und Auflisten indexierter Dokumente stellt Daten­genauigkeit und Vollständigkeit sicher.

#### Implementierungsschritte:
##### Schritt 1: Indexierte Dokumente abrufen
```java
getIndexedDocuments(nodes[0]);
```  
- **Zweck:** Verifiziert die erfolgreiche Indexierung aller erforderlichen Dokumente in Ihrem Suchnetzwerk.

### Feature 7: Netzwerk‑Knoten schließen
**Übersicht:** Das ordnungsgemäße Schließen von Knoten ist wichtig für das Ressourcen‑Management und zur Vermeidung von Speicherlecks.

#### Implementierungsschritte:
##### Schritt 1: Alle Knoten schließen
`closeNodes` fährt alle aktiven Suchknoten herunter und gibt zugewiesene Ressourcen frei.  
```java
closeNodes(nodes);
```  
- **Zweck:** Gibt die von jedem Knoten belegten Ressourcen frei und sorgt für einen sauberen Abschaltvorgang.

## Warum eine temporäre Lizenz für GroupDocs.Search verwenden?
Eine temporäre Lizenz bietet **vollen Funktionszugriff für 30 Tage** und unterstützt bis zu **50.000 indexierte Dokumente** ohne Leistungsdrosselung. Damit können Sie Indexierungsgeschwindigkeit, Abfrage‑Latenz und Skalierbarkeit an realen Daten benchmarken, bevor Sie eine Produktionslizenz erwerben. Außerdem werden Evaluierungs‑Watermarks entfernt, sodass Sie eine echte Darstellung der endgültigen Produktfähigkeiten erhalten.

## Häufige Anwendungsfälle
1. **Enterprise Document Management** – Millionen interner Dateien über Abteilungen hinweg indexieren und sofortige Volltextsuche ermöglichen.  
2. **E‑Commerce-Plattformen** – Einen durchsuchbaren Produktkatalog erstellen, der mehrere Lager und Drittanbieter‑Feeds umfasst.  
3. **Rechtsanwaltskanzleien** – Fallakten, Verträge und Beweismaterial mit benutzerdefinierten Metadaten für schnelle Abrufe organisieren.

Integrationsmöglichkeiten mit anderen Systemen umfassen CRM‑Plattformen, Content‑Management‑Systeme (CMS) und Daten‑Analyse‑Tools, die die robusten Indexierungs‑ und Suchfunktionen von GroupDocs.Search für Java nutzen.

## Leistungsüberlegungen
- **Konfiguration optimieren** – Passen Sie Ihre Konfigurationseinstellungen an Ihre spezifische Bereitstellungsumgebung an.  
- **Ressourcennutzung überwachen** – Überprüfen Sie regelmäßig CPU, Speicher und I/O, um Engpässe oder Speicherlecks zu vermeiden.  
- **Best Practices befolgen** – Halten Sie sich an Java‑Speicherverwaltungsrichtlinien, um eine effiziente Nutzung der Systemressourcen sicherzustellen.

## Häufig gestellte Fragen

**Q: Wie lange bleibt eine temporäre Lizenz gültig?**  
A: Temporäre Lizenzen sind in der Regel 30 Tage gültig, was Ihnen ausreichend Zeit gibt, das Produkt zu evaluieren.

**Q: Kann ich von einer temporären zu einer Voll‑Lizenz wechseln, ohne neu zu installieren?**  
A: Ja – ersetzen Sie die temporäre Lizenzdatei durch die Voll‑Lizenzdatei und starten Sie Ihre Anwendung neu.

**Q: Muss ich Dokumente nach dem Anwenden einer neuen Lizenz neu indexieren?**  
A: Nein, der Index bleibt erhalten; die Lizenz regelt nur die Nutzungsrechte.

**Q: Was passiert, wenn ich vergesse, Knoten zu schließen?**  
A: Nicht freigegebene Ressourcen können zu Speicherlecks führen; rufen Sie stets `closeNodes` beim Herunterfahren auf.

**Q: Ist es möglich, mehr als ein benutzerdefiniertes Attribut pro Dokument hinzuzufügen?**  
A: Absolut – rufen Sie `addAttribute` mehrfach mit unterschiedlichen Attributnamen auf.

---

**Letzte Aktualisierung:** 2026-07-02  
**Getestet mit:** GroupDocs.Search für Java 25.4  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Ein Search Network Node in .NET mit GroupDocs für effizientes Dokumenten‑Indexieren und -Abrufen bereitstellen](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Wie man ein Search Network mit GroupDocs.Search in .NET für Dokumentenmanagementsysteme implementiert](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Konfiguration des Aspose.Search Netzwerks & Hinzufügen von Dokumentattributen mit GroupDocs.Redaction für .NET: Ein umfassender Leitfaden](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)