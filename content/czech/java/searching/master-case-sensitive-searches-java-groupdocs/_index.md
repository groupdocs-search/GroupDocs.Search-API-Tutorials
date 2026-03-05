---
date: '2026-02-06'
description: Naučte se, jak přidávat dokumenty do indexu a povolit rozlišování velkých
  a malých písmen při vyhledávání v Javě s GroupDocs.Search, čímž zvýšíte přesnost
  své aplikace.
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 'Přidat dokumenty do indexu: rozlišující velká a malá písmena při vyhledávání
  v Javě s GroupDocs'
type: docs
url: /cs/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Přidání dokumentů do indexu: Ovládání vyhledávání rozlišujícího velikost písmen v Javě s GroupDocs

Získání správného kusu informace z obrovské kolekce dokumentů je základní požadavek moderních aplikací. V tomto průvodci se naučíte **jak přidat dokumenty do indexu** a provádět **vyhledávání rozlišující velikost písmen** pomocí GroupDocs.Search pro Javu. Ať už budujete úložiště právních dokumentů, katalog e‑commerce nebo systém pro správu obsahu, přesné výsledky vyhledávání udržují uživatele spokojené a vaše data důvěryhodná.

## Rychlé odpovědi
- **Jaký je hlavní krok pro zahájení vyhledávání?** Přidejte dokumenty do indexu pomocí `index.add(...)`.
- **Jak povolit vyhledávání rozlišující velikost písmen?** Nastavte `options.setUseCaseSensitiveSearch(true)`.
- **Mohu vyhledávat napříč více adresáři?** Ano – zavolejte `index.add()` pro každý složku, kterou chcete zahrnout.
- **Která metoda mi umožní vyhledávat pomocí objektů?** Použijte `SearchQuery.createWordQuery(...)`.
- **Potřebuji licenci pro testování?** Dočasná licence je k dispozici pro zkušební účely.

## Co znamená „přidat dokumenty do indexu“?
Přidání dokumentů do indexu znamená vložit vaše zdrojové soubory (PDF, Word, prostý text atd.) do GroupDocs.Search, aby mohl vytvořit prohledávatelnou datovou strukturu. Po indexaci může engine provádět rychlé dotazy, včetně těch rozlišujících velikost písmen.

## Proč povolit vyhledávání rozlišující velikost písmen v Javě?
- **Přesná shoda termínu** – rozlište „Apple“ (společnost) od „apple“ (ovoce).  
- **Regulační shoda** – některá odvětví vyžadují přesnou shodu frází.  
- **Zlepšená relevance** – uživatelé často očekávají výsledky specifické pro velikost písmen v technických nebo právních kontextech.

## Předpoklady
- JDK (doporučeno Java 17 nebo novější)  
- Maven pro správu závislostí  
- IDE jako IntelliJ IDEA nebo Eclipse  
- Základní znalost programování v Javě  

## Nastavení GroupDocs.Search pro Javu
Nejprve přidejte repozitář GroupDocs a závislost do vašeho `pom.xml`:

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

Alternativně můžete stáhnout nejnovější verzi přímo z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licencování
Pro zahájení zkušebního období navštivte GroupDocs a získejte dočasnou licenci. To vám umožní otestovat všechny funkce bez jakýchkoli omezení.

## Jak přidat dokumenty do indexu – Vyhledávání textových dotazů

### Krok 1: Vytvořte index a přidejte své dokumenty
Vytvořte složku, kde budou uloženy soubory indexu, a poté přidejte zdrojový adresář, který obsahuje dokumenty, jež chcete prohledávat.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Tip:** Můžete volat `index.add()` vícekrát, abyste **vyhledávali napříč více adresáři** v jediném indexu.

### Krok 2: Povolit vyhledávání rozlišující velikost písmen
Nastavte možnosti vyhledávání tak, aby respektovaly velikost písmen.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Krok 3: Proveďte vyhledávání rozlišující velikost písmen v textovém dotazu
Spusťte dotaz, který rozliší „Advantages“ od „advantages“.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Smyčka vypíše úplnou cestu každého dokumentu, který obsahuje přesně shodný termín s požadovanou velikostí písmen.

## Jak přidat dokumenty do indexu – Vyhledávání objektových dotazů

Objektové dotazy vám poskytují větší flexibilitu, zejména když potřebujete kombinovat více kritérií.

### Krok 1: Inicializujte druhý index (volitelné)
Pokud chcete objektové vyhledávání oddělit, vytvořte další složku pro index.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Krok 2: Znovu použijte možnost rozlišující velikost písmen
Stejná instance `SearchOptions` funguje i pro objektové dotazy.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Krok 3: Sestavte a spusťte objektový dotaz
Vytvořte objekt dotazu na slovo a předávejte jej vyhledávacímu enginu.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Použití `createWordQuery` vám později umožní kombinovat jej s frázovými, zástupnými nebo Boolean dotazy pro složitější scénáře.

## Praktické aplikace
- **Správa právních dokumentů:** Vyhledávejte konkrétní zákony, kde záleží na kapitalizaci.  
- **Platformy e‑commerce:** Rozlišujte SKU produktů jako „PRO‑X“ vs. „pro‑x“.  
- **Systémy pro správu obsahu (CMS):** Zajistěte, aby autoři našli přesné nadpisy nebo štítky.

## Úvahy o výkonu
- **Udržujte index aktuální** – reindexujte, když jsou přidány nové soubory nebo se existující změní.  
- **Sledujte využití paměti** – velké korpusy těží z inkrementálního indexování a správného nastavení velikosti haldy JVM.  
- **Využijte garbage collector Javy** – uvolněte objekty `Index`, když již nejsou potřeba.

## Časté problémy a řešení
| Problém | Řešení |
|-------|----------|
| `useCaseSensitiveSearch` se zdá být ignorováno | Ověřte, že používáte nejnovější verzi GroupDocs.Search a že byl index znovu vytvořen po změně této volby. |
| Žádné výsledky pro známý termín | Ujistěte se, že velikost písmen termínu přesně odpovídá a že dokument byl úspěšně přidán do indexu. |
| Vyhledávání v mnoha složkách zpomaluje | Přidejte každou složku samostatně pomocí `index.add()` a zvažte rozdělení indexu na shardy pro velmi velké datové sady. |

## Často kladené otázky

**Q:** Jak zacházet s velkými datovými sadami pomocí GroupDocs.Search?  
**A:** Využijte rozdělení indexu, optimalizujte nastavení paměti JVM a pravidelně kompaktně index, aby byl výkon optimální.

**Q:** Můžu vyhledávat napříč více adresáři současně?  
**A:** Ano – zavolejte `index.add()` pro každý adresář, který chcete zahrnout, a poté spusťte jediný dotaz proti sloučenému indexu.

**Q:** Jaké jsou běžné úskalí při nastavování vyhledávání rozlišujícího velikost písmen?  
**A:** Zapomenutí znovu vytvořit index po povolení `useCaseSensitiveSearch` nebo použití nesprávné velikosti písmen v řetězci dotazu.

**Q:** Jak mohu řešit chyby vyhledávání?  
**A:** Zkontrolujte logovací soubory generované GroupDocs.Search pro stack trace a potvrďte, že všechny Maven závislosti jsou správně vyřešeny.

**Q:** Je GroupDocs.Search vhodný pro aplikace v reálném čase?  
**A:** S vhodnými strategiemi indexování (inkrementální aktualizace a in‑memory cache) může poskytovat téměř real‑time výsledky vyhledávání.

## Zdroje
- **Dokumentace:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **API Reference:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Stáhnout:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **GitHub Repository:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Support Forum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Dočasná licence:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2026-02-06  
**Testováno s:** GroupDocs.Search 25.4  
**Autor:** GroupDocs  

---