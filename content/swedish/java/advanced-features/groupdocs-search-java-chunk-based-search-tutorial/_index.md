---
date: '2025-12-19'
description: Lär dig hur du lägger till dokument i indexet och aktiverar chunk‑baserad
  sökning i Java med GroupDocs.Search, vilket ökar prestandan för stora dokumentuppsättningar.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Lägg till dokument i index med chunk‑baserad sökning i Java
type: docs
url: /sv/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Lägg till dokument i index med chunk‑baserad sökning i Java

I dagens datadrivna värld är det avgörande att snabbt kunna **add documents to index** och sedan utföra chunk‑baserade sökningar för alla applikationer som hanterar stora samlingar av filer. Oavsett om du arbetar med juridiska kontrakt, kundsupportarkiv eller enorma forskningsbibliotek visar den här handledningen exakt hur du konfigurerar GroupDocs.Search för Java så att du kan indexera dokument effektivt och hämta relevant information i små bitar.

## Vad du kommer att lära dig
- Hur man skapar ett sökindex i en angiven mapp.  
- Steg för att **add documents to index** från flera platser.  
- Konfigurera sökalternativ för att möjliggöra chunk‑baserad sökning.  
- Utföra initiala och efterföljande chunk‑baserade sökningar.  
- Verkliga scenarier där chunk‑baserad dokumentsökning briljerar.

## Snabba svar
- **Vad är första steget?** Skapa en sökindexmapp.  
- **Hur inkluderar jag många filer?** Använd `index.add()` för varje dokumentmapp.  
- **Vilket alternativ möjliggör chunk‑sökning?** `options.setChunkSearch(true)`.  
- **Kan jag fortsätta söka efter den första chunken?** Ja, anropa `index.searchNext()` med token.  
- **Behöver jag en licens?** En gratis provperiod eller tillfällig licens fungerar för utveckling; en full licens krävs för produktion.

## Förutsättningar
För att följa den här guiden, se till att du har:

- **Nödvändiga bibliotek**: GroupDocs.Search för Java 25.4 eller senare.  
- **Miljöuppsättning**: En kompatibel Java Development Kit (JDK) installerad.  
- **Kunskapsförutsättningar**: Grundläggande Java‑programmering och Maven‑kunskap.

## Så här installerar du GroupDocs.Search för Java
För att börja, integrera GroupDocs.Search i ditt projekt med Maven:

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

Alternativt, ladda ner den senaste versionen från [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licensinnehav
För att prova GroupDocs.Search:

- **Gratis provperiod** – testa kärnfunktioner utan åtagande.  
- **Tillfällig licens** – utökad åtkomst för utveckling.  
- **Köp** – full licens för produktionsbruk.

### Grundläggande initiering och konfiguration
Skapa ett index i den mapp där du vill att den sökbara datan ska lagras:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## Hur man lägger till dokument i index
Nu när indexet finns är nästa logiska steg att **add documents to index** från de platser där dina filer lagras.

### 1. Skapa ett index
**Översikt**: Skapa en katalog för sökindexet.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Lägga till dokument i index
**Översikt**: Hämta filer från flera källmappar.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Konfigurera sökalternativ för chunk‑sökning
Aktivera chunk‑baserad sökning genom att justera options‑objektet.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Utföra initial chunk‑baserad sökning
Kör den första frågan med de chunk‑aktiverade alternativen.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Fortsätta chunk‑baserad sökning
Iterera genom de återstående chunkarna tills sökningen är klar.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Varför använda chunk‑baserad sökning?
Chunk‑baserad sökning delar upp enorma dokumentsamlingar i hanterbara delar, minskar minnesbelastning och snabbar upp svarstider. Det är särskilt fördelaktigt när:

1. **Juridiska team** behöver hitta specifika klausuler i tusentals kontrakt.  
2. **Kundsupportportaler** måste omedelbart visa relevanta kunskapsbasartiklar.  
3. **Forskare** sållar igenom omfattande dataset utan att ladda hela filer i minnet.

## Prestandaöverväganden
- **Minneshantering** – Tilldela tillräckligt heaputrymme (`-Xmx`) för stora index.  
- **Resursövervakning** – Håll koll på CPU‑användning under indexering och sökoperationer.  
- **Indexunderhåll** – Bygg om eller rensa indexet periodiskt för att ta bort föråldrad data.

## Vanliga fallgropar & felsökning
| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| `OutOfMemoryError` under indexering | Heap‑storlek för låg | Öka JVM‑heap (`-Xmx2g` eller högre) |
| Inga resultat returnerade | Chunk‑token bearbetas inte | Säkerställ att `while`‑loopen körs tills `getNextChunkSearchToken()` är `null` |
| Långsam sökprestanda | Indexet är inte optimerat | Kör `index.optimize()` efter massiva tillägg |

## Vanliga frågor

**Q: Vad är chunk‑baserad sökning?**  
A: Chunk‑baserad sökning delar upp datasetet i mindre delar, vilket möjliggör effektiva frågor över stora datamängder utan att ladda hela dokument i minnet.

**Q: Hur uppdaterar jag mitt index med nya filer?**  
A: Anropa helt enkelt `index.add()` med sökvägen till de nya dokumenten; indexet kommer att inkludera dem automatiskt.

**Q: Kan GroupDocs.Search hantera olika filformat?**  
A: Ja, det stöder PDF‑filer, DOCX, XLSX, PPTX och många andra vanliga format.

**Q: Vilka är typiska prestandaflaskhalsar?**  
A: Minnesbegränsningar och ooptimerade index är de vanligaste; tilldela tillräckligt heap och optimera indexet regelbundet.

**Q: Var kan jag hitta mer detaljerad dokumentation?**  
A: Besök den officiella [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) för djupgående guider och API‑referenser.

## Resurser
- **Dokumentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API‑referens**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Nedladdning**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Gratis support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Tillfällig licens**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

**Senast uppdaterad:** 2025-12-19  
**Testat med:** GroupDocs.Search 25.4 for Java  
**Författare:** GroupDocs