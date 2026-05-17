---
date: '2026-05-17'
description: Ismerje meg, hogyan konfigurálja a base port groupdocs-t egy skálázható
  GroupDocs.Search Java hálózatban, optimalizálja a lekérdezési sebességet, és állítson
  be többcsomópontos rendszereket.
keywords:
- configure base port groupdocs
- GroupDocs.Search Java setup
- multi‑node search configuration
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure base port groupdocs for a scalable GroupDocs.Search
    Java network, optimize retrieval speed, and set up multi‑node systems.
  headline: Configure base port groupdocs in Java Search Network
  type: TechArticle
- questions:
  - answer: Disabling stop words can improve search accuracy by retaining common terms
      that might be crucial in specialized domains.
    question: What is the purpose of disabling stop words in indexing?
  - answer: Start with a high `basePort` (e.g., 49100) and increment it for each subsequent
      node, ensuring every node has a unique TCP endpoint.
    question: How do I handle port conflicts when adding multiple nodes?
  - answer: Yes—just make sure the chosen ports are open in your cloud security groups
      and replace `127.0.0.1` with the appropriate public or private IP.
    question: Can I use this setup for cloud‑based applications?
  - answer: '`NormalIndex` offers a balanced trade‑off between speed and memory usage,
      while specialized indexes (e.g., `FastIndex`) target niche performance scenarios.'
    question: What is the difference between NormalIndex and other index types?
  - answer: Technically no; the limit is dictated by your hardware resources and network
      bandwidth.
    question: Is there a limit to the number of nodes I can add?
  type: FAQPage
title: Konfigurálja a base port groupdocs-t a Java Search Networkben
type: docs
url: /hu/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Alapport csoportdokumentumok konfigurálása Java keresési hálózatban

A modern, adatintenzív alkalmazásokban a **configure base port groupdocs** az első lépés egy gyors, megbízható keresési infrastruktúra kiépítéséhez. Akár több ezer PDF-et indexel, akár több szerveren terjeszkedik, az egyedi portok és könyvtárak hozzárendelése megakadályozza a csomópont‑csomópont közötti ütközéseket és egészségesen tartja a klasztert. Ez az útmutató végigvezeti Önt az előkövetelményeken, a telepítésen és egy teljes többcsomópontos konfiguráción a GroupDocs.Search for Java használatával, így ma elindíthat egy valóban skálázható keresési hálózatot.

## Gyors válaszok
- **Mi a fő cél?** Az egyedi portok és alapkönyvtárak hozzárendelése minden keresőcsomóponthoz, az ütközések megszüntetése.  
- **Szükségem van licencre?** Igen – egy próba vagy teljes licenc szükséges a termelési telepítésekhez.  
- **Melyik Java verzió támogatott?** Java 8 vagy újabb (Java 11+ ajánlott).  
- **Futtathatom felhő szervereken?** Természetesen – csak nyissa meg a kiválasztott portokat a felhő biztonsági csoportjaiban.  
- **Hány csomópontot adhatok hozzá?** Nincs szigorú korlát; csak a hardver és a hálózati kapacitás korlátozza.

## Mi az a „configure base port groupdocs”?
**Configure base port groupdocs** a folyamat, amely során egy kezdő TCP portot rendelünk minden keresőcsomóponthoz, majd a következő csomópontok számára növeljük azt. Ez az egyszerű lépés megszünteti a rettegett „port már használatban” hibákat, és alapot teremt egy tiszta, horizontálisan skálázható keresési klaszterhez, biztosítva, hogy minden csomópont egyedi végponton kommunikáljon.

## Miért használja a GroupDocs.Search-t egy skálázható hálózathoz?
A GroupDocs.Search **magas teljesítményű indexelést** biztosít (akár 50 GB/perc egy szabványos 8‑magos szerveren) és **50+ fájlformátumot** támogat, többek között PDF, DOCX, PPTX és HTML. Moduláris architektúrája lehetővé teszi indexelők, keresők, shardok és extraktorok keverését a csomópontok között, lineáris skálázhatóságot nyújtva a hardver bővítésekor. A könyvtár beépített tömörítési lehetőségeket is kínál, amelyek akár 70 %-kal csökkentik a lemezhasználatot, miközben a lekérdezési késleltetés tipikus munkaterhelésnél 200 ms alatt marad.

## Előkövetelmények
- **Java Development Kit (JDK)** 8 vagy újabb (Java 11+ ajánlott a jobb garbage‑collection-hez).  
- **IDE**, például IntelliJ IDEA vagy Eclipse.  
- **GroupDocs.Search for Java** könyvtár (25.4 vagy újabb verzió) Maven‑en vagy manuális letöltéssel telepítve.  
- Alapvető hálózati ismeretek (TCP portok, localhost vs. távoli gépek).  
- Érvényes **GroupDocs.Search** licenc (próba vagy teljes).

## A GroupDocs.Search beállítása Java-hoz

### Telepítési útmutató

**Maven beállítás:**

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

**Közvetlen letöltés:**  
Ellenkező esetben töltse le a legújabb verziót a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc beszerzése
- **Free Trial** – kezdje el a tesztelést azonnal.  
- **Temporary License** – szerezzen hosszabb próbaidőszakot a [Temporary License](https://purchase.groupdocs.com/temporary-license) oldalon.  
- **Full Purchase** – szükséges a termelési telepítésekhez.

### Alapvető inicializálás és beállítás

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## Implementációs útmutató

### Hogyan konfigurálja a base port groupdocs‑t?
A base port konfigurálásához szerkessze a hálózati konfigurációs fájlt, vagy programozottan állítsa be a `basePort` tulajdonságot egy magas, nem használt értékre, például 49100‑ra. Minden következő csomópontnál növelje a port számát eggyel (vagy egy rögzített eltolással), hogy minden csomópont a saját egyedi TCP végpontjára kötődjön, ezzel megszüntetve a port‑ütközési hibákat és egyszerűsítve a tűzfalszabályokat.

#### Alapútvonalak beállítása
Mielőtt kódot írna, határozza meg a konzisztens mappaszerkezetet. Például hozzon létre külön könyvtárakat az indexelők (`Indexer0`), keresők (`Searcher0`) és extraktorok (`Extractor0`) számára. Ez a struktúra lehetővé teszi, hogy minden csomópont gyorsan megtalálja a fájljait.

- **Miért**: Egy előre látható könyvtárhierarchia megakadályozza a „file not found” hibákat, amikor a csomópontok különböző gépeken indulnak.

#### Base port konfigurálása
Choose a high starting port to avoid clashes with common services (HTTP 80, SSH 22, etc.). Increment the port number for each new node you add.

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Miért**: Magas porttal (pl. 49100) kezdve csökken az esély a meglévő szolgáltatásokkal való ütközésre, és egyszerűsíti a tűzfalszabályok létrehozását.

#### Host cím meghatározása
During development, `localhost` works fine. For production, replace it with the server’s IP address or DNS name so remote nodes can reach each other.

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Miért**: Valódi host cím használata lehetővé teszi a gépek közötti kommunikációt, ami elengedhetetlen a felhő vagy helyi klaszterekhez.

#### Hálózati konfiguráció létrehozása
The `NetworkConfig` class bundles all networking options—base port, host, and optional SSL settings—into a single object that the Search engine consumes.

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Miért**: Ezeknek az opcióknak a központosítása újrahasználhatóvá és könnyebben karbantarthatóvá teszi a konfigurációt számos csomópont között.

#### Csomópontok hozzáadása
`SearchNode` represents an individual node in the GroupDocs.Search cluster that performs a specific function such as indexing or searching. Instantiate a `SearchNode` for each role (indexer, searcher, extractor) and register it with the `SearchEngine`. Distributing responsibilities across nodes improves parallelism and fault tolerance.

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Miért**: A feladatok dedikált csomópontok közti szétosztása csökkenti a versengést és lehetővé teszi, hogy minden gép egyetlen feladatra specializálódjon, ezáltal növelve az összesített áteresztőképességet.

#### Konfiguráció befejezése
After adding all nodes, call `engine.start()` to spin up the network. The engine will automatically bind each node to its assigned port and verify connectivity.

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Gyakori problémák és megoldások
- **Port ütközések** – Mindig növelje a `basePort` értékét minden új csomópontnál. Ellenőrizze a nyitott portokat a `netstat` vagy az operációs rendszer hálózati monitorjával.  
- **Hiányzó könyvtárak** – Győződjön meg róla, hogy minden mappa (`Indexer0`, `Searcher0`, stb.) létezik, és a Java folyamatnak van olvasási/írási jogosultsága.  
- **Hálózati elérhetőség** – Több gépes beállításra váltáskor cserélje le a `127.0.0.1`‑et a tényleges host IP‑re, és nyissa meg a kiválasztott portokat a tűzfalakban.  

## Gyakorlati alkalmazások

| Forgatókönyv | A base port groupdocs konfigurálás előnye |
|--------------|--------------------------------------------|
| Vállalati dokumentumkezelés | Zökkenőmentes skálázás a részlegek között leállás nélkül |
| Nagy CMS platformok | Gyorsabb tartalomlekérdezés, mivel az index elosztott |
| Jogi esetkezelés | Párhuzamos PDF kinyerés csökkenti a keresési késleltetést |

## Teljesítmény szempontok
- **CPU/Memory monitorozása** – Használja a Java JMX‑et vagy egy profilozó eszközt a szálhasználat figyeléséhez.  
- **Tömörítés beállítása** – a `Compression.High` lemezhelyet takarít meg, de CPU‑t terhelhet; tesztelje a `High` és `Normal` beállításokat a legjobb egyensúly megtalálásához.  
- **Rendszeres frissítések** – Az új GroupDocs.Search kiadások gyakran tartalmaznak teljesítményjavításokat; tartsa a könyvtárat naprakészen.

## Következtetés
Most már megtanulta, hogyan **configure base port groupdocs** és hogyan állítson be egy többcsomópontos keresési hálózatot a GroupDocs.Search for Java segítségével. Kísérletezzen további csomópontokkal, finomhangolja az index beállításokat, és integrálja a hálózatot meglévő alkalmazásaiba egy valóban skálázható keresési megoldás érdekében.

## Gyakran ismételt kérdések

**Q: Mi a célja a stop szavak letiltásának az indexelés során?**  
A: A stop szavak letiltása javíthatja a keresés pontosságát azáltal, hogy megtartja a gyakori kifejezéseket, amelyek speciális területeken kulcsfontosságúak lehetnek.

**Q: Hogyan kezeljem a port ütközéseket több csomópont hozzáadásakor?**  
A: Kezdjen egy magas `basePort`‑tal (pl. 49100), és növelje azt minden következő csomópontnál, biztosítva, hogy minden csomópont egyedi TCP végponttal rendelkezzen.

**Q: Használhatom ezt a beállítást felhő‑alapú alkalmazásokhoz?**  
A: Igen – csak győződjön meg róla, hogy a kiválasztott portok nyitva vannak a felhő biztonsági csoportjaiban, és cserélje le a `127.0.0.1`‑et a megfelelő publikus vagy privát IP‑re.

**Q: Mi a különbség a NormalIndex és más index típusok között?**  
A: A `NormalIndex` kiegyensúlyozott kompromisszumot kínál a sebesség és a memóriahasználat között, míg a speciális indexek (pl. `FastIndex`) speciális teljesítményhelyzetekre vannak optimalizálva.

**Q: Van korlát a hozzáadható csomópontok számában?**  
A: Technikai szempontból nincs; a korlátot a hardver erőforrásai és a hálózati sávszélesség határozza meg.

---

**Utolsó frissítés:** 2026-05-17  
**Tesztelve ezzel:** GroupDocs.Search Java 25.4  
**Szerző:** GroupDocs

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

## Kapcsolódó oktatóanyagok

- [Hogyan konfiguráljon .NET keresési hálózatot a GroupDocs.Search és a Redaction használatával](/search/net/search-network/configure-net-search-network-groupdocs/)
- [Hogyan valósítson meg keresési hálózatot a GroupDocs.Search .NET-ben dokumentumkezelő rendszerekhez](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Keresési hálózati csomópont telepítése .NET-ben a GroupDocs használatával a hatékony dokumentum indexeléshez és visszakereséshez](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)