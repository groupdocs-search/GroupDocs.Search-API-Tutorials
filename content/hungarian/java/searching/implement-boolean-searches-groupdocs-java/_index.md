---
date: '2026-07-21'
description: A Boolean lekérdezés létrehozása Java tutorial bemutatja, hogyan valósítható
  meg a boolean AND, OR, NOT keresés a GroupDocs.Search for Java segítségével, hogyan
  adhatók dokumentumok egy indexhez, és hogyan boost-olható a dokumentumok visszakeresése.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: A Boolean lekérdezés létrehozása Java tutorial lépésről‑lépésre elmagyarázza,
  hogyan építhetőek AND, OR, NOT lekérdezések a GroupDocs.Search for Java segítségével,
  hogyan adhatók dokumentumok egy indexhez, és hogyan javítható a visszakeresési teljesítmény.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Boolean lekérdezés létrehozása Java – Mesteri Boolean keresések a GroupDocs.Search
  segítségével
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Boolean lekérdezés létrehozása Java-ban: Mesteri Boolean keresések a GroupDocs.Search
  for Java segítségével'
type: docs
url: /hu/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Boolean lekérdezés létrehozása Java-ban: Mesteri Boolean keresések a GroupDocs.Search for Java-val

Nagy mennyiségű dokumentum gyűjteményének keresése olyan érzés lehet, mintha tűt keresnénk a szénakazalban. **Create Boolean Query Java** lehetővé teszi, hogy pontosan megmondja a motornak, mire van szüksége — dokumentumok, amelyek *mindkét* kifejezést tartalmazzák, *bármelyik* kifejezést, vagy *kizárják* a nem kívánt szavakat. Ebben az útmutatóban végigvezetünk a **GroupDocs.Search for Java** beállításán, a dokumentumok indexhez adásán, és erőteljes boolean lekérdezések megalkotásán, amelyek fokozzák a **document retrieval java** munkafolyamatait. A végére képes lesz tiszta, karbantartható kódot írni, amely néhány sorral hoz létre boolean lekérdezéseket Java-ban.

## Gyors válaszok
- **Mi a boolean AND lekérdezés?** Csak azokat a dokumentumokat adja vissza, amelyek tartalmazzák az összes megadott kifejezést.  
- **Miben különbözik az OR az AND-től?** Az OR olyan dokumentumokat talál, amelyek *bármelyik* kifejezést tartalmazzák, ezáltal szélesíti az eredményhalmazt.  
- **Mikor kell használni a NOT-ot?** Használja a NOT-ot a nem kívánt szavakat tartalmazó dokumentumok kiszűrésére.  
- **Szükségem van licencre?** Az ingyenes próbaidőszak tesztelésre megfelelő; a termeléshez kereskedelmi licenc szükséges.  
- **Melyik Java verzió szükséges?** A Java 8+ támogatott; a JDK 11+ ajánlott.

## Mi az **create boolean query java**?
`create boolean query java` egy keresési lekérdezés Java-ban történő felépítésére utal, amely logikai operátorokat (AND, OR, NOT) kombinál a GroupDocs.Search API használatával. Ezeknek az operátoroknak az összeállításával pontosan szabályozhatja, hogy mely dokumentumok egyeznek, lehetővé téve a fejlett szűrést, a relevancia finomhangolását és összetett keresési forgatókönyveket.

## Miért használja a GroupDocs.Search for Java-t?
- **Magas teljesítmény** nagy dokumentumkészleteken – egy szabványos szerveren egy perc alatt indexel és keres 500 GB szöveget.  
- **Gazdag API**, amely támogatja a szövegalapú és objektumalapú lekérdezéseket is, lehetővé téve, hogy a saját architektúrájához illő stílust válassza.  
- **Beépített nyelvtámogatás** a szótövezéshez, stop‑szavakhoz és fuzzy egyezéshez több mint 30 nyelven.  
- **Könnyű integráció** Maven-nel vagy közvetlen JAR letöltéssel, csak néhány kódsor szükséges a kezdéshez.

## Előkövetelmények
Mielőtt belemerülne, győződjön meg róla, hogy rendelkezik:
- **GroupDocs.Search for Java** (v25.4 vagy újabb) – lásd az alábbi letöltési linket.  
- JDK 8+ telepítve és konfigurálva az IDE-jében (IntelliJ IDEA, Eclipse, stb.).  
- Alapvető Java ismeretek és Maven a függőségkezeléshez.  

## A GroupDocs.Search for Java beállítása

### Maven beállítás
Adja hozzá a tárolót és a függőséget a `pom.xml`-hez:

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
Alternatívaként töltse le a legújabb JAR-t a hivatalos oldalról: [GroupDocs.Search for Java kiadások](https://releases.groupdocs.com/search/java/).

### Licenc beszerzése
Kezdje egy ingyenes próbalicencel, hogy felfedezze az összes funkciót. Termeléshez vásároljon kereskedelmi licencet a teljes funkcionalitás feloldásához.

### Alap inicializálás és beállítás
Hozzon létre egy index mappát, és példányosítsa az `Index` objektumot:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## Hogyan hozhat létre boolean lekérdezést Java-ban?
Az `Index` osztály egy kereshető dokumentumgyűjteményt képvisel, amely a lemezen tárolódik. A `BooleanQuery` több al‑lekérdezést kombinál logikai operátorokkal. `createAndQuery`, `createOrQuery` és `createNotQuery` az AND, OR és NOT al‑lekérdezéseket hozza létre. Töltsön be vagy hozzon létre egy `Index` példányt, adjon hozzá dokumentumokat, majd építsen egy `BooleanQuery` objektumot a `createAndQuery`, `createOrQuery` vagy `createNotQuery` használatával. Hívja meg a `index.search(query)` metódust a megfelelő dokumentumok lekéréséhez. Ez a minta egyszerű és összetett forgatókönyvekhez egyaránt működik, és csak három logikai lépést igényel: index inicializálás, dokumentum hozzáadás és lekérdezés végrehajtás.

## Boolean AND keresés

### Áttekintés
Az AND lekérdezés szűkíti az eredményeket, javítva a relevanciát, amikor több kritériumnak megfelelő dokumentumokra van szükség.

### Megvalósítási lépések
1. **Index inicializálása** – ez emellett bemutatja az **add documents to index** lépést az AND forgatókönyvhöz.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Dokumentumok indexelése**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Szöveges lekérdezés keresés végrehajtása** – egyszerű karakterlánc szintaxis használatával.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Objektum lekérdezés keresés végrehajtása** – hasznos, ha programozottan épít lekérdezéseket (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Boolean OR keresés

### Áttekintés
Az OR lekérdezés ideális feltáró keresésekhez, ahol több kulcsszó közül legalább egyet tartalmazó dokumentumokat szeretne rögzíteni (**search with or java**).

### Megvalósítási lépések
1. **Index inicializálása**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Dokumentumok indexelése**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Szöveges lekérdezés keresés végrehajtása**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Objektum lekérdezés keresés végrehajtása**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Boolean NOT keresés

### Áttekintés
A NOT lekérdezés segít eltávolítani a nem releváns dokumentumokat, például kiszűrni egy versenytárs márkanevét (**boolean search examples java**).

### Megvalósítási lépések
1. **Index inicializálása**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Dokumentumok indexelése**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Szöveges lekérdezés keresés végrehajtása**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Objektum lekérdezés keresés végrehajtása**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## Összetett Boolean lekérdezések

### Áttekintés
Az összetett lekérdezések lehetővé teszik valós keresési forgatókönyvek modellezését, például „keresse meg a sportcikkeket, amelyek kedvezőek, de kizárja bármely konkrét sportoló említését”.

### Megvalósítási lépések
1. **Index inicializálása**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Dokumentumok indexelése**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Szöveges lekérdezés keresés végrehajtása**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Objektum lekérdezés keresés végrehajtása**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## A **java boolean and or** lekérdezések gyakorlati alkalmazásai
- **Document Management Systems** – keresse meg azokat a szerződéseket, amelyek tartalmazzák a “confidential” **AND** “renewal” kifejezéseket.  
- **Legal Research** – szűrje a jogeseteket **AND**/**OR** használatával, miközben a **NOT** segítségével kizárja az elavult jogszabályokat.  
- **Customer Support** – szerezze be azokat a jegyeket, amelyek említik a “login” **AND** “error” kifejezéseket, de nem a “resolved” kifejezést.  
- **Content Curation** – gyűjtsön blogbejegyzéseket a “cloud” **OR** “serverless” témáról egy hírlevélhez.

## Gyakori hibák és hibaelhárítás
- **Hiányzó index frissítés** – új dokumentumok hozzáadása után hívja meg a `index.update()` metódust, hogy biztosítsa, hogy kereshetők legyenek.  
- **Helytelen operátorok közti szóköz** – a GroupDocs.Search szóközöket vár az operátorok (`AND`, `OR`, `NOT`) körül.  
- **Kis- és nagybetű érzékenység** – a lekérdezések alapértelmezés szerint nem érzékenyek a kis- és nagybetűkre, de az egyedi elemzők befolyásolhatják ezt.  
- **Nagy eredményhalmazok** – használjon lapozást (`search(query, 0, 100)`) a memória túlterhelés elkerülése érdekében.  

## Gyakran feltett kérdések
**K: Kombinálhatok több mint két kifejezést egy AND lekérdezésben?**  
A: Természetesen. Több `createWordQuery` objektumot is láncolhat a `createAndQuery`-val, vagy egyszerűen írja be a `"term1 AND term2 AND term3"` szöveget a szöveges lekérdezésbe.

**K: Támogatja a GroupDocs.Search a helyettesítő karakteres vagy fuzzy kereséseket?**  
A: Igen. A `*` karaktert helyettesítő karakterként használja (pl. `promot*`), vagy a `~`-t fuzzy egyezéshez (pl. `comfort~`).

**K: Hogyan korlátozhatom a keresést bizonyos fájltípusokra?**  
`FileTypeQuery` a keresési eredményeket bizonyos fájlformátumokra, például PDF vagy DOCX korlátozza.  
A: Használja a `FileTypeQuery` osztályt a PDF, DOCX stb. formátumokra való korlátozáshoz, és kombinálja azt a boolean lekérdezésével.

**K: Mi a legjobb módja az indexelés teljesítményének nyomon követésére?**  
A: Engedélyezze a beépített naplózót (`index.getLogger().setLevel(Level.INFO)`) és tekintse át az időzítési metrikákat minden egyes `add` művelet után.

**K: Van mód a bizonyos kifejezések relevanciájának növelésére?**  
`BoostQuery` növeli a megadott kifejezések relevancia pontszámát egy keresési lekérdezésben.  
A: Igen. Fontos szavakat csomagoljon `BoostQuery`-val, hogy növelje azok súlyát a pontozási algoritmusban.

---

**Utoljára frissítve:** 2026-07-21  
**Tesztelve ezzel:** GroupDocs.Search 25.4 (Java)  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [Boolean Operátorok Java – Keresési index létrehozása és faceted keresés](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Master GroupDocs.Search Java: Hatékony dokumentumkeresés és indexkezelés](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - A GroupDocs.Search Java elsajátítása – Keresési index létrehozása és kezelése](/search/java/indexing/groupdocs-search-java-create-index-guide/)