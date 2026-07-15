---
date: '2026-03-17'
description: Tanulja meg, hogyan hozhat létre indexet a GroupDocs.Search for Java
  segítségével, hogyan konfigurálhatja a szabályos és kevert karaktereket, és hogyan
  optimalizálhatja a keresést jogi ügyiratszámok és OCR képek esetén.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Hogyan hozzunk létre indexet karakterfelismeréssel Java-ban
type: docs
url: /hu/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

, links unchanged.

Check for any missing shortcodes: none.

Now produce final content.# Hogyan hozzunk létre indexet karakterfelismeréssel a GroupDocs.Search for Java használatával

A modern, dokumentum‑intenzív alkalmazásokban elengedhetetlen, hogy a **how to create index** figyelembe vegye a szöveg finomságait – például a kötőjeleket, aláhúzásokat vagy nyelvspecifikus szimbólumokat – a gyors és pontos visszakeresés érdekében. Ebben az útmutatóban végigvezetünk a karakterfelismerés beállításán a **GroupDocs.Search for Java**‑ban, lefedve a szabályos karaktereket (betűk, számok, aláhúzások) és a kevert karaktereket (például kötőjelek). A végére képes lesz testre szabni egy indexet, amely pontosan megfelel az OCR vagy képes keresési forgatókönyvének, legyen szó jogi ügyiratszámok, forráskód-repozitóriumok vagy többnyelvű PDF‑ek indexeléséről.

## Gyors válaszok
- **What does “create custom search index” mean?** Azt jelenti, hogy egy indexet úgy konfigurálunk, hogy bizonyos szimbólumokat betűként vagy kevert karakterként kezelje, ahelyett, hogy figyelmen kívül hagyná őket.  
- **Which library is used?** GroupDocs.Search for Java (v25.4 a írás időpontjában).  
- **Do I need a license?** Egy ingyenes próba a fejlesztéshez megfelelő; a termeléshez fizetett licenc szükséges.  
- **Can I index both PDFs and images?** Igen – a GroupDocs.Search támogatja az OCR‑t képeken és PDF‑eken, ha megfelelően van beállítva.  
- **Is Maven required?** A Maven a javasolt módja a függőségek kezelésének, de használhat Gradle‑t vagy manuális JAR‑okat is.

## Mi az egyedi keresőindex?
Az egyedi keresőindex lehetővé teszi, hogy meghatározd, a keresőmotor hogyan értelmezi a karaktereket. Alapértelmezés szerint sok szimbólum figyelmen kívül marad, ami hiányzó egyezéseket eredményezhet például ügyiratszámok (`2023-AB-456`) vagy kódrészletek (`my_variable`) esetén. Az ábécé szótár beállításával teljes irányítást kapsz arról, hogy a motor mi tekinthető kereshető szövegnek.

## Miért konfiguráljunk szabályos és kevert karaktereket jogi ügyiratszámokhoz?
- **Regular characters** (betűk, számok, aláhúzások) külön tokenizálódnak, lehetővé téve a pontos egyezésű kereséseket az azonosítókra.  
- **Blended characters** (kötőjelek, perjelek) egyesítik a kapcsolódó tokeneket, megakadályozva a nem kívánt szétválást az ügyiratszámok, termékkódok vagy fájlutak esetén.  
- Ez a beállítás **optimalizálja a keresőindex** teljesítményét azáltal, hogy csökkenti a token fragmentációt és javítja a relevanciát az OCR‑által generált tartalmaknál.

## Előkövetelmények
- **JDK 8** vagy újabb telepítve.  
- **Maven** a függőségkezeléshez.  
- Hozzáférés a **GroupDocs.Search for Java** könyvtárhoz (letölthető Maven‑on vagy a hivatalos oldalról).

### Szükséges könyvtárak és függőségek
Adja hozzá a tárolót és a függőségi bejegyzéseket a `pom.xml`‑hez (az alább látható módon). Az XML blokkot változatlanul kell hagyni.

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

A legújabb JAR‑okat letöltheti innen: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenc beszerzése
- **Free Trial** – tökéletes a korai kísérletezéshez.  
- **Temporary License** – hasznos hosszabb fejlesztési ciklusokhoz.  
- **Production License** – szükséges a kereskedelmi üzembe helyezéshez.  

Szerezzen licencet a hivatalos portálon: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

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

### Telepítés Maven‑nel
A *Prerequisites* szakaszból származó Maven‑konfiguráció minden, amire szüksége van. Hozzáadás után futtassa a `mvn clean install` parancsot a binárisok letöltéséhez.

### Környezet beállítási követelmények
- Győződjön meg róla, hogy a **index mappa** és a **dokumentum mappa** létezik a lemezen.  
- Használjon abszolút útvonalakat, vagy konfigurálja az IDE‑t, hogy helyesen oldja fel a relatív útvonalakat.

## Implementációs útmutató

Az alábbiakban két különálló funkciót mutatunk be: **regular characters** és **blended characters**. Minden funkció ugyanazt a mintát követi – meghatározza az útvonalakat, létrehozza az indexet, beállítja a karakter szótárat, és végül indexeli a dokumentumokat.

### 1. funkció – Szabályos karakterek

#### Áttekintés
A szabályos karaktereket független tokenekként kezelik. Ideális, ha a számok, betűk és aláhúzások pontosan úgy legyenek kereshetők, ahogy megjelennek.

#### Lépésről‑lépésre megvalósítás

**1️⃣ Set Up Paths**  
Határozza meg, hogy hol tárolódik az index és hol vannak a forrásdokumentumok.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  
Példányosítsa az indexet, és törölje az esetleg korábban beállított ábécé konfigurációt.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Define Regular Characters**  
Hozzon létre egy karaktertömböt, amely tartalmazza a számokat, latin betűket és az aláhúzást.

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

**4️⃣ Index Documents**  
Adja hozzá az összes fájlt a forrásmappából az újonnan konfigurált indexhez.

```java
index.add(documentFolder);
```

### 2. funkció – Kevert karakterek

#### Áttekintés
A kevert karakterek (például a kötőjelek) gyakran összekapcsolnak két szót. Ha *blended*-ként jelöljük őket, a motor a tokenek körülötte egyben tartja az indexelés során.

#### Lépésről‑lépésre megvalósítás

**1️⃣ Set Up Paths**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Define Blended Characters**  
Itt azt mondjuk a szótárnak, hogy a kötőjelet kevert karakterként kezelje.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index Documents**  

```java
index.add(documentFolder);
```

## Gyakorlati alkalmazások

### 1. eset – Jogi dokumentumkezelés
A jogi fájlok gyakran tartalmaznak ügyiratszámokat, például `2023-AB-456`. Az aláhúzások és kötőjelek konfigurálásával a keresés pontos egyezéseket ad anélkül, hogy szétbontaná az azonosítót, így hatékonyan **kereshet jogi ügyiratszámokat**.

### 2. eset – Forráskód-repozitóriumok
A fejlesztőknek kódrészleteket kell keresniük, ahol az aláhúzások (`my_variable`) és a kötőjelek (`my-function`) jelentőséggel bírnak. Az egyedi karakterfelismerés biztosítja, hogy a keresőmotor tiszteletben tartja ezeket a szimbólumokat.

### 3. eset – Többnyelvű adatkészletek
Ha olyan nyelvekkel dolgozik, amelyek további ábécéket használnak, **kiterjesztheti a Unicode karakterkészletet** ezeknek a tartományoknak a belefoglalásával, ezáltal biztosítva a pontos többnyelvű keresési eredményeket.

### 4. eset – PDF‑képek indexelése
Ha beolvasott PDF‑eket vagy képfájlokat indexel, az OCR kimenete gyakran vegyes karaktereket tartalmaz. A szabályos és kevert karakterek megfelelő beállítása **optimalizálja a keresőindex** teljesítményét a képalapú tartalmaknál.

## Teljesítményfontosságú szempontok

- **Resource Management** – Figyelje a heap használatát; a nagy indexek előnyben részesítik az inkrementális commit‑okat.  
- **Garbage Collection** – Szabadítsa fel a `Index` objektumokat, amikor már nincs rájuk szükség, hogy a JVM visszanyerje a memóriát.  
- **Index Optimization** – Időnként hívja meg a `index.optimize()` (ha elérhető) metódust az index tömörítéséhez és a lekérdezési sebesség javításához.

## Következtetés

Most már tudja, **hogyan hozzunk létre indexet**, amely megkülönbözteti a szabályos és kevert karaktereket a GroupDocs.Search for Java használatával. Ez a finomhangolt vezérlés lehetővé teszi, hogy OCR‑tudatos, nagy teljesítményű keresési megoldásokat építsen, amelyek a jogi, fejlesztési vagy többnyelvű környezetekhez igazodnak.

### Következő lépések
- Kísérletezzen további Unicode tartományokkal a nem latin ábécékhez.  
- Kombinálja a karakterbeállítást más GroupDocs.Search funkciókkal, például stemminggel vagy szinonimákkal.  
- Integrálja az indexet egy REST API‑ba, hogy a keresési képességeket front‑end alkalmazások számára elérhetővé tegye.

## Gyakran Ismételt Kérdések

**Q:** *Mi a célja a `CharacterType.Letter`-nek?*  
**A:** Azt mondja az indexnek, hogy a megadott karaktereket szabályos betűként kezelje, így az indexelés során külön tokenizálódnak.

**Q:** *Keverhetek szabályos és kevert karaktereket ugyanabban az indexben?*  
**A:** Igen – egyszerűen hívja meg a `setRange`‑t minden típusra; a szótár egyszerre kezeli mindkét konfigurációt.

**Q:** *Újra kell építeni az indexet az ábécé módosítása után?*  
**A:** Határozottan. A karakter szótár változásai befolyásolják a tokenizálást, ezért újra kell indexelni a dokumentumokat az új szabályok alkalmazásához.

**Q:** *Van korlát a definiálható egyedi karakterek számában?*  
**A:** A könyvtár támogatja a teljes Unicode tartományt; a teljesítmény romolhat, ha rendkívül nagy halmazt ad hozzá, ezért korlátozza a ténylegesen szükséges karakterekre.

**Q:** *Hogyan befolyásolja ez az OCR pontosságát?*  
**A:** Az index karakterkészletének az OCR motor kimenetéhez való igazításával csökkenti a hamis negatív találatokat és javítja a keresés általános relevanciáját.

---

**Last Updated:** 2026-03-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs