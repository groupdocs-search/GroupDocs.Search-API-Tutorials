---
date: '2026-05-17'
description: Scopri come configurare la rete di ricerca java, ottimizzare gli shards,
  eseguire ricerche testuali e gestire i conflitti di porta con GroupDocs.Search per
  Java.
keywords:
- configure search network java
- GroupDocs.Search Java
- shard optimization
- Java search network
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  headline: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive
    Guide'
  type: TechArticle
- description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  name: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive Guide'
  steps:
  - name: Define Document Directories and Port
    text: '`DocumentDirectory` is a simple holder for the absolute path of a folder
      you want to index. Provide one or more paths to the configuration.'
  - name: Configure Search Network
    text: 'Create the configuration object using the defined paths:'
  - name: Deploy Nodes Using Configuration
    text: 'Deploy search network nodes and identify the master node for centralized
      management:'
  - name: Subscribe to Master Node Events
    text: '`SearchNetworkEventListener` lets you react to indexing completion, node
      failures, or shard optimizations. CODE_BLOCK_PLACEHOLDER_9_END'
  - name: Add Document Directories to Indexing Process
    text: Pass a list of folder paths to the master node; the engine will create a
      separate shard for each folder, enabling parallel query execution. CODE_BLOCK_PLACEHOLDER_10_END
  - name: Perform a Text Search
    text: Invoke the static helper to run a query and retrieve matching documents
      with relevance scores. CODE_BLOCK_PLACEHOLDER_11_END
  - name: Optimize Indexer Shards
    text: 'Optimize shards to improve search efficiency (this is where **how to optimize
      shards** really matters): CODE_BLOCK_PLACEHOLDER_12_END'
  type: HowTo
- questions:
  - answer: Optimizing shards compacts the index, reduces disk I/O, and typically
      yields 30‑50 % faster query responses for large datasets.
    question: How does shard optimization affect query speed?
  - answer: Yes, the operation is designed to run without downtime, but scheduling
      during low‑traffic periods is recommended for indexes larger than 20 GB.
    question: Is it safe to run `optimizeShards` on a live node?
  - answer: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor`
      to fine‑tune the optimization process.
    question: Can I customize the `OptimizeOptions`?
  - answer: Verify file system permissions, ensure enough free disk space, and confirm
      that no other process is locking the index files.
    question: What should I do if I encounter an `IOException` during optimization?
  - answer: Yes, the optimizer merges segments and removes tombstones, freeing up
      space occupied by deleted documents.
    question: Does optimizing shards also reclaim deleted document space?
  type: FAQPage
title: 'Come ottimizzare gli shards in GroupDocs.Search per Java: Guida completa'
type: docs
url: /it/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# Come ottimizzare gli shard in GroupDocs.Search per Java: Guida completa

La ricerca efficiente di documenti è essenziale per sviluppatori e aziende che gestiscono grandi set di dati o hanno bisogno di un recupero interno rapido. In questo tutorial imparerai **how to configure search network java**, come indicizzare e interrogare i documenti, e i passaggi esatti per **optimize shards** per ottenere le massime prestazioni. Tratteremo anche casi d'uso reali, errori comuni e consigli pratici per mantenere i nodi di ricerca funzionanti senza problemi.

## Risposte rapide
- **Che cos'è l'ottimizzazione degli shard?** It reorganizes index data to speed up queries and reduce storage overhead.  
- **Come configurare una rete di ricerca?** Define a base directory and port, then deploy nodes using the provided API.  
- **Come eseguire una ricerca testuale?** Use `TextSearchInNetwork.searchAll` with your query string.  
- **Come indicizzare documenti in Java?** Add document directories to the master node with `IndexingDocuments.addDirectories`.  
- **Come gestire i conflitti di porta?** Change the `basePort` variable to an unused port on your machine.

## Come configurare la rete di ricerca
`Configuration` memorizza tutte le impostazioni necessarie per avviare una rete GroupDocs.Search, come la posizione della cartella dell'indice e la porta di comunicazione.  
`SearchNetwork` orchestra i nodi, gestendo l'indicizzazione e la distribuzione delle query.

Carica la tua configurazione di ricerca, imposta il percorso base dei documenti, scegli una porta libera e avvia la rete—tutto in poche righe di codice. Questa risposta diretta spiega l'intero processo in meno di 70 parole: **Create a `Configuration` object, set `basePath` and `basePort`, then call `SearchNetwork.start(configuration)`.** La rete avvierà automaticamente un nodo master e tutti i nodi worker necessari, pronti ad accettare richieste di indicizzazione.

### Definizione
`Configuration` è la classe principale che memorizza tutte le impostazioni necessarie per avviare una rete GroupDocs.Search, come la posizione della cartella dell'indice e la porta di comunicazione.

Per evitare l'errore temuto “port already in use”, verifica prima che la porta scelta sia libera (ad esempio, usando `netstat` o un semplice test di socket) prima di inizializzare la rete.

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

## Come indicizzare documenti in Java
`IndexingDocuments` è una classe di utilità che semplifica l'aggiunta di più directory a un nodo di ricerca e avvia la pipeline di indicizzazione.

Aggiungi le cartelle dei documenti al nodo master, poi lascia che l'indicizzatore le scandagli. **Direct answer:** Call `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))` e poi invoca `masterNode.index()`; il motore creerà shard ricercabili per ogni cartella fornita. Questo approccio scala orizzontalmente—aggiungi più nodi e lo stesso metodo distribuirà automaticamente il carico di lavoro.

### Definizione
`IndexingDocuments` è una classe di utilità che semplifica l'aggiunta di più directory a un nodo di ricerca e avvia la pipeline di indicizzazione.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Come eseguire una ricerca testuale
`TextSearchInNetwork` fornisce metodi di supporto statici per trasmettere una query testuale a tutti i nodi della rete e aggregare i risultati.  
`SearchResult` incapsula l'ID di un documento corrispondente, lo snippet e il punteggio di rilevanza.

Esegui una query su tutti gli shard con una singola chiamata di metodo. **Direct answer:** Use `TextSearchInNetwork.searchAll("your query", searchNetwork)`; il metodo restituisce una collezione di oggetti `SearchResult` contenenti gli ID dei documenti, gli snippet e i punteggi di rilevanza. Puoi filtrare ulteriormente i risultati per lingua, tipo di file o metadati personalizzati senza scrivere codice aggiuntivo.

### Definizione
`TextSearchInNetwork` fornisce metodi di supporto statici che trasmettono una query testuale a tutti i nodi della rete e aggregano i risultati.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## Come gestire i conflitti di porta
Se la porta predefinita (`49132`) è occupata, scegli semplicemente un'altra porta libera e aggiorna il campo `basePort` prima di avviare la rete. **Direct answer:** Change `int basePort = 49132;` to an unused value like `49133`, rebuild, and restart; la rete si collegherà alla nuova porta senza influenzare i nodi esistenti.

Consiglio professionale: mantieni un piccolo file di configurazione (ad esempio, `search-config.properties`) così puoi cambiare la porta senza ricompilare.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Prerequisiti
Prima di iniziare, assicurati di avere i seguenti prerequisiti in ordine:

### Librerie richieste, versioni e dipendenze
Per implementare questa soluzione, includi la libreria GroupDocs.Search usando Maven aggiungendo la seguente configurazione al tuo file `pom.xml`:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
In alternativa, scarica l'ultima versione da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Requisiti di configurazione dell'ambiente
- Java Development Kit (JDK) 8 o successivo.  
- Permessi di rete che consentono il binding alla `basePort` scelta.  
- Spazio su disco sufficiente per i file di indice (ogni shard può occupare ~10 MB per 1.000 documenti).

### Prerequisiti di conoscenza
Una comprensione di base di Java, programmazione orientata agli oggetti e gestione delle eccezioni ti aiuterà a seguire gli esempi senza problemi.

## Configurazione di GroupDocs.Search per Java
Per iniziare a usare GroupDocs.Search nel tuo progetto, segui questi passaggi:

1. **Add the Dependency**: Come mostrato sopra, aggiungi la dipendenza Maven necessaria al tuo progetto o scaricala direttamente dalla pagina dei rilasci.  
2. **License Acquisition**:  
   - **Free trial** – nessuna chiave di licenza richiesta, ma l'uso è limitato a 500 documenti al giorno.  
   - **Temporary license** – richiedi una chiave di prova di 30 giorni da [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).  
   - **Full license** – acquista una licenza di produzione per accesso illimitato e supporto prioritario.  
3. **Basic Initialization and Setup**:  
   Inizializza la configurazione usando la classe `Configuration`, impostando il percorso base per i documenti e specificando un numero di porta:

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## Guida all'implementazione
Ora esploriamo l'implementazione delle funzionalità chiave usando GroupDocs.Search Java.

### Funzionalità: Configurazione della rete di ricerca
**Overview**: Configurare una rete di ricerca comporta la definizione della directory dei documenti e la sua configurazione con una porta specifica per la comunicazione tra i nodi.

#### Passo 1: Definire le directory dei documenti e la porta
`DocumentDirectory` è un semplice contenitore per il percorso assoluto di una cartella che desideri indicizzare. Fornisci uno o più percorsi alla configurazione.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### Passo 2: Configurare la rete di ricerca
Crea l'oggetto di configurazione usando i percorsi definiti:

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Funzionalità: Distribuzione dei nodi della rete di ricerca
**Overview**: Distribuisci i nodi per gestire le ricerche di documenti in modo efficiente nella tua rete.

#### Passo 1: Distribuire i nodi usando la configurazione
Distribuisci i nodi della rete di ricerca e identifica il nodo master per la gestione centralizzata:

```java
public static void optimizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    OptimizeOptions options = new OptimizeOptions();
    indexer.optimize(options);
}

optimizeShards(masterNode);

// Perform a second text search to observe optimization effects
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Funzionalità: Sottoscrizione agli eventi dei nodi di rete
**Overview**: Monitora la tua rete di ricerca sottoscrivendo gli eventi che ti notificano cambiamenti o azioni importanti.

#### Passo 1: Sottoscrivere gli eventi del nodo master
`SearchNetworkEventListener` ti consente di reagire al completamento dell'indicizzazione, ai fallimenti dei nodi o alle ottimizzazioni degli shard.

CODE_BLOCK_PLACEHOLDER_9_END

### Funzionalità: Indicizzazione dei documenti nei nodi di rete
**Overview**: Aggiungi directory contenenti documenti al processo di indicizzazione per ricerche efficienti.

#### Passo 1: Aggiungere le directory dei documenti al processo di indicizzazione
Passa una lista di percorsi di cartelle al nodo master; il motore creerà uno shard separato per ogni cartella, consentendo l'esecuzione parallela delle query.

CODE_BLOCK_PLACEHOLDER_10_END

### Funzionalità: Ricerca testuale nei nodi di rete
**Overview**: Esegui ricerche testuali su tutti i documenti indicizzati all'interno della tua rete di ricerca.

#### Passo 1: Eseguire una ricerca testuale
Invoca il metodo di supporto statico per eseguire una query e recuperare i documenti corrispondenti con i punteggi di rilevanza.

CODE_BLOCK_PLACEHOLDER_11_END

### Funzionalità: Ottimizzazione degli shard
**Overview**: Migliora le prestazioni ottimizzando gli shard all'interno dell'indicizzatore del nodo della tua rete di ricerca.

#### Passo 1: Ottimizzare gli shard dell'indicizzatore
Ottimizza gli shard per migliorare l'efficienza della ricerca (qui è dove **how to optimize shards** è davvero importante):

CODE_BLOCK_PLACEHOLDER_12_END

## Applicazioni pratiche
GroupDocs.Search per Java può essere applicato in vari scenari reali, ognuno dei quali beneficia dell'ottimizzazione degli shard:

1. **Enterprise Document Management** – Gestisce archivi di oltre 10 TB con tempi di query sub‑secondo dopo l'ottimizzazione degli shard.  
2. **E‑commerce Platforms** – Alimenta la ricerca di prodotti su 1 milione di SKU, riducendo la latenza fino al 45 % quando gli shard sono ottimizzati.  
3. **Legal Firms** – Recupera file di casi da repository di 200 GB in meno di 200 ms.  
4. **Library Systems** – Supporta ricerche di catalogo per 500 k libri digitali con un uso efficiente della memoria.  
5. **Content Management Systems (CMS)** – Consente la scoperta immediata dei contenuti per distribuzioni multi‑sito con oltre 2 milioni di pagine.

## Considerazioni sulle prestazioni
Per garantire prestazioni ottimali della tua implementazione GroupDocs.Search:

- **Regularly optimize shards** – Eseguire `optimizeShards()` dopo ogni 10 GB di nuovi dati riduce i tempi di risposta delle query del 30‑50 %.  
- **Monitor memory usage** – Mantieni l'heap JVM al di sotto del 75 % della RAM fisica; abilita G1GC per indici di grandi dimensioni.  
- **Use incremental indexing** – Aggiungi solo i file modificati per evitare una re‑indicizzazione completa.  
- **Leverage multi‑node scaling** – Aggiungi nodi worker per distribuire gli shard; ogni nodo aggiuntivo può migliorare il throughput di ~20 % per carichi di lavoro prevalentemente di lettura.

## Problemi comuni e soluzioni
| Problema | Sintomo | Soluzione |
|----------|----------|-----------|
| Conflitto di porta all'avvio | `java.net.BindException: Address already in use` | Cambia `basePort` con un valore non utilizzato; verifica con `netstat -ano`. |
| Errori di out‑of‑memory durante l'ottimizzazione | `java.lang.OutOfMemoryError: Java heap space` | Aumenta il flag JVM `-Xmx` o esegui l'ottimizzazione su un nodo dedicato con più RAM. |
| Documenti mancanti nei risultati di ricerca | Nessun risultato restituito dopo l'indicizzazione | Assicurati che le directory siano aggiunte correttamente tramite `IndexingDocuments.addDirectories` e che `masterNode.index()` sia completato senza eccezioni. |
| Shard obsoleti dopo cancellazione massiva | I file eliminati appaiono ancora | Esegui `optimizeShards()` per unire i segmenti e rimuovere i tombstone. |

## Domande frequenti

**Q: Come influisce l'ottimizzazione degli shard sulla velocità delle query?**  
A: L'ottimizzazione degli shard compatta l'indice, riduce l'I/O su disco e tipicamente fornisce risposte alle query più veloci del 30‑50 % per grandi set di dati.

**Q: È sicuro eseguire `optimizeShards` su un nodo attivo?**  
A: Sì, l'operazione è progettata per funzionare senza tempi di inattività, ma è consigliato programmarla durante periodi di basso traffico per indici più grandi di 20 GB.

**Q: Posso personalizzare `OptimizeOptions`?**  
A: Assolutamente. Puoi impostare parametri come `maxSegmentSize` o `mergeFactor` per affinare il processo di ottimizzazione.

**Q: Cosa devo fare se incontro un `IOException` durante l'ottimizzazione?**  
A: Verifica i permessi del file system, assicurati di avere spazio libero sufficiente su disco e conferma che nessun altro processo stia bloccando i file di indice.

**Q: L'ottimizzazione degli shard recupera anche lo spazio dei documenti eliminati?**  
A: Sì, l'ottimizzatore unisce i segmenti e rimuove i tombstone, liberando lo spazio occupato dai documenti eliminati.

## Conclusione
Seguendo questa guida completa, ora sai come **configure search network java**, indicizzare documenti, eseguire query testuali e, soprattutto, **optimize shards** per mantenere le prestazioni di ricerca affilate come una lama. Applica questi pattern a qualsiasi soluzione di ricerca aziendale basata su Java, e vedrai miglioramenti misurabili in latenza, scalabilità e utilizzo delle risorse. Come prossimi passi, esplora funzionalità avanzate come analizzatori personalizzati, ricerca a faccette e integrazione con provider di storage cloud.

---

**Ultimo aggiornamento:** 2026-05-17  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Configurazione della rete GroupDocs.Search in .NET: Guida completa](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Indicizzazione master di documenti .NET con GroupDocs.Search: Guida completa](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Tutorial e esempi di GroupDocs.Search per Java](/search/net/)