---
date: '2026-01-21'
description: Scopri come aggiungere la dipendenza GroupDocs Maven, configurare e sincronizzare
  una rete di ricerca Java e aggiungere directory da indicizzare con GroupDocs.Search.
keywords:
- Java Search Network Configuration
- GroupDocs.Search for Java
- Document Indexing and Retrieval
title: Dipendenza Maven di GroupDocs – Sincronizzazione della rete di ricerca Java
type: docs
url: /it/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

 Maven di GroupDocs: Configurazione e sincronizzazione delle reti di ricerca Java

In questa guida completa scoprirai **come aggiungere la dipendenza Maven di GroupDocs** al tuo progetto e quindi configurare una solida rete di ricerca Java utilizzando GroupDocs.Search. Che tu stia gestendo atti legali, report finanziari o articoli accademici modo effic e cercare enormi collezioni di documenti è una sfida quotidiana per molte organizzazioni. Integrando la **dipendenza Maven di GroupDocs**, ottieni accesso a un potente motore di indicizzazione che scala su più nodi. Questo tutorial ti guida attraverso l'installazione della dipendenza, il deployment dei nodi di rete, l'aggiunta di directory da indicizzare e laimali.

### Risposte rapide
- **Che cos'è la indicizzare?** Usa `IndexingDocuments.addDirectories` sul nodo master.  
- **Come sincronizzare gli shard?** Chiama `SynchronizeOptions.  
-uso in produzione.

## Che cos'è la dipendenza Maven di GroupDocs?

La dipendenza Maven di GroupDocs (`com.groupdocs:groupdocs-search`) include tutte le classi necessarie per creare indici ricercabili, gestire i nodi di rete e eseguire query rapide. Aggiungerla al tuo `pom.xml` garantisce che Maven scarichi i binari corretti e le dipendenze transitive.

## Come aggiungere la dipendenza Maven di GroupDocs

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

Puoi anche scaricare il JAR direttamente dal sito ufficiale: [GroupDocs.Search per Java releases](https://releases.groupdocs.com/search/java/).

## Prerequisiti

- **JDK** (11 o superiore) installato.  
- Un IDE come IntelliJ IDEA o Eclipse.  
- Conoscenza di base di Java, familiarità con Maven e comprensione dei concetti di nodi di rete.  
- Una licenza valida di GroupDocs.Search (trial gratuito o commerciale).

## Inizializzazione e configurazione di base

Inizia creando una directory di indice:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Questo semplice passaggio prepara l'ambiente per la successiva configurazione della rete.

## Guida all'implementazione

### Funzionalità 1: Configurazione della rete di ricerca

#### Panoramica

Configurare la rete di ricerca imposta i percorsi dei file e le porte che i nodi utilizzeranno per comunicare.

##### Configurazione percorsi e porte
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
L'oggetto `configuration` ora contiene tutte le impostazioni necessarie per la tua rete di ricerca.

### Funzionalità 2: Distribuzione dei nodi della rete di ricerca

#### Panoramica

Distribuisci i nodi per distribuire il carico di lavoro sulla tua rete. Il nodo master gestisce le operazioni e gli eventi.

##### Codice di distribuzione
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Funzionalità 3: Sottoscrizione agli eventi dei nodi della rete di ricerca

#### Panoramica

Ascoltare gli eventi consente una gestione dinamica di modifiche o aggiornamenti nella tua rete.

##### Implementazione della sottoscrizione
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Funzionalità 4: Aggiunta di directory all'indice

#### Panoramica

L'aggiunta di directory è il passaggio fondamentale che rende i tuoi documenti ricercabili.

##### Aggiunta di documenti
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Funzionalità 5: Sincronizzazione degli shard nel nodo della rete di ricerca

#### Panoramica

La sincronizzazione garantisce la coerenza dei dati su tutti gli shard.

##### Codice di sincronizzazione
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

### Funzionalità 6: Chiusura dei nodi della rete di ricerca

#### Panoramica

Chiudere correttamente i nodi rilascia le risorse e previene perdite di memoria.

##### Chiusura del nodo
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Applicazioni pratiche

1. **Gestione di documenti legali** – Recupera rapidamente fascicoli e precedenti.  
2. **Gestione dei record finanziari** – Accedi a Monitora l'utilizzo dell' indici di grandi dimensioni.  
- **Strategia di scaling** – Aggiungi nodi proporzionalmente-----------|
| I nodi non riescono a connettersi | Conflitto di porta | Modifica `basePort` con un valore non utilizzato |
| Indice non aggiornato | Sottoscrizione agli eventi mancante | Assicurati che `SearchNetworkNodeEvents.subscribe(masterNode)` sia chiamato |
| Elevata latenza | Sh bilancia la distribuzione dei documenti |

## Domande frequenti

**Q: Qual è il beneficio principale dell'utilizzo di GroupDocs.Search?**  
A: Fornisce capacità di ricerca rapide e scalabili su grandi insiemi di documenti con configurazione minima.

**Q: Posso personalizzare le configurazioni dei nodi in una rete di ricerca?**  
A: Sì, è possibile impostare percorsi, porte e altre opzioni personalizzate tramite l'oggetto `Configuration`.

**Q: Come aggiungo directory all'indice dopo che la rete è in esecuzione?**  
A: Chiama `IndexingDocuments.addDirectories(masterNode, "path")` ogni volta che devi indicizzare nuove cartelle.

**Q: Come sincronizzare gli shard quando un nuovo nodo si unisce alla rete?**  
A: Usa il metodo `synchronizeShards` mostrato sopra sul nodo appena aggiunto.

**Q: È necessaria una licenza per lo sviluppo?**  
A: Una licenza di prova gratuita è sufficiente per i test; è richiesta una lic passaggi costituiscono la base per una soluzione di ricerca documenti ad alte prestazioni che può crescere con le esigenze della tua organizzazione.

---

**Ultimo aggiornamento:**