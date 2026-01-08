---
date: '2026-01-08'
description: Scopri come configurare la ricerca e abilitare gli aggiornamenti in tempo
  reale della ricerca utilizzando GroupDocs.Search per Java. Guida passo‑passo alla
  configurazione della rete, al deployment dei nodi e all’indicizzazione.
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 'Come configurare la ricerca con GroupDocs.Search in Java: Guida alla configurazione
  e al dispiegamento'
type: docs
url: /it/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# Come configurare la ricerca con GroupDocs.Search in Java

Nel mondo digitale odierno, in rapida evoluzione, **come configurare la ricerca** in modo efficiente può determinare il successo o il fallimento di un progetto. Che tu stia gestendo migliaia di contratti, articoli di ricerca o report interni, una rete di ricerca ben progettata ti consente di trovare il documento giusto in pochi secondi. Questo tutorial ti guida nella configurazione di una rete di ricerca, nella distribuzione dei nodi e nell'abilitazione degli **aggiornamenti di ricerca in tempo reale** con GroupDocs.Search per Java.

## Risposte rapide
- **Qual è lo scopo principale di una rete di ricerca?** Per distribuire l'indicizzazione e l'elaborazione delle query su più nodi per scalabilità e velocità.  
- **Quale versione della libreria è richiesta?** GroupDocs.Search per Java v25.4 o successiva.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per la valutazione; è necessaria una licenza commerciale per la produzione.  
- **Come vengono gestiti gli aggiornamenti in tempo reale?** Sottoscrivendo gli eventi del nodo che si attivano sulle modifiche dell'indicizzazione.  
- **Posso aggiungere nuove cartelle di documenti al volo?** Sì—usa il metodo `addDirectories` dell'indicizzatore.

## Cos'è “come configurare la ricerca” nel contesto di GroupDocs?
Configurare la ricerca significa impostare una **rete di ricerca** che conosce la posizione dei tuoi documenti, come comunicano i nodi e come è coordinata l'indicizzazione. Una volta configurata la rete, puoi aggiungere o rimuovere nodi senza tempi di inattività, garantendo un accesso continuo a risultati di ricerca aggiornati.

## Perché utilizzare GroupDocs.Search per Java?
- **Scalabilità:** Distribuire i carichi di lavoro su più macchine.  
- **Aggiornamenti in tempo reale:** Riflettere istantaneamente i file appena indicizzati su tutta la rete.  
- **Facilità di integrazione:** Configurazione Maven semplice e API Java chiare.  
- **Pronto per l'impresa:** Gestisce grandi corpora e scenari di query complessi.

## Prerequisiti
- **Java Development Kit (JDK) 8+** installato.  
- **Maven** per la gestione delle dipendenze.  
- Familiarità di base con Java, Maven e i concetti di ricerca.  

## Configurazione di GroupDocs.Search per Java

### Dipendenza Maven
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

**Download diretto:** Puoi anche ottenere la libreria da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
- **Prova gratuita:** Ottieni una licenza di prova per esplorare tutte le funzionalità.  
- **Licenza temporanea:** Richiedi per periodi di valutazione estesi.  
- **Licenza commerciale:** Necessaria per le distribuzioni in produzione.

### Inizializzazione di base
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Come configurare la rete di ricerca in Java

### Passo 1: Importare i pacchetti richiesti
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### Passo 2: Configurare la rete
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Parametri:** `basePath` indica la cartella dei tuoi documenti; `basePort` è la porta TCP usata per la comunicazione tra nodi.

## Distribuzione dei nodi della rete di ricerca

### Passo 1: Importare il pacchetto di distribuzione
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### Passo 2: Distribuire i nodi
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Nodo master:** Coordina le ricerche e l'indicizzazione su tutti i nodi.

## Sottoscrizione agli eventi del nodo per aggiornamenti di ricerca in tempo reale

### Passo 1: Importare il pacchetto degli eventi
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### Passo 2: Sottoscrivere gli eventi del nodo master
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Gestione degli eventi:** Abilita gli **aggiornamenti di ricerca in tempo reale** ogni volta che i documenti vengono aggiunti, aggiornati o rimossi.

## Aggiunta di directory per l'indicizzazione

### Passo 1: Importare il pacchetto dell'indicizzatore
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### Passo 2: Aggiungere directory di documenti
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Indicizzazione dinamica:** Aggiungi quante cartelle desideri; la rete le indicizzerà automaticamente.

## Recupero dei documenti indicizzati

### Passo 1: Importare il pacchetto del motore di ricerca
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### Passo 2: Recuperare le informazioni del documento
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **Gestione degli shard:** Gestisce in modo efficiente grandi dataset distribuendo i documenti tra gli shard.

## Applicazioni pratiche
1. **Gestione documentale aziendale:** Centralizza la ricerca su milioni di file.  
2. **Studi legali:** Trova rapidamente fascicoli, contratti e prove.  
3. **Ricerca accademica:** Indicizza riviste e articoli per un recupero istantaneo.

## Considerazioni sulle prestazioni
- **Ottimizzare l'indicizzazione:** Pianifica aggiornamenti regolari dell'indice e rimuovi dati obsoleti.  
- **Gestione della memoria:** Monitora l'heap JVM, soprattutto quando gestisci shard di grandi dimensioni.  
- **Pianificazione della scalabilità:** Aggiungi nodi man mano che il tuo corpus cresce; la rete bilancia automaticamente il carico.

## Problemi comuni e soluzioni

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| I nodi non possono connettersi | Conflitto di porta o firewall | Assicurati che `basePort` sia aperta e non utilizzata da altri servizi |
| L'indice non si aggiorna | Sottoscrizione agli eventi mancante | Chiama `SearchNetworkNodeEvents.subscribe(masterNode)` dopo la distribuzione |
| Errori di out‑of‑memory | Troppi shard di grandi dimensioni caricati | Riduci la dimensione dello shard o aumenta l'heap JVM (`-Xmx` flag) |

## Domande frequenti

**D: Posso aggiungere nuove directory dopo che la rete è in esecuzione?**  
R: Sì—usa il metodo `indexer.addDirectories()`; gli eventi sottoscritti propagheranno gli aggiornamenti in tempo reale.

**D: Come monitoro lo stato dei nodi?**  
R: Ogni `SearchNetworkNode` fornisce API di stato; integrale con lo strumento di monitoraggio che preferisci.

**D: È possibile eseguire il nodo master su una macchina separata?**  
R: Assolutamente. Basta assicurarsi che tutti i nodi condividano lo stesso `basePort` e possano raggiungersi sulla rete.

**D: Quali formati di file sono supportati?**  
R: GroupDocs.Search supporta PDF, Word, Excel, PowerPoint, testo semplice e molti altri formati pronti all'uso.

**D: Devo riavviare la rete dopo aver aggiunto un nuovo nodo?**  
R: No—i nodi possono essere aggiunti o rimossi dinamicamente; il nodo master riequilibrerà gli shard automaticamente.

## Conclusione
Ora hai una comprensione completa, passo dopo passo, di **come configurare la ricerca** usando GroupDocs.Search per Java, dalla configurazione iniziale agli aggiornamenti in tempo reale e all'indicizzazione distribuita. Applica questi modelli per creare soluzioni di ricerca documentale veloci, scalabili e affidabili per qualsiasi settore.

---

**Ultimo aggiornamento:** 2026-01-08  
**Testato con:** GroupDocs.Search for Java 25.4  
**Autore:** GroupDocs