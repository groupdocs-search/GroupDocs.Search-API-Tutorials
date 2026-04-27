---
date: '2026-01-19'
description: Tanulja meg, hogyan konfigurálja az elosztott keresést, és telepítsen
  egy erőteljes keresési hálózatot a GroupDocs.Search for Java használatával, javítva
  a teljesítményt és a skálázhatóságot.
keywords:
- GroupDocs.Search Java network
- search performance enhancement
- distributed search architecture
title: Elosztott keresés konfigurálása a GroupDocs.Search Java Network segítségével
type: docs
url: /hu/java/search-network/deploy-groupdocs-search-java-network/
weight: 1
---

# Elosztott keresés konfigurálása a GroupDocs.Search Java háló elengedhetetlen a hatalmas dokumentumgyűjtemények kezelése és az alacsony válaszidők fenntartása érdekében. Ez az útmutató végigére egyoldással lesz a rendelkezésére, amely készen áll a termelésre.

## Gyors válaszok
- **Mi az elosztott keresés konfigurálása?** Ez a folyamat több keresőcsomópont beállítását jelenti, amelyek együtt dolgoznak az adatok hatékony indexelésére és lekérdezésére.  
- **Hány csomópont ajánlott?** Általában 3‑5 csomópont biztosítja a jó egyensúlyt a teljesítmény és a hibatűrés között.  
- **Szükségem van licencre?** Igen – egy ideiglenes vagy teljes licenc szükséges a termelési használathoz.  
- **Mely portokat kell használni?** Válasszon olyan portokat, amelyek szabadok a szerverein; a példában a 49136‑49139 portokat használjuk.  
- **Hozzáadhatok új dokumentumokat a telepítés után?** Természetesen – bármikor **hozzáadhat dokumentumokat az indexhez** a hálózat újraindítása nélkül.  

## Mi az elosztott keresés konfigurálása?
Az elosztott keresési architektúra konfigurálása azt jelenti, hogy több független keresőcsomópontot összekapcsolunk, hogy közösen végezzék az indexelési feladatokat és közösen válaszoljanak a lekérdezésekre. Ez csökkenti az egyetlen gépre nehezedő terhelést, és javítja mind a teljesítményt, mind a megbízhatóságot.

## Miért használja a GroupDocs.Search for Java-t?
- **Magas teljesvalósítás optimalizálja az indexelés sebességét.  
- **Skálázható tervezés** – csomópontok hozzáadása vagy eltávolítása jelentős újrakonfigurálás nélkül.  
- **Gazdag dokumentumtámogatás** – működik PDF-ekkel, Word fájlokkal, e‑mail üzenetekkel és egyebekkel.  
- **Egyszerű TCP kommunikáció** – a beépített `TcpSettings` lehetővé teszi a hálózati késleltetés finomhangolását.  

## Előkövetelmények

### Szükséges könyvtárak és függőségek
Szüksége lesz **GroupDocs.Search for Java** 25.4 vagy újabb verzióra. Győződjön meg róla, hogy a fejlesztői környezetben telepítve van a Java.

### Környezet beállítási követelmények
- A Java Development Kit (JDK) telepítve van a gépén  
- Egy IDE, például IntelliJ IDEA vagy Eclipse  

### Tudás előkövetelmények
Alapvető Java programozási ismeretek és a hálózati konfiguráció általános megértése segíti a lépések zökkenőmentes követését.

## A GroupDocs.Search for Java beállítása
A kezdéshez adja hozzá a GroupDocs.Search for Java-t a projektjéhez. Ezt egyszerűen megteheti Maven-en keresztül vagy a könyvtár közvetlen letöltésével.

**Maven beállítás**  
Adja hozzá a következő tárolót és függőségkonfigurációt a `pom.xml` fájlhoz:

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

**Közvetlen letöltés**  
Alternatívaként töltse le a legújabb verziót a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc beszerzése
A GroupDocs.Search teljes kihasználásához szerezhet ideiglenes licencet vagy vásárolhat egyet. Látogassa meg a [GroupDocs licencoldalát](https://purchase.groupdocs.com/temporary-license/) a ingyenes próba vagy teljes licenc beszerzésének részleteiért.

### Alapvető inicializáljuk a GroupDocs.Search-t a Java alkalmazásában:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an index in the specified folder
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        // Add documents to the index
        index.add("YOUR_DOCUMENT_DIRECTORY");
    }
}
```

## Implementációs útmutató
Ebben a szakaszban végigvezetjük aáljuk az elosáljuk ezeket a csomópontokat hatékonyan.

#### A hálózat konfigurálása
Kezdje a konfiguráció beállításával egy alapútvonallal és porttal. Ez a lépés **konfigurálja a TCP beállításokat**, amelyek meghatározzák, hogyan kommunikálnak a csomópontok:

```java
Configuration configuration = ConfiguringSearchNetwork.configure("YOUR_DOCUMENT_DIRECTORY", 49136);
```

#### Csomópontok telepítése
Ezután telepítse a keresőhálózat csomópontjait a konfigurált beállítások használatával:

```java
public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
    // Define timeouts for sending and receiving data over the network.
    int sendTimeout = 3000;
    int receiveTimeout = 3000;

    // Create and start three nodes that can run on separate servers or together.
    SearchNetworkNode node1 = new SearchNetworkNode(
        1,
        basePath + "Node1",
        new TcpSettings(basePort + 1, sendTimeout, receiveTimeout)
    );
    node1.start();

    SearchNetworkNode node2 = new SearchNetworkNode(
        2,
        basePath + "Node2",
        new TcpSettings(basePort + 2, sendTimeout, receiveTimeout)
    );
    node2.start();

    SearchNetworkNode node3 = new SearchNetworkNode(
        3,
        basePath + "Node3",
        new TcpSettings(basePort + 3, sendTimeout, receiveTimeout)
    );
    node3.start();

    // Create and configure the main configuration node.
    SearchNetworkNode node0 = new SearchNetworkNode(
        0,
        basePath + "Node0",
        new TcpSettings(basePort, sendTimeout, receiveTimeout),
        new ConsoleLogger(),
        configuration
    );

    // Add an event handler to notify when the configuration is complete.
    node0.getEvents().ConfigurationCompleted.add(new EventHandler() {
        @Override
        public void invoke(Object s, EventArgs e) {
            // Event handling logic here (e.g., logging)
        }
    });

    // Configure all nodes in the network using the main configuration node.
    node0.configureAllNodes();

    // Start the search network by launching all configured nodes.
    node0.start();

    // Return an array of all deployed nodes.
    return new SearchNetworkNode[] {node0, node1, node2, node3};
}
```

### Hibaelhárítási tippek
- Győződjön meg arról, hogy minden csomópont könyvtára helyesen van megadva és elérhető.  
- Ellenőrizze a hálózati konfigurációkat, különösen a portbeállításokat, hogy elkerülje az ütközéseket.  
- Figyelje a naplókat bármilyen konfigurációs hiba vagy figyelmeztetés esetén.  

## Gyakorlati alkalmazások
Egy elosztott keresőhálózat telepítése számos helyzetben előnyös lehet:

1. **Nagy léptékű vállalati rendszerek** – Javítja a keresést kiterjedt dokumentumtárakban.  
2. **Tartalomkezelő platformok** – Növeli a teljesítményt nagy forgalmú, hatalmas adatvolumenű oldalakon.  
3. **E‑kereskedelmi weboldalak** – Gyorsítja a termékkereséseket a zökkenőmentes vásárlói élmény érdekében.  

## Teljesítményfontosságú szempontok
Az **elosztott keresés konfigurálása** környezet hatékony működésének fenntartásához:

- Rendszeresen frissítse az indexeket az adatváltozások tükrözésére.  
- Figyelje a CPU, memória és lemezhasználatot; szükség esetén állítsa be a `TcpSettings` időkorlátokat.  
- Alkalmazzon Java memóriahangoló zászlókat (`-Xmx`, `-Xms`) a terhelés alapján.  

## Következtetés
Az útmutató követésével megtanulta, hogyan **konfigurálja az elosztott keresést** és telepítsen egy skálázható GroupDocs.Search Java hálózatot. Ez a megoldás drámaian javíthatja alkalmazása keresési funkcióinak sebességét és megbízhatóságát.

### Következő lépések
Fedezze fel a fejlett funkciókat, például az egyedi elemzőket, szinonima kezelést és a valós idejű indexelést a keresési élmény további finomításához.

### Felhívás a cselekvésre
Kezdje el ma alkalmazni ezt a robusztus megoldást a projektjeiben, és tapasztalja meg saját szemével a teljesítményjavulást!

## GyIK szekció
**Q1: Mi az a GroupDocs.Search for Java?**  
A1: A GroupDocs.Search for Java egy erőteljes könyvtár szöveges keresések végrehajtására különböző dokumentumformátumokban, lehetővé téve a hatékony indexelést és lekérdezési képességeket.

**Q2: Hogyan szerezhetek ideiglenes licencet a GroupDocs.Search-hez?**  
A2: Látogassa meg a [GroupDocs licencoldalát](https://purchase.groupdocs.com/temporary-license/) egy ingyenes próba vagy teljes licenc beszerzéséhez.

**Q3: Használható ez a hálózati konfiguráció más dokumentumtípusokkal is?**  
A3: Igen, a GroupDocs.Search számos dokumentumformátumot támogat, így sokféle felhasználási esetben alkalmazható.

**Q4: Milyen gyakori problémák merülnek fel a csomópontok telepítésekor?**  
A4: Gyakori problémák közé tartozik a helytelenül konfigurált könyvtárak, portütközések és a nem megfelelő jogosultságok. Győződjön meg róla, hogy minden beállítás helyesen van alkalmazva a problémák elkerülése érdekében.

---

**Utolsó frissítés:** 2026-01-19  
**Tesztelve ezzel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs