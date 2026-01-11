---
date: '2026-01-11'
description: Leer hoe u een aangepaste zoekindex maakt met GroupDocs.Search voor Java,
  waarbij u reguliere en gecombineerde tekens configureert voor geavanceerde OCR-
  en afbeeldingzoekopdrachten.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Maak een aangepaste zoekindex met tekenherkenning – GroupDocs.Search Java
type: docs
url: /nl/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Maak een aangepaste zoekindex met tekenherkenning met GroupDocs.Search voor Java

In moderne, document‑intensieve toepassingen is **het maken van een aangepaste zoekindex** die de nuances van uw tekst begrijpt—zoals koppeltekens, onderstrepingsstrepen of taalspecifieke symbolen—essentieel voor snelle, nauwkeurige terugwinning. Deze tutorial leidt u door het configureren van tekenherkenning in **GroupDocs.Search voor Java**, met zowel reguliere tekens (letters, cijfers, onderstrepingsstrepen) als gecombineerde tekens (bijv. koppeltekens). Aan het einde kunt u een index aanpassen die precies voldoet aan de behoeften van uw OCR- of afbeelding‑zoekscenario.

## Snelle antwoorden
- **Wat betekent “create custom search index”?** Het betekent het configureren van een index om specifieke symbolen als letters of gecombineerde tekens te behandelen, in plaats van ze te negeren.  
- **Welke bibliotheek wordt gebruikt?** GroupDocs.Search voor Java (v25.4 op het moment van schrijven).  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een betaalde licentie is vereist voor productie.  
- **Kan ik zowel PDF’s als afbeeldingen indexeren?** Ja—GroupDocs.Search ondersteunt OCR op afbeeldingen en PDF’s wanneer correct geconfigureerd.  
- **Is Maven vereist?** Maven is de aanbevolen manier om afhankelijkheden te beheren, maar u kunt ook Gradle of handmatige JAR‑s gebruiken.  

## Wat is een aangepaste zoekindex?
Een aangepaste zoekindex stelt u in staat te definiëren hoe de zoekmachine tekens interpreteert. Standaard worden veel symbolen genegeerd, wat kan leiden tot gemiste overeenkomsten voor zaken als dossiersnummers (`ABC-123`) of code‑fragmenten (`my_variable`). Het aanpassen van het alfabet‑woordenboek geeft u volledige controle over wat de engine als doorzoekbare tekst beschouwt.

## Waarom reguliere en gecombineerde tekens configureren?
- **Reguliere tekens** (letters, cijfers, onderstrepingsstrepen) worden behandeld als zelfstandige tokens, wat exacte‑overeenkomsten verbetert.  
- **Gecombineerde tekens** (koppeltekens, schuine strepen) verbinden woorden; door ze te configureren voorkomt u ongewenste token‑splitsing, wat cruciaal is voor juridische verwijzingen, productcodes of broncode‑indexering.

## Voorvereisten
- **JDK 8** of hoger geïnstalleerd.  
- **Maven** voor afhankelijkheidsbeheer.  
- Toegang tot de **GroupDocs.Search voor Java** bibliotheek (gedownload via Maven of de officiële site).  

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

U kunt ook de nieuwste JAR‑s downloaden van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
- **Gratis proefversie** – perfect voor vroege experimenten.  
- **Tijdelijke licentie** – nuttig voor langere ontwikkelingscycli.  
- **Productielicentie** – vereist voor commerciële inzet.  

Haal een licentie via het officiële portaal: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

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
De Maven‑configuratie uit de *Voorvereisten* sectie is alles wat u nodig heeft. Na het toevoegen, voer `mvn clean install` uit om de binaries op te halen.

### Vereisten voor omgevingsinstelling
- Zorg ervoor dat de **indexmap** en **documentmap** op schijf bestaan.  
- Gebruik absolute paden of configureer uw IDE om relatieve paden correct op te lossen.  

## Implementatie‑gids

Hieronder lopen we twee afzonderlijke functies door: **reguliere tekens** en **gecombineerde tekens**. Elke functie volgt hetzelfde patroon—pad definiëren, index maken, tekenwoordenboek instellen en tenslotte uw documenten indexeren.

### Functie 1 – Reguliere tekens

#### Overzicht
Reguliere tekens worden behandeld als onafhankelijke tokens. Dit is ideaal wanneer u cijfers, letters en onderstrepingsstrepen precies zoals ze verschijnen doorzoekbaar wilt maken.

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
Bouw een tekenarray die cijfers, Latijnse letters en de onderstrepingsstreep bevat.

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
Gecombineerde tekens (zoals koppeltekens) verbinden vaak twee woorden. Door ze als *gecombineerd* te markeren, vertelt u de engine om de omliggende tokens tijdens het indexeren bij elkaar te houden.

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
Hier vertellen we het woordenboek dat het koppelstreepje als een gecombineerd teken moet worden behandeld.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Documenten indexeren**  

```java
index.add(documentFolder);
```

## Praktische toepassingen

### Gebruikssituatie 1 – Juridisch documentbeheer
Juridische bestanden bevatten vaak dossiersnummers zoals `2023-AB-456`. Door onderstrepingsstrepen en koppeltekens te configureren, geven zoekopdrachten exacte overeenkomsten terug zonder de identifier te splitsen.

### Gebruikssituatie 2 – Broncode‑repositories
Ontwikkelaars moeten code‑fragmenten doorzoeken waar onderstrepingsstrepen (`my_variable`) en koppeltekens (`my-function`) betekenisvol zijn. Aangepaste tekenherkenning zorgt ervoor dat de zoekengine deze symbolen respecteert.

### Gebruikssituatie 3 – Meertalige datasets
Bij het werken met talen die extra alfabetten gebruiken, kunt u de reguliere tekenreeks uitbreiden met die Unicode‑bereiken, waardoor nauwkeurige zoekresultaten over verschillende talen worden gegarandeerd.

## Prestatie‑overwegingen
- **Resource‑beheer** – Houd het heap‑gebruik in de gaten; grote indexen profiteren van incrementele commits.  
- **Garbage collection** – Maak `Index`‑objecten vrij wanneer ze niet meer nodig zijn zodat de JVM geheugen kan terugwinnen.  
- **Indexoptimalisatie** – Roep periodiek `index.optimize()` aan (indien beschikbaar) om de index te comprimeren en de zoek‑snelheid te verbeteren.  

## Conclusie
U weet nu hoe u een **aangepaste zoekindex** kunt maken die onderscheid maakt tussen reguliere en gecombineerde tekens met GroupDocs.Search voor Java. Deze fijnmazige controle stelt u in staat OCR‑bewuste, high‑performance zoekoplossingen te bouwen die zijn afgestemd op juridische, ontwikkelings‑ of meertalige omgevingen.

**Volgende stappen**  
- Experimenteer met extra Unicode‑bereiken voor niet‑Latijnse alfabetten.  
- Combineer tekenconfiguratie met andere GroupDocs.Search‑functies zoals stemming of synoniemen.  
- Integreer de index in een REST‑API om zoekfunctionaliteit beschikbaar te maken voor front‑end applicaties.

## Veelgestelde vragen

**V:** *Wat is het doel van `CharacterType.Letter`?*  
**A:** Het vertelt de index om de opgegeven tekens als reguliere letters te behandelen, zodat ze tijdens het indexeren apart getokeniseerd worden.

**V:** *Kan ik reguliere en gecombineerde tekens in dezelfde index combineren?*  
**A:** Ja—roep simpelweg `setRange` aan voor elk type; het woordenboek zal beide configuraties gelijktijdig afhandelen.

**V:** *Moet ik de index opnieuw opbouwen na het wijzigen van het alfabet?*  
**A:** Absoluut. Wijzigingen in het tekenwoordenboek beïnvloeden de tokenisatie, dus u moet de documenten opnieuw indexeren om de nieuwe regels toe te passen.

**V:** *Is er een limiet aan het aantal aangepaste tekens dat ik kan definiëren?*  
**A:** De bibliotheek ondersteunt het volledige Unicode‑bereik; de prestaties kunnen afnemen als u een extreem grote set toevoegt, dus beperk het tot de tekens die u daadwerkelijk nodig heeft.

**V:** *Hoe beïnvloedt dit de OCR‑nauwkeurigheid?*  
**A:** Door de tekenreeks van de index af te stemmen op de output van de OCR‑engine, vermindert u valse negatieven en verbetert u de algehele zoekrelevantie.

---

**Laatst bijgewerkt:** 2026-01-11  
**Getest met:** GroupDocs.Search 25.4 voor Java  
**Auteur:** GroupDocs