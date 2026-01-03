---
date: '2026-01-03'
description: Tanulja meg, hogyan adhat hozzá dokumentumokat az indexhez, és hogyan
  szakíthatja meg az egyesítési műveletet Java-ban a GroupDocs.Search használatával.
  Teljes útmutató a dokumentumkezeléshez Java-ban.
keywords:
- document indexing in Java
- merging documents with GroupDocs
- GroupDocs.Search Java tutorial
title: Dokumentumok hozzáadása az indexhez és egyesítése Java-ban a GroupDocs.Search
  használatával
type: docs
url: /hu/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# Dokumentumok hozzáadása az indexhez és egyesítése Java-ban a GroupDocs.Search használatával

A mai gyors tempójú digitális környezetben a **dokumentumok indexhez való hozzáadásának** hatékony megtanulása elengedhetetlen minden **document management java** megoldás számára. Akár szerződéseket, számlákat vagy belső jelentéseket kezel, egy jól felépített index lehetővé teszi az információ milliszekundumok alatt történő lekérdezését. Ez az útmutató végigvezet az indexek létrehozásán, dokumentumok hozzáadásán, egyesítési beállítások konfigurálásán, és akár a **cancel merge operation** leállításán is, ha szükséges – mindezt a GroupDocs.Search for Java segítségével.

## Gyors válaszok
- **Mi jelent a „add documents to index”?** Azt mondja a GroupDocs.Search-nek, hogy szkennelje a mappát, és tárolja a kereshető metaadatokat minden fájlhoz.  
- **Leállíthatok egy hosszú egyesítést?** Igen – használja a `Cancellation` objektumot a **cancel merge operation** időtúllépés után.  
- **Szükségem van licencre?** Egy ingyenes próba vagy ideiglenes licenc teszteléshez megfelelő; egy kereskedelmi licenc feloldja a teljes funkciókat.  
- **Melyik Java verzió szükséges?** JDK 8 vagy újabb.  
- **Alkalmas nagy adatállományokra?** Teljesen – csak figyelje a memóriát, és használjon inkrementális indexelést.

## Mi a „add documents to index” a GroupDocs.Search-ben?
A dokumentumok indexhez való hozzáadása azt jelenti, hogy egy fájlkészletet adunk a GroupDocs.Search-nek, hogy a könyvtár elemezhesse a tartalmukat, tokeneket nyerjen ki, és egy kereshető adatstruktúrát építsen. Az indexelés után gyors teljes szöveges kereséseket végezhet az összes dokumentumban.

## Miért használja a GroupDocs.Search-t a document management java-hoz?
- **Skálázható indexelés** – Több ezer fájlt kezel a teljesítmény romlása nélkül.  
- **Gazdag API** – Finomhangolt vezérlést biztosít az indexelés, egyesítés és leállítás felett.  
- **Keresztformátumú támogatás** – Alapból működik PDF, Word, Excel és számos más formátummal.

## Előfeltételek
- **GroupDocs.Search for Java** 25.4 vagy újabb verzió.  
- Maven (vagy kézi JAR letöltés).  
- Alapvető Java ismeretek és JDK 8+ környezet.

## A GroupDocs.Search for Java beállítása

### Maven telepítés
Ha Maven‑nel kezeli a függőségeket, adja hozzá a tárolót és a függőséget a `pom.xml`-hez:

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

### Közvetlen letöltés
Alternatívaként töltse le a legújabb JAR‑t a hivatalos oldalról: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenc beszerzése
- **Free Trial:** Regisztráljon a GroupDocs weboldalon egy próba licencért.  
- **Temporary License:** Kérjen ideiglenes kulcsot, ha hosszabb értékelésre van szüksége.  
- **Commercial License:** Vásárolja meg a termelési használathoz.

Miután megkapta a licencfájlt, helyezze a projektjébe, és inicializálja a könyvtárat, ahogyan később látható.

## Implementációs útmutató

### Hogyan adjon dokumentumokat az indexhez – Az első index létrehozása
Először hozzon létre egy üres indexet, amely a kereshető adatokat tárolja.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **Miért:** Ez a lépés egy tároló konténert hoz létre, ahol az indexelt tokenek lesznek mentve.

#### Dokumentumok hozzáadása az indexhez
Most mondja a GroupDocs.Search-nek, hogy szkennelje a mappát, és **add documents to index**.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **Miért:** A könyvtár beolvassa minden fájlt, kinyeri a szöveget, és a `index1`‑ben tárolja.

### Második index létrehozása rugalmas munkafolyamatokhoz
Néha különálló indexekre van szükség – például egy ügyfél adatainak elkülönítésére.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Miért:** Több index lehetővé teszi különálló dokumentumkészletek kezelését, majd későbbi egyesítését.

### Hogyan konfigurálja az egyesítési beállításokat és a merge művelet leállítását
Az egyesítés előtt finomhangolhatja a folyamatot, és akár le is állíthatja, ha túl sokáig tart.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **Miért:** A `Cancellation` lehetővé teszi, hogy automatikusan **cancel merge operation**-t hajtson végre, megakadályozva a szabadon futó feladatokat.

### Indexek egyesítése
Végül egyesítse a másodlagos indexet az elsődlegesbe.

```java
index1.merge(index2, options);
```

- **Miért:** Ennek a hívásnak a után a `index1` tartalmazza mindkét forrás összes dokumentumát, így egységes keresési élményt biztosít.

## Gyakorlati alkalmazások a Document Management Java-hoz
- **Jogász irodák:** Esetdokumentumok konszolidálása több irodából.  
- **Pénzügyi intézmények:** Negyedéves jelentések egyesítése egy kereshető adattárba.  
- **Vállalatok:** HR, megfelelőségi és szabályzati dokumentumok egyesítése vállalati szintű kereséshez.

## Teljesítmény szempontok
- **Inkrementális indexelés:** Új fájlok hozzáadása időszakosan a teljes index újraépítése helyett.  
- **Memóriafigyelés:** Nagy kötegek RAM-ot fogyaszthatnak; fontolja a kisebb darabokban történő feldolgozást.  
- **Garbage collection:** Szabadítsa fel időben a nem használt `Index` objektumokat az erőforrások felszabadításához.

## Gyakori problémák és megoldások

| Probléma | Megoldás |
|----------|----------|
| **Helytelen mappa útvonal** | Ellenőrizze a abszolút útvonalat, és győződjön meg arról, hogy az alkalmazásnak olvasási jogosultsága van. |
| **Elégtelen memória** | Növelje a JVM heap méretét (`-Xmx`), vagy indexelje a fájlokat kötegekben. |
| **A leállítás nem aktiválódik** | Győződjön meg arról, hogy a `cancelAfter` be van állítva a `merge` hívása előtt. |
| **Nem támogatott fájlformátum** | Telepítsen további formátum plugineket a GroupDocs-tól, ha szükséges. |

## Gyakran feltett kérdések

**Q:** *Miért hoznék létre több indexet egyetlen helyett?*  
A: A különálló indexek lehetővé teszik az adatcsoportok elkülönítését, különböző biztonsági szabályok alkalmazását, és csak szükség esetén egyesítik őket, ami javítja a teljesítményt és a szervezést.

**Q:** *Leállíthatok egy indexelési műveletet ugyanúgy, ahogy egy merge‑t?*  
A: Igen – használja a `Cancellation` objektumot az `add` metódussal a hosszú ideig futó indexelési feladatok leállításához.

**Q:** *Hogyan biztosíthatom az optimális teljesítményt nagyon nagy dokumentumgyűjtemények esetén?*  
A: Alkalmazzon inkrementális indexelést, figyelje a JVM memóriát, és fontolja SSD tároló használatát az index könyvtárhoz.

**Q:** *Mit tegyek, ha “Access denied” hibát kapok?*  
A: Ellenőrizze a mappa jogosultságait a Java folyamatot futtató felhasználó számára, és győződjön meg arról, hogy a licencfájl olvasható.

**Q:** *Kompatibilis a GroupDocs.Search más GroupDocs könyvtárakkal?*  
A: Teljesen – integrálható a GroupDocs.Viewer, GroupDocs.Conversion stb. könyvtárakkal egy teljes körű dokumentummegoldáshoz.

## Következtetés
Az útmutató követésével most már tudja, hogyan **add documents to index**, hogyan konfigurálja az egyesítési viselkedést, és hogyan állítsa le biztonságosan a **cancel merge operation**-t, ha szükséges – mindezt egy robusztus **document management java** munkafolyamaton belül. Kísérletezzen nagyobb adatállományokkal, fedezze fel az egyedi tokenizálókat, vagy kombinálja a GroupDocs.Search-t más GroupDocs termékekkel, hogy valóban vállalati szintű megoldást építsen.

---

**Last Updated:** 2026-01-03  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

**Erőforrások**
- **Documentation:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License Application:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)