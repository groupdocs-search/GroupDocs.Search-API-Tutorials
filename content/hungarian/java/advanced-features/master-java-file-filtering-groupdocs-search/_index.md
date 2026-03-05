---
date: '2026-02-21'
description: Tanulja meg, hogyan valósíthat meg egy Java fájlkiterjesztés-szűrőt a
  GroupDocs.Search for Java használatával, magában foglalva a logikai operátorokat,
  a létrehozási/módosítási dátumokat és az útvonal szűrőket.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: java fájl kiterjesztés szűrő a GroupDocs.Search segítségével – Útmutató
type: docs
url: /hu/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

 "Tesztelve a következővel", "Author" to "Szerző". Keep dates unchanged.

Now produce final markdown with Hungarian translation.

Make sure to keep code block placeholders unchanged.

Also ensure we keep any bold formatting (** **) and inline code unchanged.

Let's craft final answer.# A java fájlkiterjesztés szűrő elsajátítása a GroupDocs.Search segítségével

A dokumentumok növekvő tárházának kezelése gyorsan túlterhelővé válhat, különösen akkor, ha csak bizonyos fájltípusokat kell indexelni. **A java fájlkiterjesztés szűrő** lehetővé teszi, hogy pontosan megadd a GroupDocs.Search‑nek, mely kiterjesztéseket vegye fel vagy hagyja ki, így precíz irányítást kapsz az indexelési folyamatod felett. Ebben az útmutatóban lépésről‑lépésre bemutatjuk a GroupDocs.Search for Java beállítását, és megmutatjuk, hogyan kombinálhatod a fájlkiterjesztés szűrését logikai AND, OR és NOT operátorokkal, valamint dátumtartomány és útvonal szűrőkkel.

## Gyors válaszok
- **Mi a java fájlkiterjesztés szűrő?** Egy konfiguráció, amely megmondja a GroupDocs.Search‑nek, mely fájlkiterjesztéseket kell belefoglalni vagy kizárni az indexelés során.  
- **Melyik könyvtár biztosítja ezt a funkciót?** GroupDocs.Search for Java.  
- **Szükségem van licencre?** Egy ingyenes próba a kiértékeléshez megfelelő; a termeléshez teljes licenc szükséges.  
- **Összekapcsolhatok szűrőket?** Igen – összefűzheted a kiterjesztés, dátum, méret és útvonal szűrőket AND, OR, NOT logikával.  
- **Maven‑kompatibilis?** Teljesen – add hozzá a GroupDocs.Search függőséget a `pom.xml`‑hez.

## Mi a java fájlkiterjesztés szűrő?
A **java fájlkiterjesztés szűrő** egy szabálykészlet, amely minden fájl kiterjesztését kiértékeli, mielőtt az indexelő motorhoz kerülne. Az olyan kiterjesztések megadásával, mint `.txt`, `.pdf` vagy `.epub`, **belefoglalhatod a fájlokat kiterjesztés szerint** vagy **kizárhatod a fájlokat kiterjesztés szerint**, hogy az indexed fókuszált maradjon, és a keresési eredmények relevánsak legyenek.

## Miért használjunk fájlkiterjesztés szűrést a GroupDocs.Search‑szel?
- **Teljesítmény:** A nem kívánt fájlok kihagyása csökkenti az I/O‑t és felgyorsítja az indexelést.  
- **Tárhely megtakarítás:** Csak a releváns dokumentumok kerülnek az indexbe, csökkentve a lemezhasználatot.  
- **Megfelelőség:** Megakadályozza a bizalmas vagy nem támogatott fájltípusok véletlen indexelését.  
- **Rugalmasság:** Kombináld a **date range filter java** funkciókkal, hogy a konkrét időszakokban létrehozott vagy módosított fájlokat célozd meg.

## Előkövetelmények

Mielőtt elkezdenénk, győződj meg róla, hogy a következőkkel rendelkezel:

### Szükséges könyvtárak és függőségek
- **GroupDocs.Search for Java**: 25.4 vagy újabb verzió  
- **Java Development Kit (JDK)**: Telepített kompatibilis verzió  

### Környezet beállítása
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse vagy bármely Maven‑kompatibilis IDE.

### Tudás előkövetelmények
- Alap Java programozás  
- Fájl I/O ismerete Java‑ban  
- Reguláris kifejezések és dátum‑idő kezelés megértése  

## A GroupDocs.Search beállítása Java‑hoz
A GroupDocs.Search használatához hozzá kell adnod a projekted függőségei közé.

### Maven konfiguráció
Add hozzá a következő tárolót és függőség‑konfigurációt a `pom.xml` fájlodhoz:

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
Alternatívaként töltsd le a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

#### Licenc megszerzése
1. **Free Trial** – felfedezheted a funkciókat költség nélkül.  
2. **Temporary License** – teljes funkcionalitás korlátozott időre.  
3. **Purchase** – állandó licenc a termelési használathoz.  

### Alap inicializálás és beállítás
Miután a könyvtárat hozzáadtad, inicializáld az indexelési környezetet:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Implementációs útmutató
Az alábbiakban minden szűrőtípusra részletesen kitérünk, megmagyarázva **miért fontos**, és lépésről‑lépésre bemutatva a kódot, amelyet egyszerűen átmásolhatsz a projektedbe.

### Fájlkiterjesztés szűrés
Fájlok szűrése kiterjesztésük alapján az indexelés során. Ideális, ha csak e‑könyveket (`.fb2`, `.epub`) és egyszerű szövegfájlokat (`.txt`) szeretnél feldolgozni.

#### Áttekintés
Használd a `DocumentFilter.createFileExtension` metódust a fehérlista létrehozásához.

#### Implementációs lépések
1. **Create Filter**:

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logikai NOT szűrő
Kizárhatod a nem kívánt kiterjesztéseket, például weboldalakat és PDF‑eket, ha azok nem szükségesek a keresési forgatókönyvedben.

#### Implementációs lépések
1. **Create Exclusion Filter**:

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to Index Settings**:

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add Documents**:

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logikai AND szűrő
Több feltétel egyesítése – létrehozási dátum, kiterjesztés és fájlméret – úgy, hogy **csak azok a fájlok kerüljenek indexelésre, amelyek minden kritériumnak megfelelnek**.

#### Áttekintés
A `DocumentFilter.createAnd` több szűrőt egyetlen szabályba egyesít.

#### Implementációs lépések
1. **Define Filters**:

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine Filters**:

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index Documents**:

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logikai OR szűrő
Fájlok bevétele, amelyek **bármelyik** megadott feltételnek megfelelnek – hasznos, ha kis szövegfájlokat és nagyobb nem‑szöveg fájlokat egyaránt szeretnél lefedni.

#### Implementációs lépések
1. **Define Filters**:

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine Filters with Logical Conditions**:

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR Filter**:

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Létrehozási idő szűrők
Célzott fájlok, amelyek egy adott időszakon belül lettek létrehozva – klasszikus **date range filter java** szituáció.

#### Implementációs lépések
1. **Define Date Range Filter**:

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index Documents**:

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Módosítási idő szűrők
Kizárhatod azokat a fájlokat, amelyeket egy bizonyos határidő után módosítottak.

#### Implementációs lépések
1. **Define Filter**:

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index Documents**:

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Fájl útvonal szűrés
Az indexelés korlátozása olyan fájlokra, amelyek meghatározott mappákban vagy egy mintának megfelelően helyezkednek el – ideális **include files by extension** esetén egy adott könyvtárhierarchián belül.

#### Implementációs lépések
1. **Define File Path Filter**:

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Gyakori hibák és tippek

- **Never mix absolute and relative paths** in the same filter configuration – it can lead to unexpected exclusions.  
  **Soha ne keverd az abszolút és relatív útvonalakat** ugyanabban a szűrőkonfigurációban – ez váratlan kizárásokhoz vezethet.  
- **Reset the `IndexSettings`** when switching filter sets; otherwise previous filters may persist.  
  **Állítsd vissza az `IndexSettings`‑t** szűrők cseréjekor; különben a korábbi szűrők megmaradhatnak.  
- **Combine a length upper bound with an extension filter** for large collections to keep memory usage low.  
  **Kombináld a maximális hosszkorlátot egy kiterjesztés szűrővel** nagy gyűjteményeknél, hogy alacsonyan tartsd a memóriahasználatot.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) to see why a file was rejected.  
  **Engedélyezd a naplózást** (`LoggingOptions.setEnabled(true)`), hogy lásd, miért lett egy fájl elutasítva.  

## Gyakran feltett kérdések

**Q: Can I change the filter criteria after the index is created?**  
A: Yes. Rebuild the index with a new `DocumentFilter` or use incremental indexing with updated settings.  
**Q: Does the java file extension filter work on compressed archives (e.g., ZIP)?**  
A: GroupDocs.Search can index supported archive formats, but the extension filter applies to the archive itself, not the inner files. Use nested filters for deeper control.  
**Q: How do I debug why a particular file was excluded?**  
A: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect the log – it reports which filter rejected each file.  
**Q: Is it possible to combine the java file extension filter with custom regex filters?**  
A: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside the extension filter.  
**Q: What performance impact does adding many filters have?**  
A: Each filter adds a modest overhead during indexing, but the reduction in indexed data usually outweighs the cost. Test with a representative sample to find the optimal balance.  

---

**Utolsó frissítés:** 2026-02-21  
**Tesztelve a következővel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs