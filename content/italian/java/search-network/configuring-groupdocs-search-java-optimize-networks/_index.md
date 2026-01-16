---
date: '2026-01-16'
description: Scopri come configurare la rete di ricerca GroupDocs in Java e aggiungere
  sinonimi all'indice per migliorare l'efficienza della ricerca.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Configura GroupDocs.Search Network in Java – Potenzia la ricerca
type: docs
url: /it/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Configurare GroupDocs.Search Network in Java – Boost Search

Nelle applicazioni odierne guidate dai dati, **configure groupdocs search network** è il passaggio chiave per fornire risultati rapidi e accurati su collezioni di documenti massivi. Che tu stia costruendo un portale di ricerca a livello aziendale o estendendo una soluzione esistente, una rete GroupDocs.Search ben configurata ti consente di scalare orizzontalmente, aggiungere il supporto ai sinonimi e mantenere bassa la latenza. In questo tutorial imparerai come impostare, distribuire e ottimizzare una rete GroupDocs.Search usando Java, oltre a consigli pratici per aggiungere sinonimi all'indice e gestire il ciclo di vita dei nodi.

## Risposte rapide
- **Qual è il beneficio principale della configurazione di una rete GroupDocs.Search?** Consente l'indicizzazione e l'interrogazione distribuite, migliorando prestazioni e scalabilità.  
- **È necessaria una licenza per eseguire gli esempi?** Una prova gratuita è sufficiente per lo sviluppo; è richiesta una licenza commerciale per la produzione.  
- **È possibile aggiungere sinonimi senza ricostruire l'indice?** Sì—usa il dizionario dei sinonimi a runtime per **add synonyms to index**.  
- **Quanti nodi posso distribuire?** Puoi distribuire tutti i nodi che la tua infrastruttura consente; ogni nodo gira sulla propria porta.  

## Che cosa significa configurare una rete GroupDocs.Search?
Configurare una rete GroupDocs.Search significa definire la struttura delle cartelle, le porte e le impostazioni dei nodi che permettono a più istanze JVM di collaborare nell'indicizzazione e nella ricerca. Questa configurazione crea un nodo master che coordina i worker (shard) e garantisce che le query vengano eseguite sull'intero set di dati.

## Perché configurare una rete GroupDocs.Search?
- **Scalabilità** – Distribuisce il carico di indicizzazione su più macchine.  
- **Affidabilità** – I nodi possono essere aggiunti o rimossi senza tempi di inattività.  
- **Rilevanza della ricerca** – Aggiungi sinonimi all'indice per risultati più ricchi.  
- **Prestazioni** – L'esecuzione parallela delle query riduce il tempo di risposta.

## Prerequisiti
- Java Development Kit (JDK) 8 o superiore  
- Maven per la compilazione del progetto  
- Familiarità di base con la sintassi Java  
- Accesso alla libreria GroupDocs.Search for Java (scaricata via Maven o dalla pagina di rilascio ufficiale)

## Configurare GroupDocs.Search per Java

Aggiungi il repository e la dipendenza al tuo **pom.xml** Maven:

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

In alternativa, scarica l'ultima versione direttamente da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
- **Prova gratuita** – Esplora le funzionalità principali senza costi.  
- **Licenza temporanea** – Sblocca tutte le capacità per test a breve termine.  
- **Licenza commerciale** – Necessaria per le distribuzioni in produzione.

### Inizializzazione e configurazione di base
Crea una semplice classe Java per verificare che la libreria venga caricata correttamente:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Guida passo‑passo per configurare GroupDocs.Search Network

### 1. Configurazione della rete di ricerca
Definisci la cartella base dei documenti e la porta iniziale per la comunicazione tra i nodi.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Dove risiedono i dizionari (ad esempio i file dei sinonimi).  
- **basePort** – La prima porta; i nodi successivi incrementano questo valore.

### 2. Distribuzione dei nodi della rete di ricerca
Avvia più nodi worker che condividono la stessa configurazione.

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Ogni nodo gira sulla propria porta (basePort + indice) e detiene una shard dell'indice complessivo.

### 3. Sottoscrizione agli eventi dei nodi
Monitora lo stato, l'avanzamento dell'indicizzazione e le condizioni di errore collegando un listener di eventi al nodo master.

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Le callback degli eventi ti permettono di reagire all'avvio/arresto del nodo, al completamento dell'indicizzazione e a eventuali fallimenti imprevisti.

### 4. Aggiungere sinonimi all'indicizzatore di un nodo  
Migliora la rilevanza **add synonyms to index** a runtime.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Array di termini che devono essere trattati come equivalenti.  
- **clearBeforeAdding** – Imposta a `true` se desideri sostituire le voci esistenti.

### 5. Aggiungere directory per l'indicizzazione
Indica al nodo master quali cartelle contengono i documenti da rendere ricercabili.

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

Il metodo scandisce la directory in modo ricorsivo e distribuisce i file tra le shard.

### 6. Eseguire ricerche testuali nella rete
Esegui una query su tutti i nodi, opzionalmente forzando il comportamento di corrispondenza esatta.

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Imposta `exactMatchOnly` a `true` quando hai bisogno di una corrispondenza rigorosa dei termini senza stemming.

### 7. Chiudere i nodi della rete
Rilascia le risorse in modo corretto una volta completata l'elaborazione.

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Una chiusura appropriata previene perdite di memoria e mantiene la JVM in salute.

## Applicazioni pratiche
| Scenario | Come la rete aiuta |
|----------|--------------------|
| **Ricerca aziendale** | Distribuisce l'indicizzazione su server del data‑center per corpora su scala di petabyte. |
| **Gestione documenti** | Aggiunge sinonimi all'indice così gli utenti trovano i documenti anche con terminologia varia. |
| **Catalogo e‑commerce** | Distribuisce nodi specifici per regione per fornire ricerche di prodotto localizzate rapidamente. |
| **Gestione dei contenuti** | Mantiene i contenuti ricercabili mentre gli editor aggiungono nuovi file a directory specifiche. |

## Problemi comuni e soluzioni
- **Conflitti di porta** – Assicurati che la porta di ogni nodo (basePort + indice) sia libera; modifica `basePort` se necessario.  
- **Sinonimo non applicato** – Verifica di aver chiamato `indexer.setDictionary(dictionary)` dopo aver aggiunto i termini.  
- **Nodo non risponde** – Sottoscrivi gli eventi; cerca le callback `NodeFailed` per diagnosticare i problemi di rete.  
- **Perdita di memoria alla chiusura** – Invoca sempre `node.close()` per ogni nodo distribuito.

## Domande frequenti

**D: Come la distribuzione di più nodi migliora le prestazioni di ricerca?**  
R: Ogni nodo indicizza una shard dei dati, consentendo l'elaborazione parallela e riducendo la latenza delle query poiché il carico è condiviso.

**D: Posso aggiungere sinonimi senza re‑indicizzare i documenti esistenti?**  
R: Sì, puoi **add synonyms to index** a runtime tramite il dizionario dei sinonimi; le modifiche hanno effetto immediato per le nuove query.

**D: È obbligatorio sottoscrivere gli eventi dei nodi?**  
R: Non è richiesto per il funzionamento di base, ma la sottoscrizione agli eventi ti offre visibilità sullo stato dei nodi e ti aiuta a reagire rapidamente ai fallimenti.

**D: Quali sono le migliori pratiche per gestire le risorse dei nodi?**  
R: Chiudi regolarmente i nodi inattivi, monitora l'uso di memoria della JVM e ricicla i nodi durante le ore di bassa attività per mantenere il consumo di risorse ottimale.

**D: GroupDocs.Search supporta formati non testuali come PDF o immagini?**  
R: Assolutamente. La libreria estrae testo da PDF, file Office e persino esegue OCR su immagini, rendendoli ricercabili out‑of‑the‑box.

---

**Ultimo aggiornamento:** 2026-01-16  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs