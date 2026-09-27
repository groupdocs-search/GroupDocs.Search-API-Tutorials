---
date: '2026-09-27'
description: Lär dig hur du markerar text java med GroupDocs.Search för Java, inklusive
  sök dokument java, indexera dokument java och fragmentmarkering.
keywords:
- highlight text java
- search documents java
- index documents java
- java text highlighting library
- highlight terms pdf java
lastmod: '2026-09-27'
og_description: Lär dig hur du markerar text java med GroupDocs.Search för Java. Få
  steg‑för‑steg‑vägledning om indexering, sökning och fragmentmarkering för snabba
  resultat.
og_image_alt: Screenshot of highlighted search terms in a Java application using GroupDocs.Search
og_title: Markera text java med GroupDocs.Search – Snabb dokumentmarkering
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  headline: Highlight text java with GroupDocs.Search
  type: TechArticle
- description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  name: Highlight text java with GroupDocs.Search
  steps:
  - name: create and populate the index
    text: Create an index folder and add all source files you want to search. The
      `Index` class represents the searchable container.
  - name: perform search and apply highlighting
    text: Search for the term (e.g., `ipsum`) and generate an HTML file with highlighted
      matches. Use `HighlightOptions` to specify the highlight color and whether to
      use inline styles. `HighlightOptions` lets you define the foreground and background
      colors, as well as the CSS class that will be applied to ea
  - name: index and search (same as above)
    text: The same index and search steps apply; you reuse the `Index` and `SearchResult`
      objects.
  - name: define fragment context and highlight
    text: Specify how many terms before and after the match should appear in each
      fragment with `FragmentOptions`. `FragmentOptions` controls the number of surrounding
      words (`termsBefore` and `termsAfter`) that are included in each snippet, allowing
      you to balance context against snippet length.
  - name: retrieve and write highlighted fragments
    text: Collect the generated fragments and write them to an HTML file. Each fragment
      is already highlighted according to the `HighlightOptions` you configured. `fragmentHighlighter`
      is a utility that creates highlighted snippets from a `SearchResult` using the
      specified fragment and highlight options. **Di
  type: HowTo
- questions:
  - answer: It offers fast, scalable indexing, customizable highlighting, and support
      for 30+ document formats, processing 500‑page files in under 2 seconds on a
      typical server.
    question: What are the benefits of using GroupDocs.Search for Java?
  - answer: Expose the search and highlight methods via Spring Boot controllers, returning
      HTML snippets or JSON payloads that contain the highlighted fragments.
    question: How can I integrate GroupDocs.Search with a REST API?
  - answer: Yes—provide the password when adding the document to the index via `addDocument(filePath,
      password)`.
    question: Does the library handle password‑protected files?
  - answer: Absolutely; you can assign a CSS class with `options.setCssClass("myHighlight")`
      and style it globally, or modify the generated HTML after highlighting.
    question: Can I customize the highlight markup beyond color?
  - answer: The code was validated against GroupDocs.Search 25.4.
    question: What version was tested for this guide?
  type: FAQPage
tags:
- highlight text java
- GroupDocs.Search
- Java document processing
title: Markera text java med GroupDocs.Search
type: docs
url: /sv/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Markera text java med GroupDocs.Search

I moderna företagsapplikationer är **highlight text java** avgörande för att omvandla råa sökresultat till omedelbart läsbara insikter. Oavsett om du bygger en juridisk‑granskningsportal, en akademisk forskningsmotor eller en kund‑supportdashboard, gör förmågan att lokalisera och visuellt framhäva sökord att användarna sparar otaliga sekunder av manuell skanning. Denna handledning visar hur du använder **GroupDocs.Search for Java** för att **search documents java**, **index documents java**, och tillämpa både hel‑dokument‑ och fragment‑nivåmarkering, allt med bara några rader kod.

## Snabba svar
- **Vad betyder “search and highlight text”?** Det betyder att lokalisera sökord i ett dokument och visuellt framhäva dem (till exempel med en färgad bakgrund).  
- **Vilket bibliotek tillhandahåller denna funktion?** GroupDocs.Search for Java.  
- **Behöver jag en licens?** En gratis provperiod fungerar för utvärdering; en full licens krävs för produktionsanvändning.  
- **Kan jag anpassa markeringsfärger?** Ja—vilken RGB‑färg som helst kan ställas in via `HighlightOptions`.  
- **Stöds fragment‑markering?** Absolut; du kan definiera termer före/efter matchen för att skapa koncisa utdrag.

## Så markerar du text java i dokument

För att markera text java i dokument, bygg först ett index över källfilerna med lämpliga komprimeringsinställningar, kör sedan en sökfråga för att hitta de önskade termerna, och exportera slutligen resultaten till HTML, PDF eller vanlig text där varje matchning omsluts av en markerings‑tagg. Denna tre‑stegsprocess säkerställer snabb, exakt markering över stora samlingar.

1. **Skapa ett index** med komprimeringsinställningar som håller lagringsutrymmet lågt.  
2. **Utför en sökning** med den frågesträng du vill markera.  
3. **Generera utdata** (HTML, PDF eller vanlig text) där varje förekomst av sökordet omsluts av en markerings‑tagg.

## Vad är sök‑ och markeringstext?

Sök‑ och markeringstext är processen att skanna en indexerad samling för en given fråga, hämta matchande dokument och sedan markera varje förekomst av sökordet i utdata (HTML, PDF, etc.). Denna visuella ledtråd hjälper slutanvändare att omedelbart hitta relevant information.

## Varför använda GroupDocs.Search for Java?

GroupDocs.Search for Java levererar **high‑performance indexing** (upp till 50 GB per index med `Compression.High`), **rich highlighting** som fungerar på hela dokument och anpassade fragment, och **cross‑format support** för över 30 filtyper—inklusive DOCX, PDF, PPTX och TXT. Biblioteket erbjuder också **incremental indexing**, vilket gör att du kan lägga till nya filer utan att bygga om hela indexet, vilket minskar driftstopp med upp till 80 % i storskaliga distributioner.

## Förutsättningar
- Java Development Kit (JDK) 8 eller nyare.  
- Maven för beroendehantering.  
- En IDE såsom IntelliJ IDEA eller Eclipse.  
- Grundläggande kunskap om Java‑syntax.

## Konfigurera GroupDocs.Search för Java

Lägg till GroupDocs‑arkivet och beroendet i din `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

Du kan också ladda ner den senaste JAR‑filen direkt från den officiella webbplatsen: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licensförvärv
Börja med en gratis provperiod eller skaffa en tillfällig licens för utvärdering. För produktionsdistributioner, köp en full licens för att låsa upp alla funktioner.

## Implementeringsguide

Implementeringen är uppdelad i två praktiska sektioner: **highlighting in entire documents** och **highlighting in fragments**. Båda sektionerna innehåller de väsentliga stegen för **how to highlight Java** dokument med hjälp av GroupDocs.Search.

### Konfigurera indexinställningar

Innan indexering, konfigurera lagringen för att använda hög kompression—detta minskar diskutrymmet med upp till 70 % samtidigt som sökhastigheten bevaras.

`IndexSettings` är konfigurationsobjektet som styr hur indexet lagras på disk. Ställ in `Compression` till `Compression.High` för att aktivera denna optimering.  
`Compression` specificerar nivån av datakompression som tillämpas på indexfilerna, där `Compression.High` ger maximal storleksreduktion.

## Markering i hela dokument

### Steg 1: skapa och fyll indexet

Skapa en indexmapp och lägg till alla källfiler du vill söka i. Klassen `Index` representerar den sökbara behållaren.

### Steg 2: utför sökning och tillämpa markering

Sök efter termen (t.ex. `ipsum`) och generera en HTML‑fil med markerade träffar. Använd `HighlightOptions` för att specificera markeringsfärgen och om inline‑stilar ska användas.

`HighlightOptions` låter dig definiera förgrunds‑ och bakgrundsfärger samt CSS‑klassen som kommer att tillämpas på varje markerat ord.

`HtmlHighlighter` genererar HTML‑utdata med markerade termer baserat på de angivna alternativen.  
`SearchResult` innehåller listan över matchande dokument och positionerna för varje funnen term.

**Direkt svar:** Ladda ditt index, anropa `search("ipsum")`, och skicka det resulterande `SearchResult` tillsammans med en konfigurerad `HighlightOptions`‑instans till `HtmlHighlighter`. Markören returnerar HTML där varje förekomst av “ipsum” omsluts av en `<span>` med den valda bakgrundsfärgen.

Nyckelalternativ förklarade  
- **Compression** – hög kompression sparar lagring.  
- **HighlightColor** – ställ in vilket RGB‑värde som helst för att matcha ditt UI‑palett.  
- **UseInlineStyles** – `false` genererar ren HTML som kan stylas globalt med CSS.

## Markering i fragment

### Steg 1: indexera och sök (samma som ovan)

Samma index‑ och söksteg gäller; du återanvänder `Index`‑ och `SearchResult`‑objekten.

### Steg 2: definiera fragmentkontext och markering

Specificera hur många termer före och efter matchen som ska visas i varje fragment med `FragmentOptions`.

`FragmentOptions` styr antalet omgivande ord (`termsBefore` och `termsAfter`) som inkluderas i varje utdrag, vilket låter dig balansera kontext mot utdragslängd.

### Steg 3: hämta och skriv markerade fragment

Samla de genererade fragmenten och skriv dem till en HTML‑fil. Varje fragment är redan markerat enligt de `HighlightOptions` du konfigurerat.

`fragmentHighlighter` är ett verktyg som skapar markerade utdrag från ett `SearchResult` med de angivna fragment‑ och markeringsalternativen.

**Direkt svar:** Efter att ha erhållit `SearchResult`, anropa `fragmentHighlighter.highlight(searchResult, fragmentOptions, highlightOptions)`. Metoden returnerar en lista med HTML‑utdrag, var och en innehållande den matchade termen omgiven av det konfigurerade antalet kontextord och markerad med den valda färgen.

## Praktiska tillämpningar
1. **Legal document review** – markera omedelbart lagar, klausuler eller rättsreferenser i tusentals kontrakt.  
2. **Academic research** – framträda nyckelterminologi i dussintals PDF‑ och Word‑filer, vilket minskar litteraturgransknings‑tiden med upp till 60 %.  
3. **Customer support** – identifiera ordernummer eller felkoder i ärendehistorik, vilket gör att agenter kan lösa problem snabbare.

## Prestandaöverväganden
- **Index size** – hög kompression (`Compression.High`) minskar diskavtrycket med upp till 70 % utan märkbar latenspåverkan.  
- **Fragment context** – större `termsBefore/After`‑värden ökar utdragsläsbarheten men kan lägga till 10–15 ms per fråga.  
- **Memory management** – övervaka JVM‑heapen när du indexerar stora korpusar; överväg inkrementell indexering för dataset som överstiger 2 GB för att hålla minnesanvändning under 1 GB.

## Vanliga problem och lösningar
- **Indexing errors** – verifiera filsökvägar och säkerställ att applikationen har läs‑/skrivrättigheter på indexmappen.  
- **No highlights appear** – bekräfta att `UseInlineStyles` matchar ditt utdataformat (HTML vs. PDF).  
- **Color not applied** – se till att RGB‑värdena ligger inom intervallet 0‑255 och att visaren respekterar inline‑CSS eller den medföljande CSS‑klassen.

## Vanliga frågor

**Q: Vilka är fördelarna med att använda GroupDocs.Search for Java?**  
A: Det erbjuder snabb, skalbar indexering, anpassningsbar markering och stöd för över 30 dokumentformat, och bearbetar 500‑sidiga filer på under 2 sekunder på en vanlig server.

**Q: Hur kan jag integrera GroupDocs.Search med ett REST‑API?**  
A: Exponera sök‑ och markeringsmetoderna via Spring Boot‑kontrollers, som returnerar HTML‑utdrag eller JSON‑payloads som innehåller de markerade fragmenten.

**Q: Hanterar biblioteket lösenordsskyddade filer?**  
A: Ja—ange lösenordet när du lägger till dokumentet i indexet via `addDocument(filePath, password)`.

**Q: Kan jag anpassa markerings‑markupen utöver färg?**  
A: Absolut; du kan tilldela en CSS‑klass med `options.setCssClass("myHighlight")` och stilera den globalt, eller modifiera den genererade HTML‑koden efter markering.

**Q: Vilken version testades för den här guiden?**  
A: Koden validerades mot GroupDocs.Search 25.4.

**Q: Hur ställer jag in highlight options java för att använda en CSS‑klass istället för inline‑stilar?**  
A: Anropa `options.setUseInlineStyles(false)` och definiera en CSS‑regel för den klass du tilldelar via `options.setCssClass("myHighlight")`.

**Q: Finns det ett sätt att markera termer i PDF‑utdata direkt?**  
A: Ja—GroupDocs.Search fungerar med PDF‑inmatning, och markören genererar HTML som kan bäddas in i en PDF‑visare eller konverteras tillbaka till PDF med hjälp av GroupDocs.Conversion.

**Senast uppdaterad:** 2026-09-27  
**Testad med:** GroupDocs.Search 25.4  
**Författare:** GroupDocs

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

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

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

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

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

## Relaterade handledningar

- [Hur man implementerar java fulltextssökning: skapa indexkatalog med GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Lär dig hantera sökindex med GroupDocs.Search for Java](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [Lägg till dokument i index med chunk‑baserad sökning i Java](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)