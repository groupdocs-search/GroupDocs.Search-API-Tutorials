---
date: '2026-04-27'
description: Naučte se, jak v .NET pomocí GroupDocs.Search a Redaction zakrýt citlivá
  data, a zjistěte, jak přidávat dokumenty do indexu pro vyhledávání velkých dokumentů.
keywords:
- redact sensitive data
- add documents to index
- search large documents
title: GroupDocs.Search a Redaction v .NET – zakrýt citlivá data
type: docs
url: /cs/net/document-management/groupdocs-search-redaction-net-guide/
weight: 1
---

# GroupDocs.Search a Redaction v .NET – redakce citlivých údajů

Správa obrovského množství dokumentů může být náročná, zejména když potřebujete **redigovat citlivá data** a zároveň poskytovat rychlé vyhledávací možnosti. V tomto průvodci vás provedeme nastavením GroupDocs.Search spolu s GroupDocs.Redaction, ukážeme vám, jak **přidat dokumenty do indexu**, provádět efektivní operace **vyhledávání velkých dokumentů** a zajistit, aby vše bylo v souladu s požadavky na soukromí.

## Rychlé odpovědi
- **Co znamená „redact sensitive data“?** Znamená to trvalé odstranění nebo zakrytí důvěrných informací z dokumentů.  
- **Které knihovny potřebuji?** GroupDocs.Search a GroupDocs.Redaction pro .NET (k dispozici přes NuGet).  
- **Mohu automaticky indexovat .NET projekty?** Ano – podívejte se na sekci „Jak indexovat .NET“ pro podrobný návod.  
- **Jak zacházet s obrovskými soubory?** Použijte vyhledávání založené na blocích (chunk‑based), abyste zpracovávali data po zvládnutelných částech.  
- **Je pro produkci vyžadována licence?** Pro produkční použití je potřeba platná licence GroupDocs; jsou k dispozici bezplatné zkušební verze.

## Co je redakce citlivých dat?
Redakce citlivých dat je proces trvalého odstranění nebo zakrytí osobních, finančních či klasifikovaných informací z dokumentu tak, aby nebyly obnoveny ani zobrazeny neoprávněnými uživateli.

## Proč kombinovat GroupDocs.Search s Redaction?
- **Rychlost:** Vytvářejte prohledávatelné indexy, které vrací výsledky během milisekund.  
- **Bezpečnost:** Aplikujte pravidla redakce před sdílením nebo uložením dokumentů.  
- **Škálovatelnost:** Chunk search vám umožní pracovat s terabajty textu, aniž byste vyčerpali paměť.  
- **Soulad s předpisy:** Splňte GDPR, HIPAA a další předpisy tím, že zajistíte, že důvěrná data nikdy neuniknou.

## Požadavky
- Vývojové prostředí .NET (doporučeno Visual Studio).  
- Základní znalost C#.  
- Přístup k NuGet pro instalaci požadovaných balíčků.

## Nastavení GroupDocs.Redaction pro .NET

### Instalace pomocí .NET CLI
```bash
dotnet add package GroupDocs.Redaction
```

### Instalace pomocí Package Manageru
```powershell
Install-Package GroupDocs.Redaction
```

### UI NuGet Package Manageru
Vyhledejte **"GroupDocs.Redaction"** a nainstalujte nejnovější verzi.

### Kroky pro získání licence
- **Bezplatná zkušební verze:** Začněte s bezplatnou zkušební verzí a prozkoumejte funkce.  
- **Dočasná licence:** Požádejte o dočasnou licenci pro prodloužený přístup.  
- **Nákup:** Zvažte zakoupení pro dlouhodobé produkční použití.

### Základní inicializace a nastavení
```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Initialize with desired options or default ones
```

## Průvodce implementací

### Jak indexovat .NET projekty pomocí GroupDocs.Search
Níže rozdělujeme implementaci do přehledných číslovaných kroků, abyste ji mohli snadno sledovat.

#### Krok 1: Určete složku indexu
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SearchByChunks";
```
*Proč?* Definování vyhrazené složky udržuje váš index organizovaný a oddělený od surových dokumentů.

#### Krok 2: Vytvořte a nakonfigurujte index
```csharp
Index index = new Index(indexFolder);
```
*Účel:* Vytvoří nový prohledávatelný index na místě, které jste určili.

#### Krok 3: **Přidat dokumenty do indexu**
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath1");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath3");
```
*Vysvětlení:* Každé volání přidá soubor (nebo složku) do indexu, čímž jeho obsah učiní prohledávatelným.

### Vyhledávání velkých dokumentů pomocí Chunk Search
Chunk search vám umožní rozdělit obrovské soubory na menší části, čímž udržuje nízkou spotřebu paměti.

#### Krok 1: Definujte vyhledávací dotaz
```csharp
string query = "invitation";
```
*Účel:* Termín, který hledáte ve všech indexovaných souborech.

#### Krok 2: Nakonfigurujte možnosti Chunk Search
```csharp
SearchOptions options = new SearchOptions();
options.IsChunkSearch = true;
```
*Vysvětlení:* Povolení `IsChunkSearch` říká enginu, aby zpracovával data po blocích.

#### Krok 3: Proveďte počáteční vyhledávání
```csharp
SearchResult result = index.Search(query, options);
Console.WriteLine("Document count: " + result.DocumentCount);
Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
```
*Výsledek:* Zobrazuje, kolik dokumentů obsahuje termín a kolik celkových výskytů bylo nalezeno.

#### Krok 4: Pokračujte s následujícími bloky
```csharp
while (result.NextChunkSearchToken != null)
{
    result = index.SearchNext(result.NextChunkSearchToken);
    Console.WriteLine("Document count: " + result.DocumentCount);
    Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
}
```
*Proč tato smyčka?* Zajišťuje, že získáte výsledky z každého bloku, dokud není zpracována celá datová sada.

### Jak redigovat citlivá data pomocí GroupDocs.Redaction
Po nalezení informací, které je třeba chránit, aplikujte pravidla redakce.

#### Krok 1: Inicializujte nastavení redakce
```csharp
RedactorSettings settings = new RedactorSettings();
```

#### Krok 2: Aplikujte redakce
Použijte třídu `Redactor` (není zde zobrazena, aby byl zachován původní kód) k definování vzorů, textu nebo obrázků, které chcete zakrýt.  
*Tip:* Otestujte svá pravidla redakce na kopii dokumentu, abyste předešli neúmyslné ztrátě dat.

## Praktické aplikace
Tyto možnosti vynikají v mnoha odvětvích:

1. **Správa právních dokumentů** – Rychle vyhledávejte spisové složky a zároveň redigujte důvěrné údaje klienta.  
2. **Zpracování zdravotnických dat** – Chraňte PHI pacientů a zároveň umožněte klinickým pracovníkům najít relevantní záznamy.  
3. **Finanční audit** – Indexujte masivní transakční logy a redigujte čísla účtů nebo osobní identifikátory.

## Úvahy o výkonu
- **Optimalizace indexování:** Přindexujte pouze změněné soubory, aby byl index aktuální bez zbytečné práce.  
- **Správa zdrojů:** Přizpůsobte velikosti bloků (`options.ChunkSize`) podle RAM vašeho serveru.  
- **Asynchronní operace:** Pro velké dávky použijte asynchronní indexování, aby UI zůstalo responzivní.

## Často kladené otázky

**Q: Jak efektivně zacházet s velkými soubory?**  
A: Použijte vyhledávání založené na blocích (`IsChunkSearch = true`), abyste zpracovávali data v menších částech, čímž snížíte zatížení paměti.

**Q: Může GroupDocs.Redaction pracovat s šifrovanými dokumenty?**  
A: Ano – nejprve soubor dešifrujte, aplikujte redakci a poté jej v případě potřeby znovu zašifrujte.

**Q: Jaké licenční možnosti jsou k dispozici?**  
A: Bezplatná zkušební verze, dočasná licence pro hodnocení a plné komerční licence pro produkci.

**Q: Jak mohu řešit chyby indexu?**  
A: Ověřte, že cesta ke složce indexu je správná, zajistěte, aby aplikace měla oprávnění číst/zapisovat, a zkontrolujte, že jsou podporovány všechny formáty dokumentů.

**Q: Je možné dále přizpůsobit vyhledávací dotazy?**  
A: Rozhodně. Můžete kombinovat Boolean operátory, zástupné znaky a vyhledávání blízkosti pomocí API `SearchOptions`.

## Zdroje
- **Dokumentace:** [GroupDocs Redaction .NET](https://docs.groupdocs.com/search/net/)  
- **Reference API:** [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net)  
- **Stáhnout:** [Latest Releases](https://releases.groupdocs.com/search/net/)  
- **Bezplatná podpora:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Dočasná licence:** [Request Here](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2026-04-27  
**Testováno s:** GroupDocs.Search 23.9 a GroupDocs.Redaction 23.9 pro .NET  
**Autor:** GroupDocs