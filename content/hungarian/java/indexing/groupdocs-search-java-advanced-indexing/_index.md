---
date: '2026-08-15'
description: Ismerje meg, hogyan javíthatja a keresési késleltetést a GroupDocs.Search
  for Java fejlett indexelési funkcióinak használatával, beleértve a cancellation,
  async operations, multithreading és metadata customization funkciókat.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: Javítsa a keresési késleltetést a GroupDocs.Search for Java használatával,
  a cancellation, asynchronous indexing, multithreading és metadata customization
  alkalmazásával. Boost performance and reduce resource use.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: A keresési késleltetés javítása fejlett indexeléssel a GroupDocs-ban
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: A keresési késleltetés javítása fejlett indexeléssel a GroupDocs-ban
type: docs
url: /hu/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# A keresési késleltetés javítása fejlett indexeléssel a GroupDocs-ban

A mai gyors tempójú digitális környezetben a **search latency javítása** elengedhetetlen a felhasználók számára azonnali eredmények biztosításához. Akár egy egyedi keresőmotort építesz, akár egy meglévő dokumentumkezelő rendszert fejlesztesz, a megfelelő indexelési stratégia drámaian csökkentheti a késleltetést, alacsonyabb erőforrás-felhasználást eredményez, és **search latency javítja** minden szinten. Ebben az útmutatóban áttekintjük a GroupDocs.Search for Java legfontosabb funkcióit – leállítás, aszinkron indexelés, több szálas feldolgozás és metaadat testreszabás – hogy **dokumentumok hozzáadása az indexhez** gyorsabban és hatékonyabban tudj.

**Mit fogsz megtanulni**

- Hogyan lehet leállítani egy indexelési műveletet egy meghatározott idő után
- Aszinkron indexelési műveletek végrehajtása és az állapotváltozások kezelése
- Többszálas feldolgozás beállítása a gyorsabb indexeléshez
- Metaadat indexelési beállítások testreszabása a **search metadata testreszabásához**

Győződjünk meg róla, hogy minden szükséges dolog megvan, mielőtt a kódba merülünk.

## Gyors válaszok
- **Mi a leállítás funkciója?** Leállítja az indexelést egy beállított időkorlát után, felszabadítva a CPU-t és a memóriát más feladatok számára.  
- **Indexelhetek dokumentumokat aszinkron módon?** Igen – engedélyezheted a `options.setAsync(true)` segítségével.  
- **Hány szálat használhatok?** Bármely pozitív egész szám; 2‑4 szál a tipikus a legtöbb szerveren.  
- **A metaadat indexelés opcionális?** Teljesen – engedélyezheted vagy finomhangolhatod mezőnként.  
- **Szükségem van licencre ezekhez a funkciókhoz?** A próba verzió teszteléshez működik; a teljes licenc szükséges a termeléshez.

## Előkövetelmények

- **GroupDocs.Search library** – 25.4 vagy újabb verzió.  
- **Java Development Environment** – JDK 8 vagy újabb ajánlott.  
- Alapvető ismeretek a Java-val és az indexelés koncepciójával.

### A GroupDocs.Search beállítása Java-hoz

#### Maven telepítés

Add the repository and dependency to your `pom.xml` file:

`pom.xml` konfiguráció megmondja a Mavennek, hogy mely GroupDocs.Search artefaktumokat töltse le és vegye bele a projektbe.

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

#### Közvetlen letöltés

Alternatívaként töltsd le a legújabb JAR-t a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

**License acquisition** – Kezd egy ingyenes próba verzióval vagy kérj ideiglenes licencet a teljes funkciók eléréséhez.

### Alapvető inicializálás és beállítás

A `SearchIndex` osztály a belépési pont, amely egy kereshető indexet képvisel, amely lemezen vagy memóriában tárolódik.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## Mi az a „search teljesítmény optimalizálása” ebben a kontextusban?

A search teljesítmény optimalizálása azt jelenti, hogy az indexelési folyamatot úgy konfiguráljuk, hogy a megfelelő mennyiségű CPU-t, memóriát és időt használja, miközben azonnal a legrelevánsabb eredményeket szolgáltatja. A leállítás, aszinkron végrehajtás, szálkezelés és metaadatkezelés szabályozásával közvetlenül befolyásolod, milyen gyorsan tudja a motor **dokumentumok hozzáadása az indexhez** és válaszolni a lekérdezésekre.

## Miért használjunk fejlett indexelési funkciókat?

Az aszinkron és több szálas indexelés fenntartja az alkalmazásod válaszkészségét, míg a leállítás megakadályozza a szabadon futó folyamatokat. A finomhangolt metaadat beállítások lehetővé teszik a legfontosabb információk kiemelését, ami közvetlenül **search latency javítja** a végfelhasználók számára. Emellett ezek a funkciók csökkentik a CPU csúcsokat, mérséklik a memória terhelést, és simább skálázást tesznek lehetővé nagy mennyiségű dokumentum kezelésekor.

## Hogyan javítsuk a search latency-t fejlett indexeléssel?

Töltsd be a `SearchIndex` példányodat, konfiguráld a `IndexingOptions`-t leállítással, aszinkronnal és szálbeállításokkal, majd hívd meg a `index.add(document)`‑t – ez a kombináció akár 60 %-kal is csökkenti az általános indexelési időt tipikus terheléseknél, és garantálja, hogy a hosszú futású feladatok ne blokkolják a többi műveletet. Emellett módosíthatod a metaadat indexelési korlátokat, és nyomon követheted a haladást a status‑changed eseményeken keresztül, hogy a folyamat a teljesítménykereteken belül maradjon.

## Implementációs útmutató

### Leállítás tulajdonság

**Áttekintés** – Leállítja az indexelést egy meghatározott időtartam után, hogy elkerülje az erőforrások túlzott fogyasztását.

#### 1. lépés: a környezet beállítása

Hozz létre egy `SearchIndex` példányt, amely a saját index mappádra mutat.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2. lépés: indexelési beállítások létrehozása leállítással

`IndexingOptions` lehetővé teszi, hogy meghatározd, hogyan viselkedjen az indexelő motor.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Kulcspontok**

- `setCancellation()` aktiválja a funkciót.  
- `cancelAfter(int milliseconds)` definiálja az időkorlátot (ebben a példában 3 másodperc).

### Aszinkron tulajdonság

**Áttekintés** – Az indexelést háttérszálon futtatja, és figyeli az állapotváltozásokat.

#### 1. lépés: a környezet beállítása

Példányosítsd az indexet és készítsd elő a dokumentumgyűjteményt.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2. lépés: feliratkozás a status‑changed eseményre

A `StatusChanged` esemény értesít, amikor az indexelési feladat állapotot vált.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### 3. lépés: aszinkron beállítások konfigurálása

Engedélyezd az async módot, hogy a hívás azonnal visszatérjen, és a feldolgozás a háttérben folytatódjon.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Szálak tulajdonság

**Áttekintés** – Az indexelés felgyorsítása több CPU mag kihasználásával.

#### 1. lépés: környezet beállítása

Készítsd elő az indexet, és győződj meg róla, hogy a JVM-nek elegendő heap memóriája van.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2. lépés: több szálas feldolgozás beállítása

Állítsd be a munkaszálak számát; minden szál egy dokumentum részhalmazt dolgoz fel.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Metaadat indexelési opciók tulajdonság

**Áttekintés** – Finomhangolja, hogy mely dokumentum metaadatok kerülnek indexelésre és hogyan tárolódnak.

#### 1. lépés: környezet beállítása

Tölts be egy dokumentumot, amely metaadat mezőket tartalmaz, például szerző, cím és egyedi címkék.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2. lépés: metaadat opciók konfigurálása

`MetadataIndexingOptions` lehetővé teszi, hogy engedélyezd vagy letiltsd az egyes metaadat mezőket, és meghatározd a méretkorlátokat.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Gyakorlati alkalmazások

1. **Document management systems** – Használd az aszinkron indexelést, hogy a UI válaszkész maradjon, miközben nagy kötegek a háttérben kerülnek feldolgozásra.  
2. **Content search engines** – Alkalmazd a leállítást, hogy megakadályozd a hosszú futású feladatok erőforrás-elfogyasztását a csúcsforgalom alatt.  
3. **Large‑scale ingestion pipelines** – Használd a több szálas feldolgozást a **dokumentumok hozzáadása az indexhez** nagy léptékben, drámai módon csökkentve a feldolgozási időt.

## Teljesítmény szempontok

- **Thread management** – Figyeld a CPU használatot; túl sok szál kontextusváltási terhet okozhat.  
- **Memory footprint** – A metaadat korlátok (pl. `setMaxBytesToIndexField`) előre láthatóvá teszik a memóriahasználatot.  
- **Garbage collection** – Használj megfelelő JVM flag-eket (`-Xmx`, `-XX:+UseG1GC`) nagy mennyiségű korpusz indexelésekor.

## Gyakori problémák és megoldások

| Szimbólum | Valószínű ok | Megoldás |
|-----------|--------------|----------|
| Az indexelés soha nem fejeződik be | A leállítás túl alacsonyra van állítva | `cancelAfter` érték növelése vagy a leállítás eltávolítása hosszú feladatoknál |
| Nincsenek állapotfrissítések async módban | Az eseménykezelő nincs megfelelően csatolva | Győződj meg róla, hogy a `index.getEvents().StatusChanged.add(...)` hívás az `index.add` előtt történik |
| Memóriahiányos hibák | Túl sok szál vagy magas metaadatkorlátok | `options.setThreads` csökkentése és a metaadatmezők korlátjainak csökkentése |
| Hiányzó metaadatok az eredményekben | A metaadat indexelés le van tiltva | Ellenőrizd, hogy a `options.getMetadataIndexingOptions()` konfigurálva van, és nem állították be a mezők figyelmen kívül hagyására |

## Gyakran ismételt kérdések

**Q: Hogyan szerezhetek ideiglenes licencet a GroupDocs.Search-hez?**  
A: Látogasd meg a [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) oldalt, és kövesd a képernyőn megjelenő utasításokat.

**Q: Leállíthatok egy indexelési műveletet közben?**  
A: Igen – használd a leállítás tulajdonságot a `cancelAfter()`-val, vagy programozottan hívd meg a `Cancellation.cancel()`-t.

**Q: Milyen felhasználási esetek vannak az aszinkron indexelésre?**  
A: Valós idejű dokumentumlekérdezés, háttérben futó kötegelt feldolgozás, és UI‑válaszkész alkalmazások profitálnak az async indexelésből.

**Q: Biztonságos a szálak számának növelése megosztott szerveren?**  
A: Növeld fokozatosan és figyeld a CPU terhelést; erősen megosztott környezetben tartsd a szálak számát mérsékelt szinten (2‑4).

**Q: Hogyan befolyásolja a metaadat indexelés a keresési relevanciát?**  
A: A megfelelően indexelt metaadatok (szerző, létrehozás dátuma, címkék) magasabb súlyt kaphatnak a lekérdezésekben, ezáltal javítva az eredmények pontosságát.

## Következtetés

Ezeknek a fejlett GroupDocs.Search for Java funkcióknak a kihasználásával **search latency javítod** különféle helyzetekben – a gyors dokumentumfelvételtől a finomhangolt metaadatvezérlésig. Kísérletezz különböző konfigurációkkal, figyeld az erőforrás-használatot, és igazítsd a beállításokat a saját munkaterhelésedhez a legjobb eredmények eléréséhez.

---

**Legutóbb frissítve:** 2026-08-15  
**Tesztelve a következővel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [Kérdezési teljesítmény javítása a GroupDocs.Search Java-val: Index és keresés optimalizálása](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Hogyan adjunk dokumentumokat az indexhez metaadat indexeléssel Java-ban a GroupDocs.Search használatával](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Hogyan adjunk hozzá több alias-t és dokumentumot az indexhez a GroupDocs.Search for Java-ban](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)