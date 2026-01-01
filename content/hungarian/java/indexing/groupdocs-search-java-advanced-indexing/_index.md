---
date: '2025-12-29'
description: Tanulja meg, hogyan optimalizálhatja a keresési teljesítményt a GroupDocs.Search
  for Java fejlett indexelési funkcióinak használatával, beleértve a leállítást, az
  aszinkron műveleteket, a több szálú feldolgozást és a metaadat testreszabását.
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: Keresési teljesítmény optimalizálása fejlett indexelési technikákkal a GroupDocs.Search
  for Java-ban
type: docs
url: /hu/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Keresési teljesítmény optimalizálása fejlett indexelési technikákkal a GroupDocs.Search for Java-ban

A mai gyors tempójú digitális környezetben a **keresési teljesítmény optimalizálása** elengedhetetlen a felhasználók számára azonnali eredmények biztosításához. Akár egy egyedi keresőmotort építesz, akár egy meglévő dokumentumkezelő rendszert fejlesztesz, a megfelelő indexelési stratégia drámaian csökkentheti a késleltetést és az erőforrás-felhasználást. Ebben az útmutatóban a GroupDocs.Search for Java legfontosabb funkcióit—annulálás, aszinkron indexelés, több szálas feldolgozás és metaadat testreszabás—végigvezetjük, hogy **add documents index** gyorsabban és hatékonyabban tudj.

**Mit fogsz megtanulni**

- Hogyan lehet egy indexelési műveletet egy megadott idő után leállítani
- Aszinkron indexelési műveletek végrehajtása és az állapotváltozások kezelése
- Többszálas konfigurálása a gyorsabb indexeléshez
- Metaadat indexelési beállítások testreszabása

Győződj meg róla, hogy minden szükséges eszközöd megvan, mielőtt a kódba merülnénk.

## Előfeltételek

- **GroupDocs.Search Library** – 25.4 vagy újabb verzió.  
- **Java Development Environment** – JDK 8 vagy újabb ajánlott.  
- Alapvető ismeretek a Java-val és az indexelés koncepciójával kapcsolatban.

### A GroupDocs.Search for Java beállítása

#### Maven telepítés

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

#### Közvetlen letöltés

Alternatívaként töltsd le a legújabb JAR-t a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

**License Acquisition** – Kezd egy ingyenes próbaverzióval, vagy kérj ideiglenes licencet a teljes funkciókészlet feloldásához.

### Alapvető inicializálás és beállítás

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

## Gyors válaszok

- **Mi a leállítás funkciója?** Leállítja az indexelést egy beállított idő után, hogy felszabadítsa az erőforrásokat.  
- **Indexelhetek dokumentumokat aszinkron módon?** Igen – állítsd be a `options.setAsync(true)` értéket.  
- **Hány szálat használhatok?** Bármely pozitív egész szám; a legtöbb szerveren a tipikus érték 2‑4.  
- **A metaadat indexelés opcionális?** Teljesen – engedélyezheted vagy finomhangolhatod mezőnként.  
- **Szükségem van licencre ezekhez a funkciókhoz?** A próba verzió teszteléshez megfelelő; a termeléshez teljes licenc szükséges.

## Mit jelent a „Keresési teljesítmény optimalizálása” ebben a kontextusban?

A keresési teljesítmény optimalizálása azt jelenti, hogy az indexelési folyamatot úgy konfiguráljuk, hogy a megfelelő mennyiségű CPU-t, memóriát és időt használja, miközben azonnal a legrelevánsabb eredményeket szolgáltatja. A leállítás, az aszinkron végrehajtás, a szálkezelés és a metaadatok kezelése szabályozásával közvetlenül befolyásolod, milyen gyorsan tudja a motor **add documents index** és válaszolni a lekérdezésekre.

## Miért használjunk fejlett indexelési funkciókat?

- **Csökkentett késleltetés** – Az aszinkron és több szálas indexelés az alkalmazásod válaszkész maradását biztosítja.  
- **Jobb erőforrás-kezelés** – A leállítás megakadályozza a szabadon futó folyamatokat.  
- **Testreszabott keresési relevancia** – A metaadat beállítások lehetővé teszik a legfontosabb információk kiemelését.  

## Implementációs útmutató

### Annulálás tulajdonság

**Áttekintés** – Az indexelés leállítása egy megadott időtartam után, hogy elkerüld az erőforrások túlzott fogyasztását.

#### 1. lépés: A környezet beállítása

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2. lépés: Indexelési beállítások létrehozása leállítással

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
- `cancelAfter(int milliseconds)` meghatározza a timeout-ot (ebben a példában 3 másodperc).

### Aszinkron tulajdonság

**Áttekintés** – Az indexelés futtatása háttérszálon, és a státuszváltozások figyelése.

#### 1. lépés: A környezet beállítása

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2. lépés: Eseménykezelő feliratkozása a státuszváltozásra

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

#### 3. lépés: Aszinkron beállítások konfigurálása

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Szálak tulajdonság

**Áttekintés** – Az indexelés felgyorsítása több CPU mag kihasználásával.

#### 1. lépés: A környezet beállítása

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2. lépés: Többszálas konfigurálása

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Metaadat indexelési beállítások tulajdonság

**Áttekintés** – Finomhangolni, hogy mely dokumentum metaadatok kerülnek indexelésre és hogyan tárolódnak.

#### 1. lépés: A környezet beállítása

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2. lépés: Metaadat beállítások konfigurálása

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

1. **Dokumentumkezelő rendszerek** – Aszinkron indexelés használata a felhasználói felület válaszkészségének megőrzéséhez, miközben nagy kötegek a háttérben kerülnek feldolgozásra.  
2. **Tartalomkereső motorok** – Leállítás alkalmazása, hogy a hosszú futású feladatok ne terheljék a szerver erőforrásait a csúcsforgalom során.  
3. **Nagy léptékű ingestiós csővezetékek** – Többszálas feldolgozás kihasználása a **add documents index** nagy méretekben, ami drámai módon csökkenti a feldolgozási időt.  

## Teljesítmény szempontok

- **Szálkezelés** – Figyeld a CPU használatát; a túl sok szál kontextusváltási terhet okozhat.  
- **Memória lábnyoma** – A metaadat korlátok (pl. `setMaxBytesToIndexField`) segítenek a memóriahasználat kiszámíthatóvá tételében.  
- **Garbage Collection** – Használj megfelelő JVM flag-eket (`-Xmx`, `-XX:+UseG1GC`) hatalmas korpuszok indexelésekor.  

## Gyakori problémák és megoldások

| Tünet | Valószínű ok | Megoldás |
|-------|--------------|----------|
| Az indexelés soha nem fejeződik be | A leállítás túl alacsonyra van állítva | `cancelAfter` érték növelése vagy a leállítás eltávolítása hosszú feladatoknál |
| Nincs státuszfrissítés aszinkron módban | Az eseménykezelő nincs megfelelően csatolva | Győződj meg róla, hogy a `index.getEvents().StatusChanged.add(...)` hívás megtörténik a `index.add` előtt |
| Memóriahiányos hibák | Túl sok szál vagy magas metaadat korlátok | `options.setThreads` csökkentése és a metaadat mezőkorlátok alacsonyabbra állítása |
| Hiányzó metaadatok az eredményekben | A metaadat indexelés le van tiltva | Ellenőrizd, hogy a `options.getMetadataIndexingOptions()` konfigurálva van, és nem állították be a mezők figyelmen kívül hagyására |

## Gyakran ismételt kérdések

**K: Hogyan szerezhetek ideiglenes licencet a GroupDocs.Search-hez?**  
A: Látogasd meg a [GroupDocs ideiglenes licenc oldalát](https://purchase.groupdocs.com/temporary-license/).

**K: Leállíthatok egy indexelési műveletet közben?**  
A: Igen – használd a leállítási tulajdonságot a `cancelAfter()`-val, vagy programozottan hívd a `Cancellation.cancel()`-t.

**K: Milyen felhasználási esetek vannak az aszinkron indexelésre?**  
A: A valós‑idő dokumentum lekérdezés, a háttérben futó kötegelt feldolgozás és a UI‑válaszkész alkalmazások profitálnak az aszinkron indexelésből.

**K: Biztonságos a szálak számát növelni egy megosztott szerveren?**  
A: Növeld fokozatosan és figyeld a CPU terhelést; erősen megosztott környezetben tartsd a szálak számát mérsékelt szinten (2‑4).

**K: Hogyan befolyásolja a metaadat indexelés a keresési relevanciát?**  
A: A megfelelően indexelt metaadatok (szerző, létrehozás dátuma, címkék) magasabb súlyt kaphatnak a lekérdezésekben, ezáltal javítva az eredmények pontosságát.

## Következtetés

A GroupDocs.Search for Java fejlett funkcióinak alkalmazásával **optimalizálni fogod a keresési teljesítményt** különféle helyzetekben – a gyors dokumentumfelvételtől a finomhangolt metaadat-vezérlésig. Kísérletezz különböző konfigurációkkal, figyeld az erőforrás-használatot, és a beállításokat a saját munkaterhelésedhez igazítsd a legjobb eredmények eléréséhez.

---

**Utolsó frissítés:** 2025-12-29  
**Tesztelve ezzel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs