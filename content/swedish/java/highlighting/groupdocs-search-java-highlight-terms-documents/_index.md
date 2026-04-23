---
date: '2026-02-27'
description: Lär dig hur du markerar text i Java med GroupDocs.Search för Java, inklusive
  sökning av dokument i Java, indexering av dokument i Java och fragmentmarkering.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Markera text i Java med GroupDocs.Search
type: docs
url: /sv/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Markera text Java med GroupDocs.Search

I dagens snabbrörliga digitala miljö är det en nödvändig funktion att kunna **highlight text java** över stora samlingar av filer. Oavsett om du bygger en plattform för juridisk granskning, en akademisk forskningsmotor eller en kundsupportskonsol, gör det att omedelbart upptäcka de termer som användarna söker efter upplevelsen mycket mer effektiv. Denna handledning guidar dig genom att använda **GroupDocs.Search for Java** för att **search documents java**, **index documents java**, och tillämpa rik markering — både för hela dokument och för fokuserade fragment.

## Snabba svar
- **Vad betyder “search and highlight text”?** Det avser att lokalisera frågeord i ett dokument och visuellt framhäva dem (t.ex. med bakgrundsfärg).  
- **Vilket bibliotek tillhandahåller denna funktion?** GroupDocs.Search for Java.  
- **Behöver jag en licens?** En gratis provversion fungerar för utvärdering; en full licens krävs för produktion.  
- **Kan jag anpassa markeringsfärger?** Ja — vilken RGB‑färg som helst kan ställas in via `HighlightOptions`.  
- **Stöds fragmentmarkering?** Absolut; du kan definiera termer före/efter matchen för att skapa koncisa utdrag.

## Så markerar du text Java i dokument
Att markera text Java innebär tre grundläggande steg:

1. **Indexera källfilerna** så att de kan sökas snabbt.  
2. **Kör en fråga** mot indexet för att hitta matchande dokument.  
3. **Rendera resultaten med visuella ledtrådar** med hjälp av highlighter‑API:et.

Nedan utforskar vi varje steg i detalj, först för hela dokumentutdata och sedan för fragment‑nivå utdrag.

## Vad är sök och markera text?
Sök och markera text är processen att skanna ett dokumentindex för en given fråga, hämta matchande dokument och sedan markera varje förekomst av frågeordet i dokumentutdata (HTML, PDF osv.). Denna visuella ledtråd hjälper slutanvändare att omedelbart hitta relevant information.

## Varför använda GroupDocs.Search för Java?
- **Högpresterande indexering** med konfigurerbar komprimering (`index documents java`).  
- **Rik markerings‑API** som fungerar på hela dokument och på anpassade fragment (`highlight search terms java`).  
- **Stöd för flera format** (DOCX, PDF, PPTX, TXT och mer).  
- **Enkel Maven‑integration** och en ren Java‑centrerad design.

## Förutsättningar
- Java Development Kit (JDK) 8 eller nyare.  
- Maven för beroendehantering.  
- En IDE som IntelliJ IDEA eller Eclipse.  
- Grundläggande kunskap om Java‑syntax.

## Installera GroupDocs.Search för Java

Lägg till GroupDocs‑arkivet och beroendet i din `pom.xml`:

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

Du kan också ladda ner den senaste JAR‑filen direkt från den officiella webbplatsen: [GroupDocs.Search för Java‑utgåvor](https://releases.groupdocs.com/search/java/).

### Licensanskaffning
Börja med en gratis provversion eller skaffa en tillfällig licens för utvärdering. För produktionsdistributioner, köp en full licens för att låsa upp alla funktioner.

## Implementeringsguide

Implementeringen är uppdelad i två praktiska sektioner: **highlighting in entire documents** och **highlighting in fragments**. Båda sektionerna innehåller de väsentliga stegen för **how to highlight Java** dokument med hjälp av GroupDocs.Search.

### Konfigurera indexinställningar
Innan indexering, konfigurera lagringen för att använda hög kompression — detta minskar diskutrymmet samtidigt som sökhastigheten bevaras.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Markering i hela dokument

#### Steg 1: Skapa och fyll i indexet
Skapa en indexmapp och lägg till alla källfiler du vill söka igenom.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Steg 2: Utför sökning och tillämpa markering
Sök efter termen (t.ex. `ipsum`) och generera en HTML‑fil med markerade träffar.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Nyckelalternativ förklarade**  
- **Compression** – hög kompression sparar lagring.  
- **HighlightColor** – ange vilket RGB‑värde som helst för att matcha ditt UI‑palett.  
- **UseInlineStyles** – `false` genererar ren HTML som kan stylas globalt med CSS.  

### Markering i fragment

#### Steg 1: Indexera och sök (samma som ovan)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Steg 2: Definiera fragmentkontext och markering
Specificera hur många termer före och efter matchen som ska visas i varje fragment.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### Steg 3: Hämta och skriv markerade fragment
Samla de genererade fragmenten och skriv dem till en HTML‑fil.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Praktiska tillämpningar
1. **Legal Document Review** – markera omedelbart lagar, klausuler eller rättsreferenser.  
2. **Academic Research** – visa nyckelterminologi över dussintals PDF‑ och Word‑filer.  
3. **Customer Support** – identifiera ordernummer eller felkoder i ärendehistorik.

## Prestandaöverväganden
- **Index Size** – hög kompression (`Compression.High`) minskar diskutrymme.  
- **Fragment Context** – större `termsBefore/After`‑värden ökar noggrannheten men kan påverka hastigheten.  
- **Memory Management** – övervaka JVM‑heap när du indexerar stora korpusar; överväg inkrementell indexering för mycket stora mängder.

## Vanliga problem och lösningar
- **Indexing Errors** – verifiera filsökvägar och säkerställ att applikationen har läs‑/skrivrättigheter.  
- **No Highlights Appear** – bekräfta att `UseInlineStyles` matchar ditt utdataformat (HTML vs. PDF).  
- **Color Not Applied** – se till att RGB‑värdena ligger inom intervallet 0‑255 och att HTML‑visaren stödjer stilen.

## Vanliga frågor

**Q: Vilka är fördelarna med att använda GroupDocs.Search för Java?**  
A: Det erbjuder snabb, skalbar indexering, anpassningsbar markering och stöd för många dokumentformat.

**Q: Hur kan jag integrera GroupDocs.Search med ett REST‑API?**  
A: Exponera sök‑ och markeringsmetoderna via Spring Boot‑kontrollers, som returnerar HTML‑ eller JSON‑payloads.

**Q: Hanterar biblioteket lösenordsskyddade filer?**  
A: Ja — ange lösenordet när du lägger till dokumentet i indexet.

**Q: Kan jag anpassa markerings‑markupen utöver färg?**  
A: Absolut; du kan injicera CSS‑klasser via `HighlightOptions` eller modifiera HTML efter generering.

**Q: Vilken version testades för den här guiden?**  
A: Koden validerades mot GroupDocs.Search 25.4.

**Q: Hur ställer jag in highlight options java för att använda en CSS‑klass istället för inline‑stilar?**  
A: Ange `options.setUseInlineStyles(false)` och lägg till en CSS‑regel för klassen du tilldelar via `options.setCssClass("myHighlight")`.

**Q: Finns det ett sätt att highlight terms pdf java direkt när källan är en PDF?**  
A: Ja — GroupDocs.Search fungerar med PDF‑inmatning, och highlightern kommer att producera HTML som du kan bädda in i en PDF‑visare eller konvertera tillbaka till PDF med hjälp av GroupDocs.Conversion.

---

**Senast uppdaterad:** 2026-02-27  
**Testad med:** GroupDocs.Search 25.4  
**Författare:** GroupDocs