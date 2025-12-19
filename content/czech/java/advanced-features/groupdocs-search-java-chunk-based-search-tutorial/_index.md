---
date: '2025-12-19'
description: Naučte se, jak přidávat dokumenty do indexu a povolit vyhledávání založené
  na blocích v Javě pomocí GroupDocs.Search, což zvyšuje výkon při práci s velkými
  sadami dokumentů.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Přidat dokumenty do indexu s vyhledáváním založeným na blocích v Javě
type: docs
url: /cs/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Přidání dokumentů do indexu s vyhledáváním po částech v Javě

V dnešním datově řízeném světě je schopnost **přidat dokumenty do indexu** rychle a poté provádět vyhledávání po částech nezbytná pro každou aplikaci, která pracuje s velkými kolekcemi souborů. Ať už se zabýváte právními smlouvami, archivy zákaznické podpory nebo obrovskými výzkumnými knihovnami, tento tutoriál vám přesně ukáže, jak nastavit GroupDocs.Search pro Java, abyste mohli dokumenty efektivně indexovat a získávat relevantní informace v malých částech.

## Co se naučíte
- Jak vytvořit vyhledávací index ve specifikované složce.  
- Kroky k **přidání dokumentů do indexu** z více míst.  
- Konfigurace možností vyhledávání pro povolení vyhledávání po částech.  
- Provádění počátečních a následných vyhledávání po částech.  
- Reálné scénáře, kde vyhledávání dokumentů po částech vyniká.

## Rychlé odpovědi
- **Jaký je první krok?** Vytvořte složku pro vyhledávací index.  
- **Jak zahrnout mnoho souborů?** Použijte `index.add()` pro každou složku s dokumenty.  
- **Která možnost povoluje vyhledávání po částech?** `options.setChunkSearch(true)`.  
- **Mohu pokračovat ve vyhledávání po první části?** Ano, zavolejte `index.searchNext()` s tokenem.  
- **Potřebuji licenci?** Bezplatná zkušební verze nebo dočasná licence stačí pro vývoj; pro produkci je vyžadována plná licence.

## Předpoklady
Abyste mohli tento návod sledovat, ujistěte se, že máte:

- **Požadované knihovny**: GroupDocs.Search pro Java 25.4 nebo novější.  
- **Nastavení prostředí**: Nainstalovaný kompatibilní Java Development Kit (JDK).  
- **Předpoklady znalostí**: Základní programování v Javě a znalost Maven.

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

Alternativně stáhněte nejnovější verzi z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
Pro vyzkoušení GroupDocs.Search:

- **Free Trial** – vyzkoušejte základní funkce bez závazku.  
- **Temporary License** – rozšířený přístup pro vývoj.  
- **Purchase** – plná licence pro produkční použití.

### Základní inicializace a nastavení
Vytvořte index ve složce, kde chcete mít vyhledávatelná data:

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
Nyní, když existuje index, dalším logickým krokem je **přidat dokumenty do indexu** z míst, kde jsou vaše soubory uloženy.

### 1. Vytvoření indexu
**Přehled**: Nastavte adresář pro vyhledávací index.

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
Povolte vyhledávání po částech úpravou objektu options.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Provádění počátečního vyhledávání po částech
Spusťte první dotaz pomocí možností povolených pro chunk.

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
Vyhledávání po částech rozděluje obrovské kolekce dokumentů na zvládnutelné části, snižuje zatížení paměti a zrychluje odezvu. Je zvláště užitečné, když:

1. **Právní týmy** potřebují najít konkrétní klauzule v tisících smluv.  
2. **Portály zákaznické podpory** musí okamžitě zobrazit relevantní články znalostní báze.  
3. **Výzkumníci** procházejí rozsáhlé datové sady, aniž by načítali celé soubory do paměti.

## Úvahy o výkonu
- **Správa paměti** – Přidělte dostatečný heap (`-Xmx`) pro velké indexy.  
- **Monitorování zdrojů** – Sledujte využití CPU během indexování a vyhledávání.  
- **Údržba indexu** – Pravidelně přestavujte nebo čistěte index, abyste odstranili zastaralá data.

## Časté úskalí a řešení problémů
| Problém | Proč se to děje | Oprava |
|-------|----------------|-----|
| `OutOfMemoryError` během indexování | Velikost haldy příliš malá | Zvyšte JVM heap (`-Xmx2g` nebo vyšší) |
| Žádné výsledky | Chunk token nebyl zpracován | Ujistěte se, že smyčka `while` běží až dokud `getNextChunkSearchToken()` není `null` |
| Pomalý výkon vyhledávání | Index není optimalizován | Spusťte `index.optimize()` po hromadných přidáních |

## Často kladené otázky

**Q: Co je vyhledávání po částech?**  
A: Vyhledávání po částech rozděluje datovou sadu na menší části, což umožňuje efektivní dotazy nad velkými objemy dat, aniž by se načítaly celé dokumenty do paměti.

**Q: Jak aktualizuji svůj index novými soubory?**  
A: Jednoduše zavolejte `index.add()` s cestou k novým dokumentům; index je automaticky zahrne.

**Q: Dokáže GroupDocs.Search zpracovat různé formáty souborů?**  
A: Ano, podporuje PDF, DOCX, XLSX, PPTX a mnoho dalších běžných formátů.

**Q: Jaké jsou typické úzké místa výkonu?**  
A: Omezení paměti a neoptimalizované indexy jsou nejčastější; přidělte dostatečný heap a pravidelně optimalizujte index.

**Q: Kde najdu podrobnější dokumentaci?**  
A: Navštivte oficiální [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) pro podrobné návody a reference API.

## Zdroje
- **Documentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2025-12-19  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs