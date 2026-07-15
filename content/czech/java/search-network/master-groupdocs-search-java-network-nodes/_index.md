---
date: '2026-07-02'
description: Zjistěte, jak získat dočasnou licenci pro GroupDocs.Search, přidat adresáře
  do indexu a přidat vlastní atributy dokumentu při správě vyhledávacích síťových
  uzlů v Javě.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Získání dočasné licence GroupDocs – Hlavní uzly vyhledávání (Java)
type: docs
url: /cs/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Získání dočasné licence GroupDocs – Hlavní uzly vyhledávání (Java)

V tomto komplexním průvodci **získáte dočasnou licenci pro GroupDocs.Search**, nakonfigurujete víceuzlovou vyhledávací síť a naučíte se **přidávat adresáře do indexu** a **přidávat vlastní atributy dokumentů** pomocí Javy. Ať už budujete podnikovou dokumentační správu nebo prohledávatelný katalog produktů, zvládnutí těchto kroků vám umožní vyhodnotit platformu bez omezení a rychle rozšířit možnosti vyhledávání.

## Rychlé odpovědi
- **Jaký je první krok k zahájení používání GroupDocs.Search?** Získat dočasnou licenci z portálu GroupDocs.  
- **Které Maven úložiště hostuje knihovnu?** `https://releases.groupdocs.com/search/java/`.  
- **Jak přidám adresáře do indexu?** Zavolejte pomocnou metodu `addDirectoriesToIndex` na hlavním uzlu.  
- **Mohu přidat vlastní atributy dokumentu?** Ano—vyvolejte `addAttribute` s klíčem dokumentu a názvem atributu.  
- **Jak čistě vypnout uzly?** Vyvolejte `closeNodes` pro uvolnění prostředků.

## Co je dočasná licence a proč ji potřebuji?
Dočasná licence vám umožní vyhodnotit GroupDocs.Search bez jakýchkoli omezení hodnocení. Je ideální pro vývoj, testování nebo projekty proof‑of‑concept před závazkem k úplnému nákupu. Licence poskytuje plný přístup ke všem funkcím po omezenou dobu, což vám umožní měřit výkon, testovat integrační body a zajistit, že řešení splňuje vaše požadavky bez finančního závazku.

## Předpoklady

Než začneme, ujistěte se, že máte následující předpoklady připravené:

### Požadované knihovny a závislosti
Pro práci s GroupDocs.Search pro Javu zahrňte potřebné Maven závislosti:
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
Můžete také stáhnout nejnovější verzi přímo z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Nastavení prostředí
- Ujistěte se, že máte nainstalovaný kompatibilní JDK (Java 8 nebo novější).  
- Nastavte své IDE tak, aby podporovalo Maven projekty.

### Předpoklady znalostí
Základní pochopení programování v Javě a znalost správy Maven projektů bude užitečná. Pokud jste v těchto konceptech noví, zvažte prozkoumání úvodních zdrojů, abyste mohli začít.

## Jak získat dočasnou licenci
Dočasná licence se získá návštěvou portálu GroupDocs, vyplněním krátkého formuláře a umístěním získaného souboru `.lic` do složky `resources` vašeho projektu. Poté inicializujte licenci pomocí několika řádků kódu (viz úryvek níže). Pro formulář použijte oficiální stránku: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## Nastavení GroupDocs.Search pro Javu

### Informace o instalaci
Pro zahájení používání GroupDocs.Search pro Javu ve vašem projektu postupujte podle výše uvedených Maven kroků nebo stáhněte nejnovější verzi přímo z oficiální stránky vydání.

#### Kroky získání licence
1. **Free Trial** – Prozkoumejte funkce bez jakéhokoli závazku.  
2. **Temporary License** – Získejte krátkodobý klíč pro testování (viz výše).  
3. **Purchase** – Pro produkční použití zakupte plnou licenci na **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)**.

### Základní inicializace a nastavení
Inicializujte svůj projekt s GroupDocs.Search následovně:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Tento krok inicializace je klíčový pro zajištění bezproblémové funkce všech komponent ve vaší vyhledávací síti.

## Průvodce implementací
Nyní rozdělíme proces do zvládnutelných sekcí, z nichž každá se zaměřuje na konkrétní funkci nasazování a správy uzlů vyhledávací sítě.

### Funkce 1: Nastavení konfigurace
**Přehled:** Nastavení konfigurace pro vaši vyhledávací síť je prvním krokem při nasazování uzlů. Toto nastavení zahrnuje určení cest a portů, které jsou kritické pro nasazení uzlů.

#### Implementační kroky:
##### Krok 1: Definujte základní cestu a port
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Krok 2: Nakonfigurujte vyhledávací síť
Funkce `configureSearchNetwork` připravuje konfigurační objekt potřebný pro nasazení uzlů.  
`Configuration` je třída, která obsahuje všechna nastavení, jako je složka indexu, síťové porty a role uzlů.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parametry:** Základní cesta a port se používají k umístění zdrojů a navázání komunikačních kanálů.  
- **Návratová hodnota:** Nakonfigurovaný objekt `Configuration` přizpůsobený vašim nasazovacím potřebám.

### Funkce 2: Nasazení vyhledávací sítě
**Přehled:** Nasazení uzlů je nezbytné pro škálování vašich vyhledávacích schopností napříč různými prostředími nebo segmenty dat.

#### Implementační kroky:
##### Krok 1: Nasadit uzly
Funkce `deploySearchNetwork` inicializuje a vrátí pole uzlů vyhledávací sítě.  
`SearchNetworkNodes` představuje každou instanci uzlu, která se podílí na distribuovaném vyhledávacím clusteru.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parametry:** Základní cesta, port a konfigurace se používají k určení nasazovacího prostředí.  
- **Návratová hodnota:** Pole obsahující inicializované `SearchNetworkNodes`.

### Funkce 3: Přihlášení k událostem sítě
**Přehled:** Monitorování aktivit vaší vyhledávací sítě je klíčové pro udržení optimálního výkonu a spolehlivosti.

#### Implementační kroky:
##### Krok 1: Přihlásit se k událostem hlavního uzlu
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Účel:** Tento krok zajišťuje, že budete upozorněni na významné události nebo změny ve vaší vyhledávací síti.

### Funkce 4: Indexování dokumentů
**Přehled:** Přidání adresářů obsahujících dokumenty k indexování umožňuje efektivní získávání dat napříč vaší sítí.

#### Jak přidat adresáře do indexu
`addDirectoriesToIndex` je pomocná metoda, která registruje cesty ke složkám pro indexování na hlavním uzlu.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Účel:** Umožňuje rychlý přístup a prohledatelnost všech dokumentů ve specifikovaných adresářích.

### Funkce 5: Přidávání atributů k dokumentům
**Přehled:** Vlastní atributy rozšiřují metadata dokumentu, což činí vyhledávání flexibilnějším a informativnějším.

#### Jak přidat vlastní atributy dokumentu
`addAttribute` přidá vlastní metadata atribut ke konkrétnímu dokumentu v indexu.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parametry:** Zadejte uzel, klíč dokumentu a atribut, který má být přidán.  
- **Účel:** Rozšiřuje funkčnost vyhledávání obohacením dokumentů o další metadata.

### Funkce 6: Načítání indexovaných dokumentů
**Přehled:** Efektivně načíst a vypsat indexované dokumenty pro zajištění přesnosti a úplnosti dat.

#### Implementační kroky:
##### Krok 1: Získat indexované dokumenty
```java
getIndexedDocuments(nodes[0]);
```  
- **Účel:** Ověřuje úspěšné indexování všech potřebných dokumentů ve vaší vyhledávací síti.

### Funkce 7: Uzavírání uzlů sítě
**Přehled:** Správné uzavírání uzlů je klíčové pro správu prostředků a předcházení únikům paměti.

#### Implementační kroky:
##### Krok 1: Zavřít všechny uzly
`closeNodes` vypne všechny aktivní vyhledávací uzly a uvolní přidělené prostředky.  
```java
closeNodes(nodes);
```  
- **Účel:** Uvolňuje prostředky obsazené každým uzlem, což zajišťuje čistý proces vypnutí.

## Proč použít dočasnou licenci pro GroupDocs.Search?
Dočasná licence poskytuje **plný přístup ke všem funkcím po 30 dní** a podporuje až **50 000 indexovaných dokumentů** bez omezení výkonu. To vám umožní měřit rychlost indexování, latenci dotazů a škálovatelnost na reálných datech před zakoupením produkční licence. Také odstraňuje vodotisky hodnocení, což vám dává pravdivou představu o schopnostech finálního produktu.

## Běžné případy použití
1. **Enterprise Document Management** – Indexujte miliony interních souborů napříč odděleními, což umožňuje okamžité full‑textové vyhledávání.  
2. **E‑commerce Platforms** – Vytvořte prohledávatelný katalog produktů, který zahrnuje více skladů a externí zdroje.  
3. **Legal Firms** – Organizujte spisové soubory, smlouvy a důkazy s vlastními metadaty pro rychlé vyhledávání.

Možnosti integrace s dalšími systémy zahrnují CRM platformy, systémy pro správu obsahu (CMS) a nástroje pro analýzu dat, využívající robustní funkce indexování a vyhledávání poskytované GroupDocs.Search pro Javu.

## Úvahy o výkonu
Pro optimalizaci výkonu při používání GroupDocs.Search pro Javu:
- **Optimalizujte konfiguraci** – Přizpůsobte nastavení konfigurace vašemu konkrétnímu nasazovacímu prostředí.  
- **Monitorujte využití prostředků** – Pravidelně kontrolujte CPU, paměť a I/O, abyste předešli úzkým hrdlům nebo únikům paměti.  
- **Řiďte se osvědčenými postupy** – Dodržujte pokyny pro správu paměti v Javě, což zajišťuje efektivní využití systémových prostředků.

## Často kladené otázky

**Q: Jak dlouho je dočasná licence platná?**  
A: Dočasné licence jsou obvykle platné 30 dní, což vám poskytuje dostatek času k vyhodnocení produktu.

**Q: Mohu přejít z dočasné licence na plnou licenci bez přeinstalace?**  
A: Ano—nahraďte soubor dočasné licence souborem plné licence a restartujte aplikaci.

**Q: Musím po aplikaci nové licence znovu indexovat dokumenty?**  
A: Ne, index zůstává nedotčen; licence pouze řídí práva k používání.

**Q: Co se stane, když zapomenu uzly zavřít?**  
A: Neuvolněné prostředky mohou vést k únikům paměti; vždy při vypínání vyvolejte `closeNodes`.

**Q: Je možné přidat více než jeden vlastní atribut k dokumentu?**  
A: Rozhodně—voláním `addAttribute` vícekrát s různými názvy atributů.

---

**Poslední aktualizace:** 2026-07-02  
**Testováno s:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs

## Související tutoriály

- [Nasazení uzlu vyhledávací sítě v .NET pomocí GroupDocs pro efektivní indexování a načítání dokumentů](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Jak implementovat vyhledávací síť s GroupDocs.Search v .NET pro systémy správy dokumentů](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Konfigurace Aspose.Search Network a přidání atributů dokumentů s GroupDocs.Redaction pro .NET: komplexní průvodce](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)