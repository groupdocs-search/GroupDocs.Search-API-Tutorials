---
date: '2026-03-01'
description: Tanulja meg, hogyan optimalizálja a keresési teljesítményt és javítsa
  a keresési késleltetést a GroupDocs.Search for Java fejlett indexelési funkcióinak
  használatával, beleértve a leállítást, az aszinkron műveleteket, a több szálas feldolgozást
  és a metaadatok testreszabását.
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: A keresési teljesítmény optimalizálása fejlett indexelési technikákkal a GroupDocs.Search
  for Java‑ban
type: docs
url: /hu/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Optimalizálja a keresési teljesítményt fejlett indexelési technikákkal a GroupDocs.Search for Java-ban

A mai gyors tempójú digitális környezetben a **keresési teljesítmény optimalizálása** elengedhetetlen a felhasználók azonnali eredményeinek biztosításához. Akár egy egyedi keresőmotort épít, akár egy meglévő dokumentumkezelő rendszert fejleszt, a megfelelő indexelési stratégia drámaian csökkentheti a késleltetést, csökkentheti az erőforrás-felhasználást, és **javíthatja a keresési késleltetést** minden szinten. Ebben az útmutatóban a GroupDocs.Search for Java legfontosabb funkcióit mutatjuk be – megszakítás, aszinkron indexelés, több szálas feldolgozás és metaadat testreszabás – hogy **dokumentumok indexelését** gyorsabban és hatékonyabban végezhesse.

**Mit fog megtanulni**

- Hogyan lehet megszakítani egy indexelési műveletet egy meghatározott idő után  
- Aszinkron indexelési műveletek végrehajtása és az állapotváltozások kezelése  
- Több szálas konfigurálása a gyorsabb indexeléshez  
- Metaadat indexelési beállítások testreszabása  

Győződjön meg róla, hogy minden szükséges eszköz megvan, mielőtt a kódba merülünk.

## Prerequisites

- **GroupDocs.Search Library** – 25.4 vagy újabb verzió.  
- **Java Development Environment** – JDK 8 vagy újabb ajánlott.  
- Alapvető ismeretek a Java nyelvről és az indexelés koncepciójáról.

### Setting Up GroupDocs.Search for Java

#### Maven Installation

Add the repository and dependency to your `pom.xml` file:

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

#### Direct Download

Alternatively, download the latest JAR from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**License Acquisition** – Kezdje egy ingyenes próbaverzióval, vagy kérjen ideiglenes licencet a teljes funkciók eléréséhez.

### Basic Initialization and Setup

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

## Quick Answers
- **Mi a megszakítás funkciója?** Leállítja az indexelést egy beállított idő után, hogy felszabadítsa az erőforrásokat.  
- **Indexelhetek dokumentumokat aszinkron módon?** Igen – állítsa be a `options.setAsync(true)` értéket.  
- **Hány szálat használhatok?** Bármely pozitív egész szám; a tipikus érték 2‑4 a legtöbb szerveren.  
- **A metaadat indexelés opcionális?** Teljesen – engedélyezheti vagy finomhangolhatja mezőnként.  
- **Szükségem van licencre ezekhez a funkciókhoz?** A próba verzió tesztelésre elegendő; a teljes licenc a termeléshez kötelező.

## What Is “Optimize Search Performance” in This Context?

A keresési teljesítmény optimalizálása azt jelenti, hogy az indexelési folyamatot úgy konfiguráljuk, hogy a megfelelő mennyiségű CPU-t, memóriát és időt használja, miközben azonnal a legrelevánsabb eredményeket szolgáltatja. A megszakítás, az aszinkron végrehajtás, a szálkezelés és a metaadatok kezelése szabályozásával közvetlenül befolyásolhatja, milyen gyorsan képes a motor **dokumentumok indexelését** végrehajtani és a lekérdezésekre válaszolni.

## Why Use Advanced Indexing Features?

- **Csökkentett késleltetés** – Az aszinkron és több szálas indexelés az alkalmazást válaszkésznek tartja.  
- **Jobb erőforrás-kezelés** – A megszakítás megakadályozza a szabadon futó folyamatokat.  
- **Testreszabott keresési relevancia** – A metaadat beállítások lehetővé teszik a legfontosabb információk kiemelését.  

## How to improve search latency with advanced indexing?

Amikor **javítania kell a keresési késleltetést**, fontolja meg a bemutatott funkciók kombinálását: szakítsa meg a hosszú futású feladatokat, futtassa az indexelést a háttérben, és ossza szét a munkát több CPU mag között. Ez a többirányú megközelítés gyakran a legnagyobb sebességnyereséget hozza.

## Implementation Guide

### Cancellation Property

**Overview** – Cancel indexing after a specified duration to avoid over‑consumption of resources.

#### Step 1: Set Up the Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Create Indexing Options with Cancellation

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

**Key Points**

- `setCancellation()` aktiválja a funkciót.  
- `cancelAfter(int milliseconds)` határozza meg a timeout-ot (ebben a példában 3 másodperc).

### Asynchronous Property

**Overview** – Run indexing on a background thread and listen for status changes.

#### Step 1: Set Up the Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Subscribe to Status Changed Event

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

#### Step 3: Configure Asynchronous Options

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Threads Property

**Overview** – Speed up indexing by leveraging multiple CPU cores.

#### Step 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Configure Multi‑threading

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Metadata Indexing Options Property

**Overview** – Fine‑tune which document metadata gets indexed and how it’s stored.

#### Step 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Configure Metadata Options

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

## Practical Applications

1. **Dokumentumkezelő rendszerek** – Használjon aszinkron indexelést, hogy a felhasználói felület válaszkész maradjon, miközben nagy kötegeket dolgoz fel a háttérben.  
2. **Tartalomkereső motorok** – Alkalmazzon megszakítást, hogy a hosszú futású feladatok ne terheljék a szerver erőforrásait csúcsforgalom alatt.  
3. **Nagy léptékű befogadó csővezetékek** – Használjon több szálas feldolgozást a **dokumentumok indexelésének** nagy mennyiségben történő hozzáadásához, drámai módon csökkentve a feldolgozási időt.

## Performance Considerations

- **Szálkezelés** – Figyelje a CPU használatot; túl sok szál kontextusváltási terhet okozhat.  
- **Memóriahasználat** – A metaadat korlátok (pl. `setMaxBytesToIndexField`) segítenek a memóriahasználat előre jelezhetővé tételében.  
- **Garbage Collection** – Használjon megfelelő JVM zászlókat (`-Xmx`, `-XX:+UseG1GC`) nagy mennyiségű korpusz indexelésekor.

## Common Issues and Solutions

| Tünet | Valószínű ok | Megoldás |
|-------|--------------|----------|
| Az indexelés soha nem fejeződik be | Cancellation set too low | Növelje a `cancelAfter` értékét, vagy távolítsa el a megszakítást hosszú feladatoknál |
| No status updates in async mode | Event handler not attached correctly | Győződjön meg róla, hogy a `index.getEvents().StatusChanged.add(...)` hívás a `index.add` előtt történik |
| Out‑of‑memory errors | Too many threads or high metadata limits | Csökkentse a `options.setThreads` értékét, és alacsonyabb metaadatmező‑korlátokat állítson be |
| Missing metadata in results | Metadata indexing disabled | Ellenőrizze, hogy a `options.getMetadataIndexingOptions()` megfelelően konfigurált, és nem állították be a mezők figyelmen kívül hagyását |

## Frequently Asked Questions

**Q: Hogyan szerezhetek ideiglenes licencet a GroupDocs.Search-hez?**  
A: Látogassa meg a [GroupDocs ideiglenes licenc oldalát](https://purchase.groupdocs.com/temporary-license/).

**Q: Megszakíthatok egy indexelési műveletet közben?**  
A: Igen – használja a megszakítási tulajdonságot a `cancelAfter()`‑val, vagy hívja meg programozottan a `Cancellation.cancel()`‑t.

**Q: Milyen felhasználási esetek vannak az aszinkron indexelésre?**  
A: Valós idejű dokumentumlekérdezés, háttérben futó kötegelt feldolgozás és UI‑válaszkész alkalmazások profitálnak az aszinkron indexelésből.

**Q: Biztonságos-e növelni a szálak számát megosztott szerveren?**  
A: Növelje fokozatosan, és figyelje a CPU terhelést; erősen megosztott környezetben tartsa a szálak számát mérsékelt szinten (2‑4).

**Q: Hogyan befolyásolja a metaadat indexelés a keresési relevanciát?**  
A: A megfelelően indexelt metaadatok (szerző, létrehozás dátuma, címkék) nagyobb súlyt kaphatnak a lekérdezésekben, ezáltal javítva az eredmények pontosságát.

## Conclusion

Azáltal, hogy ezeket a fejlett funkciókat alkalmazza a GroupDocs.Search for Java-ban, **optimalizálni fogja a keresési teljesítményt** különféle szituációkban – a gyors dokumentumbefogadástól a finomhangolt metaadatkezelésig. Kísérletezzen különböző konfigurációkkal, figyelje az erőforrás-felhasználást, és szabja testre a beállításokat a saját munkaterheléséhez, hogy a legjobb eredményeket érje el.

---

**Last Updated:** 2026-03-01  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs