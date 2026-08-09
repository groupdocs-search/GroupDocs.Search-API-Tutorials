---
date: '2026-06-12'
description: Ismerje meg, hogyan hozhat létre keresési indexet .NET-ben, és alkalmazhat
  redakciót PDF-re a GroupDocs.Search és GroupDocs.Redaction használatával. A beállítás,
  telepítés, indexelés és a fejlett keresés részletezve.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: Keresési index létrehozása .NET-ben a GroupDocs Search és Redaction segítségével
  – Átfogó útmutató
type: docs
url: /hu/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Keresési index létrehozása .NET-ben a GroupDocs Search és Redaction segítségével – Átfogó útmutató

A mai digitális környezetben a **search index .NET** létrehozása olyan megoldás, amely gyorsan megtalálja az információkat és védi az érzékeny adatokat, minden szervezet számára kiemelt prioritás. Ez az útmutató végigvezet a skálázható GroupDocs.Search hálózat konfigurálásán, a csomópontok telepítésén, a dokumentumok indexelésén, valamint a GroupDocs.Redaction használatán a **PDF-re történő redakció alkalmazásához** – mindezt .NET környezetben.

## Gyors válaszok
- **Mi az első lépés a search index .NET létrehozásához?** Határozz meg egy alapútvonalat és portot, majd telepítsd a hálózati csomópontokat.  
- **Hogyan alkalmazhatok redakciót PDF-re a GroupDocs-szal?** Hozz létre egy `Redactor` példányt, töltsd be a PDF-et, és hívd meg a `Redact` metódust a kívánt mintákkal.  
- **Futtathatom a keresési hálózatot több gépen?** Igen—telepíts csomópontokat különálló szervereken, és hagyd, hogy a master csomópont koordinálja az indexelést és a lekérdezéseket.  
- **Szükségem van licencre a termelési használathoz?** Érvényes GroupDocs licenc szükséges a termeléshez; ideiglenes próba licenc elérhető értékeléshez.  
- **Mely .NET verziók támogatottak?** .NET Framework 4.7.2+, .NET Core 3.1+, valamint a .NET 5/6/7 teljes mértékben támogatott.

## Mi a “search index .NET” létrehozása?
*A search index .NET* létrehozása egy kereshető adattár felépítését jelenti dokumentum metaadatok és tartalom tárolására .NET könyvtárak segítségével, amelyek kinyerik a szöveget, tokenizálják a kifejezéseket, és egy optimalizált index struktúrában tárolják őket. Ez lehetővé teszi a pillanatos lekérdezési válaszokat elosztott csomópontok között, támogatja a különböző fájlformátumokat, és skálázható, nagy teljesítményű dokumentumlekérdezést biztosít vállalati alkalmazásokban.

## Miért használjuk együtt a GroupDocs Search és Redaction szolgáltatásokat?
A GroupDocs.Search **50+ fájlformátumot** támogat — beleértve a DOCX, PDF, PPTX és HTML formátumokat — és több száz oldalas dokumentumokat tud indexelni anélkül, hogy az egész fájlt a memóriába töltené. A GroupDocs.Redaction-nal kombinálva, amely **PDF-re történő redakciót** képes alkalmazni 200 ms alatti idő alatt oldalanként, egy biztonságos, nagy teljesítményű dokumentumkezelő csővezetéket kapsz.

## Előfeltételek

### Szükséges könyvtárak és függőségek
Ahhoz, hogy kövesd ezt az útmutatót, telepítsd a következő csomagokat:
- **GroupDocs.Search** .NET-hez
- **GroupDocs.Redaction** .NET-hez  

A szükséges könyvtárak telepítéséhez bármelyik módszert használhatod:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Keress rá a "GroupDocs.Search" és "GroupDocs.Redaction" kifejezésekre, majd telepítsd a legújabb verziót.

### Környezet beállítási követelmények
- .NET Framework 4.7.2 vagy újabb (vagy .NET Core 3.1+)
- Visual Studio IDE (Community, Professional vagy Enterprise)

### Tudás előfeltételek
- Alap C# programozás
- Objektum‑orientált koncepciók
- Hálózati konfigurációk és dokumentumkezelő rendszerek ismerete

## GroupDocs.Redaction beállítása .NET-hez

### Telepítési információk
A redakciós funkciók integrálásához az alkalmazásodba, kezd a GroupDocs.Redaction könyvtár hozzáadásával:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Keress rá a "GroupDocs.Redaction" kifejezésre, és telepítsd.

### Licenc beszerzése
A ingyenes próba vagy ideiglenes licenc elindításához kövesd az alábbi lépéseket:
- Látogasd meg a [GroupDocs weboldalát](https://purchase.groupdocs.com/temporary-license/) a temporális licenc igényléséhez.  
- Vásárlási lehetőségekhez navigálj a [árak oldalára](https://groupdocs.com/pricing).

Miután megkaptad a licencfájlt, alkalmazd azt az alkalmazás beállításában:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Alap inicializálás
A GroupDocs.Redaction alapvető műveletekhez történő inicializálásához használd a következő kódrészletet:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Megvalósítási útmutató

### Konfiguráció beállítása

#### Áttekintés
Ez a funkció a keresési hálózatot egy alapútvonal és portszám használatával konfigurálja, amely a dokumentumkezelő rendszer alapját képezi.

#### Definíciós horgony
A `SearchNetworkDeployment` osztály irányítja a keresési csomópontok hálózaton belüli telepítését.

#### 1. lépés: Alapútvonal és port meghatározása  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### 2. lépés: Hálózat konfigurálása  
Használd a `Configure` metódust a keresési hálózat beállításához a megadott útvonal és port alapján:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Hálózati csomópont telepítése

#### Áttekintés
Telepíts csomópontokat a konfigurált keresési hálózatodban a dokumentumok elosztott kereséséhez.

#### Definíciós horgony
A `SearchNetworkNode` egy egyedi kereshető csomópontot képvisel, amely kommunikál a master csomóponttal.

#### 1. lépés: Telepítés inicializálása  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Esemény feliratkozás a master csomópontra

#### Áttekintés
Iratkozz fel a master csomópont eseményeire a hálózati műveletek hatékony felügyelete és kezelése érdekében.

#### Definíciós horgony
A `SearchNetworkNodeEvents` visszahívásokat biztosít az indexeléshez, lekérdezés végrehajtásához és hibakezeléshez.

#### 1. lépés: A master csomópont azonosítása  
Válaszd ki az első csomópontot masterként:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### 2. lépés: Feliratkozás az eseményekre  
Iratkozz fel az eseményekre a következő módon:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Dokumentumok indexelése

#### Áttekintés
Dokumentumok indexelése a hatékony keresési műveletekhez. Ez a lépés kulcsfontosságú annak biztosításához, hogy a hálózat gyorsan visszanyerje a szükséges adatokat.

#### Definíciós horgony
A `SearchIndex` a központi objektum, amely a kereshető tokeneket és metaadatokat tárolja minden indexelt fájlhoz.

#### 1. lépés: Könyvtárak hozzáadása az indexhez  
Add meg a dokumentumokat tartalmazó könyvtárakat:

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Keresési funkció – Alap használat

#### Áttekintés
Alap keresési műveletek végrehajtása a hálózat csomópontjai között.

#### Közvetlen válasz
Hívd meg a `SearchNetwork.Query("your term")` metódust a master csomóponton, hogy azonnal visszakapd a megfelelő dokumentumokat. A metódus egy `SearchResult` objektumok gyűjteményét adja vissza, amelyek fájlútvonalakat és relevancia pontszámokat tartalmaznak.  
A `SearchNetwork.Query` egy metódus, amely keresési lekérdezést hajt végre a teljes hálózaton, és visszaadja a találatokat.

#### 1. lépés: Keresési paraméterek meghatározása  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Haladó keresési funkció

#### Áttekintés
Használj haladó keresési technikákat testreszabható paraméterekkel a pontosabb eredményekért.

#### Közvetlen válasz
Valósíts meg egy metódust, amely létrehoz egy `SearchOptions` objektumot, beállítja a `UseFuzzySearch`, `Highlight` és `PageSize` tulajdonságokat, majd átadja azt a `SearchNetwork.QueryAdvanced` metódusnak. Ez lapozható, kiemelt eredményeket ad vissza, fuzzy egyezéssel.  
A `SearchNetwork.QueryAdvanced` egy metódus, amely lekérdezést futtat haladó opciókkal, mint a fuzzy egyezés és a lapozás.

#### 1. lépés: A haladó keresési metódus megvalósítása  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### Redakció alkalmazása PDF fájlokra

#### Áttekintés
Az érzékeny információk védelme PDF tartalom redakcióval, mielőtt tárolnák vagy megosztanák.

#### Közvetlen válasz
Hozz létre egy `Redactor` példányt, töltsd be a cél PDF-et, definiálj egy `RedactionPattern`-t (pl. SSN regex), hívd meg a `redactor.Apply(pattern)` metódust, majd mentsd el a redakciózott dokumentumot. Ez a folyamat biztosítja, hogy a személyes adatok véglegesen eltávolításra kerülnek.

#### Definíciós horgony
A `Redactor` a GroupDocs.Redaction fő osztálya, amely a dokumentumokat feldolgozza és redakciós szabályokat alkalmaz.

#### Példa munkafolyamat (új kódrészlet nélkül)  
1. Inicializáld a `Redactor`-t a licenceddel.  
2. Töltsd be a PDF-et a `redactor.Load("sample.pdf")` használatával.  
3. A `RedactionPattern` egy szabályt képvisel, amely meghatározza a redakcióra szánt szöveget vagy mintát. Definiálj mintákat, például `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. Hajtsd végre a `redactor.Apply(pattern)`-t.  
5. Mentsd el a kimenetet a `redactor.Save("sample_redacted.pdf")`-val.

### Gyakorlati alkalmazások

#### Valós világban alkalmazások  
1. **Jogi dokumentumkezelés** – Hatékonyan keresd a szerződéseket és automatikusan redakciózd a kliens azonosítókat.  
2. **Egészségügyi nyilvántartások** – Találd meg a betegjegyzeteket, miközben biztosítod a HIPAA‑kompatibilis PHI redakciót.  
3. **Vállalati megfelelőség** – Szkenneld a belső kommunikációkat tiltott kifejezések után, és redakciózd őket archiválás előtt.

## Következtetés
Ez az útmutató átfogó útvonalat nyújt a **search index .NET** megoldás létrehozásához, amely skálázható, gyorsan indexel, és redakcióval védi az adatokat. A csomópontok konfigurálásával, a dokumentumok indexelésével, a haladó keresési funkciók kihasználásával és a redakció alkalmazásával a fejlesztők jelentősen javíthatják a dokumentumkezelési munkafolyamatokat, miközben szigorú biztonsági előírásokat tartanak be.

## Gyakran Ismételt Kérdések

**Q: Hogyan állíthatok be elosztott keresési hálózatot .NET-ben a GroupDocs-szal?**  
A: Határozd meg az alapútvonalat és a portot, majd hívd meg a `SearchNetworkDeployment.Deploy()` metódust a master és worker csomópontok indításához a gépek között.

**Q: Végezhetek haladó kereséseket több paraméterrel a GroupDocs-ban?**  
A: Igen—használd a `SearchOptions`-t a fuzzy egyezés, helyettesítő karakter támogatás és az eredmények kiemelésének kombinálásához egyetlen lekérdezésben.

**Q: Lehetséges a hálózati aktivitás monitorozása a master csomóponton?**  
A: Teljesen—iratkozz fel a `SearchNetworkNodeEvents` eseményekre, mint például az `IndexingCompleted` és `QueryExecuted`, a valós idejű betekintéshez.

**Q: Hogyan alkalmazok redakciót PDF fájlokra a GroupDocs használatával?**  
A: Inicializáld a `Redactor`-t, töltsd be a PDF-et, definiálj `RedactionPattern` objektumokat (regex vagy szó szerinti karakterláncok), hívd meg az `Apply` metódust, és mentsd el a tisztított dokumentumot.

**Q: Mi a legegyszerűbb módja a keresési teljesítmény javításának hálózati környezetben?**  
A: Teljesen indexeld a dokumentumkészletedet a lekérdezések előtt, oszd el a csomópontokat a párhuzamos feldolgozás kihasználásához, és állítsd be a `SearchOptions`-t a gyorsítótárazás és lapozás optimalizálásához.

---

**Utolsó frissítés:** 2026-06-12  
**Tesztelve:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [Mester .NET dokumentum indexelés a GroupDocs.Search segítségével: Átfogó útmutató](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Mester dokumentum indexelés és haladó keresési lekérdezések a GroupDocs.Redaction .NET segítségével](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [A GroupDocs Search és Redaction .NET-ben elsajátítása: Haladó dokumentumkezelés](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)