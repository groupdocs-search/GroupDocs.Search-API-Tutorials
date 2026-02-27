---
date: '2026-02-27'
description: Tanulja meg, hogyan hozhat létre kereshető indexet Java-ban a GroupDocs.Search
  for Java segítségével, hogyan adhat fájlokat a kereséshez, hogyan adhat könyvtárakat
  a csomóponthoz, és hogyan engedélyezheti a valós idejű indexelést Java-ban.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: Kereshető index létrehozása Java – A GroupDocs.Search for Java telepítése
type: docs
url: /hu/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# Kereshető Index Létrehozása Java – GroupDocs.Search for Java Telepítése

A mai adat‑központú világban a **kereshető index létrehozása Java** alkalmazásoknak hatékonyan kell kezelniük hatalmas dokumentumgyűjteményeket. Akár egy vállalati szintű keresési szolgáltatást, akár egy kisebb projektet építesz, egy jól konfigurált keresési hálózat drámaian javíthatja a lekérdezés sebességét és relevanciáját. Ebben az útmutatóban végigvezetünk a **GroupDocs.Search for Java** beállításának teljes folyamatán, a fájlok kereséshez való hozzáadásától a könyvtárak node‑hoz való hozzáadásáig, így azonnal elkezdheted a dokumentumok indexelését.

> **Miért fontos:** A kereshető index csökkenti a lekérdezési késleltetést másodpercről ezredmásodpercre, skálázható az adatmennyiség növekedésével, és lehetővé teszi erőteljes teljes‑szöveges képességek hozzáadását bármely Java‑alapú megoldáshoz – legyen az egy webportál, asztali alkalmazás vagy felhő mikro‑szolgáltatás.

## Gyors Válaszok
- **Mi a GroupDocs.Search elsődleges célja?** Egy skálázható, Java‑alapú motor biztosítása a dokumentumok indexeléséhez és kereséséhez egy elosztott hálózaton.  
- **Melyik verziót kellene használnom?** A legújabb stabil kiadás (pl. 25.4) ajánlott új projektekhez.  
- **Szükségem van licencre?** 30‑napos ingyenes próba elérhető; a termelési használathoz állandó licenc szükséges.  
- **Hozzáadhatok fájlokat és teljes könyvtárakat is?** Igen – használja az `addFiles` és `addDirectories` segédfüggvényeket a tartalom betöltéséhez.  
- **Milyen Java verzió szükséges?** Java 8 vagy újabb, Maven a függőségkezeléshez.  
- **Hogyan működik a valós idejű indexelés Java?** A node eseményekre feliratkozva automatikusan újra‑indexelheted a fájlok változásakor.

## Mi az a „kereshető index létrehozása Java”?
A kereshető index létrehozása Java‑ban azt jelenti, hogy egy adatstruktúrát építünk, amely a kifejezéseket a tartalmazó dokumentumokhoz rendeli, lehetővé téve a gyors teljes‑szöveges lekérdezéseket. A GroupDocs.Search elvégzi a nehéz munkát, így a dokumentumok betáplálására és a keresési viselkedés finomhangolására koncentrálhatsz.

## Miért használjuk a GroupDocs.Search for Java‑t?
- **Skálázható hálózati architektúra** – Több node telepítése, amelyek megosztják az indexelési terhelést.  
- **Gazdag dokumentumformátum támogatás** – PDF‑ek, Word, Excel, PowerPoint, képek és még több.  
- **Esemény‑vezérelt frissítések** – Node eseményekre feliratkozva a indexet valós időben frissen tartod.  
- **Egyszerű Maven integráció** – Néhány sor hozzáadása a `pom.xml`‑hez, és elkezdheted az indexelést.

## Valós idejű indexelés Java a GroupDocs.Search segítségével
A GroupDocs.Search eseményeket vált ki, amikor egy fájl hozzáadódik, frissül vagy eltávolításra kerül. Ezeknek az eseményeknek a kezelése során automatikusan meghívhatod az `addFiles` vagy `addDirectories` metódusokat, biztosítva, hogy az index manuális beavatkozás nélkül szinkronban maradjon. Ez a megközelítés ideális dokumentumkezelő rendszerekhez, tartalmi portálokhoz és minden olyan alkalmazáshoz, ahol az adatok gyakran változnak.

## Előfeltételek
- **JDK 8+** telepítve a fejlesztői gépeden.  
- Egy IDE, például **IntelliJ IDEA** vagy **Eclipse**.  
- Alapvető ismeretek a **Java** és **Maven** használatáról.  
- Hozzáférés a **GroupDocs.Search for Java** könyvtárhoz (letöltés vagy Maven).

## A GroupDocs.Search for Java beállítása

### Maven függőség
Add the repository and dependency to your `pom.xml`:

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

> **Pro tip:** Keep the version number up‑to‑date by checking the official releases page.

You can also download the JAR directly from the official site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
- **Free Trial:** 30‑day evaluation.  
- **Temporary License:** Request for extended testing.  
- **Purchase:** Required for production deployments.

### Basic Initialization
Create a configuration object that points to a folder where index files will be stored and defines the base communication port:

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## Hogyan hozható létre kereshető index Java‑val a GroupDocs.Search‑el?

Alább részletezzük a főbb funkciókat, amelyekre szükséged lesz a **fájlok kereséshez való hozzáadása** és a **könyvtárak node‑hoz való hozzáadása** során, miközben egy skálázható hálózatot is telepítesz.

### Feature 1 – Configuration and Network Setup
Configuring the search network is the first step toward building a searchable index.

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – Directory where the index data will be persisted.  
- **`basePort`** – Starting port; each node will increment from this value.

### Feature 2 – Deploying Search Network Nodes
Deploying nodes distributes indexing workload across multiple machines or processes.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

Each `SearchNetworkNode` runs its own indexing service, enabling you to **create a searchable index java** that scales horizontally.

### Feature 3 – Subscribing to Node Events
Real‑time updates keep the index synchronized with file system changes.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

By listening to events, you can automatically trigger re‑indexing when new files arrive.

### Feature 4 – Adding Directories to Network Node
Use this helper to **add directories to node**, recursively collecting all supported documents.

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

### Feature 5 – Adding Files to Network Node
When you need fine‑grained control, **add files to search** individually:

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

This method gives you the flexibility to index files coming from streams, cloud storage, or temporary locations.

## Gyakori felhasználási esetek
- **Vállalati dokumentumportálok**, amelyeknek azonnali keresésre van szükségük több ezer PDF‑en és Office‑fájlon.  
- **Jogi e‑discovery platformok**, ahol az új bizonyítékok folyamatosan érkeznek és valós időben kereshetők kell legyenek.  
- **Tartalomkezelő rendszerek**, amelyek képeket, prezentációkat és táblázatokat tárolnak, és teljes‑szöveges keresést igényelnek.

## Gyakori problémák és megoldások
| Probléma | Ok | Megoldás |
|-------|--------|-----|
| **Nem jelennek meg dokumentumok a keresési eredményekben** | Index nincs commit‑olva | Hívd meg a `node.getIndexer().commit()` metódust a fájlok hozzáadása után. |
| **Port konfliktus hiba** | Egy másik szolgáltatás használja a `basePort`‑ot | Válassz másik `basePort`‑ot vagy ellenőrizd a szabad portokat. |
| **Nem támogatott fájlformátum** | A könyvtár nem tartalmaz parser‑t | Győződj meg róla, hogy a fájlkiterjesztés támogatott, vagy adj hozzá egy egyedi extraktort. |

## Hibaelhárítási tippek
- **Node állapot ellenőrzése:** Használd a beépített health‑check végpontot (`http://localhost:{port}/health`) a node‑ok futásának megerősítéséhez.  
- **Memóriahasználat figyelése:** Nagy dokumentumcsoportok memóriát terhelhetnek; indexelj kisebb adagokban, és időnként hívd meg a `commit()`‑ot.  
- **Naplók ellenőrzése:** A GroupDocs.Search részletes naplókat ír a `basePath` mappába – nézd át őket a feldolgozási hibák vagy hálózati időtúllépések miatt.

## Gyakran Ismételt Kérdések

**Q: Használhatom a GroupDocs.Search‑t felhő‑alapú Java alkalmazásban?**  
A: Igen. A könyvtár bármely Java runtime‑sal működik, és a `basePath`‑t beállíthatod egy hálózaton megosztott mappára vagy helyileg csatolt felhő tárolóra.

**Q: Hogyan frissíthetem az indexet, ha egy fájl megváltozik?**  
A: Iratkozz fel a node eseményekre (lásd Feature 3) és hívd meg újra az `addFiles` vagy `addDirectories` metódusokat a módosított útvonalakra.

**Q: Van korlátozás a telepíthető node‑ok számát illetően?**  
A: Gyakorlatilag a határ a hardvered és a hálózati sávszélességed által meghatározott. Az API maga nem szab korlátot.

**Q: Új fájlok hozzáadása után újra kell indítani a node‑okat?**  
A: Nem. A fájlok hozzáadása automatikusan elindítja az indexelést; csak akkor kell commit‑olni, ha késlelteted a műveletet.

**Q: Mely dokumentumformátumok támogatottak alapból?**  
A: PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML és számos képformátum. A teljes listáért tekintsd meg a hivatalos dokumentációt.

**Q: Hogyan aktiválhatom a valós idejű indexelést Java‑val egy folyamatosan feltöltött mappához?**  
A: Implementálj egy fájlrendszer‑figyelőt (pl. `java.nio.file.WatchService`), amely a `DirectoryAdder.addDirectories(node, path)`‑t hívja meg minden új fájl észlelésekor.

---

**Utoljára frissítve:** 2026-02-27  
**Tesztelve a következővel:** GroupDocs.Search for Java 25.4  
**Szerző:** GroupDocs