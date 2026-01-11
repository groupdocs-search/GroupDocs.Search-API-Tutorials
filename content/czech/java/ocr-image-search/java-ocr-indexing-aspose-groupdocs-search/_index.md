---
date: '2026-01-11'
description: Naučte se, jak používat GroupDocs pro Java OCR indexování s Aspose.OCR,
  což umožňuje výkonné vyhledávání dokumentů v PDF, obrázcích a naskenovaných souborech.
keywords:
- Java OCR indexing
- document searchability
- OCR with GroupDocs
title: Jak použít GroupDocs pro Java OCR indexování s Aspose
type: docs
url: /cs/java/ocr-image-search/java-ocr-indexing-aspose-groupdocs-search/
weight: 1
---

# Jak používat GroupDocs pro Java OCR indexování s Aspose

V tomto průvodci se dozvíte **jak používat GroupDocs** k přidání vyhledávání poháněného OCR do vašich Java aplikací. Kombinací GroupDocs.Search s Aspose.OCR můžete převést obsah založený na obrázcích na prohledávatelný text, což výrazně zvyšuje užitečnost systémů pro správu dokumentů. Provedeme vás nastavením, indexováním, vyhledáváním a vlastním OCR integrací, vše s jasnými, krok‑za‑krokem příklady.

## Rychlé odpovědi
- **Která knihovna poskytuje OCR indexování?** GroupDocs.Search ve spojení s Aspose.OCR.  
- **Jaká verze Javy je vyžadována?** JDK 8 nebo vyšší.  
- **Potřebuji licenci?** K dispozici je bezplatná zkušební verze; pro produkční nasazení je vyžadována placená licence.  
- **Mohu indexovat jak samostatné, tak vložené obrázky?** Ano, povolte obě možnosti v `IndexingOptions`.  
- **Je podporováno vícevláknové zpracování?** Ano, můžete paralelizovat indexování pro velké datové sady.

## Co je OCR indexování s GroupDocs?
OCR indexování extrahuje text z obrázků (včetně skenovaných PDF) a ukládá jej do prohledávatelného indexu. GroupDocs.Search se stará o samotné indexování a provádění dotazů, zatímco Aspose.OCR provádí rozpoznávání znaků.

## Proč používat GroupDocs pro Java OCR indexování?
- **Vysoká přesnost** díky pokročilému OCR enginu od Aspose.  
- **Bezproblémová integrace do Javy** pomocí Maven nebo přímých JAR souborů.  
- **Flexibilní konfigurace** pro samostatné i vložené obrázky.  
- **Škálovatelný výkon** s podporou vícevláknového zpracování a optimalizací paměti.

## Požadavky
- **GroupDocs.Search** ≥ 25.4  
- **Aspose.OCR** (nejnovější verze)  
- JDK 8+ a IDE (IntelliJ, Eclipse, NetBeans)  
- Základní znalost Javy; Maven je užitečný, ale není povinný

## Nastavení GroupDocs.Search pro Java
### Použití Maven
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
Alternativně si stáhněte nejnovější verzi GroupDocs.Search pro Java z [GroupDocs releases](https://releases.groupdocs.com/search/java/).

### Získání licence
- **Free Trial** – prozkoumejte všechny funkce zdarma.  
- **Temporary License** – prodloužené testovací období.  
- **Purchase** – vyžadováno pro produkční nasazení.

### Základní inicializace a nastavení
Vytvořte složku pro index a inicializujte objekt `Index`:

```java
import com.groupdocs.search.Index;
// Specify the directory where the index will be stored.
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
// Create an instance of Index class at the specified location.
Index index = new Index(indexFolder);
```

## Jak používat GroupDocs pro OCR indexování
### Vytvoření indexu
Nejprve nastavte složku, která bude obsahovat soubory indexu:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
Index index = new Index(indexFolder);
```

### Nastavení možností OCR indexování
Povolte OCR pro samostatné i vložené obrázky a připojte vlastní OCR konektor:

```java
import com.groupdocs.search.options.IndexingOptions;
IndexingOptions options = new IndexingOptions();
options.getOcrIndexingOptions().setEnabledForSeparateImages(true);
options.getOcrIndexingOptions().setEnabledForEmbeddedImages(true);
// Set a custom OCR connector.
options.getOcrIndexingOptions().setOcrConnector(new OcrConnector());
```

### Indexování dokumentů
Přidejte své zdrojové dokumenty (PDF, Word, obrázky atd.) do indexu:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder, options);
```

### Vyhledávání v indexu
Spusťte vyhledávací dotaz proti indexovanému obsahu:

```java
import com.groupdocs.search.results.SearchResult;
String query = "water";
SearchResult result = index.search(query);
```

### Implementace OCR konektoru
Použijte Aspose.OCR k rozpoznání textu z obrázků. Implementujte rozhraní `IOcrConnector` podle ukázky:

```java
import com.groupdocs.search.options.IOcrConnector;
import com.groupdocs.search.options.OcrContext;
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import com.aspose.ocr.AsposeOCR;

public class OcrConnector implements IOcrConnector {
    @Override
    public final String recognize(OcrContext context) {
        if (null == context.getImageLocation()) {
            throw new RuntimeException("The image type is not supported: " + context.getImageLocation());
        }
        
        BufferedImage image = ImageIO.read(context.getImageLocation().toFile());
        AsposeOCR api = new AsposeOCR();
        String text = api.RecognizePage(image);
        return text;
    }
}
```

## Praktické aplikace
1. **Systémy pro správu dokumentů** – rychlé vyhledávání dokumentů obsahujících skenované obrázky.  
2. **Archivní vyhledávání** – nalezení historických záznamů v masivních archivech.  
3. **Analýza právních dokumentů** – vyhledávání smluv a důkazů, které zahrnují skenované podpisy nebo diagramy.  
4. **Vyhledávání v lékařských záznamech** – indexování pacientských formulářů, laboratorních výsledků a anotací rentgenových snímků.

## Úvahy o výkonu
- **Velikost indexu** – vyloučte zbytečná metadata, aby byl index co nejmenší.  
- **Vícevláknové zpracování** – zpracovávejte velké dávky paralelně pro zrychlení indexování.  
- **Správa paměti** – monitorujte haldu JVM při práci s vysoce rozlišenými obrázky.

## Časté problémy a řešení
- **Chyby licence** – ujistěte se, že správný licenční soubor je umístěn v pracovním adresáři aplikace.  
- **Chybějící obrázky** – ověřte, že cesty k obrázkům jsou přístupné a formáty jsou podporovány (PNG, JPEG, BMP).  
- **Out‑Of‑Memory** – zvyšte haldu JVM (`-Xmx`) nebo zpracovávejte dokumenty v menších dávkách.

## Často kladené otázky
**Q: Jak vyřešit problémy s licencí v GroupDocs.Search?**  
A: Získejte dočasnou licenci na [GroupDocs website](https://purchase.groupdocs.com/temporary-license/), která odemkne všechny funkce.

**Q: Jak nejlépe zvládnout indexování velkých dokumentů?**  
A: Využijte vícevláknové zpracování a dávkové zpracování pro zvýšení výkonu a snížení zatížení paměti.

**Q: Můžu dále přizpůsobit nastavení OCR v GroupDocs.Search?**  
A: Ano, `IndexingOptions` umožňuje jemně doladit chování OCR, například výběr jazyka a předzpracování obrázků.

**Q: Jaké jsou běžné tipy pro řešení problémů při používání GroupDocs.Search?**  
A: Zkontrolujte cesty ke složkám, ověřte, že jsou všechny závislosti přítomny, a prohlédněte výstup logu pro chybějící soubory.

**Q: Jak integrovat Aspose.OCR do existující Java aplikace?**  
A: Implementujte rozhraní `IOcrConnector` podle výše uvedeného příkladu a zajistěte správné zpracování vstupních obrázků.

## Zdroje
- [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)  
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Poslední aktualizace:** 2026-01-11  
**Testováno s:** GroupDocs.Search 25.4, Aspose.OCR nejnovější vydání  
**Autor:** GroupDocs