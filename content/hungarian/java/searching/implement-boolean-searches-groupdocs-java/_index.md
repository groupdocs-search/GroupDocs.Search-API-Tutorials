---
date: '2026-01-29'
description: Tanulja meg, hogyan valósíthat meg Java logikai AND/OR lekérdezéseket
  a GroupDocs.Search for Java segítségével, hogyan adhat dokumentumokat az indexhez,
  és hogyan javíthatja a dokumentumok visszakeresését.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'java boolean and or: Mesteri logikai keresések a GroupDocs.Search for Java
  segítségével'
type: docs
url: /hu/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: Mesteri Boolean keresések a GroupDocs.Search for Java-val

A dokumentumok hatalmas gyűjteményének keresése olyan, mintha tűt keresnénk a szénakazalban. A **java boolean and or** lekérdezésekkel pontosan megmondhatja a motornak, hogy mire van szüksége — dokumentumok, amelyek *mindkét* kifejezést tartalmazzák, *bármelyik* kifejezést, vagy *kizárják* a nem kívánt szavakat. Ebben az útmutatóban végigvezetjük a **GroupDocs.Search for Java** beállításán, a dokumentumok indexhez adásán, és a hatékony boolean lekérdezések megalkotásán, amelyek fokozzák a **document retrieval java** munkafolyamatait.

## Gyors válaszok
- **Mi az a boolean AND lekérdezés?** Csak azokat a dokumentumokat adja vissza, amelyek *összes* megadott kifejezést tartalmazzák.  
- **Hogyan különbözik az OR az AND-től?** Az OR olyan dokumentumokat talál, amelyek *bármelyik* kifejezést tartalmazzák, ezáltal szélesíti az eredményhalmazt.  
- **Mikor kell használni a NOT-ot?** A NOT-ot arra használja, hogy kiszűrje a nem kívánt szavakat tartalmazó dokumentumokat.  
- **Szükségem van licencre?** Az ingyenes próba a teszteléshez működik; a termeléshez kereskedelmi licenc szükséges.  
- **Melyik Java verzió szükséges?** Java 8+ támogatott; JDK 11+ ajánlott.

## Mi az a **java boolean and or**?
A **java boolean and or** lekérdezés logikai operátorokat (AND, OR, NOT) kombinál a keresési eredmények finomításához. A lekérdezések szerkezetével pontosan megmondhatja a GroupDocs.Search-nak, hogyan kapcsolódnak egymáshoz a kifejezések, így precíz irányítást kap a visszakeresési folyamat felett.

## Miért használja a GroupDocs.Search for Java-t?
- **High performance** nagy dokumentumkészleteken.  
- **Rich API** that supports both text‑based and object‑based queries.  
- **Built‑in language support** for stemming, stop‑words, and fuzzy matching.  
- **Easy integration** with Maven or direct JAR download.

## Előfeltételek
Mielőtt belemerülne, győződjön meg róla, hogy rendelkezik a következőkkel:
- **GroupDocs.Search for Java** (v25.4 vagy újabb) – lásd az alábbi letöltési hivatkozást.  
- JDK 8+ installed and configured in your IDE (IntelliJ IDEA, Eclipse, stb.).  
- Basic Java knowledge and Maven for dependency management.  

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
Alternatívaként töltse le a legújabb JAR-t a hivatalos oldalról: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenc beszerzése
Kezdje egy ingyenes próba licenccel, hogy felfedezze az összes funkciót. Termeléshez vásároljon kereskedelmi licencet a teljes funkcionalitás feloldásához.

### Alapvető inicializálás és beállítás
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

## java boolean and or: Boolean keresések megvalósítása

Az alábbiakban bemutatjuk a **AND**, **OR**, **NOT** és **complex** lekérdezéseket. Minden szakasz egy egyszerű szöveges lekérdezést és a megfelelő objektumalapú lekérdezést mutatja, így kiválaszthatja a kódbázisához legjobban illő stílust.

### Boolean AND keresés
Kombinálja a kifejezéseket **AND**-del, hogy csak azokat a dokumentumokat kapja, amelyek *minden* kulcsszót tartalmaznak.

#### Áttekintés
Az AND lekérdezés szűkíti az eredményeket, javítva a relevanciát, amikor több kritériumnak megfelelő dokumentumokra van szükség.

#### Implementációs lépések
1. **Initialize Index** – ez egyben bemutatja a **add documents to index**-et az AND szituációhoz.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – using the plain string syntax.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – useful when building queries programmatically (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### Boolean OR keresés
Használja a **OR**-t az eredmények bővítéséhez, a megadott kifejezések bármelyikének egyezésével.

#### Áttekintés
Az OR lekérdezés ideális felfedező keresésekhez, ahol legalább egy kulcsszót tartalmazó dokumentumokat szeretne megtalálni (**search with or java**).

#### Implementációs lépések
1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

### Boolean NOT keresés
Zárja ki a nem kívánt kifejezéseket **NOT**-tal, hogy szűrje a zajt az eredményekből.

#### Áttekintés
A NOT lekérdezés segít eltávolítani a nem releváns dokumentumokat, például egy versenytárs márkanevének kiszűrésével (**boolean search examples java**).

#### Implementációs lépések
1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

### Összetett Boolean lekérdezések
Kombinálja a **AND**, **OR**, és **NOT** operátorokat, hogy összetett keresési logikát hozzon létre a nagyon specifikus visszakeresési igényekhez.

#### Áttekintés
Az összetett lekérdezések lehetővé teszik a valós keresési szituációk modellezését, például „keresse meg a sportcikkeket, amelyek kedvezőek, de zárja ki a konkrét sportolók említését”.

#### Implementációs lépések
1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

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

## Gyakorlati alkalmazások a java boolean and or lekérdezésekhez
- **Document Management Systems** – keresse meg azokat a szerződéseket, amelyek mind a “confidential”, mind a “renewal” kifejezést tartalmazzák.  
- **Legal Research** – szűrje a jogeseteket **AND**/**OR** használatával, miközben a **NOT**-tal kizárja az elavult jogszabályokat.  
- **Customer Support** – szerezze meg azokat a jegyeket, amelyek említik a “login” **AND** “error” kifejezéseket, de nem a “resolved” kifejezést.  
- **Content Curation** – gyűjtsön blogbejegyzéseket a “cloud” **OR** “serverless” témában a hírlevélhez.

## Gyakori hibák és hibaelhárítás
- **Missing Index Refresh** – új dokumentumok hozzáadása után hívja meg a `index.update()`-et, hogy biztosítsa azok kereshetőségét.  
- **Incorrect Operator Spacing** – a GroupDocs.Search elvárja, hogy az operátorok (`AND`, `OR`, `NOT`) körül szóközök legyenek.  
- **Case Sensitivity** – a lekérdezések alapértelmezés szerint nem érzékenyek a kis- és nagybetűkre, de az egyedi elemzők ezt befolyásolhatják.  
- **Large Result Sets** – használjon lapozást (`search(query, 0, 100)`) a memória túlterhelés elkerülése érdekében.

## Gyakran feltett kérdések

**Q: Kombinálhatok több mint két kifejezést egy AND lekérdezésben?**  
A: Természetesen. Több `createWordQuery` objektumot is láncolhat a `createAndQuery`-val, vagy egyszerűen írhatja be a `"term1 AND term2 AND term3"` szöveges lekérdezésbe.

**Q: Támogatja a GroupDocs.Search a helyettesítő karakteres vagy fuzzy kereséseket?**  
A: Igen. A `*` karaktert használja helyettesítő karakterként (pl. `promot*`), vagy a `~`-t fuzzy egyezéshez (pl. `comfort~`).

**Q: Hogyan korlátozhatom a keresést konkrét fájltípusokra?**  
A: Használja a `FileTypeQuery` osztályt a PDF, DOCX stb. fájlokra való korlátozáshoz, és kombinálja a boolean lekérdezésével.

**Q: Mi a legjobb módja az indexelés teljesítményének nyomon követésére?**  
A: Engedélyezze a beépített naplózót (`index.getLogger().setLevel(Level.INFO)`) és tekintse át az időzítési metrikákat minden `add` művelet után.

**Q: Van mód a bizonyos kifejezések relevanciájának növelésére?**  
A: Igen. A fontos szavakat `BoostQuery`-vel körülvéve növelheti azok súlyát a pontozási algoritmusban.

---

**Utoljára frissítve:** 2026-01-29  
**Tesztelve ezzel:** GroupDocs.Search 25.4 (Java)  
**Szerző:** GroupDocs