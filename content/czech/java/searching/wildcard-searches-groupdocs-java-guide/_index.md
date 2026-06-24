---
date: '2026-03-23'
description: Naučte se, jak přidávat dokumenty do indexu a optimalizovat vyhledávací
  index pomocí GroupDocs.Search pro Javu, což umožňuje výkonné vyhledávání pomocí
  zástupných znaků.
keywords:
- wildcard searches in Java
- text-based wildcard search
- object-based wildcard search
title: Přidání dokumentů do indexu – Vyhledávání pomocí zástupných znaků v Javě
type: docs
url: /cs/java/searching/wildcard-searches-groupdocs-java-guide/
weight: 1
---

# Přidání dokumentů do indexu – Ovládání vyhledávání pomocí zástupných znaků v Javě s GroupDocs.Search

Odemkněte sílu textových a objektových vyhledávání pomocí zástupných znaků pomocí GroupDocs.Search pro Javu. V tomto průvodci se naučíte, jak **add documents to index**, nakonfigurovat pokročilé vzory a udržet váš vyhledávací index optimalizovaný pro rychlé výsledky.

## Rychlé odpovědi
- **Co znamená “add documents to index”?** Vytváří vyhledávatelnou datovou strukturu, kterou může GroupDocs.Search efektivně dotazovat.  
- **Které klíčové slovo zvyšuje výkon?** Používání stručných vzorů se zástupnými znaky a pravidelné operace **optimize search index**.  
- **Potřebuji speciální nastavení paměti?** Ano — monitorujte **java search memory management**, abyste se vyhnuli chybám out‑of‑memory u velkých datových sad.  
- **Mohu tyto funkce použít v aplikaci Spring Boot?** Rozhodně; stačí zahrnout Maven závislost a nakonfigurovat složku indexu.  
- **Je pro produkci vyžadována licence?** Platná licence GroupDocs.Search je nutná pro komerční nasazení.

## Co je “add documents to index” v GroupDocs.Search?
Přidání dokumentů do indexu znamená vložit vaše zdrojové soubory (PDF, DOCX, TXT atd.) do vyhledávatelného úložiště, které GroupDocs.Search vytváří v pozadí. Po indexování můžete spouštět rychlé dotazy se zástupnými znaky, aniž byste pokaždé prohledávali původní soubory.

## Proč používat vyhledávání se zástupnými znaky s GroupDocs.Search?
Vyhledávání se zástupnými znaky vám umožňuje najít částečná slova nebo vzory — ideální pro situace, kdy uživatelé pamatují jen fragmenty výrazu. Tato flexibilita zlepšuje uživatelský zážitek v systémech pro správu dokumentů, obsahových portálech a nástrojích pro data‑mining.

## Předpoklady
- **Java Development Kit (JDK)** — verze 8 nebo novější.  
- Základní znalosti programování v Javě.  
- IDE, například IntelliJ IDEA nebo Eclipse.  
- Maven pro správu závislostí (nebo můžete JAR stáhnout přímo).  

## Nastavení GroupDocs.Search pro Javu

### Maven Setup
Přidejte repozitář a závislost do souboru `pom.xml`:

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
Pokud raději nepoužíváte Maven, stáhněte nejnovější JAR z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
- **Free Trial:** Prozkoumejte základní funkce zdarma.  
- **Temporary License:** Aktivujte pokročilé funkce během hodnocení.  
- **Purchase:** Získejte komerční licenci pro produkční použití.

## Průvodce implementací

### Funkce 1: Textové vyhledávání se zástupnými znaky

#### Krok 1 — Nastavte index a **add documents to index**
Nejprve vytvořte složku indexu a přidejte své zdrojové dokumenty:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\AdvancedUsage\\Searching\\WildcardSearch\\QueryInTextForm";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

Index index = new Index(indexFolder);
index.add(documentsFolder);
```

#### Krok 2 — Proveďte dotazy se zástupnými znaky
Spusťte vyhledávání založené na vzoru přímo na textu:

```java
// Search for words matching 'm???is'
String query1 = "m???is";
SearchResult result1 = index.search(query1); // Finds words like 'mauris', 'mollis'

// Search for words matching 'pri?(1~7)'
String query2 = "pri?(1~7)";
SearchResult result2 = index.search(query2); // Finds words like 'private', 'principles'
```

**Vysvětlení**  
- `indexFolder` ukládá vyhledávatelný index na disku.  
- `documentsFolder` ukazuje na umístění souborů, které chcete **add documents to index**.  
- `search()` provádí dotaz se zástupnými znaky a vrací odpovídající výsledky.

### Funkce 2: Objektové vyhledávání se zástupnými znaky

#### Krok 1 — Nastavte index (stejně jako předtím)
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\AdvancedUsage\\Searching\\WildcardSearch\\QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

#### Krok 2 — Vytvořte `WordPattern` pro složité dotazy
Objektové vyhledávání vám poskytuje jemnozrnnou kontrolu nad každým prvkem vzoru:

```java
// Create a WordPattern for 'm???is'
WordPattern pattern1 = new WordPattern();
pattern1.appendString("m");
pattern1.appendOneCharacterWildcard();
pattern1.appendOneCharacterWildcard();
pattern1.appendOneCharacterWildcard();
pattern1.appendString("is");

SearchQuery query1 = SearchQuery.createWordPatternQuery(pattern1);
SearchResult result1 = index.search(query1); // Finds words like 'mauris', 'mollis'

// Create a WordPattern for 'pri?(1~7)'
WordPattern pattern2 = new WordPattern();
pattern2.appendString("pri");
pattern2.appendWildcard(1, 7);

SearchQuery query2 = SearchQuery.createWordPatternQuery(pattern2);
SearchResult result2 = index.search(query2); // Finds words like 'private', 'principles'
```

**Vysvětlení**  
- `WordPattern` vám umožňuje sestavit vyhledávací vzor krok za krokem.  
- `appendOneCharacterWildcard()` přidává zástupný znak `?`.  
- `appendWildcard(min, max)` přidává zástupný znak založený na rozsahu (`?(min~max)`).  

## Praktické aplikace
1. **Document Management:** Rychle najděte soubory, když je znám jen část výrazu.  
2. **Content Retrieval Engines:** Pohánějte vyhledávací lišty v CMS platformách s flexibilním porovnáváním.  
3. **Data Mining:** Extrahujte vzorovaná data z velkých korpusů bez úplných textových skenů.

## Úvahy o výkonu

### Optimalizace vyhledávacího indexu
- **Regular Re‑indexing:** Po hromadných aktualizacích znovu vytvořte index, aby byly časy vyhledávání nízké.  
- **Compact Storage:** Použijte `index.optimize()` (pokud je k dispozici) ke zmenšení velikosti indexu.

### Správa paměti pro Java Search
- **Heap Size:** Přidělte dostatečnou haldu (`-Xmx2g` nebo vyšší) pro velké sady dokumentů.  
- **Streaming Indexing:** Zpracovávejte soubory po dávkách, abyste se vyhnuli načtení všeho najednou do paměti.

### Obecné osvědčené postupy
- Udržujte vzory se zástupnými znaky co nejkonkrétnější; příliš obecné vzory zvyšují zátěž CPU.  
- Sledujte přestávky GC, pokud zaznamenáte špičky latence během těžkých vyhledávacích úloh.

## Závěr
Naučíte-li se, jak **add documents to index** a využít jak textové, tak objektové dotazy se zástupnými znaky, můžete výrazně zlepšit vyhledávací zážitek v jakékoli Java aplikaci. Nezapomeňte pravidelně **optimize search index** a rozumně spravovat paměť pro škálovatelný výkon. Experimentujte s různými vzory, integrujte kód do svých služeb a užijte si dnes rychlé a flexibilní výsledky vyhledávání!

## Často kladené otázky

**Q1: Co je vyhledávání se zástupnými znaky?**  
A: Vyhledávání se zástupnými znaky vám umožňuje najít slova nebo fráze pomocí zástupných znaků jako `?` (jedna znak) nebo `*` (více znaků).

**Q2: Jak nainstaluji GroupDocs.Search pro Javu?**  
A: Použijte Maven s repozitářem a závislostí uvedenou výše, nebo stáhněte JAR přímo z oficiální stránky vydání.

**Q3: Dokážou vyhledávání se zástupnými znaky pracovat s velkými datovými sadami?**  
A: Ano, ale měli byste **optimize search index** a sledovat **java search memory management**, aby byl zachován výkon.

**Q4: Jaké jsou běžné úskalí?**  
A: Nesprávné cesty k indexu, používání příliš obecných zástupných znaků a zanedbání konfigurace paměti mohou způsobit pomalé vyhledávání nebo chyby out‑of‑memory.

**Q5: Kde najdu další zdroje?**  
A: Navštivte [GroupDocs documentation](https://docs.groupdocs.com/search/java/) pro podrobné průvodce a reference API.

## Zdroje

- **Documentation:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Reference:** [GroupDocs Search API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [GroupDocs.Search Downloads](https://releases.groupdocs.com/search/java/)
- **GitHub:** [GroupDocs.Search on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free Support:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**Poslední aktualizace:** 2026-03-23  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

---