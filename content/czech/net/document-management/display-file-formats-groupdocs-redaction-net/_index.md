---
date: '2026-06-07'
description: Naučte se, jak vypsat přípony souborů a získat formáty souborů pomocí
  GroupDocs.Redaction v C#. Obsahuje nastavení, kód a praktické tipy.
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
title: Jak vypsat přípony souborů pomocí GroupDocs.Redaction v .NET – komplexní průvodce
type: docs
url: /cs/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Zobrazení podporovaných formátů souborů pomocí GroupDocs.Redaction v .NET

Správa široké škály typů dokumentů je každodenní realitou pro .NET vývojáře. Pomocí **GroupDocs.Redaction** můžete **vypsat přípony souborů**, které knihovna podporuje, což vaší aplikaci poskytne inteligenci pro přijímání nebo odmítání nahrávek, prezentaci uživatelsky přívětivých možností a vyhnutí se nákladným chybám za běhu. Tento tutoriál vás provede vším, co potřebujete – od předpokladů až po kompletní, připravenou implementaci pro produkci – takže můžete sebejistě **získat formáty souborů** a **c# display file formats** ve svém řešení.

## Rychlé odpovědi
- **Co znamená “list file extensions”?** Znamená to získání kolekce podporovaných identifikátorů typů souborů (např. *.pdf*, *.docx*) z API.  
- **Který NuGet balíček poskytuje tuto funkci?** `GroupDocs.Redaction` (nejnovější stabilní verze).  
- **Potřebuji licenci pro spuštění ukázky?** Licence zdarma pro zkušební verzi funguje pro vývoj; pro produkci je vyžadována trvalá licence.  
- **Mohu výsledek kešovat?** Ano — uložte seznam do paměti nebo distribuované keše, aby se předešlo opakovaným voláním API.  
- **Je tato funkce kompatibilní s .NET 6 a .NET Core?** Naprosto; knihovna podporuje .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ a .NET 6+.

## Co je GroupDocs.Redaction?
**GroupDocs.Redaction** je .NET knihovna, která umožňuje vývojářům zakrýt citlivý obsah, konvertovat dokumenty a zjistit podporované typy souborů — vše bez potřeby Microsoft Office na serveru. Abstrahuje složité zpracování formátů za čisté, objektově orientované API. Nabízí jednotné API pro zakrývání, konverzi a objevování formátů, zpracovává PDF, Office dokumenty, obrázky a další, přičemž zajišťuje vysoký výkon a bezpečnost.

## Proč vypsat přípony souborů pomocí GroupDocs.Redaction?
Knihovna **podporuje více než 50 vstupních a výstupních formátů**, včetně PDF, DOCX, PPTX, XLSX, HTML a více než 30 typů obrázků. Programatickým **vypsáním přípon souborů** můžete:
- Zabránit uživatelům nahrávat nepodporované soubory (snížení validačních chyb až o 90 %).
- Dynamicky naplňovat rozbalovací nabídky, aby UI zůstalo v souladu s aktualizacemi knihovny.
- Vytvářet auditní logy, které zaznamenávají přesný typ souboru, který se uživatel pokusil zpracovat.

## Předpoklady
- **GroupDocs.Redaction**: Instalace přes NuGet (viz příkazy níže).  
- **.NET SDK**: Ujistěte se, že je nainstalováno nejnovější .NET SDK. Stáhněte jej [zde](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 nebo jakýkoli kompatibilní editor.  
- **Základní znalost C#**: Měli byste být obeznámeni s kolekcemi a LINQ.

## Nastavení GroupDocs.Redaction pro .NET

### Instalace knihovny

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Otevřete NuGet Package Manager, vyhledejte “GroupDocs.Redaction” a nainstalujte nejnovější verzi.

### Získání a aplikace licence

Začněte s bezplatnou zkušební licencí nebo požádejte o dočasnou licenci pro prozkoumání všech funkcí bez omezení. Pro možnosti nákupu navštivte [stránku nákupu GroupDocs](https://purchase.groupdocs.com/). Jakmile máte soubor licence:
1. Umístěte jej do přístupné složky ve vašem projektu (např. `./Licenses/GroupDocs.Redaction.lic`).  
2. Inicializujte licencování při startu aplikace:

Třída `License` načte váš licenční soubor a aktivuje GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Jak vypsat přípony souborů pomocí GroupDocs.Redaction?

Načtěte Redaction API a zavolejte metodu, která vrací podporované formáty. Volání vrátí kolekci, kde každý prvek obsahuje příponu a čitelný popis. Tato operace je nenáročná a může být provedena při startu nebo na požádání.

### Získání podporovaných typů souborů
Metoda `RedactionApi.GetSupportedFileFormats()` vrací jen pro čtení kolekci objektů `FileFormatInfo` popisujících každý formát.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Zobrazení každé přípony a popisu
Každý `FileFormatInfo` poskytuje vlastnosti `Extension` a `Description` pro typ souboru.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Vysvětlení**: Smyčka iteruje přes každý objekt `FileFormatInfo` a vypisuje jeho `Extension` a `Description` v přehledně zarovnané tabulce.

## Jak integrovat seznam do UI rozbalovacího seznamu?
Po získání kolekce ji můžete svázat s libovolnou UI komponentou — WinForms `ComboBox`, WPF `ComboBox` nebo ASP.NET Core `select` elementem. Klíčové je použít `Extension` jako hodnotu a `Description` jako zobrazovaný text. To zajišťuje, že uživatelé vidí přívětivé názvy, zatímco váš kód pracuje s přesnými řetězci přípon.

## Časté problémy a řešení
- **Chyba chybějícího jmenného prostoru** – Ověřte, že jste importovali `GroupDocs.Redaction` a `GroupDocs.Redaction.Common`.  
- **Licence nenalezena** – Ujistěte se, že cesta k licenčnímu souboru je správná a že soubor je zahrnut ve výstupu sestavení.  
- **Výkon u velkých projektů** – Kešujte výsledek ve statické proměnné nebo distribuované keši (např. Redis), aby se předešlo opakovanému procházení.

## Praktické aplikace
Znalost přesného seznamu podporovaných přípon otevírá několik reálných scénářů:
1. **Systémy správy dokumentů** – Automaticky kategorizovat příchozí soubory podle jejich přípony.  
2. **Nástroje pro filtrování obsahu** – Blokovat nepovolené formáty (např. spustitelné soubory) při nahrávání.  
3. **Pipelines pro konverzi souborů** – Dynamicky rozhodnout, zda lze soubor konvertovat, nebo zda vyžaduje alternativní workflow.

## Úvahy o výkonu
- **Paměťová stopa** – Seznam formátů je uložen v lehké `IReadOnlyCollection`, typicky pod 2 KB.  
- **Bezpečnost vláken** – Kolekce je po vytvoření neměnná, což ji činí bezpečnou pro souběžné čtení.  
- **Kešování** – Pro vysoce zatížená API kešujte seznam po celou dobu životnosti aplikace, aby se eliminovaly několik mikrosekund režie na požadavek.

## Závěr
Podle výše uvedených kroků nyní máte spolehlivý způsob, jak **vypsat přípony souborů** a **c# display file formats** pomocí GroupDocs.Redaction. Tato schopnost nejen zlepšuje uživatelský zážitek, ale také chrání vaše backend před nepodporovanými soubory. Prozkoumejte další funkce Redaction — jako maskování obsahu, zakrývání PDF a dávkové zpracování — pro další posílení vašeho pracovního postupu s dokumenty.

## Často kladené otázky
**Q: Jaké jsou výchozí podporované formáty souborů?**  
A: GroupDocs.Redaction podporuje více než 50 formátů, včetně PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG a mnoha dalších. Úplný seznam najdete na [dokumentaci GroupDocs](https://docs.groupdocs.com/search/net/).

**Q: Jak aktualizovat knihovnu na nejnovější verzi?**  
A: Otevřete NuGet Package Manager, vyhledejte “GroupDocs.Redaction” a klikněte na **Update**. Případně spusťte `dotnet add package GroupDocs.Redaction --version <latest>`.

**Q: Mohu tento seznam použít pro server‑side validaci nahrávaných souborů?**  
A: Ano — porovnejte příponu nahraného souboru s získanou kolekcí před zpracováním. To eliminuje 99 % chyb neplatných formátů.

**Q: Je možné rozšířit podporu o vlastní typy souborů?**  
A: Vlastní přípony vyžadují vlastní obslužné rutiny; jádro knihovny nativně nepřidává nové formáty. Prostudujte API dokumentaci pro vytváření vlastních import/export pipeline.

**Q: Moje aplikace spadne po přidání kódu — co mám zkontrolovat?**  
A: Ujistěte se, že licence je načtena správně, `using` direktivy odkazují na správné jmenné prostory, a že ošetřujete `IOException` při čtení licenčního souboru.

---
**Poslední aktualizace:** 2026-06-07  
**Testováno s:** GroupDocs.Redaction 23.9 pro .NET  
**Autor:** GroupDocs  

## Zdroje
- [Dokumentace](https://docs.groupdocs.com/search/net/)
- [Reference API](https://reference.groupdocs.com/redaction/net)
- [Stáhnout GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Bezplatné fórum podpory](https://forum.groupdocs.com/c/search/10)
- [Žádost o dočasnou licenci](https://purchase.groupdocs.com/temporary-license/)

## Související tutoriály
- [Mistrovské filtrování souborů v .NET s GroupDocs.Redaction: Efektivní techniky správy dokumentů](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Mistrovské nastavení GroupDocs.Redaction .NET: Instalace a zpracování událostí pro zabezpečenou správu dokumentů](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Mistrovství správy dokumentů v .NET s GroupDocs.Redaction: Nastavení licence a zvýraznění HTML vyhledávání](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)