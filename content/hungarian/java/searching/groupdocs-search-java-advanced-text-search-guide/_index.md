---
date: '2026-01-24'
description: Ismerje meg, hogyan adhat dokumentumokat az indexhez, és végezhet fejlett
  szövegkeresést Java-ban a GroupDocs.Search használatával. Konfigurálja az indexeket,
  engedélyezze a szótári formákat, és optimalizálja a teljesítményt.
keywords:
- GroupDocs.Search Java
- advanced text search
- Java indexing
title: Dokumentumok hozzáadása az indexhez a GroupDocs.Search Java-val
type: docs
url: /hu/java/searching/groupdocs-search-java-advanced-text-search-guide/
weight: 1
---

# Dokumentumok hozzáadása az indexhez a GroupDocs.Search Java-val

Modern alkalmazásokban a **dokumentumok indexhez adása** gyorsan és hatékony keresés lehetővé tétele igazi fordulópont. Akár vállalati tudásbázist, jogi dokumentumtárat vagy e‑kereskedelmi termékkatalógust építesz, ennek a folyamatnak az elsajátítása lehetővé teszi, hogy gyors, releváns eredményeket nyújts a végfelhasználóknak. Ebben az útmutatóban végigvezetünk a GroupDocs.Search for Java beállításán, egy index létrehozásán, a dokumentumok hozzáadásán, a fejlett szöveges keresési funkciók engedélyezésén és a teljesítmény finomhangolásán.

## Gyors válaszok
- **Mi jelenti a „dokumentumok indexhez adása” kifejezést?** Azt jelenti, hogy a forrásfájlokat egy kereshető adatstruktúrába töltjük, amelyet a GroupDocs.Search lekérdezhet.
- **Melyik könyvtárverzió szükséges?** A GroupDocs.Search for Java 25.4 (vagy újabb) támogatja az itt bemutatott funkciókat.
- **Szükségem van licencre?** A ingyenes próba verzió fejlesztéshez használható; a termeléshez kereskedelmi licenc szükséges.
- **Kereshetek különböző szótári formákat?** Igen—engedélyezd a `setUseWordFormsSearch(true)` beállítást a `SearchOptions`-ban.
- **A Maven az egyetlen telepítési mód?** Nem, a JAR-t közvetlenül is letöltheted (lásd a Direct Download linket).

## Mi a „dokumentumok indexhez adása”?
A dokumentumok indexhez adása azt jelenti, hogy a forrásfájlokat beolvasod, kinyered a kereshető szöveget, és ezt az információt egy strukturált formátumban tárolod, amely gyors lekérdezést tesz lehetővé. A GroupDocs.Search számos fájltípust natívan támogat, így a vállalati logikára koncentrálhatsz a feldolgozás helyett.

## Miért használjunk fejlett szöveges keresési Java technikákat?
A fejlett szöveges keresési Java képességek—például szótári forma felismerés, fuzzy egyezés és egyedi rangsorolás—segítik a felhasználókat információk megtalálásában még akkor is, ha a lekérdezés nem pontos egyezés. Ez növeli a felhasználói elégedettséget és csökkenti a dokumentumok keresésére fordított időt.

## Előfeltételek
- **Szükséges könyvtárak**: GroupDocs.Search for Java 25.4.
- **Környezet beállítása**: Java JDK 8 vagy újabb, Maven (vagy kézi JAR kezelés).
- **Tudás előfeltételek**: Alap Java programozás és Maven függőségkezelés.

## A GroupDocs.Search for Java beállítása
Mielőtt kódot írnál, győződj meg róla, hogy a könyvtár elérhető a projekted számára.

### Maven beállítás
Add the following configuration to your `pom.xml` file:

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

### Direct Download
Ha nem szeretnél Maven-t használni, letöltheted a legújabb JAR-t a hivatalos oldalról: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenc megszerzésének lépései
1. **Ingyenes próba** – költség nélkül felfedezheted az API-t.  
2. **Ideiglenes licenc** – meghosszabbíthatod a próbaidőszakot alaposabb teszteléshez.  
3. **Vásárlás** – kereskedelmi licencet szerezhetsz a termeléshez.

## Lépésről‑lépésre megvalósítási útmutató

### 1. Index létrehozása és konfigurálása
Az index bármely keresési megoldás gerince. Tokenizált szöveget és metaadatokat tárol a gyors lekérdezéshez.

#### Áttekintés
Létrehozunk egy mappát a lemezen, amely az index fájlokat tárolja.

#### Kód
```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/SearchForDifferentWordForms";
Index index = new Index(indexFolder);
```

*Explanation*: A `Index` konstruktor egy mappára mutat, ahol az összes index adat tárolódik. Cseréld le a `YOUR_DOCUMENT_DIRECTORY`-t a géped tényleges útvonalára.

### 2. Hogyan adjunk dokumentumokat az indexhez
Miután az index létezik, **dokumentumokat kell hozzáadni az indexhez**, hogy kereshetővé váljanak.

#### Áttekintés
A GroupDocs.Search beolvassa a megadott könyvtárat, és indexeli az összes támogatott fájltípust, amelyet megtalál.

#### Kód
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
index.add(documentsFolder);
```

*Explanation*: Az `add` metódus rekurzívan feldolgozza a mappát, kinyeri a szöveget, és az indexbe tárolja. Győződj meg róla, hogy az útvonal helyes, és az alkalmazásnak olvasási jogosultsága van.

### 3. Keresési beállítások konfigurálása szótári formákhoz
A keresések nyelvtani variációk (pl. „wish”, „wished”, „wishes”) tolerálásához engedélyezd a szótári forma keresést.

#### Áttekintés
A `SearchOptions`-t módosítjuk, hogy bekapcsoljuk ezt a funkciót.

#### Kód
```java
import com.groupdocs.search.SearchOptions;

SearchOptions options = new SearchOptions();
options.setUseWordFormsSearch(true); // Enables search for different grammatical variations of words.
```

*Explanation*: A `setUseWordFormsSearch(true)` beállítás azt mondja a motornak, hogy bővítse a lekérdezéseket a ismert ragozásokkal, ezáltal javítva a visszahívást.

### 4. Keresés végrehajtása
Az index feltöltése és a beállítások konfigurálása után most végrehajthatunk egy lekérdezést.

#### Áttekintés
A „wished” szót fogjuk keresni, és visszakapjuk a megfelelő dokumentumokat.

#### Kód
```java
import com.groupdocs.search.SearchResult;

String query = "wished";
SearchResult result = index.search(query, options);
```

*Explanation*: A `search` metódus a definiált opciókkal hajtja végre a lekérdezést az indexelt tartalmon. A visszakapott `SearchResult` egy találatok gyűjteményét tartalmazza, mindegyik dokumentumreferenciával és szövegrészlettel.

## Gyakori problémák és hibaelhárítás
- **Helytelen útvonalak** – Ellenőrizd a `indexFolder` és `documentsFolder` értékeket elírások és megfelelő hozzáférési jogok szempontjából.
- **Nem támogatott fájlformátumok** – Győződj meg róla, hogy a dokumentumaid a GroupDocs.Search dokumentációban felsorolt formátumok között vannak.
- **Teljesítmény lassulás** – Nagy adatállományok esetén fontold meg a kötegelt indexelést és a JVM heap használatának figyelését.

## Gyakorlati alkalmazások
1. **Vállalati dokumentumkezelés** – Gyorsan megtalálod a szabályzatokat, szerződéseket vagy HR kézikönyveket több ezer fájl között.  
2. **Jogi kutatás** – Előző eseteket találhatsz meg még akkor is, ha a pontos megfogalmazás eltér, a szótári forma keresésnek köszönhetően.  
3. **E‑kereskedelmi katalógusok** – Lehetővé teszi a vásárlók számára, hogy a termékleírásokat változatos terminológiával keressék.

## Teljesítmény tippek
- Csak akkor indexelj újra, ha új dokumentumok kerülnek hozzáadásra vagy a meglévők megváltoznak.  
- Használd a Java `-Xmx` kapcsolót a nagy indexekhez elegendő heap memória lefoglalásához.  
- Időnként hívd meg az `index.optimize()`-t (ha elérhető), hogy tömörítsd az index fájlokat.

## Következtetés
Most már tudod, hogyan **adj dokumentumokat az indexhez**, engedélyezd a fejlett szöveges keresést, és finomhangold a GroupDocs.Search for Java-t. Ezek a technikák lehetővé teszik, hogy válaszkész, funkciógazdag keresési élményeket építs bármilyen dokumentumgyűjteményen.

### Következő lépések
- Kísérletezz a fuzzy egyezéssel és egyedi rangsorolással.  
- Integráld a keresési modult egy REST API-ba a front‑end számára.  
- Fedezd fel a többnyelvű támogatást nyelvspecifikus elemzők konfigurálásával.

## Gyakran ismételt kérdések

**Q1: Milyen formátumokat támogat a GroupDocs.Search?**  
A1: Széles körű formátumokat támogat, többek között DOCX, PDF, PPTX, TXT és még sok más. Tekintsd meg a hivatalos dokumentációt a teljes listáért.

**Q2: Hogyan frissíthetem az indexet új dokumentumokkal?**  
A2: Egyszerűen hívd meg újra az `index.add(newDocumentsFolder)`-t; a könyvtár csak az új vagy módosított fájlokat adja hozzá.

**Q3: Testreszabhatom tovább a keresési lekérdezéseket?**  
A3: Igen— a `SearchOptions` lehetőségeket kínál a fuzzy kereséshez, a kis- és nagybetű érzékenységhez, valamint az eredmények lapozásához.

**Q4: A kereséseim lassúak—mit tehetek?**  
A4: Győződj meg róla, hogy az index gyors SSD tárolón van, növeld a JVM heap méretét, és kerüld a felesleges nagy fájlok indexelését.

**Q5: Hol kaphatok segítséget a közösségtől?**  
A5: Használd a hivatalos támogatási fórumot: [GroupDocs Support Forum](https://forum.groupdocs.com/c/search/10).

## Erőforrások
- **Documentation**: Mélyreható útmutatókat találsz a [GroupDocs Documentation](https://docs.groupdocs.com/search/java/) oldalon

---

**Legutóbb frissítve:** 2026-01-24  
**Tesztelve ezzel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs