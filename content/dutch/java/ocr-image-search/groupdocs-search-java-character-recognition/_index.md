---
date: '2026-03-17'
description: Leer hoe u een index maakt met GroupDocs.Search voor Java, reguliere
  en gecombineerde tekens configureert, en de zoekopdracht optimaliseert voor juridische
  zaaknummers en OCR‑afbeeldingen.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Hoe een index te maken met tekenherkenning in Java
type: docs
url: /nl/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Hoe een index te maken met tekenherkenning met GroupDocs.Search voor Java

In moderne document‑intensieve toepassingen is **hoe een index te maken** die rekening houdt met de nuances van uw tekst—zoals koppeltekens, onderstrepingstekens of taalspecifieke symbolen—essentieel voor snelle, nauwkeurige zoekresultaten. In deze tutorial lopen we door het configureren van tekenherkenning in **GroupDocs.Search for Java**, waarbij zowel reguliere tekens (letters, cijfers, onderstrepingstekens) als gecombineerde tekens (bijv. koppeltekens) worden behandeld. Aan het einde kunt u een index op maat maken die precies voldoet aan de behoeften van uw OCR‑ of afbeelding‑zoekscenario, of u nu juridische zaaknummers, broncode‑repositories of meertalige PDF‑bestanden indexeert.

## Snelle antwoorden
- **Wat betekent “create custom search index”?** Het betekent dat u een index configureert om specifieke symbolen als letters of gecombineerde tekens te behandelen, in plaats van ze te negeren.  
- **Welke bibliotheek wordt gebruikt?** GroupDocs.Search for Java (v25.4 op het moment van schrijven).  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een betaalde licentie is vereist voor productie.  
- **Kan ik zowel PDF’s als afbeeldingen indexeren?** Ja—GroupDocs.Search ondersteunt OCR op afbeeldingen en PDF’s wanneer correct geconfigureerd.  
- **Is Maven vereist?** Maven is de aanbevolen manier om afhankelijkheden te beheren, maar u kunt ook Gradle of handmatige JAR‑bestanden gebruiken.  

## Wat is een aangepaste zoekindex?
Een aangepaste zoekindex stelt u in staat te definiëren hoe de zoekmachine tekens interpreteert. Standaard worden veel symbolen genegeerd, wat kan leiden tot gemiste overeenkomsten voor zaken zoals zaaknummers (`2023-AB-456`) of code‑fragmenten (`my_variable`). Het aanpassen van het alfabet‑woordenboek geeft u volledige controle over wat de engine als doorzoekbare tekst beschouwt.

## Waarom reguliere en gecombineerde tekens configureren voor juridische zaaknummers?
- **Reguliere tekens** (letters, cijfers, onderstrepingstekens) worden afzonderlijk getokeniseerd, waardoor exacte‑overeenkomsten voor identifiers mogelijk zijn.  
- **Gecombineerde tekens** (koppeltekens, schuine strepen) houden gerelateerde tokens bij elkaar, waardoor ongewenste splitsing van zaaknummers, productcodes of bestandspaden wordt voorkomen.  
- Deze configuratie **optimaliseert de zoekindex**-prestaties door tokenfragmentatie te verminderen en de relevantie voor OCR‑gegenereerde inhoud te verbeteren.

## Voorvereisten
- **JDK 8** of later geïnstalleerd.  
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

U kunt ook de nieuwste JAR‑bestanden downloaden van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
- **Gratis proefversie** – perfect voor vroege experimenten.  
- **Tijdelijke licentie** – nuttig voor langere ontwikkelingscycli.  
- **Productielicentie** – vereist voor commerciële implementatie.  

Haal een licentie op via het officiële portaal: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Basisinitialisatie
De onderstaande codefragment toont de minimale code die nodig is om een lege index op te starten. Houd het ongewijzigd; we zullen later verder bouwen.

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
De Maven‑configuratie uit de sectie *Voorvereisten* is alles wat u nodig heeft. Na het toevoegen, voer `mvn clean install` uit om de binaries op te halen.

### Vereisten voor omgeving configuratie
- Zorg ervoor dat de **indexmap** en **documentmap** op schijf bestaan.  
- Gebruik absolute paden of configureer uw IDE om relatieve paden correct op te lossen.  

## Implementatie‑gids

Hieronder lopen we twee afzonderlijke functies door: **reguliere tekens** en **gecombineerde tekens**. Elke functie volgt hetzelfde patroon—pad definiëren, de index maken, het tekenwoordenboek instellen en tenslotte uw documenten indexeren.

### Functie 1 – Reguliere tekens

#### Overzicht
Reguliere tekens worden behandeld als onafhankelijke tokens. Dit is ideaal wanneer u cijfers, letters en onderstrepingstekens exact zoals ze verschijnen doorzoekbaar wilt maken.

#### Stapsgewijze implementatie

**1️⃣ Pad instellen**  
Definieer waar de index wordt opgeslagen en waar uw bron‑documenten zich bevinden.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Index maken en configureren**  
Instantieer de index en wis eventuele vooraf bestaande alfabet‑configuratie.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Reguliere tekens definiëren**  
Maak een tekenarray die cijfers, Latijnse letters en het onderstrepingsteken bevat.

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

### Functie 2 – Gecombineerde tekens

#### Overzicht
Gecombineerde tekens (zoals koppeltekens) verbinden vaak twee woorden. Het markeren als *gecombineerd* vertelt de engine om de omliggende tokens tijdens het indexeren bij elkaar te houden.

#### Stapsgewijze implementatie

**1️⃣ Pad instellen**  

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

### Gebruikssituatie 1 – Juridisch documentbeheer
Juridische bestanden bevatten vaak zaaknummers zoals `2023-AB-456`. Door onderstrepingstekens en koppeltekens te configureren, geven zoekopdrachten exacte overeenkomsten terug zonder de identifier te splitsen, waardoor u **juridische zaaknummers** efficiënt kunt doorzoeken.

### Gebruikssituatie 2 – Broncode‑repositories
Ontwikkelaars moeten code‑fragmenten doorzoeken waar onderstrepingstekens (`my_variable`) en koppeltekens (`my-function`) betekenisvol zijn. Aangepaste tekenherkenning zorgt ervoor dat de zoekengine deze symbolen respecteert.

### Gebruikssituatie 3 – Meertalige datasets
Bij het werken met talen die extra alfabetten gebruiken, kunt u de **Unicode‑karakterset uitbreiden** om die reeksen op te nemen, waardoor nauwkeurige zoekresultaten over verschillende talen worden gegarandeerd.

### Gebruikssituatie 4 – PDF‑afbeeldingen indexeren
Als u gescande PDF‑bestanden of afbeeldingen indexeert, bevat de OCR‑output vaak gemengde tekens. Het correct configureren van reguliere en gecombineerde tekens **optimaliseert de zoekindex**‑prestaties voor op afbeeldingen gebaseerde inhoud.

## Prestatie‑overwegingen

- **Resource Management** – Houd het heap‑gebruik in de gaten; grote indexen profiteren van incrementele commits.  
- **Garbage Collection** – Maak `Index`‑objecten vrij wanneer ze niet meer nodig zijn zodat de JVM geheugen kan terugwinnen.  
- **Index Optimization** – Roep periodiek `index.optimize()` aan (indien beschikbaar) om de index te comprimeren en de query‑snelheid te verbeteren.  

## Conclusie

U weet nu **hoe een index te maken** die onderscheid maakt tussen reguliere en gecombineerde tekens met GroupDocs.Search voor Java. Deze fijnmazige controle stelt u in staat OCR‑bewuste, high‑performance zoekoplossingen te bouwen die zijn afgestemd op juridische, ontwikkelings‑ of meertalige omgevingen.

### Volgende stappen
- Experimenteer met extra Unicode‑reeksen voor niet‑Latijnse alfabetten.  
- Combineer tekenconfiguratie met andere GroupDocs.Search‑functies zoals stemming of synoniemen.  
- Integreer de index in een REST‑API om zoekfunctionaliteit beschikbaar te maken voor front‑end applicaties.

## Veelgestelde vragen

**Q:** *Wat is het doel van `CharacterType.Letter`?*  
**A:** Het vertelt de index om de opgegeven tekens als reguliere letters te behandelen, zodat ze tijdens het indexeren afzonderlijk worden getokeniseerd.

**Q:** *Kan ik reguliere en gecombineerde tekens in dezelfde index combineren?*  
**A:** Ja—roep simpelweg `setRange` aan voor elk type; het woordenboek zal beide configuraties gelijktijdig afhandelen.

**Q:** *Moet ik de index opnieuw bouwen na het wijzigen van het alfabet?*  
**A:** Absoluut. Wijzigingen in het tekenwoordenboek beïnvloeden de tokenisatie, dus u moet de documenten opnieuw indexeren om de nieuwe regels toe te passen.

**Q:** *Is er een limiet aan het aantal aangepaste tekens dat ik kan definiëren?*  
**A:** De bibliotheek ondersteunt het volledige Unicode‑bereik; de prestaties kunnen afnemen als u een extreem grote set toevoegt, dus beperk het tot tekens die u daadwerkelijk nodig heeft.

**Q:** *Hoe beïnvloedt dit de OCR‑nauwkeurigheid?*  
**A:** Door de karakterset van de index af te stemmen op de output van de OCR‑engine, vermindert u valse negatieven en verbetert u de algehele zoekrelevantie.

---

**Last Updated:** 2026-03-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---