---
date: '2026-07-02'
description: Lär dig hur du skaffar en tillfällig licens för GroupDocs.Search, lägger
  till kataloger i indexet och lägger till anpassade dokumentattribut samtidigt som
  du hanterar Java-söknätverkets noder.
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
title: Skaffa tillfällig licens GroupDocs – Master Search Nodes (Java)
type: docs
url: /sv/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Skaffa tillfällig licens GroupDocs – Master Search Nodes (Java)

I den här omfattande guiden kommer du att **skaffa en tillfällig licens för GroupDocs.Search**, konfigurera ett multi‑node söknätverk och lära dig hur du **lägger till kataloger för indexering** och **lägger till anpassade dokumentattribut** med Java. Oavsett om du bygger ett företagsdokumenthanteringssystem eller en sökbar produktkatalog, gör dessa steg det möjligt att utvärdera plattformen utan begränsningar och snabbt skala dina sökfunktioner.

## Snabba svar
- **Vad är det första steget för att börja använda GroupDocs.Search?** Skaffa en tillfällig licens från GroupDocs-portalen.  
- **Vilket Maven‑arkiv innehåller biblioteket?** `https://releases.groupdocs.com/search/java/`.  
- **Hur lägger jag till kataloger för indexering?** Anropa hjälpfunktionen `addDirectoriesToIndex` på master‑noden.  
- **Kan jag lägga till anpassade dokumentattribut?** Ja—anropa `addAttribute` med dokumentnyckeln och attributnamnet.  
- **Hur stänger jag av noder på ett korrekt sätt?** Anropa `closeNodes` för att frigöra resurser.

## Vad är en tillfällig licens och varför behöver jag den?
En tillfällig licens låter dig utvärdera GroupDocs.Search utan några begränsningar i utvärderingen. Den är perfekt för utveckling, testning eller proof‑of‑concept‑projekt innan du gör ett fullständigt köp. Licensen ger full åtkomst till alla funktioner under en begränsad period, vilket gör att du kan benchmarka prestanda, testa integrationspunkter och säkerställa att lösningen uppfyller dina krav utan ekonomiskt åtagande.

## Förutsättningar

Innan vi börjar, se till att du har följande förutsättningar på plats:

### Nödvändiga bibliotek och beroenden
För att arbeta med GroupDocs.Search för Java, inkludera de nödvändiga Maven‑beroendena:
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
Du kan också ladda ner den senaste versionen direkt från [GroupDocs.Search för Java‑utgåvor](https://releases.groupdocs.com/search/java/).

### Miljöinställning
- Se till att du har en kompatibel JDK installerad (Java 8 eller senare).  
- Ställ in din IDE för att stödja Maven‑projekt.

### Kunskapsförutsättningar
En grundläggande förståelse för Java‑programmering och bekantskap med Maven‑projektledning kommer att vara fördelaktigt. Om du är ny på dessa koncept, överväg att utforska introduktionsresurser för att komma igång.

## Hur du skaffar en tillfällig licens
En tillfällig licens erhålls genom att besöka GroupDocs‑portalen, fylla i ett kort formulär och placera den mottagna `.lic`‑filen i ditt projekts `resources`‑mapp. Initiera sedan licensen med några kodrader (se kodsnutten nedan). För formuläret, använd den officiella sidan: [GroupDocs Tillfällig licens](https://purchase.groupdocs.com/temporary-license/).

## Konfigurera GroupDocs.Search för Java

### Installationsinformation
För att börja använda GroupDocs.Search för Java i ditt projekt, följ Maven‑stegen ovan eller ladda ner den senaste versionen direkt från den officiella utgivningssidan.

#### Steg för licensanskaffning
1. **Gratis provperiod** – Utforska funktionerna utan något åtagande.  
2. **Tillfällig licens** – Skaffa en korttidsnyckel för testning (se avsnittet ovan).  
3. **Köp** – För produktionsanvändning, köp en full licens från **[GroupDocs köpsida](https://purchase.groupdocs.com/)**.

### Grundläggande initiering och konfiguration
Initiera ditt projekt med GroupDocs.Search på följande sätt:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Detta initieringssteg är avgörande för att säkerställa att alla komponenter fungerar sömlöst inom ditt söknätverk.

## Implementeringsguide
Låt oss nu dela upp processen i hanterbara sektioner, var och en fokuserad på en specifik funktion för att distribuera och hantera söknätverksnoder.

### Funktion 1: Konfigurationsinställning
**Översikt:** Att konfigurera inställningarna för ditt söknätverk är det första steget i att distribuera noder. Denna konfiguration innebär att specificera sökvägar och portar som är kritiska för noddistribution.

#### Implementeringssteg:
##### Steg 1: Definiera basväg och port
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Steg 2: Konfigurera söknätverk
`configureSearchNetwork`‑funktionen förbereder konfigurationsobjektet som behövs för att distribuera noder.  
`Configuration` är en klass som innehåller alla inställningar såsom indexmapp, nätverksportar och nodroller.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parametrar:** Basvägen och porten används för att lokalisera resurser och etablera kommunikationskanaler.  
- **Returvärde:** Ett konfigurerat `Configuration`‑objekt anpassat till dina distributionsbehov.

### Funktion 2: Distribution av söknätverk
**Översikt:** Att distribuera noder är nödvändigt för att skala dina sökfunktioner över olika miljöer eller datasegment.

#### Implementeringssteg:
##### Steg 1: Distribuera noder
`deploySearchNetwork`‑funktionen initierar och returnerar en array av söknätverksnoder.  
`SearchNetworkNodes` representerar varje nodinstans som deltar i det distribuerade sökklustret.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parametrar:** Basväg, port och konfiguration används för att bestämma distributionsmiljön.  
- **Returvärde:** En array som innehåller initierade `SearchNetworkNodes`.

### Funktion 3: Prenumerera på nätverkshändelser
**Översikt:** Att övervaka ditt söknätverks aktiviteter är avgörande för att upprätthålla optimal prestanda och tillförlitlighet.

#### Implementeringssteg:
##### Steg 1: Prenumerera på master‑nodens händelser
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Syfte:** Detta steg säkerställer att du blir informerad om betydande händelser eller förändringar inom ditt söknätverk.

### Funktion 4: Indexering av dokument
**Översikt:** Att lägga till kataloger som innehåller dokument för indexering möjliggör effektiv datatillgång över ditt nätverk.

#### Hur du lägger till kataloger för indexering
`addDirectoriesToIndex` är en hjälpfunktion som registrerar mappvägar för indexering på master‑noden.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Syfte:** Underlättar snabb åtkomst och sökbarhet för alla dokument i angivna kataloger.

### Funktion 5: Lägga till attribut till dokument
**Översikt:** Anpassade attribut förbättrar dokumentmetadata, vilket gör sökningar mer flexibla och informativa.

#### Hur du lägger till anpassade dokumentattribut
`addAttribute` lägger till ett anpassat metadata‑attribut till ett specificerat dokument i indexet.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parametrar:** Specificera noden, dokumentnyckeln och attributet som ska läggas till.  
- **Syfte:** Utökar sökfunktionaliteten genom att berika dokument med ytterligare metadata.

### Funktion 6: Hämta indexerade dokument
**Översikt:** Hämta och lista indexerade dokument effektivt för att säkerställa datakorrekthet och fullständighet.

#### Implementeringssteg:
##### Steg 1: Hämta indexerade dokument
```java
getIndexedDocuments(nodes[0]);
```  
- **Syfte:** Verifierar den lyckade indexeringen av alla nödvändiga dokument inom ditt söknätverk.

### Funktion 7: Stänga nätverksnoder
**Översikt:** Att korrekt stänga noder är viktigt för resurshantering och för att förhindra minnesläckor.

#### Implementeringssteg:
##### Steg 1: Stäng alla noder
`closeNodes` stänger av alla aktiva söknoder och frigör allokerade resurser.  
```java
closeNodes(nodes);
```  
- **Syfte:** Frigör resurser som varje nod upptar, vilket säkerställer en ren avstängningsprocess.

## Varför använda en tillfällig licens för GroupDocs.Search?
En tillfällig licens ger **full åtkomst till alla funktioner i 30 dagar** och stödjer upp till **50 000 indexerade dokument** utan prestandabegränsningar. Detta låter dig benchmarka indexeringshastighet, frågelatens och skalbarhet på verkliga data innan du köper en produktionslicens. Den tar också bort utvärderingsvattenstämplar, vilket ger dig en sann representation av slutproduktens kapabiliteter.

## Vanliga användningsfall
1. **Enterprise Document Management** – Indexera miljontals interna filer över avdelningar, vilket möjliggör omedelbar fulltextssökning.  
2. **E‑commerce Platforms** – Bygg en sökbar produktkatalog som sträcker sig över flera lager och tredjepartsflöden.  
3. **Legal Firms** – Organisera ärendefiler, kontrakt och bevis med anpassad metadata för snabb återvinning.

Integrationsmöjligheter med andra system inkluderar CRM‑plattformar, innehållshanteringssystem (CMS) och dataanalysverktyg, som utnyttjar de robusta indexerings- och sökfunktionerna som GroupDocs.Search för Java tillhandahåller.

## Prestandaöverväganden
För att optimera prestanda när du använder GroupDocs.Search för Java:
- **Optimera konfigurationen** – Anpassa dina konfigurationsinställningar för att matcha din specifika distributionsmiljö.  
- **Övervaka resursanvändning** – Kontrollera regelbundet CPU, minne och I/O för att förhindra flaskhalsar eller minnesläckor.  
- **Följ bästa praxis** – Följ Java‑minneshanteringsriktlinjer för att säkerställa effektiv användning av systemresurser.

## Vanliga frågor

**Q: Hur länge är en tillfällig licens giltig?**  
A: Tillfälliga licenser är vanligtvis giltiga i 30 dagar, vilket ger dig gott om tid att utvärdera produkten.

**Q: Kan jag byta från en tillfällig till en full licens utan ominstallation?**  
A: Ja—byt ut den tillfälliga licensfilen mot den fullständiga licensfilen och starta om din applikation.

**Q: Måste jag indexera om dokument efter att ha applicerat en ny licens?**  
A: Nej, indexet förblir intakt; licensen styr endast användningsrättigheterna.

**Q: Vad händer om jag glömmer att stänga av noder?**  
A: Ofrigjorda resurser kan leda till minnesläckor; anropa alltid `closeNodes` vid avstängning.

**Q: Är det möjligt att lägga till mer än ett anpassat attribut per dokument?**  
A: Absolut—anropa `addAttribute` flera gånger med olika attributnamn.

---

**Senast uppdaterad:** 2026-07-02  
**Testad med:** GroupDocs.Search för Java 25.4  
**Författare:** GroupDocs

## Relaterade handledningar

- [Distribuera en söknätverksnod i .NET med GroupDocs för effektiv dokumentindexering och återhämtning](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Hur man implementerar ett söknätverk med GroupDocs.Search i .NET för dokumenthanteringssystem](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Konfigurera Aspose.Search‑nätverk & lägga till dokumentattribut med GroupDocs.Redaction för .NET: En omfattande guide](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)