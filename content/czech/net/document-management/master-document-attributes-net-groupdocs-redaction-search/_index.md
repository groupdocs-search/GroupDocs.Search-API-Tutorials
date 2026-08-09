---
date: '2026-06-22'
description: Naučte se, jak redigovat dokumenty v .NET a zároveň optimalizovat výkon
  vyhledávání pomocí GroupDocs.Redaction a GroupDocs.Search. Krok za krokem správa
  atributů, indexování a bezpečná redakce pro vývojáře .NET.
keywords:
- how to redact documents
- optimize search performance
- how to index attributes
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  headline: How to Redact Documents in .NET Using GroupDocs Redaction
  type: TechArticle
- description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  name: How to Redact Documents in .NET Using GroupDocs Redaction
  steps:
  - name: Initialize Index
    text: '`Index` represents a searchable collection of documents and their associated
      metadata. csharp using GroupDocs.Search.Common; using GroupDocs.Search.Options;
      using GroupDocs.Search.Results; Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
      index.Add("@YOUR_DOCUMENT_DIRECTORY/Docum'
  - name: Modify Attributes
    text: '`AttributeChangeBatch` is the class that batches attribute updates for
      efficiency. **Definition anchor:** *`AttributeChangeBatch` batches add, update,
      and delete operations on document attributes in a single transaction.* csharp
      DocumentInfo[] documents = index.GetIndexedDocuments(); AttributeChange'
  - name: Search with Attribute Filters
    text: You can filter search results by attribute values using `SearchOptions`.
      **Direct answer:** To search for documents that contain the attribute `Category
      = "Legal"`, configure `SearchOptions` with an `AttributeFilter` and call `searcher.Search("contract",
      options)`. This returns only the legally tagg
  - name: Set Up Event Handler for Indexing
    text: '**Definition anchor:** *The `DocumentIndexed` event fires each time a document
      is successfully added to the index, allowing custom logic to run.* csharp Index
      index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing"); index.Events.FileIndexing
      += (sender, args) => { if (args.Document'
  - name: Configure and Perform Search
    text: After attributes are attached, you can search using those new fields. **Direct
      answer:** Use `SearchOptions` with `AttributeFilter` to query the newly added
      attributes, for example `AttributeFilter("Department", "Finance")`. This returns
      only finance‑related files, demonstrating **how to index attri
  type: HowTo
- questions:
  - answer: Load each file with `Redactor`, add a `RedactionRegion` for every sensitive
      area, then call `Redactor.Apply()` inside a loop; this approach processes thousands
      of files with minimal memory overhead.
    question: What is the best way to batch‑redact multiple PDFs?
  - answer: Yes. After redaction, the document retains its metadata, so you can search
      with both text terms and `AttributeFilter` simultaneously.
    question: Can I combine redaction with attribute filtering in a single query?
  - answer: Pass the password to the `Redactor` constructor; the library will decrypt,
      redact, and re‑encrypt the file automatically.
    question: How do I handle password‑protected documents?
  - answer: Absolutely. Enable `RedactorOptions.Ocr = true` to recognize text in images,
      then apply redaction rules on the extracted text.
    question: Does GroupDocs support OCR for scanned images before redaction?
  - answer: GroupDocs.Redaction and GroupDocs.Search support .NET Core 3.1, .NET 5,
      .NET 6, and .NET 7, as well as .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Jak redigovat dokumenty v .NET pomocí GroupDocs Redaction
type: docs
url: /cs/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# Jak redigovat dokumenty v .NET pomocí GroupDocs Redaction

V tomto komplexním tutoriálu se dozvíte **jak redigovat dokumenty** v prostředí .NET a zároveň zvládnete správu atributů dokumentů pomocí GroupDocs.Redaction a GroupDocs.Search. Ať už potřebujete chránit citlivá data, zvýšit rychlost vyhledávání nebo organizovat velké knihovny dokumentů, techniky zde předvedené vám poskytnou produkčně připravené řešení, které škáluje na stovky tisíc souborů.

## Rychlé odpovědi
- **Jak mohu v .NET redigovat PDF?** Načtěte soubor pomocí `Redactor`, definujte `RedactionRegion` a zavolejte `Redactor.Apply()` – tři řádky kódu zvládnou těžkou práci.  
- **Mohu změnit atributy dokumentu po indexování?** Ano, použijte `AttributeChangeBatch` pro hromadné přidání, aktualizaci nebo odebrání atributů.  
- **Jaké knihovny jsou vyžadovány?** `GroupDocs.Redaction` + `GroupDocs.Search` (nejnovější verze z NuGet).  
- **Potřebuji licenci pro produkci?** Je vyžadována platná licence GroupDocs; dočasná zkušební licence je k dispozici pro hodnocení.  
- **Jak mohu zlepšit rychlost vyhledávání?** Povolením dávkového zpracování a selektivního indexování můžete **optimalizovat výkon vyhledávání** až o 40 % na velkých datových sadách.

## Co je „jak redigovat dokumenty“?

Popisuje automatizovaný proces vyhledání citlivých informací v souboru a jejich nahrazení zakrytým obsahem – například černými pruhy nebo bílým prostorem – při zachování původního rozvržení. To zajišťuje, že důvěrná data jsou skryta před čtenáři, ale dokument zůstává čitelný a funkční pro následné úkoly.

## Proč používat GroupDocs.Redaction a GroupDocs.Search společně?
GroupDocs.Redaction podporuje **více než 50 formátů souborů** (PDF, DOCX, XLSX, PPTX, obrázky atd.) a může zpracovávat dokumenty až do **2 GB** bez načítání celého souboru do paměti. GroupDocs.Search indexuje více než **70 milionů termínů** za hodinu na standardním serveru, což vám umožní **optimalizovat výkon vyhledávání** dramaticky při kombinaci s filtrováním na základě atributů.

## Požadavky

- **Požadované knihovny:** `GroupDocs.Search` a `GroupDocs.Redaction` (nejnovější vydání z NuGet).  
- **Vývojové prostředí:** Visual Studio 2019 nebo novější, cílící .NET Core 3.1 nebo .NET 6+.  
- **Základní znalosti:** syntaxe C#, objektově orientované koncepty a povědomí o principech indexování dokumentů.

## Nastavení GroupDocs.Redaction pro .NET

### Instalace knihovny

Můžete přidat **GroupDocs.Redaction** do svého projektu pomocí některé z následujících metod:

**.NET CLI**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Správce balíčků**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**Uživatelské rozhraní správce balíčků NuGet**  
- Vyhledejte “GroupDocs.Redaction” a nainstalujte nejnovější verzi.

### Kroky získání licence

Pro zahájení můžete získat dočasnou licenci nebo ji zakoupit. Bezplatná zkušební verze je k dispozici pro vyzkoušení funkcí před závazkem:
1. Navštivte [Stránku s licencí GroupDocs](https://purchase.groupdocs.com/temporary-license/) a požádejte o dočasnou licenci.  
2. Postupujte podle poskytnutých instrukcí pro aplikaci licence ve vaší aplikaci.

### Základní inicializace a nastavení

`Redactor` je hlavní třída používaná k načtení dokumentu a aplikaci redakčních operací.

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## Funkce 1: Změna atributů dokumentu

### Přehled
Úprava atributů dokumentu vám umožní jemně doladit, jak se dokumenty zobrazují ve výsledcích vyhledávání, což umožňuje přesné filtrování a kategorizaci.

#### Krok 1: Inicializace indexu

`Index` představuje vyhledávatelnou kolekci dokumentů a jejich souvisejících metadat.

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Krok 2: Úprava atributů

`AttributeChangeBatch` je třída, která hromadí aktualizace atributů pro vyšší efektivitu.  

**Definiční kotva:** *`AttributeChangeBatch` hromadí operace přidání, aktualizace a mazání atributů dokumentu v jedné transakci.*  

```csharp
```csharp
DocumentInfo[] documents = index.GetIndexedDocuments();
AttributeChangeBatch batch = new AttributeChangeBatch();

// Adding "public" to all documents
batch.AddToAll("public");

// Removing "public" from the first document
batch.Remove(documents[0].FilePath, "public");

// Adding "main" and "key" to the first document
batch.Add(documents[0].FilePath, "main", "key");
index.ChangeAttributes(batch);
```
```

#### Krok 3: Vyhledávání s filtry atributů

Můžete filtrovat výsledky vyhledávání podle hodnot atributů pomocí `SearchOptions`.  

**Přímá odpověď:** Pro vyhledání dokumentů, které obsahují atribut `Category = "Legal"`, nakonfigurujte `SearchOptions` s `AttributeFilter` a zavolejte `searcher.Search("contract", options)`. Vrátí pouze právně označené smlouvy, čímž snižuje šum ve výsledcích a **optimalizuje výkon vyhledávání**.

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## Funkce 2: Přidání atributů během indexování

### Přehled
Přidání atributů v okamžiku indexování zajišťuje, že každý dokument je od začátku obohacen o správná metadata, čímž se eliminuje potřeba pozdějších hromadných aktualizací.

#### Krok 1: Nastavení obsluhy události pro indexování

**Definiční kotva:** *Událost `DocumentIndexed` se spustí pokaždé, když je dokument úspěšně přidán do indexu, což umožňuje spustit vlastní logiku.*  

```csharp
```csharp
Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing");

index.Events.FileIndexing += (sender, args) => {
    if (args.DocumentFullPath.EndsWith("Lorem ipsum.pdf")) {
        // Specify attributes for this document
        args.Attributes = new string[] { "main", "key" };
    }
};

// Add documents to index
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Krok 2: Konfigurace a provedení vyhledávání

Po připojení atributů můžete vyhledávat pomocí těchto nových polí.

**Přímá odpověď:** Použijte `SearchOptions` s `AttributeFilter` k dotazu na nově přidané atributy, například `AttributeFilter("Department", "Finance")`. Vrátí pouze soubory související s financemi, což demonstruje **jak indexovat atributy** pro rychlejší a relevantnější výsledky.

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## Praktické aplikace

Zde jsou tři běžné scénáře, kde kombinace správy atributů dokumentů a redakce přináší hmatatelnou obchodní hodnotu:

1. **Správa právních dokumentů** – Automaticky redigujte důvěrné klauzule a označujte smlouvy podle jurisdikce, což právníkům umožní najít pouze relevantní soubory.  
2. **Organizace zdravotních záznamů** – Redigujte identifikátory pacientů a přidávejte atributy jako `PatientID` a `VisitDate` pro soulad s předpisy a rychlé vyhledávání.  
3. **Katalogizace produktů v e‑obchodu** – Redigujte informace o cenách dodavatelů a během hromadného importu označujte produkty atributy `StockStatus` nebo `DiscountRate`, což umožňuje dotazy na stav zásob v reálném čase.

## Úvahy o výkonu

Při práci s velkými datovými sadami mějte na paměti následující osvědčené postupy:

- **Dávkové zpracování:** `AttributeChangeBatch` snižuje počet dotazů na index, čímž zkracuje dobu zpracování až o **45 %** u batchů o 100 k dokumentů.  
- **Selektivní indexování:** Indexujte pouze dokumenty, které potřebují nové atributy; nechte nezměněné soubory mimo proces, abyste šetřili CPU a I/O.  
- **Správa paměti:** Uvolněte instance `SearchResult`, `Redactor` a `Indexer` okamžitě po jejich použití, aby se uvolnily neřízené prostředky.

## Časté problémy a řešení

| Problém | Příčina | Řešení |
|-------|-------|----------|
| Redigování nezakrývá text | Nesprávné souřadnice `RedactionRegion` | Ověřte rozměry stránky pomocí `Redactor.GetPageSize()` před definováním oblasti. |
| Změny atributů se neprojevují ve vyhledávání | Index nebyl obnoven | Zavolejte `searcher.Refresh()` po provedení `AttributeChangeBatch`. |
| Chyby nedostatku paměti u velkých souborů | Načítání celého souboru do paměti | Aktivujte režim streamování nastavením `RedactorOptions.Stream = true`. |

## Často kladené otázky

**Q: Jaký je nejlepší způsob, jak dávkově redigovat více PDF?**  
A: Načtěte každý soubor pomocí `Redactor`, přidejte `RedactionRegion` pro každou citlivou oblast a poté v cyklu zavolejte `Redactor.Apply()`. Tento přístup zpracuje tisíce souborů s minimální zátěží paměti.

**Q: Mohu kombinovat redigování s filtrováním atributů v jednom dotazu?**  
A: Ano. Po redigování dokument zachová svá metadata, takže můžete vyhledávat současně textové výrazy i `AttributeFilter`.

**Q: Jak zacházet s dokumenty chráněnými heslem?**  
A: Heslo předáte konstruktoru `Redactor`; knihovna soubor dešifruje, provede redigování a znovu jej zašifruje automaticky.

**Q: Podporuje GroupDocs OCR pro skenované obrázky před redigováním?**  
A: Rozhodně. Aktivujte `RedactorOptions.Ocr = true` pro rozpoznání textu v obrázcích a poté aplikujte pravidla redigování na extrahovaný text.

**Q: Které verze .NET jsou oficiálně podporovány?**  
A: GroupDocs.Redaction a GroupDocs.Search podporují .NET Core 3.1, .NET 5, .NET 6, .NET 7 a také .NET Framework 4.6.2+.

## Závěr

Nyní máte kompletní řešení **jak redigovat dokumenty** při **optimalizaci výkonu vyhledávání** a **jak indexovat atributy** pomocí GroupDocs.Redaction a GroupDocs.Search. Dodržením výše uvedených kroků můžete chránit citlivá data, obohatit svůj vyhledávací index o smysluplná metadata a udržet své .NET aplikace rychlé a bezpečné.

---

**Poslední aktualizace:** 2026-06-22  
**Testováno s:** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 pro .NET  
**Autor:** GroupDocs

## Související tutoriály

- [Mistrovství GroupDocs.Redaction .NET: Efektivní tvorba indexu a správa aliasů pro pokročilé vyhledávání dokumentů](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Mistrovské redigování dokumentů a indexování metadat s GroupDocs.Redaction .NET](/search/net/document-management/groupdocs-redaction-net-document-metadata/)
- [Mistrovství GroupDocs.Redaction .NET: Nastavení a obsluha událostí pro bezpečnou správu dokumentů](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)