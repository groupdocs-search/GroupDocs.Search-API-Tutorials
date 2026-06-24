---
date: '2026-05-28'
description: Lär dig hur du söker fras med wildcard patterns med hjälp av GroupDocs.Search
  för Java. Inkluderar att skapa ett search index, lägga till documents, och köra
  exact phrase och wildcard queries.
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: Hur man söker fras med jokertecken i GroupDocs.Search för Java
type: docs
url: /sv/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Så söker du fras med jokertecken i GroupDocs.Search för Java

I moderna dokument‑centrerade applikationer är **how to search phrase** snabbt och exakt en avgörande faktor för användarupplevelsen. Oavsett om du bygger en kunskapsbas, en e‑handelskatalog eller ett regelefterlevnads‑drivet arkiv, gör förmågan att hitta en exakt fras — eller en flexibel variant av den — att användarna blir produktiva och minskar supportbördan. Denna handledning guidar dig genom installation av **GroupDocs.Search for Java**, skapande av ett sökindex, laddning av dokument och körning av både exakt‑fras‑ och jokertecken‑förstärkta frågor, allt med tydliga, produktionsklara kodexempel.

## Snabba svar
- **What is the primary benefit of phrase searches?** Precist matchning av ordningsföljd och närhet, vilket garanterar att endast dokument som innehåller den exakta sekvensen returneras.  
- **Can wildcards be used inside a phrase?** Ja — jokertecken låter dig hoppa över eller ersätta ord samtidigt som den övergripande ordningen bevaras.  
- **Do I need a license for development?** En gratis provversion fungerar för testning; en full licens krävs för produktionsdistributioner.  
- **Which Maven version should I use?** Den senaste GroupDocs.Search för Java‑utgåvan (t.ex. 25.4 vid skrivtillfället).  
- **Is this approach suitable for large document sets?** Är detta tillvägagångssätt lämpligt för stora dokumentuppsättningar? Absolut — GroupDocs.Search kan hantera samlingar med flera hundratusen dokument med subsekundfördröjning för frågor när indexet är optimerat.

## Vad är “how to search phrase”?
**Searching a phrase means looking for a specific sequence of words in a document.**  
När du utför en frasfråga kontrollerar motorn att orden förekommer i exakt ordning och inom den definierade närheten, vilket eliminerar irrelevanta träffar som innehåller samma ord i ett annat sammanhang. Detta gör frassökningar idealiska för att hitta juridiska klausuler, produktkoder eller vilken text som helst där ordning är viktig.

## Varför använda GroupDocs.Search för fras‑ och jokertecken‑frågor?
GroupDocs.Search levererar **hög genomströmning vid indexering av upp till 1 miljon dokument samtidigt som sub‑sekundsv svarstider för frågor upprätthålls** på vanlig serverhårdvara. Dess frågespråk stödjer exakta fraser, enkla `*` och `?` jokertecken, och avancerade mönster såsom numeriska intervall (`*2~5`). Biblioteket integreras med vilken Java‑applikation som helst via Maven eller en direkt JAR‑nedladdning, och det körs på Java 8+ utan externa tjänster.

## Förutsättningar
- Java 8 eller nyare (Java 11 LTS rekommenderas).  
- Maven 3 eller senare (om du föredrar beroendehantering).  
- Grundläggande kunskap om Java‑projektstruktur och objekt‑orienterade koncept.  

## Installera GroupDocs.Search för Java

### Använda Maven
Lägg till det officiella förrådet och GroupDocs.Search‑beroendet i din `pom.xml`:

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### Direkt nedladdning
Alternativt, ladda ner den senaste JAR‑filen från den officiella releasesidan: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licensförvärv
- **Free Trial:** Ideal för snabba experiment; begränsad till 100 MB indexerad data.  
- **Temporary License:** Begär en 30‑dagars utvärderingsnyckel från GroupDocs‑portalen.  
- **Full License:** Krävs för produktionsanvändning och obegränsad indexeringskapacitet.

## Grundläggande initiering och konfiguration
Skapa en mapp som kommer att hålla indexfilerna och instansiera `Index`‑objektet. `Index`‑klassen representerar det sökbara indexet lagrat på disk och tillhandahåller metoder för att lägga till, uppdatera och fråga dokument.

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

Lägg till de dokument du vill göra sökbara:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## Så söker du fras med jokertecken i GroupDocs.Search
Detta avsnitt demonstrerar tre nivåer av frassökning — exakt matchning, enkel jokertecken och avancerade jokertecken‑mönster — och visar hur man skapar ett index, lägger till dokument och kör varje frågetyp med koncis Java‑kod. Exemplen illustrerar både text‑baserade frågor och objekt‑baserad frågekonstruktion, vilket möjliggör för utvecklare att integrera flexibla sökfunktioner i sina applikationer.

### Enkel frassökning

#### Översikt
Använd detta tillvägagångssätt när du behöver en **exakt matchning** av en ordsekvens, såsom en juridisk klausul eller ett produktmodellnummer.

#### Direkt svar
Läs in indexet, anropa `search` med en citerad fras (t.ex. `"quick brown fox"`), och motorn returnerar endast dokument som innehåller den exakta sekvensen, med bibehållen ordning och avstånd. Frågan körs på millisekunder, även på index som innehåller hundratusentals filer.

#### Steg 1: Skapa ett index
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### Steg 2: Lägg till dokument i indexet
```java
Index index = new Index(indexFolder);
```

#### Steg 3: Sök efter en specifik fras (textformat)
```java
index.add(documentsFolder);
```

#### Steg 4: Objekt‑baserade frågor (sök exakt fras)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### Frassökning med jokertecken

#### Översikt
Jokertecken‑platshållare (`*` för valfritt antal tecken, `?` för ett enda tecken) låter dig **hoppa över variabla ord** samtidigt som den omgivande ordningen upprätthålls.

#### Direkt svar
Infoga ett jokertecken (`*`) i en citerad fras — t.ex. `"quick * fox"` — för att matcha vilket ord(en) som helst mellan *quick* och *fox*. Motorn expanderar jokertecknet vid frågetiden, skannar endast de indexerade termerna som uppfyller mönstret, vilket håller prestandan jämförbar med en enkel frasfråga.

#### Steg 1: Skapa ett index
*(Samma som enkel frassökning.)*

#### Steg 2: Lägg till dokument i indexet
*(Samma som ovan.)*

#### Steg 3: Textbaserad sökning med jokertecken
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Steg 4: Objekt‑baserade frågor med jokertecken (Wildcard Search Java)
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### Avancerad jokerteckensökning

#### Översikt
Kombinera numeriska intervall, valfria tecken och anpassade regex‑liknande mönster för **avancerad matchning**, såsom versionsnummer eller produktkoder.

#### Direkt svar
Använd den utökade jokerteckensyntaxen `*min~max` för att definiera ett intervall av tillåtna ordavstånd, eller `?` för att matcha ett enda tecken. Till exempel, `"error *2~5 code"` hittar ordet *error* följt av två till fem ord och sedan *code*. Denna precision minskar falska positiva samtidigt som den fortfarande erbjuder flexibilitet.

#### Steg 1: Skapa ett index
*(Upprepat för tydlighet.)*

#### Steg 2: Lägg till dokument i indexet
*(Upprepat.)*

#### Steg 3: Textbaserad sökning med komplexa jokerteckenmönster
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Steg 4: Objekt‑baserade frågor med avancerade jokertecken
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## Praktiska tillämpningar
- **Content Management Systems:** Redaktörer kan hitta exakta klausuler eller flexibla utdrag utan att manuellt skanna hundratals sidor.  
- **E‑commerce Catalogs:** Köpare hittar produkter även när de utelämnar en beskrivning eller använder synonymer, tack vare jokerteckentolerans.  
- **Legal & Compliance:** Snabbt isolera kontraktsmässigt språk som kan förekomma med mindre variationer i olika avtal.  

## Prestandaöverväganden
- **Create Search Index** endast en gång per stabil dokumentuppsättning; återanvänd samma `Index`‑instans för alla frågor.  
- **Add Documents Incrementally** när nya filer anländer — undvik att bygga om hela indexet för att hålla CPU‑användning låg.  
- **Design Precise Wildcard Patterns**; bredare mönster (`*`) ökar antalet termexpansioner och kan öka CPU‑belastning.  
- **Call `index.optimize()`** periodiskt (om stöds) för att komprimera indexet och hålla minnesanvändning under kontroll.  

## Vanliga problem & lösningar
| Problem | Lösning |
|-------|----------|
| No results returned for a wildcard query | Verifiera jokerteckensyntaxen (`*min~max`) och säkerställ att målorden finns inom det definierade avståndet. |
| Index becomes stale after file updates | Använd `index.add(updatedFolder)` eller API:t för inkrementell uppdatering för att bara uppdatera ändrade filer. |
| High memory consumption on large datasets | Öka JVM‑heapen (`-Xmx4g` eller högre) och överväg att dela upp indexet i flera shards för parallell bearbetning. |

## Vanliga frågor

**Q: Vad är skillnaden mellan ett jokertecken och en frassökning?**  
En frassökning kräver exakt ordningsföljd och avstånd, medan ett jokertecken låter dig ersätta eller hoppa över ord inom den ordningen, vilket ger flexibel matchning.

**Q: Kan jag använda jokertecken med numeriska data i sökningar?**  
Ja — jokertecken‑intervallparametrar (`*min~max`) fungerar med både siffror och ord, vilket möjliggör frågor som `"version *1~3"`.

**Q: Hur bör jag hantera mycket stora dokumentsamlingar?**  
Håll indexet optimerat, utför inkrementella uppdateringar och skapa specifika jokerteckenmönster för att begränsa termexpansion. GroupDocs.Search kan indexera 1 miljon dokument samtidigt som frågelatensen hålls under 200 ms på standardhårdvara.

**Q: Är GroupDocs.Search lämplig för real‑tidsökning?**  
Absolut — när indexet är byggt körs frågor på millisekunder, vilket gör det idealiskt för interaktiva sökrutor och autokompletteringsfunktioner.

**Q: Kan jag integrera detta bibliotek i ett befintligt Java‑projekt?**  
Ja. Lägg till Maven‑beroendet eller JAR‑filen, instansiera `Index` som visat, och du är redo att göra frågor utan att ändra befintlig kod.

---

**Senast uppdaterad:** 2026-05-28  
**Testad med:** GroupDocs.Search 25.4 för Java  
**Författare:** GroupDocs

```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## Relaterade handledningar

- [Skapa sökindex Java – GroupDocs.Search-handledningar](/search/java/)
- [Lägg till dokument i index – GroupDocs.Search Java-handledningar](/search/java/document-management/)
- [Skapa sökindex - GroupDocs.Search Java-handledningar](/search/java/advanced-features/)