---
date: '2026-05-02'
description: Ismerje meg, hogyan konfigurálja a keresést és engedélyezze a valós idejű
  keresési frissítéseket a GroupDocs.Search for Java használatával. Lépésről‑lépésre
  útmutató a hálózati beállításhoz, a csomópont telepítéséhez és az indexeléshez.
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: Hogyan konfiguráljuk a keresést a GroupDocs.Search használatával Java-ban –
  Konfigurációs és telepítési útmutató
type: docs
url: /hu/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# Hogyan konfiguráljuk a keresést a GroupDocs.Search használatával Java-ban

A mai gyorsan változó digitális világban a **hogyan konfiguráljuk a keresést** hatékonyan döntő lehet egy projekt sikerében. Akár több ezer szerződést, kutatási anyagot vagy belső jelentést kezel, egy jól megtervezett keresési hálózat lehetővé teszi a megfelelő dokumentum másodpercek alatt történő megtalálását. Ez az útmutató végigvezet a keresési hálózat konfigurálásán, a csomópontok telepítésén, és a **valós idejű keresési frissítések** engedélyezésén a GroupDocs.Search for Java segítségével.

## Gyors válaszok
- **Mi a keresési hálózat elsődleges célja?** A indexelés és lekérdezés feldolgozásának több csomópont között történő elosztása a skálázhatóság és a sebesség érdekében.  
- **Melyik könyvtárverzió szükséges?** GroupDocs.Search for Java v25.4 vagy újabb.  
- **Szükségem van licencre?** Az ingyenes próba a kiértékeléshez elegendő; a termeléshez kereskedelmi licenc szükséges.  
- **Hogyan kezelik a valós idejű frissítéseket?** Az indexelési változásokkor aktiválódó csomópont eseményekre feliratkozással.  
- **Hozzáadhatok új dokumentummappákat menet közben?** Igen — használja az indexelő `addDirectories` metódusát.

## Mi a “hogyan konfiguráljuk a keresést” a GroupDocs kontextusában?
A keresés konfigurálása egy **keresési hálózat** beállítását jelenti, amely tudja, hol találhatók a dokumentumok, hogyan kommunikálnak a csomópontok, és hogyan koordinálódik az indexelés. Ha a hálózat konfigurálva van, csomópontokat hozzáadhat vagy eltávolíthat leállás nélkül, biztosítva a folyamatos hozzáférést a naprakész keresési eredményekhez.

## Miért használjuk a GroupDocs.Search for Java-t?
- **Skálázhatóság:** A munkaterhek elosztása több gép között.  
- **Valós‑idejű frissítések:** Az újonnan indexelt fájlok azonnali tükrözése a hálózaton.  
- **Könnyű integráció:** Egyszerű Maven beállítás és tiszta Java API-k.  
- **Vállalati szintű:** Nagy korpuszok és összetett lekérdezési forgatókönyvek kezelése.

## Előfeltételek
- **Java Development Kit (JDK) 8+** telepítve.  
- **Maven** a függőségkezeléshez.  
- Alapvető ismeretek a Java, Maven és a keresési koncepciók terén.

## A GroupDocs.Search for Java beállítása

### Maven függőség
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

**Közvetlen letöltés:** A könyvtárat letöltheti a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc beszerzése
- **Ingyenes próba:** Szerezzen próbalisencet a funkciók kipróbálásához.  
- **Ideiglenes licenc:** Kérjen hosszabb kiértékelési időszakot.  
- **Kereskedelmi licenc:** A termelési környezethez szükséges.

### Alap inicializálás
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Hogyan konfiguráljuk a keresési hálózatot Java-ban

### 1. lépés: Szükséges csomagok importálása
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### 2. lépés: A hálózat konfigurálása
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Paraméterek:** `basePath` a dokumentum mappára mutat; `basePort` a csomópontok közötti TCP port.

## Keresési hálózati csomópontok telepítése

### 1. lépés: Telepítési csomag importálása
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### 2. lépés: Csomópontok telepítése
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Mester csomópont:** Koordinálja a kereséseket és az indexelést az összes csomópont között. A **mester csomópont** beállításait, például a shard kiosztást és az egészség ellenőrzéseket, konfigurálhatja.

## Feliratkozás a csomópont eseményekre a valós idejű keresési frissítésekhez

### 1. lépés: Esemény csomag importálása
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### 2. lépés: Feliratkozás a mester csomópont eseményeire
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Eseménykezelés:** Lehetővé teszi a **valós idejű keresési frissítéseket**, amikor dokumentumok hozzáadódnak, frissülnek vagy eltávolításra kerülnek.

## Könyvtárak hozzáadása az indexeléshez

### 1. lépés: Indexelő csomag importálása
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### 2. lépés: Dokumentum könyvtárak hozzáadása
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Dinamikus indexelés:** Használja az `addDirectories` metódust a **könyvtárak indexhez adásához** menet közben a hálózat újraindítása nélkül.

## Indexelt dokumentumok lekérése

### 1. lépés: Kereső csomag importálása
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### 2. lépés: Dokumentum információk lekérése
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **Shard kezelés:** Hatékonyan kezeli a nagy adathalmazokat a dokumentumok shard-ek közötti elosztásával. A **shard méret optimalizálásához** figyelje a shard statisztikákat, és a jövőbeni kiadásokban módosítsa a `shardSize` konfigurációt.

## Miért fontos ez a projektje számára
Egy megfelelően konfigurált keresési hálózat megszünteti a szűk keresztmetszeteket, csökkenti a késleltetést, és biztosítja, hogy a felhasználók mindig a dokumentum legújabb verzióját lássák. A valós‑idejű frissítések és a **könyvtárak indexhez adásának** lehetősége leállás nélkül különösen értékes jogi irodák, kutatóintézetek és minden olyan szervezet számára, amely folyamatosan változó dokumentumgyűjteményekkel dolgozik.

## Gyakorlati alkalmazások
1. **Vállalati dokumentumkezelés:** A keresés központosítása több millió fájl között.  
2. **Jogi irodák:** Gyorsan megtalálni az ügyiratokat, szerződéseket és bizonyítékokat.  
3. **Akademiai kutatás:** Folyóiratok és tanulmányok indexelése az azonnali lekérdezéshez.

## Teljesítmény szempontok
- **Indexelés optimalizálása:** Rendszeres index frissítések ütemezése és a régi adatok tisztítása.  
- **Memória kezelés:** Figyelje a JVM heap-et, különösen nagy shard-ek kezelésekor.  
- **Skálázhatósági tervezés:** Hozzáadjon csomópontokat a korpusz növekedésével; a hálózat automatikusan kiegyensúlyozza a terhelést.  
- **Shard méret optimalizálása:** A kisebb shard-ek javítják a lekérdezési késleltetést, míg a nagyobb shard-ek csökkentik a terhelést. Finomhangolja a hardver és a lekérdezési minták alapján.

## Gyakori problémák és megoldások
| Probléma | Ok | Megoldás |
|----------|----|----------|
| A csomópontok nem tudnak csatlakozni | Port ütközés vagy tűzfal | Győződjön meg róla, hogy a `basePort` nyitva van, és más szolgáltatások nem használják |
| Az index nem frissül | Esemény feliratkozás hiányzik | Hívja meg a `SearchNetworkNodeEvents.subscribe(masterNode)` metódust a telepítés után |
| Memóriahiányos hibák | Túl sok nagy shard betöltve | Csökkentse a shard méretét vagy növelje a JVM heap-et (`-Xmx` zászló) |

## Gyakran Ismételt Kérdések

**K: Hozzáadhatok új könyvtárakat a hálózat futása után?**  
V: Igen — használja a `indexer.addDirectories()` metódust; a feliratkozott események valós időben terjesztik a frissítéseket.

**K: Hogyan monitorozhatom a csomópont egészségét?**  
V: Minden `SearchNetworkNode` állapot API-kat biztosít; integrálja a kedvenc felügyeleti eszközével.

**K: Lehet a mester csomópontot külön gépen futtatni?**  
V: Természetesen. Csak győződjön meg róla, hogy minden csomópont ugyanazt a `basePort`-ot használja, és elérik egymást a hálózaton.

**K: Milyen fájlformátumok támogatottak?**  
V: A GroupDocs.Search támogatja a PDF-eket, Word, Excel, PowerPoint, egyszerű szöveget és sok más formátumot alapból.

**K: Új csomópont hozzáadása után újra kell indítani a hálózatot?**  
V: Nem — a csomópontok dinamikusan hozzáadhatók vagy eltávolíthatók; a mester csomópont automatikusan újraosztja a shard-eket.

## Összegzés
Most, hogy ismeri a **hogyan konfiguráljuk a keresést** a GroupDocs.Search for Java használatával, gyors, skálázható és megbízható dokumentumkereső megoldásokat építhet, amelyek lépést tartanak szervezete növekedésével. Alkalmazza ezeket a mintákat, hogy valós‑idejű, elosztott keresési élményeket hozzon létre bármely iparág számára.

---

**Utoljára frissítve:** 2026-05-02  
**Tesztelve a következővel:** GroupDocs.Search for Java 25.4  
**Szerző:** GroupDocs