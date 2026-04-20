---
date: '2026-03-17'
description: Naučte se, jak vytvořit index pomocí GroupDocs.Search pro Javu, nakonfigurovat
  běžné a kombinované znaky a optimalizovat vyhledávání pro čísla právních případů
  a OCR obrázky.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Jak vytvořit index s rozpoznáváním znaků v Javě
type: docs
url: /cs/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Jak vytvořit index s rozpoznáváním znaků pomocí GroupDocs.Search pro Java

V moderních aplikacích pracujících s velkým množstvím dokumentů je **jak vytvořit index**, který respektuje nuance vašeho textu – například pomlčky, podtržítka nebo jazykově specifické symboly – nezbytný pro rychlé a přesné vyhledávání. V tomto tutoriálu vás provedeme konfigurací rozpoznávání znaků v **GroupDocs.Search pro Java**, pokrývající jak běžné znaky (písmena, číslice, podtržítka), tak i kombinované znaky (např. pomlčky). Na konci budete schopni přizpůsobit index tak, aby vyhovoval přesným potřebám vašeho scénáře OCR nebo vyhledávání obrázků, ať už indexujete právní spisové čísla, repozitáře zdrojového kódu nebo vícejazyčné PDF.

## Rychlé odpovědi
- **Co znamená “create custom search index”?** Znamená to konfiguraci indexu tak, aby konkrétní symboly byly považovány za písmena nebo kombinované znaky, místo aby byly ignorovány.  
- **Která knihovna se používá?** GroupDocs.Search pro Java (v25.4 v době psaní).  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; placená licence je vyžadována pro produkci.  
- **Mohu indexovat jak PDF, tak obrázky?** Ano – GroupDocs.Search podporuje OCR na obrázcích a PDF, pokud je správně nakonfigurován.  
- **Je Maven povinný?** Maven je doporučený způsob správy závislostí, ale můžete také použít Gradle nebo ruční JAR soubory.  

## Co je vlastní vyhledávací index?
Vlastní vyhledávací index vám umožňuje definovat, jak vyhledávač interpretuje znaky. Ve výchozím nastavení jsou mnohé symboly ignorovány, což může vést k nevyhledání shod pro věci jako spisová čísla (`2023-AB-456`) nebo úryvky kódu (`my_variable`). Úprava slovníku abecedy vám dává plnou kontrolu nad tím, co engine považuje za prohledávatelný text.

## Proč konfigurovat běžné a kombinované znaky pro právní spisová čísla?
- **Běžné znaky** (písmena, číslice, podtržítka) jsou tokenizovány samostatně, což umožňuje vyhledávání přesných shod pro identifikátory.  
- **Kombinované znaky** (pomlčky, lomítka) udržují související tokeny pohromadě, čímž zabraňují nechtěnému rozdělení spisových čísel, kódů produktů nebo cest k souborům.  
- Tato konfigurace **optimalizuje výkon vyhledávacího indexu** snížením fragmentace tokenů a zlepšením relevance pro obsah generovaný OCR.  

## Předpoklady
- **JDK 8** nebo novější nainstalováno.  
- **Maven** pro správu závislostí.  
- Přístup ke knihovně **GroupDocs.Search pro Java** (stažené přes Maven nebo oficiální stránky).  

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

Také můžete stáhnout nejnovější JAR soubory z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
- **Free Trial** – ideální pro rané experimentování.  
- **Temporary License** – užitečná pro delší vývojové cykly.  
- **Production License** – vyžadována pro komerční nasazení.  

Získejte licenci z oficiálního portálu: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Základní inicializace
Níže uvedený úryvek ukazuje minimální kód potřebný k vytvoření prázdného indexu. Nechte jej beze změny; později na něj navážeme.

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

Níže projdeme dvě odlišné funkce: **běžné znaky** a **kombinované znaky**. Každá funkce následuje stejný vzor – definujte cesty, vytvořte index, nastavte slovník znaků a nakonec indexujte své dokumenty.

### Funkce 1 – Běžné znaky

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
Instancujte index a vymažte jakoukoli předchozí konfiguraci abecedy.

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

### Funkce 2 – Kombinované znaky

#### Přehled
Kombinované znaky (jako pomlčky) často spojují dvě slova. Označení je jako *blended* říká enginu, aby během indexování udržel okolní tokeny pohromadě.

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

### Případ použití 1 – Správa právních dokumentů
Právní soubory často obsahují spisová čísla jako `2023-AB-456`. Konfigurací podtržítek a pomlček vyhledávání vrací přesné shody bez rozdělení identifikátoru, což vám pomáhá **efektivně vyhledávat právní spisová čísla**.

### Případ použití 2 – Repozitáře zdrojového kódu
Vývojáři potřebují vyhledávat úryvky kódu, kde jsou podtržítka (`my_variable`) a pomlčky (`my-function`) významná. Vlastní rozpoznávání znaků zajišťuje, že vyhledávač respektuje tyto symboly.

### Případ použití 3 – Vícejazyčné datové sady
Při práci s jazyky, které používají další abecedy, můžete **rozšířit sadu znaků Unicode** tak, aby zahrnovala tyto rozsahy, což zaručuje přesné výsledky vyhledávání napříč jazyky.

### Případ použití 4 – Indexování PDF obrázků
Pokud indexujete naskenované PDF nebo soubory s obrázky, výstup OCR často obsahuje smíšené znaky. Správná konfigurace běžných a kombinovaných znaků **optimalizuje výkon vyhledávacího indexu** pro obsah založený na obrázcích.

## Úvahy o výkonu

- **Správa zdrojů** – Sledujte využití haldy; velké indexy těží z inkrementálních commitů.  
- **Garbage Collection** – Uvolněte objekty `Index`, když jsou hotové, aby JVM mohl uvolnit paměť.  
- **Optimalizace indexu** – Periodicky zavolejte `index.optimize()` (pokud je k dispozici) pro kompakci indexu a zlepšení rychlosti dotazů.  

## Závěr

Nyní víte **jak vytvořit index**, který rozlišuje mezi běžnými a kombinovanými znaky pomocí GroupDocs.Search pro Java. Tato jemná kontrola vám umožňuje vytvářet OCR‑vědomá, výkonná vyhledávací řešení přizpůsobená právnímu, vývojářskému nebo vícejazyčnému prostředí.

### Další kroky
- Experimentujte s dalšími rozsahy Unicode pro ne‑latinské abecedy.  
- Kombinujte konfiguraci znaků s dalšími funkcemi GroupDocs.Search, jako je stemming nebo synonymum.  
- Integrovat index do REST API pro zpřístupnění vyhledávacích schopností front‑end aplikacím.

## Často kladené otázky

**Q:** *Jaký je účel `CharacterType.Letter`?*  
**A:** Říká indexu, aby považoval dodané znaky za běžná písmena, takže jsou během indexování tokenizovány samostatně.

**Q:** *Mohu v jednom indexu kombinovat běžné i kombinované znaky?*  
**A:** Ano – stačí zavolat `setRange` pro každý typ; slovník bude obě konfigurace zpracovávat současně.

**Q:** *Musím po změně abecedy znovu vytvořit index?*  
**A:** Rozhodně. Změny ve slovníku znaků ovlivňují tokenizaci, takže musíte dokumenty znovu indexovat, aby se nová pravidla aplikovala.

**Q:** *Existuje limit na počet vlastních znaků, které mohu definovat?*  
**A:** Knihovna podporuje celý rozsah Unicode; výkon může klesnout, pokud přidáte extrémně velkou sadu, takže ji omezte na znaky, které skutečně potřebujete.

**Q:** *Jak to ovlivňuje přesnost OCR?*  
**A:** Zarovnáním sady znaků indexu s výstupem OCR motoru snížíte počet falešných negativ a zlepšíte celkovou relevanci vyhledávání.

---

**Poslední aktualizace:** 2026-03-17  
**Testováno s:** GroupDocs.Search 25.4 pro Java  
**Autor:** GroupDocs