---
date: '2026-01-16'
description: Tanulja meg, hogyan végezzen szöveges keresést és optimalizálja a keresési
  teljesítményt a GroupDocs.Search for Java segítségével. Tartalmazza a keresési hálózat
  beállításának, kereshető index létrehozásának és a dokumentumindex törlésének lépéseit.
keywords:
- GroupDocs.Search for Java
- search network optimization
- document indexing with GroupDocs
title: Szövegkeresés végrehajtása a GroupDocs.Search for Java-val
type: docs
url: /hu/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Perform Text Search with GroupDocs.Search for Java
## Performance Optimization
## How to Implement and Optimize a Search Network with GroupDocs.Search for Java

### Introduction
A mai adatvezérelt világban a **perform text search** gyors végrehajtásának képessége a hatalmas dokumentumgyűjteményekben versenyelőnyt jelent. Akár belső tudásbázist, jogi esetek tárolóját vagy egy e‑kereskedelmi termékkatalógust építesz, egy jól hangolt keresési hálózat jelentősen javíthatja a felhasználói elégedettséget. Ebben az útmutatóban megtanulod, hogyan **set up search network**, **create searchable index**, **optimize search performance**, és akár **delete documents index** is szükség esetén – mindezt a GroupDocs.Search for Java használatával.

**What You'll Learn**
- Keresési hálózat konfigurálása a GroupDocs.Search segítségével  
- Csomópontok telepítése a hálózaton belül  
- Dokumentumok hatékony indexelése (`index documents java`)  
- Szövegkeresések végrehajtása a hálózaton (`perform text search`)  
- Specifikus dokumentumok törlése az indexből (`delete documents index`)  

Merüljünk el abban, hogyan használhatod ki ezeket a funkciókat egy optimalizált keresési élmény létrehozásához.

## Quick Answers
- **Mi a GroupDocs.Search for Java fő célja?** Teljes szöveges keresést biztosít számos dokumentumformátumon.  
- **Hogyan hajtható végre szövegkeresés elosztott környezetben?** Telepíts egy keresési hálózatot, indexeld a dokumentumokat egy master csomóponton, majd kérdezz le bármelyik csomópontot.  
- **Törölhetek dokumentumokat az indexből anélkül, hogy újraépíteném?** Igen, használd a Delete API-t a kiválasztott fájlok eltávolításához.  
- **Milyen Java verzió szükséges?** JDK 8 vagy újabb.  
- **Szükséges licenc a termeléshez?** Érvényes GroupDocs.Search licenc szükséges; ingyenes próba elérhető.

## What is “perform text search”?
A szövegkeresés végrehajtása azt jelenti, hogy egy teljes szöveges indexet kérdezünk le, hogy olyan dokumentumokat kapjunk, amelyek tartalmazzák a megadott kulcsszavakat vagy kifejezéseket. A GroupDocs.Search egy fordított indexet épít, amely ezeknek a kereséseknek a végrehajtását rendkívül gyorsá teszi, még több ezer fájl esetén is.

## Why set up a search network?
A keresési hálózat elosztja az indexelési és lekérdezési terhelést több csomópont között, lehetővé téve a **optimize search performance**, a horizontális skálázást és a magas rendelkezésre állás fenntartását. Ez az architektúra ideális vállalati szintű dokumentumtárolók számára, ahol a késleltetés és a sávszélesség fontos.

### Prerequisites
- **Szükséges könyvtárak:** GroupDocs.Search for Java 25.4 (legújabb).  
- **Környezet:** Java JDK 8+, Maven.  
- **Ismeretek:** Alap Java programozás és hálózati koncepciók ismerete.

### Setting Up GroupDocs.Search for Java
A kezdéshez integráld a GroupDocs.Search-et a Java projektedbe az alábbi beállításokkal:

#### Maven Setup
Add the repository and dependency to your `pom.xml` file:

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

#### Direct Download
Alternatively, you can [download the latest version directly from GroupDocs](https://releases.groupdocs.com/search/java/).

#### License Acquisition
GroupDocs offers a free trial, which allows you to evaluate its features before purchase. You can obtain a temporary license by following the steps on their [purchase page](https://purchase.groupdocs.com/temporary-license/). This will enable full functionality during your testing phase.

#### Basic Initialization and Setup
Initialize GroupDocs.Search in your Java application with:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

### Implementation Guide

#### Configuring the Search Network
**Overview:** Áttekintés: Állíts be egy alapútvonalat és portot a keresési hálózatodhoz, hogy a csomópontok hatékonyan kommunikálhassanak.

##### Step 1: Define Base Configuration
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Paraméterek:**  
  - `basePath`: Könyvtár útvonal a hálózati műveletekhez.  
  - `basePort`: A keresési hálózat által használt portszám.

##### Step 2: Troubleshooting
Győződj meg arról, hogy a megadott portot nem blokkolja a tűzfal, vagy nem használja másik alkalmazás. Szükség szerint módosítsd a konfliktusok elkerülése érdekében.

#### Deploying Search Network Nodes
**Overview:** Áttekintés: A konfigurációddal telepíts csomópontokat a hálózatodban elosztott indexeléshez és kereséshez.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Kulcsfontosságú konfigurációs beállítások:**  
  - **Base Path & Port:** Ezeknek az értékeknek meg kell egyezniük az első konfigurációban használtakkal a konzisztencia biztosítása érdekében.

#### Indexing Documents (`create searchable index`)
**Overview:** Áttekintés: Dokumentumok hatékony hozzáadása a keresési indexhez egy master csomópont használatával.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Cél:**  
  - `masterNode`: Az elsődleges csomópont, amely a dokumentumok indexelését kezeli.  
  - `documentsPath`: Az a könyvtár útvonal, amely a dokumentumokat tartalmazza.

##### Troubleshooting Tips
Ellenőrizd, hogy a dokumentum útvonalak helyesek és elérhetők. Győződj meg róla, hogy a jogosultságok engedélyezik a könyvtárak olvasását.

#### Searching Text in Network (`perform text search`)
**Overview:** Áttekintés: Átfogó szöveges keresések végrehajtása az indexelt hálózaton.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Paraméterek:**  
  - `query`: A keresett szöveg.  
  - `masterNode`: A keresést végző csomópont.

#### Deleting Documents from Index (`delete documents index`)
**Overview:** Áttekintés: Specifikus dokumentumok eltávolítása az indexből a fájl útvonalak segítségével.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Metódus célja:**  
  - `node`: A célcsoport csomópont a törlési műveletekhez.  
  - `filePaths`: Az indexből eltávolítandó dokumentumok útvonalai.

##### Troubleshooting
Győződj meg arról, hogy a fájl útvonalak pontosak és a fájlok léteznek a könyvtárban. Ha a problémák továbbra is fennállnak, ellenőrizd a hálózati jogosultságokat és a kapcsolódást.

### Practical Applications
1. **Vállalati dokumentumkezelés:** Belső tudáslekérdezés egyszerűsítése.  
2. **Jogi esetek elemzése:** Gyorsan megtalálni a releváns esetfájlokat több tárolóban.  
3. **E‑kereskedelmi platformok:** A termékkeresés sebességének növelése leírások és vélemények indexelésével.  
4. **Akademiai kutatás:** Nagy digitális könyvtárak, tanulmányok és szakdolgozatok hatékony keresése.  
5. **Ügyfélszolgálati rendszerek:** Válaszidő csökkentése azáltal, hogy az ügyintézők azonnal kereshetnek a korábbi jegyek között.

### Performance Considerations
- **Az indexelés sebességének optimalizálása:** Új dokumentumok fokozatos hozzáadása csúcsidőn kívül, hogy alacsony maradjon a késleltetés.  
- **Erőforrás-használati irányelvek:** Figyeld a CPU-t és a memóriát, különösen a csomópontok számának növelésekor.  
- **Java memória kezelése:** Állítsd be a JVM heap beállításokat a terhelés alapján (pl. `-Xmx2g` közepes méretű indexekhez).

### Conclusion
Az útmutató követésével megtanultad, hogyan **set up search network**, **create searchable index**, **perform text search**, és **delete documents index** a GroupDocs.Search for Java segítségével. Ezek a képességek gyors és megbízható dokumentumlekérdezést tesznek lehetővé elosztott környezetekben.

**Next Steps**
- Kísérletezz különböző csomópont konfigurációkkal, hogy megtaláld a terhelésedhez legoptimálisabb egyensúlyt.  
- Mélyedj el a fejlett indexelési lehetőségekben, mint az egyedi elemzők és a relevancia finomhangolása.  
- Fedezd fel a integrációt más GroupDocs termékekkel az átfogó dokumentumfeldolgozáshoz.

## Frequently Asked Questions

**Q: Mi a fő felhasználási eset a GroupDocs.Search for Java esetén?**  
A: Teljes szöveges keresést biztosít számos dokumentumformátumon, lehetővé téve a **perform text search** nagy tárolókban.

**Q: Hogyan javíthatom a keresés sebességét egy nagy hálózatban?**  
A: Telepíts további csomópontokat, hangold a JVM heap-et, és ütemezd az indexelést alacsony forgalmú időszakokra a **optimize search performance** érdekében.

**Q: Lehetséges egyetlen dokumentumot törölni anélkül, hogy újraindexelné az egész gyűjteményt  
A: Igen, használd a **delete documents index** API-t, ahogy a kódpéldában látható, a specifikus fájlok eltávolításához.

**Q: Szükségem van licencre a fejlesztéshez?**  
A: Egy ingyenes próba licenc elegendő a teszteléshez; a termelési környezethez kereskedelmi licenc szükséges.

**Q: Indexelhetek PDF-eket, Word fájlokat és e‑mail üzeneteket együtt?**  
A: Természetesen— a GroupDocs.Search alapból támogat számos formátumot.

---

**Last Updated:** 2026-01-16  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs