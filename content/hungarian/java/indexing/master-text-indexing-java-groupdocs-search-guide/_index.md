---
date: '2026-11-02'
description: Ismerje meg, hogyan adhat hozzá mappát az indexhez a GroupDocs.Search
  Java-ban, konfigurálhatja a magas tömörítést, és futtathat gyors teljes szöveges
  lekérdezéseket.
keywords:
- add folder to index
- java full text search
- groupdocs search compression
lastmod: '2026-11-02'
og_description: Ismerje meg, hogyan adhat hozzá mappát az indexhez a GroupDocs.Search
  Java-ban, konfigurálhatja a tömörítést, és végrehajthat gyors teljes szöveges kereséseket.
  Ideális nagy dokumentumkészletekhez.
og_image_alt: Guide showing Java code for adding a folder to a GroupDocs.Search index
og_title: Hogyan adjon hozzá mappát az indexhez a GroupDocs.Search segítségével Java-ban
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  headline: How to add folder to index with GroupDocs.Search in Java
  type: TechArticle
- description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  name: How to add folder to index with GroupDocs.Search in Java
  steps:
  - name: define the index folder
    text: 'Choose a directory where the index files will reside:'
  - name: configure index settings
    text: '`TextStorageSettings` configures how text is stored in the index, including
      compression level. `Compression` is an enum that specifies the desired compression
      algorithm.'
  - name: create the index with custom settings
    text: 'Instantiate the index using the configuration defined above:'
  type: HowTo
- questions:
  - answer: It is a robust Java library that provides advanced full‑text search capabilities,
      including indexing, compression, and complex query support.
    question: What is GroupDocs.Search?
  - answer: Enable high compression (`Compression.High`) and periodically commit changes
      to keep the index lean. Also, allocate sufficient heap memory (e.g., 4 GB for
      indexes over 20 GB).
    question: How do I handle large datasets with GroupDocs.Search?
  - answer: Yes, the library can be embedded in any Java‑based backend, REST services,
      or micro‑services architecture.
    question: Can I integrate GroupDocs.Search with existing enterprise systems?
  - answer: Use the `index.add()` method to append new files and `index.delete()`
      to remove obsolete ones, then re‑run `index.optimize()` if needed.
    question: What if my index becomes outdated?
  - answer: Visit the community forum at [GroupDocs forums](https://forum.groupdocs.com/c/search/10)
      for troubleshooting and best‑practice tips.
    question: Where can I get help or support?
  type: FAQPage
tags:
- add folder to index
- groupdocs search
- java search indexing
title: Hogyan adjon hozzá mappát az indexhez a GroupDocs.Search segítségével Java-ban
type: docs
url: /hu/java/indexing/master-text-indexing-java-groupdocs-search-guide/
weight: 1
---

# Hogyan adjon hozzá mappát az indexhez a GroupDocs.Search Java-ban

Ha **java full text search**‑re van szüksége, amely millió dokumentumra is skálázható, jó helyen jár. Ebben az útmutatóban megtanulja, hogyan **adjon hozzá mappát az indexhez** a GroupDocs.Search segítségével, hogyan konfiguráljon nagy tömörítésű tárolást, és hogyan futtasson villámgyors lekérdezéseket. A végére egy termelésre kész megoldást kap, amelyet bármely Java projektbe be lehet illeszteni.

## Gyors válaszok
- **Mi a fő könyvtár?** GroupDocs.Search for Java  
- **Hogyan adjon hozzá egy mappát az indexhez?** Használja az `index.add(folderPath)` metódust  
- **Be tudom-e állítani a szövegtömörítést?** Igen, a `TextStorageSettings(Compression.High)` segítségével  
- **Melyik Java verzió szükséges?** JDK 8 vagy újabb  
- **Hol szerezhetek próbaverziós licencet?** A GroupDocs weboldaláról vagy a tároló oldaláról  

## Mi az a java full text search és miért fontos?

A Java full text search nyers dokumentumokat fordít visszafelé mutató indexbe, lehetővé téve almásodperces lekérdezést bármely kifejezésre több ezer fájl között. Ez a képesség elengedhetetlen jogi adattárak, kutatási könyvtárak és vállalati tudásbázisok számára, ahol a felhasználók azonnali eredményeket várnak. Emellett növeli a modern alkalmazások termelékenységét.

## Miért használjuk a groupdocs.search‑t java full text search‑hez?

A GroupDocs.Search magas áteresztőképességű indexelést és lekérdezés-végrehajtást biztosít beépített nagy tömörítéssel. **50+ bemeneti és kimeneti formátumot** támogat – köztük PDF, DOCX, EML és HTML – és képes több száz oldalas dokumentumokat feldolgozni anélkül, hogy az egész fájlt a memóriába töltené, így a tipikus munkaterhelés esetén a memóriahasználat 200 MB alatt marad.

## Előfeltételek

- **GroupDocs.Search for Java** (25.4 vagy újabb verzió) – a magkönyvtár, amely az indexelést és keresést biztosítja.  
- **JDK 8+** telepítve és beállítva – a SDK minimális futtatási környezete.  
- **Maven** a függőségkezeléshez – egyszerűsíti a könyvtár projektbe való felvételét.  
- Egy IDE, például **IntelliJ IDEA** vagy **Eclipse** – a Java kód írásához és hibakereséséhez.

## A GroupDocs.Search beállítása java-hoz

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
Alternatívaként töltse le a legújabb verziót a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

#### Licencbeszerzés
- **Ingyenes próba** – minden funkció kipróbálása kötelezettség nélkül.  
- **Ideiglenes licenc** – meghosszabbított tesztidőszak.  
- **Vásárlás** – a teljes termelési funkciók feloldása.

### Alapvető inicializálás és beállítás
Az `Index` az a fő osztály, amelyet index létrehozására, megnyitására és kezelésére használunk.

```java
import com.groupdocs.search.Index;

public class InitializeSearch {
    public static void main(String[] args) {
        // Path to store index data
        String indexPath = "path/to/index";
        
        // Creating an index at specified location
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## Szöveg indexelése egyedi tömörítéssel

### 1. lépés: az index mappájának meghatározása
Válasszon egy könyvtárat, ahol az indexfájlok tárolódni fognak:

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\StoringTextOfIndexedDocuments";
```

### 2. lépés: index beállításainak konfigurálása
A `TextStorageSettings` határozza meg, hogyan tárolódik a szöveg az indexben, beleértve a tömörítési szintet is. A `Compression` egy enum, amely a kívánt tömörítési algoritmust jelöli.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.options.TextStorageSettings;
import com.groupdocs.search.compression.Compression;

IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### 3. lépés: index létrehozása egyedi beállításokkal
Hozza létre az indexet a fent definiált konfigurációval:

```java
Index index = new Index(indexFolder, settings);
System.out.println("Index created with high compression.");
```

## Hogyan adjon hozzá egy mappát az indexhez

Az `Index` a kereshető indexet képviselő fő osztály.

Töltse be a meglévő indexet (vagy hozza létre újat), majd hívja meg az `add` metódust az `Index` objektumon. Az `add` művelet beolvassa a megadott könyvtárat, kinyeri a szöveget minden támogatott fájlból, és a tömörített indexbe helyezi, készen az azonnali keresésre.

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual document path.
Index index = new Index(indexFolder);
```

## Hogyan keressen az indexelt dokumentumokban

A `SearchResult` egyetlen találatot reprezentál a dokumentum útvonalával és relevanciájával.

Határozzon meg egy keresési lekérdezés‑sztringet, amely a keresett kifejezést vagy szókapcsolatot tartalmazza, majd hívja meg a `search` metódust az `Index` példányon. A metódus egy `SearchResult` objektumok gyűjteményét adja vissza, mindegyik tartalmazza a dokumentum útvonalát, a relevancia‑pontszámot és egy szövegrészletet, amely kiemeli a találatot.

```java
index.add(documentsFolder);
System.out.println("Documents added successfully.");
```

## Gyakorlati alkalmazások

Valós példák, ahol a **java full text search** ragyog:

1. **Jogi dokumentumkezelés** – az ügyiratok azonnali visszakeresése.  
2. **Akademiai kutatási könyvtárak** – gyors keresés dolgozatok és értekezések között.  
3. **Vállalati tudásbázisok** – gyors hozzáférés kézikönyvekhez és GYIK‑hez.  
4. **Tartalomkezelő rendszerek** – hatékony tartalomfelfedezés nagy webhelyek esetén.  
5. **Ügyfélszolgálati archívumok** – gyors keresés a múltbeli jegyek és csevegések között.  

## Teljesítménybeli megfontolások

- **Tömörítés vs. sebesség**: A magas tömörítés akár 70 % lemezhelyet takaríthat meg, de mérsékelt indexelési többletterhet okoz; futtasson benchmark teszteket az adatmennyiségre vonatkozóan.  
- **Memória kezelés**: Legalább 2 GB heapet biztosítson 10 GB‑nál nagyobb indexekhez, hogy elkerülje a `OutOfMemoryError` hibát.  
- **Index frissítések**: Új dokumentumok hozzáadásához használja az `index.add()`‑t, és időnként hívja meg az `index.optimize()`‑t az index kompakt tartásához.  
- **Lekérdezés optimalizálás**: Használja a fejlett lekérdezés‑szintaxist (helyettesítő karakterek, közelség, fuzzy keresés) a találatok szűkítéséhez és a válaszidő csökkentéséhez.

## Gyakori hibák és profi tippek

- **Hiba:** Elfelejti meghívni az `index.optimize()`‑t a tömeges hozzáadások után.  
  **Profi tipp:** Futtassa az `index.optimize()`‑t éjszakánként, hogy az index kompakt maradjon.  

- **Hiba:** Alapértelmezett (alacsony) tömörítés használata hatalmas adatkészleteken.  
  **Profi tipp:** Állítsa `Compression.High`‑ra a termelési környezetben a tárolási költségek csökkentése érdekében.  

- **Hiba:** Nem kezeli az `IOException`‑t hálózati megosztásról történő fájlhozzáadáskor.  
  **Profi tipp:** Tegye az `index.add()`‑t try‑catch blokkba, és naplózza a hibákat későbbi felülvizsgálatra.  

## Gyakran feltett kérdések

**K: Mi a GroupDocs.Search?**  
V: Egy robusztus Java könyvtár, amely fejlett full‑text keresési képességeket biztosít, beleértve az indexelést, tömörítést és összetett lekérdezéstámogatást.

**K: Hogyan kezeljem a nagy adatállományokat a GroupDocs.Search‑szal?**  
V: Engedélyezze a magas tömörítést (`Compression.High`) és időszakosan commit‑olja a változásokat, hogy az index karcsú maradjon. Emellett biztosítson elegendő heap memóriát (például 4 GB 20 GB‑nál nagyobb indexekhez).

**K: Integrálhatom a GroupDocs.Search‑t meglévő vállalati rendszerekkel?**  
V: Igen, a könyvtár beágyazható bármely Java‑alapú háttérrendszerbe, REST szolgáltatásba vagy mikro‑szolgáltatás‑architektúrába.

**K: Mi a teendő, ha az index elavul?**  
V: Használja az `index.add()` metódust új fájlok hozzáadásához és az `index.delete()`‑t elavultak eltávolításához, majd szükség esetén futtassa újra az `index.optimize()`‑t.

**K: Hol kaphatok segítséget vagy támogatást?**  
V: Látogassa meg a közösségi fórumot a [GroupDocs forums](https://forum.groupdocs.com/c/search/10) oldalon a hibakereséshez és legjobb gyakorlatokhoz.

## További források

- Részletes használati útmutató: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- Teljes API referencia: [API Reference Guide](https://reference.groupdocs.com/search/java)  
- Legújabb funkciók nyomon követése: [Latest Releases](https://releases.groupdocs.com/search/java/)  

---

**Utoljára frissítve:** 2026-11-02  
**Tesztelve a következővel:** GroupDocs.Search 25.4  
**Szerző:** GroupDocs  

---

```java
String query = "sample";  
```

```java
import com.groupdocs.search.results.SearchResult;

SearchResult result = index.search(query);
System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## Kapcsolódó oktatóanyagok

- [Groupdocs Search Java Create Index Guide](/search/java/indexing/groupdocs-search-java-create-index-guide/)
- [Mastering Groupdocs Search Java Index Management Guide](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Java Full Text Search Library – Optimize Index with GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)