---
date: '2026-08-05'
description: Ismerje meg, hogyan tisztítható meg a könyvtár Java-ban, miközben automatizáljuk
  a document indexing-et, a renaming files-et és a copying content-et a GroupDocs.Search
  segítségével.
keywords:
- how to clean directory
- copy files java
- delete all files folder
- how to rename files
- rename files java
- create searchable index
lastmod: '2026-08-05'
og_description: Ismerje meg, hogyan tisztítható meg a könyvtár Java-ban, miközben
  automatikusan létrehozzuk a searchable index-et, a renaming files-et és a copying
  content-et a GroupDocs.Search segítségével. Kövesse a step‑by‑step útmutatót és
  a best‑practice tippeket.
og_image_alt: 'Developer guide: clean directory in Java using GroupDocs.Search'
og_title: Hogyan tisztítsuk meg a könyvtárat Java-ban a GroupDocs.Search segítségével
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to clean directory in Java while automating document indexing,
    renaming files, and copying content using GroupDocs.Search.
  headline: How to clean directory in Java with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: Yes. The `Files.walk()` approach recursively deletes all nested files
      and folders.
    question: Can I clean a directory that contains sub‑folders?
  - answer: No. Sending a rename notification and calling `index.update()` is sufficient.
    question: Do I need to rebuild the whole index after each rename?
  - answer: It depends on JVM memory; processing in smaller batches or using streams
      helps manage large data sets.
    question: How large a folder can I clean before hitting performance limits?
  - answer: A free trial is available, but a paid license is required for production
      use.
    question: Is GroupDocs.Search free for development?
  - answer: Absolutely. GroupDocs.Search supports many formats; just add the folder
      containing those files to the index.
    question: Can I use this approach with other file types (e.g., PDFs, DOCX)?
  type: FAQPage
tags:
- clean directory
- GroupDocs.Search
- Java file management
- document indexing
- file renaming
title: Hogyan tisztítsuk meg a könyvtárat Java-ban a GroupDocs.Search segítségével
type: docs
url: /hu/java/indexing/automate-document-indexing-groupdocs-search-java/
weight: 1
---

# Hogyan tisztítsuk meg a könyvtárat Java-ban a GroupDocs.Search segítségével

Ha **clean directory java**-t kell végeznie a dokumentumok indexelésének és átnevezésének automatizálása közben, jó helyen jár. A fájlok mozgatásának, törlésének és az index frissítésének kézi kezelése hibára hajlamos és időigényes. Ebben az útmutatóban megmutatjuk, hogyan tud Java tisztítani egy mappát, kereshető indexet építeni, fájlokat átnevezni, és mindent szinkronban tartani a **GroupDocs.Search for Java** használatával.

## Gyors válaszok
- **Mi jelent a “clean directory java”?** A célkönyvtárban lévő összes fájl és alkönyvtár törlése Java kóddal.  
- **Melyik könyvtár hozza létre a kereshető indexet?** GroupDocs.Search for Java.  
- **Hogyan nevezhetek át egy dokumentumot és tarthatom naprakészen az indexet?** Használja a `File.renameTo()`-t, majd értesítse az indexet a `Notification.createRenameNotification` segítségével.  
- **Másolhatok fájlokat a mappa tisztítása után?** Igen – a Java Streams képes fájlokat másolni az index megőrzése mellett.  
- **Szükséges licenc a termeléshez?** Érvényes GroupDocs.Search licenc szükséges a kereskedelmi használathoz.

## Mi a könyvtár tisztítása?
**How to clean directory** arra utal, hogy programozottan eltávolítunk minden fájlt és alkönyvtárat egy megadott mappából. Ez a lépés biztosítja, hogy a régi vagy duplikált adatok ne zavarják a későbbi indexelést vagy másolási műveleteket. Gyakran használják kötegelt feldolgozás, adatátvitel vagy keresőindex újraépítése előtt, hogy csak friss tartalom legyen jelen. A tisztítás automatizálásával a fejlesztők elkerülhetik a kézi hibákat, és beépíthetik a lépést a CI folyamatokba.

## Miért automatizáljuk a dokumentumok indexelését és átnevezését?
Az ilyen feladatok automatizálása megszünteti a kézi munkát, csökkenti az emberi hibákat, és garantálja, hogy a kereshető index mindig a fájlrendszer aktuális állapotát tükrözze. A GroupDocs.Search több mint **50+ fájlformátumot** tud indexelni, és több száz oldalas dokumentumokat kezel anélkül, hogy a teljes fájlt a memóriába töltené, így gyors és megbízható keresési eredményeket biztosít.

## Előkövetelmények
- **GroupDocs.Search for Java** (Version 25.4 vagy későbbi) – támogat 50+ bemeneti és kimeneti formátumot.  
- JDK 8 + és egy IDE, például IntelliJ IDEA vagy Eclipse.  
- Alap Java ismeretek, különösen fájl I/O.  

## A GroupDocs.Search for Java beállítása

### Maven függőség
Adja hozzá a tárolót és a függőséget a `pom.xml`-hez:

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
Alternatívaként töltse le a legújabb verziót a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc
Szerezzen be egy ingyenes próbaidőszakot, egy ideiglenes értékelő licencet, vagy vásároljon teljes licencet a termelési használathoz.

### Alap inicializálás
Hozzon létre egy `Index` példányt, amely a kereshető adatokat tárolja:

```java
import com.groupdocs.search.Index;

public class Main {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/DocumentIndexingAndRenaming/Index";
        Index index = new Index(indexFolder);
    }
}
```

**Definition anchor:** A `Index` osztály a GroupDocs.Search központi komponense, amely kereshető metaadatokat tárol, és módszereket biztosít dokumentumok hozzáadásához, frissítéséhez vagy törléséhez.

## Hogyan tisztítsuk meg a könyvtárat Java-ban?
Töltse be a célmappát, járja be a fájrafáját, és törölje minden bejegyzést fordított sorrendben. Ez a megközelítés garantálja, hogy a fájlok a szülőkönyvtárak előtt kerülnek törlésre, elkerülve a „könyvtár nem üres” hibákat.

A `Files.walk()` metódus egy `Path` objektumok áramát adja vissza, amelyek a megadott gyökér alatt lévő minden fájlt és alkönyvtárat képviselik. A `Comparator.reverseOrder()`-rel rendezés biztosítja, hogy a mélyebb útvonalak a szülők előtt legyenek feldolgozva, lehetővé téve a biztonságos törlést.

```java
import java.io.File;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class DirectoryCleaningAndFileCopying {
    public static void main(String[] args) throws IOException {
        String targetDirectory = "YOUR_DOCUMENT_DIRECTORY/DocumentIndexingAndRenaming/Documents/";

        Files.walk(Paths.get(targetDirectory))
             .map(Path::toFile)
             .sorted((o1, o2) -> -o1.compareTo(o2))
             .forEach(File::delete);
    }
}
```

*Magyarázat:*  
- `Files.walk()` rekurzívan felsorolja az összes fájlt és alkönyvtárat.  
- A `Comparator.reverseOrder()`-rel rendezés biztosítja a megfelelő törlési sorrendet.

## Hogyan nevezhetünk át fájlokat Java-ban, miközben az index pontos marad?
Nevezze át a fizikai fájlt a `Files.move()` (vagy egyszerű esetekben a `File.renameTo()`) segítségével, majd küldjön egy átnevezési értesítést az indexnek, hogy a keresési eredmények helyesek maradjanak.

`Files.move()` atomikusan mozgat vagy átnevezi a fájlt, megbízhatóbb megoldást nyújtva a `File.renameTo()`-nál különböző platformokon.

```java
import com.groupdocs.search.Notification;

public class DocumentIndexingAndRenaming {
    public static void main(String[] args) {
        // Define paths for renaming
        String oldDocumentPath = "YOUR_DOCUMENT_DIRECTORY/DocumentIndexingAndRenaming/Documents/Lorem ipsum.txt";
        String newDocumentPath = "YOUR_DOCUMENT_DIRECTORY/DocumentIndexingAndRenaming/Documents/Lorem ipsum renamed.txt";

        java.io.File fileToRename = new java.io.File(oldDocumentPath);
        boolean renameSuccessful = fileToRename.renameTo(new java.io.File(newDocumentPath));

        if (renameSuccessful) {
            // Notify the index about the renaming
            Notification notification = Notification.createRenameNotification(oldDocumentPath, newDocumentPath);
            index.notifyIndex(notification);

            // Update the index to reflect changes
            index.update();
        }
    }
}
```

**Definition anchor:** A `Notification.createRenameNotification()` egy értesítési objektumot hoz létre, amely tájékoztatja a GroupDocs.Search-et, hogy egy dokumentum neve megváltozott, és az index frissíti a belső hivatkozásait.

## Hogyan másolhatunk fájlokat Java-ban a könyvtár tisztítása után?
Miután a mappa tiszta, új fájlokat másolhat bele Java Streams segítségével. A másolási művelet felülírja a meglévő fájlokat, biztosítva, hogy a mappa a dokumentumok legújabb verzióját tartalmazza. Ez a lépés általában a újonnan másolt fájlok indexhez adásával következik, hogy azonnal kereshetővé váljanak.

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.stream.Stream;

public class DirectoryCleaningAndFileCopying {
    public static void main(String[] args) throws IOException {
        String sourceDirectory = "YOUR_SOURCE_DIRECTORY/ExampleFiles/";
        String targetDirectory = "YOUR_DOCUMENT_DIRECTORY/DocumentIndexingAndRenaming/Documents/";

        try (Stream<Path> paths = Files.walk(Paths.get(sourceDirectory))) {
            paths.filter(Files::isRegularFile)
                 .forEach(sourcePath -> {
                     Path destPath = Paths.get(targetDirectory + sourcePath.getFileName().toString());
                     try {
                         Files.copy(sourcePath, destPath, java.nio.file.StandardCopyOption.REPLACE_EXISTING);
                     } catch (IOException e) {
                         e.printStackTrace();
                     }
                 });
        }
    }
}
```

*Magyarázat:*  
- Az áram csak a szabályos fájlokat szűri, majd mindegyiket a célkönyvtárba másolja, szükség esetén felülírva a meglévő fájlokat.

## Megvalósítási útmutató

### 1. dokumentumok hozzáadása az indexhez (kereshető index létrehozása)
Adja hozzá a forrásmappát az indexhez, hogy minden dokumentum azonnal kereshető legyen.

```java
import com.groupdocs.search.Index;

public class DocumentIndexingAndRenaming {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/DocumentIndexingAndRenaming/Index";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentIndexingAndRenaming/Documents/";

        // Create an Index
        Index index = new Index(indexFolder);

        // Add documents to the index
        index.add(documentFolder);
    }
}
```

*Magyarázat:*  
- `indexFolder` – ahol az indexfájlok tárolódnak.  
- `documentFolder` – a forrásmappa, amely a kereshetővé tenni kívánt fájlokat tartalmazza.

## Gyakorlati alkalmazások
- **Vállalati dokumentumkezelés** – Indexelés automatizálása több ezer szerződéshez, és a fájlnevek szinkronban tartása.  
- **Jogász irodák** – Gyorsan átnevezheti az ügyiratokat, miközben megőrzi a kereshető tartalmat.  
- **Tartalomkezelő rendszerek** – Használja a könyvtár tisztítása mintát a média mappák frissítéséhez kézi takarítás nélkül.  

## Teljesítménybeli megfontolások
- **Index mérete** – Időnként tömörítse az indexet, ha nagyra nő; a GroupDocs.Search egy `compact()` metódust biztosít, amely akár 30 % -kal is csökkentheti a tárhelyet.  
- **Memóriahasználat** – Fájlokat 500 – 1 000 darabos kötegekben dolgozzon fel, hogy elkerülje az `OutOfMemoryError`-t.  
- **Párhuzamosság** – Tömeges műveletekhez fontolja meg a Java `ExecutorService` használatát a tisztítás, másolás és indexelés párhuzamosításához, ami akár 40 % -kal is csökkentheti a teljes futási időt többmagos szervereken.  

## Gyakori problémák és tippek

| Probléma | Ok | Megoldás |
|----------|----|----------|
| Átnevezés sikertelen | A fájl zárolva van vagy az útvonal érvénytelen | Győződjön meg róla, hogy a fájl nincs megnyitva máshol; használja a `Files.move`-t a megbízhatóbb átnevezéshez. |
| Az index nem frissül | Az értesítés nem lett elküldve | Mindig hívja meg a `index.notifyIndex(notification)`-t, majd az `index.update()`-t. |
| Elavult keresési eredmények másolás után | Az index még mindig a régi fájlokra mutat | Adja hozzá újra a célmappát az indexhez, vagy hívja meg a `index.update()`-t másolás után. |
| Lassú tisztítás nagy mappák esetén | Egy szálas bejárás | Használjon párhuzamos streameket vagy ossza fel a mappát kisebb kötegekre. |
| Jogosultsági hibák | Nem elegendő operációs rendszer jogosultság | Futtassa a JVM-et megfelelő jogosultságokkal, vagy állítsa be a mappa ACL-eket. |

## Gyakran ismételt kérdések

**Q: Tisztíthatok-e olyan könyvtárat, amely alkönyvtárakat tartalmaz?**  
A: Igen. A `Files.walk()` megközelítés rekurzívan törli az összes beágyazott fájlt és mappát.

**Q: Újra kell építenem az egész indexet minden átnevezés után?**  
A: Nem. Egy átnevezési értesítés küldése és az `index.update()` meghívása elegendő.

**Q: Mekkora mappát tisztíthatok, mielőtt a teljesítménykorlátokba ütköznék?**  
A: Ez a JVM memória függvénye; kisebb kötegekben történő feldolgozás vagy streamek használata segít a nagy adathalmazok kezelésében.

**Q: A GroupDocs.Search ingyenes fejlesztéshez?**  
A: Elérhető egy ingyenes próba, de a termelési használathoz fizetett licenc szükséges.

**Q: Alkalmazhatom ezt a megközelítést más fájltípusokkal (pl. PDF, DOCX)?**  
A: Természetesen. A GroupDocs.Search sok formátumot támogat; egyszerűen adja hozzá a megfelelő fájlokat tartalmazó mappát az indexhez.

**Utolsó frissítés:** 2026-08-05  
**Tesztelt verzió:** GroupDocs.Search 25.4  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [Hogyan hozzunk létre index könyvtárat Java-val a GroupDocs.Search segítségével](/search/java/indexing/groupdocs-search-java-create-index/)
- [Keresőindex könyvtár létrehozása és licenc beállítása – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Kereshető index létrehozása Java – A GroupDocs.Search for Java telepítése](/search/java/getting-started/deploy-groupdocs-search-java-setup-guide/)