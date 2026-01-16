---
date: '2026-01-16'
description: Tanulja meg, hogyan konfigurálja a GroupDocs keresési hálózatot Java-ban,
  és adjon hozzá szinonimákat az indexhez a keresési hatékonyság növelése érdekében.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: A GroupDocs.Search hálózat konfigurálása Java-ban – Boost Search
type: docs
url: /hu/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# GroupDocs.Search hálózat konfigurálása Java-ban – Keresés felgyorsítása

A mai adat‑vezérelt alkalmazásokban a **configure groupdocs search network** a kulcsfontosságú lépés a gyors, pontos eredmények biztosításához hatalmas dokumentumgyűjteményekben. Akár vállalati szintű keresőportált épít, akár meglévő megoldást bővít, egy jól konfigurált GroupDocs.Search hálózat lehetővé teszi a horizontális skálázást, a szinonima‑támogatás hozzáadását, és az alacsony késleltetés fenntartását. Ebben az útmutatóban megtanulja, hogyan állítsa be, telepítse és finomhangolja a GroupDocs.Search hálózatot Java használatával, valamint gyakorlati tippeket a szinonimák indexhez való hozzáadásához és a csomópontok életciklusának kezeléséhez.

## Gyors válaszok
- **Mi a fő előnye a GroupDocs.Search hálózat konfigurálásának?** Ez lehetővé teszi a elosztott indexelést és lekérdezést, javítva a teljesítményt és a skálázhatóságot.  
- **Szükségem van licencre a példák futtatásához?** A ingyenes próba verzió fejlesztéshez megfelelő; a termeléshez kereskedelmi licenc szükséges.  
- **Hozzáadhatók a szinonimák az index újraépítése nélkül?** Igen—használja a szinonima szótárat futásidőben a **add synonyms to index** művelethez.  
- **Hány csomópontot telepíthetek?** Az infrastruktúrája által megengedett számú csomópontot telepítheti; minden csomópont saját porton fut.  

## Mi a GroupDocs.Search hálózat konfigurálása?
A GroupDocs.Search hálózat konfigurálása azt jelenti, hogy meghatározzuk a mappaszerkezetet, a portokat és a csomópont beállításait, amelyek lehetővé teszik több JVM példány együttműködését az indexelésben és a keresésben. Ez a beállítás egy master‑node‑ot hoz létre, amely koordinálja a munkásokat (shard‑okat), és biztosítja, hogy a lekérdezések az egész adatkészleten végrehajtásra kerüljenek.

## Miért konfiguráljunk GroupDocs.Search hálózatot?
- **Skálázhatóság** – Az indexelési terhelés elosztása több gép között.  
- **Megbízhatóság** – A csomópontok hozzáadhatók vagy eltávolíthatók leállás nélkül.  
- **Keresési relevancia** – Szinonimák hozzáadása az indexhez a gazdagabb eredményekért.  
- **Teljesítmény** – A párhuzamos lekérdezés végrehajtás csökkenti a válaszidőt.

## Előkövetelmények
- Java Development Kit (JDK) 8 vagy újabb  
- Maven a projekt felépítéséhez  
- Alapvető ismeretek a Java szintaxisban  
- Hozzáférés a GroupDocs.Search for Java könyvtárhoz (letölthető Maven‑en vagy a hivatalos kiadási oldalon)

## GroupDocs.Search beállítása Java-hoz

Adja hozzá a tárolót és a függőséget a Maven **pom.xml** fájlhoz:

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

Alternatív megoldásként töltse le a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc beszerzése
- **Free Trial** – Fedezze fel a fő funkciókat költség nélkül.  
- **Temporary License** – Teljes képességek feloldása rövid távú teszteléshez.  
- **Commercial License** – Szükséges a termelési telepítésekhez.

### Alap inicializálás és beállítás
Hozzon létre egy egyszerű Java osztályt a könyvtár helyes betöltésének ellenőrzéséhez:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Lépésről‑lépésre útmutató a GroupDocs.Search hálózat konfigurálásához

### 1. A keresőhálózat konfigurálása
Határozza meg az alap dokumentum mappát és a kezdő portot a csomópontok közötti kommunikációhoz.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Ahol a szótárak (pl. szinonima fájlok) találhatók.  
- **basePort** – Az első port; a következő csomópontok ettől az értéktől növekvő portot kapnak.

### 2. Keresőhálózati csomópontok telepítése
Indítson el több munkás csomópontot, amelyek ugyanazt a konfigurációt használják.

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Minden csomópont saját porton (basePort + index) fut, és az összes index egy shard‑ját tartalmazza.

### 3. Csomópont eseményekre feliratkozás
Figyelje az állapotot, az indexelés előrehaladását és a hibákat egy eseményfigyelő csatolásával a master node‑hoz.

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Az esemény visszahívások lehetővé teszik, hogy reagáljon a csomópont indítására/leállítására, az indexelés befejezésére és a váratlan hibákra.

### 4. Szinonimák hozzáadása egy csomópont indexelőjéhez  
Növelje a relevanciát a **add synonyms to index** futásidőben történő használatával.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – A kifejezések tömbje, amelyeket ekvivalensnek kell tekinteni.  
- **clearBeforeAdding** – Állítsa `true`‑ra, ha a meglévő bejegyzéseket felül szeretné írni.

### 5. Könyvtárak hozzáadása az indexeléshez
Adja meg a master node‑nak, mely mappák tartalmazzák a kereshető dokumentumokat.

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

A metódus rekurzívan bejárja a könyvtárat és elosztja a fájlokat a shard‑ok között.

### 6. Szöveges keresés végrehajtása a hálózatban
Hajtsa végre a lekérdezést az összes csomóponton, opcionálisan kényszerítve a pontos egyezést.

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Állítsa `exactMatchOnly`‑t `true`‑ra, ha szigorú kifejezés egyezésre van szükség ragozás nélkül.

### 7. Hálózati csomópontok lezárása
Szabadítsa fel az erőforrásokat elegánsan, miután a feldolgozás befejeződött.

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

A megfelelő leállítás megakadályozza a memória szivárgást és egészségesen tartja a JVM‑et.

## Gyakorlati alkalmazások
| Szenárió | Hogyan segít a hálózat |
|----------|-----------------------|
| **Enterprise Search** | Indexelés elosztása adatközponti szerverek között petabájt‑méretű korpuszokhoz. |
| **Document Management** | Szinonimák hozzáadása az indexhez, hogy a felhasználók a változó terminológia ellenére is megtalálják a dokumentumokat. |
| **E‑commerce Catalog** | Régió‑specifikus csomópontok telepítése a lokalizált termékkeresések gyors kiszolgálásához. |
| **Content Management** | A tartalom kereshető marad, miközben a szerkesztők új fájlokat adnak hozzá meghatározott könyvtárakhoz. |

## Gyakori problémák és megoldások
- **Port ütközések** – Győződjön meg róla, hogy minden csomópont portja (basePort + index) szabad; szükség esetén módosítsa a `basePort`‑ot.  
- **Szinonima nem alkalmazott** – Ellenőrizze, hogy a kifejezések hozzáadása után meghívta a `indexer.setDictionary(dictionary)`‑t.  
- **Csomópont nem válaszol** – Iratkozzon fel az eseményekre; keresse a `NodeFailed` visszahívásokat a hálózati problémák diagnosztizálásához.  
- **Memória szivárgás lezáráskor** – Mindig hívja meg a `node.close()`‑t minden telepített csomópontnál.

## Gyakran feltett kérdések

**Q: Hogyan javítja a több csomópont telepítése a keresési teljesítményt?**  
A: Minden csomópont a data egy shard‑ját indexeli, lehetővé téve a párhuzamos feldolgozást és csökkentve a lekérdezési késleltetést, mivel a terhelés megoszlik.

**Q: Hozzáadhatok szinonimákat anélkül, hogy újraindexelném a meglévő dokumentumokat?**  
A: Igen, a szinonima szótár használatával futásidőben **add synonyms to index**; a változások azonnal érvénybe lépnek az új lekérdezéseknél.

**Q: Kötelező feliratkozni a csomópont eseményekre?**  
A: Bár az alapműködéshez nem szükséges, az eseményekre való feliratkozás láthatóságot biztosít a csomópont állapotáról, és segít gyorsan reagálni a hibákra.

**Q: Mik a legjobb gyakorlatok a csomópont erőforrások kezelésére?**  
A: Rendszeresen zárja le az üresjárati csomópontokat, figyelje a JVM memóriahasználatát, és a csúcsidőn kívül újrahasznosítsa a csomópontokat az erőforrás-fogyasztás optimalizálása érdekében.

**Q: Támogatja a GroupDocs.Search a nem‑szöveges formátumokat, például PDF‑eket vagy képeket?**  
A: Teljes mértékben. A könyvtár szöveget nyer ki a PDF‑ekből, Office fájlokból, és még OCR‑t is végez képeken, így azok is kereshetők azonnal.

---

**Legutóbb frissítve:** 2026-01-16  
**Tesztelve a következővel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs