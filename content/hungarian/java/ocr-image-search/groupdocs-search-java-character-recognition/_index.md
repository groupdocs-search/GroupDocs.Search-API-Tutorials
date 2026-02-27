---
date: '2026-01-11'
description: Ismerje meg, hogyan hozhat létre egyedi keresési indexet a GroupDocs.Search
  for Java segítségével, szabályos és kevert karakterek beállításával a fejlett OCR-hez
  és képkereséshez.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Egyéni keresési index létrehozása karakterfelismeréssel – GroupDocs.Search
  Java
type: docs
url: /hu/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Egyedi keresési index létrehozása karakterfelismeréssel a GroupDocs.Search for Java használatával

A modern, dokumentum‑intenzív alkalmazásokban elengedhetetlen a **custom search index** létrehozása, amely megérti a szöveg finomságait – például a kötőjeleket, aláhúzásokat vagy nyelvspecifikus szimbólumokat – a gyors és pontos visszakeresés érdekében. Ez az útmutató végigvezet a karakterfelismerés konfigurálásán a **GroupDocs.Search for Java**‑ban, mind a szabályos karakterek (betűk, számjegyek, aláhúzások), mind a kevert karakterek (pl. kötőjelek) tekintetében. A végére képes lesz egy olyan index testreszabására, amely pontosan megfelel az OCR vagy képkeresési forgatókönyvének.

## Gyors válaszok
- **Mi jelenti a „create custom search index” kifejezést?** Ez azt jelenti, hogy egy indexet úgy konfigurálunk, hogy bizonyos szimbólumokat betűként vagy kevert karakterként kezelje, ahelyett, hogy figyelmen kívül hagyná őket.  
- **Melyik könyvtár van használatban?** GroupDocs.Search for Java (v25.4 a írás időpontjában).  
- **Szükségem van licencre?** A fejlesztéshez egy ingyenes próba verzió elegendő; a termeléshez fizetett licenc szükséges.  
- **Indexelhetek PDF‑eket és képeket is?** Igen – a GroupDocs.Search megfelelő beállítás esetén támogatja az OCR‑t képeken és PDF‑eken.  
- **Kell Maven?** A Maven a függőségek kezelésének ajánlott módja, de használhat Gradle‑t vagy manuális JAR‑okat is.  

## Mi az egyedi keresési index?
Az egyedi keresési index lehetővé teszi, hogy meghatározd, a keresőmotor hogyan értelmezi a karaktereket. Alapértelmezés szerint sok szimbólum figyelmen kívül marad, ami hiányzó találatokhoz vezethet például ügyiratszámok (`ABC-123`) vagy kódrészletek (`my_variable`) esetén. Az ábécé szótár módosításával teljes irányítást kapsz arról, hogy a motor mit tekint kereshető szövegnek.

## Miért konfiguráljuk a szabályos és kevert karaktereket?
- **Szabályos karakterek** (betűk, számjegyek, aláhúzások) önálló tokenként kezelődnek, javítva a pontos egyezésű kereséseket.  
- **Kevert karakterek** (kötőjelek, perjelek) összekapcsolják a szavakat; ezek konfigurálása megakadályozza a nem kívánt token szétválasztást, ami kulcsfontosságú jogi hivatkozások, termékkódok vagy forráskód indexelése esetén.  

## Előfeltételek
- **JDK 8** vagy újabb telepítve.  
- **Maven** a függőségek kezeléséhez.  
- Hozzáférés a **GroupDocs.Search for Java** könyvtárhoz (Maven‑en vagy a hivatalos weboldalon keresztül letölthető).  

### Szükséges könyvtárak és függőségek
Adja hozzá a tárolót és a függőségi bejegyzéseket a `pom.xml` fájlhoz (az alább látható módon). Az XML blokkot változatlanul kell hagyni.

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

A legújabb JAR‑okat letöltheti a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc beszerzése
- **Free Trial** – tökéletes a korai kísérletezéshez.  
- **Temporary License** – hasznos hosszabb fejlesztési ciklusokhoz.  
- **Production License** – szükséges a kereskedelmi üzembe helyezéshez.  

Licencet szerezhet a hivatalos portálon: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Alap inicializálás
Az alábbi kódrészlet mutatja a minimális kódot egy üres index elindításához. Hagyja változatlanul; később bővítjük.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## A GroupDocs.Search for Java beállítása

### Telepítés Maven‑en keresztül
A *Prerequisites* szakaszból származó Maven‑konfiguráció minden, amire szüksége van. Hozzáadás után futtassa a `mvn clean install` parancsot a binárisok letöltéséhez.

### Környezet beállítási követelmények
- Győződjön meg arról, hogy a **index mappa** és a **dokumentum mappa** létezik a lemezen.  
- Használjon abszolút útvonalakat, vagy konfigurálja az IDE‑t, hogy helyesen oldja fel a relatív útvonalakat.  

## Implementációs útmutató
Az alábbiakban két különálló funkciót mutatunk be: **regular characters** és **blended characters**. Minden funkció ugyanazt a mintát követi – meghatározza az útvonalakat, létrehozza az indexet, beállítja a karakter szótárat, és végül indexeli a dokumentumokat.

### 1. funkció – Szabályos karakterek

#### Áttekintés
A szabályos karakterek független tokenként kezelődnek. Ideális, ha a számjegyeket, betűket és aláhúzásokat pontosan úgy szeretné keresni, ahogy megjelennek.

#### Lépésről‑lépésre megvalósítás

**1️⃣ Útvonalak beállítása**  
Határozza meg, hogy hol tárolja az indexet, és hol vannak a forrásdokumentumok.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Index létrehozása és konfigurálása**  
Példányosítsa az indexet, és törölje az esetleg már meglévő ábécé beállítást.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Szabályos karakterek meghatározása**  
Készítsen karaktertömböt, amely tartalmazza a számjegyeket, a latin betűket és az aláhúzást.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Dokumentumok indexelése**  
Adja hozzá az összes fájlt a forrásmappából az újonnan konfigurált indexhez.

```java
index.add(documentFolder);
```

### 2. funkció – Kevert karakterek

#### Áttekintés
A kevert karakterek (például a kötőjelek) gyakran összekapcsolnak két szót. Ha *blended*-ként jelöljük őket, a motor az indexelés során egyben tartja a környező tokeneket.

#### Lépésről‑lépésre megvalósítás

**1️⃣ Útvonalak beállítása**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Index létrehozása és konfigurálása**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Kevert karakterek meghatározása**  
Itt azt mondjuk meg a szótárnak, hogy a kötőjelet kevert karakterként kezelje.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Dokumentumok indexelése**  

```java
index.add(documentFolder);
```

## Gyakorlati alkalmazások

### 1. eset – Jogi dokumentumkezelés
A jogi fájlok gyakran tartalmaznak ügyiratszámokat, például `2023-AB-456`. Az aláhúzások és kötőjelek konfigurálásával a keresés pontos egyezéseket ad vissza, anélkül, hogy szétválasztaná az azonosítót.

### 2. eset – Forráskód tárolók
A fejlesztőknek olyan kódrészleteket kell keresniük, ahol az aláhúzások (`my_variable`) és a kötőjelek (`my-function`) jelentőséggel bírnak. Az egyedi karakterfelismerés biztosítja, hogy a keresőmotor tiszteletben tartja ezeket a szimbólumokat.

### 3. eset – Többnyelvű adathalmazok
Ha olyan nyelvekkel dolgozik, amelyek további ábécéket használnak, kibővítheti a szabályos karakterkészletet a megfelelő Unicode tartományokkal, ezáltal biztosítva a pontos többnyelvű keresési eredményeket.

## Teljesítménybeli megfontolások
- **Resource Management** – Figyelje a heap használatot; a nagy indexek előnyben részesítik az inkrementális commit‑okat.  
- **Garbage Collection** – Szabadítsa fel az `Index` objektumokat, amikor már nincs rájuk szükség, hogy a JVM visszanyerje a memóriát.  
- **Index Optimization** – Időnként hívja meg a `index.optimize()` metódust (ha elérhető), hogy tömörítse az indexet és javítsa a lekérdezési sebességet.  

## Következtetés
Most már tudja, hogyan **hozzon létre egy egyedi keresési indexet**, amely megkülönbözteti a szabályos és kevert karaktereket a GroupDocs.Search for Java használatával. Ez a finomhangolt vezérlés lehetővé teszi, hogy OCR‑tudatos, nagy teljesítményű keresési megoldásokat építsen, amelyek a jogi, fejlesztői vagy többnyelvű környezetekhez igazodnak.

**Következő lépések**  
- Kísérletezzen további Unicode tartományokkal a nem latin ábécékhez.  
- Kombinálja a karakterkonfigurációt más GroupDocs.Search funkciókkal, például stemminggel vagy szinonimákkal.  
- Integrálja az indexet egy REST API‑ba, hogy a keresési képességeket front‑end alkalmazások számára tegye elérhetővé.

## Gyakran ismételt kérdések

**Q:** *Mi a `CharacterType.Letter` célja?*  
**A:** Azt mondja az indexnek, hogy a megadott karaktereket szabályos betűként kezelje, így az indexelés során külön tokenekre bontja őket.

**Q:** *Keverhetek szabályos és kevert karaktereket ugyanabban az indexben?*  
**A:** Igen – egyszerűen hívja meg a `setRange` metódust minden típusra; a szótár egyidejűleg kezeli mindkét konfigurációt.

**Q:** *Újra kell építeni az indexet az ábécé módosítása után?*  
**A:** Teljesen igaz. A karakter szótár változásai befolyásolják a tokenizálást, ezért újra kell indexelni a dokumentumokat az új szabályok alkalmazásához.

**Q:** *Van korlát a definiálható egyedi karakterek számában?*  
**A:** A könyvtár támogatja a teljes Unicode tartományt; a teljesítmény romolhat, ha rendkívül nagy halmazt ad hozzá, ezért korlátozza a ténylegesen szükséges karakterekre.

**Q:** *Hogyan befolyásolja ez az OCR pontosságát?*  
**A:** Az index karakterkészletének az OCR motor kimenetéhez való igazításával csökkenti a hamis negatív eredményeket és javítja a keresés általános relevanciáját.

---

**Utoljára frissítve:** 2026-01-11  
**Tesztelve:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs