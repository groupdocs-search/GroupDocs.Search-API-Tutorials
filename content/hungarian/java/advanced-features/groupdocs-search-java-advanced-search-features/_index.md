---
date: '2026-02-16'
description: Tanulja meg, hogyan valósítsa meg a helyettesítő karakteres keresést
  Java-ban, a dátumtartomány keresést és az egyedi dátumformátumot Java-ban a GroupDocs.Search
  for Java használatával, beleértve a hibakezelést és a teljesítményoptimalizálást.
keywords:
- GroupDocs.Search Java
- advanced search features Java
- Java indexing errors
title: Wildcard keresés Java-ban a GroupDocs.Search – Haladó funkciók
type: docs
url: /hu/java/advanced-features/groupdocs-search-java-advanced-search-features/
weight: 1
---

.# Wildcard Search Java a GroupDocs.Search‑vel – Haladó funkciók

A modern, adat‑központú alkalmazásokban a **wildcard search java** az egyik legflexibilisebb módja annak, hogy a felhasználók információt találjanak meg még akkor is, ha csak egy szó részletét ismerik. Akár megfelelőségi portált, e‑kereskedelmi katalógust vagy tartalomkezelő rendszert építesz, a wildcard keresés kombinálása dátumtartomány, faceted, numerikus, regex és boolean lekérdezésekkel valóban erőteljes keresőmotort biztosít. Ez az útmutató végigvezet minden haladó funkción, bemutatja, hogyan kezelhetők az indexelési hibák, és teljesítmény‑hangolási tippeket kínál – mind mindegyik kész‑másolható Java kóddal.

## Gyors válaszok
- **Mi az a wildcard search java?** Egy lekérdezés, amely `?` vagy `*` helyőrzőket használ egy vagy több karakter egyezésére egy kifejezésben.  
- **Melyik könyvtár biztosítja?** A GroupDocs.Search for Java.  
- **Szükségem van licencre?** Egy ingyenes próba a fejlesztéshez megfelelő; a kereskedelmi használathoz termelési licenc szükséges.  
- **Kombinálhatom dátumtartomány lekérdezésekkel?** Igen – keverheted a wildcard, dátumtartomány, faceted és boolean klauzulákat egyetlen lekérdezésben.  
- **Gyors-e nagy adathalmazok esetén?** Ha megfelelően indexelt, a keresések almásodperces idő alatt futnak még milliók dokumentuma esetén is.  

## Mi az a wildcard search java?
A wildcard search java lehetővé teszi, hogy olyan dokumentumokat találj, ahol egy kifejezés mintának felel meg, például `?ffect` (illeszkedik a *affect* vagy *effect* szavakra) vagy `prod*` (illeszkedik a *product*, *production* stb. szavakra). Ideális elírások, részleges beviteli adatok vagy a pontos megfogalmazás ismeretlensége esetén.

## Miért használjuk a GroupDocs.Search‑t Java‑hoz?
A GroupDocs.Search egységes API‑t kínál számos lekérdezéstípushoz – egyszerű, **wildcard search java**, faceted, numerikus, dátumtartomány, regex, boolean és phrase – így összetett keresési élményeket építhetsz anélkül, hogy több könyvtárat kellene kezelni. Az esemény‑vezérelt hibakezelés pedig ellenállóvá teszi az indexelési folyamatot.

## Előfeltételek
- **GroupDocs.Search Java könyvtár** (v25.4 vagy újabb).  
- **Java Development Kit (JDK)**, amely kompatibilis a projekteddel.  
- Maven a függőségkezeléshez (vagy kézi letöltés).  

### Szükséges könyvtárak és környezet beállítása
Add the GroupDocs repository and dependency to your `pom.xml`:

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

### Alternatív beállítás
Közvetlen letöltéshez látogasd meg a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalt.

### Licencelés és kezdeti beállítás
Kezdd egy ingyenes próbaidőszakkal vagy egy ideiglenes licenccel:

- Látogasd meg a [GroupDocs License Options](https://purchase.groupdocs.com/temporary-license/) oldalt a részletekért.

Most hozzuk létre az index mappát, amely a kereshető adatokat tárolja.

## A GroupDocs.Search beállítása Java‑hoz

### Alapvető inicializálás
Először példányosíts egy `Index` objektumot, amely egy lemezen lévő mappára mutat:

```java
import com.groupdocs.search.*;

// Initialize Index
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\BasicUsage\\BuildSearchQuery";
Index index = new Index(indexFolder);
```

Most már van egy átjáród minden keresési művelethez.

## Implementációs útmutató

### 1. funkció: Hiba kezelés az indexelés során
#### Hogyan rögzítsük az indexelési hibákat (Java)

```java
import com.groupdocs.search.events.*;

index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
    @Override
    public void invoke(Object sender, IndexErrorEventArgs args) {
        System.out.println(args.getMessage()); // Output the error message
    }
});

// Add documents to the index
index.add("YOUR_DOCUMENT_DIRECTORY");
```

*Miért fontos*: Az `ErrorOccurred` esemény figyelésével naplózhatod a problémákat, újrapróbálhatod a sikertelen fájlokat, vagy értesítheted a felhasználókat anélkül, hogy az egész folyamat összeomlana.

### 2. funkció: Egyszerű keresési lekérdezés
#### Mi az egyszerű keresés?

```java
import com.groupdocs.search.*;

String query = "volutpat";
SearchResult result = index.search(query);
```

*Eredmény*: Visszaad minden dokumentumot, amely tartalmazza a **volutpat** kifejezést.

### 3. funkció: Wildcard keresési lekérdezés
#### Hogyan működik a wildcard search java?

```java
String query = "?ffect";
SearchResult result = index.search(query);
```

*Eredmény*: Mind a **affect**, mind az **effect** egyezést talál, bemutatva a `?` helyőrző erejét.

### 4. funkció: Faceted keresési lekérdezés
#### Hogyan hajtsuk végre a faceted search java-t

```java
String query = "Content: magna";
SearchResult result = index.search(query);
```

*Eredmény*: Korlátozza a keresést a **Content** mezőre, ami ideális a metaadatok, például kategória vagy szerző szerinti szűréshez.

### 5. funkció: Numerikus tartomány keresési lekérdezés
#### Hogyan keressünk numerikus tartományokat

```java
String query = "2000 ~~ 3000";
SearchResult result = index.search(query);
```

*Eredmény*: Visszaadja azokat a dokumentumokat, ahol a numerikus értékek 2000 és 3000 között vannak.

### 6. funkció: Dátumtartomány keresési lekérdezés
#### Hogyan hajtsuk végre a dátumtartomány keresést (egyedi dátumformátum java)

```java
import com.groupdocs.search.options.*;
import java.util.*;

String query = "daterange(2000-01-01 ~~ 2001-06-15)";
SearchOptions options = new SearchOptions();

options.getDateFormats().clear();
DateFormatElement[] elements = {
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

SearchResult result = index.search(query, options);
```

*Magyarázat*: A `SearchOptions` testreszabásával megmondod a motornak, hogy ismerje fel a **MM/DD/YYYY** formátumú dátumokat, majd lekérdezi az összes rekordot 2000. január 1. és 2001. június 15. között.

### 7. funkció: Reguláris kifejezés keresési lekérdezés
#### Hogyan futtassuk a regex search java-t

```java
String query = "^(.)\\1{2,}";
SearchResult result = index.search(query);
```

*Eredmény*: Megtalálja három vagy több azonos karakterből álló sorozatokat (pl. „aaa”, „111”).

### 8. funkció: Boolean keresési lekérdezés
#### Hogyan kombináljuk a feltételeket a boolean search java-val

```java
String query = "justo AND NOT 3456";
SearchResult result = index.search(query);
```

*Eredmény*: Visszaadja azokat a dokumentumokat, amelyek tartalmazzák a **justo** szót, de kizárja azokat, amelyekben **3456** is szerepel.

### 9. funkció: Összetett Boolean keresési lekérdezés
#### Hogyan készítsünk fejlett boolean lekérdezéseket

```java
String query = "FileName: Engl?(1~3) OR Content: (3456 AND consequat)";
SearchResult result = index.search(query);
```

*Eredmény*: Olyan fájlneveket keres, amelyek hasonlóak az „English” szóra (1‑3 karakteres eltéréseket engedve) **vagy** olyan tartalmat, amely mind a **3456**, mind a **consequat** szavakat tartalmazza.

### 10. funkció: Phrase keresési lekérdezés
#### Hogyan keressünk pontos kifejezéseket

```java
String query = "\"ipsum dolor sit amet\"";
SearchResult result = index.search(query);
```

*Eredmény*: Csak azokat a dokumentumokat adja vissza, amelyek pontosan a **ipsum dolor sit amet** kifejezést tartalmazzák.

## Gyakorlati alkalmazások
1. **E‑kereskedelmi platformok** – Használd a **faceted search java**-t a termékek méret, szín és márka szerinti szűréséhez.  
2. **Tartalomkezelő rendszerek** – Kombináld a **boolean search java**-t a phrase kereséssel, hogy fejlett szerkesztői eszközöket biztosíts.  
3. **Adat‑elemző eszközök** – Használd a **date range search** és **custom date format java** funkciókat időalapú jelentések és irányítópultok létrehozásához.  

## Gyakori problémák és megoldások
- **Nincs eredmény a dátumtartomány kereséshez** – Ellenőrizd, hogy a dokumentumaidban szereplő dátumformátum egyezik-e a hozzáadott egyedi `DateFormat`-tal.  
- **A regex lekérdezések túl sok találatot adnak** – Finomítsd a mintát vagy korlátozd a keresés hatókörét további mezőminősítőkkel.  
- **Az indexelési hibák nem kerülnek rögzítésre** – Győződj meg róla, hogy az eseménykezelő **a `index.add(...)` hívása előtt** van csatolva.  
- **A wildcard keresés lassúnak tűnik** – Kerüld a vezető wildcard‑eket (`*term`) nagyon nagy indexeknél; részesítsd előnyben a suffix vagy infix mintákat.  

## Gyakran ismételt kérdések

**Q: Kombinálhatom a dátumtartomány keresést más lekérdezéstípusokkal?**  
A: Természetesen. Egy dátumtartomány klauzulát kombinálhatsz wildcard, boolean, faceted vagy regex mintákkal egyetlen lekérdezésben.

**Q: Újra kell építeni az indexet a dátumformátumok módosítása után?**  
A: Igen. Az index tokenizált kifejezéseket tárol; csak a `SearchOptions` frissítése nem tokenizálja újra a meglévő adatokat. A formátumok módosítása után újra kell indexelni a dokumentumokat.

**Q: Hogyan kezeli a GroupDocs.Search a nagy indexeket?**  
A: Inkrementális indexelést és lemezen tárolást használ, ami lehetővé teszi, hogy milliók dokumentumáig skálázz, miközben alacsony a memóriahasználat.

**Q: Van korlát a wildcard karakterek számában?**  
A: A wildcard‑ok hatékonyan feldolgozhatók, de sok vezető wildcard (pl. `*term`) teljesítménycsökkenést okozhat. Inkább prefix vagy suffix wildcard‑okat használj.

**Q: Melyik licencmodell ajánlott a termeléshez?**  
A: A GroupDocs által kínált örökös vagy előfizetéses licenc biztosítja a frissítéseket, támogatást és a korlátozások nélküli telepítést.

## Következtetés
A **wildcard search java** és a GroupDocs.Search for Java által kínált teljes haladó lekérdezéstípus‑készlet elsajátításával rendkívül gyors, funkciógazdag keresési élményeket építhetsz. Valósíts meg robusztus hibakezelést, finomhangold az indexet, és kombináld a lekérdezéseket, hogy gyakorlatilag bármilyen visszakeresési helyzetet kielégítsenek. Kezdj el ma kísérletezni, és emeld alkalmazásod adat‑hozzáférési képességeit.

---

**Utolsó frissítés:** 2026-02-16  
**Tesztelve ezzel:** GroupDocs.Search 25.4 (Java)  
**Szerző:** GroupDocs