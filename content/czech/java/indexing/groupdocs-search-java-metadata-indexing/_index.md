---
date: '2026-01-06'
description: Naučte se, jak přidávat dokumenty do indexu a vyhledávat dokumenty podle
  metadat pomocí GroupDocs.Search Java. Ovládněte nastavení indexu, vytvářejte indexy,
  přidávejte dokumenty a provádějte přesná vyhledávání.
keywords:
- metadata indexing java
- GroupDocs Search Java
- document management with metadata
title: Jak přidat dokumenty do indexu s metadatovým indexováním v Javě pomocí GroupDocs.Search
type: docs
url: /cs/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# Jak přidat dokumenty do indexu s indexací metadat v Javě pomocí GroupDocs.Search

V moderních aplikacích je **přidání dokumentů do indexu** rychle a spolehlivě nezbytné pro poskytování rychlých vyhledávacích zážitků. Ať už budujete právní úložiště, znalostní bázi zákaznické podpory nebo interní dokumentový portál, využití metadat umožňuje **vyhledávat dokumenty podle metadat** jako je autor, název nebo vlastní štítky. Tento průvodce vás provede kompletním procesem – konfigurací nastavení indexu, vytvořením indexu zaměřeného na metadata, přidáním vašich souborů a prováděním výkonných vyhledávání – vše s GroupDocs.Search pro Javu.

## Rychlé odpovědi
- **Jaký je hlavní účel indexování metadat?** Umožňuje rychlé vyhledávání na základě vlastností dokumentu místo obsahu plného textu.  
- **Která metoda přidává soubory do indexu?** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **Mohu vyhledávat podle vlastních polí metadat?** Ano, jakmile jsou pole indexována, můžete je dotazovat přímo.  
- **Potřebuji licenci pro vývoj?** Dočasná zkušební licence stačí pro hodnocení; pro produkci je vyžadována plná licence.  
- **Jaká verze Javy je požadována?** Doporučuje se JDK 8 nebo vyšší.

## Co je indexování metadat v GroupDocs.Search?
Indexování metadat extrahuje a ukládá atributy dokumentu (např. autor, datum vytvoření, vlastní štítky) do vyhledávatelné struktury. Když **přidáte dokumenty do indexu**, engine zaznamená tyto atributy, což vám umožní spouštět přesné dotazy jako „najít všechny PDF vytvořené *John Doe*“.

## Proč používat GroupDocs.Search pro indexování metadat?
- **Výkon:** Vyhledávání metadat je nenáročné a vrací výsledky v milisekundách.  
- **Flexibilita:** Podporuje širokou škálu formátů souborů (PDF, DOCX, PPT atd.).  
- **Škálovatelnost:** Zvládá miliony dokumentů s minimální paměťovou stopou.  

## Předpoklady
- GroupDocs.Search pro Javu ≥ 25.4.  
- Nainstalovaný a nakonfigurovaný JDK 8 nebo novější.  
- Základní znalost Javy a Maven.  

## Nastavení GroupDocs.Search pro Javu

### Pokyny k instalaci
Přidejte repozitář GroupDocs a závislost do vašeho `pom.xml`:

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

Můžete také stáhnout nejnovější binární soubory přímo z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
Pro získání dočasné licence pro testování:

1. Navštivte webové stránky GroupDocs a přejděte do sekce **Purchase**.  
2. Vyberte plán **temporary license**, který odpovídá vašim potřebám hodnocení.  

## Implementace krok za krokem

### Funkce 1: Konfigurace nastavení indexu
Nakonfigurujte index tak, aby se zaměřoval na metadata:

```java
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.IndexType;

// Initialize index settings
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);  // Focus on metadata indexing
```

- `setIndexType(IndexType.MetadataIndex)` říká engine, aby upřednostňoval metadata před obsahem plného textu.

### Funkce 2: Vytvoření indexu ve specifikovaném adresáři
Vytvořte fyzický adresář indexu, kde budou uložena všechna metadata:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

Nahraďte `YOUR_DOCUMENT_DIRECTORY` cestou, která odpovídá uspořádání vašeho projektu.

### Funkce 3: Jak přidat dokumenty do indexu
Nyní, když index existuje, můžete **přidat dokumenty do indexu**, aby se staly vyhledávatelnými:

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**Tipy:**  
- Ověřte, že cesta ke složce je správná a aplikace má oprávnění ke čtení.  
- GroupDocs.Search automaticky extrahuje podporovaná metadata z každého souboru.

### Funkce 4: Vyhledávání dokumentů podle metadat
Spusťte dotaz, který cílí na pole metadat, například vyhledávání dokumentů, kde je jazyk angličtina:

```java
import com.groupdocs.search.results.SearchResult;

String query = "English";  // Define search query
SearchResult result = index.search(query);  // Perform the search

// Process results (example)
for (int i = 0; i < result.getDocumentCount(); i++) {
    System.out.println("Found document: " + result.getFoundDocument(i).getFilePath());
}
```

- `search(query)` prohledává indexovaná metadata a vrací odpovídající dokumenty.

## Praktické aplikace
1. **Enterprise Document Management:** Vyhledávejte smlouvy podle data smlouvy nebo jména signatáře.  
2. **Digital Library Catalogs:** Umožněte uživatelům procházet knihy podle žánru, roku vydání nebo autora.  
3. **CRM Systems:** Rychle najděte soubory klientů pomocí vlastních metadat jako je ID zákazníka nebo region.  

## Úvahy o výkonu
- **Postupné aktualizace:** Použijte `index.addOrUpdate()` pro nové nebo změněné soubory místo přestavování celého indexu.  
- **Ladění paměti:** Přizpůsobte velikost haldy JVM (`-Xmx`) podle objemu indexovaných metadat.  
- **Optimalizované úložiště:** Pravidelně volajte `index.optimize()`, aby se index zkomprimoval a zlepšila se rychlost dotazů.

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Žádné výsledky nebyly vráceny** | Ověřte, že očekávaná pole metadat jsou ve zdrojových souborech skutečně přítomna. |
| **Chyby oprávnění** | Ujistěte se, že proces Java má přístup ke čtení jak ke složce s dokumenty, tak k adresáři indexu. |
| **Chyby nedostatku paměti** | Zvyšte velikost haldy JVM nebo rozdělte operaci `add` do menších skupin souborů. |

## Často kladené otázky

**Q: Co je indexování metadat?**  
A: Indexování metadat ukládá atributy dokumentu (autor, název, vlastní štítky) do vyhledávatelné struktury, což umožňuje rychlé vyhledávání bez skenování plného textu.

**Q: Jak získám dočasnou licenci?**  
A: Navštivte stránku nákupu GroupDocs a postupujte podle kroků k získání zkušební licence.

**Q: Mohu tímto nastavením indexovat PDF?**  
A: Ano, GroupDocs.Search podporuje PDF, DOCX, PPT a mnoho dalších formátů.

**Q: Jaké jsou běžné problémy při přidávání dokumentů?**  
A: Ověřte správné cesty k souborům a ujistěte se, že aplikace má oprávnění ke čtení adresářů.

**Q: Jak optimalizovat výkon vyhledávání?**  
A: Pravidelně aktualizujte svůj index, používejte postupné přidávání a laděte nastavení paměti JVM.

## Zdroje

- **Dokumentace:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **Reference API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Stáhnout:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub repozitář:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Bezplatné fórum podpory:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **Dočasná licence:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2026-01-06  
**Testováno s:** GroupDocs.Search Java 25.4  
**Autor:** GroupDocs