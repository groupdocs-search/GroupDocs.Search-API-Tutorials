---
date: '2026-02-19'
description: Lär dig hur du inaktiverar stoppord i sökningar och lägger till dokument
  i indexet med GroupDocs.Search för Java, vilket ökar sökfrågans noggrannhet.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 'Stopord i sökning: Lägg till dokument i index med GroupDocs.Search Java'
type: docs
url: /sv/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Stoppord i sökning: Lägg till dokument i index med GroupDocs.Search Java

Om du behöver **lägga till dokument i index** samtidigt som du säkerställer att ingen viktig term—särskilt vanliga—ignoreras, har du kommit till rätt ställe. I den här guiden visar vi hur du **inaktiverar stoppord i sökning** med GroupDocs.Search för Java, så varje token (även “on”, “by” eller “the”) blir sökbar och dina resultat blir mycket mer exakta.

## Snabba svar
- **Vad betyder “add documents to index”?** Det betyder att ladda dina källfiler i ett sökbart index så att de kan frågas effektivt.  
- **Varför skulle jag inaktivera stoppord?** För att inkludera vanliga ord (t.ex. “on”, “the”) i sökningar när dessa termer är meningsfulla för din domän.  
- **Vilken biblioteksversion krävs?** GroupDocs.Search för Java 25.4 eller senare.  
- **Behöver jag en licens?** En gratis provperiod fungerar för utvärdering; en permanent licens krävs för produktion.  
- **Kan jag använda detta i ett Maven‑projekt?** Ja – lägg bara till förrådet och beroendet som visas nedan.

## Vad är stoppord i sökning och varför kan du vilja inaktivera dem?
Stoppord är frekventa termer som många sökmotorer automatiskt filtrerar bort för att snabba upp frågor. Även om detta förbättrar prestanda för generiska webbsökningar, kan det försämra precisionen i specialiserade domäner—juridiska kontrakt, e‑handelskataloger eller tekniska manualer—där ord som “on”, “by” eller “as” har verklig betydelse. Att inaktivera stoppord låter dig behandla varje ord som betydelsefullt, vilket säkerställer att inget relevant dokument missas.

## Hur fungerar att lägga till dokument i index i GroupDocs.Search?
När du lägger till dokument läser biblioteket varje fil, tokeniserar dess innehåll och lagrar tokenarna i en optimerad datastruktur (indexet). När det är indexerat kan motorn hämta matchande dokument på millisekunder, även för stora samlingar.

## Förutsättningar

- **Krävda bibliotek**: GroupDocs.Search för Java 25.4 (eller nyare).  
- **Utvecklingsmiljö**: IntelliJ IDEA, Eclipse eller någon Java‑IDE du föredrar.  
- **Grundläggande kunskap**: Bekantskap med Java‑syntax och konceptet indexering.

## Installera GroupDocs.Search för Java

### Maven‑installation

Om du använder Maven, inkludera följande i din `pom.xml`:

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

Alternativt, ladda ner den senaste versionen från [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Steg för att skaffa licens
- **Gratis provperiod** – börja testa omedelbart.  
- **Tillfällig licens** – skaffa en tidsbegränsad nyckel för full funktionalitet.  
- **Köp** – säkra en permanent licens för produktionsanvändning.

## Grundläggande initiering och konfiguration

Skapa en instans av `IndexSettings` för att styra hur indexet beter sig:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Hur man inaktiverar stoppord i sökning (Java)

Följande rad stänger av det inbyggda stoppordfiltret:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Parametrar*: `setUseStopWords` accepterar ett boolean‑värde.  
*Syfte*: Säkerställer att varje ord—inklusive vanliga stoppord—indexeras och är sökbart.

## Hur man lägger till dokument i index

### Definiera utdatamappen

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Specificera dokumentmappen

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Nu blir varje fil i `YOUR_DOCUMENT_DIRECTORY` **added documents to index** och klar för frågor.

## Utföra en sökfråga

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Eftersom stoppord är inaktiverade kommer termen `"on"` att beaktas under sökningen, vilket returnerar träffar som annars skulle ignoreras.

## Praktiska tillämpningar

1. **Företagsdokument­sökning** – Säkerställ att kritisk terminologi inte filtreras bort.  
2. **E‑handelsplattformar** – Förbättra produktupptäckt genom att indexera varje ord i produktbeskrivningar.  
3. **Juridiska forskningsverktyg** – Fånga varje juridisk term, även de som vanligtvis behandlas som stoppord.

## Prestandaöverväganden

- **Optimeringstips**: Uppdatera och rensa ditt index regelbundet för att hålla sökhastigheten hög.  
- **Resursanvändning**: Övervaka JVM‑heap‑storlek; stora index kan kräva justering av skräpsamlingsinställningar.  
- **Java‑minneshantering**: Använd effektiva datastrukturer och överväg off‑heap‑lagring för mycket stora korpusar.

## Vanliga problem och lösningar

| Symptom | Likely Cause | Fix |
|---|---|---|
| Inga resultat för vanliga ord | `setUseStopWords(true)` (standard) | Anropa `setUseStopWords(false)` som visas ovan. |
| Out‑of‑memory‑fel under indexering | Indexering av för många stora filer samtidigt | Indexera filer i batcher; öka `-Xmx`‑JVM‑alternativet. |
| Sökning returnerar föråldrad data | Indexet uppdateras inte efter att nya filer lagts till | Anropa `index.update()` eller lägg till de ändrade dokumenten igen. |

## Vanliga frågor

**Q: Vad är stoppord?**  
A: Stoppord är vanliga termer (t.ex. “the”, “is”, “on”) som många sökmotorer ignorerar för att snabba upp frågor. Att inaktivera dem låter dig behandla varje token som sökbar.

**Q: Varför inaktivera stoppord i sökindex?**  
A: När exakt frasmatchning krävs—t.ex. i juridiska eller tekniska dokument—bär varje ord betydelse, så du måste inkludera stoppord.

**Q: Hur hanterar GroupDocs.Search stora datamängder?**  
A: Biblioteket använder optimerade datastrukturer och inkrementell indexering för att hålla minnesanvändningen låg, även med miljontals dokument.

**Q: Kan jag integrera GroupDocs.Search med andra Java‑applikationer?**  
A: Ja, API:et är designat för enkel inbäddning i vilket Java‑baserat system som helst, från webbtjänster till skrivbordsappar.

**Q: Vad ska jag göra om mina sökresultat inte är korrekta?**  
A: Verifiera att indexet innehåller alla nödvändiga dokument (`add documents to index`), säkerställ att stoppordsfiltret är inaktiverat om det behövs, och överväg att bygga om indexet efter större förändringar.

## Ytterligare resurser

- **Dokumentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API‑referens**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Nedladdning**: [Hämta den senaste GroupDocs.Search för Java](https://releases.groupdocs.com/search/java/)
- **GitHub‑arkiv**: [Utforska på GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Gratis support**: [Gå med i GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Tillfällig licens**: [Ansök om en tillfällig licens](https://purchase.groupdocs.com/temporary-license/)

Genom att följa den här guiden vet du nu hur du **add documents to index** och **disable stop words in search** för att leverera mer exakta resultat i dina Java‑applikationer.

---

**Senast uppdaterad:** 2026-02-19  
**Testat med:** GroupDocs.Search för Java 25.4  
**Författare:** GroupDocs  

---