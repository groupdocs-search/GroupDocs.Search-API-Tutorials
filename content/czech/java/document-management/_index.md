---
date: 2026-10-12
description: Naučte se, jak aktualizovat index, přidávat dokumenty a mazat položky
  indexu pomocí GroupDocs.Search pro Java. Podrobné kroky, osvědčené postupy a ukázky
  kódu.
keywords:
- how to update index
- how to add documents
- how to delete index
lastmod: 2026-10-12
og_description: Naučte se, jak aktualizovat index, přidávat dokumenty a mazat položky
  indexu s GroupDocs.Search pro Java. Postupujte podle podrobných návodů a tipů na
  výkon.
og_image_alt: Guide to updating index, adding and deleting documents using GroupDocs.Search
  Java SDK
og_title: Jak aktualizovat index a přidat dokumenty pomocí GroupDocs.Search Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: Learn how to update index, add documents, and delete index entries
    using GroupDocs.Search for Java. Detailed steps, best practices, and code examples.
  headline: How to update index and add docs with GroupDocs.Search Java
  type: TechArticle
- description: Learn how to update index, add documents, and delete index entries
    using GroupDocs.Search for Java. Detailed steps, best practices, and code examples.
  name: How to update index and add docs with GroupDocs.Search Java
  steps:
  - name: open or create the index
    text: '`Index index = new Index("path/to/index");` creates the folder if it does
      not exist and prepares internal structures for fast lookup.'
  - name: add a single document
    text: '`index.addDocument(new File("contracts/contract1.pdf"));` inserts the PDF,
      automatically detecting its format and extracting text.'
  - name: add multiple documents in a batch
    text: Iterate over a directory and call `addDocument` for each file. Batch processing
      reduces I/O overhead and improves overall throughput.
  type: HowTo
- questions:
  - answer: Call `deleteDocument(documentId)` with the unique identifier; the entry
      is instantly purged and storage is reclaimed.
    question: How do I remove documents from index?
  - answer: Yes, you can set custom metadata (e.g., category, author) via the `Document`
      object's attribute API before adding it to the index.
    question: Can I modify document attributes to enhance search accuracy?
  - answer: The official GroupDocs.Search documentation includes a step‑by‑step tutorial
      that covers index creation, document addition, and query execution.
    question: Is there a “search index tutorial” for beginners?
  - answer: The library includes linguistic features that improve accuracy for homophones
      and similar‑sounding words.
    question: Does GroupDocs.Search support homophone recognition?
  - answer: Java 8 or later is required; the library is fully compatible with Java
      11 and newer LTS releases.
    question: What version of Java is required for the latest GroupDocs.Search?
  type: FAQPage
tags:
- update index
- document management
- GroupDocs.Search Java
- add documents
title: Jak aktualizovat index a přidat dokumenty pomocí GroupDocs.Search Java
type: docs
url: /cs/java/document-management/
weight: 6
---

# Jak aktualizovat index a přidávat dokumenty pomocí GroupDocs.Search Java

Efektivní správa vyhledávacího indexu je nezbytná pro každou aplikaci založenou na Javě, která potřebuje rychlé a přesné získávání informací. V tomto tutoriálu se naučíte **jak aktualizovat index**, stejně jako jak přidávat a mazat dokumenty pomocí GroupDocs.Search pro Java. Uvidíte osvědčené postupy, tipy na výkon a příklady reálných případů použití, které udržují váš index úsporný a dotazy bleskově rychlé.

## Rychlé odpovědi
- **Jaký je první krok k přidání dokumentů do indexu?** Vytvořte nebo otevřete instanci `Index` a zavolejte `addDocument(...)`.
- **Mohu odstranit dokumenty z indexu?** Ano, zavolejte `deleteDocument(...)` s identifikátorem dokumentu.
- **Potřebuji speciální licenci?** Pro produkční použití je vyžadována platná licence GroupDocs.Search pro Java.
- **Která verze Javy je podporována?** Java 8 a vyšší jsou plně podporovány.
- **Kde najdu více příkladů?** Viz oficiální dokumentace GroupDocs.Search pro Java a reference API.

## Co znamená „přidat dokumenty do indexu“ v GroupDocs.Search?
`addDocument` operace vloží prohledávatelný obsah souboru (PDF, DOCX, TXT atd.) do datové struktury indexu. To umožní okamžité dotazování na dokument a zajistí, že následné aktualizace nebo mazání zůstanou synchronizovány se zdrojovými soubory. Také zaznamená metadata, jako je název souboru a velikost, která lze použít pro filtrování výsledků vyhledávání.

## Proč používat GroupDocs.Search pro projekty správy dokumentů v Javě?
GroupDocs.Search zpracovává až **10 milionů dokumentů** s latencí pod sekundu, podporuje **více než 100 formátů souborů** a nabízí vestavěné ladění relevance. API je lehké, vyžaduje jen několik řádků kódu a hladce se integruje s jakoukoliv Java aplikací – ať už běží na desktopu, serveru nebo v cloudovém prostředí.

## Předpoklady
- Java 8 + vývojové prostředí (IDE, JDK, Maven/Gradle).  
- Knihovna GroupDocs.Search pro Java (ke stažení z oficiálního webu).  
- Platná licence GroupDocs.Search (dočasné licence jsou k dispozici pro testování).

## Jak přidat dokumenty do indexu v GroupDocs.Search pro Java?
Načtěte cílový soubor a zavolejte `addDocument` na instanci `Index` – tento jediný volání extrahuje text, detekuje jazyk a uloží prohledávatelné tokeny. Metoda také vrací ID dokumentu, které byste měli uložit pro budoucí operace aktualizace nebo mazání.

Třída `Index` je hlavní objekt, který představuje prohledávatelnou kolekci uloženou na disku. Po jejím vytvoření jsou všechny následné operace – přidávání, aktualizace, mazání a optimalizace – prováděny prostřednictvím této instance.

### Krok 1: otevřít nebo vytvořit index
`Index index = new Index("path/to/index");` vytvoří složku, pokud neexistuje, a připraví interní struktury pro rychlé vyhledávání.

### Krok 2: přidat jeden dokument
`index.addDocument(new File("contracts/contract1.pdf"));` vloží PDF, automaticky detekuje jeho formát a extrahuje text.

### Krok 3: přidat více dokumentů najednou
Procházejte adresář a pro každý soubor zavolejte `addDocument`. Dávkové zpracování snižuje I/O režii a zlepšuje celkovou propustnost.

## Jak aktualizovat index, když se zdrojový soubor změní?
`updateDocument` aktualizuje existující dokument v indexu pomocí jeho identifikátoru. Nahraďte starý obsah nejnovější verzí zavoláním této metody a předáním stejného identifikátoru dokumentu, který jste získali při prvním přidání souboru. Tato operace přepíše pouze změněné tokeny a zbytek indexu ponechá nedotčený pro maximální efektivitu.

### Postupná aktualizace
1. Získejte ID dokumentu (uložte jej při prvním přidání souboru).  
2. Zavolejte `index.updateDocument(documentId, new File("contracts/contract1_v2.pdf"));` pro obnovení záznamu.  
3. Volitelně spusťte `index.optimize()` po velkém dávkovém aktualizování, aby byl index kompaktní.

## Jak bezpečně smazat položky indexu?
`deleteDocument` odstraní dokument z indexu podle jeho identifikátoru. Odstranění dokumentu uvolní úložný prostor a zabrání zastaralým datům ovlivnit relevance skóre. Zavolejte `deleteDocument` s identifikátorem; index okamžitě vyloučí soubor z budoucích vyhledávání a aktualizuje interní seznamy příspěvků pro zachování výkonu dotazů.

## Jak optimalizovat index pro maximální výkon?
`optimize()` komprimuje index sloučením segmentů a vyčištěním smazaných položek. Po hromadném přidání, aktualizacích nebo mazání zavolejte tuto metodu pro kompresi seznamů příspěvků a reorganizaci úložných struktur. Tento krok může zlepšit latenci dotazů až o **30 %** u velkých indexů a pomáhá udržet velikost indexu na zvládnutelné úrovni.

## Běžné případy použití
- **Právní repozitáře dokumentů:** Přidávejte, aktualizujte a odstraňujte spisové soubory při zachování vysoké relevance pro vyhledávání klíčových slov.  
- **Podnikové znalostní báze:** Udržujte interní manuály, politiky a FAQ prohledávatelné, jak se vyvíjejí.  
- **E‑commerce katalogy:** Indexujte specifikace produktů a odstraňujte vyřazené položky bez výpadku.

## Řešení problémů a tipy
- **Profesionální tip:** Dávkově přidávejte dokumenty během mimošpičkových hodin, aby se předešlo výkyvům výkonu.  
- **Nevýhoda:** Vynechání `optimize()` po masivních mazáních může vést k fragmentovaným indexům a pomalejším dotazům.  
- **Zpracování chyb:** Zabalte všechny operace s indexem do `try‑catch` bloků, aby se elegantně ošetřila `IndexException`.  
- **Tip pro výkon:** Použijte `IndexSettings` k ladění využití paměti při práci s velmi velkými datovými sadami (např. nastavte `maxMemoryUsage` na vyšší hodnotu na serverech s dostatkem RAM).  
- **Bezpečnost paměti:** Pro soubory větší než 500 MB zvažte streamování vstupu do `addDocument`, aby byl otisk haldy JVM nízký.

## Často kladené otázky

**Q: Jak mohu odstranit dokumenty z indexu?**  
A: Zavolejte `deleteDocument(documentId)` s unikátním identifikátorem; položka je okamžitě vymazána a úložný prostor je uvolněn.

**Q: Mohu upravit atributy dokumentu pro zlepšení přesnosti vyhledávání?**  
A: Ano, můžete nastavit vlastní metadata (např. kategorie, autor) pomocí API atributů objektu `Document` před jeho přidáním do indexu.

**Q: Existuje „tutorial pro vyhledávací index“ pro začátečníky?**  
A: Oficiální dokumentace GroupDocs.Search obsahuje krok‑za‑krokem tutorial, který pokrývá vytvoření indexu, přidání dokumentů a provádění dotazů.

**Q: Podporuje GroupDocs.Search rozpoznávání homofonů?**  
A: Knihovna zahrnuje jazykové funkce, které zlepšují přesnost pro homofony a podobně znějící slova.

**Q: Jaká verze Javy je vyžadována pro nejnovější GroupDocs.Search?**  
A: Je vyžadována Java 8 nebo novější; knihovna je plně kompatibilní s Java 11 a novějšími LTS verzemi.

## Dostupné tutoriály

### [Jak aktualizovat a spravovat verze indexu v GroupDocs.Search pro Java&#58; Komplexní průvodce](./guide-updating-index-versions-groupdocs-search-java/)
Naučte se efektivně aktualizovat a spravovat verze indexu pomocí GroupDocs.Search pro Java. Tento průvodce pokrývá indexování dokumentů, aktualizace verzí a optimalizaci výkonu.

### [Mistrovská správa dokumentů s GroupDocs.Search pro Java&#58; Průvodce rozpoznáváním homofonů a indexací](./groupdocs-search-java-homophone-document-management-guide/)
Naučte se spravovat dokumenty pomocí GroupDocs.Search pro Java, se zaměřením na rozpoznávání homofonů a efektivní indexaci. Zvyšte přesnost vyhledávání a výkon.

### [Mistrovství v atributech dokumentů s GroupDocs.Search v Javě pro vylepšené indexování a správu](./groupdocs-search-java-modify-attributes-indexing/)
Naučte se dynamicky upravovat a přidávat atributy dokumentů pomocí GroupDocs.Search pro Java. Vylepšete svůj systém správy dokumentů tím, že ovládnete techniky indexování.

### [Mistrovství v GroupDocs.Search v Javě&#58; Kompletní průvodce správou indexu a vyhledáváním dokumentů](./mastering-groupdocs-search-java-index-management-guide/)
Naučte se efektivně spravovat indexy dokumentů pomocí GroupDocs.Search pro Java. Rozšiřte své vyhledávací možnosti napříč různými dokumenty, od právních papírů po obchodní zprávy.

## Další zdroje

- [Dokumentace GroupDocs.Search pro Java](https://docs.groupdocs.com/search/java/)
- [Reference API GroupDocs.Search pro Java](https://reference.groupdocs.com/search/java/)
- [Stáhnout GroupDocs.Search pro Java](https://releases.groupdocs.com/search/java/)
- [Fórum GroupDocs.Search](https://forum.groupdocs.com/c/search)
- [Bezplatná podpora](https://forum.groupdocs.com/)
- [Dočasná licence](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2026-10-12  
**Testováno s:** GroupDocs.Search pro Java 23.11  
**Autor:** GroupDocs

## Související tutoriály

- [Jak aktualizovat index v Javě s GroupDocs.Search – Kompletní průvodce](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Jak vytvořit index dokumentů a přidávat dokumenty pomocí GroupDocs.Search API pro Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Jak přidat více aliasů a přidávat dokumenty do indexu v GroupDocs.Search pro Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)