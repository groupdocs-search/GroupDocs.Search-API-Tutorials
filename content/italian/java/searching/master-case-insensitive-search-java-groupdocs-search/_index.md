---
date: '2026-07-31'
description: Scopri come implementare la ricerca senza distinzione tra maiuscole e
  minuscole in Java aggiungendo documenti a un indice con GroupDocs.Search, usando
  la sostituzione dei caratteri per normalizzare il testo durante l'indicizzazione.
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: La ricerca senza distinzione tra maiuscole e minuscole in Java ti
  consente di aggiungere documenti a un indice e interrogarli senza preoccuparti del
  caso delle lettere. Questa guida mostra come GroupDocs.Search normalizza il testo
  durante l'indicizzazione per risultati rapidi e affidabili.
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Ricerca senza distinzione tra maiuscole e minuscole in Java – Indicizza
  documenti con GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: Aggiungi documenti all'indice per la ricerca senza distinzione tra maiuscole
  e minuscole in Java
type: docs
url: /it/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# Aggiungere Documenti all'Indice per la Ricerca Case‑Insensitive in Java

Quando hai bisogno di **case insensitive search java** che trovi in modo affidabile le informazioni indipendentemente da come gli utenti le digitano, la chiave è aggiungere documenti a un indice normalizzando il testo. In questo tutorial vediamo come configurare GroupDocs.Search per Java in modo che ogni documento indicizzato venga automaticamente convertito in minuscolo (o trasformato in altro modo) durante l'indicizzazione, garantendo risultati case‑insensitive senza logica aggiuntiva al momento della query.

## Risposte Rapide
- **Cosa significa “add documents to index”?** Significa caricare i file sorgente in una struttura dati ricercabile così che possano essere interrogati in seguito.  
- **Perché usare la sostituzione dei caratteri?** Normalizza ogni carattere — tipicamente in minuscolo — così le ricerche ignorano automaticamente le differenze di maiuscole/minuscole.  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per lo sviluppo; è necessaria una licenza completa per le distribuzioni in produzione.  
- **Quale versione di Java è richiesta?** Java 8 o successiva; la libreria è ottimizzata per Java 11+ per prestazioni ottimali.  
- **Posso passare a una ricerca case‑sensitive quando necessario?** Sì — le opzioni di ricerca consentono di attivare/disattivare la sensibilità al maiuscolo per ogni query.

## Che cosa significa “add documents to index” in GroupDocs.Search?

Carica i tuoi file sorgente (PDF, DOCX, TXT, ecc.) in un indice ricercabile affinché il motore possa recuperarli rapidamente. Aggiungere documenti a un indice analizza ogni file, estrae il testo semplice e lo memorizza in una struttura dati ottimizzata che consente ricerche veloci.

## Perché abilitare la sostituzione dei caratteri durante l'indicizzazione?

La sostituzione dei caratteri converte ogni carattere in un equivalente predefinito — più comunemente in minuscolo — mentre l'indice viene costruito. Questo garantisce che le variazioni di maiuscole/minuscole, diacritici o simboli specifici della locale non influenzino i risultati della ricerca. Normalizzando il testo al momento dell'indicizzazione, il motore può confrontare le query con un insieme di token coerente, fornendo un comportamento case‑insensitive rapido e affidabile senza elaborazioni aggiuntive per ogni ricerca.

## Prerequisiti
- **GroupDocs.Search for Java** versione 25.4 o successiva (la libreria supporta oltre 30 formati di file e può indicizzare documenti di centinaia di pagine senza caricare l'intero file in memoria).  
- **Java Development Kit (JDK)** 8 o successivo installato.  
- Familiarità di base con **Maven** (o capacità di aggiungere JAR manualmente).  

## Configurazione di GroupDocs.Search per Java

### Configurazione Maven
Aggiungi il repository GroupDocs e la dipendenza al tuo `pom.xml`:

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

### Download Diretto
Se preferisci non usare Maven, scarica l'ultimo JAR dal sito ufficiale: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della Licenza
- **Free Trial** – scarica una licenza di prova per iniziare a sperimentare.  
- **Temporary License** – richiedi una licenza di test estesa dal portale GroupDocs.  
- **Full License** – acquista una licenza di produzione quando sei pronto a mettere in produzione.

### Inizializzazione di Base (Creare l'indice)
Il frammento seguente crea una cartella indice e abilita le sostituzioni dei caratteri:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Guida all'Implementazione

### Abilitare la Sostituzione dei Caratteri nelle Impostazioni dell'Indice
Attivare questa funzionalità indica al motore di sostituire i caratteri durante l'indicizzazione, che è il passaggio fondamentale per il comportamento case‑insensitive.

#### Passo 1: Configurare `IndexSettings`
`IndexSettings` è l'oggetto di configurazione che controlla come l'indice memorizza e elabora il testo. Impostando `useCharacterReplacements` su **true**, attivi la conversione automatica in minuscolo (o qualsiasi mappatura personalizzata tu fornisca).

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### Configurare le Sostituzioni dei Caratteri
Mappa ogni carattere al suo equivalente minuscolo (o a qualsiasi mappatura personalizzata necessaria).

#### Passo 2: Definire e Aggiungere Coppie di Sostituzione
Il dizionario di sostituzione contiene coppie come `'A' → 'a'`, `'É' → 'e'`, ecc. Aggiungere queste coppie prima dell'indicizzazione garantisce che ogni token sia normalizzato.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Indicizzare Documenti
Ora che l'indice è pronto, puoi **add documents to index** da qualsiasi cartella.

#### Passo 3: Aggiungere Documenti per l'Indicizzazione
GroupDocs.Search scansiona la directory di destinazione, estrae il testo da ogni tipo di file supportato, applica la mappa di sostituzione e scrive i token nello storage dell'indice.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Eseguire una Ricerca Case‑Sensitive (Opzionale)

#### Passo 4: Eseguire Ricerche Case‑Sensitive
`SearchOptions` configura il comportamento della query, ad esempio attivando/disattivando la sensibilità al maiuscolo, consentendo un controllo fine su come vengono eseguite le ricerche.  
`SearchOptions.setUseCaseSensitiveSearch(true)` forza il motore a trattare i caratteri maiuscoli e minuscoli come distinti durante una query specifica, sovrascrivendo il comportamento predefinito case‑insensitive.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## Applicazioni Pratiche
1. **Marketing Campaigns** – Normalizza i nomi dei prodotti affinché i team di vendita possano trovare le risorse senza preoccuparsi delle maiuscole.  
2. **Customer Support** – Alimenta le caselle di ricerca del help‑desk che restituiscono l'articolo corretto sia che l'utente digiti “login” o “Login”.  
3. **E‑commerce Catalogs** – Garantisce che gli acquirenti trovino gli articoli indipendentemente da come digitano i titoli dei prodotti, migliorando i tassi di conversione.

## Considerazioni sulle Prestazioni
- **Organize Source Files** – Una gerarchia di cartelle ordinata riduce il tempo di scansione durante il passaggio **add documents to index**.  
- **Monitor Memory** – Indicizzare grandi corpora può consumare molta RAM; elaborare i file in batch da 500 – 1 000 elementi mantiene l'uso dell'heap sotto controllo.  
- **Asynchronous Indexing** – Quando supportato, esegui l'indicizzazione su un thread in background per mantenere l'interfaccia reattiva ed evitare di bloccare le operazioni dell'utente.

## Problemi Comuni e Risoluzione

| Sintomo | Causa Probabile | Risoluzione |
|---------|-----------------|-------------|
| Nessun risultato restituito per un termine noto | Sostituzioni dei caratteri non abilitate | Verifica `settings.setUseCharacterReplacements(true)` e che la mappa di sostituzione contenga i caratteri necessari. |
| Errore Out‑of‑memory durante l'indicizzazione | Indicizzazione di troppi file grandi contemporaneamente | Indicizza in batch più piccoli o aumenta l'heap JVM (`-Xmx4g`). |
| La ricerca restituisce risultati case‑sensitive inaspettatamente | `SearchOptions.setUseCaseSensitiveSearch(true)` era impostato | Rimuovi o imposta a `false` per il comportamento predefinito case‑insensitive. |
| Il tempo di caricamento dell'indice supera le aspettative | Struttura delle cartelle inefficiente o SSD non utilizzato | Riorganizza i file, elimina i documenti inutilizzati e memorizza l'indice su un SSD veloce. |
| I caratteri speciali vengono ignorati | Mappa di sostituzione priva di voci Unicode | Aggiungi mappature per caratteri come “é”, “ß”, “ø” ai loro equivalenti desiderati. |

## Domande Frequenti

**Q: Come gestisco i caratteri speciali (ad esempio “é”, “ß”) durante l'indicizzazione?**  
A: Includi quei caratteri nella tua mappa di sostituzione, mappandoli ai loro equivalenti ASCII o lasciandoli invariati in base ai requisiti di ricerca.

**Q: Posso limitare la sostituzione dei caratteri a una lingua specifica?**  
A: Sì. Crea un array di sostituzione personalizzato che contenga solo i caratteri della lingua target prima di aggiungerlo al dizionario.

**Q: Cosa devo fare se l'indice impiega molto tempo a caricarsi?**  
A: Ottimizza la struttura delle cartelle, rimuovi i file non necessari e memorizza l'indice su un SSD ad alta velocità. L'indicizzazione incrementale riduce anche il carico di caricamento.

**Q: È possibile annullare le sostituzioni dei caratteri dopo l'indicizzazione?**  
A: No. Le sostituzioni sono incorporate nei dati indicizzati; è necessario ricostruire l'indice con nuove impostazioni per modificarle.

**Q: Dove posso trovare una documentazione API più dettagliata?**  
A: La documentazione ufficiale e il riferimento API forniscono dettagli esaustivi (vedi Risorse sotto).

## Risorse
- [Documentazione](https://docs.groupdocs.com/search/java/)
- [Riferimento API](https://reference.groupdocs.com/search/java)
- [Download GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [Repository GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Forum di Supporto Gratuito](https://forum.groupdocs.com/c/search/10)
- [Informazioni sulla Licenza Temporanea](https://purchase.groupdocs.com/temporary-license/) 

---

**Ultimo Aggiornamento:** 2026-07-31  
**Testato Con:** GroupDocs.Search 25.4 per Java  
**Autore:** GroupDocs  

---

## Tutorial Correlati

- [Sostituzione dei Caratteri in GroupDocs.Search Java: Guida Completa per Migliorare la Ricerca Testuale e l'Indicizzazione](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [Aggiungere documenti all'indice: ricerca Java case‑sensitive con GroupDocs](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [Come Aggiungere Documenti all'Indice con GroupDocs.Search per Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)