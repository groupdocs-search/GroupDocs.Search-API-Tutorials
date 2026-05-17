---
date: '2026-05-17'
description: Ismerje meg, hogyan konfigurálja a keresési hálózatot Java-ban, optimalizálja
  a shard-okat, szöveges keresést végez, és kezelje a portütközéseket a GroupDocs.Search
  for Java segítségével.
keywords:
- configure search network java
- GroupDocs.Search Java
- shard optimization
- Java search network
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  headline: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive
    Guide'
  type: TechArticle
- description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  name: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive Guide'
  steps:
  - name: Define Document Directories and Port
    text: '`DocumentDirectory` is a simple holder for the absolute path of a folder
      you want to index. Provide one or more paths to the configuration.'
  - name: Configure Search Network
    text: 'Create the configuration object using the defined paths:'
  - name: Deploy Nodes Using Configuration
    text: 'Deploy search network nodes and identify the master node for centralized
      management:'
  - name: Subscribe to Master Node Events
    text: '`SearchNetworkEventListener` lets you react to indexing completion, node
      failures, or shard optimizations. CODE_BLOCK_PLACEHOLDER_9_END'
  - name: Add Document Directories to Indexing Process
    text: Pass a list of folder paths to the master node; the engine will create a
      separate shard for each folder, enabling parallel query execution. CODE_BLOCK_PLACEHOLDER_10_END
  - name: Perform a Text Search
    text: Invoke the static helper to run a query and retrieve matching documents
      with relevance scores. CODE_BLOCK_PLACEHOLDER_11_END
  - name: Optimize Indexer Shards
    text: 'Optimize shards to improve search efficiency (this is where **how to optimize
      shards** really matters): CODE_BLOCK_PLACEHOLDER_12_END'
  type: HowTo
- questions:
  - answer: Optimizing shards compacts the index, reduces disk I/O, and typically
      yields 30‑50 % faster query responses for large datasets.
    question: How does shard optimization affect query speed?
  - answer: Yes, the operation is designed to run without downtime, but scheduling
      during low‑traffic periods is recommended for indexes larger than 20 GB.
    question: Is it safe to run `optimizeShards` on a live node?
  - answer: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor`
      to fine‑tune the optimization process.
    question: Can I customize the `OptimizeOptions`?
  - answer: Verify file system permissions, ensure enough free disk space, and confirm
      that no other process is locking the index files.
    question: What should I do if I encounter an `IOException` during optimization?
  - answer: Yes, the optimizer merges segments and removes tombstones, freeing up
      space occupied by deleted documents.
    question: Does optimizing shards also reclaim deleted document space?
  type: FAQPage
title: 'Hogyan optimalizáljuk a shard-okat a GroupDocs.Search for Java-ban: Átfogó
  útmutató'
type: docs
url: /hu/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# Hogyan optimalizáljuk a shard-okat a GroupDocs.Search for Java-ban: Átfogó útmutató

A hatékony dokumentumkeresés elengedhetetlen a fejlesztők és vállalkozások számára, amelyek nagy adatállományokat kezelnek vagy gyors belső lekérdezésre van szükségük. Ebben az oktatóanyagról megtanulja, hogyan **konfigurálja a search network java**-t, hogyan indexel és kérdez le dokumentumokat, valamint a **shard-ok optimalizálásának** pontos lépéseit a legjobb teljesítmény érdekében. Emellett valós példákat, gyakori buktatókat és gyakorlati tippeket is bemutatunk a keresőcsomópontok zökkenőmentes működéséhez.

## Gyors válaszok
- **Mi a shard optimalizálás?** Átstrukturálja az indexadatokat a lekérdezések felgyorsítása és a tárolási terhelés csökkentése érdekében.  
- **Hogyan konfigurálja a keresőhálózatot?** Határozzon meg egy alapkönyvtárat és portot, majd telepítse a csomópontokat a biztosított API segítségével.  
- **Hogyan hajtson végre szöveges keresést?** Használja a `TextSearchInNetwork.searchAll` metódust a lekérdezés karakterláncával.  
- **Hogyan indexel dokumentumokat Java-ban?** Adjon hozzá dokumentumkönyvtárakat a master csomóponthoz a `IndexingDocuments.addDirectories` segítségével.  
- **Hogyan kezelje a portütközéseket?** Módosítsa a `basePort` változót egy nem használt portra a gépén.

## Hogyan konfigurálja a keresőhálózatot
`Configuration` tárolja a GroupDocs.Search hálózat indításához szükséges összes beállítást, például az indexmappa helyét és a kommunikációs portot.  
`SearchNetwork` irányítja a csomópontokat, kezelve az indexelést és a lekérdezés elosztását.

Töltse be a keresési konfigurációt, állítsa be a dokumentumok alapútját, válasszon egy szabad portot, és indítsa el a hálózatot – mindezt néhány kódsorban. Ez a közvetlen válasz kevesebb, mint 70 szóban magyarázza el a teljes folyamatot: **Hozzon létre egy `Configuration` objektumot, állítsa be a `basePath` és `basePort` értékeket, majd hívja meg a `SearchNetwork.start(configuration)` metódust.** A hálózat automatikusan elindít egy master csomópontot és a szükséges worker csomópontokat, készen áll az indexelési kérések fogadására.

### Definíció horgony
`Configuration` a központi osztály, amely a GroupDocs.Search hálózat indításához szükséges összes beállítást tárolja, például az indexmappa helyét és a kommunikációs portot.

Az elkerülendő „port már használatban” hiba érdekében először ellenőrizze, hogy a kiválasztott port szabad (pl. `netstat` vagy egyszerű socket teszt használatával), mielőtt inicializálná a hálózatot.

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

## Hogyan indexeljen dokumentumokat Java-ban
`IndexingDocuments` egy segédosztály, amely egyszerűsíti több könyvtár hozzáadását egy keresőcsomóponthoz, és elindítja az indexelési folyamatot.

Adja hozzá a dokumentum mappákat a master csomóponthoz, majd hagyja, hogy az indexelő bejárja őket. **Közvetlen válasz:** Hívja meg a `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))` metódust, majd indítsa el a `masterNode.index()`-et; a motor kereshető shard-okat hoz létre minden megadott mappához. Ez a megközelítés vízszintesen skálázható – adjon hozzá több csomópontot, és ugyanaz a metódus automatikusan elosztja a munkaterhet.

### Definíció horgony
`IndexingDocuments` egy segédosztály, amely egyszerűsíti több könyvtár hozzáadását egy keresőcsomóponthoz, és elindítja az indexelési folyamatot.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Hogyan hajtson végre szöveges keresést
`TextSearchInNetwork` statikus segédmetódusokat biztosít, amelyek egy szöveges lekérdezést sugároznak a hálózat minden csomópontjára, és összegzik az eredményeket.  
`SearchResult` tartalmazza a megtalált dokumentum azonosítóját, kivonatát és relevancia pontszámát.

Futtasson lekérdezést az összes shard-on egyetlen metódushívással. **Közvetlen válasz:** Használja a `TextSearchInNetwork.searchAll("your query", searchNetwork)` metódust; a metódus `SearchResult` objektumok gyűjteményét adja vissza, amelyek dokumentumazonosítókat, kivonatokat és relevancia pontszámokat tartalmaznak. További szűréseket végezhet nyelv, fájltípus vagy egyedi metaadatok alapján anélkül, hogy extra kódot írna.

### Definíció horgony
`TextSearchInNetwork` statikus segédmetódusokat biztosít, amelyek egy szöveges lekérdezést sugároznak a hálózat minden csomópontjára, és összegzik az eredményeket.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## Hogyan kezelje a portütközéseket
Ha az alapértelmezett port (`49132`) foglalt, egyszerűen válasszon egy másik szabad portot, és frissítse a `basePort` mezőt a hálózat indítása előtt. **Közvetlen válasz:** Módosítsa a `int basePort = 49132;` sort egy nem használt értékre, például `49133`, építse újra, és indítsa újra; a hálózat az új portra fog kötődni a meglévő csomópontokat érintés nélkül.

Pro tipp: Tartson egy kis konfigurációs fájlt (pl. `search-config.properties`), így a portot újrafordítás nélkül módosíthatja.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Előfeltételek
Mielőtt elkezdenénk, győződjön meg róla, hogy a következő előfeltételek rendelkezésre állnak:

### Szükséges könyvtárak, verziók és függőségek
A megoldás megvalósításához adja hozzá a GroupDocs.Search könyvtárat Maven segítségével, a következő konfigurációt beillesztve a `pom.xml` fájlba:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
Alternatívaként töltse le a legújabb verziót a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Környezet beállítási követelmények
- Java Development Kit (JDK) 8 vagy újabb.
- Hálózati engedélyek, amelyek lehetővé teszik a kiválasztott `basePort`-ra való kötést.
- Megfelelő lemezterület az indexfájlokhoz (minden shard körülbelül ~10 MB-ot foglal 1 000 dokumentumra).

### Tudás előfeltételek
Az Java, az objektum‑orientált programozás és a kivételkezelés alapvető ismerete segíti a példák zökkenőmentes követését.

## A GroupDocs.Search for Java beállítása
A GroupDocs.Search projektbe való integrálásához kövesse az alábbi lépéseket:

1. **Add the Dependency**: Ahogy fent látható, adja hozzá a szükséges Maven függőséget a projektjéhez, vagy töltse le közvetlenül a kiadási oldalról.  
2. **License Acquisition**:  
   - **Free trial** – licenckulcs nem szükséges, de a használat napi 500 dokumentumra korlátozódik.  
   - **Temporary license** – kérjen 30‑napos próbakulcsot a [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) oldalról.  
   - **Full license** – vásároljon termelési licencet korlátlan hozzáféréshez és prioritásos támogatáshoz.  
3. **Basic Initialization and Setup**:  
   Initialize the configuration using the `Configuration` class, setting up the base path for documents and specifying a port number:

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## Implementációs útmutató
Most vizsgáljuk meg a kulcsfontosságú funkciók megvalósítását a GroupDocs.Search Java segítségével.

### Funkció: Keresőhálózat konfigurálása
**Áttekintés**: A keresőhálózat beállítása magában foglalja a dokumentumkönyvtár meghatározását és egy adott port konfigurálását a csomópontok közötti kommunikációhoz.

#### 1. lépés: Dokumentumkönyvtárak és port meghatározása
`DocumentDirectory` egy egyszerű tároló az indexelni kívánt mappa abszolút útvonalához. Adjon meg egy vagy több útvonalat a konfigurációban.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### 2. lépés: Keresőhálózat konfigurálása
Hozza létre a konfigurációs objektumot a megadott útvonalak felhasználásával:

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Funkció: Keresőhálózati csomópontok telepítése
**Áttekintés**: Telepítse a csomópontokat a dokumentumkeresések hatékony kezelése érdekében a hálózatában.

#### 1. lépés: Csomópontok telepítése konfigurációval
Telepítse a keresőhálózati csomópontokat, és azonosítsa a master csomópontot a központosított kezeléshez:

```java
public static void optimizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    OptimizeOptions options = new OptimizeOptions();
    indexer.optimize(options);
}

optimizeShards(masterNode);

// Perform a second text search to observe optimization effects
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Funkció: Hálózati csomópont eseményekre feliratkozás
**Áttekintés**: Figyelje a keresőhálózatot eseményekre való feliratkozással, amelyek fontos változásokról vagy műveletekről értesítik.

#### 1. lépés: Master csomópont eseményeire való feliratkozás
`SearchNetworkEventListener` lehetővé teszi, hogy reagáljon az indexelés befejezésére, csomópont hibákra vagy shard optimalizációkra.

CODE_BLOCK_PLACEHOLDER_9_END

### Funkció: Dokumentumok indexelése hálózati csomópontokban
**Áttekintés**: Adjon hozzá könyvtárakat, amelyek dokumentumokat tartalmaznak, az indexelési folyamathoz a hatékony keresés érdekében.

#### 1. lépés: Dokumentumkönyvtárak hozzáadása az indexelési folyamathoz
Adjon át egy mappautak listáját a master csomóponthoz; a motor minden mappához külön shard-ot hoz létre, lehetővé téve a párhuzamos lekérdezés végrehajtását.

CODE_BLOCK_PLACEHOLDER_10_END

### Funkció: Szöveges keresés hálózati csomópontokban
**Áttekintés**: Szöveges keresések végrehajtása az összes indexelt dokumentumon a keresőhálózatában.

#### 1. lépés: Szöveges keresés végrehajtása
Hívja meg a statikus segédmetódust egy lekérdezés futtatásához és a relevancia pontszámokkal rendelkező egyező dokumentumok lekéréséhez.

CODE_BLOCK_PLACEHOLDER_11_END

### Funkció: Shard-ok optimalizálása
**Áttekintés**: Javítsa a teljesítményt a keresőhálózati csomópont indexelőjében lévő shard-ok optimalizálásával.

#### 1. lépés: Indexelő shard-ok optimalizálása
Optimalizálja a shard-okat a keresési hatékonyság javítása érdekében (itt jön képbe a **shard-ok optimalizálása** valódi jelentősége):

CODE_BLOCK_PLACEHOLDER_12_END

## Gyakorlati alkalmazások
A GroupDocs.Search for Java különféle valós helyzetekben alkalmazható, mindegyik a shard optimalizálásból profitál:

1. **Enterprise Document Management** – 10 TB+ archívumot kezel almásodperces lekérdezési időkkel a shard optimalizálás után.  
2. **E‑commerce Platforms** – 1 millió SKU termékkeresést támogat, a shard-ok optimalizálásakor akár 45 %-kal csökkenti a késleltetést.  
3. **Legal Firms** – 200 GB-os tárolókból 200 ms alatti idő alatt nyeri ki az ügyiratokat.  
4. **Library Systems** – 500 e digitális könyv katalóguskeresését támogatja hatékony memóriahasználattal.  
5. **Content Management Systems (CMS)** – Azonnali tartalomfelfedezést tesz lehetővé többoldalas telepítésekhez, több mint 2 millió oldallal.

## Teljesítmény szempontok
A GroupDocs.Search megvalósításának optimális teljesítményének biztosításához:

- **Rendszeresen optimalizálja a shard-okat** – Az `optimizeShards()` futtatása minden 10 GB új adat után 30‑50 % -kal csökkenti a lekérdezési válaszidőt.  
- **Figyelje a memóriahasználatot** – Tartsa a JVM heap-et a fizikai RAM 75 %-a alatt; nagy indexekhez engedélyezze a G1GC-t.  
- **Használjon inkrementális indexelést** – Csak a módosított fájlokat adja hozzá, hogy elkerülje a teljes újraindexelést.  
- **Használja a többcsomópontos skálázást** – Adjon hozzá worker csomópontokat a shard-ok elosztásához; minden további csomópont körülbelül ~20 %-kal növelheti a throughput-ot olvasás‑intenzív munkaterhelések esetén.

## Gyakori problémák és megoldások
| Probléma | Tünet | Megoldás |
|----------|-------|----------|
| Portütközés indításkor | `java.net.BindException: Address already in use` | Módosítsa a `basePort`-ot egy nem használt értékre; ellenőrizze a `netstat -ano` segítségével. |
| Memóriahiányos hibák optimalizálás közben | `java.lang.OutOfMemoryError: Java heap space` | Növelje a JVM `-Xmx` kapcsolót, vagy futtassa az optimalizálást egy dedikált, több RAM-mal rendelkező csomóponton. |
| Hiányzó dokumentumok a keresési eredményekben | Nincsenek eredmények az indexelés után | Győződjön meg róla, hogy a könyvtárak helyesen lettek hozzáadva a `IndexingDocuments.addDirectories` segítségével, és hogy a `masterNode.index()` kivétel nélkül befejeződött. |
| Elavult shard-ok tömeges törlés után | A törölt fájlok még megjelennek | Futtassa az `optimizeShards()`-t a szegmensek egyesítéséhez és a tombstone-ök eltávolításához. |

## Gyakran feltett kérdések

**Q: Hogyan befolyásolja a shard optimalizálás a lekérdezés sebességét?**  
A: A shard-ok optimalizálása tömöríti az indexet, csökkenti a lemez‑I/O‑t, és általában 30‑50 % gyorsabb lekérdezési válaszidőt eredményez nagy adathalmazok esetén.

**Q: Biztonságos-e a `optimizeShards` futtatása élő csomóponton?**  
A: Igen, a művelet úgy van tervezve, hogy leállás nélkül fusson, de 20 GB-nál nagyobb indexek esetén ajánlott alacsony forgalmú időszakban ütemezni.

**Q: Testreszabhatom a `OptimizeOptions`-t?**  
A: Természetesen. Beállíthatja például a `maxSegmentSize` vagy a `mergeFactor` paramétereket az optimalizálási folyamat finomhangolásához.

**Q: Mit tegyek, ha `IOException`-t kapok optimalizálás közben?**  
A: Ellenőrizze a fájlrendszer jogosultságait, biztosítsa a megfelelő szabad lemezterületet, és győződjön meg arról, hogy semmilyen más folyamat nem zárolja az indexfájlokat.

**Q: Az optimalizálás visszaszerzi a törölt dokumentumok helyét is?**  
A: Igen, az optimalizáló egyesíti a szegmenseket és eltávolítja a tombstone-öket, felszabadítva a törölt dokumentumok által elfoglalt helyet.

## Következtetés
Ezzel az átfogó útmutatóval most már tudja, hogyan **konfigurálja a search network java**-t, indexeljen dokumentumokat, futtasson szöveges lekérdezéseket, és ami a legfontosabb, hogyan **optimalizálja a shard-okat**, hogy a keresési teljesítmény éles maradjon. Alkalmazza ezeket a mintákat bármely Java‑alapú vállalati keresési megoldásra, és mérhető javulást fog látni a késleltetésben, a skálázhatóságban és az erőforrás‑felhasználásban. A következő lépésekhez fedezze fel a fejlett funkciókat, például az egyedi elemzőket, a facettált keresést és a felhő‑tárolók integrációját.

**Legutóbb frissítve:** 2026-05-17  
**Tesztelve:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [GroupDocs.Search hálózat konfigurálása .NET‑ben: Átfogó útmutató](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Mester .NET dokumentum indexelés a GroupDocs.Search‑szel: Átfogó útmutató](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Oktatóanyagok és példák a GroupDocs.Search for Java-hoz](/search/net/)