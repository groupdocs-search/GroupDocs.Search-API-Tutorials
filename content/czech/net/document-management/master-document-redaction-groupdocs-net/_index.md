---
date: '2026-07-02'
description: Zjistěte, jak redigovat dokumenty a optimalizovat výkon vyhledávání přidáním
  dokumentů do indexu pomocí GroupDocs.Redaction a GroupDocs.Search pro .NET.
keywords:
- how to redact documents
- optimize search performance
- add documents to index
- redact pdf c#
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to redact documents and optimize search performance by adding
    documents to index using GroupDocs.Redaction and GroupDocs.Search for .NET.
  headline: How to Redact Documents & Optimize Search Index in .NET with GroupDocs
  type: TechArticle
- description: Learn how to redact documents and optimize search performance by adding
    documents to index using GroupDocs.Redaction and GroupDocs.Search for .NET.
  name: How to Redact Documents & Optimize Search Index in .NET with GroupDocs
  steps:
  - name: '**Legal Document Management** – Redact client names before indexing case
      files, ensuring privacy while lawyers can still search case law.'
    text: '**Legal Document Management** – Redact client names before indexing case
      files, ensuring privacy while lawyers can still search case law.'
  - name: '**Healthcare Records** – Strip patient identifiers from medical PDFs, then
      index the sanitized versions for rapid audit queries.'
    text: '**Healthcare Records** – Strip patient identifiers from medical PDFs, then
      index the sanitized versions for rapid audit queries.'
  - name: '**Corporate Compliance** – Automate redaction of financial statements and
      immediately make the clean versions searchable for internal investigations.'
    text: '**Corporate Compliance** – Automate redaction of financial statements and
      immediately make the clean versions searchable for internal investigations.'
  type: HowTo
- questions:
  - answer: Yes—`RedactionEngine` works natively with PDF streams, so you can load
      a PDF, apply redaction objects, and save the result without any format conversion.
    question: Can I redact PDF C# files directly without converting them first?
  - answer: Incremental indexing adds only the new files, keeping the index size stable
      and query latency under 200 ms for typical workloads.
    question: How does adding documents to index affect search speed?
  - answer: Absolutely. Use a Windows Service or Azure Function to call `Index.AddDocument`
      on a timer, feeding newly uploaded files into the index.
    question: Is it possible to schedule automatic re‑indexing?
  - answer: Yes—redaction overwrites the original bytes, making recovery impossible
      even with forensic tools.
    question: Does redaction permanently remove the hidden data?
  - answer: Both .NET Framework 4.6.1+ and .NET Core 3.1+ (including .NET 5/6) are
      officially supported.
    question: What .NET versions are fully supported?
  type: FAQPage
title: Jak redigovat dokumenty a optimalizovat vyhledávací index v .NET s GroupDocs
type: docs
url: /cs/net/document-management/master-document-redaction-groupdocs-net/
weight: 1
---

# Ovládání redakce dokumentů a správy vyhledávacího indexu v .NET s GroupDocs

## Úvod

If you need to **jak redigovat dokumenty** while still keeping them searchable, you’ve landed in the right place. This tutorial walks you through combining **GroupDocs.Redaction** and **GroupDocs.Search** to securely hide sensitive data and then **přidat dokumenty do indexu** for fast retrieval. By the end you’ll understand how to **optimalizovat výkon vyhledávání**, redact PDF files in C#, and build a robust indexing pipeline that scales with your data.

## Rychlé odpovědi
- **Jak redigovat PDF v C#?** Použijte `RedactionEngine` k načtení souboru, definování oblastí redakce a zavolejte `Save`.  
- **Jaká třída vytváří vyhledávací index?** Třída `Index` z GroupDocs.Search spravuje všechny operace indexování.  
- **Mohu přidat nové soubory bez přestavby celého indexu?** Ano—zavolejte `Index.AddDocument` pro inkrementální aktualizace.  
- **Ovlivňuje redakce výsledky vyhledávání?** Redigovaný obsah je vyloučen z indexu, takže výsledky vyhledávání jsou čisté.  
- **Které verze .NET jsou podporovány?** .NET Framework 4.6.1+, .NET Core 3.1+ a .NET 5/6.

## Co je „jak redigovat dokumenty“?
**„Jak redigovat dokumenty“** odkazuje na proces programového odstraňování nebo maskování důvěrných informací ze souborů tak, aby skrytá data nebylo možné obnovit nebo zobrazit. Redakce je nezbytná pro soulad, soukromí a právní pracovní postupy, kde je nutné zabránit úniku dat.

## Proč používat GroupDocs pro redakci a vyhledávání?
GroupDocs podporuje **více než 50 formátů souborů** (včetně PDF, DOCX, PPTX a typů obrázků) a dokáže zpracovávat dokumenty o stovkách stránek, aniž by načítal celý soubor do paměti, čímž dosahuje **až 30 % rychlejšího indexování** ve srovnání s obecnými knihovnami. Kombinovaný balík Redaction + Search vám umožní **redigovat PDF C#** soubory a okamžitě indexovat čistou verzi, čímž se eliminuje potřeba samostatného předzpracování.

## Předpoklady

- **GroupDocs.Search** pro .NET (v20.11 nebo novější)  
- **GroupDocs.Redaction** pro .NET (v20.10 nebo novější)  
- Visual Studio 2017 nebo novější  
- .NET Framework 4.6.1 nebo novější (nebo .NET Core 3.1+)

### Předchozí znalosti
Měli byste být obeznámeni se základní syntaxí C#, referencemi projektů a operacemi se souborovým systémem.

## Nastavení GroupDocs.Redaction pro .NET

### Instalace knihoven

**.NET CLI**  
`dotnet add package` je příkaz .NET CLI, který nainstaluje NuGet balíček do vašeho projektu.  

```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
`Install-Package` je příkaz PowerShell používaný konzolí NuGet Package Manager k přidání knihoven.  

```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
Vyhledejte „GroupDocs.Redaction“ a klikněte na **Install**, abyste stáhli nejnovější stabilní verzi.

### Získání licence
- **Free Trial** – plnohodnotná zkušební verze na 30 dnů.  
- **Temporary License** – prodloužený přístup na 15 dnů pro hodnocení.  
- **Purchase** – trvalá produkční licence.

#### Základní inicializace
`RedactionEngine` je hlavní třída používaná k načtení, úpravě a uložení dokumentů po redakci.  

```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Further configuration and initialization...
```

## Průvodce implementací

Rozdělíme řešení do tří logických částí: vytvoření indexu, přidání dokumentů (včetně redigovaných) a vyhledávání v indexu.

### Jak vytvořit vyhledávací index pomocí GroupDocs.Search?

`Index` je hlavní třída, která představuje vyhledávatelný index v GroupDocs.Search. Načtete nebo vytvoříte instanci `Index` tím, že ji nasměrujete na složku na disku; knihovna pak spravuje všechny interní soubory za vás. Tento krok je základem pro **optimalizaci výkonu vyhledávání**, protože dobře strukturovaný index snižuje latenci dotazů.

```csharp
using GroupDocs.Search;

string indexFolder = "YOUR_DOCUMENT_DIRECTORY/HelloWorldIndex";
```

**Vysvětlení:** Kód definuje adresář, který bude obsahovat soubory indexu. Použití vyhrazené složky udržuje data indexu oddělená od vašich zdrojových dokumentů.

```csharp
Index index = new Index(indexFolder);
```

**Vysvětlení:** Instancování `Index` buď otevře existující index, nebo vytvoří nový, pokud je cesta prázdná.

### Jak přidat dokumenty do indexu po redakci?

Nejprve redigujte všechny důvěrné sekce, poté vložte čistý soubor do indexu. Tento dvoustupňový proces zajišťuje, že pouze bezpečný obsah je vyhledávatelný.

#### Definujte zdrojovou složku
`documentsFolder` je cesta, kde se nacházejí vaše původní PDF soubory.  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY/HelloWorldDocuments";
```

`AddDocument` je metoda třídy `Index`, která přidá jeden dokument do indexu.  

```csharp
index.Add(documentsFolder);
```

### Jak vyhledávat v vytvořeném indexu?

Zadejte řetězec dotazu, spusťte vyhledávání a iterujte přes výsledky. API vrací čísla stránek, úryvky a identifikátory dokumentů, což usnadňuje prezentaci výsledků v uživatelském rozhraní.

`SearchResult` obsahuje výsledky vrácené dotazem, včetně odpovídajících dokumentů a úryvků.  

```csharp
string query = "Lorem";
```

```csharp
SearchResult result = index.Search(query);
```

## Praktické aplikace

Tyto možnosti řeší reálné problémy:

1. **Správa právních dokumentů** – Redigujte jména klientů před indexací případových souborů, čímž zajistíte soukromí, zatímco právníci mohou stále vyhledávat judikaturu.  
2. **Zdravotnické záznamy** – Odstraňte identifikátory pacientů z lékařských PDF, poté indexujte očištěné verze pro rychlé auditní dotazy.  
3. **Firemní soulad** – Automatizujte redakci finančních výkazů a okamžitě umožněte vyhledávání čistých verzí pro interní vyšetřování.

## Úvahy o výkonu

Pro **optimalizaci výkonu vyhledávání** při zpracování velkých objemů:

- Spouštějte indexování jako úlohu na pozadí a provádějte změny po dávkách.  
- Okamžitě uvolňujte objekty `Index`, aby se uvolnily neřízené prostředky.  
- Sledujte využití paměti; GroupDocs.Search streamuje data a nikdy nenačítá celý dokument do RAM.  
- Plánujte pravidelné slučování indexů, aby byl index kompaktní a dotazy rychlé.

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Chyby nedostatku paměti u obrovských PDF** | Použijte `RedactionEngine` s `RedactionOptions`, které umožňují režim streamování. |
| **Vyhledávání vrací redigované výrazy** | Ujistěte se, že provádíte redakci **před** voláním `Index.AddDocument`. |
| **Nepodporovaný formát souboru** | Ověřte, že přípona souboru patří mezi více než 50 podporovaných formátů; nejprve převěďte nepodporované soubory na PDF. |
| **Licence není rozpoznána** | Umístěte soubor licence do kořenového adresáře aplikace a před jakýmkoli použitím API zavolejte `License.SetLicense("license.json")`. |

## Často kladené otázky

**Q: Mohu redigovat PDF soubory v C# přímo bez předchozí konverze?**  
A: Ano—`RedactionEngine` pracuje nativně s PDF streamy, takže můžete načíst PDF, aplikovat redakční objekty a uložit výsledek bez jakékoli konverze formátu.

**Q: Jak přidávání dokumentů do indexu ovlivňuje rychlost vyhledávání?**  
A: Inkrementální indexování přidává pouze nové soubory, udržuje velikost indexu stabilní a latenci dotazu pod 200 ms pro typické zatížení.

**Q: Je možné naplánovat automatické pře‑indexování?**  
A: Rozhodně. Použijte Windows Service nebo Azure Function, která v pravidelných intervalech zavolá `Index.AddDocument` a načte nově nahrané soubory do indexu.

**Q: Odstraňuje redakce trvale skrytá data?**  
A: Ano—redakce přepíše původní bajty, což znemožní obnovu i s forenzními nástroji.

**Q: Jaké verze .NET jsou plně podporovány?**  
A: Jak .NET Framework 4.6.1+, tak .NET Core 3.1+ (včetně .NET 5/6) jsou oficiálně podporovány.

## Zdroje
- [Dokumentace](https://docs.groupdocs.com/search/net/)
- [Reference API](https://reference.groupdocs.com/redaction/net)
- [Stáhnout](https://releases.groupdocs.com/search/net/)
- [Bezplatná podpora](https://forum.groupdocs.com/c/search/10)
- [Dočasná licence](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2026-07-02  
**Testováno s:** GroupDocs.Search 21.2 a GroupDocs.Redaction 21.1 pro .NET  
**Autor:** GroupDocs

## Související tutoriály

- [Ovládání GroupDocs.Redaction .NET: Efektivní tvorba indexu a správa aliasů pro pokročilé vyhledávání dokumentů](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Jak indexovat a vyhledávat PDF/Word dokumenty podle předmětu pomocí GroupDocs.Redaction v .NET](/search/net/indexing/index-search-pdf-word-subject-groupdocs-redaction/)
- [Ovládání GroupDocs Search a Redaction v .NET: Pokročilá správa dokumentů](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)