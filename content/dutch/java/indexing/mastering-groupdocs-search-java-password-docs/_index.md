---
date: '2026-10-28'
description: Leer hoe u meerdere bestandstypen kunt doorzoeken en een doorzoekbare
  index kunt maken voor wachtwoordbeveiligde documenten in Java met GroupDocs.Search.
  Stapsgewijze handleiding met code, tips en prestatie‑trucs.
keywords:
- search multiple file types
- build searchable index
- password protected document indexing java
- groupdocs.search java api
lastmod: '2026-10-28'
og_description: Leer hoe u meerdere bestandstypen kunt doorzoeken en een doorzoekbare
  index kunt maken voor wachtwoordbeveiligde documenten in Java met GroupDocs.Search.
  Stapsgewijze handleiding met code, tips en prestatie‑trucs.
og_image_alt: Guide showing Java code to search multiple file types and index password‑protected
  documents with GroupDocs.Search
og_title: Hoe meerdere bestandstypen te zoeken en documenten te indexeren in Java
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
title: Hoe meerdere bestandstypen te zoeken en documenten te indexeren in Java
type: docs
url: /nl/java/indexing/mastering-groupdocs-search-java-password-docs/
weight: 1
---

# Hoe meerdere bestandstypen te zoeken en documenten te indexeren in Java

In moderne ondernemingen moet u vaak **meerdere bestandstypen zoeken** terwijl vertrouwelijke bestanden achter wachtwoorden worden vergrendeld. Deze tutorial laat zien hoe u een doorzoekbare index bouwt voor wachtwoord‑beveiligde documenten in Java met GroupDocs.Search. U ziet hoe u een wachtwoordwoordenboek configureert, wachtwoord‑vereiste gebeurtenissen afhandelt en de prestaties optimaliseert voor grote batches — allemaal zonder eigen decryptielogica te schrijven.

## Snelle antwoorden
- **Waar gaat deze tutorial over?** Indexeren van wachtwoord‑beveiligde documenten met een wachtwoordwoordenboek en een event‑listener.  
- **Welke bibliotheek is vereist?** GroupDocs.Search for Java (latest version).  
- **Heb ik een licentie nodig?** Een tijdelijke gratis proeflicentie is beschikbaar voor evaluatie.  
- **Kan ik andere bestandstypen indexeren?** Ja, GroupDocs.Search ondersteunt 120+ formaten inclusief PDF, DOCX, XLSX, PPTX en afbeeldingen.  
- **Welke Java‑versie is nodig?** JDK 8 of later.  

## Wat is “create document index java”?
`create document index java` verwijst naar het proces van het construeren van een doorzoekbare datastructuur die termen koppelt aan de locaties van door Java beheerde bestanden. Met GroupDocs.Search extraheert de engine automatisch tekst uit ondersteunde formaten — inclusief versleutelde PDF’s, Office‑documenten en afbeeldingen — zodat u full‑text zoekopdrachten kunt uitvoeren zonder zelf decryptiecode te schrijven. Deze aanpak vereenvoudigt de zoekimplementatie terwijl de documentbeveiliging behouden blijft.

## Waarom GroupDocs.Search gebruiken voor wachtwoord‑beveiligde bestanden?
GroupDocs.Search biedt een zero‑touch ontgrendelingsmechanisme dat wachtwoorden uit een woordenboek of een event‑handler toepast, zodat u versleutelde bestanden in één enkele doorloop kunt indexeren. Het verwerkt tot 2 miljoen documenten per uur op een standaard 8‑core server, ondersteunt meer dan 120 bestandstypen en biedt een rijke querytaal met Boolean, wildcard‑ en fuzzy‑operatoren — allemaal essentieel voor het bouwen van een doorzoekbare index die diverse inhoud bestrijkt.

## Voorvereisten
- Java Development Kit (JDK) 8+ geïnstalleerd en toegevoegd aan uw `PATH`.  
- Een IDE zoals IntelliJ IDEA of Eclipse.  
- Maven voor afhankelijkheidsbeheer.  
- GroupDocs.Search for Java – voeg de bibliotheek toe via Maven (zie de installatie‑sectie).

## GroupDocs.Search voor Java instellen

### Maven gebruiken
Voeg de repository en afhankelijkheid toe aan uw `pom.xml`‑bestand:

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

### Directe download
U kunt ook de nieuwste versie direct downloaden van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

Om te beginnen met een proeflicentie, bezoek [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) en volg de instructies om uw gratis proefversie te verkrijgen.

## Hoe documenten te indexeren met een wachtwoordwoordenboek

U kunt een **doorzoekbare index bouwen** door een woordenboek te leveren dat bestands‑paden koppelt aan hun wachtwoorden. De engine haalt automatisch het juiste wachtwoord op tijdens het indexeren.

### Overzicht
Sla documentwachtwoorden op in een eenvoudige sleutel‑waarde‑map zodat de index‑engine bestanden op aanvraag kan ontgrendelen.

### Stap 1: definieer de index en de documentenmap
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordDictionary";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Stap 2: maak een index
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Stap 3: voeg documentwachtwoorden toe
```java
// Add passwords for specific files using their absolute paths
String path1 = new File(documentsFolder + "/English.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path1, "123456");

String path2 = new File(documentsFolder + "/SampleDocument.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path2, "123456");
```

### Stap 4: indexeer documenten
```java
// Automatically retrieve passwords from the dictionary during indexing
index.add(documentsFolder);
```

### Stap 5: zoek in de index
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

**Tip:** Voor productie‑scenario's laadt u wachtwoorden uit een veilige kluis (bijv. Azure Key Vault of AWS Secrets Manager) in plaats van ze hard‑gecodeerd op te nemen.

#### Probleemoplossing
- Controleer of elk wachtwoord overeenkomt met het daadwerkelijke beschermingswachtwoord van het bestand.  
- Controleer de bestands‑paden; een onjuist pad veroorzaakt `FileNotFoundException`.

## Hoe documenten te indexeren met een event‑listener voor wachtwoordvereiste?

U kunt wachtwoorden alleen leveren wanneer de engine een wachtwoord‑vereiste‑event uitlokt, waardoor inloggegevens uit het geheugen blijven en dynamische wachtwoordresolutie mogelijk is.

Wanneer de index‑engine een versleuteld bestand tegenkomt, triggert het een callback waarin u het wachtwoord kunt opzoeken in een veilige opslag of on‑the‑fly kunt berekenen. Deze methode verkleint het aanvalsoppervlak vergeleken met het opslaan van alle wachtwoorden in een woordenboek.

### Overzicht
Lever wachtwoorden on‑the‑fly via een event‑callback, waardoor uw inloggegevensopslag geïsoleerd blijft.

### Stap 1: definieer de index en de documentenmap
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordEvent";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Stap 2: maak een index
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Stap 3: abonneer op het wachtwoord‑vereiste‑event
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

### Stap 4: indexeer documenten
```java
// The event handler will supply passwords as required during indexing
index.add(documentsFolder);
```

### Stap 5: zoek in de index
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

#### Probleemoplossing
- Zorg ervoor dat de event‑handler alle bestandsextensies dekt die u wilt indexeren.  
- Test eerst met een paar voorbeeldbestanden om te bevestigen dat het wachtwoord wordt toegepast.

## Praktische toepassingen

1. **Enterprise document management** – automatiseer het indexeren van vertrouwelijke contracten, HR‑bestanden en financiële rapporten terwijl ze versleuteld blijven in rust.  
2. **Legal archives** – haal snel dossiers op zonder gevoelige inhoud bloot te stellen.  
3. **Healthcare records** – indexeer patiënt‑PDF’s en Word‑documenten terwijl u voldoet aan de HIPAA‑vereisten.

## Prestatie‑overwegingen

- **Memory allocation** – wijs voldoende heap‑geheugen toe (`-Xmx2g` of hoger) voor grote batches.  
- **Parallel indexing** – gebruik `index.addAsync(...)` of voer meerdere indexeer‑threads uit om tot **2 miljoen documenten per uur** te behalen op een 8‑core machine. `index.addAsync(...)` is een methode die documenten in de wachtrij zet voor asynchrone indexering.  
- **Index maintenance** – roep periodiek `index.optimize()` aan om de index te comprimeren en de query‑snelheid te verbeteren.

## Veelvoorkomende problemen en oplossingen

- **Wrong password** – het document wordt overgeslagen en er wordt een waarschuwing gelogd. Controleer uw wachtwoordbron.  
- **Unsupported format** – installeer de benodigde format‑plugins of converteer bestanden naar een ondersteund type vóór het indexeren.  
- **Large files** – vergroot de heap‑grootte en overweeg ze in kleinere batches te indexeren om `OutOfMemoryError` te voorkomen.

## Veelgestelde vragen

**Q: Hoe ga ik om met verschillende bestandsformaten?**  
A: GroupDocs.Search ondersteunt meer dan 120 formaten, waaronder PDF, DOCX, XLSX, PPTX en gangbare afbeeldings‑typen. Installeer format‑plugins indien nodig.

**Q: Wat gebeurt er als een wachtwoord onjuist is?**  
A: Het document wordt overgeslagen en er wordt een waarschuwing gelogd; controleer uw wachtwoordwoordenboek of event‑handler.

**Q: Kan ik bestanden die in de cloud zijn opgeslagen indexeren?**  
A: Ja, maar ze moeten eerst naar een lokale tijdelijke map worden gedownload omdat de engine werkt met bestands‑systeem‑paden.

**Q: Hoe kan ik de zoekrelevantie verbeteren?**  
A: Pas de scoring aan met `IndexOptions`, voeg synoniemen toe, en gebruik geavanceerde query‑syntaxis zoals `field:term~` voor fuzzy matching. `IndexOptions` is een configuratie‑object dat scoring en indexeer‑gedrag regelt.

**Q: Wat moet ik doen als het indexeren voor sommige bestanden faalt?**  
A: Bekijk de log‑output; veelvoorkomende oorzaken zijn ontbrekende wachtwoorden, corrupte bestanden of niet‑ondersteunde formaten.

## Bronnen
- [GroupDocs.Search Documentatie](https://docs.groupdocs.com/search/java/)
- [API‑referentie](https://reference.groupdocs.com/search/java)
- [GroupDocs.Search downloaden](https://releases.groupdocs.com/search/java/)
- [GitHub-repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Gratis ondersteuningsforum](https://forum.groupdocs.com/c/search/10)
- [Informatie over tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)

Door deze gids te volgen, weet u nu **hoe u meerdere bestandstypen kunt zoeken** en **wachtwoord‑beveiligde documenten kunt indexeren** in Java, waardoor zowel de beveiliging als de vindbaarheid in uw applicaties wordt verbeterd.

---

**Laatst bijgewerkt:** 2026-10-28  
**Getest met:** GroupDocs.Search 25.4 for Java  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Hoe wachtwoord‑beveiligde documenten in Java te indexeren met GroupDocs.Search](/search/java/indexing/mastering-groupdocs-search-java-password-docs/)
- [Verbeter query‑prestaties met GroupDocs.Search Java: index en zoek optimaliseren](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)