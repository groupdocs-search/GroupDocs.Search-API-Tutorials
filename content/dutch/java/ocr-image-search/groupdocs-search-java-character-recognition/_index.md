---
date: '2026-11-02'
description: Maak een aangepaste zoekindex in Java met GroupDocs.Search om reguliere
  en gecombineerde tekens te verwerken, OCR-beeldzoekopdrachten te optimaliseren en
  de zoekopdracht naar juridische zaaknummers te verbeteren.
keywords:
- custom search index java
- GroupDocs.Search Java
- character recognition java
- OCR search Java
- search library Java
lastmod: '2026-11-02'
og_description: Maak een aangepaste zoekindex in Java met GroupDocs.Search om reguliere
  en gecombineerde tekens te verwerken, OCR-beeldzoekopdrachten te optimaliseren en
  de zoekopdracht naar juridische zaaknummers te verbeteren.
og_image_alt: Guide showing custom search index creation in Java with GroupDocs.Search
og_title: Maak een aangepaste zoekindex in Java met GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Create a custom search index java using GroupDocs.Search to handle
    regular and blended characters, optimize OCR image search, and improve legal case
    number retrieval.
  headline: Create a custom search index java with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It means configuring an index to treat specific symbols as letters or
      blended characters, rather than ignoring them.
    question: What does “create custom search index” mean?
  - answer: GroupDocs.Search for Java (v25.4 at the time of writing).
    question: Which library is used?
  - answer: A free trial works for development; a paid license is required for production.
    question: Do I need a license?
  - answer: Yes—GroupDocs.Search supports OCR on images and PDFs when properly configured.
    question: Can I index both PDFs and images?
  - answer: Maven is the recommended way to manage dependencies, but you can also
      use Gradle or manual JARs.
    question: Is Maven required?
  type: FAQPage
tags:
- custom search index
- GroupDocs.Search
- Java OCR
- character recognition
- search library
title: Maak een aangepaste zoekindex in Java met GroupDocs.Search
type: docs
url: /nl/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Maak een aangepaste zoekindex java met GroupDocs.Search

In moderne, document‑intensieve toepassingen is het creëren van een **custom search index java** die rekening houdt met de nuances van uw tekst—zoals koppeltekens, onderstrepingen of taalspecifieke symbolen—essentieel voor snelle, nauwkeurige terugwinning. Deze tutorial leidt u door het configureren van tekenherkenning in **GroupDocs.Search for Java**, waarbij zowel reguliere tekens (letters, cijfers, onderstrepingen) als gecombineerde tekens (bijv. koppeltekens) worden behandeld. Aan het einde kunt u een index op maat maken die precies voldoet aan de behoeften van OCR‑ of afbeelding‑zoekscenario's, of u nu juridische zaaknummers, broncode‑repositories of meertalige PDF‑bestanden indexeert.

## Snelle antwoorden
- **Wat betekent “create custom search index”?** Het betekent het configureren van een index om specifieke symbolen als letters of gecombineerde tekens te behandelen, in plaats van ze te negeren.  
- **Welke bibliotheek wordt gebruikt?** GroupDocs.Search for Java (v25.4 op het moment van schrijven).  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een betaalde licentie is vereist voor productie.  
- **Kan ik zowel PDF's als afbeeldingen indexeren?** Ja—GroupDocs.Search ondersteunt OCR op afbeeldingen en PDF's wanneer correct geconfigureerd.  
- **Is Maven vereist?** Maven is de aanbevolen manier om afhankelijkheden te beheren, maar u kunt ook Gradle of handmatige JAR's gebruiken.

## Wat is een custom search index java?
De **custom search index java** is een doorzoekbare datastructuur die u kunt vormgeven door te definiëren welke tekens als letters, cijfers of gecombineerde symbolen worden behandeld. Standaard worden veel symbolen genegeerd, wat kan leiden tot gemiste overeenkomsten voor identificatoren zoals zaaknummers (`2023-AB-456`) of codefragmenten (`my_variable`). Het aanpassen van het alfabetwoordenboek geeft u volledige controle over tokenisatie, wat leidt tot hogere relevantie en snellere query‑uitvoering.

## Waarom reguliere en gecombineerde tekens configureren voor juridische zaaknummers?
Het behandelen van koppeltekens en schuine strepen als gecombineerde tekens houdt gerelateerde tokens bij elkaar, waardoor ongewenste splitsing van identificatoren zoals zaaknummers, productcodes of bestandspaden wordt voorkomen. Deze configuratie **optimaliseert de prestaties van de zoekindex** door tokenfragmentatie te verminderen en verbetert de relevantie voor OCR‑gegenereerde inhoud, vooral bij juridische documenten die sterk afhankelijk zijn van gestructureerde identificatoren.

## Vereisten
- **JDK 8** of later geïnstalleerd.  
- **Maven** voor afhankelijkheidsbeheer.  
- Toegang tot de **GroupDocs.Search for Java** bibliotheek (gedownload via Maven of de officiële site).  

### Vereiste bibliotheken en afhankelijkheden
Voeg de repository‑ en afhankelijkheidsvermeldingen toe aan uw `pom.xml` (zoals hieronder weergegeven). Het XML‑blok moet ongewijzigd blijven.

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

U kunt ook de nieuwste JAR's downloaden van [GroupDocs.Search voor Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
- **Gratis proefversie** – perfect voor vroege experimenten.  
- **Tijdelijke licentie** – handig voor langere ontwikkelingscycli.  
- **Productielicentie** – vereist voor commerciële implementatie.  

Haal een licentie op via het officiële portaal: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Basisinitialisatie
De onderstaande codefragment toont de minimale code die nodig is om een lege index op te starten. De `Index`‑klasse is de kerncomponent die de doorzoekbare gegevens opslaat en beheert. Laat het ongewijzigd; we zullen later verder bouwen.

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

## GroupDocs.Search voor Java instellen

### Installatie via Maven
De Maven‑configuratie uit de sectie *Vereisten* is alles wat u nodig heeft. Na het toevoegen, voer `mvn clean install` uit om de binaries op te halen.

### Vereisten voor omgeving‑configuratie
- Zorg ervoor dat de **indexmap** en **documentmap** op de schijf bestaan.  
- Gebruik absolute paden of configureer uw IDE om relatieve paden correct op te lossen.  

## Implementatie‑gids

Hieronder lopen we twee afzonderlijke functies door: **reguliere tekens** en **gecombineerde tekens**. Elke functie volgt hetzelfde patroon—definieer paden, maak de index, stel het tekenwoordenboek in, en indexeer uiteindelijk uw documenten.

### Functie 1 – reguliere tekens

#### Overzicht
Reguliere tekens worden behandeld als onafhankelijke tokens. Dit is ideaal wanneer u cijfers, letters en onderstrepingen exact zoals ze verschijnen doorzoekbaar wilt maken.

#### Stapsgewijze implementatie

**1️⃣ Padinstellingen**  
Definieer waar de index wordt opgeslagen en waar uw bronbestanden zich bevinden.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Index maken en configureren**  
Instantieer de index en wis eventuele vooraf bestaande alfabetconfiguratie.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Reguliere tekens definiëren**  
Bouw een tekenarray die cijfers, Latijnse letters en de onderstreping bevat.

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

**4️⃣ Documenten indexeren**  
Voeg alle bestanden uit de bronmap toe aan de nieuw geconfigureerde index.

```java
index.add(documentFolder);
```

### Functie 2 – gecombineerde tekens

#### Overzicht
Gecombineerde tekens (zoals koppeltekens) verbinden vaak twee woorden. Ze markeren als *gecombineerd* vertelt de engine om de omliggende tokens tijdens het indexeren bij elkaar te houden.

#### Stapsgewijze implementatie

**1️⃣ Padinstellingen**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Index maken en configureren**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Gecombineerde tekens definiëren**  
Hier vertellen we het woordenboek dat het koppelteken als een gecombineerd teken moet worden behandeld.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Documenten indexeren**  

```java
index.add(documentFolder);
```

## Praktische toepassingen

### Gebruikssituatie 1 – juridisch documentbeheer
Juridische bestanden bevatten vaak zaaknummers zoals `2023-AB-456`. Door onderstrepingen en koppeltekens te configureren, geven zoekopdrachten exacte overeenkomsten terug zonder de identifier te splitsen, waardoor u **juridische zaaknummers** efficiënt kunt doorzoeken.

### Gebruikssituatie 2 – broncode‑repositories
Ontwikkelaars moeten codefragmenten doorzoeken waar onderstrepingen (`my_variable`) en koppeltekens (`my-function`) betekenisvol zijn. Aangepaste tekenherkenning zorgt ervoor dat de zoekengine deze symbolen respecteert.

### Gebruikssituatie 3 – meertalige datasets
Bij het werken met talen die extra alfabetten gebruiken, kunt u de **Unicode‑tekenset uitbreiden** om die reeksen op te nemen, waardoor nauwkeurige zoekresultaten over verschillende talen worden gegarandeerd.

### Gebruikssituatie 4 – PDF‑afbeeldingen indexeren
Als u gescande PDF's of afbeeldingsbestanden indexeert, bevat de OCR‑output vaak gemengde tekens. Het correct configureren van reguliere en gecombineerde tekens **optimaliseert de prestaties van de zoekindex** voor op afbeeldingen gebaseerde inhoud.

## Prestatie‑overwegingen

- **Resource‑beheer** – monitor heap‑gebruik; grote indexen profiteren van incrementele commits.  
- **Garbage collection** – geef `Index`‑objecten vrij wanneer ze niet meer nodig zijn zodat de JVM geheugen kan terugwinnen.  
- **Indexoptimalisatie** – roep periodiek `index.optimize()` aan (indien beschikbaar) om de index te comprimeren en de query‑snelheid te verbeteren.  

## Conclusie

U weet nu **hoe u een custom search index java** kunt maken die onderscheid maakt tussen reguliere en gecombineerde tekens met GroupDocs.Search for Java. Deze fijnmazige controle stelt u in staat OCR‑bewuste, high‑performance zoekoplossingen te bouwen die zijn afgestemd op juridische, ontwikkelings‑ of meertalige omgevingen.

### Volgende stappen
- Experimenteer met extra Unicode‑reeksen voor niet‑Latijnse alfabetten.  
- Combineer tekenconfiguratie met andere GroupDocs.Search‑functies zoals stemming of synoniemen.  
- Stel de index beschikbaar via een REST‑API zodat front‑end applicaties zoekopdrachten via HTTP kunnen uitvoeren.  

## Veelgestelde vragen

**Q:** *Wat is het doel van `CharacterType.Letter`?*  
**A:** Het vertelt de index om de opgegeven tekens als reguliere letters te behandelen, zodat ze tijdens het indexeren afzonderlijk worden getokeniseerd.

**Q:** *Kan ik reguliere en gecombineerde tekens combineren in dezelfde index?*  
**A:** Ja—roep eenvoudig `setRange` aan voor elk type; het woordenboek zal beide configuraties gelijktijdig afhandelen.

**Q:** *Moet ik de index opnieuw opbouwen na het wijzigen van het alfabet?*  
**A:** Absoluut. Wijzigingen in het tekenwoordenboek beïnvloeden de tokenisatie, dus u moet de documenten opnieuw indexeren om de nieuwe regels toe te passen.

**Q:** *Is er een limiet aan het aantal aangepaste tekens dat ik kan definiëren?*  
**A:** De bibliotheek ondersteunt het volledige Unicode‑bereik; de prestaties kunnen afnemen als u een extreem grote set toevoegt, dus beperk het tot de tekens die u daadwerkelijk nodig heeft.

**Q:** *Hoe beïnvloedt dit de OCR‑nauwkeurigheid?*  
**A:** Door de tekenset van de index af te stemmen op de output van de OCR‑engine, vermindert u valse negatieven en verbetert u de algehele zoekrelevantie.

---

**Last Updated:** 2026-11-02  
**Tested with:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Gerelateerde tutorials

- [Maak en beheer GroupDocs Search Java-index](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Maak zoekindexdirectory & stel licentie in – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Java Full Text Search-bibliotheek – Index optimaliseren met GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)