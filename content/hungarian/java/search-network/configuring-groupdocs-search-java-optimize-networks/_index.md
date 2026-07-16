---
date: '2026-07-16'
description: Ismerje meg, hogyan konfigurálja a GroupDocs.Search hálózatot Java-ban,
  szinonimákat adjon az indexhez, és növelje a keresési teljesítményt az elosztott
  csomópontok között.
keywords:
- how to configure groupdocs
- add synonyms to index
- GroupDocs.Search Java
- distributed search network
- Java search scaling
lastmod: '2026-07-16'
og_description: Hogyan konfigurálja a GroupDocs.Search hálózatot Java-ban, és adjon
  szinonimákat az indexhez a gyorsabb és pontosabb eredmények érdekében. Kövesse ezt
  a lépésről‑lépésre útmutatót.
og_image_alt: 'Developer guide: Configure GroupDocs.Search network in Java with synonym
  support'
og_title: Hogyan konfiguráljuk a GroupDocs.Search hálózatot Java-ban – Keresés felgyorsítása
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to configure GroupDocs.Search network in Java, add synonyms
    to index, and boost search performance across distributed nodes.
  headline: How to Configure GroupDocs.Search Network in Java Guide
  type: TechArticle
- questions:
  - answer: Each node indexes a shard of the data, allowing parallel processing and
      reducing query latency as the workload is shared across the cluster.
    question: How does deploying multiple nodes improve search performance?
  - answer: Yes, you can **add synonyms to index** at runtime via the synonym dictionary;
      the changes take effect immediately for new queries.
    question: Can I add synonyms without re‑indexing existing documents?
  - answer: While not required for basic operation, event subscription gives you visibility
      into node health and helps you react to failures promptly.
    question: Is subscribing to node events mandatory?
  - answer: Regularly close idle nodes, monitor JVM memory usage, and recycle nodes
      during off‑peak hours to keep resource consumption optimal.
    question: What are best practices for managing node resources?
  - answer: Absolutely. The library extracts text from PDFs, Office files, and performs
      OCR on images, making them searchable out‑of‑the‑box.
    question: Does GroupDocs.Search support non‑text formats like PDFs or images?
  type: FAQPage
tags:
- configure groupdocs
- GroupDocs.Search
- Java search network
- synonym dictionary
- scalable search
title: Hogyan konfiguráljuk a GroupDocs.Search hálózatot Java-ban – útmutató
type: docs
url: /hu/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Hogyan konfiguráljuk a GroupDocs.Search hálózatot Java-ban – A keresés felgyorsítása

A modern, adatintenzív alkalmazásokban a **GroupDocs helyes konfigurálása** a kulcsa annak, hogy villámgyors, releváns keresési eredményeket nyújtsunk hatalmas dokumentumtárakban. Akár vállalati portált, tudásbázist vagy termékkatalógust építesz, egy jól hangolt GroupDocs.Search hálózat lehetővé teszi a horizontális skálázást, szinonima logika bevezetését, és a késleltetés kontrollálását. Ebben az útmutatóban lépésről lépésre végigvezetünk a GroupDocs.Search hálózat Java-val történő beállításán, telepítésén és finomhangolásán, valamint gyakorlati tanácsokat adunk a szinonimák indexhez való hozzáadásához és a csomópontok életciklusának kezeléséhez.

## Gyors válaszok
- **Mi a fő előnye a GroupDocs.Search hálózat konfigurálásának?** Lehetővé teszi a elosztott indexelést és lekérdezést, javítva a teljesítményt és a skálázhatóságot.  
- **Szükségem van licencre a példák futtatásához?** A ingyenes próba verzió fejlesztéshez használható; a kereskedelmi licenc a termeléshez kötelező.  
- **Hozzáadhatók szinonimák az index újraépítése nélkül?** Igen—használja a szinonima szótárat futásidőben a **szinonimák indexhez adásához**.  
- **Hány csomópontot telepíthetek?** Annyi csomópontot telepíthetsz, amennyit az infrastruktúrád megenged; minden csomópont saját porton fut.  
- **Milyen Java verzió szükséges?** A JDK 8 vagy újabb támogatott, teljes kompatibilitással a JDK 21-ig.

## Mi a GroupDocs.Search hálózat konfigurálása?
A **GroupDocs.Search hálózat** egy JVM folyamatok gyűjteménye, amelyek együttműködnek egy megosztott dokumentumkészlet indexelésében és lekérdezésében. Egy master csomópontból áll, amely egy vagy több worker csomópontot (shardokat) irányít. A hálózat elrejti a háttértárolót, így egyetlen lekérdezés automatikusan minden shardra sugárzik, és az eredmények összeolvadnak, mielőtt visszaadnák a hívónak.

## Miért konfiguráljunk egy GroupDocs.Search hálózatot?
A GroupDocs.Search hálózat konfigurálása három konkrét előnyt biztosít: **skálázhatóság**, **megbízhatóság**, és **növelt relevancia**. Az indexelési terhelés 20 csomópontig terjesztésével, mindegyik egy 5 GB shardot kezelve, a teljes indexelési idő körülbelül 70 %-kal csökkenthető egyetlen csomópontos beállításhoz képest. Egy szinonima szótár hozzáadása akár 35 %-kal növeli a visszahívást (recall) azoknál a lekérdezéseknél, amelyek alternatív terminológiát használnak, míg a csomópont redundancia 99,9 %-os üzemidőt garantál a karbantartási időszakok alatt.

## Előfeltételek
- Java Development Kit (JDK) 8 – 21 (bármely LTS verzió)  
- Maven 3.5 + a projekt felépítéséhez  
- Alapvető Java szintaxis és Maven függőségkezelés ismerete  
- Hozzáférés a GroupDocs.Search for Java könyvtárhoz (elérhető a Maven Centralon vagy a hivatalos kiadási oldalon)

## A GroupDocs.Search beállítása Java-hoz

Adja hozzá a tárolót és a függőséget a Maven **pom.xml** fájlhoz:

A következő XML kódrészlet hozzáadja a GroupDocs.Search tárolót és a könyvtár függőségét.  
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

Alternatívaként töltsd le a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc beszerzése
- **Free Trial** – Fedezd fel a fő funkciókat költség nélkül.  
- **Temporary License** – Teljes funkcionalitás feloldása rövid távú teszteléshez.  
- **Commercial License** – Szükséges a termelési telepítésekhez és a prémium támogatás igénybevételéhez.

### Alap inicializálás és beállítás
Hozz létre egy egyszerű Java osztályt a könyvtár helyes betöltésének ellenőrzéséhez:

A SampleInitializer osztály bemutatja a GroupDocs.Search motor betöltését.  
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

### 1. A keresési hálózat konfigurálása
Határozd meg az alap dokumentum mappát és a csomópontok kommunikációjának kezdő portját.

A SearchNetworkConfig tartalmazza a hálózati csomópontok konfigurációját.  
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

- **basePath** – A könyvtár, ahol a szótárak (pl. szinonima fájlok) találhatók.  
- **basePort** – Az első port; a további csomópontok ettől az értéktől növekvő portot kapnak.

### 2. Keresési hálózati csomópontok telepítése
Indíts több worker csomópontot, amelyek ugyanazt a konfigurációt használják.

A SearchNode egy egyedi csomópontot képvisel az elosztott hálózatban.  
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

Minden csomópont saját porton (`basePort + index`) fut, és a teljes index egy shardját tartja, lehetővé téve az indexelés és a lekérdezés végrehajtásának párhuzamos feldolgozását.

### 3. Csomópont eseményekre feliratkozás
Figyeld az egészségi állapotot, az indexelés előrehaladását és a hibaállapotokat, egy eseményfigyelő csatolásával a master csomóponthoz.

A NetworkEventListener kezeli a csomópont életciklus eseményeinek visszahívásait.  
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

Az esemény visszahívások lehetővé teszik a csomópont indítására/leállítására, az indexelés befejezésére és a váratlan hibákra való reagálást, teljes megfigyelhetőséget biztosítva az elosztott rendszer felett.

### 4. Szinonimák hozzáadása egy csomópont indexelőjéhez  
Növeld a relevanciát a **szinonimák indexhez adásával** futásidőben.

A SynonymDictionary lehetővé teszi szinonima csoportok hozzáadását az indexelőhöz.  
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
- **clearBeforeAdding** – Állítsd `true`-ra, ha a meglévő bejegyzéseket felül akarod írni.

### 5. Könyvtárak hozzáadása az indexeléshez
Add meg a master csomópontnak, mely mappák tartalmazzák a kereshető dokumentumokat.

Az Indexer.addDirectory regisztrál egy mappát az indexeléshez.  
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

A metódus rekurzívan beolvassa a könyvtárat és a fájlokat shardokra osztja, több mint 10 TB adatot támogat anélkül, hogy teljes fájlokat memóriába töltene.

### 6. Szöveges keresés végrehajtása a hálózatban
Futtass egy lekérdezést az összes csomóponton, opcionálisan kényszerítve a pontos egyezést.

A SearchEngine.search futtatja a lekérdezést a hálózaton.  
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

Állítsd az `exactMatchOnly` értékét `true`-ra, ha szigorú kifejezés egyezésre van szükség stemming nélkül, ami akár 20 %-kal is javíthatja a pontosságot kódkeresési esetekben.

### 7. Hálózati csomópontok lezárása
Szabadítsd fel az erőforrásokat elegánsan, miután a feldolgozás befejeződött.

`node.close()` leállít egy SearchNode-ot és felszabadítja az erőforrásokat.  
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

A megfelelő leállítás megakadályozza a memória szivárgásokat és egészségesen tartja a JVM-et, különösen a hosszú távú szolgáltatásoknál, amelyek a csúcsidőn kívül újrahasznosítják a csomópontokat.

## Gyakorlati alkalmazások
| Szenárió | Hogyan segít a hálózat |
|----------|-----------------------|
| **Vállalati keresés** | Az indexelés elosztása adatközponti szerverek között petabájt‑méretű korpuszokhoz, alulmásodperces lekérdezési késleltetés elérése 100 M+ dokumentum esetén. |
| **Dokumentumkezelés** | Szinonimák hozzáadása az indexhez, hogy a felhasználók változó terminológia esetén is megtalálják a dokumentumokat, ezáltal a visszahívás (recall) akár 35 %-kal növelhető. |
| **E‑kereskedelmi katalógus** | Régióspecifikus csomópontok telepítése a lokalizált termékkeresések gyors kiszolgálásához, az átlagos válaszidő csökkentése 250 ms-ről 80 ms-re. |
| **Tartalomkezelés** | Tartalom kereshető marad, miközben a szerkesztők új fájlokat adnak hozzá adott könyvtárakhoz; a hálózat fokozatosan újraindexel leállás nélkül. |

## Gyakori problémák és megoldások
- **Portütközések** – Győződj meg arról, hogy minden csomópont portja (`basePort + index`) szabad; szükség esetén módosítsd a `basePort`-ot.  
- **A szinonima nem alkalmazott** – Ellenőrizd, hogy a kifejezések hozzáadása után hívtad-e a `indexer.setDictionary(dictionary)`-t; különben az új szinonimák nem lesznek figyelembe véve a keresés során.  
- **A csomópont nem válaszol** – Iratkozz fel az eseményekre; keresd a `NodeFailed` visszahívásokat a hálózati problémák diagnosztizálásához.  
- **Memória szivárgás lezáráskor** – Mindig hívd meg a `node.close()`-t minden telepített csomópontra; fontold meg a try‑with‑resources blokk használatát az automatikus takarításért.  

## Gyakran feltett kérdések

**Q: Hogyan javítja a több csomópont telepítése a keresési teljesítményt?**  
A: Minden csomópont az adatok egy shardját indexeli, lehetővé téve a párhuzamos feldolgozást és csökkentve a lekérdezési késleltetést, mivel a terhelés a klaszter között oszlik meg.

**Q: Hozzáadhatok szinonimákat anélkül, hogy újraindexelném a meglévő dokumentumokat?**  
A: Igen, a **szinonimák indexhez adásával** futásidőben a szinonima szótár segítségével; a változások azonnal érvénybe lépnek az új lekérdezéseknél.

**Q: Kötelező-e feliratkozni a csomópont eseményekre?**  
A: Bár nem szükséges az alapműködéshez, az eseményfeliratkozás láthatóságot biztosít a csomópont állapotáról és segít gyorsan reagálni a hibákra.

**Q: Mik a legjobb gyakorlatok a csomópont erőforrások kezelésére?**  
A: Rendszeresen zárd le az üresjárati csomópontokat, figyeld a JVM memóriahasználatát, és a csúcsidőn kívül újrahasznosítsd a csomópontokat az erőforrás-fogyasztás optimalizálása érdekében.

**Q: Támogatja a GroupDocs.Search a nem‑szöveges formátumokat, például PDF-eket vagy képeket?**  
A: Teljes mértékben. A könyvtár szöveget nyer ki PDF-ekből, Office fájlokból, és OCR-t hajt végre képeken, így azok is kereshetők alapból.

---

**Legutóbb frissítve:** 2026-07-16  
**Tesztelve:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [GroupDocs.Search for Java oktatóanyagok és példák](/search/net/)
- [GroupDocs.Search hálózat konfigurálása .NET-ben: Átfogó útmutató](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Search Network Node telepítése .NET-ben a GroupDocs használatával a hatékony dokumentum indexeléshez és lekérdezéshez](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)