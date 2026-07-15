---
date: '2026-04-04'
description: Naučte se vyhledávat právní dokumenty a spravovat indexy pomocí GroupDocs.Search
  a integrovat redakci pro lékařské záznamy s GroupDocs.Redaction v .NET.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: Vyhledávejte právní dokumenty pomocí GroupDocs Search & Redaction pro .NET
type: docs
url: /cs/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Vyhledávání právních dokumentů pomocí GroupDocs Search & Redaction v .NET

V dnešním datově řízeném prostředí je **vyhledávání právních dokumentů** rychle a bezpečně kritickým požadavkem pro každou organizaci. Ať už pracujete s kontrakty, soudními podáními nebo zprávami o souladu, GroupDocs.Search vám poskytuje rychlý, škálovatelný index, zatímco GroupDocs.Redaction zajišťuje, že citlivé informace zůstávají skryté. Tento tutoriál vás provede nastavením vyhledávatelného indexu, přidáváním dokumentů z více složek a konfigurací redakce, abyste mohli bezpečně vyhledávat lékařské záznamy a další důvěrné soubory.

## Rychlé odpovědi
- **Co dělá GroupDocs.Search?** Vytváří full‑textový vyhledávatelný index pro širokou škálu formátů dokumentů.  
- **Mohu redigovat informace před vyhledáváním?** Ano – použijte GroupDocs.Redaction k maskování nebo odstranění citlivých dat.  
- **Jak přidám dokumenty do indexu?** Zavolejte `index.Add("folderPath")` pro každou složku, kterou chcete zahrnout.  
- **Jaké typy souborů jsou podporovány?** PDF, DOCX, PPTX, TXT a mnoho dalších.  
- **Potřebuji licenci pro produkci?** Je k dispozici dočasná zkušební verze; pro komerční použití je vyžadována trvalá licence.

## Předpoklady
Abyste mohli sledovat tento tutoriál, ujistěte se, že máte:
- .NET Core SDK (3.1 nebo novější) nainstalovaný.
- Visual Studio Code, Visual Studio nebo jiné IDE podporující .NET.
- Základní znalosti programování v C#.

### Získání licence
Můžete začít s bezplatnou zkušební verzí obou knihoven. Pro delší používání zvažte získání dočasné licence nebo zakoupení licence na [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

## Instalace požadovaných balíčků

**Instalace GroupDocs.Search:**  
Pomocí **.NET CLI** spusťte:
```bash
dotnet add package GroupDocs.Search
```
Alternativně použijte Package Manager Console ve Visual Studiu:
```powershell
Install-Package GroupDocs.Search
```

**Instalace GroupDocs.Redaction:**  
- Použijte .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- Nebo přes Package Manager:
```powershell
Install-Package GroupDocs.Redaction
```

Navštivte rozhraní NuGet Package Manager UI a vyhledejte "GroupDocs.Redaction", pokud chcete instalovat pomocí GUI.

## Konfigurace nastavení Redactoru
Než začnete redigovat, možná budete chtít upravit chování redaktoru (např. nastavit barvu redakce nebo definovat vlastní vzory). Následující úryvek ukazuje základní inicializaci:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Tip:** Přizpůsobte `redactorSettings` tak, aby odpovídala zásadám souladu vaší organizace (např. nahraďte text černými rámečky, aplikujte OCR před redakcí atd.).

## Průvodce implementací

### Jak vyhledávat právní dokumenty?
Vytvoření vyhledávatelného indexu je základem pro rychlé vyhledávání právních dokumentů. GroupDocs.Search vám umožní nasměrovat na libovolnou složku, vytvořit index a poté spouštět složité dotazy napříč tisíci soubory.

### Jak přidat dokumenty do indexu
Přidávání dokumentů je jednoduché – stačí nasměrovat knihovnu na adresáře, které obsahují vaše soubory. Můžete přidat více složek, což je užitečné, když je váš právní korpus rozprostřen na různých místech.

#### Vytváření a správa indexu
**Přehled:**  
Vytvoření indexu je prvním krokem k efektivním operacím vyhledávání dokumentů. GroupDocs.Search vám umožní vytvořit vyhledávatelný index v libovolném adresáři dle vašeho výběru, což umožňuje rychlé vyhledávání dokumentů.

##### Krok 1: Vytvořit index
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Vysvětlení:* `Index` inicializuje vyhledávací index ve zadaném adresáři. Ujistěte se, že cesta odpovídá struktuře složek vašeho projektu.

##### Krok 2: Přidání dokumentů do indexu
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Vysvětlení:* Metoda `Add` prohledá danou složku a zahrne každý podporovaný dokument do indexu. Použijte ji k **přidání dokumentů do indexu** z více zdrojů, jako jsou smlouvy, soudní spisy nebo lékařské záznamy.

### Získání a zobrazení zpráv o indexování
**Přehled:**  
Zprávy o indexování vám poskytují přehled o tom, kolik dokumentů bylo zpracováno, celkovém počtu termínů a velikosti úložiště – klíčové metriky pro ladění výkonu.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*Vysvětlení:* `GetIndexingReports` vrací pole zpráv, které podrobně popisují proces indexování, což vám pomáhá sledovat a optimalizovat výkon.

## Praktické aplikace
1. **Správa právních dokumentů:** Automatizujte indexování soudních spisů pro okamžité vyhledání zákonů, podání a rozhodnutí.  
2. **Systém lékařských záznamů:** Vyhledávejte záznamy pacientů při zachování soukromí pomocí GroupDocs.Redaction k maskování PHI.  
3. **Firemní HR portál:** Kombinujte vyhledávatelné soubory zaměstnanců s redakcí pro ochranu osobních údajů.

## Úvahy o výkonu
- **Optimalizace velikosti indexu:** Pravidelně odstraňujte zastaralé položky a přestavujte index, aby zůstal úsporný.  
- **Správa paměti:** Využijte garbage collector .NET; uvolněte objekty `Index`, když již nejsou potřeba.  
- **Nejlepší praktiky škálovatelnosti:** Ukládejte index na rychlé SSD úložiště a zvažte rozdělení velkých korpusů do více indexů.

## Často kladené otázky

**Q: Jaké jsou hlavní využití GroupDocs.Search?**  
A: Je ideální pro vytváření vyhledávatelných indexů z velkých kolekcí dokumentů, umožňující rychlé vyhledávání právních a lékařských souborů.

**Q: Jak GroupDocs.Redaction zajišťuje soukromí dat?**  
A: Umožňuje definovat redakční vzory, které trvale odstraní nebo maskují citlivé informace před indexací nebo sdílením dokumentu.

**Q: Mohu tyto knihovny použít v cloudovém prostředí?**  
A: Ano – obě knihovny fungují v Azure, AWS nebo v jakémkoli kontejnerizovaném .NET nasazení s řádnou licencí.

**Q: Jaké formáty souborů jsou podporovány GroupDocs.Search?**  
A: PDF, Word, Excel, PowerPoint, TXT, HTML a mnoho dalších podnikových formátů.

**Q: Jak řešit chyby při indexování?**  
A: Ověřte cesty ke složkám, zkontrolujte oprávnění souborů a prohlédněte výstup konzole z `IndexingReport` pro konkrétní chybové kódy.

## Zdroje
- **Dokumentace:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **API Reference:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Stáhnout:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Bezplatná podpora:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Dočasná licence:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Poslední aktualizace:** 2026-04-04  
**Testováno s:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 pro .NET  
**Autor:** GroupDocs