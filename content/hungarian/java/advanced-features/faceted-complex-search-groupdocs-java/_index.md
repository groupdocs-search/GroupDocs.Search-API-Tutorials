---
date: '2025-12-16'
description: Tanulja meg, hogyan hozhat létre keresőindexet Java-ban, és valósítsa
  meg a facettált és összetett kereséseket a GroupDocs.Search használatával, növelve
  a keresési teljesítményt és a felhasználói élményt.
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: Keresési index létrehozása Java-ban – Faszetált és összetett keresések
type: docs
url: /hu/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Keresési index létrehozása Java‑ban – Facettált és összetett keresések

Egy erőteljes **search experience** megvalósítása Java‑ban ijesztőnek tűnhet, különösen, ha **create search index Java** projekteket kell létrehozni, amelyek nagy dokumentumgyűjteményeket kezelnek. Szerencsére a **GroupDocs.Search for Java** gazdag API‑t biztosít, amely lehetővé teszi facettált és összetett lekérdezések felépítését néhány kódsorral. Ebben az útmutatóban megtudja, hogyan állítsa be a könyvtárat, **create a search index Java**, dokumentumok hozzáadását, valamint egyszerű facettált keresések és kifinomult többkritériumos lekérdezések futtatását.

## Gyors válaszok
- **Mi az a facettált keresés?** A módja annak, hogy az eredményeket előre meghatározott kategóriák (pl. fájltípus, dátum) szerint szűrjük.  
- **Hogyan hozhatok létre egy search index Java‑t?** Inicializáljon egy `Index` objektumot, amely egy mappára mutat, és adjon hozzá dokumentumokat.  
- **Kombinálhatok több kritériumot?** Igen—használjon objektumalapú lekérdezéseket vagy Boolean operátorokat egy szöveges lekérdezésben.  
- **Szükségem van licencre?** Egy ingyenes próba a fejlesztéshez megfelelő; egy kereskedelmi licenc eltávolítja a korlátozásokat.  
- **Melyik IDE a legjobb?** Bármely Java IDE (IntelliJ IDEA, Eclipse, NetBeans) megfelelő.

## Mi az a “create search index java”?
A search index létrehozása Java‑ban azt jelenti, hogy egy kereshető adatstruktúrát építünk, amely tárolja a dokumentum metaadatait és tartalmát, lehetővé téve a gyors visszakeresést a felhasználói lekérdezések alapján. A GroupDocs.Search esetén az index a lemezen tárolódik, fokozatosan frissíthető, és támogatja a fejlett funkciókat, mint a facettálás és az összetett Boolean logika.

## Miért használjuk a GroupDocs.Search‑t facettált és összetett lekérdezésekhez?
- **Out‑of‑the‑box faceting** – Beépített facettálás – szűrés mezők szerint, például fájlnév, méret vagy egyéni metaadatok.  
- **Rich query language** – Gazdag lekérdezési nyelv – szöveg, kifejezés és mező lekérdezések keverése AND/OR/NOT operátorokkal.  
- **Scalable performance** – Skálázható teljesítmény – milliók dokumentumait indexeli, miközben alacsony keresési késleltetést tart.  
- **Pure Java** – Tiszta Java – nincs natív függőség, bármely JDK 8+ környezetben működik.

## Előkövetelmények

Mielőtt belemerülnénk, győződjön meg róla, hogy a következőkkel rendelkezik:

- **JDK 8 or newer** – JDK 8 vagy újabb telepítve és konfigurálva az IDE‑ben.  
- **Maven** (or Gradle) – Maven (vagy Gradle) a függőségkezeléshez.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Basic familiarity with Java OOP concepts and Maven project structure – Alapvető ismeretek a Java OOP koncepciókról és a Maven projekt struktúráról.

## A GroupDocs.Search beállítása Java‑hoz

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
Alternatívaként töltse le a legújabb JAR‑t a hivatalos kiadási oldalról:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Licenc beszerzése
A teljes funkcionalitás feloldásához:

1. **Free trial** – Ingyenes próba – tökéletes fejlesztéshez és teszteléshez.  
2. **Temporary evaluation license** – Ideiglenes értékelő licenc – meghosszabbítja a próba korlátait.  
3. **Commercial license** – Kereskedelmi licenc – eltávolítja az összes korlátozást a termelési használathoz.

### Alap inicializálás és beállítás
Az alábbi kódrészlet bemutatja, hogyan **create a search index Java** a `Index` osztály példányosításával:

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

Az index elkészültével áttérhetünk a valós környezetben használható facettált és összetett lekérdezésekre.

## Hogyan hozhatunk létre search index java – Egyszerű facettált keresés

A facettált keresés lehetővé teszi a felhasználók számára, hogy az eredményeket előre meghatározott kategóriák (facettek) értékeinek kiválasztásával szűkítsék. Az alábbiakban lépésről‑lépésre bemutatjuk.

### 1. lépés: Index létrehozása
Először irányítsa a `Index`‑et egy mappára, ahol az indexfájlok tárolódnak.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### 2. lépés: Dokumentumok hozzáadása az indexhez
Adja meg a GroupDocs.Search‑nek, hol találhatók a forrásdokumentumok. Minden támogatott fájltípus (PDF, DOCX, TXT, stb.) automatikusan indexálva lesz.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### 3. lépés: Keresés a Content mezőben szöveges lekérdezéssel
Egy gyors szöveges lekérdezés a `content` mező szerint szűri. A `content: Pellentesque` szintaxis csak azokat a dokumentumokat adja vissza, amelyek a szövegtestben tartalmazzák a *Pellentesque* szót.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### 4. lépés: Keresés objektumalapú lekérdezéssel
Az objektumalapú lekérdezések finomhangolt vezérlést biztosítanak. Itt egy szó lekérdezést építünk, mezőlekérdezésbe ágyazzuk, majd végrehajtjuk.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Hogyan hozhatunk létre search index java – Összetett lekérdezés keresés

Az összetett lekérdezések több mezőt, Boolean operátorokat és kifejezés kereséseket kombinálnak. Ez ideális olyan helyzetekben, mint az e‑commerce szűrők vagy a jogi dokumentumok kutatása.

### 1. lépés: Index létrehozása összetett lekérdezésekhez
Használja újra ugyanazt a mappaszerkezetet; az indexet megoszthatja egyszerű és összetett forgatókönyvek között is.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### 2. lépés: Keresés szöveges lekérdezéssel
Az alábbi lekérdezés olyan fájlokat keres, amelyek neve *lorem* **és** *ipsum* **vagy** a tartalom tartalmazza a két pontos kifejezést.

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

### 3. lépés: Keresés objektumalapú lekérdezéssel
Az objektumalapú felépítés tükrözi a szöveges lekérdezést, de típusbiztonságot és IDE‑támogatást biztosít.

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

## Gyakorlati alkalmazások facettált és összetett keresésekhez

| Forgatókönyv | Hogyan segít a facettálás | Példa lekérdezés |
|--------------|---------------------------|------------------|
| **E‑commerce katalógus** | Szűrés kategória, ár, márka szerint | `category: Electronics AND price:[100 TO 500]` |
| **Jogi dokumentum tároló** | Szűrés ügyiratszám, joghatóság szerint | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Kutatási archívumok** | Szerző, publikációs év és kulcsszavak kombinálása | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Vállalati intranet** | Keresés fájltípus és részleg szerint | `filetype: pdf AND department: HR` |

## Gyakori hibák és hibaelhárítás

- **Empty results** – Üres eredmények – Ellenőrizze, hogy a dokumentumok sikeresen hozzá lettek-e adva (`index.getDocumentCount()` segíthet).  
- **Stale index** – Elavult index – Fájlok hozzáadása vagy eltávolítása után hívja meg a `index.update()`‑t, hogy az index szinkronban legyen.  
- **Incorrect field names** – Helytelen mezőnevek – Használja a `CommonFieldNames` konstansokat (`Content`, `FileName`, stb.) a gépelési hibák elkerülése érdekében.  
- **Performance bottlenecks** – Teljesítmény szűk keresztmetszet – Nagy gyűjtemények esetén fontolja meg a `index.setCacheSize()` engedélyezését vagy egy dedikált SSD használatát az index mappához.

## Gyakran feltett kérdések

**Q: Használhatom a GroupDocs.Search‑t Spring Boot‑tal?**  
A: Természetesen. Csak adja hozzá a Maven függőséget, konfigurálja az indexet Spring bean‑ként, és injektálja ahol szükséges.

**Q: Támogatja a könyvtár az egyéni metaadatmezőket?**  
A: Igen – a indexelés során felhasználó által definiált mezőket adhat hozzá, majd azokon facettálhat.

**Q: Mekkora lehet az index mérete?**  
A: Az index lemezen alapul, és milliók dokumentumát képes kezelni; csak biztosítsa a megfelelő tárhelyet és figyelje a gyorsítótár beállításait.

**Q: Van mód a találatok relevancia szerinti rangsorolására?**  
A: A GroupDocs.Search automatikusan pontszámot ad a találatoknak; a pontszámot a `SearchResult.getDocument(i).getScore()`‑val kérdezheti le.

**Q: Mi történik, ha titkosított PDF‑eket indexel?**  
A: Adja meg a jelszót a dokumentum hozzáadásakor: `index.add(filePath, password)`.

## Következtetés

Most már magabiztosan **create a search index Java** a GroupDocs.Search‑szal, dokumentumok hozzáadásával, valamint egyszerű facettált lekérdezések és kifinomult Boolean keresések megalkotásával. Ezek a lehetőségek lehetővé teszik, hogy gyors, pontos és felhasználóbarát keresési élményeket nyújtson számos alkalmazásban – az e‑commerce platformoktól a vállalati tudásbázisokig.

Készen áll a következő lépésre? Fedezze fel a **GroupDocs.Search** fejlett funkcióit, mint a **kiemelés**, **javaslatok**, és a **valós‑idejű indexelés**, hogy tovább növelje alkalmazása keresési erejét.

---

**Legutóbb frissítve:** 2025-12-16  
**Tesztelve ezzel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs