---
date: '2026-10-28'
description: Lär dig hur du söker i flera filtyper och bygger ett sökbart index för
  lösenordsskyddade dokument i Java med GroupDocs.Search. Steg‑för‑steg‑guide med
  kod, tips och prestandatrick.
keywords:
- search multiple file types
- build searchable index
- password protected document indexing java
- groupdocs.search java api
lastmod: '2026-10-28'
og_description: Lär dig hur du söker i flera filtyper och bygger ett sökbart index
  för lösenordsskyddade dokument i Java med GroupDocs.Search. Steg‑för‑steg‑guide
  med kod, tips och prestandatrick.
og_image_alt: Guide showing Java code to search multiple file types and index password‑protected
  documents with GroupDocs.Search
og_title: Hur man söker i flera filtyper och indexerar dokument i Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-28'
  description: Learn how to search multiple file types and build a searchable index
    for password‑protected documents in Java using GroupDocs.Search. Step‑by‑step
    guide with code, tips, and performance tricks.
  headline: How to search multiple file types and index docs in Java
  type: TechArticle
- questions:
  - answer: GroupDocs.Search supports 120+ formats including PDF, DOCX, XLSX, PPTX,
      and common image types. Install format plugins if required.
    question: How do I handle different file formats?
  - answer: The document is skipped and a warning is logged; verify your password
      dictionary or event handler.
    question: What happens if a password is wrong?
  - answer: Yes, but they must be downloaded to a local temporary folder first because
      the engine works with file‑system paths.
    question: Can I index files stored in the cloud?
  - answer: Adjust scoring with `IndexOptions`, add synonyms, and use advanced query
      syntax such as `field:term~` for fuzzy matching. `IndexOptions` is a configuration
      object that controls scoring and indexing behavior.
    question: How can I improve search relevance?
  - answer: Review the log output; common causes are missing passwords, corrupted
      files, or unsupported formats.
    question: What should I do if indexing fails for some files?
  type: FAQPage
tags:
- search multiple file types
- GroupDocs.Search
- Java indexing
- password‑protected docs
- document search
title: Hur man söker i flera filtyper och indexerar dokument i Java
type: docs
url: /sv/java/indexing/mastering-groupdocs-search-java-password-docs/
weight: 1
---

# Hur man söker i flera filtyper och indexerar dokument i Java

I moderna företag behöver du ofta **söka i flera filtyper** samtidigt som du håller konfidentiella filer låsta bakom lösenord. Denna handledning visar hur du bygger ett sökbart index för lösenordsskyddade dokument i Java med GroupDocs.Search. Du kommer att se hur du konfigurerar ett lösenordslexikon, hanterar lösenord‑krävande händelser och optimerar prestanda för stora batcher — allt utan att skriva egen avkrypteringskod.

## Snabba svar
- **Vad täcker den här handledningen?** Indexering av lösenordsskyddade dokument med ett lösenordslexikon och en händelselyssnare.  
- **Vilket bibliotek krävs?** GroupDocs.Search för Java (senaste versionen).  
- **Behöver jag en licens?** En tillfällig gratis provlicens finns tillgänglig för utvärdering.  
- **Kan jag indexera andra filtyper?** Ja, GroupDocs.Search stödjer över 120 format inklusive PDF, DOCX, XLSX, PPTX och bilder.  
- **Vilken Java‑version behövs?** JDK 8 eller senare.  

## Vad är “create document index java”?
`create document index java` avser processen att konstruera en sökbar datastruktur som mappar termer till placeringarna för Java‑hanterade filer. Med GroupDocs.Search extraherar motorn automatiskt text från stödda format — inklusive krypterade PDF‑filer, Office‑dokument och bilder — så att du kan utföra fulltextsökningar utan att skriva någon avkrypteringskod själv. Detta tillvägagångssätt förenklar sökimplementeringen samtidigt som dokumentens säkerhet bevaras.

## Varför använda GroupDocs.Search för lösenordsskyddade filer?
GroupDocs.Search erbjuder en noll‑touch upplåsningsmekanism som använder lösenord från ett lexikon eller en händelsehanterare, vilket låter dig indexera krypterade filer i ett enda pass. Den bearbetar upp till 2 miljoner dokument per timme på en standard 8‑kärnig server, stödjer över 120 filtyper och erbjuder ett rikt frågespråk med Boolean‑, wildcard‑ och fuzzy‑operatorer — allt nödvändigt för att bygga ett sökbart index som omfattar mångsidigt innehåll.

## Förutsättningar
- Java Development Kit (JDK) 8+ installerat och tillagt i din `PATH`.  
- En IDE som IntelliJ IDEA eller Eclipse.  
- Maven för beroendehantering.  
- GroupDocs.Search för Java – lägg till biblioteket via Maven (se installationsavsnittet).  

## Installera GroupDocs.Search för Java

### Använda Maven
Lägg till repository och beroende i din `pom.xml`-fil:

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
Alternativt kan du ladda ner den senaste versionen direkt från [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

För att komma igång med en provlicens, besök [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) och följ instruktionerna för att få din gratis provperiod.

## Hur man indexerar dokument med ett lösenordslexikon

Du kan **bygga ett sökbart index** genom att tillhandahålla ett lexikon som mappar filsökvägar till deras lösenord. Motorn kommer automatiskt att hämta rätt lösenord under indexeringen.

### Översikt
Spara dokumentlösenord i en enkel nyckel‑värde‑karta så att indexeringsmotorn kan låsa upp filer vid behov.

### Steg 1: definiera indexet och dokumentmappen
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordDictionary";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Steg 2: skapa ett index
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Steg 3: lägg till dokumentlösenord
```java
// Add passwords for specific files using their absolute paths
String path1 = new File(documentsFolder + "/English.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path1, "123456");

String path2 = new File(documentsFolder + "/SampleDocument.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path2, "123456");
```

### Steg 4: indexera dokument
```java
// Automatically retrieve passwords from the dictionary during indexing
index.add(documentsFolder);
```

### Steg 5: sök i indexet
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

**Tips:** För produktionsscenarier, ladda lösenord från ett säkert valv (t.ex. Azure Key Vault eller AWS Secrets Manager) istället för att hårdkoda dem.

#### Felsökning
- Verifiera att varje lösenord matchar filens faktiska skyddslösenord.  
- Dubbelkolla filsökvägar; en felaktig sökväg utlöser `FileNotFoundException`.

## Hur man indexerar dokument med en händelselyssnare för lösenordskrav?

Du kan tillhandahålla lösenord endast när motorn utlöser ett lösenord‑krävande evenemang, vilket håller kredentialer utanför minnet och möjliggör dynamisk lösenordslösning.

När indexeringsmotorn stöter på en krypterad fil, utlöser den en återuppringning där du kan slå upp lösenordet från ett säkert lagringsutrymme eller beräkna det i farten. Denna metod minskar attackytan jämfört med att lagra alla lösenord i ett lexikon.

### Översikt
Tillhandahåll lösenord i farten via en händelserückuppringning, så att ditt kredentiallager hålls isolerat.

### Steg 1: definiera indexet och dokumentmappen
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordEvent";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Steg 2: skapa ett index
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Steg 3: prenumerera på lösenord‑krävande händelse
```java
index.getEvents().PasswordRequired.add(new EventHandler<PasswordRequiredEventArgs>() {
    @Override
    public void invoke(Object sender, PasswordRequiredEventArgs args) {
        // Provide password for DOCX files when needed
        if (args.getDocumentFullPath().endsWith(".docx")) {
            args.setPassword("123456");
        }
    }
});
```

### Steg 4: indexera dokument
```java
// The event handler will supply passwords as required during indexing
index.add(documentsFolder);
```

### Steg 5: sök i indexet
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

#### Felsökning
- Säkerställ att händelsehanteraren täcker alla filändelser du behöver indexera.  
- Testa först med några exempel-filer för att bekräfta att lösenordet tillämpas.

## Praktiska tillämpningar

1. **Enterprise document management** – automatisera indexering av konfidentiella kontrakt, HR‑filer och finansiella rapporter samtidigt som de hålls krypterade i vila.  
2. **Legal archives** – hämta snabbt ärendehandlingar utan att exponera känsligt innehåll.  
3. **Healthcare records** – indexera patient‑PDF‑filer och Word‑dokument samtidigt som du följer HIPAA‑kraven.

## Prestandaöverväganden

- **Minnesallokering** – allokera tillräckligt heap‑minne (`-Xmx2g` eller högre) för stora batcher.  
- **Parallell indexering** – använd `index.addAsync(...)` eller kör flera indexeringstrådar för att uppnå upp till **2 miljoner dokument per timme** på en 8‑kärnig maskin. `index.addAsync(...)` är en metod som köar dokument för asynkron indexering.  
- **Indexunderhåll** – anropa periodiskt `index.optimize()` för att komprimera indexet och förbättra frågehastigheten.

## Vanliga problem och lösningar

- **Fel lösenord** – dokumentet hoppas över och en varning loggas. Dubbelkolla din lösenordskälla.  
- **Ej stödd format** – installera nödvändiga format‑plugins eller konvertera filer till ett stödt format innan indexering.  
- **Stora filer** – öka heap‑storleken och överväg att indexera dem i mindre batcher för att undvika `OutOfMemoryError`.

## Vanliga frågor

**Q: Hur hanterar jag olika filformat?**  
A: GroupDocs.Search stödjer över 120 format inklusive PDF, DOCX, XLSX, PPTX och vanliga bildtyper. Installera format‑plugins om det behövs.

**Q: Vad händer om ett lösenord är fel?**  
A: Dokumentet hoppas över och en varning loggas; verifiera ditt lösenordslexikon eller händelsehanterare.

**Q: Kan jag indexera filer lagrade i molnet?**  
A: Ja, men de måste först laddas ner till en lokal temporär mapp eftersom motorn arbetar med filsystemssökvägar.

**Q: Hur kan jag förbättra sökrelevansen?**  
A: Justera poängsättningen med `IndexOptions`, lägg till synonymer och använd avancerad frågesyntax såsom `field:term~` för fuzzy‑matchning. `IndexOptions` är ett konfigurationsobjekt som styr poängsättning och indexeringsbeteende.

**Q: Vad ska jag göra om indexeringen misslyckas för vissa filer?**  
A: Granska loggutdata; vanliga orsaker är saknade lösenord, korrupta filer eller ej stödda format.

## Resurser
- [GroupDocs.Search-dokumentation](https://docs.groupdocs.com/search/java/)
- [API‑referens](https://reference.groupdocs.com/search/java)
- [Ladda ner GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub‑arkiv](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Gratis supportforum](https://forum.groupdocs.com/c/search/10)
- [Information om tillfällig licens](https://purchase.groupdocs.com/temporary-license/)

Genom att följa den här guiden vet du nu **hur man söker i flera filtyper** och **indexerar lösenordsskyddade dokument** i Java, vilket förbättrar både säkerhet och upptäckbarhet i dina applikationer.

---

**Senast uppdaterad:** 2026-10-28  
**Testad med:** GroupDocs.Search 25.4 för Java  
**Författare:** GroupDocs

## Relaterade handledningar

- [Hur man indexerar lösenordsskyddade dokument i Java med GroupDocs.Search](/search/java/indexing/mastering-groupdocs-search-java-password-docs/)
- [Förbättra frågeprestanda med GroupDocs.Search Java: Optimera index & sökning](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)