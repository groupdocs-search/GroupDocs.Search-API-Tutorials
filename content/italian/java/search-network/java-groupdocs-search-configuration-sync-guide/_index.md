---
date: '2026-05-17'
description: Scopri come aggiungere la dipendenza Maven di groupdocs, configurare
  una rete di ricerca Java e aggiungere directory all'indice per un recupero di documenti
  rapido e scalabile.
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: Come aggiungere la dipendenza Maven di GroupDocs per la rete di ricerca
type: docs
url: /it/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# Come aggiungere la dipendenza Maven di GroupDocs per la rete di ricerca

In questa guida completa scoprirai **how to add groupdocs Maven dependency**, configurare una robusta rete di ricerca Java usando GroupDocs.Search e mantenere sincronizzati i tuoi shard. Che tu stia indicizzando atti legali, bilanci finanziari o articoli accademici, i passaggi seguenti ti aiuteranno a creare indici ricercabili, distribuire il carico delle query tra i nodi e mantenere la coerenza dei dati con il minimo sforzo.

## Risposte rapide
- **What is the GroupDocs Maven dependency?** Un artefatto Maven che raggruppa la libreria GroupDocs.Search per progetti Java.  
- **Why use a search network?** Distribuisce il carico di indicizzazione e delle query su più nodi, migliorando velocità e affidabilità.  
- **How do I add directories to index?** Usa `IndexingDocuments.addDirectories` sul nodo master.  
- **How to sync shards?** Chiama `SynchronizeOptions` su ogni `Indexer` del nodo.  
- **Do I need a license?** Sì, è necessaria una licenza di prova o commerciale per l'uso in produzione.

## Cos'è la dipendenza Maven di GroupDocs?

Il `GroupDocs Maven dependency` è un artefatto Maven che raggruppa la libreria GroupDocs.Search per progetti Java.  
Fornisce tutte le classi necessarie per creare indici ricercabili, gestire i nodi della rete ed eseguire query rapide, e Maven risolve automaticamente le dipendenze transitive, offrendoti un motore di ricerca pronto all'uso con poche righe nel tuo `pom.xml`.

## Come aggiungere la dipendenza Maven di GroupDocs

Aggiungi le voci del repository e della dipendenza al tuo `pom.xml`, quindi esegui `mvn clean install`; Maven scarica il JAR `groupdocs-search` e le librerie richieste, rendendo l'API disponibile nel tuo progetto. Dopo che la build è completata con successo, puoi iniziare a utilizzare immediatamente le classi `com.groupdocs.search` .

### Configurazione Maven

Aggiungi il repository e la dipendenza al tuo `pom.xml`:

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

> **Consiglio:** Mantieni il numero di versione aggiornato controllando la pagina ufficiale delle release.

Puoi anche scaricare il JAR direttamente dal sito ufficiale: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## Perché usare una rete di ricerca?

Una rete di ricerca consente la scalabilità orizzontale partizionando l'indice in shard che risiedono su nodi separati. GroupDocs.Search può gestire **oltre 50 formati di input** e processare **documenti di centinaia di pagine** senza caricare l'intero file in memoria, fornendo risposte alle query in meno di un secondo anche con l'aumento del volume dei dati.

## Prerequisiti

- **JDK** (11 o superiore) installato.  
- Un IDE come IntelliJ IDEA o Eclipse.  
- Conoscenze di base di Java, familiarità con Maven e comprensione dei concetti di nodo di rete.  
- Una licenza valida di GroupDocs.Search (prova gratuita o commerciale).

## Inizializzazione e configurazione di base

Inizia creando una directory di indice:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Questa semplice operazione prepara l'ambiente per la successiva configurazione della rete.

## Guida all'implementazione

### Funzione 1: Configurazione della rete di ricerca

#### Panoramica

Configurare la rete di ricerca imposta i percorsi dei file e le porte che i nodi utilizzeranno per comunicare.

##### Configurazione di percorsi e porte

Configuration è una classe che contiene i percorsi di rete, le porte e altre impostazioni per il cluster di ricerca.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
L'oggetto `configuration` ora contiene tutte le impostazioni necessarie per la tua rete di ricerca.

### Funzione 2: Distribuzione dei nodi della rete di ricerca

#### Panoramica

Distribuisci i nodi per distribuire il carico di lavoro nella tua rete. Il nodo master gestisce le operazioni e gli eventi.

##### Codice di distribuzione

SearchNetworkNode rappresenta un nodo nella rete di ricerca che può fungere da master o worker.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Funzione 3: Sottoscrizione agli eventi dei nodi della rete di ricerca

#### Panoramica

Ascoltare gli eventi consente di gestire dinamicamente le modifiche o gli aggiornamenti nella tua rete.

##### Implementazione della sottoscrizione

SearchNetworkNodeEvents fornisce hook di eventi per il ciclo di vita del nodo e le azioni di indicizzazione.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Funzione 4: Aggiunta di directory all'indice

#### Panoramica

Aggiungere directory è il passaggio fondamentale che rende i tuoi documenti ricercabili.

##### Aggiunta di documenti

`IndexingDocuments.addDirectories` aggiunge percorsi di cartelle all'indice per l'elaborazione.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Funzione 5: Sincronizzazione degli shard nel nodo della rete di ricerca

#### Panoramica

La sincronizzazione garantisce la coerenza dei dati tra tutti gli shard.

##### Codice di sincronizzazione

`SynchronizeOptions` configura come gli shard vengono sincronizzati tra i nodi.  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### Funzione 6: Chiusura dei nodi della rete di ricerca

#### Panoramica

Chiudere correttamente i nodi rilascia le risorse e previene perdite di memoria.

##### Chiusura del nodo

`close()` rilascia le risorse e spegne il nodo della rete di ricerca.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Applicazioni pratiche

1. **Legal Document Management** – Recupera rapidamente fascicoli e precedenti.  
2. **Financial Record Keeping** – Accedi a estratti conto e tracciati di audit in pochi secondi.  
3. **Academic Research** – Cerca tra migliaia di articoli per trovare citazioni rilevanti.

## Considerazioni sulle prestazioni

- **Optimize Queries** – Scrivi query concise per ridurre il tempo di risposta.  
- **Memory Management** – Monitora l'uso dell'heap JVM; considera la messa a punto del GC per indici di grandi dimensioni.  
- **Scaling Strategy** – Aggiungi nodi proporzionalmente al volume dei dati e al carico delle query.

## Problemi comuni e soluzioni

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| I nodi non riescono a connettersi | Conflitto di porta | Modifica `basePort` con un valore non utilizzato |
| L'indice non si aggiorna | Sottoscrizione agli eventi mancante | Assicurati che `SearchNetworkNodeEvents.subscribe(masterNode)` sia chiamato |
| Alta latenza | Shard insufficienti | Aumenta il numero di nodi e bilancia la distribuzione dei documenti |

## Domande frequenti

**Q: Qual è il beneficio principale dell'utilizzo di GroupDocs.Search?**  
A: Fornisce capacità di ricerca rapide e scalabili su grandi insiemi di documenti con configurazione minima.

**Q: Posso personalizzare le configurazioni dei nodi in una rete di ricerca?**  
A: Sì, puoi impostare percorsi, porte e altre opzioni personalizzate tramite l'oggetto `Configuration`.

**Q: Come aggiungo directory all'indice dopo che la rete è in esecuzione?**  
A: Chiama `IndexingDocuments.addDirectories(masterNode, "path")` ogni volta che devi indicizzare nuove cartelle.

**Q: Come sincronizzare gli shard quando un nuovo nodo si unisce alla rete?**  
A: Usa il metodo `synchronizeShards` mostrato sopra sul nodo appena aggiunto.

**Q: È necessaria una licenza per lo sviluppo?**  
A: Una licenza di prova gratuita è sufficiente per i test; è necessaria una licenza commerciale per la produzione.

## Conclusione

Seguendo questa guida ora sai come **add groupdocs Maven dependency**, configurare una rete di ricerca multi‑nodo, indicizzare directory e mantenere sincronizzati gli shard. Questi passaggi costituiscono la base per una soluzione di ricerca documenti ad alte prestazioni che può crescere con le esigenze della tua organizzazione.

---

**Ultimo aggiornamento:** 2026-05-17  
**Testato con:** GroupDocs.Search 25.4  
**Autore:** GroupDocs

## Tutorial correlati

- [Tutorial e esempi di GroupDocs.Search per Java](/search/net/)
- [Configurazione della rete GroupDocs.Search in .NET: Guida completa](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Come implementare una rete di ricerca con GroupDocs.Search in .NET per sistemi di gestione documentale](/search/net/search-network/implement-search-network-groupdocs-dotnet/)