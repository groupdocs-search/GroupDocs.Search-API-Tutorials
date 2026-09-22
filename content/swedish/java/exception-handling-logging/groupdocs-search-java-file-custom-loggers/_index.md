---
date: '2026-09-21'
description: Lär dig hur du skapar logger, ställer in max loggstorlek och använder
  console logger i GroupDocs.Search för Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Lär dig hur du skapar logger, ställer in max loggstorlek och använder
  console logger i GroupDocs.Search för Java. Följ steg‑för‑steg‑instruktioner och
  bästa‑praxis‑tips.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Hur man skapar logger och begränsar loggstorlek i GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: Hur man skapar logger och begränsar loggstorlek i GroupDocs.Search för Java
type: docs
url: /sv/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Hur man skapar logger och begränsar loggfilens storlek i GroupDocs.Search för Java

I den här handledningen kommer du att **skapa logger**‑implementationer för GroupDocs.Search, konfigurera en maximal loggfilstorlek och växla mellan fil‑baserad och konsollogging. Korrekt logghantering förhindrar att diskar fylls upp under stora indexeringsjobb, förbättrar felsökning och ger dig omedelbar återkoppling under utveckling. Vi börjar med Maven‑installationen, går igenom logger‑konfigurationen och avslutar med en enkel sökfråga som demonstrerar loggern i praktiken.

## Snabba svar
- **Vad betyder “begränsa loggfilens storlek”?** Det sätter en gräns för den maximala storleken på en loggfil, vilket förhindrar okontrollerad tillväxt på disken.  
- **Vilken logger låter dig begränsa loggfilens storlek?** Den inbyggda `FileLogger` accepterar en max‑storleksparameter.  
- **Hur använder jag console logger java?** Instansiera `ConsoleLogger` och sätt den på `IndexSettings`.  
- **Behöver jag en licens för GroupDocs.Search?** En provversion fungerar för utvärdering; en kommersiell licens krävs för produktion.  
- **Vad är första steget?** Lägg till GroupDocs.Search‑beroendet i ditt Maven‑projekt.  

## Vad är begränsning av loggfilens storlek?
**Begränsning av loggfilens storlek**‑inställningen talar om för loggern att sluta skriva nya poster när filen når ett definierat tröskelvärde (t.ex. 4 MB). När gränsen nås, antingen kastar loggern bort ytterligare meddelanden eller roterar till en ny fil, vilket gör diskanvändningen förutsägbar.

## Varför använda fil‑ och anpassade loggers med GroupDocs.Search?
Fil‑ och anpassade loggers ger dig möjlighet till revision, felsökningsinsikt och flexibilitet. I produktionsmiljöer ger filloggar en permanent registrering av varje indexerings‑ och sökoperation, medan konsolloggar levererar omedelbar återkoppling under utveckling. Dessa loggar hjälper team att övervaka prestanda, spåra fel och uppfylla efterlevnadskrav genom att bevara en detaljerad aktivitetsspårning.

## Förutsättningar
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 eller nyare, med en IDE såsom IntelliJ IDEA eller Eclipse.  
- Grundläggande kunskap om Maven och Java‑programmering.  

## Installera GroupDocs.Search för Java

Lägg till biblioteket i ditt projekt med någon av metoderna nedan.

**Maven setup:**  

```text
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
```

**Direkt nedladdning:**  
Download the latest JAR from the official site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licensanskaffning
Obtain a trial or purchase a license via the [licensing page](https://purchase.groupdocs.com/temporary-license/).

## Hur man skapar en anpassad logger för GroupDocs.Search
Att skapa en anpassad logger är enkelt eftersom GroupDocs.Search förlitar sig på `ILogger`‑gränssnittet. Genom att implementera detta gränssnitt—eller genom att ärva den medföljande `FileLogger` eller `ConsoleLogger`—kan du injicera ytterligare beteende såsom fjärrvidarebefordran eller loggrotation. Du kan också lägga till initialiseringslogik, som att öppna nätverksanslutningar, och säkerställa att resurser stängs i loggerns avstängningsmetod. Detta tillvägagångssätt låter dig integrera med övervakningsplattformar som ELK eller Splunk.

### Definition ankare
`ILogger` är det centrala loggkontraktet i GroupDocs.Search; vilken klass som helst som implementerar dess `log(Level, String)`‑metod kan bli en logger.

### Exempelmetod (utan kodblock)
1. Skapa en klass som implementerar `ILogger`.  
2. Åsidosätt `log`‑metoden för att skriva meddelanden till ditt valda mål (fil, databas, HTTP‑endpoint).  
3. I indexkonfigurationen, anropa `settings.setLogger(new YourCustomLogger())`.  

## Hur man begränsar loggfilens storlek med File Logger
`FileLogger`‑klassen skriver loggposter till en fil på disken och accepterar ett argument för maximal storlek. Genom att ange storleksgränsen stoppar loggern automatiskt att lägga till nya poster eller skapar en ny fil när tröskeln nås, vilket förhindrar okontrollerad diskökning. Detta beteende säkerställer att loggning inte stör indexeringsprestanda samtidigt som en koncis händelserapport hålls.

### Definition ankare
`FileLogger` är en inbyggd logger som sparar meddelanden i en textfil och stödjer en konfigurerbar maximal filstorlek.

### Steg‑för‑steg guide
1️⃣ **Importera nödvändiga paket**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Ställ in indexinställningar med File Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **Skapa eller ladda indexet**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Lägg till dokument i indexet**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Utför en sökfråga**  
```text
```java
SearchResult result = index.search(query);
```
```

**Viktigt:** `FileLogger`‑konstruktorns andra argument (`4.0`) definierar **maximal loggstorlek** i megabyte, vilket direkt adresserar kravet på **begränsning av loggfilens storlek**.

## Hur man använder console logger java
När du behöver omedelbar synlighet av logghändelser skriver `ConsoleLogger` varje meddelande till `System.out`. Denna logger är lättviktig och trådsäker, vilket gör den lämplig för utvecklings‑ och felsökningssessioner. Den ger omedelbar återkoppling om indexeringsframsteg, sökfrågor och fel utan att kräva fil‑I/O, vilket kan snabba upp iterativ testning.

### Definition ankare
`ConsoleLogger` är en lättviktig logger som skriver loggposter till standardkonsolströmmen, vilket gör den idealisk för felsökningssessioner.

### Konfigurationssteg
1️⃣ **Importera konsolloggern**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Ställ in indexinställningar med Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Skapa eller ladda indexet**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Lägg till dokument och utför en sökning**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Tips:** Konsolloggern är idealisk under utveckling eftersom den skriver ut varje loggpost omedelbart, vilket hjälper dig att verifiera att indexering och sökning fungerar som förväntat.

## Praktiska tillämpningar
1. **Dokumenthanteringssystem:** Behåll revisionsspår för varje dokument som indexeras, vilket uppfyller efterlevnadskrav.  
2. **Företagssökmotorer:** Övervaka frågeprestanda och felhastigheter i realtid, vilket möjliggör snabba SLA‑kontroller.  
3. **Juridisk & efterlevnadsprogramvara:** Registrera sökord och tidsstämplar för regulatorisk rapportering, med loggar bevarade under den föreskrivna lagringsperioden.

## Prestandaöverväganden
- **Loggstorlek:** Genom att **sätta maximal loggstorlek** undviker du överdriven diskanvändning som annars kan sakta ner JVM:s skräpsamlare.  
- **Asynkron loggning:** För hög‑genomströmning, omslut din logger i en asynkron kö för att frikoppla I/O från indexeringstråden (implementation utanför denna guides omfattning).  
- **Minneshantering:** Frigör stora `Index`‑objekt med `index.close()` när de inte längre behövs för att hålla JVM‑avtrycket lågt.

## Vanliga problem & lösningar
- **Loggväg ej åtkomlig:** Verifiera att katalogen finns och att applikationen har skrivbehörighet för det användarkonto som kör JVM.  
- **Loggern avfyras inte:** Säkerställ att du anropar `settings.setLogger(...)` *innan* du skapar `Index`‑objektet; annars används standardloggern.  
- **Konsolutdata saknas:** Bekräfta att du kör applikationen i en terminal som visar `System.out`, och att inget logg‑ramverk (t.ex. SLF4J) avlyssnar utdata.

## Vanliga frågor

**Q: Vad styr den andra parametern i `FileLogger`?**  
A: Den sätter den maximala storleken på loggfilen i megabyte, vilket låter dig **sätta maximal loggstorlek** och förhindra okontrollerad tillväxt.

**Q: Kan jag kombinera fil‑ och konsolloggers?**  
A: Ja. Skapa en anpassad logger som vidarebefordrar varje `log`‑anrop till både en `FileLogger` och en `ConsoleLogger`, och registrera sedan den sammansatta loggern med `IndexSettings`.

**Q: Hur lägger jag till dokument i indexet efter den initiala skapelsen?**  
A: Anropa `index.add(pathToNewDocs)` när som helst; den konfigurerade loggern kommer automatiskt att registrera tillägget.

**Q: Är `ConsoleLogger` trådsäker?**  
A: Den skriver direkt till `System.out`, vilket JVM synkroniserar internt, vilket gör den säker för typiska flertrådade användningsfall.

**Q: Påverkar begränsning av loggfilens storlek mängden lagrad information?**  
A: När storleksgränsen nås, kastas nya poster antingen bort eller roterar loggern till en ny fil, beroende på den implementering du väljer.

## Resurser
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

**Last Updated:** 2026-09-21  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs  

## Relaterade handledningar

- [Hur man implementerar loggning - Undantagshantering och loggningshandledningar för GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Implementera asynkron loggning i Java med GroupDocs.Search – Guide för anpassad logger](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Skapa sökindex Java – GroupDocs.Search handledningar](/search/java/indexing/)