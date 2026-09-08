---
date: '2026-07-31'
description: Lär dig hur du implementerar skiftlägesokänslig sökning i Java genom
  att lägga till dokument i ett index med GroupDocs.Search, och använder teckenersättning
  för att normalisera text under indexering.
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: Skiftlägesokänslig sökning i Java låter dig lägga till dokument i
  ett index och söka dem utan att oroa dig för bokstavsstorlek. Denna guide visar
  hur GroupDocs.Search normaliserar text under indexering för snabba, pålitliga resultat.
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Skiftlägesokänslig sökning Java – Indexera dokument med GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: Lägg till dokument i index för skiftlägesokänslig sökning i Java
type: docs
url: /sv/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# Lägg till dokument i index för skiftlägesokänslig sökning i Java

När du behöver **case insensitive search java** som på ett pålitligt sätt hittar information oavsett hur användare skriver den, är nyckeln att lägga till dokument i ett index samtidigt som texten normaliseras. I den här handledningen går vi igenom hur du konfigurerar GroupDocs.Search för Java så att varje dokument du indexerar automatiskt omvandlas till gemener (eller på annat sätt transformeras) under indexeringen, vilket garanterar skiftlägesokänsliga resultat utan extra logik vid frågetiden.

## Snabba svar
- **Vad betyder “add documents to index”?** Det betyder att ladda källfiler i en sökbar datastruktur så att de kan frågas senare.  
- **Varför använda teckenersättning?** Det normaliserar varje tecken—vanligtvis till gemener—så att sökningar automatiskt ignorerar skillnader i skiftläge.  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en full licens krävs för produktionsdistributioner.  
- **Vilken Java-version krävs?** Java 8 eller nyare; biblioteket riktar sig mot Java 11+ för optimal prestanda.  
- **Kan jag växla till skiftlägeskänslig sökning vid behov?** Ja—sökalternativ låter dig växla skiftlägeskänslighet per fråga.

## Vad betyder “add documents to index” i GroupDocs.Search?

Ladda dina källfiler (PDF, DOCX, TXT osv.) i ett sökbart index så att motorn kan hämta dem snabbt. Att lägga till dokument i ett index analyserar varje fil, extraherar ren text och lagrar den i en optimerad datastruktur som möjliggör snabba uppslag.

## Varför aktivera teckenersättning under indexering?

Teckenersättning konverterar varje tecken till en fördefinierad motsvarighet—vanligtvis gemener—under byggandet av indexet. Detta säkerställer att variationer i versalisering, diakritiska tecken eller lokalspecifika symboler inte påverkar sökresultaten. Genom att normalisera texten vid indexering kan motorn matcha frågor mot en konsekvent tokenuppsättning, vilket ger snabb, pålitlig skiftlägesokänslig funktion utan extra bearbetning för varje sökning.

## Förutsättningar
- **GroupDocs.Search for Java** version 25.4 eller nyare (biblioteket stödjer över 30 filformat och kan indexera dokument med flera hundra sidor utan att ladda hela filen i minnet).  
- **Java Development Kit (JDK)** 8 eller senare installerat.  
- Grundläggande kunskap om **Maven** (eller möjlighet att lägga till JAR-filer manuellt).  

## Konfigurera GroupDocs.Search för Java

### Maven-inställning
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

### Direkt nedladdning
Om du föredrar att inte använda Maven, hämta den senaste JAR‑filen från den officiella sidan: [GroupDocs.Search för Java-utgåvor](https://releases.groupdocs.com/search/java/).

### Licensanskaffning
- **Free Trial** – ladda ner en provlicens för att börja experimentera.  
- **Temporary License** – begär en utökad testlicens från GroupDocs‑portalen.  
- **Full License** – köp en produktionslicens när du är redo att gå live.

### Grundläggande initiering (Skapa indexet)
Följande kodsnutt skapar en indexmapp och aktiverar teckenersättningar:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Implementeringsguide

### Aktivera teckenersättning i indexinställningarna
Att aktivera den här funktionen instruerar motorn att ersätta tecken under indexering, vilket är kärnsteg för skiftlägesokänslig funktion.

#### Steg 1: Konfigurera `IndexSettings`
`IndexSettings` är konfigurationsobjektet som styr hur indexet lagrar och bearbetar text. Genom att sätta `useCharacterReplacements` till **true** slår du på automatisk gemener (eller någon anpassad mappning du tillhandahåller).

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### Konfigurera teckenersättningar
Mappa varje tecken till dess gemena motsvarighet (eller någon anpassad mappning du behöver).

#### Steg 2: Definiera och lägg till ersättningspar
Ersättningsordboken innehåller par som `'A' → 'a'`, `'É' → 'e'` osv. Att lägga till dessa par före indexering säkerställer att varje token normaliseras.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Indexera dokument
Nu när indexet är klart kan du **add documents to index** från vilken mapp som helst.

#### Steg 3: Lägg till dokument för indexering
GroupDocs.Search skannar målkatalogen, extraherar text från varje stödd filtyp, tillämpar ersättningsmappen och skriver tokenarna till indexlagringen.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Utför skiftlägeskänslig sökning (valfritt)

#### Steg 4: Utför skiftlägeskänsliga sökningar
`SearchOptions` konfigurerar frågebeteende, såsom att växla skiftlägeskänslighet, vilket möjliggör finjusterad kontroll över hur sökningar utförs.  
`SearchOptions.setUseCaseSensitiveSearch(true)` tvingar motorn att behandla stora och små tecken som olika under en specifik fråga, vilket åsidosätter standardbeteendet för skiftlägesokänslig sökning.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## Praktiska tillämpningar
1. **Marketing Campaigns** – Normalisera produktnamn så säljteam kan hitta resurser utan att oroa sig för skiftläge.  
2. **Customer Support** – Driv help‑desk sökrutor som returnerar rätt artikel oavsett om användaren skriver “login” eller “Login”.  
3. **E‑commerce Catalogs** – Säkerställ att kunder hittar produkter oavsett hur de skriver produktnamn, vilket förbättrar konverteringsgraden.

## Prestandaöverväganden
- **Organize Source Files** – En välordnad mappstruktur minskar den tid som spenderas på skanning under steget **add documents to index**.  
- **Monitor Memory** – Indexering av stora korpusar kan förbruka betydande RAM; att bearbeta filer i satser om 500 – 1 000 objekt håller heap‑användningen under kontroll.  
- **Asynchronous Indexing** – När det stöds, kör indexering på en bakgrundstråd för att hålla UI responsivt och undvika att blockera användaroperationer.

## Vanliga problem & felsökning
| Symptom | Trolig orsak | Åtgärd |
|---------|--------------|-----|
| Inga resultat returneras för ett känt begrepp | Teckenersättningar är inte aktiverade | Verifiera `settings.setUseCharacterReplacements(true)` och att ersättningsmappen innehåller de nödvändiga tecknen. |
| Out‑of‑memory‑fel under indexering | Indexering av för många stora filer samtidigt | Indexera i mindre satser eller öka JVM‑heap (`-Xmx4g`). |
| Sökning returnerar oväntat skiftlägeskänsliga resultat | `SearchOptions.setUseCaseSensitiveSearch(true)` var satt | Ta bort eller sätt till `false` för standardbeteendet skiftlägesokänslig sökning. |
| Indexladdningstid överstiger förväntningarna | Ineffektiv mappstruktur eller SSD används inte | Omorganisera filer, rensa bort oanvända dokument och lagra indexet på en snabb SSD. |
| Specialtecken ignoreras | Ersättningsmappen saknar Unicode‑poster | Lägg till mappningar för tecken som “é”, “ß”, “ø” till deras önskade motsvarigheter. |

## Vanliga frågor

**Q: Hur hanterar jag specialtecken (t.ex. “é”, “ß”) under indexering?**  
A: Inkludera dessa tecken i din ersättningskarta, mappa dem till deras ASCII‑motsvarigheter eller behåll dem oförändrade beroende på sökkrav.

**Q: Kan jag begränsa teckenersättning till ett specifikt språk?**  
A: Ja. Bygg en anpassad ersättningsarray som endast innehåller tecken för målspråket innan du lägger till den i ordboken.

**Q: Vad ska jag göra om indexet tar lång tid att ladda?**  
A: Optimera mappstrukturen, ta bort onödiga filer och lagra indexet på en högpresterande SSD. Inkrementell indexering minskar också laddningsbördan.

**Q: Är det möjligt att återställa teckenersättningar efter indexering?**  
A: Nej. Ersättningar är inbäddade i den indexerade datan; du måste bygga om indexet med nya inställningar för att ändra dem.

**Q: Var kan jag hitta mer detaljerad API‑dokumentation?**  
A: De officiella dokumenten och API‑referensen ger utförliga detaljer (se resurserna nedan).

## Resurser
- [Dokumentation](https://docs.groupdocs.com/search/java/)
- [API‑referens](https://reference.groupdocs.com/search/java)
- [Ladda ner GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub‑arkiv](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Gratis supportforum](https://forum.groupdocs.com/c/search/10)
- [Information om temporär licens](https://purchase.groupdocs.com/temporary-license/) 

---

**Senast uppdaterad:** 2026-07-31  
**Testad med:** GroupDocs.Search 25.4 for Java  
**Författare:** GroupDocs  

## Relaterade handledningar

- [Teckenersättning i GroupDocs.Search Java: En omfattande guide för att förbättra textsökning och indexering](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [Lägg till dokument i index: skiftlägeskänslig Java-sökning med GroupDocs](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [Hur man lägger till dokument i index med GroupDocs.Search för Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)