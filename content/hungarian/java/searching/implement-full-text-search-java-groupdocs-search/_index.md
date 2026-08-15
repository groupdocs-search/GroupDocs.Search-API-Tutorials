---
date: '2026-08-15'
description: Ismerjen meg egy full text search példát Java-ban a GroupDocs.Search
  segítségével, amely bemutatja a dokumentumok indexhez adását, a boolean query java
  használatát és a teljesítmény optimalizálását.
keywords:
- full text search example
- add documents to index
- boolean query java
lastmod: '2026-08-15'
og_description: Fedezze fel a full text search példát Java-ban a GroupDocs.Search
  segítségével. Ismerje meg, hogyan adhat dokumentumokat az indexhez, hogyan készíthet
  boolean query java utasításokat, és hogyan növelheti a keresés teljesítményét.
og_image_alt: Guide showing how to implement a full text search example in Java with
  GroupDocs.Search
og_title: Full text search példa Java-ban a GroupDocs.Search használatával
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn a full text search example in Java with GroupDocs.Search, covering
    adding documents to index, boolean query java, and performance optimization.
  headline: Full text search example in Java using GroupDocs.Search
  type: TechArticle
- description: Learn a full text search example in Java with GroupDocs.Search, covering
    adding documents to index, boolean query java, and performance optimization.
  name: Full text search example in Java using GroupDocs.Search
  steps:
  - name: create an index
    text: The `Index` class is the searchable container that stores indexed documents
      on disk.
  - name: add documents (add documents to index)
    text: You can index everything in a folder or limit to certain extensions using
      a `DocumentFilter`. > **Explanation:** > - `Index` represents the searchable
      database. > - `add()` ingests files; the wildcard `*.*` grabs all files, while
      `DocumentFilter` lets you fine‑tune the **add documents to index** ste
  - name: execute the search
    text: '> **Explanation:** > - `search()` runs the query against the index. > -
      `getDocumentCount()` tells you how many documents matched—useful for quick sanity
      checks.'
  type: HowTo
- questions:
  - answer: It indexes the raw text of every document so you can query any word or
      phrase instantly.
    question: What is full text search example?
  - answer: GroupDocs.Search for Java handles PDF, DOCX, XLSX, PPTX, HTML, TXT, and
      over 50 other file types.
    question: Which library supports multiple formats?
  - answer: Call the `index.add()` method with a folder path or a custom `DocumentFilter`.
    question: How do I add documents to index?
  - answer: Yes—combine terms with AND, OR, NOT for precise results.
    question: Can I run Boolean queries?
  - answer: Use incremental indexing, enable result caching, and disable phonetic
      search unless needed.
    question: How do I improve performance?
  type: FAQPage
tags:
- full text search
- GroupDocs.Search
- Java document indexing
- search performance
title: Full text search példa Java-ban a GroupDocs.Search használatával
type: docs
url: /hu/java/searching/implement-full-text-search-java-groupdocs-search/
weight: 1
---

# Teljes szöveges keresés példa Java-ban a GroupDocs.Search használatával

Ha **teljes szöveges keresés példát** keres, amely PDF-ek, Word fájlok, táblázatok és egyéb formátumok között működik, jó helyen jár. A több ezer dokumentum manuális átvizsgálása óriási szűk keresztmetszet, de a GroupDocs.Search for Java automatizálja az indexelést és a lekérdezést villámgyorsan. Ebben az útmutatóban mindent végigvezetünk, amire szüksége van a működéshez – a dokumentumok indexhez adásától, a boolean lekérdezés Java utasítások megírásáig, egészen a keresési teljesítmény optimalizálásáig a termelési környezetben.

## Gyors válaszok
- **Mi a teljes szöveges keresés példa?** Az összes dokumentum nyers szövegét indexeli, így bármely szót vagy kifejezést azonnal lekérdezhet.  
- **Melyik könyvtár támogat több formátumot?** A GroupDocs.Search for Java kezeli a PDF, DOCX, XLSX, PPTX, HTML, TXT és több mint 50 egyéb fájltípust.  
- **Hogyan adhatok dokumentumokat az indexhez?** Hívja meg az `index.add()` metódust egy mappával vagy egy egyéni `DocumentFilter`-rel.  
- **Futtathatok Boolean lekérdezéseket?** Igen—összekapcsolhatja a kifejezéseket AND, OR, NOT operátorokkal a pontos eredményekért.  
- **Hogyan javíthatom a teljesítményt?** Használjon inkrementális indexelést, engedélyezze az eredménygyorsítót, és tiltsa le a fonetikus keresést, ha nincs rá szükség.

## Mi a teljes szöveges keresés példa?
A teljes szöveges keresés példa lehetővé teszi a dokumentumok teljes szöveges tartalmának átvizsgálását, hatékony indexben való tárolását, és a megfelelő rekordok azonnali visszaadását. A fájlnév‑alapú keresésekkel ellentétben a PDF‑ek, Word dokumentumok, táblázatok és egyéb támogatott formátumok belsejét is átnézi, így ideális dokumentumkezelő rendszerekhez, ügyfélszolgálati portálokhoz és bármely alkalmazáshoz, ahol a felhasználóknak gyorsan kell információt találniuk.

## Miért használjuk a GroupDocs.Search for Java-t?
A GroupDocs.Search for Java több mint 50 fájltípushoz nyújt többformátumos támogatást, köztük PDF, DOCX, XLSX, PPTX, HTML és egyszerű szöveg. Millió fájlra skálázható, miközben alacsony memóriahasználatot biztosít az index lemezen történő tárolásával. A könyvtár fejlett lekérdezési nyelvet tartalmaz beépített Boolean, fuzzy és fonetikus keresésekkel, és egyetlen Maven függőséggel integrálható, így percek alatt elkezdhet indexelni.

## Előfeltételek
- **Java 11+** (Java 8 is működik, de a jobb teljesítmény érdekében a Java 11 vagy újabb ajánlott).  
- **Maven** a függőségkezeléshez.  
- A **GroupDocs.Search** licenc (egy ingyenes próbaverzió kulcs elegendő a fejlesztéshez).  

### Szükséges könyvtárak és függőségek
Addja a tárolót és a függőséget a `pom.xml`‑hez:

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

A részletes használathoz tekintse meg a [dokumentációt](https://docs.groupdocs.com/search/java/).

### Környezet beállítása
- Telepítse a JDK‑t (8 vagy újabb) és konfigurálja a `JAVA_HOME` változót.  
- Használjon IDE‑t, például IntelliJ IDEA‑t vagy Eclipse‑et a könnyebb hibakereséshez.  

### Tudás előfeltételek
- Alapvető Java programozási koncepciók.  
- Ismerje a Maven `pom.xml` struktúráját.  

## A GroupDocs.Search for Java beállítása
A könyvtárat behozhatja Maven‑en keresztül (lásd fent) vagy manuálisan letöltheti a JAR‑t.

### Közvetlen letöltés (ha a manuális beállítást részesíti előnyben)
Szerezze be a legújabb csomagot a [GroupDocs.Search for Java kiadások](https://releases.groupdocs.com/search/java/) oldaláról.

### Licenc beszerzési lépések
1. **Ingyenes próba** – Regisztráljon és kapjon egy ideiglenes kulcsot.  
2. **Ideiglenes licenc** – Kérjen hosszabb távú kulcsot a kiterjesztett teszteléshez.  
3. **Megvásárlás** – Frissítsen teljes kereskedelmi licencre, amikor készen áll a termelésre.

### Alapvető inicializálás és beállítás
Hozzon létre egy index mappát a lemezen, és ellenőrizze, hogy a könyvtár helyesen betöltődik:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index in the specified directory
        Index index = new Index("C:\\MyIndex");
        
        System.out.println("GroupDocs.Search initialized!");
    }
}
```

> **Pro tipp:** Tartsa az index könyvtárát egy gyors SSD‑n a lekérdezési késleltetés minimalizálása érdekében.

## Dokumentumok hozzáadása az indexhez
**Miért fontos ez:** Keresési eredmények nem lehetségesek indexelt tartalom nélkül. Az alábbiakban bemutatjuk, hogyan adhat hozzá teljes mappákat vagy szűrheti a konkrét fájltípusokat.

### 1. lépés: index létrehozása
Az `Index` osztály a kereshető tároló, amely a lemezen tárolja az indexelt dokumentumokat.

```java
Index index = new Index("C:\\MyIndex");
```

### 2. lépés: dokumentumok hozzáadása (dokumentumok indexelése)
Az egész mappát indexelheti, vagy egy `DocumentFilter` segítségével korlátozhatja a kiterjesztéseket.

```java
index.add("C:\\Documents\\*.*"); // Adds all documents from the specified directory
// For specific file types, use:
index.add("C:\\Reports", new DocumentFilter() {
    @Override
    public boolean accept(String fileName) {
        return fileName.endsWith(".pdf") || fileName.endsWith(".docx");
    }
});
```

> **Magyarázat:**  
> - `Index` a kereshető adatbázist jelenti.  
> - `add()` fájlokat olvas be; a `*.*` helyettesítő minden fájlt, míg a `DocumentFilter` finomhangolja a **dokumentumok indexelése** lépést.

## Keresés végrehajtása (dokumentumok keresése Java)
Miután az index tartalmaz adatot, lekérdezheti azt.

### 1. lépés: lekérdezés létrehozása
```java
String query = "GroupDocs";
```

### 2. lépés: keresés végrehajtása
```java
SearchResult result = index.search(query);
System.out.println("Documents found: " + result.getDocumentCount());
```

> **Magyarázat:**  
> - `search()` futtatja a lekérdezést az indexen.  
> - `getDocumentCount()` megmutatja, hány dokumentum egyezett – hasznos gyors ellenőrzéshez.

## Haladó lekérdezési technikák (boolean lekérdezés Java)
### Boolean lekérdezések
A `BooleanQuery` osztály lehetővé teszi összetett kifejezések építését AND, OR, NOT operátorokkal.

```java
String booleanQuery = "GroupDocs AND Java";
SearchResult booleanResult = index.search(booleanQuery);
```

### Fonetikus keresések (opcionális a fuzzy egyezéshez)
A `PhoneticSearch` funkció lehetővé teszi a fonetikus egyezést helytelenül írt kifejezésekre, de extra terhet jelent.

```java
index.getSettings().setPhoneticSearch(true);
```

> **When to use:** Engedélyezze a fonetikus keresést csak akkor, ha a felhasználók gyakran elütik a szavakat; egyébként tartsa letiltva a **keresési teljesítmény optimalizálása** érdekében.

## Gyakori problémák és megoldások
| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Hiányzó dokumentumok** | Helytelen fájlútvonal vagy nem elegendő jogosultság | Ellenőrizze az útvonalat és adjon olvasási jogosultságot |
| **Lassú lekérdezések** | Nagy index gyorsítótár nélkül vagy felesleges fonetikus keresés | Engedélyezze a gyorsítótárat, tiltsa le a fonetikus keresést, és fontolja meg az index felosztását |
| **Memóriahiány hibák** | Az index mérete meghaladja a JVM heap-et | Növelje a `-Xmx` értékét vagy használjon inkrementális indexelést |

## Gyakorlati alkalmazások
A GroupDocs.Search kiemelkedik a valós helyzetekben:

1. **Tartalomkezelő rendszerek** – Azonnali teljes szöveges keresést biztosítanak cikkek, PDF‑ek és médiaeszközök között.  
2. **Ügyfélszolgálati portálok** – Az ügynökök másodpercek alatt megtalálják a megfelelő kézikönyveket vagy irányelveket.  
3. **Vállalati dokumentumtárak** – Keresés szerződések, jelentések és megfelelőségi dokumentumok között anélkül, hogy az adatokat külön adatbázisba kellene áthelyezni.

## Teljesítmény szempontok
### A keresés teljesítményének optimalizálása
- **Inkrementális indexelés:** Csak a módosított fájlokat adja hozzá vagy frissítse, a teljes index újraépítése helyett.  
- **Gyorsítótárazás:** Tartsa a gyakran használt lekérdezési eredményeket memóriában.  
- **Erőforrás monitorozás:** Állítsa be a JVM heap‑et (`-Xmx2g` vagy nagyobb) az index mérete alapján.

### Erőforrás‑használati irányelvek
- Tárolja az index mappát egy gyors SSD vagy NVMe meghajtón.  
- Figyelje a CPU‑t és a memóriát a tömeges indexelés során; korlátozza a kötegelt műveleteket a csúcsok elkerülése érdekében.

### Legjobb gyakorlatok a Java memória kezeléséhez
- Használja a `try‑with‑resources`‑t az adatfolyamokkal való munka során.  
- Nullázza a nagy objektumokat használat után a szemétgyűjtés segítése érdekében.

## Összegzés
Most már rendelkezik egy komplett, termelés‑kész **teljes szöveges keresés példával** Java‑ban a GroupDocs.Search segítségével. A könyvtár beállításától, **dokumentumok indexeléséig**, a **boolean lekérdezés Java** utasítások megírásáig, egészen a **keresési teljesítmény optimalizálásáig**, minden lépés lefedésre került.  

### Következő lépések
Fedezze fel a mélyebb funkciókat, például egyedi elemzőket, szinonima szótárakat és felhő‑tároló integrációt, a hivatalos [GroupDocs.Search dokumentáció](https://docs.groupdocs.com/search/java/) megtekintésével.

---

## Gyakran ismételt kérdések

**Q:** Milyen fájlformátumokat támogat a GroupDocs.Search?  
**A:** Több mint 50 formátum, köztük PDF, DOCX, XLSX, PPTX, HTML, TXT és számos képformátum.

**Q:** Hogyan kezeljem a nagy adathalmazokat?  
**A:** Ossza fel őket több indexre, frissítse inkrementálisan, és engedélyezze az eredménygyorsítót a késleltetés alacsonyan tartásához.

**Q:** Futtatható a GroupDocs.Search felhő környezetben?  
**A:** Igen—az index mappát mutathatja egy csatolt felhő‑tárolóra (például Azure Blob, AWS S3 fájlrendszer‑illesztővel).

**Q:** Mik az előnyei a GroupDocs.Search‑nek más könyvtárakkal szemben?  
**A:** Többformátumos támogatás, beépített Boolean/fonetikus lekérdezések, valamint egy könnyű Java API, amely millió dokumentumot dolgoz fel alacsony memóriaigénnyel.

**Q:** Hogyan hárítsam el a teljesítményproblémákat?  
**A:** Vizsgálja felül az index beállításait, tiltsa le a fonetikus keresést, ha nincs rá szükség, és figyelje a JVM memória/CPU használatát az indexelés és lekérdezés során.

**Legutóbb frissítve:** 2026-08-15  
**Tesztelve ezzel:** GroupDocs.Search 25.4  
**Szerző:** GroupDocs  

**Erőforrások**  
- **Dokumentáció:** [GroupDocs.Search dokumentáció](https://docs.groupdocs.com/search/java/)  
- **API referencia:** [API referencia útmutató](https://reference.groupdocs.com/search/java)  
- **Letöltés:** [Legújabb kiadások](https://releases.groupdocs.com/search/java/)  
- **GitHub:** [Forráskód a GitHub-on](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Támogatás:** [Fórum és közösségi támogatás](https://forum.groupdocs.com/c/search/10)  
- **Licenc:** [Ideiglenes licenc kérése](https://purchase.groupdocs.com/temporary-license/)  

## Kapcsolódó oktatóanyagok

- [Hogyan valósítsuk meg a Java teljes szöveges keresést: index könyvtár létrehozása a GroupDocs.Search segítségével](/search/java/indexing/groupdocs-search-java-create-index/)
- [Hogyan adjunk dokumentumokat az indexhez a GroupDocs.Search for Java használatával](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Kérdezési teljesítmény javítása a GroupDocs.Search Java-val: Index és keresés optimalizálása](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)