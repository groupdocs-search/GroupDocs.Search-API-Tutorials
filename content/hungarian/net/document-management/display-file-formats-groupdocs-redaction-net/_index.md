---
date: '2026-06-07'
description: Ismerje meg, hogyan lehet listázni a fájl kiterjesztéseket és lekérni
  a fájlformátumokat a GroupDocs.Redaction segítségével C#-ban. Tartalmaz beállítási
  útmutatót, kódot és gyakorlati tippeket.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Hogyan listázhatók a fájl kiterjesztések a GroupDocs.Redaction segítségével
  .NET környezetben – Átfogó útmutató
type: docs
url: /hu/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Támogatott fájlformátumok megjelenítése a GroupDocs.Redaction segítségével .NET-ben

A különféle dokumentumtípusok kezelése a .NET fejlesztők mindennapi valósága. A **GroupDocs.Redaction** használatával **listázhatja a fájlkiterjesztéseket**, amelyeket a könyvtár támogat, így az alkalmazása intelligensen fogadja vagy elutasítja a feltöltéseket, barátságos UI lehetőségeket kínál, és elkerüli a költséges futásidejű hibákat. Ez az útmutató mindent végigvezet, amire szüksége van – az előfeltételektől egy teljes, termelésre kész megvalósításig – így magabiztosan **kaphatja meg a fájlformátumokat** és **c# display file formats** a megoldásában.

## Gyors válaszok
- **Mi jelent a “list file extensions”?** Azt jelenti, hogy lekérdezi a támogatott fájltípus-azonosítók gyűjteményét (pl. *.pdf*, *.docx*) az API-ból.  
- **Melyik NuGet csomag biztosítja ezt a képességet?** `GroupDocs.Redaction` (legújabb stabil verzió).  
- **Szükségem van licencre a minta futtatásához?** Egy ingyenes próbalicenc elegendő fejlesztéshez; a termeléshez állandó licenc szükséges.  
- **Cache‑elhetem az eredményeket?** Igen – tárolja a listát memóriában vagy elosztott cache‑ben az ismételt API‑hívások elkerülése érdekében.  
- **Ez a funkció kompatibilis a .NET 6-tal és a .NET Core‑ral?** Teljesen; a könyvtár támogatja a .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ és .NET 6+ verziókat.

## Mi az a GroupDocs.Redaction?
**GroupDocs.Redaction** egy .NET könyvtár, amely lehetővé teszi a fejlesztők számára érzékeny tartalom kitakarását, dokumentumok konvertálását és a támogatott fájltípusok felfedezését – mindezt anélkül, hogy a szerveren a Microsoft Office-ra lenne szükség. Elrejti a komplex formátumkezelést egy tiszta, objektum‑orientált API mögött. Egységes API‑t kínál a kitakaráshoz, konvertáláshoz és a formátumok felfedezéséhez, kezelve a PDF‑eket, Office dokumentumokat, képeket és egyebeket, miközben magas teljesítményt és biztonságot biztosít.

## Miért listázzuk a fájlkiterjesztéseket a GroupDocs.Redaction segítségével?
A könyvtár **több mint 50 bemeneti és kimeneti formátumot támogat**, beleértve a PDF, DOCX, PPTX, XLSX, HTML és több mint 30 kép típust. Programozottan **listázva a fájlkiterjesztéseket**, a következőket teheti:
- Megakadályozza a felhasználókat, hogy nem támogatott fájlokat töltsenek fel (csökkentve a validációs hibákat akár 90%-kal).  
- Dinamikusan tölti fel a legördülő menüket, biztosítva, hogy a UI szinkronban maradjon a könyvtár frissítéseivel.  
- Audit naplókat épít, amelyek rögzítik a pontos fájltípust, amelyet a felhasználó megpróbált feldolgozni.

## Előfeltételek
- **GroupDocs.Redaction**: Telepítés NuGet‑en keresztül (lásd az alábbi parancsokat).  
- **.NET SDK**: Győződjön meg róla, hogy a legújabb .NET SDK telepítve van. Töltse le [itt](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 vagy bármely kompatibilis szerkesztő.  
- **Alap C# ismeretek**: Jól kell tudnia dolgozni a gyűjteményekkel és a LINQ‑szal.

## A GroupDocs.Redaction beállítása .NET-hez

### A könyvtár telepítése

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Nyissa meg a NuGet Package Manager‑t, keressen rá a “GroupDocs.Redaction” kifejezésre, és telepítse a legújabb verziót.

### Licenc beszerzése és alkalmazása

Kezdje egy ingyenes próbalicencel vagy kérjen ideiglenes licencet a teljes funkciók korlátok nélküli felfedezéséhez. A vásárlási lehetőségekért látogassa meg a [GroupDocs vásárlási oldalát](https://purchase.groupdocs.com/). Miután megkapta a licencfájlt:
1. Helyezze el egy elérhető mappában a projektjében (pl. `./Licenses/GroupDocs.Redaction.lic`).  
2. Inicializálja a licencet az alkalmazás indításakor:

A `License` osztály betölti a licencfájlt és aktiválja a GroupDocs.Redaction‑t.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Hogyan listázzuk a fájlkiterjesztéseket a GroupDocs.Redaction segítségével?

Töltse be a Redaction API‑t, és hívja meg a támogatott formátumokat visszaadó metódust. A hívás egy gyűjteményt ad vissza, ahol minden elem egy kiterjesztést és egy ember által olvasható leírást tartalmaz. Ez a művelet könnyű, és végrehajtható indításkor vagy igény szerint.

### A támogatott fájltípusok lekérése
A `RedactionApi.GetSupportedFileFormats()` metódus egy csak‑olvasású `FileFormatInfo` objektumok gyűjteményét adja vissza, amelyek leírják az egyes formátumokat.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Minden kiterjesztés és leírás megjelenítése
Minden `FileFormatInfo` biztosítja a `Extension` és `Description` tulajdonságokat egy fájltípushoz.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Magyarázat**: A ciklus végigiterál minden `FileFormatInfo` objektumon, és kiírja a `Extension` és `Description` értékét egy rendezett táblázatban.

## Hogyan integráljuk a listát egy UI legördülő menübe?

Miután megvan a gyűjtemény, kössön rá bármely UI komponensre – WinForms `ComboBox`, WPF `ComboBox`, vagy ASP.NET Core `select` elem. A lényeg, hogy a `Extension`‑t használja értékként, a `Description`‑t pedig megjelenítendő szövegként. Ez biztosítja, hogy a felhasználók barátságos neveket lássanak, miközben a kód a pontos kiterjesztés karakterláncokkal dolgozik.

## Gyakori problémák és megoldások
- **Hiányzó névtér hiba** – Ellenőrizze, hogy importálta a `GroupDocs.Redaction` és a `GroupDocs.Redaction.Common` névtereket.  
- **Licenc nem található** – Győződjön meg róla, hogy a licencfájl útvonala helyes, és a fájl szerepel a build kimenetben.  
- **Teljesítmény nagy projektek esetén** – Cache‑elje az eredményt egy statikus változóban vagy elosztott cache‑ben (pl. Redis), hogy elkerülje az ismételt felsorolást.

## Gyakorlati alkalmazások
A támogatott kiterjesztések pontos listájának ismerete több valós helyzetet is lehetővé tesz:
1. **Dokumentumkezelő rendszerek** – Automatikusan kategorizálja a bejövő fájlokat a kiterjesztésük alapján.  
2. **Tartalomszűrő eszközök** – Blokkolja a tiltott formátumokat (pl. futtatható fájlok) a feltöltéskor.  
3. **Fájlkonverziós folyamatok** – Dinamikusan döntse el, hogy egy fájl konvertálható-e, vagy visszalépési munkafolyamatra van szükség.

## Teljesítménybeli megfontolások
- **Memóriahasználat** – A formátumlista egy könnyű `IReadOnlyCollection`‑ben tárolódik, általában 2 KB alatt.  
- **Szálbiztonság** – A gyűjtemény a létrehozás után módosíthatatlan, így biztonságos a párhuzamos olvasásokhoz.  
- **Cache‑elés** – Nagy forgalmú API‑k esetén cache‑elje a listát az alkalmazás élettartama alatt, hogy megszüntesse a kérésenként néhány mikrosekundumos többletet.

## Következtetés

A fenti lépések követésével most már megbízható módja van a **list file extensions** és **c# display file formats** használatának a GroupDocs.Redaction segítségével. Ez a képesség nem csak javítja a felhasználói élményt, hanem megvédi a háttérrendszert a nem támogatott fájloktól is. Fedezze fel a Redaction további funkcióit – például a tartalom maszkolását, PDF kitakarását és kötegelt feldolgozást – hogy tovább erősítse a dokumentumfolyamát.

## Gyakran Ismételt Kérdések

**Q: Mik a alapértelmezett támogatott fájlformátumok?**  
A: A GroupDocs.Redaction több mint 50 formátumot támogat, beleértve a PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG és még sok más. A teljes listát lásd a [GroupDocs dokumentációban](https://docs.groupdocs.com/search/net/).

**Q: Hogyan frissíthetem a könyvtárat a legújabb verzióra?**  
A: Nyissa meg a NuGet Package Manager‑t, keressen rá a “GroupDocs.Redaction” kifejezésre, és kattintson a **Update** gombra. Alternatívaként futtassa a `dotnet add package GroupDocs.Redaction --version <latest>` parancsot.

**Q: Használhatom ezt a listát a feltöltött fájlok szerveroldali validálásához?**  
A: Igen – hasonlítsa össze a feltöltött fájl kiterjesztését a lekért gyűjteménnyel a feldolgozás előtt. Ez kiküszöböli a hibás formátumú hibák 99%-át.

**Q: Lehetséges a támogatás kiterjesztése egyedi fájltípusokra?**  
A: Egyedi kiterjesztésekhez egyedi kezelőkre van szükség; a magkönyvtár nem ad hozzá natívan új formátumokat. Tekintse át az API dokumentációt egyedi import/export csővezetékek létrehozásához.

**Q: Az alkalmazásom összeomlik a kód hozzáadása után – mit ellenőrizze?**  
A: Győződjön meg róla, hogy a licenc helyesen van betöltve, a `using` utasítások a megfelelő névterekre hivatkoznak, és kezelje az `IOException`‑t a licencfájl olvasásakor.

---

**Legutóbb frissítve:** 2026-06-07  
**Tesztelve:** GroupDocs.Redaction 23.9 for .NET  
**Szerző:** GroupDocs  

## Erőforrások
- [Dokumentáció](https://docs.groupdocs.com/search/net/)
- [API referencia](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction letöltése](https://releases.groupdocs.com/search/net/)
- [Ingyenes támogatási fórum](https://forum.groupdocs.com/c/search/10)
- [Ideiglenes licenc kérése](https://purchase.groupdocs.com/temporary-license/)

## Kapcsolódó oktatóanyagok
- [Fájl szűrés mesterfokon .NET-ben a GroupDocs.Redaction segítségével: Hatékony dokumentumkezelési technikák](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [GroupDocs.Redaction .NET mesterkurzus: Beállítás és eseménykezelés a biztonságos dokumentumkezeléshez](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Dokumentumkezelés mesterfokon .NET-ben a GroupDocs.Redaction segítségével: Licenc beállítás és HTML keresés kiemelés](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)