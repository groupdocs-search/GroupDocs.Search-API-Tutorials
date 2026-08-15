---
date: '2026-08-15'
description: Scopri come migliorare search latency utilizzando le funzionalità di
  indicizzazione avanzata di GroupDocs.Search for Java, inclusi cancellation, async
  operations, multithreading e metadata customization.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: Migliora search latency con GroupDocs.Search for Java utilizzando
  cancellation, asynchronous indexing, multithreading e metadata customization. Incrementa
  performance e riduci resource use.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: Migliora search latency con l'indicizzazione avanzata in GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: Migliora search latency con l'indicizzazione avanzata in GroupDocs
type: docs
url: /it/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Migliora la latenza di ricerca con l'indicizzazione avanzata in GroupDocs

Nell'attuale ambiente digitale frenetico, **migliorare la latenza di ricerca** è essenziale per fornire risultati istantanei agli utenti. Che tu stia costruendo un motore di ricerca personalizzato o migliorando un sistema di gestione documenti esistente, la giusta strategia di indicizzazione può ridurre drasticamente la latenza, diminuire il consumo di risorse e **migliorare la latenza di ricerca** in tutti gli ambiti. In questo tutorial esamineremo le funzionalità più potenti di GroupDocs.Search per Java—cancellazione, indicizzazione asincrona, multithreading e personalizzazione dei metadati—così potrai **aggiungere documenti all'indice** più velocemente e in modo più efficiente.

**Cosa imparerai**

- Come annullare un'operazione di indicizzazione dopo un tempo specificato  
- Eseguire operazioni di indicizzazione asincrona e gestire i cambiamenti di stato  
- Configurare il multithreading per un'indicizzazione più veloce  
- Personalizzare le opzioni di indicizzazione dei metadati per **personalizzare i metadati di ricerca**  

Assicuriamoci che tu abbia tutto il necessario prima di immergerci nel codice.

## Risposte rapide
- **Cosa fa la cancellazione?** Interrompe l'indicizzazione dopo un timeout impostato, liberando CPU e memoria per altri compiti.  
- **Posso indicizzare i documenti in modo asincrono?** Sì – abilitalo con `options.setAsync(true)`.  
- **Quanti thread posso usare?** Qualsiasi intero positivo; 2‑4 thread sono tipici per la maggior parte dei server.  
- **L'indicizzazione dei metadati è opzionale?** Assolutamente – puoi abilitarla o regolarla per campo.  
- **Ho bisogno di una licenza per queste funzionalità?** Una versione di prova è sufficiente per i test; è necessaria una licenza completa per la produzione.

## Prerequisiti

- **Libreria GroupDocs.Search** – versione 25.4 o successiva.  
- **Ambiente di sviluppo Java** – JDK 8 o superiore è consigliato.  
- Familiarità di base con Java e il concetto di indicizzazione.

### Configurazione di GroupDocs.Search per Java

#### Installazione Maven

Aggiungi il repository e la dipendenza al tuo file `pom.xml`:

`pom.xml` configuration tells Maven which GroupDocs.Search artifacts to download and include in your project.

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

#### Download diretto

In alternativa, scarica l'ultimo JAR da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**Acquisizione della licenza** – Inizia con una prova gratuita o richiedi una licenza temporanea per sbloccare l'intero set di funzionalità.

### Inizializzazione e configurazione di base

La classe `SearchIndex` è il punto di ingresso che rappresenta un indice ricercabile memorizzato su disco o in memoria.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## Cosa significa “ottimizzare le prestazioni di ricerca” in questo contesto?

Ottimizzare le prestazioni di ricerca significa configurare il processo di indicizzazione in modo che consumi la giusta quantità di CPU, memoria e tempo, fornendo al contempo i risultati più pertinenti istantaneamente. Controllando la cancellazione, l'esecuzione asincrona, il threading e la gestione dei metadati, influenzi direttamente la rapidità con cui il motore può **aggiungere documenti all'indice** e rispondere alle query.

## Perché utilizzare le funzionalità di indicizzazione avanzate?

L'indicizzazione asincrona e multithread mantiene la tua applicazione reattiva, mentre la cancellazione previene processi incontrollati. Opzioni di metadati finemente regolate ti permettono di evidenziare le informazioni più importanti, migliorando direttamente la **latenza di ricerca** per gli utenti finali. Inoltre, queste funzionalità riducono i picchi di CPU, diminuiscono la pressione sulla memoria e consentono una scalabilità più fluida quando si gestiscono grandi volumi di documenti.

## Come migliorare la latenza di ricerca con l'indicizzazione avanzata?

Carica la tua istanza `SearchIndex`, configura `IndexingOptions` con impostazioni di cancellazione, asincronia e thread, quindi chiama `index.add(document)` — questa combinazione riduce il tempo totale di indicizzazione fino al 60 % su carichi di lavoro tipici e garantisce che i processi a lunga durata non blocchino altre operazioni. Puoi anche regolare i limiti di indicizzazione dei metadati e monitorare l'avanzamento tramite gli eventi di cambio stato per assicurare che la pipeline rimanga entro i budget di prestazioni.

## Guida all'implementazione

### Proprietà di cancellazione

**Panoramica** – Annulla l'indicizzazione dopo una durata specificata per evitare il consumo eccessivo di risorse.

#### Passo 1: configurare l'ambiente

Crea un'istanza `SearchIndex` che punti alla cartella del tuo indice.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Passo 2: creare le opzioni di indicizzazione con cancellazione

`IndexingOptions` ti consente di specificare come si comporta il motore di indicizzazione.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Punti chiave**

- `setCancellation()` attiva la funzionalità.  
- `cancelAfter(int milliseconds)` definisce il timeout (3 secondi in questo esempio).

### Proprietà asincrona

**Panoramica** – Esegui l'indicizzazione su un thread in background e ascolta i cambiamenti di stato.

#### Passo 1: configurare l'ambiente

Istanzia l'indice e prepara la collezione di documenti.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Passo 2: iscriversi all'evento di cambio stato

L'evento `StatusChanged` ti notifica quando il lavoro di indicizzazione passa da uno stato all'altro.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Passo 3: configurare le opzioni asincrone

Abilita la modalità asincrona così la chiamata restituisce immediatamente e l'elaborazione continua in background.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Proprietà dei thread

**Panoramica** – Accelerare l'indicizzazione sfruttando più core CPU.

#### Passo 1: configurare l'ambiente

Prepara l'indice e assicurati che la JVM abbia sufficiente memoria heap.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Passo 2: configurare il multithreading

Imposta il numero di thread di lavoro; ogni thread elabora un sottoinsieme di documenti.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Proprietà delle opzioni di indicizzazione dei metadati

**Panoramica** – Regola finemente quali metadati del documento vengono indicizzati e come vengono memorizzati.

#### Passo 1: configurare l'ambiente

Carica un documento che contiene campi di metadati come autore, titolo e tag personalizzati.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Passo 2: configurare le opzioni dei metadati

`MetadataIndexingOptions` ti consente di abilitare o disabilitare singoli campi di metadati e definire limiti di dimensione.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Applicazioni pratiche

1. **Sistemi di gestione documenti** – Usa l'indicizzazione asincrona per mantenere l'interfaccia utente reattiva mentre grandi lotti vengono elaborati in background.  
2. **Motori di ricerca di contenuti** – Applica la cancellazione per impedire che lavori a lunga durata monopolizzino le risorse del server durante i picchi di traffico.  
3. **Pipeline di ingestione su larga scala** – Sfrutta il multithreading per **aggiungere documenti all'indice** su larga scala, riducendo drasticamente il tempo di elaborazione.  

## Considerazioni sulle prestazioni

- **Gestione dei thread** – Monitora l'uso della CPU; troppi thread possono causare overhead di cambio contesto.  
- **Impronta di memoria** – I limiti dei metadati (ad esempio, `setMaxBytesToIndexField`) mantengono prevedibile l'uso della memoria.  
- **Garbage collection** – Usa flag JVM appropriati (`-Xmx`, `-XX:+UseG1GC`) quando indicizzi corpora massivi.  

## Problemi comuni e soluzioni

| Sintomo | Probabile causa | Soluzione |
|---------|----------------|-----------|
| L'indicizzazione non termina mai | Cancellazione impostata troppo bassa | Aumenta il valore di `cancelAfter` o rimuovi la cancellazione per lavori lunghi |
| Nessun aggiornamento di stato in modalità asincrona | Gestore eventi non collegato correttamente | Assicurati che `index.getEvents().StatusChanged.add(...)` sia chiamato prima di `index.add` |
| Errori di out‑of‑memory | Troppi thread o limiti di metadati elevati | Riduci `options.setThreads` e abbassa i limiti dei campi di metadati |
| Metadati mancanti nei risultati | Indicizzazione dei metadati disabilitata | Verifica che `options.getMetadataIndexingOptions()` sia configurato e non impostato per ignorare i campi |

## Domande frequenti

**Q: Come posso ottenere una licenza temporanea per GroupDocs.Search?**  
A: Visita la [pagina della licenza temporanea di GroupDocs](https://purchase.groupdocs.com/temporary-license/) e segui le istruzioni sullo schermo.

**Q: Posso annullare un'operazione di indicizzazione a metà?**  
A: Sì – usa la proprietà di cancellazione con `cancelAfter()` o invoca `Cancellation.cancel()` programmaticamente.

**Q: Quali sono alcuni casi d'uso per l'indicizzazione asincrona?**  
A: Recupero di documenti in tempo reale, elaborazione batch in background e applicazioni con interfaccia utente reattiva beneficiano dell'indicizzazione asincrona.

**Q: È sicuro aumentare il numero di thread su un server condiviso?**  
A: Aumenta gradualmente e monitora il carico CPU; in ambienti fortemente condivisi, mantieni il numero di thread moderato (2‑4).

**Q: Come influisce l'indicizzazione dei metadati sulla pertinenza della ricerca?**  
A: I metadati indicizzati correttamente (autore, data di creazione, tag) possono avere un peso maggiore nelle query, migliorando l'accuratezza dei risultati.

## Conclusione

Adottando queste funzionalità avanzate di GroupDocs.Search per Java, **migliorerai la latenza di ricerca** in una varietà di scenari—dall'ingestione rapida di documenti al controllo fine dei metadati. Sperimenta con diverse configurazioni, monitora l'uso delle risorse e adatta le impostazioni al tuo carico di lavoro specifico per ottenere i migliori risultati.

---

**Ultimo aggiornamento:** 2026-08-15  
**Testato con:** GroupDocs.Search 25.4 per Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Migliora le prestazioni delle query con GroupDocs.Search Java: Ottimizza indice e ricerca](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Come aggiungere documenti all'indice con indicizzazione dei metadati in Java usando GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Come aggiungere più alias e aggiungere documenti all'indice in GroupDocs.Search per Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)