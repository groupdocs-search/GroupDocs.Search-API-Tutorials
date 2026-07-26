---
date: '2026-07-26'
description: Naučte se, jak vytvořit index v .NET pomocí GroupDocs.Search a integrovat
  redakci s GroupDocs.Redaction, což umožňuje rychlé vyhledávání dokumentů a zpracování
  dat.
keywords:
- how to create index
- how to add documents
- how to delete document
- search index .net
lastmod: '2026-07-26'
og_description: Naučte se, jak vytvořit index v .NET pomocí GroupDocs.Search a integrovat
  redakci s GroupDocs.Redaction, což umožňuje rychlé vyhledávání dokumentů a zpracování
  dat.
og_image_alt: Guide showing GroupDocs Search index creation and Redaction integration
  in .NET
og_title: Jak vytvořit index v .NET pomocí GroupDocs Search API
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  headline: How to Create Index in .NET with GroupDocs Search API
  type: TechArticle
- description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  name: How to Create Index in .NET with GroupDocs Search API
  steps:
  - name: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
    text: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
  - name: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
    text: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
  - name: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
    text: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
  - name: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
    text: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
  - name: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
    text: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search can index over 150 formats—including PDFs, DOCX,
      PPTX, XLSX, and image types—by extracting embedded text via OCR where necessary.
    question: Can I index non‑text files with GroupDocs?
  - answer: Use `AddFolder` with a configurable batch size, run indexing in a background
      service, and periodically call `Optimize()` to merge small index segments.
    question: How do I handle large volumes of documents?
  - answer: Redaction removes personally identifiable information before it ever reaches
      the index, guaranteeing that search results never expose protected data.
    question: What are the benefits of using redaction with indexing?
  - answer: GroupDocs.Search provides synonym dictionaries, custom tokenizers, and
      regular‑expression filters, allowing you to fine‑tune relevance scoring.
    question: Is it possible to customize search algorithms?
  - answer: Verify folder permissions, ensure the .NET runtime matches the library’s
      target, and check the log file generated in the index folder for detailed error
      messages.
    question: How do I troubleshoot common indexing issues?
  type: FAQPage
tags:
- index management
- GroupDocs.Search
- GroupDocs.Redaction
- C# document indexing
- document redaction .NET
title: Jak vytvořit index v .NET pomocí GroupDocs Search API
type: docs
url: /cs/net/document-management/master-net-index-management-groupdocs-search-redaction/
weight: 1
---

# Jak vytvořit index v .NET s GroupDocs Search API

V tomto tutoriálu se dozvíte **jak vytvořit index** pro vaše .NET aplikace pomocí GroupDocs.Search a poté chránit citlivý obsah pomocí GroupDocs.Redaction. Na konci průvodce budete schopni vytvořit, aktualizovat a ořezat prohledávatelný index a pochopíte, proč je kombinace vyhledávání a redakce nejlepší praxí pro zabezpečenou správu dokumentů.

## Rychlé odpovědi
- **Co znamená „jak vytvořit index“?** Znamená to vytvoření prohledávatelné datové struktury, která mapuje obsah dokumentu na rychlé vyhledávací klíče.  
- **Které knihovny jsou vyžadovány?** GroupDocs.Search a GroupDocs.Redaction pro .NET (balíčky NuGet).  
- **Mohu indexovat PDF, Word a obrázky?** Ano — podporováno je více než 150 formátů přímo z krabice.  
- **Jak smažu dokument z indexu?** Zavolejte metodu `Delete` s cestou nebo ID dokumentu.  
- **Provádí se redakce před nebo po indexování?** Redakce by měla proběhnout jako první, aby chráněná data nikdy nešla do indexu.

## Co je „jak vytvořit index“?
Fráze **jak vytvořit index** odkazuje na proces generování prohledávatelné datové struktury, která ukládá mapování termín‑dokument pro rychlé získání. V GroupDocs tato struktura žije na disku a může být inkrementálně aktualizována bez nutnosti přestavovat celou kolekci.

## Proč používat GroupDocs.Search a GroupDocs.Redaction společně?
GroupDocs.Search podporuje indexování **více než 150 formátů souborů** a dokáže zpracovat indexy větší než **10 GB**, přičemž udržuje využití paměti pod 200 MB, protože soubory streamuje místo jejich úplného načtení. Přidání GroupDocs.Redaction zajišťuje, že jakýkoli důvěrný text, obrázky nebo metadata jsou odstraněny dříve, než obsah vůbec dorazí do indexu, což garantuje soulad s GDPR, HIPAA a dalšími předpisy.

## Předpoklady
- **Knihovny a verze** – Nainstalujte nejnovější balíčky NuGet **GroupDocs.Search** a **GroupDocs.Redaction**, které jsou kompatibilní s .NET 6 nebo novějším.  
- **IDE** – Visual Studio 2022 (nebo jakékoli IDE podporující .NET 6).  
- **Znalosti** – Základní dovednosti v C#, znalost práce se soubory (I/O) a pochopení konceptů indexování.

## Nastavení GroupDocs.Redaction pro .NET

### Instalace

**Using .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Using Package Manager Console in Visual Studio:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Můžete také najít „GroupDocs.Redaction“ v uživatelském rozhraní NuGet Package Manager a nainstalovat nejnovější stabilní verzi.

### Získání licence

Můžete získat bezplatnou zkušební verzi nebo požádat o dočasnou licenci, abyste mohli prozkoumat všechny funkce bez omezení. Navštivte [GroupDocs' Purchase Page](https://purchase.groupdocs.com/temporary-license/) pro více informací o získání licence.

### Základní inicializace

Redactor je hlavní třída, která provádí operace redakce na dokumentu.  
Následující úryvek ukazuje minimální kód potřebný k zahájení používání GroupDocs.Redaction:  
```csharp
// Initialize the Redactor with a file path or stream
using (Redactor redactor = new Redactor("input.docx"))
{
    // Your redaction code here
}
```  

Toto jednoduché nastavení je vše, co potřebujete k zahájení používání GroupDocs.Redaction.

## Průvodce implementací

### Jak vytvořit index?
`Index` představuje prohledávatelný kontejner, který obsahuje slovníky termínů a metadata dokumentů.  
Načtěte nebo vytvořte objekt `Index`, nasměrujte jej do složky, kde budou uloženy soubory indexu, a zavolejte `Create`. Operace zapíše potřebné soubory metadat a připraví engine pro ingestování dokumentů.  
```text
// Direct answer (40‑70 words):
Create a new `Index` instance by specifying the folder path where the index will reside, then invoke `Create()` to initialise the storage structures. The method writes index headers, term dictionaries, and a lock file, making the folder ready for document addition. This step is required only once per index location.
```

#### Krok 1: Vytvořit index
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/DeleteIndexedPaths";
Index index = new Index(indexFolder);
// This line initializes an index at the provided folder path.
```  

### Jak přidat dokumenty do indexu?
`Add` vloží jeden dokument do indexu, zatímco `AddFolder` zpracuje všechny soubory v adresáři.  
Soubory přidáte voláním `Add` nebo `AddFolder`. Engine načte každý podporovaný soubor, extrahuje text a aktualizuje slovník termínů.  
```text
// Direct answer (40‑70 words):
Use `index.AddFolder("C:\\Docs")` or `index.Add("C:\\Docs\\file.pdf")` to feed documents into the index. The API streams each file, extracts searchable text, and stores term‑frequency data without loading the entire file into memory, which lets you index thousands of large PDFs efficiently.
```

#### Krok 2: Přidat složky dokumentů
```csharp
string documentsFolder1 = @"YOUR_DOCUMENT_DIRECTORY";
string documentsFolder2 = @"YOUR_DOCUMENT_DIRECTORY2";

index.Add(documentsFolder1);  // Adding the first folder of documents to the index
index.Add(documentsFolder2);  // Adding the second folder of documents to the index
```  

### Jak získat indexované cesty?
`GetIndexedPaths` vrací kolekci všech cest dokumentů uložených v indexu.  
Získání seznamu indexovaných cest souborů vám umožní ověřit, které dokumenty jsou momentálně prohledávatelné.  
```text
// Direct answer (40‑70 words):
Call `index.GetIndexedDocuments()` to obtain a collection of `IndexedDocumentInfo` objects, each containing the original file path, document ID, and indexing timestamp. Loop through the collection and output the `FilePath` property to confirm that every expected file has been successfully added.
```

#### Krok 3: Zobrazit indexované cesty
```csharp
string[] indexedPaths1 = index.GetIndexedPaths();
foreach (string path in indexedPaths1)
{
    Console.WriteLine(path); // Outputs the document paths
}
```  

### Jak smazat dokument z indexu?
`Delete` odstraní dokument z indexu podle jeho cesty nebo identifikátoru.  
Když je soubor odstraněn nebo se stane zastaralým, měli byste smazat jeho záznam, aby výsledky vyhledávání zůstaly přesné.  
```text
// Direct answer (40‑70 words):
Invoke `index.Delete("C:\\Docs\\obsolete.pdf")` or `index.Delete(documentId)` to purge a specific document from the index. The method removes all term entries linked to that file, updates the term dictionary, and frees the space on disk, ensuring that future queries no longer return the deleted content.
```

#### Krok 4: Smazat konkrétní cesty
```csharp
using GroupDocs.Search.Options;

string[] pathsToDelete = { @"YOUR_DOCUMENT_DIRECTORY" };
DeleteResult deleteResult = index.Delete(pathsToDelete, new UpdateOptions());
// This deletes specified document paths from the index.
```  

### Jak ověřit zbývající indexované cesty po smazání?
Po odstranění můžete znovu spustit metodu pro získání, abyste se ujistili, že index odráží aktuální stav.  
```text
// Direct answer (40‑70 words):
Run `index.GetIndexedDocuments()` again and compare the resulting list with the pre‑deletion list. The missing file path confirms successful deletion, while the remaining entries confirm the index’s integrity. This verification step is especially important in automated pipelines.
```

#### Krok 5: Ověřit zbývající cesty
```csharp
string[] indexedPaths2 = index.GetIndexedPaths();
foreach (string path in indexedPaths2)
{
    Console.WriteLine(path); // Displays remaining paths after deletion
}
```  

## Praktické aplikace

1. **Systémy správy dokumentů** – Rychle najděte smlouvy, faktury nebo manuály mezi miliony souborů.  
2. **Právní revize dokumentů** – Redigujte privilegované informace před indexováním, aby nedošlo k náhodnému odhalení.  
3. **Archivní řešení** – Uchovávejte prohledávatelná metadata historických záznamů bez načítání celých archivů do paměti.  
4. **Platformy pro správu obsahu** – Zajišťují vyhledávání napříč celým webem pro blogy, znalostní báze a multimediální knihovny.  
5. **Audity souladu s předpisy** – Zajišťují, že pouze očištěný obsah je prohledávatelný, splňující regulační požadavky.

## Úvahy o výkonu

- **Optimalizace indexování** – Plánujte inkrementální indexování každou noc; použijte `AddFolder` s velikostí dávky 100 souborů pro snížení špiček I/O.  
- **Správa zdrojů** – Sledujte CPU a RAM; GroupDocs.Search zpracovává soubory ve streamovacím režimu, udržuje špičkovou paměť pod 200 MB i pro indexy o velikosti 10 GB.  
- **Nejlepší postupy** – Ukládejte index na SSD pro subsekundovou odezvu dotazů a povolte kompresi (`index.Compression = true`) pro snížení využití disku na polovinu.

## Často kladené otázky

**Q: Mohu indexovat ne‑textové soubory pomocí GroupDocs?**  
A: Ano, GroupDocs.Search může indexovat více než 150 formátů — včetně PDF, DOCX, PPTX, XLSX a typů obrázků — extrahováním vloženého textu pomocí OCR, kde je to potřeba.

**Q: Jak zvládnout velké objemy dokumentů?**  
A: Použijte `AddFolder` s konfigurovatelnou velikostí dávky, spusťte indexování ve službě na pozadí a pravidelně volajte `Optimize()`, aby se sloučily malé segmenty indexu.

**Q: Jaké jsou výhody používání redakce spolu s indexováním?**  
A: Redakce odstraňuje osobně identifikovatelné informace dříve, než vůbec dorazí do indexu, což zaručuje, že výsledky vyhledávání nikdy neodhalí chráněná data.

**Q: Je možné přizpůsobit vyhledávací algoritmy?**  
A: GroupDocs.Search poskytuje slovníky synonym, vlastní tokenizéry a filtry regulárních výrazů, což vám umožní jemně doladit skórování relevance.

**Q: Jak řešit běžné problémy s indexováním?**  
A: Ověřte oprávnění složky, ujistěte se, že .NET runtime odpovídá cíli knihovny, a zkontrolujte soubor protokolu vygenerovaný v adresáři indexu pro podrobné chybové zprávy.

## Zdroje

- **Dokumentace**: [GroupDocs Redaction .NET Docs](https://docs.groupdocs.com/search/net/)  
- **API reference**: [GroupDocs Redaction .NET API](https://reference.groupdocs.com/redaction/net)  
- **Stáhnout**: [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/)  
- **Bezplatná podpora**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Dočasná licence**: [Request a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

Prozkoumejte tyto zdroje, abyste prohloubili své znalosti a vylepšili implementaci GroupDocs.Search a Redaction v .NET. Šťastné programování!

---

**Last Updated:** 2026-07-26  
**Tested With:** GroupDocs.Search 23.10, GroupDocs.Redaction 23.10 for .NET  
**Author:** GroupDocs

## Související tutoriály

- [Mistrovské vytváření a slučování indexů s GroupDocs.Redaction .NET pro efektivní správu dokumentů](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [Mistrovství GroupDocs.Redaction .NET: Efektivní vytváření indexu a správa aliasů pro pokročilé vyhledávání dokumentů](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Mistrovství GroupDocs Search a Redaction v .NET: Komplexní průvodce pro správu dokumentů](/search/net/document-management/groupdocs-search-redaction-net-tutorial/)