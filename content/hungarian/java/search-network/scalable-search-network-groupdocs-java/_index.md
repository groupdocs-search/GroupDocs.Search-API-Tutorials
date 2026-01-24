---
date: '2026-01-24'
description: Tanulja meg, hogyan konfigurálja az alap port groupdocs-ot a skálázható
  keresőhálózatokhoz a GroupDocs.Search Java használatával, optimalizálja a lekérdezési
  sebességet, és állítson be többcsomópontos rendszereket.
keywords:
- scalable search network
- GroupDocs.Search Java configuration
- multi-node search setup
title: Alap port groupdocs beállítása a Java Search Networkben
type: docs
url: /hu/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Base port groupdocs konfigurálása Java keresési hálózatban

A modern, adat‑intenzív alkalmazásokban a **configuring base port groupdocs** alapvető lépés egy gyors, megbízható keresési infrastruktúra kiépítéséhez. Akár több ezer PDF‑et kezel, akár több szerveren skáláz, a megfelelő portok és útvonalak beállítása biztosítja, hogy minden csomópont konfliktus nélkül kommunikáljon a többiekkel. Ez az útmutató minden részletet bemutat – az előkövetelményektől a teljes több‑csomópontos konfigurációig –, hogy magabiztosan indíthasson egy skálázható keresési hálózatot a GroupDocs.Search for Java‑val.

## Gyors válaszok
- **Mi a fő cél?** Egyedi portok és könyvtárak beállítása minden keresési csomóponthoz, a konfliktusok elkerülése érdekében.  
- **Szükségem van licencre?** Igen, a termelésben való használathoz próbaverzió vagy teljes licenc szükséges.  
- **Mely Java verzió támogatott?** Java 8 vagy újabb.  
- **Futtatható ez felhő szervereken?** Teljesen – csak győződjön meg róla, hogy a portok nyitva vannak a biztonsági csoportokban.  
- **Hány csomópontot adhatok hozzá?** Nincs szigorú korlát; annyit adhat hozzá, amennyit a hardvere és a hálózata megenged.

## Mi az a „configure base port groupdocs”?
Amikor **configure base port groupdocs**‑t hajt végre, egy kezdő TCP‑portot rendel minden csomóponthoz (és a további csomópontokhoz növeli azt). Ez az egyszerű lépés megszünteti a „port már használatban” hibákat, és alapot teremt egy tiszta, horizontálisan skálázható keresési klaszternak.

## Miért használjuk a GroupDocs.Search‑t egy skálázható hálózathoz?
- **Nagy teljesítmény** – optimalizált indexelési és keresési algoritmusok.  
- **Rugalmas architektúra** – keverhet indexelőket, keresőket, shard‑okat és extraktorokat a csomópontok között.  
- **Könnyű integráció** – bármely Java alkalmazással működik, helyi vagy felhő környezetben.  
- **Robusztus licencelés** – próbaverziók lehetővé teszik a tesztelést a kötelezettségvállalás előtt.

## Előkövetelmények
- **Java Development Kit (JDK)** 8 vagy újabb.  
- **IDE** például IntelliJ IDEA vagy Eclipse.  
- **GroupDocs.Search for Java** könyvtár (25.4 vagy újabb verzió) Maven‑en vagy manuális letöltésen keresztül telepítve.  
- Alapvető hálózati ismeretek (TCP portok, localhost vs. távoli gép).

## GroupDocs.Search for Java beállítása

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

Alternatívaként töltse le a legújabb verziót a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc megszerzése

- **Ingyenes próba** – azonnal elkezdheti a tesztelést.  
- **Ideiglenes licenc** – hosszabb próba a [Temporary License](https://purchase.groupdocs.com/temporary-license) oldalon.  
- **Teljes vásárlás** – kötelező a termelési környezetben.

### Alap inicializálás és beállítás

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

### Hogyan konfiguráljuk a base port groupdocs‑t

#### Alap útvonalak beállítása

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

- **Miért**: Egy konzisztens könyvtárstruktúra lehetővé teszi, hogy minden csomópont egyértelműen megtalálja az index, shard vagy extractor fájljait.

#### Base port konfigurálása

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Miért**: Egy magasabb kezdő portszám (pl. 49100) csökkenti a gyakori szolgáltatásokkal való ütközés valószínűségét. Növelje a portot minden további csomópontnál.

#### Host cím meghatározása

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Miért**: Fejlesztéskor az `localhost` ideális; termelésben cserélje le a szerver IP‑címére vagy DNS‑nevére.

#### Hálózati konfiguráció létrehozása

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

- **Miért**: Ezek a beállítások egyensúlyt teremtenek a sebesség és a tárhely hatékonyság között, így egy karcsú, mégis erőteljes keresési indexet kap.

#### Csomópontok hozzáadása

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

- **Miért**: A feladatok (indexelés vs. keresés, shardolás vs. extrakció) szétosztása a csomópontok között növeli a párhuzamosságot és a hibatűrést.

#### Konfiguráció befejezése

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Gyakori problémák és megoldások

- **Portütközések** – Mindig növelje a `basePort` értékét minden új csomópontnál. Ellenőrizze a `netstat` vagy az operációs rendszer portfigyelőjével.  
- **Hiányzó könyvtárak** – Győződjön meg róla, hogy minden hivatkozott mappa (`Indexer0`, `Searcher0` stb.) létezik, és a Java folyamatnak van írás‑/olvasási joga.  
- **H.0.0.1`‑et a tényleges host IP‑re, és nyissa meg a kiválasztott portokat a tűzfalakon.

## Gyakorlati alkalmazások

| Szenárió | A base port groupdocs konfigurálásának előnye |
|----------|----------------------------------------------|
kezelés | Zökkenőmentes skálázás osztályok között leállás nélkül |
| Nagy CMS platformok | Gyorsabb tartalomlekérdezés a megosztott indexnek köszönhetően |
| Jogi ügykezelés | A PDF‑éhez.  
- **** – A `Compression.High` helyet takarít meg a lemezen, de CPU‑t terhelhet; tesztelje a `High` és a `Normal` beállításokat is.  
- **Rendszeres frissítés** – Az új GroupDocs.Search kiadások gyakran tartalmaznak teljesítményjavító javításokat.

## Összegzés

Most már megtanulta, hogyan **configure base port groupdocs**‑t, és hogyan állítson be egy több‑csomópontos keresési hálózatot a GroupDocs.Search for Java‑val. Kísérletezzen további csomópontokkal, finomítsa az index beállításait, és integrálja a hálózatot meglévő alkalmazásaiba egy valóban skálázható keresési megoldás érdekében.

## Gyakran ismételt kérdések

**K: Mi a célja a stop‑szavak letiltásának az indexelés során?**  
V: A stop‑szavak letiltása javíthatja a keresési pontosságot, mivel megtartja azokat a gyakori kifejezéseket, amelyek speciális területeken kritikusak lehetnek.

**K: Hogyan kezeljem a portütközéseket több csomópont hozzáadásakor?**  
V: Kezdje egy magas `basePort` értékkel (pl. 49100), és minden további csomópontnál növelje azt, biztosítva, hogy minden csomópont egyedi TCP‑végponttal rendelkezzen.

**K: Használható ez a beállítás felhő‑alapú alkalmazásokhoz?**  
V: Igen – csak győződjön meg róla, hogy a kiválasztott portok nyitva vannak a felhő biztonsági csoportjaiban, és cserélje le a `127.0.0.1`‑et a megfelelő publikus vagy privát IP‑re.

**K: Mi a különbség a NormalIndex és más index típusok között?**  
V: A `NormalIndex` kiegyensúlyozott kompromisszumot kínál a sebesség és a memóriahasználat között, míg a speciális`) egyedi teljesítmény‑szcenáriókra vannak optimalizálva.

**K: Van korlátozás a hozzáadható csomópontok számában?**  
V: Technikai szempontból nincs; a határ a hardver erőforrásaitól és a hálóz