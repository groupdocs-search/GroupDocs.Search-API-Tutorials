---
date: '2026-02-06'
description: Ismerje meg, hogyan indexelhet dokumentumokat, és adhat hozzá dokumentumokat
  az indexhez a GroupDocs.Search for Java használatával. Készítsen erőteljes keresőalkalmazásokat
  szöveg- és objektumlekérdezésekkel.
keywords:
- GroupDocs.Search Java
- document indexing in Java
- Java document search
title: Hogyan indexeljük a dokumentumokat a GroupDocs.Search for Java segítségével
type: docs
url: /hu/java/searching/master-document-search-groupdocs-java/
weight: 1
---

# Dokumentumok indexelése a GroupDocs.Search for Java segítségével

A mai adat‑központú világban a **dokumentumok hatékony indexelése** kritikus készség minden olyan Java fejlesztő számára, aki nagy fájlkészletekkel dolgozik. Akár jogi szerződéseket, pénzügyi kimutatásokat vagy belső jelentéseket kezel, a megfelelő információ gyors megtalálása órákat takaríthat meg a manuális munkában. Ebben az útmutatóban megtanulja, **hogyan indexeljen dokumentumokat** a GroupDocs.Search könyvtár segítségével, majd szöveges és objektumalapú lekérdezéseket hajtson végre a létrehozott indexen. Kezdjünk is!

## Gyors válaszok
- **Mi az első lépés a dokumentumok indexeléséhez?** Hozzon létre egy `Index` objektumot, amely egy olyan mappára mutat, ahol az index tárolva lesz.  
- **Melyik metódus ad dokumentumokat az indexhez?** Használja a `index.add("PATH_TO_DOCUMENTS")`-t.  
- **Kereshetek numerikus tartományokat?** Igen, egy szöveges lekérdezéssel, például `"400 ~~ 4000"` vagy egy objektum lekérdezéssel a `SearchQuery.createNumericRangeQuery` segítségével.  
- **Szükségem van licencre?** Elérhető egy ingyenes próba, a kereskedelmi licenc pedig a teljes funkciókat feloldja.  
- **Melyik Java verzió szükséges?** JDK 8 vagy újabb.

## Mi az a dokumentumok indexelése a GroupDocs.Search segítségével?
A dokumentumok indexelése azt jelenti, hogy egy mappában lévő fájlok tartalmát beolvassuk, és kereshető tokeneket tárolunk egy dedikált index mappában. Ez az előfeldolgozási lépés villámgyors kereséseket tesz lehetővé később, mivel a könyvtár a kész indexet keresgéli a nyers fájlok helyett.

## Miért használjuk a GroupDocs.Search for Java‑t?
- **Teljesítmény:** A keresések ezrek fájlja esetén is ezredmásodperc alatt lefutnak.  
- **Formátumtámogatás:** Kezeli a PDF‑eket, Word‑et, Excel‑t, PowerPoint‑ot és még sok mást.  
- **Rugalmasság:** Támogatja az egyszerű szöveges lekérdezéseket, numerikus tartományokat és összetett objektum lekérdezéseket.  
- **Skálázhatóság:** Az index könnyen frissíthető új dokumentumok hozzáadásával anélkül, hogy újra kellene építeni.

## Előkövetelmények
- Maven telepítve a függőségkezeléshez.  
- Egy IDE, például IntelliJ IDEA vagy Eclipse.  
- Alap Java ismeretek (OOP koncepciók, kivételkezelés).  

## A GroupDocs.Search for Java beállítása
### Maven beállítás
Adja hozzá a repót és a függőséget a `pom.xml`-hez:

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
A legújabb JAR‑t letöltheti a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról is.

#### Licenc megszerzésének lépései
1. **Ingyenes próba** – a könyvtár költség nélkül történő felfedezése.  
2. **Ideiglenes licenc** – kérjen rövid távú kulcsot a kiterjesztett értékeléshez.  
3. **Vásárlás** – szerezzen teljes licencet a termelési használathoz.

## Alap inicializálás és beállítás
A **dokumentumok indexhez adásához** először egy `Index` objektumot hoz létre, amely arra a mappára mutat, ahol az index fájlok tárolva lesznek:

```java
import com.groupdocs.search.Index;

// Initialize the index by specifying a directory path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");
```

Ez a sor létrehozza (vagy megnyitja) az indexet, amely készen áll a dokumentumok fogadására.

## Implementációs útmutató
### Dokumentumok létrehozása és indexelése
#### Hogyan adjunk dokumentumokat az indexhez
Az `add` metódus beolvassa egy mappa tartalmát, és kereshető adatokat tárol minden egyes fájlhoz.

```java
import com.groupdocs.search.Index;

// Initialize an index at the specified path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");

// Add documents from a directory for indexing
index.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Paraméterek:** Az útvonal karakterlánc arra a mappára mutat, amely a indexelni kívánt fájlokat tartalmazza.  
- **Cél:** Ez után az index tartalmazza az összes támogatott dokumentumtípus tokenjeit, lehetővé téve a gyors kereséseket.

### Szöveges lekérdezés keresés
#### Hogyan hajtsunk végre szöveges numerikus tartomány keresést
Kereshet egy egyszerű karakterlánc segítségével, amely meghatároz egy tartományt.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define a query for numeric values within a specific range
String query1 = "400 ~~ 4000";

// Execute text-based search on indexed data
SearchResult result1 = index.search(query1);
```

- **Paraméterek:** A `"400 ~~ 4000"` lekérdezési karakterlánc azt mondja a motornak, hogy találja meg a 400 és 4000 közötti számokat.  
- **Visszatérési érték:** A `SearchResult` tartalmazza a megfelelő dokumentumok listáját és a kiemeléseket.

### Objektum lekérdezés keresés
#### Hogyan használjunk objektum lekérdezést numerikus tartományokhoz
Az objektumalapú lekérdezések programozott vezérlést biztosítanak a keresési feltételek felett.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Create a numeric range query object
SearchQuery query2 = SearchQuery.createNumericRangeQuery(400, 4000);

// Perform search using the query object
SearchResult result2 = index.search(query2);
```

- **Paraméterek:** A `createNumericRangeQuery` megkapja a kezdő és befejező egész számokat.  
- **Cél:** Ez a metódus ideális, ha több feltételt kell kombinálni vagy dinamikusan kell lekérdezéseket építeni.

## Gyakorlati alkalmazások
Íme néhány valós példája annak, amikor a **dokumentumok indexelése** forradalmi hatású:

1. **Jogi dokumentumkezelés** – klauzulák, ügyszámok vagy dátumok keresése több ezer szerződésben.  
2. **Pénzügyi jelentés** – olyan tranzakciók lekérdezése, amelyek egy adott pénzügyi tartományba esnek.  
3. **Készletkövetés** – tételek keresése sorozatszám, tétel kód vagy SKU tartomány alapján.  

A GroupDocs.Search adatbázisokkal, felhőtárolóval vagy üzenetsorokkal való integrálása tovább automatizálhatja a dokumentum munkafolyamatokat.

## Teljesítmény szempontok
- **Rendszeres index frissítések:** Futtassa újra az `index.add`-t új fájlokhoz, hogy az index naprakész maradjon.  
- **Erőforrás-kezelés:** Figyelje a heap használatát; nagy indexek esetén előnyös a JVM szemétgyűjtés beállításainak finomhangolása.  
- **Lekérdezés optimalizálás:** Használjon objektum lekérdezéseket összetett szűrőkhez, hogy csökkentse a felesleges beolvasást.

## Gyakori problémák és megoldások
| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **A keresés nem ad eredményt** | Az index nincs felépítve vagy a mappa útvonala helytelen | Ellenőrizze, hogy az `index.add` a megfelelő könyvtárban lett végrehajtva, és hogy az index mappa írható. |
| **OutOfMemoryError indexelés közben** | Nagyon nagy fájlok vagy nem elegendő heap | Növelje a JVM `-Xmx` értékét, vagy kisebb adagokban indexelje a fájlokat. |
| **Nem támogatott fájlformátum** | A fájltípus nem ismerhető fel a GroupDocs.Search által | Győződjön meg róla, hogy a fájl kiterjesztése a támogatott listán szerepel (PDF, DOCX, XLSX, stb.). |

## Gyakran feltett kérdések
**Q: Hogyan frissíthetem a meglévő indexet új dokumentumokkal?**  
A: Hívja újra az `index.add("NEW_DOCUMENT_PATH")`-t; a könyvtár az új bejegyzéseket egyesíti anélkül, hogy újraépítené az egész indexet.

**Q: Kezelheti a GroupDocs.Search a különböző fájlformátumokat?**  
A: Igen, támogatja a PDF‑eket, Word‑et, Excel‑t, PowerPoint‑ot, egyszerű szöveget és számos más gyakori formátumot.

**Q: Mik a rendszerkövetelmények a GroupDocs.Search használatához?**  
A: Java 8+ futtatókörnyezet, elegendő RAM (legalább 2 GB közepes méretű gyűjteményekhez), és olvasási/írási hozzáférés az index mappához.

**Q: Hogyan háríthatom el a keresési teljesítményproblémákat?**  
A: Győződjön meg róla, hogy az index naprakész, profilozza a lekérdezéseket, és ellenőrizze a JVM memória beállításait. A indexelt mezők számának csökkentése is javíthatja a sebességet.

**Q: Van lehetőség szinonimákkal vagy fuzzy kereséssel keresni?**  
A: Igen, a GroupDocs.Search szinonima szótárakat és fuzzy keresési opciókat kínál, amelyeket a `SearchOptions` osztályon keresztül lehet engedélyezni.

## Következtetés
Most már alapos ismeretekkel rendelkezik a **dokumentumok indexeléséről** a GroupDocs.Search for Java használatával, arról, hogyan **adjunk dokumentumokat az indexhez**, és hogyan hajtsunk végre szöveges és objektumalapú lekérdezéseket egyaránt. E technikák integrálásával Java alkalmazásai gyors és pontos keresési élményt nyújtanak bármilyen dokumentumtárban.

Készen áll a következő lépésre? Fedezze fel a facettált keresést, a szinonima kezelést, vagy integrálja az indexet egy REST API‑val, hogy a keresési funkciókat más szolgáltatások számára is elérhetővé tegye.

---

**Utoljára frissítve:** 2026-02-06  
**Tesztelve a következővel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs