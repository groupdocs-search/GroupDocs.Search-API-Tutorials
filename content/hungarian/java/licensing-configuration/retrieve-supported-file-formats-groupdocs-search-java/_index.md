---
date: '2026-01-16'
description: Tanulja meg, hogyan használja a GroupDocs-ot, és szerezze meg a Java
  fájlkiterjesztéseket azáltal, hogy lekéri az összes támogatott fájlformátumot a
  GroupDocs.Search for Java segítségével. Ideális fejlesztőknek, akik dokumentumfeldolgozó
  könyvtárakat integrálnak.
keywords:
- GroupDocs.Search for Java
- retrieve supported file formats
- Java document processing
title: Hogyan használjuk a GroupDocs-ot a Java-ban támogatott fájlformátumok lekérdezéséhez
type: docs
url: /hu/java/licensing-configuration/retrieve-supported-file-formats-groupdocs-search-java/
weight: 1
---

# Hogyan használjuk a GroupDocs-ot a támogatott fájlformátumok lekérdezéséhez Java-ban

Ha kíváncsi vagy **hogyan használjuk a GroupDocs-ot**, hogy megtudd, pontosan milyen fájltípusokat képes kezelni az alkalmazásod, jó helyen jársz. Ebben az útmutatóban végigvezetünk a támogatott formátumok teljes listájának lekérésén a GroupDocs.Search for Java segítségével, így magabiztosan megjelenítheted vagy ellenőrizheted a fájlkiterjesztéseket a felhasználói felületedben.

## Gyors válaszok
- **Mi a funkció?** Visszaad minden fájlkiterjesztést, amelyet a GroupDocs.Search indexelni tud.  
- **Miért hasznos?** Lehetővé teszi, hogy dinamikusan tájékoztasd a felhasználókat a támogatott feltöltésekről, és elkerüld a nem támogatott fájlok hibáit.  
- **Szükségem van licencre?** Az ingyenes próbaidőszak teszteléshez elegendő; a termeléshez teljes licenc szükséges.  
- **Milyen Java verzió szükséges?** Java 8 vagy újabb.  
- **Szükséges-e extra konfiguráció?** Nem – csak add hozzá a függőséget, és hívd meg az API-t.

## Mi az a GroupDocs.Search?
A GroupDocs.Search egy Java könyvtár, amely gyors, teljes szöveges keresést biztosít számos dokumentumformátumon keresztül. Elrejti a PDF-ek, Word fájlok, táblázatok és sok más típus feldolgozásának összetettségét, egyszerű API-t nyújtva az indexeléshez és a lekérdezéshez.

## Miért kell lekérdezni a támogatott fájlformátumokat?
Az pontos kiterjesztéslista segít:
- Dinamikus feltöltő widgetek építésében, amelyek csak a támogatott fájlokat engedélyezik.  
- Pontos dokumentáció készítésében a végfelhasználók számára.  
- A futásidejű hibák csökkentésében, amelyek a nem támogatott formátumok indexeléséből adódnak.

## Előfeltételek
- **Java Development Kit (JDK) 8+**  
- **Maven** a függőségkezeléshez  
- **IDE**, például IntelliJ IDEA vagy Eclipse  

Az alapvető Java és Maven ismeretek segítik a lépések gördülékeny végrehajtását.

## A GroupDocs.Search beállítása Java-hoz

### Maven beállítás
Add hozzá a GroupDocs tárolót és a függőséget a `pom.xml` fájlodhoz:

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
Ha inkább, letöltheted a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc megszerzésének lépései
- **Ingyenes próba** – a fő funkciók felfedezése.  
- **Ideiglenes licenc** – korlátozások nélkül tesztelés.  
- **Teljes licenc** – a termelésre kész funkciók feloldása.

#### Alapvető inicializálás és beállítás
Miután a függőség hozzá lett adva, létrehozhatsz egy indexet és dokumentumokat adhatsz hozzá:

```java
import com.groupdocs.search.*;

public class InitializeGroupDocs {
    public static void main(String[] args) {
        // Create an index in the specified folder
        Index index = new Index("path/to/index/folder");
        
        // Add documents to the index from a folder
        index.add("path/to/documents/folder");
    }
}
```

## Hogyan használjuk a GroupDocs-ot a fájlkiterjesztések lekérésére Java-ban

### Támogatott fájlformátumok lekérése
Az alábbi lépések bemutatják, hogyan lehet lekérni a teljes listát a fájlkiterjesztésekről, amelyeket a GroupDocs.Search támogat.

#### 1. lépés – A szükséges osztály importálása
```java
import com.groupdocs.search.results.FileType;
```

#### 2. lépés – A támogatott típusok gyűjteményének lekérése
```java
Iterable<FileType> supportedFileTypes = FileType.getSupportedFileTypes();
```

#### 3. lépés – Az egyes formátumok bejárása és kiírása
```java
for (FileType fileType : supportedFileTypes) {
    System.out.println(fileType.getExtension() + " - " + fileType.getDescription());
}
```

A kódrészlet futtatása például `pdf - Portable Document Format` sorokat ír ki, így kész listát kapsz a felhasználói felület legördülő menüjéhez vagy az ellenőrző logikához.

### Hibaelhárítási tippek
- **Class Not Found** – Ellenőrizd, hogy a Maven függőség helyesen fel lett-e oldva.  
- **Útvonal problémák** – Győződj meg róla, hogy az index mappája létezik és írható.  

## Gyakorlati alkalmazások
1. **Dokumentumkezelő rendszerek** – Dinamikusan listázzák a támogatott feltöltéseket.  
2. **Webes fájlfeltöltések** – Az ügyféloldalon a lekért lista alapján ellenőrzik a fájltípusokat.  
3. **Biztonsági mentési megoldások** – A nem támogatott fájlok kiszűrése archiválás előtt.

## Teljesítménybeli megfontolások
- Tárold a lekért listát memóriában, ha gyakran kell hozzáférned; a hívás maga könnyű.  
- Tartsd naprakészen a GroupDocs.Search könyvtárat a teljesítményjavulások érdekében.

## Gyakori problémák és megoldások
| Probléma | Ok | Megoldás |
|----------|----|----------|
| `FileType` osztály hiányzik | Függőség nincs hozzáadva | Futtasd újra a `mvn clean install` parancsot a függőség hozzáadása után |
| Nem jelenik meg a kimenet | `System.out` le van tiltva az IDE-ben | Ellenőrizd a konzol beállításait vagy futtasd a parancssorból |

## Gyakran feltett kérdések

**Q: Mi a GroupDocs.Search?**  
A: Egy Java könyvtár, amely lehetővé teszi a teljes szöveges keresést számos dokumentumformátumon anélkül, hogy külön parsereket kellene használni.

**Q: Hogyan frissíthetem a könyvtár verzióját?**  
A: Módosítsd a `<version>` elemet a `pom.xml`‑ben, majd futtasd a `mvn clean install` parancsot.

**Q: Használhatom ezt a funkciót nem‑Java projektben?**  
A: A bemutatott API Java‑specifikus, de a GroupDocs hasonló képességeket kínál .NET, Python és egyéb platformok számára is.

**Q: Mi van, ha egy szükséges fájltípus hiányzik?**  
A: Vedd fel a kapcsolatot a GroupDocs támogatással; gyakran adnak hozzá új formátumokat a későbbi kiadásokban.

**Q: Szükséges-e kereskedelmi licenc a termeléshez?**  
A: Igen, a teljes licenc eltávolítja a próbaidőszak korlátozásait és biztosítja a kereskedelmi felhasználási jogokat.

## Források
- [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- [API Reference](https://reference.groupdocs.com/search/java)  
- [Download Latest Version](https://releases.groupdocs.com/search/java/)  
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)  
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license/)

---

**Utoljára frissítve:** 2026-01-16  
**Tesztelve a következővel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs