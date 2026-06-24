---
date: '2026-03-23'
description: Ismerje meg, hogyan adhat dokumentumokat az indexhez, és optimalizálhatja
  a keresési indexet a GroupDocs.Search for Java segítségével, lehetővé téve a hatékony
  helyettesítő karakteres kereséseket.
keywords:
- wildcard searches in Java
- text-based wildcard search
- object-based wildcard search
title: Dokumentumok hozzáadása az indexhez – Helyettesítő karakteres keresések Java-ban
type: docs
url: /hu/java/searching/wildcard-searches-groupdocs-java-guide/
weight: 1
---

# Dokumentumok hozzáadása az indexhez – A helyettesítő karakteres keresések elsajátítása Java-ban a GroupDocs.Search segítségével

Fedezd fel a szöveg‑ és objektumalapú helyettesítő karakteres keresések erejét a GroupDocs.Search for Java használatával. Ebben az útmutatóban megtanulod, hogyan **adj dokumentumokat az indexhez**, hogyan konfigurálj fejlett mintákat, és hogyan tartsd optimalizálva a keresési indexet a gyors eredmények érdekében.

## Gyors válaszok
- **Mit jelent a „dokumentumok hozzáadása az indexhez”?** Egy kereshető adatstruktúrát hoz létre, amelyet a GroupDocs.Search hatékonyan tud lekérdezni.  
- **Melyik kulcsszó növeli a teljesítményt?** A tömör helyettesítő karakteres minták használata és a rendszeres **optimize search index** műveletek.  
- **Szükség van speciális memória beállításokra?** Igen – figyeld a **java search memory management** beállításokat, hogy elkerüld a memóriahiányt nagy adathalmazok esetén.  
- **Használhatom ezeket a funkciókat Spring Boot alkalmazásban?** Természetesen; csak add hozzá a Maven‑függőséget és konfiguráld az index mappát.  
- **Szükséges licenc a termeléshez?** Egy érvényes GroupDocs.Search licenc szükséges a kereskedelmi telepítésekhez.

## Mi az a „dokumentumok hozzáadása az indexhez” a GroupDocs.Search‑ben?
A dokumentumok indexhez adása azt jelenti, hogy a forrásfájljaidat (PDF, DOCX, TXT stb.) egy kereshető tárolóba töltöd, amelyet a GroupDocs.Search a háttérben épít fel. Az indexelés után gyors helyettesítő karakteres lekérdezéseket futtathatsz anélkül, hogy minden alkalommal a eredeti fájlokat kellene átvizsgálnod.

## Miért használjunk helyettesítő karakteres kereséseket a GroupDocs.Search‑szel?
A helyettesítő karakteres keresések lehetővé teszik részleges szavak vagy minták egyezését – tökéletes megoldás olyan helyzetekben, amikor a felhasználók csak egy kifejezés részletét emlékezik. Ez a rugalmasság javítja a felhasználói élményt dokumentumkezelő rendszerekben, tartalomportálokban és adatbányászati eszközökben.

## Előfeltételek
- **Java Development Kit (JDK)** – 8-as vagy újabb verzió.  
- Alapvető Java programozási ismeretek.  
- IntelliJ IDEA vagy Eclipse fejlesztőkörnyezet.  
- Maven a függőségkezeléshez (vagy letöltheted a JAR‑t közvetlenül).  

## A GroupDocs.Search for Java beállítása

### Maven beállítás
Add hozzá a tárolót és a függőséget a `pom.xml` fájlodhoz:

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
Ha nem szeretnél Maven‑t használni, töltsd le a legújabb JAR‑t a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldaláról.

### Licenc megszerzése
- **Ingyenes próba:** Fedezd fel a fő funkciókat költség nélkül.  
- **Ideiglenes licenc:** Aktiváld a fejlett képességeket értékelés közben.  
- **Vásárlás:** Szerezz kereskedelmi licencet a termelési környezethez.

## Implementációs útmutató

### Funkció 1: Szöveg‑alapú helyettesítő karakteres keresés

#### 1. lépés – Az index beállítása és **dokumentumok hozzáadása az indexhez**
Először hozz létre egy index mappát, majd add hozzá a forrásdokumentumokat:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\AdvancedUsage\\Searching\\WildcardSearch\\QueryInTextForm";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

Index index = new Index(indexFolder);
index.add(documentsFolder);
```

#### 2. lépés – Helyettesítő karakteres lekérdezések végrehajtása
Futtass minta‑alapú kereséseket közvetlenül a szövegen:

```java
// Search for words matching 'm???is'
String query1 = "m???is";
SearchResult result1 = index.search(query1); // Finds words like 'mauris', 'mollis'

// Search for words matching 'pri?(1~7)'
String query2 = "pri?(1~7)";
SearchResult result2 = index.search(query2); // Finds words like 'private', 'principles'
```

**Magyarázat**  
- `indexFolder` a kereshető indexet tárolja a lemezen.  
- `documentsFolder` arra a helyre mutat, ahol a **dokumentumok hozzáadása az indexhez** kívánt fájlok találhatók.  
- `search()` végrehajtja a helyettesítő karakteres lekérdezést, és visszaadja a találatokat.

### Funkció 2: Objektum‑alapú helyettesítő karakteres keresés

#### 1. lépés – Az index beállítása (ugyanúgy, mint korábban)
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\AdvancedUsage\\Searching\\WildcardSearch\\QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

#### 2. lépés – `WordPattern` építése összetett lekérdezésekhez
Az objektumalapú keresések finom kontrollt biztosítanak minden mintaelem felett:

```java
// Create a WordPattern for 'm???is'
WordPattern pattern1 = new WordPattern();
pattern1.appendString("m");
pattern1.appendOneCharacterWildcard();
pattern1.appendOneCharacterWildcard();
pattern1.appendOneCharacterWildcard();
pattern1.appendString("is");

SearchQuery query1 = SearchQuery.createWordPatternQuery(pattern1);
SearchResult result1 = index.search(query1); // Finds words like 'mauris', 'mollis'

// Create a WordPattern for 'pri?(1~7)'
WordPattern pattern2 = new WordPattern();
pattern2.appendString("pri");
pattern2.appendWildcard(1, 7);

SearchQuery query2 = SearchQuery.createWordPatternQuery(pattern2);
SearchResult result2 = index.search(query2); // Finds words like 'private', 'principles'
```

**Magyarázat**  
- A `WordPattern` lehetővé teszi a keresési minta lépésről‑lépésre történő összeállítását.  
- `appendOneCharacterWildcard()` egy `?` helyőrzőt ad hozzá.  
- `appendWildcard(min, max)` egy tartomány‑alapú helyettesítő karaktert (`?(min~max)`) ad hozzá.  

## Gyakorlati alkalmazások
1. **Dokumentumkezelés:** Gyorsan megtalálja a fájlokat, ha csak a kifejezés egy része ismert.  
2. **Tartalom‑lekérdező motorok:** Rugalmas egyezést biztosít a CMS platformok keresősávjaiban.  
3. **Adatbányászat:** Mintázatos adatot nyer ki nagy korpuszokból teljes szöveges átvizsgálás nélkül.

## Teljesítmény‑szempontok

### Keresési index optimalizálása
- **Rendszeres újra‑indexelés:** Tömeges frissítések után építsd újra az indexet, hogy alacsonyan tartsd a keresési időket.  
- **Tömör tárolás:** Használd az `index.optimize()` (ha elérhető) metódust az index méretének csökkentéséhez.

### Java keresési memória kezelése
- **Heap méret:** Rendeljen elegendő heap‑memóriát (`-Xmx2g` vagy nagyobb) nagy dokumentumkészletekhez.  
- **Streaming indexelés:** Fájlok batch‑enkénti feldolgozása, hogy ne kelljen mindent egyszerre a memóriába betölteni.

### Általános legjobb gyakorlatok
- A helyettesítő karakteres mintákat tedd a lehető legspecifikusabbá; a túl általános minták CPU‑terhelést növelnek.  
- Figyeld a GC‑szüneteket, ha késleltetés‑csúcsokat észlelsz nehéz keresési terhelés alatt.

## Következtetés
A **dokumentumok hozzáadása az indexhez** és a szöveg‑ és objektumalapú helyettesítő karakteres lekérdezések használatának elsajátításával drámaian javíthatod a keresési élményt bármely Java‑alkalmazásban. Ne felejtsd el rendszeresen **optimize search index**‑et futtatni, és bölcsen kezelni a memóriát a skálázható teljesítmény érdekében. Kísérletezz különböző mintákkal, integráld a kódot a szolgáltatásaidba, és élvezd a gyors, rugalmas keresési eredményeket még ma!

## Gyakran Ismételt Kérdések

**Q1: Mi az a helyettesítő karakteres keresés?**  
A: A helyettesítő karakteres keresés lehetővé teszi szavak vagy kifejezések egyezését `?` (egyes karakter) vagy `*` (több karakter) helyőrzőkkel.

**Q2: Hogyan telepíthetem a GroupDocs.Search for Java‑t?**  
A: Használd a fent bemutatott Maven‑tárolót és függőséget, vagy töltsd le a JAR‑t közvetlenül a hivatalos kiadási oldalról.

**Q3: Kezelhetnek a helyettesítő karakteres keresések nagy adatállományokat?**  
Igen, de rendszeresen **optimize search index**‑et kell futtatni, és figyelni a **java search memory management** beállításokra a teljesítmény fenntartása érdekében.

**Q4: Mik a gyakori buktatók?**  
A: Hibás index útvonalak, túl általános helyettesítő karakterek használata, valamint a memória‑konfiguráció elhanyagolása lassú kereséseket vagy memória‑hiányt okozhat.

**Q5: Hol találok további forrásokat?**  
Látogasd meg a [GroupDocs dokumentációt](https://docs.groupdocs.com/search/java/) a részletes útmutatók és API‑referenciákért.

## Források

- **Dokumentáció:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API‑referencia:** [GroupDocs Search API Reference](https://reference.groupdocs.com/search/java)
- **Letöltés:** [GroupDocs.Search Downloads](https://releases.groupdocs.com/search/java/)
- **GitHub:** [GroupDocs.Search on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Ingyenes támogatás:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Ideiglenes licenc:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**Utoljára frissítve:** 2026-03-23  
**Tesztelt verzió:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs  

---