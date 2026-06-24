---
date: '2026-04-02'
description: Naučte se filtrovat podle přípony souboru a vyhledávat pouze soubory
  txt pomocí GroupDocs.Redaction pro .NET — zvyšte efektivitu správy dokumentů.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Filtrování podle přípony souboru v .NET pomocí GroupDocs.Redaction
type: docs
url: /cs/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Filtrace podle přípony souboru v .NET pomocí GroupDocs.Redaction

Prohledávání obrovské kolekce souborů může být ohromující, zejména když potřebujete výsledky jen z konkrétních typů souborů. V tomto tutoriálu se dozvíte **jak filtrovat podle přípony souboru** pomocí GroupDocs.Redaction pro .NET, což vám umožní vyhledávat jen soubory txt nebo jakoukoli jinou zvolenou příponu. Provedeme vás nastavením filtrů jak podle typu souboru, tak podle cesty, abyste mohli rychle najít přesně dokumenty, které potřebujete.

## Rychlé odpovědi
- **Co dělá „filtrace podle přípony souboru“?** Omezuje vyhledávání na dokumenty, které odpovídají zadané příloze souboru (např. *.txt).  
- **Proč k tomu použít GroupDocs.Redaction?** Poskytuje vestavěné API pro filtrování, která jsou rychlá a snadno integrovatelná.  
- **Potřebuji licenci?** Bezplatná zkušební verze stačí pro testování; pro produkční nasazení je vyžadována placená licence.  
- **Které verze .NET jsou podporovány?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Mohu kombinovat filtry podle typu souboru a cesty?** Ano – můžete použít více filtrů pro vysoce přesná vyhledávání.

## Co se naučíte
- Jak **filtrovat podle přípony souboru**, aby byly prohledávány jen textové soubory.  
- Jak nastavit **filtry cesty k souboru**, aby se výsledky omezily na konkrétní složky nebo pojmenovací vzory.  
- Tipy, jak udržet index rychlý a úsporný na paměť.

## Předpoklady

Předtím, než začnete, ujistěte se, že máte:

- **Knihovnu GroupDocs.Redaction** nainstalovanou a kompatibilní s vaším .NET projektem.  
- Vývojové prostředí, jako je Visual Studio nebo VS Code.  
- Základní znalost C# a povědomí o struktuře .NET projektu.

## Nastavení GroupDocs.Redaction pro .NET

Nejprve přidejte knihovnu do svého projektu.

**Použití .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Použití Package Manageru:**  
```bash
Install-Package GroupDocs.Redaction
```

Nebo najděte „GroupDocs.Redaction“ v uživatelském rozhraní NuGet Package Manageru a nainstalujte nejnovější verzi.

### Získání licence

Můžete začít s bezplatnou zkušební verzí nebo požádat o dočasnou licenci. Pro dlouhodobé projekty zakupte licenci na oficiálních stránkách.

### Základní inicializace

Po instalaci balíčku vytvořte index, který bude obsahovat odkazy na vaše dokumenty:  
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Průvodce implementací

### Funkce 1: Nastavení filtru pro textové dokumenty (.txt)

#### Jak filtrovat podle přípony souboru pro textové dokumenty

1. **Definujte index a složky s dokumenty**  
   Nastavte cesty, kde se nacházejí vaše zdrojové soubory:  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Vytvořte index**  
   Načtěte všechny soubory ze zdrojové složky do indexu:  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Nakonfigurujte možnosti vyhledávání s filtrem podle přípony souboru**  
   Řekněte enginu, aby zvažoval jen soubory *.txt:  

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Proveďte vyhledávání**  
   Spusťte dotaz; filtr zajistí, že soubory, které nejsou textové, budou ignorovány:  

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Vysvětlení*: Metoda `Search` vrací shody, které splňují filtr, což výrazně snižuje šum a zlepšuje výkon.

### Funkce 2: Filtry cesty k souboru

#### Proč používat filtry cesty k souboru?

Někdy potřebujete omezit vyhledávání na konkrétní složku oddělení nebo sadu souborů, které sdílejí pojmenovací konvenci. Filtry cesty vám umožní přesně to.

1. **Definujte index a složky s dokumenty**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Vytvořte index**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Nakonfigurujte možnosti vyhledávání s regulárním výrazem založeným na cestě**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Tento regulární výraz odpovídá libovolnému souboru, jehož úplná cesta obsahuje slovo „Lorem“, což vám umožní cílit na konkrétní podadresáře.

4. **Spusťte vyhledávání založené na cestě**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Praktické aplikace
- **Správa právních dokumentů** – Rychle najděte relevantní smlouvy uložené jako prosté textové soubory.  
- **Akademický výzkum** – Vyberte jen *.txt výzkumné poznámky, které patří do konkrétní složky projektu.  
- **Firemní reportování** – Filtrovat interní zprávy podle cesty oddělení (např. `/Finance/2025/`).  

## Úvahy o výkonu
- Indexujte jen typy dokumentů, které skutečně potřebujete; zbytečné soubory zvětšují velikost indexu a dobu vyhledávání.  
- Udržujte svůj index aktuální pomocí naplánované úlohy, která volá `index.Add()` pro nové nebo změněné soubory.  
- Používejte jednoduché regulární výrazy; příliš složité vzory mohou zpomalit vyhledávací engine.  
- Uvolněte objekty `Index`, když již nejsou potřeba, aby se uvolnila paměť.

## Závěr
Nyní víte, jak **filtrovat podle přípony souboru** a použít **filtry cesty k souboru** pomocí GroupDocs.Redaction pro .NET. Tyto techniky vám poskytují jemnou kontrolu nad velkými kolekcemi dokumentů, což zrychluje a zpřesňuje vyhledávání. Dále experimentujte s kombinací více filtrů nebo integrací vyhledávání do většího pracovního postupu aplikace.

## Sekce FAQ

**Q1: Mohu filtrovat dokumenty jiné než textové soubory?**  
A1: Ano, GroupDocs.Redaction podporuje mnoho formátů. Změňte argument v `CreateFileExtension` na požadovanou příponu (např. ".pdf").

**Q2: Jak pravidelně aktualizuji svůj vyhledávací index?**  
A2: Naplánujte službu na pozadí nebo cron úlohu, která spustí `index.Add()` na adresářích, které chcete udržovat aktuální.

**Q3: Má filtrování podle cesty k souboru dopad na výkon?**  
A3: Správně optimalizované regulární výrazy mají minimální dopad, ale vždy provádějte benchmark s vaším vlastním datasetem.

**Q4: Mohu kombinovat více filtrů pro přesnější vyhledávání?**  
A4: Rozhodně. Můžete řetězit filtry nebo vytvořit složené filtry, které cílí současně na typ souboru i cestu.

**Q5: Kde najdu další zdroje o GroupDocs.Redaction?**  
A5: Navštivte oficiální dokumentaci na [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) pro podrobné návody a reference API.

## Často kladené otázky

**Q: Funguje `SearchDocumentFilter` s šifrovanými soubory?**  
A: Filtr samotný pracuje s metadaty souboru, takže šifrované soubory jsou stále indexovány, pokud během indexování poskytnete potřebné dešifrovací údaje.

**Q: Mohu pro filtrování cesty použít zástupné znaky místo regulárního výrazu?**  
A: API v současnosti vyžaduje regulární výraz, ale můžete simulovat jednoduché zástupné znaky (např. `.*` pro libovolné znaky).

**Q: Jak velký může být index, než budu muset uvažovat o rozdělení (sharding)?**  
A: Indexy o velikosti několika stovek gigabajtů mohou těžit z rozdělení do více logických indexů; testujte výkon, jak se vaše kolekce rozrůstá.

**Q: Existují vestavěné metody pro odstranění dokumentů z indexu?**  
A: Ano – zavolejte `index.Delete(documentId)` nebo `index.DeleteAll()` pro správu zastaralých položek.

**Q: Existuje způsob, jak zobrazit náhled výsledků vyhledávání před načtením celého dokumentu?**  
A: Objekt `SearchResult` obsahuje informace o úryvku, které můžete zobrazit v UI, aniž byste otevírali celý soubor.

## Zdroje
- **Dokumentace**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **Reference API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Stáhnout**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **Bezplatná podpora**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Dočasná licence**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Poslední aktualizace:** 2026-04-02  
**Testováno s:** GroupDocs.Redaction 23.12 pro .NET  
**Autor:** GroupDocs