---
date: '2026-06-07'
description: Zjistěte, jak efektivně aktualizovat index pomocí GroupDocs.Search a
  Redaction pro .NET a vylepšit tak váš systém správy dokumentů.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: Jak aktualizovat index pomocí GroupDocs.Search a Redaction (.NET)
type: docs
url: /cs/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# Jak aktualizovat index pomocí GroupDocs.Search & Redaction (.NET)

V moderních, datově řízených podnicích může **jak aktualizovat index** rychle a spolehlivě rozhodnout o úspěchu vašeho vyhledávacího zážitku. Ať už zpracováváte tisíce smluv nebo rozsáhlou znalostní bázi, udržování vyhledávacího indexu v souladu s nejnovějšími změnami dokumentů je nezbytné pro rychlé a přesné výsledky. Tento tutoriál vás provede používáním GroupDocs.Search pro .NET společně s GroupDocs.Redaction k **aktualizaci indexu**, správě verzovaných indexů a ochraně citlivého obsahu – vše v čistém .NET projektu.

## Rychlé odpovědi
- **Co znamená “jak aktualizovat index”?** Jedná se o proces úpravy existujícího vyhledávacího indexu, aby se nové nebo změněné dokumenty staly vyhledávatelné bez nutnosti kompletního přestavování.  
- **Které knihovny jsou vyžadovány?** GroupDocs.Search a GroupDocs.Redaction pro .NET (obě dostupné přes NuGet).  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro testování; produkční licence odemkne plnou funkčnost.  
- **Mohu to spustit na .NET Core?** Ano, knihovny podporují .NET Framework 4.5+, .NET Core 3.1+ a .NET 5/6+.  
- **Jaký výkon mohu očekávat?** Aktualizace 1 GB indexu se 2 vlákny skončí za méně než minutu na typickém 4‑jádrovém serveru.

## Co je “jak aktualizovat index”?
**Jak aktualizovat index** odkazuje na techniku aplikování inkrementálních změn na existující vyhledávací index místo jeho kompletního přestavování. Tento přístup snižuje prostoje, šetří cykly CPU a udržuje výsledky vyhledávání aktuální, když jsou dokumenty přidávány, upravovány nebo odstraňovány.

## Proč použít GroupDocs.Search & Redaction pro aktualizace indexu?
GroupDocs.Search podporuje **více než 50 formátů souborů** (PDF, DOCX, XLSX, PPTX, HTML, obrázky atd.) a dokáže zpracovat dokumenty s mnoha stovkami stránek, aniž by načítal celý soubor do paměti. V kombinaci s GroupDocs.Redaction můžete automaticky odstranit nebo zamaskovat citlivá data před indexací, což zajišťuje soulad s předpisy a zároveň zachovává relevanci vyhledávání.

## Předpoklady

- **GroupDocs.Search** – nainstalujte přes NuGet.  
- **GroupDocs.Redaction for .NET** – vyžadováno pro funkce redakce.  
- Visual Studio (nebo jakékoli .NET IDE) s nainstalovaným .NET 6+.  
- Základní znalost C# a povědomí o konceptech indexování.

### Požadované knihovny a verze
- **GroupDocs.Search** – nejnovější stabilní verze z NuGet.  
- **GroupDocs.Redaction for .NET** – nejnovější stabilní verze z NuGet.

### Požadavky na nastavení prostředí
- Počítač s Windows nebo Linuxem s nainstalovaným .NET SDK.  
- Přístup ke složce, kde budou uloženy soubory indexu.

### Předpoklady znalostí
- Porozumění základům indexování dokumentů a vyhledávání.  
- Povědomí o správě životního cyklu dokumentů v podnikovém systému.

## Nastavení GroupDocs.Redaction pro .NET

### Instalace balíčků

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Vyhledejte “GroupDocs.Redaction” a nainstalujte nejnovější verzi.

### Kroky získání licence
1. **Free Trial** – začněte s trial verzí pro prozkoumání všech funkcí.  
2. **Temporary License** – požádejte o dočasný klíč pro rozšířené testování.  
3. **Purchase** – získejte plnou licenci pro produkční nasazení.

### Základní inicializace a nastavení
`Redactor` je hlavní třída, která aplikuje pravidla redakce na dokumenty.  
Pro zahájení odkažte na obor názvů Redaction a vytvořte instanci `Redactor`:

```csharp
using GroupDocs.Redaction;
```

## Průvodce implementací

Probereme dvě hlavní funkce: aktualizaci indexovaných dokumentů a správu verzí indexu.

### Jak aktualizovat index pomocí GroupDocs.Search?

`Index` představuje vyhledávatelnou kolekci uloženou na disku.  
`UpdateOptions` konfiguruje, jak jsou prováděny inkrementální aktualizace (např. počet vláken).  
`UpdateDocument` aplikuje změny na jeden dokument a `Commit` dokončuje všechny čekající aktualizace.

**Direct answer (40‑70 words):**  
Vytvořte objekt `Index`, který ukazuje na složku s vaším indexem, použijte `UpdateOptions` k určení počtu vláken, pro každý změněný soubor zavolejte `UpdateDocument` a nakonec spusťte `Commit` pro uložení změn. Tento inkrementální přístup aktualizuje pouze upravené části, takže je index aktuální bez nutnosti kompletního přestavování.

#### Funkce 1: Aktualizace indexovaných dokumentů

##### Přehled
Aktualizace indexovaných dokumentů zajišťuje, že výsledky vyhledávání odrážejí nejnovější obsah, i když jsou dokumenty upravovány nebo nahrazovány.

##### Krok 1: Vytvoření indexu
Třída `Index` je objekt nejvyšší úrovně, který představuje vyhledávatelnou kolekci na disku.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### Krok 2: Přidání dokumentů do indexu
Přidejte soubory ze složky; knihovna automaticky extrahuje vyhledávatelný text.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### Krok 3: Vyhledání a aktualizace
Spusťte dotaz, upravte zdrojový soubor a poté zavolejte `UpdateDocument` se stejným `UpdateOptions`, který byl použit během indexování.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Proč to funguje:** Nastavením `Threads = 2` aktualizace využívá dva jádra CPU, což zkracuje dobu zpracování přibližně na polovinu na čtyřjádrovém stroji.

### Jak udržet kontrolu verzí indexu?

`IndexUpdater` je pomocná třída, která aktualizuje starší formáty indexu na nejnovější verzi podporovanou knihovnou.

**Direct answer (40‑70 words):**  
Vytvořte instanci `IndexUpdater` s cestou k vašemu existujícímu indexu, zavolejte `CanUpdateVersion()` pro ověření kompatibility a v případě potřeby spusťte `UpdateVersion()`. Po aktualizaci načtěte index v novém formátu a proveďte vyhledávání pro potvrzení, že vše funguje. Tím zajistíte plynulou migraci mezi verzemi knihovny.

#### Funkce 2: Správa verzí indexu

##### Přehled
Správa verzí zajišťuje, že starší indexy zůstávají vyhledávatelné po aktualizaci knihovny.

##### Krok 1: Kontrola kompatibility
`IndexUpdater` kontroluje, zda lze aktuální index aktualizovat na nejnovější formát.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### Krok 2: Načtení a vyhledání
Po aktualizaci načtěte obnovený index a spusťte dotaz pro ověření integrity.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Proč to funguje:** Ochrana `CanUpdateVersion` zabraňuje výjimkám za běhu způsobeným neodpovídajícími schématy indexu a poskytuje bezpečnou cestu pro aktualizaci.

## Praktické aplikace

Reálné scénáře, kde **jak aktualizovat index** má význam:

1. **Správa právních dokumentů** – Rychle přeindexujte smlouvy po změnách a zároveň odstraňte důvěrné klauzule.  
2. **Firemní archivy** – Udržujte historické záznamy vyhledávatelné bez nutnosti přepracování milionů souborů.  
3. **Systémy správy obsahu (CMS)** – Posílejte inkrementální aktualizace do vyhledávacího indexu, když autoři publikují nové články.

## Úvahy o výkonu

- **Možnosti vláken:** Nastavte `UpdateOptions.Threads` podle počtu jader CPU; více vláken zvyšuje propustnost, ale také spotřebu paměti.  
- **Využití zdrojů:** Sledujte RAM; knihovna streamuje soubory, takže špičky v paměti jsou minimální i u PDF s 500 stránkami.  
- **Osvedčené postupy:** Plánujte pravidelné inkrementální aktualizace a odstraňujte zastaralé verze indexu pro udržení optimálního výkonu.

## Časté problémy a řešení

| Problém | Příčina | Řešení |
|-------|-------|----------|
| **Index not found** | Špatná cesta ke složce | Ověřte, že konstruktor `Index` ukazuje na správný adresář. |
| **Version mismatch error** | Použití staršího indexu s novější knihovnou | Spusťte tok `IndexUpdater` před běžným indexováním. |
| **Redaction not applied** | Pravidla redakce načtena po indexování | Aplikujte redakci **před** přidáním dokumentů do indexu. |

## Často kladené otázky

**Q: Jaký je rozdíl mezi `UpdateDocument` a `Rebuild`?**  
A: `UpdateDocument` mění pouze změněné soubory, zatímco `Rebuild` znovu vytvoří celý index od začátku, což spotřebuje více času a zdrojů.

**Q: Mohu aktualizovat více dokumentů paralelně?**  
A: Ano, nastavte `UpdateOptions.Threads` na počet jader, která chcete využít; knihovna interně zpracovává paralelní zpracování.

**Q: Podporuje GroupDocs.Search šifrované PDF?**  
A: Rozhodně. Zadejte heslo pomocí `SearchOptions.Password` při načítání dokumentu.

**Q: Jak ověřím, že redakce byla úspěšná před indexací?**  
A: Zavolejte `Redactor.Apply()` a zkontrolujte velikost výstupního souboru; snížená velikost často naznačuje úspěšnou redakci.

**Q: Jaké verze .NET jsou oficiálně podporovány?**  
A: .NET Framework 4.5+, .NET Core 3.1+, .NET 5 a .NET 6+.

## Závěr

Nyní máte kompletní, připravený průvodce pro **jak aktualizovat index** pomocí GroupDocs.Search a jak udržet tyto indexy verze‑kompatibilní s GroupDocs.Redaction pro .NET. Dodržením výše uvedených kroků zajistíte, že vaše vyhledávací vrstva zůstane rychlá, přesná a v souladu s předpisy o ochraně soukromí dat.

**Další kroky:**  
- Experimentujte s různými nastaveními `Threads`, abyste našli optimální hodnotu pro váš hardware.  
- Prozkoumejte pokročilé vzory redakce (např. odstraňování SSN pomocí regulárních výrazů) před indexací.  
- Integrujte rutinu aktualizace indexu do vašeho CI/CD pipeline pro plně automatizovanou správu dokumentů.

---

**Last Updated:** 2026-06-07  
**Tested With:** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**Author:** GroupDocs  

## Zdroje
- [Dokumentace](https://docs.groupdocs.com/search/net/)
- [Reference API](https://reference.groupdocs.com/redaction/net)
- [Stáhnout GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Bezplatné fórum podpory](https://forum.groupdocs.com/c/search/10)
- [Dočasná licence](https://purchase.groupdocs.com/temporary-license/)

## Související tutoriály

- [Mistrovství GroupDocs.Redaction .NET: Efektivní tvorba indexu a správa aliasů pro pokročilé vyhledávání dokumentů](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Implementace synonymického vyhledávání s GroupDocs.Redaction .NET pro vylepšenou správu dokumentů](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [Mistrovství GroupDocs Search a Redaction v .NET: Pokročilá správa dokumentů](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)