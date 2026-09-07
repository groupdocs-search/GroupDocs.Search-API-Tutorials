---
date: '2026-07-07'
description: Scopri come eliminare l'indice, eseguire la ricerca full text Java e
  ottimizzare le prestazioni di ricerca utilizzando GroupDocs.Search for Java. Guida
  passo‑passo con configurazione della rete e indicizzazione.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: Come eliminare l'indice e eseguire la ricerca full text Java con GroupDocs.Search.
  Segui questa guida per configurare una rete di ricerca, creare un indice ricercabile
  e ottimizzare le prestazioni di ricerca.
og_title: Come eliminare l'indice e eseguire la ricerca testuale con GroupDocs.Search
  for Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: Come eliminare l'indice e eseguire la ricerca testuale con GroupDocs.Search
  for Java
type: docs
url: /it/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Come eliminare l'indice e eseguire la ricerca di testo con GroupDocs.Search per Java

Nel mondo odierno guidato dai dati, **how to delete index** rapidamente mantenendo capacità di ricerca full‑text Java fulminee è un vantaggio competitivo. Che tu stia costruendo una base di conoscenza interna, un repository di casi legali o un catalogo prodotti e‑commerce, una rete di ricerca ben ottimizzata può migliorare drasticamente la soddisfazione degli utenti. In questa guida imparerai a **set up a search network**, **create a searchable index**, **optimize search performance** e **delete documents from the index** quando necessario—tutto usando GroupDocs.Search per Java.

## Risposte rapide
- **Qual è lo scopo principale di GroupDocs.Search per Java?** Fornisce ricerca full‑text su oltre 50 formati di documenti, consentendo un rapido recupero delle parole chiave.  
- **Come eseguo la ricerca di testo in un ambiente distribuito?** Distribuisci una rete di ricerca, indicizza i documenti su un nodo master, quindi interroga qualsiasi nodo.  
- **Posso eliminare documenti dall'indice senza ricostruirlo?** Sì, usa l'API Delete per rimuovere i file selezionati, effettivamente *how to delete index* senza una completa re‑indicizzazione.  
- **Quale versione di Java è richiesta?** JDK 8 o superiore.  
- **È necessaria una licenza per la produzione?** È richiesta una licenza valida di GroupDocs.Search; è disponibile una prova gratuita.

## Cos'è “perform text search”?
Eseguire una ricerca di testo significa interrogare un indice full‑text per recuperare i documenti che contengono le parole chiave o le frasi specificate. GroupDocs.Search costruisce un indice invertito che rende queste ricerche estremamente rapide, anche su migliaia di file.

## Perché configurare una rete di ricerca?
Una rete di ricerca distribuisce i carichi di indicizzazione e di interrogazione su più nodi, consentendo di **ottimizzare le prestazioni di ricerca**, scalare orizzontalmente e mantenere alta disponibilità. Questa architettura è ideale per repository di documenti a livello enterprise dove latenza e throughput sono importanti.

## Come implementare e ottimizzare una rete di ricerca con GroupDocs.Search per Java
Carica la tua configurazione, avvia un nodo master, quindi aggiungi nodi worker che condividono lo stesso percorso base e porta. Distribuire la rete in questo modo consente a qualsiasi nodo di gestire richieste di indicizzazione o di interrogazione, fornendo tempi di risposta coerenti anche quando il numero di documenti cresce fino a centinaia di migliaia.

### Panoramica passo‑passo
1. **Definisci una configurazione di base** che includa una directory condivisa e una porta TCP.  
2. **Avvia il nodo master** per gestire l'indice e coordinare i nodi worker.  
3. **Aggiungi nodi worker** che si connettono al master, abilitando indicizzazione e ricerca parallele.  
4. **Monitora l'utilizzo delle risorse** e ottimizza le impostazioni dell'heap JVM per mantenere bassa la latenza.

## Come eliminare l'indice in GroupDocs.Search per Java
`SearchNode` rappresenta un nodo nella rete GroupDocs.Search che gestisce le operazioni di indicizzazione e interrogazione. Il metodo `delete` rimuove i documenti specificati dall'indice.

### Passaggi per eliminazione diretta
- Chiama il metodo `delete` sull'istanza `SearchNode`.  
- Fornisci un array di percorsi di file relativi.  
- Conferma le modifiche; l'indice viene aggiornato istantaneamente e le ricerche successive non restituiscono più i file rimossi.

## Cos'è una rete di ricerca?
Una **rete di ricerca** è un cluster di nodi interconnessi che condividono un repository di indice comune, consentendo indicizzazione e interrogazione distribuite. Permette scalabilità orizzontale e tolleranza ai guasti per collezioni di documenti su larga scala.

## Come creare un indice ricercabile (index documents java)
Il metodo `add` indicizza un documento nell'indice di ricerca. Aggiungi documenti al nodo master usando il metodo `add`; la rete propaga le modifiche a tutti i nodi worker. Questo approccio garantisce che ogni nodo possa servire query sull'indice più recente senza passaggi di sincronizzazione aggiuntivi.

### Azioni chiave
- Puntare il nodo master alla cartella contenente i file sorgente.  
- Invocare la routine di indicizzazione; la rete elabora ogni file e aggiorna l'indice invertito.  
- Verificare che i file dell'indice compaiano nella directory di archiviazione designata.

## Come rimuovere i file indicizzati (remove indexed files)
Quando un documento diventa obsoleto, chiama l'API `delete` con il suo percorso. Il sistema rimuove le voci del file dall'indice invertito, liberando spazio di archiviazione e prevenendo risultati obsoleti.

## Configurazione di GroupDocs.Search per Java
Per iniziare, integra GroupDocs.Search nel tuo progetto Java usando la seguente configurazione:

### Configurazione Maven
Aggiungi il repository e la dipendenza al tuo file `pom.xml`:

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
In alternativa, puoi [scaricare l'ultima versione direttamente da GroupDocs](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
GroupDocs offre una prova gratuita, che ti permette di valutare le sue funzionalità prima dell'acquisto. Puoi ottenere una licenza temporanea seguendo i passaggi sulla loro [pagina di acquisto](https://purchase.groupdocs.com/temporary-license/). Questo abiliterà la piena funzionalità durante la fase di test.

### Inizializzazione e configurazione di base
Inizializza GroupDocs.Search nella tua applicazione Java con:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## Guida all'implementazione

### Configurazione della rete di ricerca
**Panoramica:** Definisci un percorso base e una porta per la tua rete di ricerca, consentendo ai nodi di comunicare efficacemente.

#### Passo 1: Definisci la configurazione di base
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parametri:**  
  - `basePath`: Percorso della directory per le operazioni di rete.  
  - `basePort`: Numero di porta usato dalla rete di ricerca.

#### Passo 2: Risoluzione dei problemi
Assicurati che la porta specificata non sia bloccata dalle impostazioni del firewall o utilizzata da un'altra applicazione. Regola se necessario per evitare conflitti.

### Distribuzione dei nodi della rete di ricerca
**Panoramica:** Utilizzando la tua configurazione, distribuisci i nodi nella tua rete per indicizzazione e ricerca distribuite.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Opzioni di configurazione chiave:**  
  - **Base Path & Port:** Questi valori devono corrispondere a quelli usati nella configurazione iniziale per garantire coerenza.

### Indicizzazione dei documenti (`create searchable index`)
**Panoramica:** Aggiungi documenti all'indice di ricerca in modo efficiente usando un nodo master.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Scopo:**  
  - `masterNode`: Il nodo principale che gestisce l'indicizzazione dei documenti.  
  - `documentsPath`: Percorso della directory contenente i documenti.

#### Suggerimenti per la risoluzione dei problemi
Verifica che i percorsi dei documenti siano corretti e accessibili. Assicurati che le autorizzazioni consentano la lettura di queste directory.

### Ricerca di testo nella rete (`perform text search`)
**Panoramica:** Esegui ricerche di testo complete attraverso la tua rete indicizzata.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parametri:**  
  - `query`: Il testo che stai cercando.  
  - `masterNode`: Nodo che esegue la ricerca.

### Eliminazione di documenti dall'indice (`delete documents index`)
**Panoramica:** Rimuovi documenti specifici dal tuo indice usando i loro percorsi file.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Scopo del metodo:**  
  - `node`: Il nodo target per le operazioni di eliminazione.  
  - `filePaths`: Percorsi dei documenti da rimuovere dall'indice.

#### Risoluzione dei problemi
Assicurati che i percorsi dei file siano precisi e che i file esistano nella tua directory. Se i problemi persistono, verifica le autorizzazioni di rete e la connettività.

## Applicazioni pratiche
1. **Gestione documentale aziendale:** Ottimizza il recupero della conoscenza interna.  
2. **Analisi di casi legali:** Trova rapidamente i file di caso rilevanti attraverso più repository.  
3. **Piattaforme e‑commerce:** Aumenta la velocità di ricerca dei prodotti indicizzando descrizioni e recensioni.  
4. **Ricerca accademica:** Ricerca efficientemente grandi biblioteche digitali di articoli e tesi.  
5. **Sistemi di supporto clienti:** Riduci i tempi di risposta consentendo agli operatori di cercare i ticket passati istantaneamente.

## Considerazioni sulle prestazioni
- **Ottimizza la velocità di indicizzazione:** Aggiungi incrementalmente nuovi documenti durante le ore non di punta per mantenere bassa la latenza.  
- **Linee guida sull'uso delle risorse:** Monitora CPU e memoria, specialmente quando aumenti il numero di nodi.  
- **Gestione della memoria Java:** Ottimizza le impostazioni dell'heap JVM in base al carico di lavoro (ad esempio, `-Xmx2g` per indici di dimensione media).

## Conclusione
Seguendo questa guida hai imparato a **configurare una rete di ricerca**, **creare un indice ricercabile**, **eseguire la ricerca di testo** e **eliminare l'indice dei documenti** usando GroupDocs.Search per Java. Queste capacità consentono un recupero di documenti veloce e affidabile in ambienti distribuiti.

**Prossimi passi**
- Sperimenta con diverse configurazioni dei nodi per trovare l'equilibrio ottimale per il tuo carico di lavoro.  
- Approfondisci le opzioni di indicizzazione avanzate come analizzatori personalizzati e la regolazione della rilevanza.  
- Esplora l'integrazione con altri prodotti GroupDocs per una gestione dei documenti end‑to‑end.

## Domande frequenti

**D: Qual è il caso d'uso principale per GroupDocs.Search per Java?**  
R: Fornisce ricerca full‑text su molti formati di documenti, consentendoti di **perform text search** in grandi repository.

**D: Come posso migliorare la velocità di ricerca in una grande rete?**  
R: Distribuisci nodi aggiuntivi, ottimizza l'heap JVM e programma l'indicizzazione durante periodi di basso traffico per **ottimizzare le prestazioni di ricerca**.

**D: È possibile eliminare un singolo documento senza re‑indicizzare l'intera collezione?**  
R: Sì, usa l'API **delete documents index** come mostrato nell'esempio di codice per rimuovere file specifici.

**D: È necessaria una licenza per lo sviluppo?**  
R: Una licenza di prova gratuita è sufficiente per i test; è necessaria una licenza commerciale per le distribuzioni in produzione.

**D: Posso indicizzare PDF, file Word e email insieme?**  
R: Assolutamente—GroupDocs.Search supporta una vasta gamma di formati fin da subito.

---

**Ultimo aggiornamento:** 2026-07-07  
**Testato con:** GroupDocs.Search per Java 25.4  
**Autore:** GroupDocs

## Tutorial correlati

- [Come indicizzare testo in Java con la guida GroupDocs.Search](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [Ottimizza le prestazioni di ricerca con tecniche di indicizzazione avanzate in GroupDocs.Search per Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [Migliora le prestazioni delle query con GroupDocs.Search Java: ottimizza indice e ricerca](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)