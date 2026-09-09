---
date: '2026-08-10'
description: Ismerje meg, hogyan hozhat létre kereshető indexet Java-ban, és engedélyezheti
  a kis‑ és nagybetű érzékeny keresést a GroupDocs.Search segítségével, növelve a
  Java alkalmazások pontosságát.
keywords:
- create searchable index java
- case sensitive search java
- groupdocs search java tutorial
- java text query search
lastmod: '2026-08-10'
og_description: Ismerje meg, hogyan hozhat létre kereshető indexet Java-ban, és engedélyezheti
  a kis‑ és nagybetű érzékeny keresést a GroupDocs.Search segítségével. Lépésről‑lépésre
  útmutató Java fejlesztőknek.
og_image_alt: Guide to creating a searchable index in Java using GroupDocs with case‑sensitive
  search
og_title: 'Kereshető index létrehozása Java-ban: dokumentumok hozzáadása kis‑ és nagybetű
  érzékeny kereséshez'
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to create searchable index java and enable case‑sensitive
    search with GroupDocs.Search, boosting accuracy for Java applications.
  headline: 'Create searchable index java: add docs case‑sensitive search'
  type: TechArticle
- description: Learn how to create searchable index java and enable case‑sensitive
    search with GroupDocs.Search, boosting accuracy for Java applications.
  name: 'Create searchable index java: add docs case‑sensitive search'
  steps:
  - name: create an index and add your documents
    text: The `Index` class represents a searchable storage area on disk where documents
      are indexed. > **Pro tip:** You can call `index.add()` multiple times to **search
      across multiple directories** in a single index.
  - name: enable case‑sensitive search
    text: '`SearchOptions` configures how queries are processed, including case sensitivity
      and other search behaviors.'
  - name: execute a case‑sensitive text query
    text: '`SearchQuery` builds the query object that the engine evaluates against
      the index. The loop prints the full path of each document that contains the
      exact case‑matched term.'
  - name: initialize a second index (optional)
    text: A second `Index` instance can be created to isolate object‑based searches
      from plain‑text searches.
  - name: re‑use the case‑sensitive option
    text: '`SearchOptions` can be reused across different query types to maintain
      consistent case handling.'
  - name: build and run an object query
    text: '`WordQuery` represents a word‑level search that can be combined with other
      query types for complex searches. Using `createWordQuery` lets you later combine
      it with phrase, wildcard, or Boolean queries for more complex scenarios.'
  type: HowTo
- questions:
  - answer: Add documents to an index with `index.add(...)`.
    question: What is the primary step to start searching?
  - answer: Set `options.setUseCaseSensitiveSearch(true)`.
    question: How do you enable case‑sensitive search?
  - answer: Yes – call `index.add()` for each folder you want to include.
    question: Can you search across multiple directories?
  - answer: Use `SearchQuery.createWordQuery(...)`.
    question: Which method lets you search with objects?
  - answer: A temporary license is available for trial purposes.
    question: Do you need a license for testing?
  type: FAQPage
tags:
- create searchable index
- case-sensitive search
- groupdocs search
- java document processing
title: 'Kereshető index létrehozása Java-ban: dokumentumok hozzáadása kis‑ és nagybetű
  érzékeny kereséshez'
type: docs
url: /hu/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Kereshető index létrehozása Java: dokumentumok hozzáadása kis- és nagybetű érzékeny keresés

A modern Java‑alkalmazásokban a **creating a searchable index java** az alapja a gyors, pontos információkinyerésnek nagy dokumentumgyűjteményekből. Ez az útmutató bemutatja, hogyan adhatunk dokumentumokat egy indexhez, hogyan engedélyezhetjük a kis‑ és nagybetű érzékeny keresést, és hogyan finomhangolhatjuk a folyamatot a GroupDocs.Search segítségével. Akár jogi adattárat, e‑kereskedelmi katalógust vagy tartalomkezelő rendszert épít, ezek a lépések segítenek pontos eredményeket nyújtani, amelyekkel a felhasználók elégedettek lesznek.

## Gyors válaszok
- **Mi a legfontosabb lépés a keresés megkezdéséhez?** Add dokumentumokat egy indexhez a `index.add(...)` használatával.  
- **Hogyan lehet engedélyezni a kis‑ és nagybetű érzékeny keresést?** Állítsa be a `options.setUseCaseSensitiveSearch(true)` értéket.  
- **Kereshet több könyvtárban egyszerre?** Igen – hívja meg az `index.add()`‑t minden mappához, amelyet fel szeretne venni.  
- **Melyik metódus teszi lehetővé a objektumokkal való keresést?** Használja a `SearchQuery.createWordQuery(...)`‑t.  
- **Szükség van licencre a teszteléshez?** Ideiglenes licenc áll rendelkezésre próbaverzióhoz.

## Mit jelent a „dokumentumok hozzáadása az indexhez”?
A dokumentumok indexhez adása azt jelenti, hogy forrásfájljait (PDF‑ek, Word‑dokumentumok, egyszerű szöveg stb.) a GroupDocs.Search‑nek átadjuk, hogy kereshető adatstruktúrát építsen fel. Az index tokenizált kifejezéseket, pozíciókat és metaadatokat tárol, lehetővé téve a motor számára a gyors lekérdezések végrehajtását, beleértve a kis‑ és nagybetű érzékeny kereséseket, és a találatok hatékony rangsorolását.

## Miért engedélyezzük a kis‑ és nagybetű érzékeny keresést Java‑ban?
A kis‑ és nagybetű érzékeny keresés lehetővé teszi, hogy a motor megkülönböztesse azokat a kifejezéseket, amelyek csak betűméretben térnek el, ami kritikus olyan területeken, ahol a nagybetűhasználat jelentéssel bír. Ez pontos kifejezés egyezést biztosít, támogatja a szabályozási megfelelőségi követelményeket, és javítja a relevanciát azáltal, hogy a felhasználó lekérdezésének pontos betűesetét visszaadja.

- **Pontos kifejezés egyezés** – például „Apple” (cég) vs. „apple” (gyümölcs).  
- **Szabályozási megfelelőség** – sok iparág pontos kifejezés egyezést igényel.  
- **Javított relevancia** – a technikai és jogi felhasználók gyakran elvárják a betűérzékeny eredményeket.

## Előfeltételek
- JDK 17 vagy újabb (ajánlott)  
- Maven a függőségkezeléshez  
- IDE, például IntelliJ IDEA vagy Eclipse  
- Alapvető ismeretek a Java programozásban  

## A GroupDocs.Search beállítása Java‑hoz
Az alábbi Maven‑kódrészlet hozzáadja a GroupDocs.Search tárolót és a szükséges függőséget a projektjéhez.

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

Alternatívaként letöltheti a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licencelés
A próbaverzió elindításához látogasson el a GroupDocs oldalára, és szerezzen be egy ideiglenes licencet. Ez lehetővé teszi, hogy korlátozás nélkül tesztelje az összes funkciót.

## Hogyan hozzunk létre kereshető indexet Java – szöveges lekérdezés keresés

### 1. lépés: index létrehozása és dokumentumok hozzáadása
Az `Index` osztály egy kereshető tárolóhelyet képvisel a lemezen, ahol a dokumentumok indexelésre kerülnek.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Pro tipp:** Többször is meghívhatja a `index.add()`‑t, hogy **több könyvtárban keressen** egyetlen indexben.

### 2. lépés: kis‑ és nagybetű érzékeny keresés engedélyezése
A `SearchOptions` beállítja, hogyan dolgozzák fel a lekérdezéseket, beleértve a betűérzékenységet és egyéb keresési viselkedéseket.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### 3. lépés: kis‑ és nagybetű érzékeny szöveges lekérdezés végrehajtása
A `SearchQuery` felépíti a lekérdezésobjektumot, amelyet a motor az index ellen értékel ki.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

A ciklus kiírja minden olyan dokumentum teljes elérési útját, amely pontosan a betűérzékeny kifejezést tartalmazza.

## Hogyan hozzunk létre kereshető indexet Java – objektum lekérdezés keresés

### 1. lépés: második index inicializálása (opcionális)
Egy második `Index` példány létrehozható, hogy elkülönítse az objektumalapú kereséseket a sima szöveges keresésektől.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### 2. lépés: a kis‑ és nagybetű érzékeny opció újrahasználata
A `SearchOptions` újra felhasználható különböző lekérdezéstípusok között, hogy egységes betűkezelést biztosítson.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### 3. lépés: objektum lekérdezés felépítése és futtatása
A `WordQuery` egy szószintű keresést képvisel, amely más lekérdezéstípusokkal kombinálható összetett keresésekhez.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

A `createWordQuery` használatával később kombinálhatja azt kifejezés, helyettesítő karakter vagy Boolean lekérdezésekkel összetettebb forgatókönyvekhez.

## Gyakorlati alkalmazások
- **Jogi dokumentumkezelés:** Olyan eset‑specifikus jogszabályok lekérdezése, ahol a nagybetűhasználat számít.  
- **E‑kereskedelmi platformok:** Termékszámok (SKU‑k) megkülönböztetése, például „PRO‑X” vs. „pro‑x”.  
- **Tartalomkezelő rendszerek (CMS):** Biztosítja, hogy a szerzők pontosan megtalálják a címeket vagy címkéket.

## Teljesítmény szempontok
- **Az index naprakészen tartása** – új fájlok hozzáadásakor vagy meglévők módosításakor újraindexeljen.  
- **Memóriahasználat monitorozása** – nagy korpuszok esetén előnyös az inkrementális indexelés és a megfelelő JVM heap méretezés.  
- **A Java szemétgyűjtőjének kihasználása** – szabadítsa fel az `Index` objektumokat, ha már nincs rájuk szükség.

## Gyakori problémák és megoldások
| Probléma | Megoldás |
|----------|----------|
| `useCaseSensitiveSearch` figyelmen kívül marad | Ellenőrizze, hogy a legújabb GroupDocs.Search verziót használja, és hogy az opció módosítása után újraépítette-e az indexet. |
| Nem ad vissza eredményt egy ismert kifejezésre | Győződjön meg róla, hogy a kifejezés betűesete pontosan egyezik, és hogy a dokumentum sikeresen hozzá lett adva az indexhez. |
| Sok mappa keresése lelassul | Adja hozzá minden mappát egyenként a `index.add()`‑val, és fontolja meg az index szétbontását shard‑okra nagyon nagy adathalmazok esetén. |

## Gyakran feltett kérdések

**Q:** Hogyan kezeljem a nagy adatállományokat a GroupDocs.Search‑szal?  
**A:** Használjon indexparticionálást, finomhangolja a JVM memóriabeállításokat, és időnként tömörítse az indexet a teljesítmény optimális szinten tartásához.

**Q:** Kereshetek több könyvtárban egyszerre?  
**A:** Igen – hívja meg az `index.add()`‑t minden könyvtárhoz, amelyet fel szeretne venni, majd futtasson egyetlen lekérdezést a kombinált indexen.

**Q:** Mik a gyakori buktatók a kis‑ és nagybetű érzékeny keresés beállításakor?  
**A:** Az index újraépítésének elhagyása a `useCaseSensitiveSearch` engedélyezése után, vagy a helytelen betűeset használata a lekérdezésben.

**Q:** Hogyan hibaelháríthatom a keresési hibákat?  
**A:** Ellenőrizze a GroupDocs.Search által generált naplófájlokat a stack trace‑ekért, és győződjön meg arról, hogy minden Maven‑függőség helyesen fel van oldva.

**Q:** Alkalmas a GroupDocs.Search valós‑idő alkalmazásokhoz?  
**A:** Megfelelő indexelési stratégiákkal (inkrementális frissítések és memóriában tárolt gyorsítótár) közel‑valós‑idő keresési eredményeket képes biztosítani.

## Források
- **Dokumentáció:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **API referencia:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Letöltés:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **GitHub tároló:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Támogatási fórum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Ideiglenes licenc:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Legutóbb frissítve:** 2026-08-10  
**Tesztelve a következővel:** GroupDocs.Search 25.4  
**Szerző:** GroupDocs  

## Kapcsolódó oktatóanyagok

- [Create Search Index Java – GroupDocs.Search Tutorials](/search/java/indexing/)
- [How to Add Documents to Index with GroupDocs.Search for Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [How to add documents to index with Metadata Indexing in Java using GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)