---
date: '2026-01-19'
description: Tanulja meg, hogyan konfigurálja a hálózatot és telepíti a GroupDocs.Search
  for Java‑t, beleértve az indexelést, a képes keresést, a csomópont telepítését és
  az eseményfeliratkozást.
keywords:
- GroupDocs.Search Java Network
- Java-based document search network
- configuring and deploying GroupDocs.Search
title: 'Hogyan konfiguráljuk a hálózatot: A GroupDocs.Search Java konfigurációs és
  telepítési útmutató megvalósítása'
type: docs
url: /hu/java/search-network/implement-groupdocs-search-java-network-configuration-deployment/
weight: 1
---

# Hogyan konfiguráljuk a hálózatot a GroupDocs.Search Java-val

## Bevezetés
A mai digitális környezetben a **hálózat konfigurálása** beállítások nagy léptékű dokumentumkereséshez kritikus készség minden vállalat számára. A hagyományos megoldások gyakran teljesítménykorlátba ütköznek, amikor az adathalmaz nő, de a **GroupDocs.Search for Java** skálázható, nagy teljesítményű alapot biztosít. Ebben az útmutatóban végigvezetünk mindenen, amire szükség van egy robusztus keresőhálózat felállításához – a portok konfigurálásától a csomópontok telepítéséig, a dokumentumok indexeléséig, az eseményekre való feliratkozásig, sőt még képes keresés végrehajtásáig.

### Gyors válaszok
- **Mi a keresőhálózat elsődleges célja?** Az indexelés és a lekérdezési terhelés elosztása több csomópont között a jobb skálázhatóság és megbízhatóság érdekében.  
- **Melyik portot használja alapértelmezés szerint a GroupDocs.Search?** A példában a **49120** portot használja, de bármely szabad portot választhat.  
- **Hozzáadhatok vagy eltávolíthatok csomópontokat leállás nélkül?** Igen – a csomópontok dinamikusan telepíthetők vagy visszavonhatók.  
- **Szükségem van licencre a termeléshez?** Teljes licenc szükséges a termelési használathoz; próbaverziók elérhetők értékeléshez.  
- **Támogatott-e a képes keresés alapból?** Igen – a GroupDocs.Search beépített képhash összehasonlítást biztosít.

## Mi az a keresőhálózat?
A keresőhálózat összekapcsolt **SearchNetworkNode** példányok gyűjteménye, amelyek megosztják az indexelési információkat és közösen válaszolnak a lekérdezésekre. Ez az architektúra lehetővé teszi hatalmas dokumentumgyűjtemények kezelését alacsony válaszidő mellett.

## Miért használjuk a GroupDocs.Search for Java-t?
- **Skálázhatóság:** Adjunk hozzá csomópontokat, ahogy a tároló növekszik.  
- **Teljesítmény:** A párhuzamos indexelés és lekérdezésfeldolgozás csökkenti a késleltetést.  
- **Rugalmasság:** Támogatja a szöveget, PDF-et, Office fájlokat és képes keresést.  
- **Esemény‑vezérelt kezelés:** Valós idejű felügyelet eseményfeliratkozásokon keresztül.

## Előkövetelmények
- **JDK 8+** telepítve.  
- Olyan IDE, mint a **IntelliJ IDEA** vagy az **Eclipse**.  
- Maven a függőségkezeléshez.  
- Alapvető Java és hálózati ismeretek.

### Szükséges könyvtárak és függőségek
Adja hozzá a GroupDocs tárolót és függőséget a `pom.xml` fájlhoz:

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

Alternatívaként töltse le a legújabb verziót a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

## A GroupDocs.Search for Java beállítása
### Telepítés Maven-en keresztül
A fenti Maven kódrészlet automatikusan beilleszti a könyvtárat a projektbe.

### Licenc beszerzése
- **Ingyenes próba** – a fő funkciók felfedezése.  
- **Ideiglenes licenc** – meghosszabbított tesztelési időszak.  
- **Teljes licenc** – termelésre kész, korlátlan használat.

### Alap inicializálás és beállítás
```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an instance of Index with the path to store index data.
        String indexPath = "path/to/index";
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Implementációs útmutató
Most minden fő feladatba mélyedünk el, világos, lépésről‑lépésre kódrészletekkel.

### Hogyan telepítsünk csomópontokat egy keresőhálózatban
Több csomópont telepítése elosztja a munkaterhet és javítja a hibatűrést.

```java
public class SearchNetworkDeployment {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY";
        int basePort = 49120; // Change if necessary.
        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        System.out.println("Deployed " + nodes.length + " search network nodes.");
    }
}
```

**Magyarázat:**  
- `basePath` a dokumentumokat tartalmazó mappára mutat.  
- `basePort` a **keresőhálózati port**, amelyen minden csomópont hallgat; állítsa be a konfliktusok elkerülése érdekében.  
- A metódus egy `SearchNetworkNode` objektumok tömbjét adja vissza, amelyek az egyes aktív csomópontokat képviselik.

### Hogyan iratkozzunk fel eseményekre
Az eseményfeliratkozás élő betekintést nyújt a csomópont állapotába, az indexelés előrehaladásába és a hibákba.

```java
public class NodeEventSubscription {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY";
        int basePort = 49120; // Adjust if needed.
        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

        SearchNetworkEvents.subscribe(nodes[0]);
        
        System.out.println("Subscribed to events for the master node.");
    }
}
```

**Magyarázat:**  
- `nodes[0]` **master csomópontként** van kezelve; feliratkozhat egyes munkavégző csomópontokra is külön-külön.

### Hogyan indexeljük a dokumentumokat
A hatékony indexelés a gyors keresési eredmények gerince.

```java
public class DocumentIndexing {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY";
        int basePort = 49120; // Change if there is a conflict.
        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

        IndexingDocuments.addDirectories(nodes[0], "YOUR_DOCUMENT_DIRECTORY");
        
        System.out.println("Added directories to master node's index.");
    }
}
```

**Magyarázat:**  
- `addDirectories` megadja a master csomópontnak, mely mappákat kell beolvasni és indexelni.  
- Az indexelés után minden csomópont lekérdezheti a megosztott indexet.

### Hogyan hajtsunk végre képes keresést
A GroupDocs.Search támogatja a képhash összehasonlítást, lehetővé téve a vizuálisan hasonló elemek megtalálását.

```java
public class ImageSearch {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY";
        int basePort = 49120; // Modify if needed.
        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

        SearchImage searchImage = SearchImage.create("YOUR_DOCUMENT_DIRECTORY/ic_arrow_back_black_18dp.png");

        imageSearch(nodes[0], searchImage, 8);
    }
}
```

**Magyarázat:**  
- `SearchImage.create` betölti a referencia képet.  
- `imageSearch` a kiválasztott csomóponton futtatja a lekérdezést, legfeljebb **8** hash különbséget engedélyezve (állítható szigorúbb vagy lazább egyezéshez).

### Hogyan konfiguráljuk a hálózati portokat
Ha a környezet már a **49120** portot használja, átállíthatja bármely szabad TCP portra:

```java
int customPort = 50000; // Example of a custom port.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, customPort);
```

Győződjön meg róla, hogy a kiválasztott port nyitva van a tűzfalon, és más szolgáltatások nem használják.

## Gyakori problémák és hibaelhárítás
| Tünet | Valószínű ok | Megoldás |
|---------|---------------|-----|
| A csomópontok nem indulnak el | Portütközés | Válasszon másik `basePort`-ot, és frissítse a tűzfal szabályait. |
| Az indexelés lassú | Nem elegendő I/O sávszélesség | Használjon SSD tárolót és engedélyezze az inkrementális indexelést. |
| Az eseményfeliratkozás nem működik | Hiányzó eseménykezelő regisztráció | Győződjön meg róla, hogy a `SearchNetworkEvents.subscribe(node)` hívás megtörténik, mielőtt bármilyen indexelés elkezdődik. |
| A képes keresés nem ad eredményt | A hash különbség túl alacsony | Növelje a megengedett hash különbséget (pl. ran ismételt kérdések

**Q: Hogyan optimalizálhatom az indexelés teljesítményét egy GroupDocs.Search hálózatban?**  
A: Használjon inkrementális indexelést, tárolja az indexet gyors SSD-ken, és biztosítson elegendő heap memóriát a JVM-nek.

**Q: Hozzáadhatok vagy eltávolíthatok csomópontokat a teljes keresőhálózat újraindítása nélkül?**  
A: Igen – a csomópontok dinamikusan telepíthetők vagy visszavonhatók. Czter nézet frissítéséhez.

**Q: Hogyan javítja az eseményfeliratkozás a hálózat menedzsmentjét?**  
A: A feliratkozott riasztásokat biztosítanak a csomópont állapotváltozásairól, az indexelés előrehaladásáról és a hibákról, lehetővé téve a proaktív hibaelhárítást.

**Q: Lehet egyszerre több különböző dokumentumformátumot keresni?**  
A: Természetesen. Aól függ. Alkalópvesse a legjobb adatvédelmi gyakorlatokat.

---

**Utolsó frissítés:** 2026-01-19  
**Tesztelve:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs