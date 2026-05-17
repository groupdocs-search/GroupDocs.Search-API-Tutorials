---
date: '2026-05-17'
description: Ismerje meg, hogyan adhatja hozzá a groupdocs Maven függőséget, állíthatja
  be a Java keresési hálózatot, és adhat hozzá könyvtárakat az indexhez a gyors, skálázható
  dokumentumlekérdezéshez.
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: Hogyan adjon hozzá GroupDocs Maven függőséget a keresési hálózathoz
type: docs
url: /hu/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# Hogyan adjon hozzá GroupDocs Maven függőséget a keresési hálózathoz

Ebben az átfogó útmutatóban megtudja, hogyan **adjon hozzá groupdocs Maven függőséget**, konfiguráljon egy robusztus Java keresési hálózatot a GroupDocs.Search használatával, és tartsa szinkronban a shardokat. Akár jogi dokumentumokat, pénzügyi kimutatásokat vagy tudományos dolgozatokat indexel, az alábbi lépések segítenek kereshető indexeket létrehozni, a lekérdezési terhelést a csomópontok között elosztani, és minimális erőfeszítéssel adatkonzisztenciát fenntartani.

## Gyors válaszok
- **Mi a GroupDocs Maven függőség?** A Maven artefakt, amely a GroupDocs.Search könyvtárat csomagolja Java projektekhez.  
- **Miért használjon keresési hálózatot?** Az indexelési és lekérdezési terhelést több csomópont között osztja el, javítva a sebességet és a megbízhatóságot.  
- **Hogyan adhatok hozzá könyvtárakat az indexhez?** Használja az `IndexingDocuments.addDirectories` metódust a master csomóponton.  
- **Hogyan szinkronizálja a shardokat?** Hívja meg a `SynchronizeOptions`-t minden csomópont `Indexer`-én.  
- **Szükségem van licencre?** Igen, a termelési használathoz próbaverzió vagy kereskedelmi licenc szükséges.

## Mi a GroupDocs Maven függőség?

A `GroupDocs Maven dependency` egy Maven artefakt, amely a GroupDocs.Search könyvtárat csomagolja Java projektekhez.  
Minden szükséges osztályt biztosít a kereshető indexek létrehozásához, a hálózati csomópontok kezeléséhez és a gyors lekérdezések végrehajtásához, és a Maven automatikusan feloldja a tranzitív függőségeket, így néhány sor a `pom.xml`-ben egy használatra kész keresőmotorral biztosítja.

## Hogyan adja hozzá a GroupDocs Maven függőséget

Adja hozzá a tárolót és a függőségi bejegyzéseket a `pom.xml`-hez, majd futtassa a `mvn clean install` parancsot; a Maven letölti a `groupdocs-search` JAR-t és a szükséges könyvtárakat, így az API elérhetővé válik a projektben. A build sikeres befejezése után azonnal használhatja a `com.groupdocs.search` osztályokat.

### Maven konfiguráció

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

> **Pro tipp:** Tartsa naprakészen a verziószámot az hivatalos kiadások oldalának ellenőrzésével.

A JAR-t közvetlenül is letöltheti az hivatalos oldalról: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## Miért használjon keresési hálózatot?

A keresési hálózat lehetővé teszi a horizontális skálázást az index shardokra bontásával, amelyek különálló csomópontokon helyezkednek el. A GroupDocs.Search **50+ bemeneti formátumot** képes kezelni és **több száz oldalas dokumentumokat** feldolgozni anélkül, hogy az egész fájlt a memóriába töltené, így almásodperces lekérdezési válaszokat biztosít még az adatvolumen növekedése esetén is.

## Előfeltételek

- **JDK** (11 vagy újabb) telepítve.  
- Egy IDE, például IntelliJ IDEA vagy Eclipse.  
- Alap Java ismeretek, Maven ismeret, és a hálózati csomópontok koncepciójának megértése.  
- Érvényes GroupDocs.Search licenc (ingyenes próba vagy kereskedelmi).

## Alap inicializálás és beállítás

Kezdje egy indexkönyvtár létrehozásával:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Ez az egyszerű lépés előkészíti a környezetet a későbbi hálózati konfigurációhoz.

## Megvalósítási útmutató

### 1. funkció: Keresési hálózat konfigurálása

#### Áttekintés

A keresési hálózat konfigurálása beállítja a fájl útvonalakat és portokat, amelyeket a csomópontok a kommunikációhoz használnak.

##### Útvonalak és portok beállítása

A Configuration egy osztály, amely a hálózati útvonalakat, portokat és egyéb beállításokat tartalmazza a keresési klaszterhez.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
A `configuration` objektum most már tartalmazza a keresési hálózat összes szükséges beállítását.

### 2. funkció: Keresési hálózati csomópontok telepítése

#### Áttekintés

Telepítse a csomópontokat a munkaterhelés hálózaton belüli elosztásához. A master csomópont kezeli a műveleteket és eseményeket.

##### Telepítési kód

A SearchNetworkNode egy csomópontot képvisel a keresési hálózatban, amely master vagy worker szerepet is betölthet.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### 3. funkció: Keresési hálózati csomópont eseményekre feliratkozás

#### Áttekintés

Az események figyelése lehetővé teszi a hálózat változásainak vagy frissítéseinek dinamikus kezelését.

##### Feliratkozási megvalósítás

A SearchNetworkNodeEvents eseményhorgokat biztosít a csomópont életciklusához és az indexelési műveletekhez.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### 4. funkció: Könyvtárak hozzáadása az indexhez

#### Áttekintés

A könyvtárak hozzáadása a kulcsfontosságú lépés, amely a dokumentumokat kereshetővé teszi.

##### Dokumentum hozzáadása

`IndexingDocuments.addDirectories` hozzáadja a mappák útvonalait az indexhez feldolgozás céljából.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### 5. funkció: Shardok szinkronizálása a keresési hálózati csomóponton

#### Áttekintés

A szinkronizáció biztosítja az adatkonzisztenciát az összes shard között.

##### Szinkronizációs kód

`SynchronizeOptions` konfigurálja, hogyan szinkronizálódnak a shardok a csomópontok között.  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### 6. funkció: Keresési hálózati csomópontok lezárása

#### Áttekintés

A csomópontok megfelelő lezárása felszabadítja az erőforrásokat és megakadályozza a memória szivárgásokat.

##### Csomópont lezárása

`close()` felszabadítja az erőforrásokat és leállítja a keresési hálózati csomópontot.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Gyakorlati alkalmazások

1. **Jogi dokumentumkezelés** – Gyorsan lekérheti az ügyiratokat és precedenseket.  
2. **Pénzügyi nyilvántartás** – Másodpercek alatt hozzáférhet a kimutatásokhoz és audit nyomokhoz.  
3. **Tudományos kutatás** – Kereshet több ezer dolgozat között, hogy megtalálja a releváns idézeteket.

## Teljesítmény szempontok

- **Lekérdezések optimalizálása** – Írjon tömör lekérdezéseket a válaszidő csökkentése érdekében.  
- **Memóriakezelés** – Figyelje a JVM heap használatát; nagy indexek esetén fontolja meg a GC hangolást.  
- **Skálázási stratégia** – Adj hozzá csomópontokat arányosan az adatvolumenhez és a lekérdezési terheléshez.

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|----------|----|----------|
| A csomópontok nem tudnak csatlakozni | Port ütközés | `basePort` módosítása egy nem használt értékre |
| Az index nem frissül | Eseményfeliratkozás hiányzik | Győződjön meg róla, hogy a `SearchNetworkNodeEvents.subscribe(masterNode)` meghívásra kerül |
| Magas késleltetés | Nem elegendő shard | Növelje a csomópontok számát és egyensúlyozza a dokumentumok eloszlását |

## Gyakran feltett kérdések

**K: Mi a fő előnye a GroupDocs.Search használatának?**  
V: Gyors, skálázható keresési képességeket biztosít nagy dokumentumkészletekhez minimális konfigurációval.

**K: Testreszabhatom a csomópont beállításait egy keresési hálózatban?**  
V: Igen, egyéni útvonalakat, portokat és egyéb beállításokat állíthat be a `Configuration` objektumon keresztül.

**K: Hogyan adhatok hozzá könyvtárakat az indexhez, miután a hálózat már fut?**  
V: Hívja meg a `IndexingDocuments.addDirectories(masterNode, "path")` metódust, amikor új mappákat kell indexelni.

**K: Hogyan szinkronizáljam a shardokat, amikor egy új csomópont csatlakozik a hálózathoz?**  
V: Használja a fent bemutatott `synchronizeShards` metódust az újonnan hozzáadott csomóponton.

**K: Szükségem van licencre a fejlesztéshez?**  
V: Az ingyenes próba licenc elegendő a teszteléshez; a termeléshez kereskedelmi licenc szükséges.

## Összegzés

A guide követésével most már tudja, hogyan **adjon hozzá groupdocs Maven függőséget**, konfiguráljon egy többcsomópontos keresési hálózatot, indexeljen könyvtárakat, és tartsa a shardokat szinkronban. Ezek a lépések egy nagy teljesítményű dokumentumkereső megoldás alapját képezik, amely a szervezet igényeivel együtt növekedhet.

---

**Utolsó frissítés:** 2026-05-17  
**Tesztelve a következővel:** GroupDocs.Search 25.4  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [Oktatóanyagok és példák a GroupDocs.Search Java-hoz](/search/net/)
- [GroupDocs.Search hálózat konfigurálása .NET-ben: Átfogó útmutató](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Hogyan valósítsunk meg keresési hálózatot a GroupDocs.Search .NET-ben dokumentumkezelő rendszerekhez](/search/net/search-network/implement-search-network-groupdocs-dotnet/)