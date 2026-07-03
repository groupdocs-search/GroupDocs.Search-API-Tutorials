---
date: '2026-02-21'
description: Naučte se, jak přidávat dokumenty do indexu a zvyšovat výkonnost vyhledávání
  pomocí chunk‑based vyhledávání v Javě s využitím GroupDocs.Search, optimalizovat
  paměť vyhledávacího indexu v Javě pro velké sady dokumentů.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Přidat dokumenty do indexu s vyhledáváním po částech v Javě
type: docs
url: /cs/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

"

Proceed.

I'll translate.

Also note "step-by-step in order - do not skip sections". Provide full translation.

Let's craft.

# Přidání dokumentů do indexu s vyhledáváním po částech v Javě

V moderních aplikacích, které potřebují **rychle přidávat dokumenty do indexu** a poté provádět rychlé dotazy po částech, chcete řešení, které škáluje bez přetížení paměti. Tento tutoriál vás provede nastavením GroupDocs.Search pro Java, přidáním více složek s dokumenty a konfigurací enginu tak, aby **zvýšil výkon vyhledávání** a zároveň udržel **paměť indexu vyhledávání v Javě** pod kontrolou. Ať už indexujete právní smlouvy, podporné tikety nebo výzkumné práce, níže uvedené kroky vám poskytnou implementaci připravenou pro produkci.

## Rychlé odpovědi
- **Jaký je první krok?** Vytvořit složku pro index vyhledávání.  
- **Jak zahrnout mnoho souborů?** Použijte `index.add()` pro každou složku s dokumenty.  
- **Která možnost povoluje vyhledávání po částech?** `options.setChunkSearch(true)`.  
- **Mohu pokračovat ve vyhledávání po první části?** Ano, zavolejte `index.searchNext()` s tokenem.  
- **Potřebuji licenci?** Pro vývoj stačí bezplatná zkušební nebo dočasná licence; pro produkci je vyžadována plná licence.  

## Co se naučíte
- Jak vytvořit index vyhledávání ve specifikované složce.  
- Kroky k **přidání dokumentů do indexu** z více umístění.  
- Konfiguraci možností vyhledávání pro povolení vyhledávání po částech.  
- Provádění počátečního a následného vyhledávání po částech.  
- Reálné scénáře, kde vyhledávání po částech vyniká.  

## Předpoklady
Abyste mohli tento návod sledovat, ujistěte se, že máte:

- **Požadované knihovny**: GroupDocs.Search pro Java 25.4 nebo novější.  
- **Nastavení prostředí**: Nainstalovaný kompatibilní Java Development Kit (JDK).  
- **Základní znalosti**: Základy programování v Javě a znalost Maven.

## Nastavení GroupDocs.Search pro Java
Pro začátek integrujte GroupDocs.Search do svého projektu pomocí Maven:

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

Alternativně si stáhněte nejnovější verzi z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
Pro vyzkoušení GroupDocs.Search:

- **Bezplatná zkušební verze** – otestujte základní funkce bez závazku.  
- **Dočasná licence** – prodloužený přístup pro vývoj.  
- **Nákup** – plná licence pro produkční použití.

### Základní inicializace a nastavení
Vytvořte index ve složce, kde má být uložená prohledávatelná data:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## Jak přidat dokumenty do indexu
Nyní, když index existuje, dalším logickým krokem je **přidat dokumenty do indexu** z míst, kde jsou vaše soubory uloženy.

### 1. Vytvoření indexu
**Přehled**: Nastavte adresář pro index vyhledávání.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Přidání dokumentů do indexu
**Přehled**: Načtěte soubory z několika zdrojových složek.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Konfigurace možností vyhledávání pro Chunk Search
Povolte vyhledávání po částech úpravou objektu možností.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Provádění počátečního vyhledávání po částech
Spusťte první dotaz s možnostmi povolenými pro částečné vyhledávání.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Pokračování ve vyhledávání po částech
Iterujte přes zbývající části, dokud není vyhledávání dokončeno.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Proč používat vyhledávání po částech?
Vyhledávání po částech rozděluje obrovské kolekce dokumentů na zvládnutelné úseky, snižuje zatížení paměti a urychluje odezvu. Je zvláště užitečné, když:

1. **Právní týmy** potřebují najít konkrétní klauzule v tisících smluv.  
2. **Portály zákaznické podpory** musí okamžitě zobrazit relevantní články znalostní báze.  
3. **Výzkumníci** procházejí rozsáhlé datové sady, aniž by načítali celé soubory do paměti.

## Jak tento přístup **zvyšuje výkon vyhledávání**
Vyhledáváním menších částí místo celých souborů může engine:

- Přeskočit irelevantní sekce již na začátku, čímž šetří CPU cykly.  
- Udržovat v paměti pouze aktivní část, což přímo snižuje spotřebu **paměti indexu vyhledávání v Javě**.  
- Paralelizovat zpracování částí na vícejádrových strojích pro rychlejší výsledky.

## Správa **paměti indexu vyhledávání v Javě**
I když vyhledávání po částech již snižuje paměťovou stopu, můžete dále ladit JVM:

- Přidělte dostatečnou haldu (`-Xmx2g` nebo vyšší) podle velikosti indexu.  
- Použijte `index.optimize()` po hromadném přidání pro kompresi struktury indexu.  
- Sledujte pauzy GC pomocí nástrojů jako VisualVM, abyste předešli špičkám latence.

## Úvahy o výkonu
- **Správa paměti** – Přidělte dostatečnou velikost haldy (`-Xmx`) pro velké indexy.  
- **Monitorování zdrojů** – Sledujte využití CPU během indexování a vyhledávání.  
- **Údržba indexu** – Pravidelně obnovujte nebo čistěte index, aby se odstranily zastaralá data.

## Časté chyby a řešení problémů
| Problém | Proč se vyskytuje | Řešení |
|-------|----------------|-----|
| `OutOfMemoryError` během indexování | Příliš malá velikost haldy | Zvyšte haldu JVM (`-Xmx2g` nebo vyšší) |
| Žádné výsledky | Token části nebyl zpracován | Ujistěte se, že smyčka `while` běží, dokud `getNextChunkSearchToken()` není `null` |
| Pomalejší výkon vyhledávání | Index není optimalizován | Spusťte `index.optimize()` po hromadném přidání |

## Často kladené otázky

**Q: Co je vyhledávání po částech?**  
A: Vyhledávání po částech rozděluje datovou sadu na menší úseky, což umožňuje efektivní dotazy nad velkými objemy dat bez načítání celých dokumentů do paměti.

**Q: Jak aktualizuji svůj index novými soubory?**  
A: Stačí zavolat `index.add()` s cestou k novým dokumentům; index je automaticky zahrne.

**Q: Dokáže GroupDocs.Search pracovat s různými formáty souborů?**  
A: Ano, podporuje PDF, DOCX, XLSX, PPTX a mnoho dalších běžných formátů.

**Q: Jaké jsou typické úzké hrdla výkonu?**  
A: Omezení paměti a neoptimalizované indexy jsou nejčastější; přidělte dostatečnou haldu a pravidelně optimalizujte index.

**Q: Kde najdu podrobnější dokumentaci?**  
A: Navštivte oficiální [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) pro podrobné návody a reference API.

**Q: Funguje vyhledávání po částech s šifrovanými PDF?**  
A: Ano, pokud poskytnete heslo pomocí příslušného přetížení API.

**Q: Jak mohu sledovat průběh indexování?**  
A: Použijte přetížení `Index.add()`, které vrací objekt `Progress`, nebo se napojte na zpětné volání logování.

## Zdroje
- **Dokumentace**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Reference API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Stáhnout**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Bezplatná podpora**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Dočasná licence**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Poslední aktualizace:** 2026-02-21  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

---