---
date: '2026-02-21'
description: Lär dig hur du lägger till dokument i indexet och ökar sökprestandan
  med chunk‑baserad sökning i Java med GroupDocs.Search, samt optimerar Java‑sökindexets
  minnesanvändning för stora dokumentuppsättningar.
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

I moderna applikationer som behöver **lägga till dokument i index** snabbt och sedan utföra snabba, chunk‑baserade frågor, vill du ha en lösning som skalar utan att spränga minnet. Denna handledning guidar dig genom att konfigurera GroupDocs.Search för Java, lägga till flera dokumentmappar och konfigurera motorn för att **öka sökprestanda** samtidigt som **java search index memory**‑användning hålls under kontroll. Oavsett om du indexerar juridiska kontrakt, supportärenden eller forskningsartiklar, kommer stegen nedan att ge dig en produktionsklar implementation.

## Snabba svar
- **Vad är det första steget?** Skapa en sökindexmapp.  
- **Hur inkluderar jag många filer?** Använd `index.add()` för varje dokumentmapp.  
- **Vilket alternativ aktiverar chunk‑sökning?** `options.setChunkSearch(true)`.  
- **Kan jag fortsätta söka efter den första chunken?** Ja, anropa `index.searchNext()` med token.  
- **Behöver jag en licens?** En gratis provperiod eller tillfällig licens fungerar för utveckling; en full licens krävs för produktion.  

## Vad du kommer att lära dig
- Hur man skapar ett sökindex i en angiven mapp.  
- Steg för att **lägga till dokument i index** från flera platser.  
- Konfigurera sökalternativ för att aktivera chunk‑baserad sökning.  
- Utföra initiala och efterföljande chunk‑baserade sökningar.  
- Verkliga scenarier där chunk‑baserad dokumentsökning glänser.  

## Förutsättningar
För att följa denna guide, se till att du har:

- **Nödvändiga bibliotek**: GroupDocs.Search för Java 25.4 eller senare.  
- **Miljöinställning**: Ett kompatibelt Java Development Kit (JDK) installerat.  
- **Kunskapsförutsättningar**: Grundläggande Java‑programmering och Maven‑kunskap.  

## Installera GroupDocs.Search för Java
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
- **Köp** – full licens för produktionsanvändning.  

### Grundläggande initiering och konfiguration
Skapa ett index i den mapp där du vill att de sökbara data ska lagras:

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
Nu när indexet finns, är nästa logiska steg att **lägga till dokument i index** från de platser där dina filer är lagrade.

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
Chunk‑baserad sökning delar upp massiva dokumentsamlingar i hanterbara delar, minskar minnesbelastning och snabbar upp svarstider. Det är särskilt fördelaktigt när:

1. **Juridiska team** behöver hitta specifika klausuler i tusentals kontrakt.  
2. **Kundsupportportaler** måste omedelbart visa relevanta kunskapsbasartiklar.  
3. **Forskare** sållar igenom omfattande dataset utan att ladda hela filer i minnet.  

## Hur detta tillvägagångssätt **ökar sökprestanda**
Genom att söka i mindre chunkar istället för hela filer kan motorn:

- Hoppa över irrelevanta sektioner tidigt, vilket minskar CPU‑cykler.  
- Hålla endast den aktiva chunken i minnet, vilket direkt minskar **java search index memory**‑förbrukning.  
- Parallellisera chunk‑bearbetning på flerkärniga maskiner för snabbare resultat.  

## Hantera **java search index memory**
Även om chunk‑baserad sökning redan minskar minnesavtrycket, kan du ytterligare finjustera JVM:n:

- Tilldela tillräckligt heap (`-Xmx2g` eller högre) baserat på indexstorlek.  
- Använd `index.optimize()` efter massiva tillägg för att komprimera indexstrukturen.  
- Övervaka GC‑pauser med verktyg som VisualVM för att undvika latensspikar.  

## Prestandaöverväganden
- **Minneshantering** – Tilldela tillräckligt heap‑utrymme (`-Xmx`) för stora index.  
- **Resursövervakning** – Håll ett öga på CPU‑användning under indexering och sökoperationer.  
- **Indexunderhåll** – Återuppbygg eller rensa indexet periodiskt för att ta bort föråldrade data.  

## Vanliga fallgropar & felsökning
| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| `OutOfMemoryError` under indexering | Heap‑storlek för låg | Öka JVM‑heap (`-Xmx2g` eller högre) |
| Inga resultat returneras | Chunk‑token bearbetas inte | Säkerställ att `while`‑loopen körs tills `getNextChunkSearchToken()` är `null` |
| Långsam sökprestanda | Indexet är inte optimerat | Kör `index.optimize()` efter massiva tillägg |

## Vanliga frågor

**Q: Vad är chunk‑baserad sökning?**  
A: Chunk‑baserad sökning delar upp datasetet i mindre delar, vilket möjliggör effektiva frågor över stora datamängder utan att ladda hela dokument i minnet.

**Q: Hur uppdaterar jag mitt index med nya filer?**  
A: Anropa helt enkelt `index.add()` med sökvägen till de nya dokumenten; indexet kommer att inkludera dem automatiskt.

**Q: Kan GroupDocs.Search hantera olika filformat?**  
A: Ja, det stödjer PDF‑filer, DOCX, XLSX, PPTX och många andra vanliga format.

**Q: Vilka är typiska prestandaflaskhalsar?**  
A: Minnesbegränsningar och ooptimerade index är de vanligaste; tilldela tillräckligt heap och optimera indexet regelbundet.

**Q: Var kan jag hitta mer detaljerad dokumentation?**  
A: Besök den officiella [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) för djupgående guider och API‑referenser.

**Q: Fungerar chunk‑baserad sökning med krypterade PDF‑filer?**  
A: Ja, så länge du anger lösenordet via den lämpliga API‑överladdningen.

**Q: Hur kan jag övervaka indexeringsförloppet?**  
A: Använd `Index.add()`‑överladdningen som returnerar ett `Progress`‑objekt eller anslut till loggnings‑callback‑funktioner.

## Resurser
- **Dokumentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API‑referens**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Nedladdning**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Gratis support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Tillfällig licens**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Senast uppdaterad:** 2026-02-21  
**Testad med:** GroupDocs.Search 25.4 för Java  
**Författare:** GroupDocs