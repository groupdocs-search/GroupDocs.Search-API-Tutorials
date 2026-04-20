---
date: '2026-02-06'
description: Lär dig hur du lägger till dokument i indexet och aktiverar skiftlägeskänslig
  sökning i Java med GroupDocs.Search, vilket ökar noggrannheten i din applikation.
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 'Lägg till dokument i indexet: skiftlägeskänslig Java‑sökning med GroupDocs'
type: docs
url: /sv/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Lägg till dokument i index: Mästra skiftlägeskänsliga sökningar i Java med GroupDocs

Att hämta rätt information från en enorm samling dokument är ett grundläggande krav för moderna applikationer. I den här guiden lär du dig **hur du lägger till dokument i index** och utför **skiftlägeskänsliga sökningar** med GroupDocs.Search för Java. Oavsett om du bygger ett juridiskt dokumentarkiv, en e‑handelskatalog eller ett innehållshanteringssystem, ger precisa sökresultat nöjda användare och pålitliga data.

## Snabba svar
- **Vad är det första steget för att börja söka?** Lägg till dokument i ett index med `index.add(...)`.
- **Hur aktiverar man skiftlägeskänslig sökning?** Sätt `options.setUseCaseSensitiveSearch(true)`.
- **Kan jag söka i flera kataloger?** Ja – anropa `index.add()` för varje mapp du vill inkludera.
- **Vilken metod låter mig söka med objekt?** Använd `SearchQuery.createWordQuery(...)`.
- **Behöver jag en licens för testning?** En tillfällig licens finns tillgänglig för provändamål.

## Vad betyder “lägga till dokument i index”?
Att lägga till dokument i ett index innebär att mata dina källfiler (PDF‑filer, Word‑dokument, vanlig text osv.) till GroupDocs.Search så att den kan bygga en sökbar datastruktur. När de är indexerade kan motorn utföra snabba frågor, inklusive skiftlägeskänsliga.

## Varför aktivera skiftlägeskänslig sökning i Java?
- **Exakt termmatchning** – skilj mellan “Apple” (företaget) och “apple” (frukten).  
- **Regulatorisk efterlevnad** – vissa branscher kräver exakt frasmatchning.  
- **Förbättrad relevans** – användare förväntar sig ofta skiftlägespecifika resultat i tekniska eller juridiska sammanhang.

## Förutsättningar
- JDK (Java 17 eller senare rekommenderas)  
- Maven för beroendehantering  
- En IDE som IntelliJ IDEA eller Eclipse  
- Grundläggande kunskap om Java‑programmering  

## Konfigurera GroupDocs.Search för Java
Börja med att lägga till GroupDocs‑arkivet och beroendet i din `pom.xml`:

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

Alternativt kan du ladda ner den senaste versionen direkt från [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licensiering
För att komma igång med en provperiod, besök GroupDocs för att skaffa en tillfällig licens. Detta gör att du kan testa alla funktioner utan några begränsningar.

## Så lägger du till dokument i index – Textfrågesökning

### Steg 1: Skapa ett index och lägg till dina dokument
Skapa en mapp där indexfilerna ska lagras, och lägg sedan till källkatalogen som innehåller de dokument du vill söka i.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Proffstips:** Du kan anropa `index.add()` flera gånger för att **söka i flera kataloger** i ett enda index.

### Steg 2: Aktivera skiftlägeskänslig sökning
Konfigurera sökalternativen så att de respekterar bokstavsstorlek.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Steg 3: Utför en skiftlägeskänslig textfråga
Kör en fråga som skiljer “Advantages” från “advantages”.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Loopen skriver ut hela sökvägen för varje dokument som innehåller den exakt skiftlägesmatchade termen.

## Så lägger du till dokument i index – Objektfrågesökning

Objektfrågor ger dig mer flexibilitet, särskilt när du behöver kombinera flera kriterier.

### Steg 1: Initiera ett andra index (valfritt)
Om du föredrar att hålla objektbaserade sökningar separata, skapa en annan indexmapp.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Steg 2: Återanvänd det skiftlägeskänsliga alternativet
Samma `SearchOptions`‑instans fungerar för objektfrågor.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Steg 3: Bygg och kör en objektfråga
Skapa ett ordfrågeobjekt och skicka det till sökmotorn.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Att använda `createWordQuery` låter dig senare kombinera det med fras-, jokertecken- eller booleska frågor för mer komplexa scenarier.

## Praktiska tillämpningar
- **Juridisk dokumenthantering:** Hämta fall‑specifika lagar där versalisering är viktig.  
- **E‑handelsplattformar:** Skilj mellan produkt‑SKU:er som “PRO‑X” och “pro‑x”.  
- **Content Management Systems (CMS):** Säkerställ att författare hittar exakta rubriker eller taggar.

## Prestandaöverväganden
- **Håll indexet uppdaterat** – återindexera när nya filer läggs till eller befintliga ändras.  
- **Övervaka minnesanvändning** – stora korpusar drar nytta av inkrementell indexering och korrekt JVM‑heap‑storlek.  
- **Utnyttja Javas skräpsamlare** – frigör `Index`‑objekt när de inte längre behövs.

## Vanliga problem och lösningar
| Problem | Lösning |
|-------|----------|
| `useCaseSensitiveSearch` verkar ignoreras | Verifiera att du använder den senaste versionen av GroupDocs.Search och att indexet byggdes om efter att alternativet ändrats. |
| Inga resultat returnerades för en känd term | Säkerställ att termens skiftläge matchar exakt och att dokumentet har lagts till i indexet. |
| Sökning i många mappar blir långsam | Lägg till varje mapp individuellt med `index.add()` och överväg att dela upp indexet i shards för mycket stora datamängder. |

## Vanliga frågor

**Q:** Hur hanterar jag stora datamängder med GroupDocs.Search?  
**A:** Använd indexpartitionering, justera JVM‑minnesinställningar och komprimera indexet periodiskt för att hålla prestandan optimal.

**Q:** Kan jag söka i flera kataloger samtidigt?  
**A:** Ja – anropa `index.add()` för varje katalog du vill inkludera, och kör sedan en enda fråga mot det kombinerade indexet.

**Q:** Vilka vanliga fallgropar finns vid konfiguration av skiftlägeskänsliga sökningar?  
**A:** Att glömma att återindexera efter att ha aktiverat `useCaseSensitiveSearch`, eller att använda fel skiftläge i frågesträngen.

**Q:** Hur kan jag felsöka sökfel?  
**A:** Kontrollera loggfilerna som genereras av GroupDocs.Search för stackspår, och bekräfta att alla Maven‑beroenden är korrekt lösta.

**Q:** Är GroupDocs.Search lämplig för realtidstillämpningar?  
**A:** Med rätt indexeringsstrategier (inkrementella uppdateringar och cache i minnet) kan den leverera nästan realtidsresultat.

## Resurser
- **Dokumentation:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **API‑referens:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Nedladdning:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **GitHub‑arkiv:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Supportforum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Tillfällig licens:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Senast uppdaterad:** 2026-02-06  
**Testad med:** GroupDocs.Search 25.4  
**Författare:** GroupDocs