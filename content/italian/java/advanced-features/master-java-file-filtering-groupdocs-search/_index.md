---
date: '2026-09-06'
description: Scopri come filtrare le estensioni dei file java utilizzando GroupDocs.Search
  per Java, coprendo gli operatori logici AND, OR, NOT, i filtri di intervallo di
  date e i filtri di percorso.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: Filtra le estensioni dei file java usando GroupDocs.Search. Scopri
  come combinare i filtri di estensione, intervallo di date e percorso con gli operatori
  logici in Java.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: Filtra le estensioni dei file java con GroupDocs.Search – Guida completa
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: Come filtrare le estensioni dei file java con GroupDocs.Search
type: docs
url: /it/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Filtra le estensioni dei file java con GroupDocs.Search

In questo tutorial completo imparerai come **filtrare le estensioni dei file java** durante l'indicizzazione dei documenti con GroupDocs.Search. Alla fine della guida sarai in grado di includere solo i tipi di file di cui hai bisogno, escludere formati indesiderati e combinare queste regole con filtri di intervallo di date e di percorso usando gli operatori logici AND, OR e NOT. Questo approccio mantiene il tuo indice snello, velocizza le ricerche e ti aiuta a rispettare le politiche di gestione dei dati.

## Risposte rapide
- **Che cos'è il filtro di estensione file java?** È una regola che indica a GroupDocs.Search quali estensioni di file includere o escludere durante l'indicizzazione.  
- **Quale libreria fornisce questa funzionalità?** GroupDocs.Search for Java.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per la valutazione; è necessaria una licenza completa per la produzione.  
- **Posso combinare i filtri?** Sì – è possibile concatenare filtri di estensione, data, dimensione e percorso con la logica AND, OR, NOT.  
- **È compatibile con Maven?** Assolutamente – aggiungi la dipendenza GroupDocs.Search al tuo `pom.xml`.

## Cos'è un filtro di estensione file java?
Un **filtro di estensione file java** è un insieme di regole che valuta l'estensione di ogni file prima che venga inviato al motore di indicizzazione. Specificando estensioni come `.txt`, `.pdf` o `.epub`, è possibile **includere file per estensione** o **escludere file per estensione** per mantenere l'indice focalizzato e i risultati di ricerca pertinenti.

## Perché utilizzare il filtraggio delle estensioni dei file con GroupDocs.Search?
Il filtraggio delle estensioni dei file migliora l'efficienza dell'indicizzazione escludendo formati irrilevanti, riduce i requisiti di archiviazione e aiuta a rispettare le norme di conformità impedendo l'ingresso di contenuti indesiderati nell'indice. Consente inoltre risposte più rapide alle query perché il motore di ricerca elabora un set di dati più piccolo e più pertinente.

- **Performance:** Saltare i file indesiderati riduce I/O e velocizza l'indicizzazione fino al 40 % su grandi repository.  
- **Risparmio di spazio:** Solo i documenti pertinenti vengono memorizzati nell'indice, riducendo l'uso del disco di una media del 30 %.  
- **Conformità:** Previene l'indicizzazione accidentale di tipi di file riservati o non supportati.  
- **Flessibilità:** Combinalo con le funzionalità **date range filter java** per mirare ai file creati o modificati entro periodi specifici.

## Prerequisiti

Prima di iniziare, assicurati di avere quanto segue:

### Librerie e dipendenze richieste
- **GroupDocs.Search for Java** – versione 25.4 o successiva (supporta oltre 60 formati di input).  
- **Java Development Kit (JDK)** – qualsiasi versione compatibile (8 o successiva).

### Configurazione dell'ambiente
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse o qualsiasi IDE compatibile con Maven.

### Prerequisiti di conoscenza
- Programmazione Java di base.  
- Familiarità con I/O di file in Java.  
- Comprensione delle espressioni regolari e della gestione di data‑ora.

## Configurazione di GroupDocs.Search per Java
Per iniziare a utilizzare GroupDocs.Search, è necessario includerlo come dipendenza nel tuo progetto.

### Configurazione Maven
Aggiungi la seguente configurazione del repository e della dipendenza al tuo file `pom.xml`:

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

### Download diretto
In alternativa, scarica l'ultima versione direttamente da [Versioni di GroupDocs.Search per Java](https://releases.groupdocs.com/search/java/).

#### Acquisizione della licenza
1. **Prova gratuita** – esplora le funzionalità senza costi.  
2. **Licenza temporanea** – ottieni la funzionalità completa per un periodo limitato.  
3. **Acquisto** – ottieni una licenza permanente per l'uso in produzione.

### Inizializzazione e configurazione di base
Una volta aggiunta la libreria, inizializza il tuo ambiente di indicizzazione. La classe `IndexSettings` contiene tutte le opzioni di configurazione, inclusi i filtri.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Guida all'implementazione
Di seguito approfondiamo ogni tipo di filtro, spiegando **perché è importante** e fornendo istruzioni passo‑passo che puoi copiare nel tuo progetto.

### Filtraggio delle estensioni dei file
Filtra i file per le loro estensioni durante l'indicizzazione. È perfetto quando vuoi elaborare solo e‑book (`.fb2`, `.epub`) e file di testo semplice (`.txt`).

#### Panoramica
`DocumentFilter.createFileExtension` crea una whitelist di estensioni.

#### Passaggi di implementazione
1. **Crea filtro** – definisci le estensioni che desideri mantenere.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Inizializza l'indice e aggiungi i documenti** – applica il filtro durante la costruzione di `IndexSettings`.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtro LOGICO NOT
Escludi estensioni specifiche, come pagine web e PDF, quando non sono necessarie per il tuo scenario di ricerca.

#### Passaggi di implementazione
1. **Crea filtro di esclusione** – specifica le estensioni da rifiutare.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Applica alle impostazioni dell'indice** – combina il filtro NOT con altre regole.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Aggiungi documenti** – solo i file che superano il filtro combinato vengono indicizzati.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtro LOGICO AND
Combina diverse condizioni—data di creazione, estensione e dimensione del file—così che **solo i file che soddisfano tutti i criteri** vengano indicizzati.

#### Panoramica
`DocumentFilter.createAnd` unisce più filtri in un'unica regola.

#### Passaggi di implementazione
1. **Definisci filtri** – crea filtri individuali per ogni condizione.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combina i filtri** – usa l'operatore AND per richiedere tutte le condizioni.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Indicizza i documenti** – passa il filtro combinato al pipeline di indicizzazione.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtro LOGICO OR
Includi i file che soddisfano **qualsiasi** delle condizioni specificate—utile quando vuoi catturare sia piccoli file di testo sia file non‑testo più grandi.

#### Passaggi di implementazione
1. **Definisci filtri** – crea filtri separati per ogni condizione alternativa.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combina i filtri con condizioni logiche** – usa l'operatore OR.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalizza il filtro OR** – allega il filtro combinato alla configurazione dell'indice.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtri per data di creazione
Seleziona i file creati entro un periodo specifico—uno scenario classico di **date range filter java**.

#### Passaggi di implementazione
1. **Definisci filtro di intervallo di date** – specifica le date di inizio e fine.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Indicizza i documenti** – solo i file i cui timestamp di creazione rientrano nell'intervallo vengono indicizzati.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtri per data di modifica
Escludi i file che sono stati modificati dopo una certa data di cut‑off.

#### Passaggi di implementazione
1. **Definisci filtro** – imposta il timestamp massimo di modifica.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Indicizza i documenti** – i file più recenti della data di cut‑off vengono ignorati.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtraggio del percorso dei file
Limita l'indicizzazione ai file situati in cartelle specifiche o che corrispondono a un modello—ideale per **include files by extension** all'interno di una gerarchia di directory specifica.

#### Passaggi di implementazione
1. **Definisci filtro di percorso file** – usa pattern glob o regex per corrispondere alle directory.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Inizializza l'indice e aggiungi i documenti** – applica il filtro di percorso insieme ad altre regole.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Problemi comuni e consigli

- **Non mescolare mai percorsi assoluti e relativi** nella stessa configurazione di filtro – può portare a esclusioni inattese.  
- **Reimposta `IndexSettings`** quando cambi set di filtri; altrimenti i filtri precedenti potrebbero persistere.  
- **Combina un limite superiore di lunghezza con un filtro di estensione** per grandi collezioni per mantenere basso l'uso della memoria.  
- LoggingOptions controlla la configurazione del logging per GroupDocs.Search.  
- **Abilita il logging** (`LoggingOptions.setEnabled(true)`) per vedere perché un file è stato rifiutato.  

## Domande frequenti

**D: Posso modificare i criteri del filtro dopo la creazione dell'indice?**  
R: Sì. Ricostruisci l'indice con un nuovo `DocumentFilter` o utilizza l'indicizzazione incrementale con impostazioni aggiornate.

**D: Il filtro di estensione file java funziona su archivi compressi (ad esempio, ZIP)?**  
R: GroupDocs.Search può indicizzare i formati di archivio supportati, ma il filtro di estensione si applica all'archivio stesso, non ai file interni. Usa filtri annidati per un controllo più approfondito.

**D: Come posso debugare perché un file particolare è stato escluso?**  
R: Abilita il logging della libreria (`LoggingOptions.setEnabled(true)`) e ispeziona il log – segnala quale filtro ha rifiutato ogni file.

**D: È possibile combinare il filtro di estensione file java con filtri regex personalizzati?**  
R: Assolutamente. Avvolgi un filtro regex all'interno di `DocumentFilter.createAnd()` insieme al filtro di estensione.

**D: Qual è l'impatto sulle prestazioni dell'aggiunta di molti filtri?**  
R: Ogni filtro aggiunge un modesto overhead durante l'indicizzazione, ma la riduzione dei dati indicizzati solitamente supera il costo. Testa con un campione rappresentativo per trovare il bilancio ottimale.

---

**Ultimo aggiornamento:** 2026-09-06  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Formato data personalizzato Java | Ricerca per intervallo di date con GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: Ricerca booleana avanzata con GroupDocs.Search per Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Ottimizza le prestazioni di ricerca con tecniche di indicizzazione avanzate in GroupDocs.Search per Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}