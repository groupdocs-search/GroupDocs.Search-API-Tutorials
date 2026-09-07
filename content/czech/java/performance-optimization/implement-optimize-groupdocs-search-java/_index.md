---
date: '2026-07-07'
description: Naučte se, jak smazat index, provádět full text search Java a optimalizovat
  search performance pomocí GroupDocs.Search for Java. Podrobný návod krok za krokem
  s nastavením network a indexováním.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: Jak smazat index a provádět full text search Java pomocí GroupDocs.Search.
  Postupujte podle tohoto návodu k nastavení search network, vytvoření searchable
  index a optimalizaci search performance.
og_title: Jak smazat index a provádět textové vyhledávání pomocí GroupDocs.Search
  for Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: Jak smazat index a provádět textové vyhledávání pomocí GroupDocs.Search for
  Java
type: docs
url: /cs/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Jak odstranit index a provádět textové vyhledávání pomocí GroupDocs.Search pro Java

V dnešním datově řízeném světě je **jak odstranit index** rychle a zároveň poskytovat bleskově rychlé full‑textové vyhledávání v Javě konkurenční výhodou. Ať už budujete interní znalostní bázi, úložiště právních případů nebo katalog produktů pro e‑commerce, dobře vyladěná vyhledávací síť může výrazně zlepšit spokojenost uživatelů. V tomto průvodci se naučíte, jak **nastavit vyhledávací síť**, **vytvořit prohledávatelný index**, **optimalizovat výkon vyhledávání** a **odstranit dokumenty z indexu**, když je to potřeba — vše pomocí GroupDocs.Search pro Java.

## Rychlé odpovědi
- **Jaký je hlavní účel GroupDocs.Search pro Java?** Poskytuje full‑textové vyhledávání napříč více než 50 formáty dokumentů, což umožňuje rychlé vyhledávání klíčových slov.  
- **Jak provádět textové vyhledávání v distribuovaném prostředí?** Nasadíte vyhledávací síť, indexujete dokumenty na hlavním uzlu a poté dotazujete libovolný uzel.  
- **Mohu odstranit dokumenty z indexu bez jeho přestavby?** Ano, použijte Delete API k odstranění vybraných souborů, čímž efektivně *jak odstranit index* bez úplného přeindexování.  
- **Jaká verze Javy je vyžadována?** JDK 8 nebo vyšší.  
- **Je pro produkci potřeba licence?** Je vyžadována platná licence GroupDocs.Search; k dispozici je bezplatná zkušební verze.

## Co je „perform text search“?
Provádění textového vyhledávání znamená dotazování full‑textového indexu za účelem získání dokumentů, které obsahují zadaná klíčová slova nebo fráze. GroupDocs.Search vytváří invertovaný index, který umožňuje tyto vyhledávání provádět extrémně rychle, i při tisících souborů.

## Proč nastavit vyhledávací síť?
Vyhledávací síť rozděluje zátěž indexování a dotazování mezi více uzlů, což vám umožní **optimalizovat výkon vyhledávání**, horizontálně škálovat a udržovat vysokou dostupnost. Tato architektura je ideální pro podnikové úložiště dokumentů, kde jsou důležité latence a propustnost.

## Jak implementovat a optimalizovat vyhledávací síť pomocí GroupDocs.Search pro Java
Načtěte svou konfiguraci, spusťte hlavní uzel a poté přidejte pracovní uzly, které sdílejí stejnou základní cestu a port. Nasazením sítě tímto způsobem umožníte libovolnému uzlu zpracovávat požadavky na indexování nebo dotazy, což poskytuje konzistentní časy odezvy i při růstu počtu dokumentů na stovky tisíc.

### Přehled krok za krokem
1. **Definovat základní konfiguraci**, která zahrnuje sdílený adresář a TCP port.  
2. **Spustit hlavní uzel**, který spravuje index a koordinuje pracovní uzly.  
3. **Přidat pracovní uzly**, které se připojují k hlavnímu uzlu, což umožňuje paralelní indexování a vyhledávání.  
4. **Monitorovat využití zdrojů** a ladit nastavení haldy JVM, aby byla latence nízká.

## Jak odstranit index v GroupDocs.Search pro Java
`SearchNode` představuje uzel v síti GroupDocs.Search, který spravuje operace indexování a dotazování. Metoda `delete` odstraňuje zadané dokumenty z indexu.

### Přímé kroky pro odstranění
- Zavolejte metodu `delete` na instanci `SearchNode`.  
- Poskytněte pole relativních cest k souborům.  
- Proveďte commit změn; index je okamžitě aktualizován a následná vyhledávání již nevracejí odstraněné soubory.

## Co je vyhledávací síť?
**Vyhledávací síť** je klastr propojených uzlů, které sdílejí společné úložiště indexu, což umožňuje distribuované indexování a provádění dotazů. Umožňuje horizontální škálování a odolnost vůči chybám pro rozsáhlé kolekce dokumentů.

## Jak vytvořit prohledávatelný index (index documents java)
Metoda `add` indexuje dokument do vyhledávacího indexu. Přidejte dokumenty do hlavního uzlu pomocí metody `add`; síť rozšíří změny na všechny pracovní uzly. Tento přístup zajišťuje, že každý uzel může obsluhovat dotazy vůči nejnovějšímu indexu bez dalších kroků synchronizace.

### Klíčové akce
- Nastavte hlavní uzel na složku obsahující zdrojové soubory.  
- Zavolejte rutinu indexování; síť zpracuje každý soubor a aktualizuje invertovaný index.  
- Ověřte, že soubory indexu se objevují v určeném úložném adresáři.

## Jak odstranit indexované soubory (remove indexed files)
Když se dokument stane zastaralým, zavolejte API `delete` s jeho cestou. Systém odstraní záznamy souboru z invertovaného indexu, uvolní úložiště a zabrání zastaralým výsledkům.

## Nastavení GroupDocs.Search pro Java
Pro začátek integrujte GroupDocs.Search do svého Java projektu pomocí následujícího nastavení:

### Maven nastavení
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
Alternativně můžete [stáhnout nejnovější verzi přímo od GroupDocs](https://releases.groupdocs.com/search/java/).

### Získání licence
GroupDocs nabízí bezplatnou zkušební verzi, která vám umožní vyzkoušet funkce před nákupem. Dočasnou licenci můžete získat podle kroků na jejich [stránce nákupu](https://purchase.groupdocs.com/temporary-license/). To vám během testovací fáze umožní plnou funkčnost.

### Základní inicializace a nastavení
Inicializujte GroupDocs.Search ve své Java aplikaci pomocí:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## Průvodce implementací

### Konfigurace vyhledávací sítě
**Přehled:** Nastavte základní cestu a port pro vaši vyhledávací síť, což umožní uzlům efektivně komunikovat.

#### Krok 1: Definovat základní konfiguraci
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parametry:**  
  - `basePath`: Cesta k adresáři pro operace sítě.  
  - `basePort`: Číslo portu používaného vyhledávací sítí.

#### Krok 2: Odstraňování potíží
Ujistěte se, že zvolený port není blokován nastavením firewallu ani používán jinou aplikací. Podle potřeby jej upravte, aby nedocházelo ke konfliktům.

### Nasazení uzlů vyhledávací sítě
**Přehled:** Pomocí vaší konfigurace nasadíte uzly po celé síti pro distribuované indexování a vyhledávání.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Klíčové konfigurační možnosti:**  
  - **Base Path & Port:** Tyto hodnoty by měly odpovídat těm, které byly použity v počáteční konfiguraci, aby byla zajištěna konzistence.

### Indexování dokumentů (`create searchable index`)
**Přehled:** Efektivně přidávejte dokumenty do vyhledávacího indexu pomocí hlavního uzlu.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Účel:**  
  - `masterNode`: Primární uzel spravující indexování dokumentů.  
  - `documentsPath`: Cesta k adresáři obsahujícímu dokumenty.

#### Tipy pro odstraňování potíží
Ověřte, že cesty k dokumentům jsou správné a přístupné. Ujistěte se, že oprávnění umožňují čtení z těchto adresářů.

### Vyhledávání textu v síti (`perform text search`)
**Přehled:** Provádějte komplexní textové vyhledávání napříč vaším indexovaným sítí.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parametry:**  
  - `query`: Text, který hledáte.  
  - `masterNode`: Uzlu provádějícímu vyhledávání.

### Odstraňování dokumentů z indexu (`delete documents index`)
**Přehled:** Odstraňte konkrétní dokumenty z indexu pomocí jejich cest k souborům.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Účel metody:**  
  - `node`: Cílový uzel pro operace odstraňování.  
  - `filePaths`: Cesty k dokumentům, které mají být z indexu odstraněny.

#### Odstraňování potíží
Ujistěte se, že cesty k souborům jsou přesné a že soubory existují ve vašem adresáři. Pokud problémy přetrvávají, zkontrolujte oprávnění a konektivitu sítě.

## Praktické aplikace
1. **Enterprise Document Management:** Zefektivněte interní vyhledávání znalostí.  
2. **Legal Case Analysis:** Rychle najděte relevantní soubory případů napříč více úložišti.  
3. **E‑commerce Platforms:** Zvyšte rychlost vyhledávání produktů indexováním popisů a recenzí.  
4. **Academic Research:** Efektivně prohledejte velké digitální knihovny článků a diplomových prací.  
5. **Customer Support Systems:** Snižte dobu odezvy tím, že umožníte operátorům okamžitě prohledávat staré tickety.

## Úvahy o výkonu
- **Optimalizovat rychlost indexování:** Přidávejte nové dokumenty inkrementálně během mimošpičkových hodin, aby byla latence nízká.  
- **Pokyny pro využití zdrojů:** Monitorujte CPU a paměť, zejména při škálování počtu uzlů.  
- **Správa paměti v Javě:** Laděte nastavení haldy JVM podle zatížení (např. `-Xmx2g` pro středně velké indexy).

## Závěr
Podle tohoto průvodce jste se naučili, jak **nastavit vyhledávací síť**, **vytvořit prohledávatelný index**, **provádět textové vyhledávání** a **odstraňovat dokumenty z indexu** pomocí GroupDocs.Search pro Java. Tyto možnosti umožňují rychlé a spolehlivé získávání dokumentů v distribuovaných prostředích.

**Další kroky**
- Experimentujte s různými konfiguracemi uzlů, abyste našli optimální rovnováhu pro své zatížení.  
- Prozkoumejte podrobněji pokročilé možnosti indexování, jako jsou vlastní analyzátory a ladění relevance.  
- Prozkoumejte integraci s dalšími produkty GroupDocs pro kompletní zpracování dokumentů.

## Často kladené otázky

**Q: Jaký je hlavní případ použití GroupDocs.Search pro Java?**  
A: Poskytuje full‑textové vyhledávání napříč mnoha formáty dokumentů, což vám umožní **provádět textové vyhledávání** ve velkých úložištích.

**Q: Jak mohu zlepšit rychlost vyhledávání ve velké síti?**  
A: Nasadíte další uzly, ladíte haldu JVM a naplánujete indexování během období nízkého provozu, abyste **optimalizovali výkon vyhledávání**.

**Q: Je možné odstranit jediný dokument bez přeindexování celé kolekce?**  
A: Ano, použijte API **delete documents index**, jak je ukázáno v příkladu kódu, k odstranění konkrétních souborů.

**Q: Potřebuji licenci pro vývoj?**  
A: Bezplatná zkušební licence stačí pro testování; pro produkční nasazení je vyžadována komerční licence.

**Q: Mohu indexovat PDF, Word soubory a e‑maily společně?**  
A: Rozhodně — GroupDocs.Search podporuje širokou škálu formátů přímo z krabice.

**Poslední aktualizace:** 2026-07-07  
**Testováno s:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs

## Související tutoriály

- [Jak indexovat text v Javě s průvodcem GroupDocs.Search](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [Optimalizace výkonu vyhledávání pomocí pokročilých technik indexování v GroupDocs.Search pro Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [Zlepšení výkonu dotazů s GroupDocs.Search Java: optimalizace indexu a vyhledávání](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)