---
date: '2025-12-26'
description: Tanulja meg, hogyan hozhat létre kereshető indexet Java‑ban a GroupDocs.Search
  for Java segítségével, hogyan adhat hozzá fájlokat a kereséshez, és hogyan adhat
  hozzá könyvtárakat a csomóponthoz.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: Kereshető index létrehozása Java-ban – A GroupDocs.Search for Java telepítése
type: docs
url: /hu/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# Kereshető Index Létrehozása Java – GroupDocs.Search for Java Telepítése

A mai adat‑központú világban a **creating a searchable index java** alkalmazásoknak hatékonyan kell kezelniük a hatalmas dokumentumgyűjteményeket. Akár vállalati szintű keresési szolgáltatást, akár kisebb projektet építesz, egy jól konfigurált keresési hálózat drámaian javíthatja a visszakeresés sebességét és relevanciáját. Ebben az útmutatóban végigvezetünk a **GroupDocs.Search for Java** beállításának teljes folyamatán, a kereséshez fájlok hozzáadásától a könyvtárak node‑hoz adásáig, hogy azonnal elkezdhesd a dokumentumok indexelését.

## Gyors Válaszok
- **What is the primary purpose of GroupDocs.Search?** A skálázható, Java‑alapú motor biztosítása a dokumentumok indexelésére és keresésére egy elosztott hálózaton.  
- **Which version should I use?** Az új projektekhez a legújabb stabil kiadás (pl. 25.4) ajánlott.  
- **Do I need a license?** 30‑napos ingyenes próba elérhető; a termelési használathoz állandó licenc szükséges.  
- **Can I add both files and whole directories?** Igen – használja a `addFiles` és `addDirectories` segédfüggvényeket a tartalom betöltéséhez.  
- **What Java version is required?** Java 8 vagy újabb, Maven a függőségkezeléshez.

## Mi az a “create searchable index java”?
A kereshető index létrehozása Java-ban azt jelenti, hogy egy olyan adatstruktúrát építünk, amely a kifejezéseket a tartalmazó dokumentumokhoz rendeli, lehetővé téve a gyors teljes szöveges lekérdezéseket. A GroupDocs.Search elvégzi a nehéz munkát, így Ön a dokumentumok betáplálására és a keresési viselkedés finomhangolására koncentrálhat.

## Miért használjuk a GroupDocs.Search for Java‑t?
- **Scalable network architecture** – Több node telepítése, amely megosztja az indexelési terhelést.  
- **Rich document format support** – PDF‑ek, Word, Excel, PowerPoint, képek és egyebek.  
- **Event‑driven updates** – Iratkozzon fel a node eseményekre, hogy a index valós időben friss maradjon.  
- **Simple Maven integration** – Néhány sor hozzáadása a `pom.xml`‑hez, és kezdje el az indexelést.

## Előkövetelmények
- **JDK 8+** telepítve a fejlesztői gépen.  
- Egy IDE, például **IntelliJ IDEA** vagy **Eclipse**.  
- Alapvető ismeretek a **Java**‑ról és a **Maven**‑ról.  
- Hozzáférés a **GroupDocs.Search for Java** könyvtárhoz (letöltés vagy Maven).

## A GroupDocs.Search for Java beállítása

### Maven függőség
Adja hozzá a tárolót és a függőséget a `pom.xml`‑hez:

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

> **Pro tip:** Tartsa naprakészen a verziószámot az hivatalos kiadások oldalának ellenőrzésével.

A JAR‑t közvetlenül is letöltheti a hivatalos oldalról: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenc Beszerzése
- **Free Trial:** 30‑napos értékelés.  
- **Temporary License:** Kérjen hosszabb teszteléshez.  
- **Purchase:** Szükséges a termelési telepítésekhez.

### Alap Inicializálás
Hozzon létre egy konfigurációs objektumot, amely egy mappára mutat, ahol az indexfájlok tárolódnak, és meghatározza az alap kommunikációs portot:

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

## Hogyan hozhatunk létre searchable index java‑t a GroupDocs.Search‑szal?
Az alábbiakban bontjuk le a fő funkciókat, amelyekre szüksége lesz a **add files to search** és a **add directories to node** végrehajtásához, miközben egy skálázható hálózatot telepít.

### 1. funkció – Konfiguráció és Hálózati Beállítás
A keresési hálózat konfigurálása az első lépés a kereshető index felépítése felé.

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

- **`basePath`** – Könyvtár, ahol az indexadatok tárolódnak.  
- **`basePort`** – Kezdő port; minden node ezt az értéket növeli.

### 2. funkció – Keresési Hálózati Node-ok Telepítése
A node-ok telepítése elosztja az indexelési terhelést több gép vagy folyamat között.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

Minden `SearchNetworkNode` saját indexelési szolgáltatást futtat, lehetővé téve, hogy **create a searchable index java** vízszintesen skálázható legyen.

### 3. funkció – Node Eseményekre Feliratkozás
A valós idejű frissítések szinkronban tartják az indexet a fájlrendszer változásaival.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

Az események figyelésével automatikusan indíthatja az új fájlok érkezésekor a re‑indexelést.

### 4. funkció – Könyvtárak Hozzáadása a Hálózati Node-hoz
Használja ezt a segédfüggvényt a **add directories to node** végrehajtásához, rekurzívan összegyűjtve az összes támogatott dokumentumot.

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

### 5. funkció – Fájlok Hozzáadása a Hálózati Node-hoz
Ha finomhangolt vezérlésre van szükség, **add files to search** egyenként:

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

Ez a módszer rugalmasságot biztosít a streamekből, felhő tárolóból vagy ideiglenes helyekről származó fájlok indexeléséhez.

## Gyakori Problémák és Megoldások
| Probléma | Ok | Megoldás |
|----------|----|----------|
| **Nem jelennek meg dokumentumok a keresési eredményekben** | Az index nincs elkötelezve | Hívja meg a `node.getIndexer().commit()`‑t a fájlok hozzáadása után. |
| **Port ütközés hiba** | Egy másik szolgáltatás használja a `basePort`‑ot | Válasszon másik `basePort`‑ot, vagy ellenőrizze a szabad portokat. |
| **Nem támogatott fájlformátum** | A könyvtár nem tartalmaz parsert | Győződjön meg róla, hogy a fájlkiterjesztés támogatott, vagy adjon hozzá egy egyedi kinyerőt. |

## Gyakran Ismételt Kérdések

**Q: Használhatom a GroupDocs.Search‑t felhőalapú Java alkalmazásban?**  
A: Igen. A könyvtár bármely Java futtatókörnyezettel működik, és a `basePath`‑t egy hálózati csatolt mappára vagy helyileg csatolt felhő tárolóra mutathatja.

**Q: Hogyan frissíthetem az indexet, ha egy fájl megváltozik?**  
A: Iratkozzon fel a node eseményekre (lásd 3. funkció), és hívja meg újra a `addFiles` vagy `addDirectories`‑t a módosított útvonalakra.

**Q: Van korlátja a telepíthető node-ok számának?**  
A: Gyakorlatilag a korlátot a hardver és a hálózati sávszélesség határozza meg. Az API önmagában nem szab korlátot.

**Q: Új fájlok hozzáadása után újra kell indítanom a node-okat?**  
A: Nem. A fájlok hozzáadása automatikusan elindítja az indexelést; csak akkor kell elkötelezni, ha késlelteti a műveletet.

**Q: Mely dokumentumformátumok támogatottak alapból?**  
A: PDF‑ek, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML és számos képformátum. Lásd a hivatalos dokumentációt a teljes listáért.

---

**Legutóbb frissítve:** 2025-12-26  
**Tesztelve ezzel:** GroupDocs.Search for Java 25.4  
**Szerző:** GroupDocs