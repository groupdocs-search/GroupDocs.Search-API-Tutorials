---
date: '2026-05-12'
description: '...'
keywords:
- java full text search
- document management java
- GroupDocs.Search merging
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: 'Learn java full text search with GroupDocs.Search: add documents to
    index, configure merge options, and cancel merge operation. Ideal for document
    management java solutions.'
  headline: java full text search – add docs & merge with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It tells GroupDocs.Search to scan a folder, extract searchable tokens,
      and store metadata for each file.
    question: What does “add documents to index” mean?
  - answer: Yes—use the `Cancellation` object to abort a merge after a configurable
      timeout.
    question: Can I stop a long merge?
  - answer: A free trial or temporary license works for testing; a commercial license
      unlocks full features.
    question: Do I need a license?
  - answer: JDK 8 or newer.
    question: Which Java version is required?
  - answer: Absolutely—GroupDocs.Search can handle multi‑hundred‑page documents with
      incremental indexing.
    question: Is this suitable for large datasets?
  type: FAQPage
title: '...'
type: docs
url: /cs/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# java full text search – přidat dokumenty a sloučit s GroupDocs.Search

V moderních podnikovém prostředích je **java full text search** páteří každého robustního systému pro správu dokumentů v Javě. Ať už potřebujete indexovat smlouvy, faktury nebo interní zprávy, dobře navržený index vám umožní získat správné informace během milisekund. Tento tutoriál vás provede vytvořením indexu, přidáním dokumentů, konfigurací možností sloučení a bezpečným zrušením operace sloučení – vše pomocí GroupDocs.Search pro Javu.

## Rychlé odpovědi
- **Co znamená „add documents to index“?** Říká GroupDocs.Search, aby prohledal složku, extrahoval vyhledávatelné tokeny a uložil metadata pro každý soubor.  
- **Mohu zastavit dlouhé sloučení?** Ano – použijte objekt `Cancellation` k přerušení sloučení po nastavitelném časovém limitu.  
- **Potřebuji licenci?** Pro testování stačí bezplatná zkušební nebo dočasná licence; komerční licence odemkne všechny funkce.  
- **Jaká verze Javy je vyžadována?** JDK 8 nebo novější.  
- **Je to vhodné pro velké datové sady?** Rozhodně – GroupDocs.Search zvládne dokumenty o stovkách stránek s inkrementálním indexováním.

## Co znamená „add documents to index“ v GroupDocs.Search?
**Přidání dokumentů do indexu znamená vložit kolekci souborů do GroupDocs.Search, aby knihovna mohla analyzovat jejich obsah, extrahovat tokeny a vytvořit vyhledávatelnou datovou strukturu.** Proces vytvoří kompaktní reprezentaci, která umožňuje bleskově rychlé full‑textové dotazy napříč všemi indexovanými soubory.

## Proč použít GroupDocs.Search pro správu dokumentů v Javě?
GroupDocs.Search poskytuje **škálovatelné indexování pro více než 50 vstupních formátů** (PDF, DOCX, XLSX, PPTX, HTML, obrázky atd.) a dokáže zpracovat **dokumenty až do 2 GB bez načítání celého souboru do paměti**. Jeho API vám dává detailní kontrolu nad indexováním, sloučením a zrušením, což z něj činí špičkovou volbu pro enterprise‑úroveň řešení java full text search.

## Požadavky
- **GroupDocs.Search for Java** verze 25.4 nebo novější.  
- Maven (nebo ruční stažení JAR).  
- Základní znalost Javy a prostředí JDK 8+.

## Nastavení GroupDocs.Search pro Javu

### Instalace pomocí Maven
Pokud spravujete závislosti pomocí Maven, přidejte úložiště a závislost do vašeho `pom.xml`:

```xml
<repositories>
    <repository>
        <id>repository.groupdocs.com</id>
        <name>GroupDocs Repository</name>
        <url>https://releases.groupdocs.com/search/java/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>com.groupdocs</groupId>
        <artifactId>groupdocs-search</artifactId>
        <version>25.4</version>
    </dependency>
</dependencies>
```

### Přímé stažení
Alternativně stáhněte nejnovější JAR z oficiální stránky: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
- **Free Trial:** Zaregistrujte se na webu GroupDocs a získejte zkušební licenci.  
- **Temporary License:** Požádejte o dočasný klíč, pokud potřebujete prodloužené hodnocení.  
- **Commercial License:** Zakupte pro produkční použití.

Po získání souboru licence jej umístěte do projektu a inicializujte knihovnu, jak je ukázáno níže.

## Praktický návod

### Jak přidat dokumenty do indexu – vytvoření prvního indexu
**Načtěte nebo vytvořte prázdný index vytvořením instance třídy `Index`, která představuje vyhledávatelný kontejner na disku.** Tento krok připraví úložné místo pro všechny tokeny, které budou z vašich dokumentů vygenerovány.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **Proč:** Tento krok nastaví úložný kontejner, kde budou uloženy indexované tokeny.

#### Přidání dokumentů do indexu
**Zavolejte `index.add` s cestou ke složce; metoda prohledá každý soubor, extrahuje text a uloží vyhledávatelná metadata do indexu.** Operace probíhá v jednom průchodu a respektuje nastavený `IndexSettings`.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **Proč:** Knihovna načte každý soubor, extrahuje text a uloží jej do `index1`.

### Vytvoření druhého indexu pro flexibilní pracovní postupy
**Vytvořte další objekt `Index`, který bude obsahovat samostatnou sadu dokumentů, což umožňuje izolované zpracování před sloučením.** Tento vzor je užitečný pro multi‑tenant scénáře nebo etapové indexování.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Proč:** Více indexů vám umožní spravovat odlišné sady dokumentů a později je sloučit.

### Jak nakonfigurovat možnosti sloučení a zrušit operaci sloučení
**Vytvořte instanci `MergeOptions`, nastavte požadované parametry a připojte token `Cancellation`, který přeruší sloučení po zadaném časovém limitu.** To vám poskytuje plnou kontrolu nad využitím zdrojů během velkých sloučení.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **Proč:** `Cancellation` vám dává možnost **automaticky zrušit operaci sloučení**, čímž zabraňuje nekontrolovatelným úlohám.

### Sloučení indexů
**Zavolejte `index1.merge(index2, mergeOptions)`; primární index absorbuje všechny dokumenty ze sekundárního indexu při zachování integrity tokenů.** Po sloučení máte jednotné vyhledávatelné úložiště.

```java
index1.merge(index2, options);
```

- **Proč:** Po tomto volání `index1` obsahuje všechny dokumenty z obou zdrojů, což vám poskytuje jednotný vyhledávací zážitek.

## Praktické aplikace pro správu dokumentů v Javě
- **Legal firms:** Konsolidujte spisové soubory z více kanceláří do jednoho vyhledávatelného indexu.  
- **Financial institutions:** Sloučte čtvrtletní zprávy do jednotného úložiště pro rychlé auditní dotazy.  
- **Enterprises:** Kombinujte HR politiky, manuály pro soulad a interní příručky pro podnikovou vyhledávací funkci.

## Úvahy o výkonu
- **Incremental indexing:** Přidávejte nové soubory periodicky místo přestavování celého indexu.  
- **Memory monitoring:** Velké dávky mohou spotřebovat RAM; zpracovávejte soubory v menších částech nebo povolte režim streamování.  
- **Garbage collection:** Uvolněte nepoužívané objekty `Index` okamžitě, aby se uvolnily zdroje.  
- **SSD storage:** Ukládání souborů indexu na SSD může zvýšit rychlost sloučení až 2×.

## Časté problémy a řešení

| Problém | Řešení |
|---------|--------|
| **Nesprávná cesta ke složce** | Ověřte absolutní cestu a zajistěte, aby aplikace měla oprávnění ke čtení. |
| **Nedostatečná paměť** | Zvyšte haldu JVM (`-Xmx`) nebo indexujte soubory po dávkách. |
| **Zrušení nebylo spuštěno** | Ujistěte se, že `cancelAfter` je nastaveno před voláním `merge`. |
| **Není podporovaný formát souboru** | V případě potřeby nainstalujte další pluginy formátů od GroupDocs. |

## Často kladené otázky

**Q:** *Proč bych měl vytvořit více indexů místo jednoho?*  
**A:** Samostatné indexy vám umožní izolovat datové domény, aplikovat odlišné bezpečnostní politiky a sloučit je jen když je potřeba, což zlepšuje výkon a organizaci.

**Q:** *Mohu zrušit operaci indexování stejným způsobem jako zrušení sloučení?*  
**A:** Ano – použijte objekt `Cancellation` s metodou `add` k zastavení dlouho běžících úloh indexování.

**Q:** *Jak zajistit optimální výkon při velmi velkých kolekcích dokumentů?*  
**A:** Provádějte inkrementální indexování, monitorujte paměť JVM a ukládejte index na SSD. Zvažte použití nastavení `BatchSize` k omezení počtu dokumentů v paměti.

**Q:** *Co mám dělat, pokud obdržím chybu „Access denied“?*  
**A:** Zkontrolujte oprávnění ke složce pro uživatele, který spouští proces Java, a ujistěte se, že soubor licence je čitelný.

**Q:** *Je GroupDocs.Search kompatibilní s ostatními knihovnami GroupDocs?*  
**A:** Rozhodně – můžete jej integrovat s GroupDocs.Viewer, GroupDocs.Conversion a dalšími pro vytvoření kompletního dokumentového řešení.

## Závěr
Po přečtení tohoto návodu nyní víte, jak **přidat dokumenty do indexu**, nakonfigurovat chování sloučení a bezpečně **zrušit operaci sloučení**, pokud je to potřeba – vše v rámci robustního workflow **java full text search**. Experimentujte s většími datovými sadami, prozkoumejte vlastní tokenizéry nebo kombinujte GroupDocs.Search s ostatními produkty GroupDocs pro vytvoření enterprise‑úrovňového řešení.

**Zdroje**
- **Dokumentace:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **Reference API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Stáhnout:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **Repozitář na GitHubu:** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Bezplatné fórum podpory:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Žádost o dočasnou licenci:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**Last Updated:** 2026-05-12  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Související tutoriály

- [Jak přidat dokumenty do indexu s metadatovým indexováním v Javě pomocí GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Přidat dokumenty do indexu a zakázat stop slova v GroupDocs.Search Java pro vyšší přesnost vyhledávání](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)
- [Přidat dokumenty do indexu – tutoriály GroupDocs.Search Java](/search/java/document-management/)