---
date: '2026-09-06'
description: Lär dig hur du filtrerar filändelser java med GroupDocs.Search för Java,
  inklusive logiska AND, OR, NOT-operatorer, date range filters och path filters.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: Filtrera filändelser java med GroupDocs.Search. Lär dig kombinera
  extension, date range och path filters med logiska operatorer i Java.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: Filtrera filändelser java med GroupDocs.Search – Komplett guide
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: Hur man filtrerar filändelser java med GroupDocs.Search
type: docs
url: /sv/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Filfilter för filändelser java med GroupDocs.Search

I den här omfattande handledningen kommer du att lära dig hur du **filter file extensions java** när du indexerar dokument med GroupDocs.Search. I slutet av guiden kommer du att kunna inkludera endast de filtyper du behöver, exkludera oönskade format och kombinera dessa regler med datumintervall- och sökvägsfilter med logiska AND-, OR- och NOT‑operatorer. Detta tillvägagångssätt håller ditt index smalt, påskyndar sökningar och hjälper dig att följa databehandlingspolicyer.

## Snabba svar
- **Vad är java file extension filter?** Det är en regel som talar om för GroupDocs.Search vilka filändelser som ska inkluderas eller exkluderas under indexering.  
- **Vilket bibliotek tillhandahåller denna funktion?** GroupDocs.Search for Java.  
- **Behöver jag en licens?** En gratis provperiod fungerar för utvärdering; en full licens krävs för produktion.  
- **Kan jag kombinera filter?** Ja – du kan kedja ihop extensions-, datum-, storleks- och sökvägsfilter med AND, OR, NOT‑logik.  
- **Är det Maven‑kompatibelt?** Absolut – lägg till GroupDocs.Search‑beroendet i din `pom.xml`.

## Vad är ett java file extension filter?
Ett **java file extension filter** är en regeluppsättning som utvärderar varje fils filändelse innan den skickas till indexeringsmotorn. Genom att ange ändelser som `.txt`, `.pdf` eller `.epub` kan du **include files by extension** eller **exclude files by extension** för att hålla ditt index fokuserat och dina sökresultat relevanta.

## Varför använda filändelsefiltrering med GroupDocs.Search?
Filändelsefiltrering förbättrar indexeringseffektiviteten genom att exkludera irrelevanta format, minskar lagringskraven och hjälper till att uppfylla efterlevnadsregler genom att förhindra oönskat innehåll från att hamna i indexet. Det möjliggör också snabbare svar på frågor eftersom sökmotorn bearbetar en mindre, mer relevant datamängd.

- **Prestanda:** Att hoppa över oönskade filer minskar I/O och påskyndar indexering med upp till 40 % i stora arkiv.  
- **Lagringsbesparingar:** Endast relevanta dokument lagras i indexet, vilket minskar diskutrymmet med i genomsnitt 30 %.  
- **Efterlevnad:** Förhindra oavsiktlig indexering av konfidentiella eller ej stödda filtyper.  
- **Flexibilitet:** Kombinera med **date range filter java**-funktioner för att rikta in dig på filer som skapats eller modifierats inom specifika perioder.

## Förutsättningar

Innan vi börjar, se till att du har följande:

### Nödvändiga bibliotek och beroenden
- **GroupDocs.Search for Java** – version 25.4 eller senare (stödjer 60+ inmatningsformat).  
- **Java Development Kit (JDK)** – någon kompatibel version (8 eller nyare).

### Miljöinställning
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse eller någon Maven‑kompatibel IDE.

### Kunskapsförutsättningar
- Grundläggande Java-programmering.  
- Bekantskap med fil‑I/O i Java.  
- Förståelse för reguljära uttryck och datum‑tidshantering.

## Konfigurera GroupDocs.Search för Java
För att börja använda GroupDocs.Search måste du inkludera det som ett beroende i ditt projekt.

### Maven‑konfiguration
Lägg till följande repository‑ och beroende‑konfiguration i din `pom.xml`‑fil:

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

### Direkt nedladdning
Alternativt, ladda ner den senaste versionen direkt från [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Licensförvärv
1. **Free trial** – utforska funktionerna utan kostnad.  
2. **Temporary license** – få full funktionalitet under en begränsad period.  
3. **Purchase** – skaffa en permanent licens för produktionsbruk.

### Grundläggande initiering och konfiguration
När biblioteket har lagts till, initiera din indexeringsmiljö. Klassen `IndexSettings` innehåller alla konfigurationsalternativ, inklusive filter.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Implementeringsguide
Nedan går vi igenom varje filtertyp, förklarar **why it matters** och ger steg‑för‑steg‑instruktioner som du kan kopiera in i ditt projekt.

### Filändelsefiltrering
Filtrera filer efter deras filändelser under indexering. Detta är perfekt när du bara vill bearbeta e‑böcker (`.fb2`, `.epub`) och rena textfiler (`.txt`).

#### Översikt
`DocumentFilter.createFileExtension` skapar en vitlista av filändelser.

#### Implementeringssteg
1. **Create filter** – definiera de filändelser du vill behålla.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize index and add documents** – tillämpa filtret när du konstruerar `IndexSettings`.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logiskt NOT‑filter
Exkludera specifika filändelser, såsom webbsidor och PDF‑filer, när de inte behövs för ditt sökscenario.

#### Implementeringssteg
1. **Create exclusion filter** – ange filändelser som ska avvisas.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to index settings** – kombinera NOT‑filtret med andra regler.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add documents** – endast filer som klarar det kombinerade filtret indexeras.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logiskt AND‑filter
Kombinera flera villkor—skapandedatum, filändelse och filstorlek—så att **only files that meet all criteria** indexeras.

#### Översikt
`DocumentFilter.createAnd` slår samman flera filter till en enda regel.

#### Implementeringssteg
1. **Define filters** – skapa individuella filter för varje villkor.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine filters** – använd AND‑operatorn för att kräva alla villkor.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index documents** – mata in det kombinerade filtret i indexeringspipeline.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logiskt OR‑filter
Inkludera filer som uppfyller **any** av de angivna villkoren—användbart när du vill fånga både små textfiler och större icke‑textfiler.

#### Implementeringssteg
1. **Define filters** – skapa separata filter för varje alternativt villkor.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine filters with logical conditions** – använd OR‑operatorn.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR filter** – fäst det kombinerade filtret till indexkonfigurationen.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Skapandetidsfilter
Målsätt filer som skapats inom en specifik period—ett klassiskt **date range filter java**-scenario.

#### Implementeringssteg
1. **Define date‑range filter** – ange start- och slutdatum.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index documents** – endast filer vars skapelsestämplar faller inom intervallet indexeras.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Modifieringstidsfilter
Exkludera filer som modifierats efter ett visst avstängningsdatum.

#### Implementeringssteg
1. **Define filter** – sätt det maximala modifieringstidstämpeln.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index documents** – filer som är nyare än avstängningsdatumet ignoreras.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filvägsfiltrering
Begränsa indexering till filer som finns i specifika mappar eller matchar ett mönster—idealiskt för **include files by extension** inom en viss kataloghierarki.

#### Implementeringssteg
1. **Define file‑path filter** – använd glob‑ eller regex‑mönster för att matcha kataloger.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize index and add documents** – tillämpa sökvägsfiltret tillsammans med andra regler.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Vanliga fallgropar & tips

- **Never mix absolute and relative paths** i samma filterkonfiguration – det kan leda till oväntade exkluderingar.  
- **Reset the `IndexSettings`** när du byter filteruppsättningar; annars kan tidigare filter kvarstå.  
- **Combine a length upper bound with an extension filter** för stora samlingar för att hålla minnesanvändningen låg.  
- LoggingOptions styr loggningskonfigurationen för GroupDocs.Search.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) för att se varför en fil avvisades.  

## Vanliga frågor

**Q: Kan jag ändra filterkriterierna efter att indexet har skapats?**  
A: Ja. Bygg om indexet med ett nytt `DocumentFilter` eller använd inkrementell indexering med uppdaterade inställningar.

**Q: Fungerar java file extension filter på komprimerade arkiv (t.ex. ZIP)?**  
A: GroupDocs.Search kan indexera stödda arkivformat, men filändelsefiltret gäller själva arkivet, inte de inre filerna. Använd nästlade filter för djupare kontroll.

**Q: Hur felsöker jag varför en viss fil exkluderades?**  
A: Aktivera bibliotekets loggning (`LoggingOptions.setEnabled(true)`) och inspektera loggen – den rapporterar vilket filter som avvisade varje fil.

**Q: Är det möjligt att kombinera java file extension filter med anpassade regex‑filter?**  
A: Absolut. Inkludera ett regex‑filter i `DocumentFilter.createAnd()` tillsammans med filändelsefiltret.

**Q: Vilken prestandapåverkan har det att lägga till många filter?**  
A: Varje filter tillför en måttlig overhead under indexering, men minskningen av indexerad data väger vanligtvis upp kostnaden. Testa med ett representativt urval för att hitta den optimala balansen.

---

**Senast uppdaterad:** 2026-09-06  
**Testat med:** GroupDocs.Search 25.4 for Java  
**Författare:** GroupDocs

## Relaterade handledningar

- [Anpassat datumformat Java | Datumintervallssökning med GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: Mästra booleska sökningar med GroupDocs.Search för Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Optimera sökprestanda med avancerade indexeringstekniker i GroupDocs.Search för Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}