---
date: '2026-01-08'
description: Tanulja meg, hogyan konfigurálja a keresést és engedélyezze a valós idejű
  keresési frissítéseket a GroupDocs.Search for Java használatával. Lépésről‑lépésre
  útmutató a hálózati beállításokról, a csomópont telepítéséről és az indexelésről.
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 'Hogyan konfiguráljuk a keresést a GroupDocs.Search használatával Java-ban:
  Konfigurációs és telepítési útmutató'
type: docs
url: /hu/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# Hogyan konfiguráljuk a keresést a GroupDocs.Search segítségével Java-ban

A mai gyorsan változó digitális világban a **keresés konfigurálásának** hatékony módja döntheti el egy projekt sikerét. Legyen szó több ezer szerződésről, kutatási anyagról vagy belső jelentésről, egy jól megtervezett keresési hálózat lehetővé teszi a megfelelő dokumentum másodpercek alatt történő megtalálását. Ez az útmutató végigvezet a keresési hálózat konfigurálásán, a csomópontok telepítésén és a **valós idejű keresési frissítések** engedélyezésén a GroupDocs.Search for Java segítségével.

## Gyors válaszok
- **Mi a keresési hálózat elsődleges célja?** Az indexelés és a lekérdezés feldolgozásának elosztása több csomópont között a skálázhatóság és a sebesség érdekében.  
- **Melyik könyvtárverzió szükséges?** GroupDocs.Search for Java v25.4 vagy újabb.  
- **Szükségem van licencre?** Az ingyenes próba verzió elegendő a kiértékeléshez; a gyártási környezethez kereskedelmi licenc szükséges.  
- **Hogyan kezelik a valós idejű frissítéseket?** Az indexelési változásokra aktiválódó csomópont eseményekre feliratkozással.  
- **Hozzáadhatok új dokumentum mappákat menet közben?** Igen – használja az indexelő `addDirectories` metódusát.

## Mi a “keresés konfigurálása” a GroupDocs kontextusában?
A keresés konfigurálása egy **keresési hálózat** beállítását jelenti, amely tudja, hol találhatók a dokumentumok, hogyan kommunikálnak a csomópontok, és hogyan koordinálódik az indexelés. A hálózat konfigurálása után csomópontokat adhat hozzá vagy távolíthat el leállás nélkül, biztosítva a folyamatos hozzáférést a naprakész keresési eredményekhez.

## Miért használjuk a GroupDocs.Search for Java-t?
- **Skálázhatóság:** A munkaterhelés elosztása több gép között.  
- **Valós‑idejű frissítések:** Az újonnan indexelt fájlok azonnali tükrözése a hálózaton.  
- **Könnyű integráció:** Egyszerű Maven beállítás és átlátható Java API-k.  
- **Vállalati szintű:** Nagy korpuszok és összetett lekérdezési forgatókönyvek kezelése.

## Előfeltételek
- **Java Development Kit (JDK) 8+** telepítve.  
- **Maven** a függőségek kezeléséhez.  
- Alapvető ismeretek a Java, Maven és a keresési koncepciók terén.  

## A GroupDocs.Search for Java beállítása

### Maven függőség
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

**Közvetlen letöltés:** A könyvtárat letöltheti a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc beszerzése
- **Ingyenes próba:** Szerezzen próbalisencet a funkciók kipróbálásához.  
- **Ideiglenes licenc:** Kérjen hosszabb kiértékelési időszakot.  
- **Kereskedelmi licenc:** Gyártási környezethez kötelező.

### Alapvető inicializálás
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
- **Paraméterek:** A `basePath` a dokumentum mappára mutat; a `basePort` a csomópontok közötti TCP port.

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
- **Mester csomópont:** Koordinálja a kereséseket és az indexelést az összes csomópont között.

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

## Mappák hozzáadása az indexeléshez

### 1. lépés: Indexelő csomag importálása
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### 2. lépés: Dokumentum mappák hozzáadása
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Dinamikus indexelés:** Tetszőleges számú mappát adhat hozzá; a hálózat automatikusan indexeli őket.

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
- **Shard kezelés:** Hatékonyan kezeli a nagy adathalmazokat a dokumentumok shard-okra való elosztásával.

## Gyakorlati alkalmazások
1. **Vállalati dokumentumkezelés:** Központosítja a keresést milliók fájljain.  
2. **Jogász irodák:** Gyorsan megtalálja az ügyiratokat, szerződéseket és bizonyítékokat.  
3. **Akademiai kutatás:** Indexeli a folyóiratokat és dolgozatokat az azonnali lekéréshez.

## Teljesítmény szempontok
- **Indexelés optimalizálása:** Rendszeres index frissítések ütemezése és a régi adatok törlése.  
- **Memória kezelés:** Figyelje a JVM heap-et, különösen nagy shard-ok kezelésekor.  
- **Skálázhatóság tervezése:** Növelje a csomópontok számát a korpusz növekedésével; a hálózat automatikusan kiegyensúlyozza a terhelést.

## Gyakori problémák és megoldások
| Probléma | Ok | Megoldás |
|----------|----|----------|
| Csomópontok nem tudnak csatlakozni | Port ütközés vagy tűzfal | Győződjön meg róla, hogy a `basePort` nyitva van és nem használja más szolgáltatás |
| Az index nem frissül | Esemény feliratkozás hiányzik | Hívja meg a `SearchNetworkNodeEvents.subscribe(masterNode)`-t a telepítés után |
| Memóriahiány hibák | Túl sok nagy shard betöltve | Csökkentse a shard méretét vagy növelje a JVM heap-et (`-Xmx` flag) |

## Gyakran ismételt kérdések

**Kérdés: Hozzáadhatok új mappákat a hálózat futása közben?**  
Válasz: Igen – használja a `indexer.addDirectories()` metódust; a feliratkozott események valós időben terjesztik a frissítéseket.

**Kérdés: Hogyan monitorozhatom a csomópontok állapotát?**  
Válasz: Minden `SearchNetworkNode` állapot API-t biztosít; integrálja a kedvenc felügyeleti eszközével.

**Kérdés: Lehet a mester csomópontot külön gépen futtatni?**  
Válasz: Természetesen. Csak biztosítsa, hogy minden csomópont ugyanazt a `basePort`-ot használja, és elérje egymást a hálózaton.

**Kérdés: Milyen fájlformátumok támogatottak?**  
Válasz: A GroupDocs.Search alapból támogatja a PDF-eket, Word, Excel, PowerPoint, egyszerű szöveget és sok más formátumot.

**Kérdés: Új csomópont hozzáadása után újra kell indítani a hálózatot?**  
Válasz: Nem – a csomópontok dinamikusan hozzáadhatók vagy eltávolíthatók; a mester csomópont automatikusan újraosztja a shard-okat.

## Összegzés
Most már teljes, lépésről‑lépésre megértése van arról, hogyan konfiguráljuk a keresést a GroupDocs.Search for Java segítségével, az első beállítástól a valós‑idejű frissítésekig és a elosztott indexelésig. Alkalmazza ezeket a mintákat, hogy gyors, skálázható és megbízható dokumentumkereső megoldásokat építsen bármely iparág számára.

---

**Last Updated:** 2026-01-08  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs