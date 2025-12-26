---
date: '2025-12-26'
description: Lär dig hur du söker och markerar text i dokument med GroupDocs.Search
  för Java. Utforska tekniker för markering av hela dokumentet och fragment.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Sök och markera text med GroupDocs.Search för Java
type: docs
url: /sv/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Sök och markera text i dokument med GroupDocs.Search för Java

I dagens digitala era är **search and highlight text** över enorma dokumentsamlingar ett vanligt krav. Oavsett om du bygger ett verktyg för juridisk granskning, en akademisk forskningsportal eller en kund‑support‑dashboard, så förbättrar möjligheten att omedelbart hitta och framhäva nyckeltermer användbarheten avsevärt. I den här omfattande guiden kommer du att upptäcka hur du implementerar **search and highlight text** med GroupDocs.Search för Java — med både markering av hela dokument och fragment‑nivåmarkering för fokuserat sammanhang.

## Snabba svar
- **What does “search and highlight text” mean?** Det innebär att lokalisera frågeord i ett dokument och visuellt framhäva dem (t.ex. med bakgrundsfärg).  
- **Which library provides this capability?** GroupDocs.Search för Java.  
- **Do I need a license?** En gratis provperiod fungerar för utvärdering; en full licens krävs för produktion.  
- **Can I customize highlight colors?** Ja — någon RGB‑färg kan ställas in via `HighlightOptions`.  
- **Is fragment highlighting supported?** Absolut; du kan definiera termer före/efter träffen för att skapa koncisa utdrag.

## Vad är Search and Highlight Text?
Search and highlight text är processen att skanna ett dokumentindex för en given fråga, hämta matchande dokument och sedan markera varje förekomst av sökordet i dokumentets utdata (HTML, PDF osv.). Denna visuella ledtråd hjälper slutanvändare att omedelbart hitta relevant information.

## Varför använda GroupDocs.Search för Java?
- **High‑performance indexing** med konfigurerbar komprimering.  
- **Rich highlighting API** som fungerar på hela dokument och på anpassade fragment.  
- **Cross‑format support** (DOCX, PDF, PPTX, TXT och mer).  
- **Easy Maven integration** och tydligt Java‑centrerat API.

## Förutsättningar
- Java Development Kit (JDK) 8 eller nyare.  
- Maven för beroendehantering.  
- En IDE såsom IntelliJ IDEA eller Eclipse.  
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

Du kan också ladda ner den senaste JAR‑filen direkt från den officiella webbplatsen: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licensanskaffning
Börja med en gratis provperiod eller skaffa en tillfällig licens för utvärdering. För produktionsutplaceringar, köp en full licens för att låsa upp alla funktioner.

## Implementeringsguide

Implementeringen är uppdelad i två praktiska sektioner: **highlighting in entire documents** och **highlighting in fragments**. Båda sektionerna innehåller de väsentliga stegen för **how to highlight Java**‑dokument med GroupDocs.Search.

### Konfigurera indexinställningar
Innan indexering, konfigurera lagringen för att använda hög komprimering — detta minskar diskutrymmet samtidigt som sökhastigheten bevaras.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Markering i hela dokument

#### Steg 1: Skapa och fylla indexet
Skapa en indexmapp och lägg till alla källfiler du vill söka i.

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
- **Compression** — hög komprimering sparar lagring.  
- **HighlightColor** — ställ in valfri RGB‑värde för att matcha ditt UI‑palett.  
- **UseInlineStyles** — `false` genererar ren HTML som kan stylas globalt med CSS.

### Markering i fragment

#### Steg 1: Indexera och sök (samma som ovan)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Steg 2: Definiera fragmentkontext och markering
Ange hur många termer före och efter träffen som ska visas i varje fragment.

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
1. **Legal Document Review** — markera omedelbart lagar, klausuler eller rättsreferenser.  
2. **Academic Research** — lyft fram nyckelterminologi i dussintals PDF‑ och Word‑filer.  
3. **Customer Support** — identifiera ordernummer eller felkoder i ärendehistorik.

## Prestandaöverväganden
- **Index Size** — hög komprimering (`Compression.High`) minskar diskavtrycket.  
- **Fragment Context** — större `termsBefore/After`‑värden ökar precision men kan påverka hastigheten.  
- **Memory Management** — övervaka JVM‑heap när du indexerar stora korpusar; överväg inkrementell indexering för mycket stora mängder.

## Vanliga problem och lösningar
- **Indexing Errors** — verifiera filsökvägar och säkerställ att applikationen har läs‑/skrivrättigheter.  
- **No Highlights Appear** — bekräfta att `UseInlineStyles` matchar ditt utdataformat (HTML vs. PDF).  
- **Color Not Applied** — kontrollera att RGB‑värdena ligger inom intervallet 0‑255 och att HTML‑visaren stödjer stilen.

## Vanliga frågor

**Q: What are the benefits of using GroupDocs.Search for Java?**  
A: Det erbjuder snabb, skalbar indexering, anpassningsbar markering och stöd för många dokumentformat.

**Q: How can I integrate GroupDocs.Search with a REST API?**  
A: Exponera sök‑ och markeringsmetoderna via Spring Boot‑kontrollers, som returnerar HTML‑ eller JSON‑payloads.

**Q: Does the library handle password‑protected files?**  
A: Ja — ange lösenordet när du lägger till dokumentet i indexet.

**Q: Can I customize the highlight markup beyond color?**  
A: Absolut; du kan injicera CSS‑klasser via `HighlightOptions` eller modifiera HTML efter generering.

**Q: What version was tested for this guide?**  
A: Koden validerades mot GroupDocs.Search 25.4.

---

**Last Updated:** 2025-12-26  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs