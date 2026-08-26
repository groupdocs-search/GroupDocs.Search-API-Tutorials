---
date: '2026-08-26'
description: Ismerje meg, hogyan a boolean operators Java lehetővé teszi, hogy gyors
  search index-et építsen, content search Java-t hajtson végre, és faceted queries-t
  futtasson a GroupDocs.Search segítségével.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: Ismerje meg, hogyan a boolean operators Java lehetővé teszi, hogy
  gyors search index-et építsen, content search Java-t hajtson végre, és faceted queries-t
  hajtsa végre a GroupDocs.Search segítségével.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – build search index és faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – létrehozni search index & faceted search
type: docs
url: /hu/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean operátorok Java – keresési index létrehozása és facettált keresés

Egy erőteljes **search experience** megvalósítása Java-ban ijesztőnek tűnhet, különösen, ha **create a search index Java**-t kell létrehozni, amely támogatja a **boolean operators Java**-t a facettált és összetett lekérdezésekhez. Ebben az oktatóanyagban végigvezetjük a **GroupDocs.Search for Java** beállítását, egy index felépítését, dokumentumok hozzáadását, valamint egyszerű facettált keresések és kifinomult többkritériumos lekérdezések megalkotását, amelyek Boolean logikát használnak. A végére megérted, hogyan lehet kihasználni a **content search Java**, **filename search Java**, és még a **update index Java** műveleteket is az adatok frissességének biztosításához.

## Gyors válaszok
- **Mi az a facettált keresés?** Egy mód a találatok szűrésére előre meghatározott kategóriák, például fájltípus vagy dátum szerint.  
- **Hogyan hozhatok létre egy search index Java‑t?** Inicializálj egy `Index` objektumot, amely egy mappára mutat, és adj hozzá dokumentumokat.  
- **Kombinálhatok több feltételt Boolean operátorokkal?** Igen—használj objektumalapú lekérdezéseket vagy Boolean operátorokat egy szöveges lekérdezésben.  
- **Szükségem van licencre?** Egy ingyenes próba működik fejlesztéshez; egy kereskedelmi licenc eltávolítja a korlátokat.  
- **Melyik IDE a legjobb?** Bármely Java IDE (IntelliJ IDEA, Eclipse, NetBeans) megfelelő.

## Mi az a “create search index java”?

A search index Java létrehozása egy lemez‑alapú struktúra felépítését jelenti, amely tárolja a dokumentum szövegét és metaadatait, lehetővé téve a megfelelő dokumentumok azonnali lekérdezésen keresztüli visszakeresését. Az index a kifejezéseket dokumentumazonosítókhoz rendeli, gyors keresést támogat, és fokozatosan frissíthető a fájlok változása esetén, ezáltal biztosítva az erőteljes keresési funkciók alapját.

## Miért használjuk a GroupDocs.Search‑t facettált és összetett lekérdezésekhez?

A GroupDocs.Search for Java beépített facettálást, Boolean lekérdezés támogatást és nagy teljesítményű indexelést biztosít, amely akár 10 millió dokumentumot is képes kezelni, miközben a lekérdezési késleltetés tipikus szerver hardveren 200 ms alatt marad. Kész mezőszűrőket, gazdag lekérdezési nyelvet és tisztán Java kompatibilitást kínál, így ideális vállalati szintű keresési forgatókönyvekhez.

## Előfeltételek

- **JDK 8 vagy újabb** telepítve és konfigurálva az IDE-ben.  
- **Maven** (vagy Gradle) a függőségkezeléshez.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Alapvető ismeretek a Java OOP koncepciókról és a Maven projekt struktúrájáról.

## A GroupDocs.Search for Java beállítása

### Maven beállítás
Adja hozzá a tárolót és a függőséget a `pom.xml` fájlhoz:

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

### Közvetlen letöltés
Alternatívaként töltse le a legújabb JAR-t a hivatalos kiadási oldalról:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Licenc beszerzése
A teljes funkcionalitás feloldásához:

1. **Free trial** – tökéletes fejlesztéshez és teszteléshez.  
2. **Temporary evaluation license** – meghosszabbítja a próbaidő korlátait.  
3. **Commercial license** – eltávolítja az összes korlátozást a termelésben való használathoz.

### Alap inicializálás és beállítás
Az `Index` osztály a fő komponens, amely egy lemezen tárolt kereshető indexet képvisel. Az alábbi kódrészlet megmutatja, hogyan lehet **create a search index Java**-t létrehozni az `Index` osztály példányosításával:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

Az index készen áll, így továbbléphetünk a valóságos facettált és összetett lekérdezésekre.

## Hogyan használjuk a boolean operators java – Egyszerű facettált keresés

Töltse be az indexet, adjon hozzá dokumentumokat, és indítson mező lekérdezést; a kétlépéses minta lehetővé teszi a facett számok és a szűrt eredmények egyetlen hívásban történő lekérését. Ez a megközelítés intuitív módot biztosít a felhasználóknak az eredmények szűkítésére kategóriák, például fájltípus, szerző vagy egyedi metaadatok szerint.

### 1. lépés: Index létrehozása
Először mutassa a `Index`-et egy mappára, ahol az index fájlok tárolódnak.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### 2. lépés: Dokumentumok hozzáadása az indexhez
Adja meg a GroupDocs.Search-nek, hol találhatók a forrásdokumentumok. Minden támogatott fájltípus (PDF, DOCX, TXT stb.) automatikusan indexelésre kerül.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### 3. lépés: Keresés a content mezőben szöveges lekérdezéssel
Egy gyors szöveges lekérdezés a `content` mező szerint szűr. A `content: Pellentesque` szintaxis csak azokat a dokumentumokat adja vissza, amelyek a szövegtestben tartalmazzák a *Pellentesque* szót.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### 4. lépés: Keresés objektum lekérdezéssel
Az objektumalapú lekérdezések finomhangolt vezérlést biztosítanak. Itt egy szó lekérdezést építünk, mező lekérdezésbe csomagoljuk, és végrehajtjuk.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Hogyan használjuk a boolean operators java – Összetett lekérdezés keresés

Összetett lekérdezés végrehajtásához kombináljon több mezőfeltételt AND/OR/NOT operátorokkal, és opcionálisan vegyen fel kifejezés kereséseket. Minden feltételt mező lekérdezésekkel adhat meg, beágyazhatja őket Boolean operátorokkal, és a relevanciát boost-olással szabályozhatja, így csak a legrelevánsabb dokumentumokat kapja, amelyek minden szükséges kritériumnak megfelelnek.

### 1. lépés: Index létrehozása összetett lekérdezésekhez
Használja újra ugyanazt a mappaszerkezetet; az indexet megoszthatja egyszerű és összetett forgatókönyvek között.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### 2. lépés: Keresés szöveges lekérdezéssel
A következő lekérdezés olyan fájlokat keres, amelyek neve *lorem* **és** *ipsum* **vagy** a tartalom tartalmazza a két pontos kifejezést.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### 3. lépés: Keresés objektum lekérdezéssel
Az objektumalapú felépítés tükrözi a szöveges lekérdezést, de típusbiztonságot és IDE támogatást nyújt.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## A facettált és összetett keresések gyakorlati alkalmazásai

| Szenárió | Hogyan segít a facettálás | Példa lekérdezés |
|----------|--------------------------|-----------------|
| **E‑commerce catalog** | Szűrés kategória, ár, márka szerint | `category: Electronics AND price:[100 TO 500]` |
| **Legal document repository** | Szűrés ügyiratszám, joghatóság szerint | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Research archives** | Kombinálja a szerzőt, kiadási évet, kulcsszavakat | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Enterprise intranet** | Keresés fájltípus és részleg szerint | `filetype: pdf AND department: HR` |

## Gyakori buktatók és hibaelhárítás

A `SearchResult` objektum tartalmazza a lekérdezésnek megfelelő dokumentumokat, és hozzáférést biztosít a relevancia pontszámokhoz és a kiemelt részletekhez.  
A `CommonFieldNames` osztály definiálja a szabványos mezőneveket, például a `Content` és `FileName`-t, amelyeket az API mindenhol használ.

- **Üres eredmények** – Ellenőrizze, hogy a dokumentumok sikeresen hozzá lettek-e adva (`index.getDocumentCount()` segíthet).  
- **Elavult index** – Fájlok hozzáadása vagy eltávolítása után hívja meg a `index.update()`-t a **update index java** frissítéséhez, és tartsa az indexet szinkronban.  
- **Helytelen mezőnevek** – Használja a `CommonFieldNames` konstansokat (`Content`, `FileName`, stb.) a helyesírási hibák elkerülése érdekében.  
- **Teljesítménybeli szűk keresztmetszetek** – Nagy gyűjtemények esetén fontolja meg a `index.setCacheSize()` engedélyezését vagy egy dedikált SSD használatát az index mappához.  
- **Hiányzó kiemelések** – A **highlight search results java** funkcióhoz szerezze be a megtalált részleteket a `SearchResult.getFragments()` segítségével (itt nem látható, de elérhető az API-ban).

## Gyakran feltett kérdések

**K: Használhatom a GroupDocs.Search‑t Spring Boot‑tal?**  
A: Természetesen. Adja hozzá a Maven függőséget, konfigurálja az indexet Spring bean‑ként, és injektálja bárhol, ahol keresési képességre van szükség.

**K: Támogatja a könyvtár az egyedi metaadatmezőket?**  
A: Igen – a indexelés során hozzáadhat felhasználó által definiált mezőket, majd facettálhat rajtuk.

**K: Mekkora lehet az index mérete?**  
A: A lemez‑alapú index akár 10 millió dokumentumot is kezel; csak biztosítsa a megfelelő tárolókapacitást és figyelje a gyorsítótár beállításait.

**K: Van mód a találatok relevancia szerinti rangsorolására?**  
A: A GroupDocs.Search automatikusan pontszámot ad a találatoknak; a pontszámot a `SearchResult.getDocument(i).getScore()` segítségével kérheti le.

**K: Mi történik, ha titkosított PDF‑eket indexelek?**  
A: Adja meg a jelszót a dokumentum hozzáadása során: `index.add(filePath, password)`.

## Következtetés

Eddig már kényelmesen kellene tudnia **create a search index Java**-t használni a GroupDocs.Search‑szal, dokumentumok hozzáadását, valamint egyszerű facettált lekérdezések és kifinomult Boolean keresések megalkotását a **boolean operators java** segítségével. Ezek a képességek lehetővé teszik, hogy gyors, pontos és felhasználóbarát keresési élményeket nyújtson széles körű alkalmazásokban – az e‑commerce platformoktól a vállalati tudásbázisokig.

Készen áll a következő lépésre? Fedezze fel a **GroupDocs.Search** fejlett funkcióit, mint a **highlighting**, **suggestions**, és a **real‑time indexing**, hogy tovább növelje alkalmazása keresési teljesítményét.

---

**Legutóbb frissítve:** 2026-08-26  
**Tesztelve:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [Wildcard keresés Java a GroupDocs.Search‑szal – Haladó funkciók](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Hogyan frissítsük az Index Java‑t a GroupDocs.Search‑szal – Átfogó útmutató](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Hogyan valósítsuk meg a java teljes szöveges keresést: index könyvtár létrehozása a GroupDocs.Search‑szal](/search/java/indexing/groupdocs-search-java-create-index/)