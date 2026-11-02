---
date: '2026-11-02'
description: Vytvořte vlastní vyhledávací index java pomocí GroupDocs.Search pro zpracování
  běžných i kombinovaných znaků, optimalizaci vyhledávání obrázků OCR a zlepšení vyhledávání
  právních čísel případů.
keywords:
- custom search index java
- GroupDocs.Search Java
- character recognition java
- OCR search Java
- search library Java
lastmod: '2026-11-02'
og_description: Vytvořte vlastní vyhledávací index java pomocí GroupDocs.Search pro
  zpracování běžných i kombinovaných znaků, optimalizaci vyhledávání obrázků OCR a
  zlepšení vyhledávání právních čísel případů.
og_image_alt: Guide showing custom search index creation in Java with GroupDocs.Search
og_title: Vytvořte vlastní vyhledávací index java s GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Create a custom search index java using GroupDocs.Search to handle
    regular and blended characters, optimize OCR image search, and improve legal case
    number retrieval.
  headline: Create a custom search index java with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It means configuring an index to treat specific symbols as letters or
      blended characters, rather than ignoring them.
    question: What does “create custom search index” mean?
  - answer: GroupDocs.Search for Java (v25.4 at the time of writing).
    question: Which library is used?
  - answer: A free trial works for development; a paid license is required for production.
    question: Do I need a license?
  - answer: Yes—GroupDocs.Search supports OCR on images and PDFs when properly configured.
    question: Can I index both PDFs and images?
  - answer: Maven is the recommended way to manage dependencies, but you can also
      use Gradle or manual JARs.
    question: Is Maven required?
  type: FAQPage
tags:
- custom search index
- GroupDocs.Search
- Java OCR
- character recognition
- search library
title: Vytvořte vlastní vyhledávací index java s GroupDocs.Search
type: docs
url: /cs/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Vytvoření vlastního vyhledávacího indexu java s GroupDocs.Search

V moderních aplikacích s velkým objemem dokumentů je vytvoření **vlastního vyhledávacího indexu java**, který respektuje nuance vašeho textu — například pomlčky, podtržítka nebo jazykově specifické symboly — nezbytné pro rychlé a přesné vyhledávání. Tento tutoriál vás provede nastavením rozpoznávání znaků v **GroupDocs.Search for Java**, pokrývající jak běžné znaky (písmena, číslice, podtržítka), tak kombinované znaky (např. pomlčky). Na konci budete schopni přizpůsobit index tak, aby vyhovoval přesným potřebám OCR nebo scénářům vyhledávání obrázků, ať už indexujete právní spisová čísla, repozitáře zdrojového kódu nebo vícejazyčné PDF.

## Rychlé odpovědi
- **Co znamená „vytvořit vlastní vyhledávací index“?** Znamená to nastavení indexu tak, aby specifické symboly byly považovány za písmena nebo kombinované znaky, místo aby byly ignorovány.  
- **Která knihovna je použita?** GroupDocs.Search for Java (v25.4 v době psaní).  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; placená licence je vyžadována pro produkci.  
- **Mohu indexovat jak PDF, tak obrázky?** Ano — GroupDocs.Search podporuje OCR na obrázcích a PDF, pokud je správně nakonfigurován.  
- **Je Maven vyžadován?** Maven je doporučený způsob správy závislostí, ale můžete také použít Gradle nebo ruční JAR soubory.

## Co je vlastní vyhledávací index java?
**Vlastní vyhledávací index java** je vyhledávatelná datová struktura, kterou můžete tvarovat definováním, které znaky jsou považovány za písmena, číslice nebo kombinované symboly. Ve výchozím nastavení jsou mnohé symboly ignorovány, což může způsobit neúspěšné shody pro identifikátory jako čísla případů (`2023-AB-456`) nebo úryvky kódu (`my_variable`). Úprava slovníku abecedy vám dává plnou kontrolu nad tokenizací, což vede k vyšší relevanci a rychlejšímu provádění dotazů.

## Proč konfigurovat běžné a kombinované znaky pro právní spisová čísla?
Považování pomlček a lomítek za kombinované znaky udržuje související tokeny pohromadě, což zabraňuje nechtěnému rozdělení identifikátorů, jako jsou spisová čísla, kódy produktů nebo cesty k souborům. Toto nastavení **optimalizuje výkon vyhledávacího indexu** snížením fragmentace tokenů a zlepšuje relevanci pro obsah generovaný OCR, zejména při práci s právními dokumenty, které silně spoléhají na strukturované identifikátory.

## Předpoklady
- **JDK 8** nebo novější nainstalováno.  
- **Maven** pro správu závislostí.  
- Přístup ke knihovně **GroupDocs.Search for Java** (stažené přes Maven nebo oficiální stránky).  

### Požadované knihovny a závislosti
Přidejte záznamy repozitáře a závislosti do vašeho `pom.xml` (jak je uvedeno níže). XML blok musí zůstat nezměněn.

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

Můžete také stáhnout nejnovější JAR soubory z [vydání GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/).

### Získání licence
- **Bezplatná zkušební verze** – ideální pro první experimenty.  
- **Dočasná licence** – užitečná pro delší vývojové cykly.  
- **Produkční licence** – vyžadována pro komerční nasazení.  

Získejte licenci z oficiálního portálu: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Základní inicializace
Níže uvedený úryvek ukazuje minimální kód potřebný k vytvoření prázdného indexu. Třída `Index` je hlavní komponenta, která ukládá a spravuje vyhledávatelná data. Nechte ji beze změny; později na ní budeme stavět.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Nastavení GroupDocs.Search pro Java

### Instalace pomocí Maven
Maven konfigurace ze sekce *Předpoklady* je vše, co potřebujete. Po jejím přidání spusťte `mvn clean install` pro stažení binárek.

### Požadavky na nastavení prostředí
- Ujistěte se, že **složka indexu** a **složka dokumentů** existují na disku.  
- Používejte absolutní cesty nebo nakonfigurujte své IDE tak, aby správně řešilo relativní cesty.

## Průvodce implementací

Níže projdeme dvě odlišné funkce: **běžné znaky** a **kombinované znaky**. Každá funkce následuje stejný vzor — definujte cesty, vytvořte index, nastavte slovník znaků a nakonec indexujte své dokumenty.

### Funkce 1 – běžné znaky

#### Přehled
Běžné znaky jsou považovány za nezávislé tokeny. To je ideální, když chcete, aby číslice, písmena a podtržítka byly vyhledatelné přesně tak, jak se objevují.

#### Implementace krok za krokem

**1️⃣ Nastavení cest**  
Definujte, kde bude index uložen a kde se nacházejí vaše zdrojové dokumenty.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Vytvoření a konfigurace indexu**  
Instancujte index a vymažte jakékoli předchozí nastavení abecedy.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Definice běžných znaků**  
Vytvořte pole znaků, které zahrnuje číslice, latinská písmena a podtržítko.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Indexování dokumentů**  
Přidejte všechny soubory ze zdrojové složky do nově nakonfigurovaného indexu.

```java
index.add(documentFolder);
```

### Funkce 2 – kombinované znaky

#### Přehled
Kombinované znaky (např. pomlčky) často spojují dvě slova. Označení jako *kombinované* říká enginu, aby během indexování udržel okolní tokeny pohromadě.

#### Implementace krok za krokem

**1️⃣ Nastavení cest**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Vytvoření a konfigurace indexu**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Definice kombinovaných znaků**  
Zde říkáme slovníku, že pomlčka by měla být považována za kombinovaný znak.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Indexování dokumentů**  

```java
index.add(documentFolder);
```

## Praktické aplikace

### Případ použití 1 – správa právních dokumentů
Právní soubory často obsahují spisová čísla jako `2023-AB-456`. Konfigurací podtržítek a pomlček vyhledávání vrací přesné shody bez rozdělení identifikátoru, což vám pomáhá **efektivně vyhledávat právní spisová čísla**.

### Případ použití 2 – repozitáře zdrojového kódu
Vývojáři potřebují vyhledávat úryvky kódu, kde jsou podtržítka (`my_variable`) a pomlčky (`my-function`) významná. Vlastní rozpoznávání znaků zajišťuje, že vyhledávací engine respektuje tyto symboly.

### Případ použití 3 – vícejazyčné datové sady
Při práci s jazyky, které používají další abecedy, můžete **rozšířit sadu znaků Unicode** tak, aby zahrnovala tyto rozsahy, což zaručuje přesné výsledky vyhledávání napříč jazyky.

### Případ použití 4 – indexování PDF obrázků
Pokud indexujete naskenované PDF nebo soubory obrázků, výstup OCR často obsahuje smíšené znaky. Správná konfigurace běžných a kombinovaných znaků **optimalizuje výkon vyhledávacího indexu** pro obsah založený na obrázcích.

## Úvahy o výkonu

- **Správa zdrojů** – monitorujte využití haldy; velké indexy těží z inkrementálních commitů.  
- **Garbage collection** – uvolněte objekty `Index` po dokončení, aby JVM mohl uvolnit paměť.  
- **Optimalizace indexu** – periodicky zavolejte `index.optimize()` (pokud je k dispozici) pro kompakci indexu a zlepšení rychlosti dotazů.  

## Závěr

Nyní víte **jak vytvořit vlastní vyhledávací index java**, který rozlišuje mezi běžnými a kombinovanými znaky pomocí GroupDocs.Search for Java. Tato jemná kontrola vám umožňuje vytvářet OCR‑vědomá, vysoce výkonná vyhledávací řešení přizpůsobená právnímu, vývojářskému nebo vícejazyčnému prostředí.

### Další kroky
- Experimentujte s dalšími rozsahy Unicode pro ne‑latinské abecedy.  
- Kombinujte konfiguraci znaků s dalšími funkcemi GroupDocs.Search, jako je stemming nebo synonymum.  
- Zveřejněte index přes REST API, aby front‑end aplikace mohly provádět vyhledávání přes HTTP.  

## Často kladené otázky

**Q:** *Jaký je účel `CharacterType.Letter`?*  
**A:** Říká indexu, aby považoval dodané znaky za běžná písmena, takže jsou během indexování tokenizovány samostatně.

**Q:** *Mohu kombinovat běžné a kombinované znaky ve stejném indexu?*  
**A:** Ano — stačí zavolat `setRange` pro každý typ; slovník zvládne obě konfigurace současně.

**Q:** *Musím po změně abecedy znovu vytvořit index?*  
**A:** Rozhodně. Změny ve slovníku znaků ovlivňují tokenizaci, takže musíte dokumenty znovu indexovat, aby se nová pravidla aplikovala.

**Q:** *Existuje limit na počet vlastních znaků, které mohu definovat?*  
**A:** Knihovna podporuje celý rozsah Unicode; výkon může klesat, pokud přidáte extrémně velkou sadu, takže omezte na znaky, které skutečně potřebujete.

**Q:** *Jak to ovlivňuje přesnost OCR?*  
**A:** Přizpůsobením sady znaků indexu výstupu OCR snižujete falešné negativy a zlepšujete celkovou relevanci vyhledávání.

---

**Poslední aktualizace:** 2026-11-02  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Související tutoriály

- [Vytvořit a spravovat GroupDocs Search Java index](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Vytvořit adresář vyhledávacího indexu a nastavit licenci – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Java knihovna pro full‑textové vyhledávání – optimalizace indexu s GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)