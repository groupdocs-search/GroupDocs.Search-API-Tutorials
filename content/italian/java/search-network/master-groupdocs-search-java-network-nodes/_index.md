---
date: '2026-07-02'
description: Scopri come ottenere una licenza temporanea per GroupDocs.Search, aggiungere
  directory all'indice e aggiungere attributi personalizzati ai documenti mentre gestisci
  i nodi della rete di ricerca Java.
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
title: Ottenere licenza temporanea GroupDocs – Master Search Nodes (Java)
type: docs
url: /it/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Ottieni Licenza Temporanea GroupDocs – Nodi Master di Ricerca (Java)

In questa guida completa **otterrai una licenza temporanea per GroupDocs.Search**, configurerai una rete di ricerca multi‑nodo e imparerai come **aggiungere directory all'indice** e **aggiungere attributi personalizzati ai documenti** usando Java. Che tu stia costruendo un sistema di gestione documentale aziendale o un catalogo di prodotti ricercabile, padroneggiare questi passaggi ti consente di valutare la piattaforma senza restrizioni e di scalare rapidamente le tue capacità di ricerca.

## Risposte Rapide
- **Qual è il primo passo per iniziare a usare GroupDocs.Search?** Ottieni una licenza temporanea dal portale GroupDocs.  
- **Quale repository Maven ospita la libreria?** `https://releases.groupdocs.com/search/java/`.  
- **Come aggiungo directory all'indice?** Chiama l'helper `addDirectoriesToIndex` sul nodo master.  
- **Posso aggiungere attributi personalizzati ai documenti?** Sì—invoca `addAttribute` con la chiave del documento e il nome dell'attributo.  
- **Come chiudo correttamente i nodi?** Invoca `closeNodes` per rilasciare le risorse.

## Cos'è una licenza temporanea e perché ne ho bisogno?
Una licenza temporanea ti consente di valutare GroupDocs.Search senza alcuna limitazione di valutazione. È perfetta per sviluppo, test o progetti proof‑of‑concept prima di impegnarsi in un acquisto completo. La licenza garantisce l'accesso a tutte le funzionalità per un periodo limitato, permettendoti di misurare le prestazioni, testare i punti di integrazione e assicurarti che la soluzione soddisfi i tuoi requisiti senza impegno finanziario.

## Prerequisiti

Prima di iniziare, assicurati di avere i seguenti prerequisiti in ordine:

### Librerie e Dipendenze Richieste
Per lavorare con GroupDocs.Search per Java, includi le dipendenze Maven necessarie:
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
Puoi anche scaricare l'ultima versione direttamente da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Configurazione dell'Ambiente
- Assicurati di avere installato un JDK compatibile (Java 8 o successivo).  
- Configura il tuo IDE per supportare progetti Maven.

### Prerequisiti di Conoscenza
Una comprensione di base della programmazione Java e familiarità con la gestione di progetti Maven saranno utili. Se sei nuovo a questi concetti, considera di esplorare risorse introduttive per iniziare.

## Come ottenere una licenza temporanea
Una licenza temporanea si ottiene visitando il portale GroupDocs, compilando un breve modulo di richiesta e posizionando il file `.lic` ricevuto nella cartella `resources` del tuo progetto. Quindi inizializza la licenza con poche righe di codice (vedi lo snippet sotto). Per il modulo di richiesta, utilizza la pagina ufficiale: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## Configurazione di GroupDocs.Search per Java

### Informazioni sull'Installazione
Per iniziare a usare GroupDocs.Search per Java nel tuo progetto, segui i passaggi Maven sopra o scarica l'ultima versione direttamente dalla pagina ufficiale dei rilasci.

#### Passaggi per l'Acquisizione della Licenza
1. **Prova Gratuita** – Esplora le funzionalità senza alcun impegno.  
2. **Licenza Temporanea** – Ottieni una chiave a breve termine per i test (vedi la sezione sopra).  
3. **Acquisto** – Per l'uso in produzione, acquista una licenza completa dalla **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)**.

### Inizializzazione e Configurazione di Base
Initialize your project with GroupDocs.Search as follows:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Questo passaggio di inizializzazione è fondamentale per garantire che tutti i componenti funzionino senza problemi all'interno della tua rete di ricerca.

## Guida all'Implementazione
Ora, suddividiamo il processo in sezioni gestibili, ognuna focalizzata su una specifica funzionalità di distribuzione e gestione dei nodi della rete di ricerca.

### Funzionalità 1: Configurazione
**Panoramica:** Configurare le impostazioni per la tua rete di ricerca è il primo passo per distribuire i nodi. Questa configurazione prevede la specifica di percorsi e porte critiche per il deployment dei nodi.

#### Passaggi di Implementazione:
##### Passo 1: Definire Percorso Base e Porta
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Passo 2: Configurare la Rete di Ricerca
La funzione `configureSearchNetwork` prepara l'oggetto di configurazione necessario per distribuire i nodi.  
`Configuration` è una classe che contiene tutte le impostazioni come la cartella dell'indice, le porte di rete e i ruoli dei nodi.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parametri:** Il percorso base e la porta sono usati per localizzare le risorse e stabilire i canali di comunicazione.  
- **Valore di ritorno:** Un oggetto `Configuration` configurato su misura per le tue esigenze di deployment.

### Funzionalità 2: Distribuzione della Rete di Ricerca
**Panoramica:** Distribuire i nodi è essenziale per scalare le tue capacità di ricerca attraverso diversi ambienti o segmenti di dati.

#### Passaggi di Implementazione:
##### Passo 1: Distribuire i Nodi
La funzione `deploySearchNetwork` inizializza e restituisce un array di nodi della rete di ricerca.  
`SearchNetworkNodes` rappresenta ogni istanza di nodo che partecipa al cluster di ricerca distribuito.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parametri:** Il percorso base, la porta e la configurazione sono usati per determinare l'ambiente di deployment.  
- **Valore di ritorno:** Un array contenente `SearchNetworkNodes` inizializzati.

### Funzionalità 3: Sottoscrizione agli Eventi della Rete
**Panoramica:** Monitorare le attività della tua rete di ricerca è cruciale per mantenere prestazioni ottimali e affidabilità.

#### Passaggi di Implementazione:
##### Passo 1: Sottoscrivere agli Eventi del Nodo Master
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Scopo:** Questo passo garantisce che tu sia avvisato di eventi o cambiamenti significativi all'interno della tua rete di ricerca.

### Funzionalità 4: Indicizzazione dei Documenti
**Panoramica:** Aggiungere directory contenenti documenti da indicizzare consente un recupero dati efficiente attraverso la tua rete.

#### Come aggiungere directory all'indice
`addDirectoriesToIndex` è un metodo helper che registra i percorsi delle cartelle per l'indicizzazione sul nodo master.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Scopo:** Facilita l'accesso rapido e la ricercabilità di tutti i documenti nelle directory specificate.

### Funzionalità 5: Aggiunta di Attributi ai Documenti
**Panoramica:** Gli attributi personalizzati arricchiscono i metadati dei documenti, rendendo le ricerche più flessibili e informative.

#### Come aggiungere attributi personalizzati ai documenti
`addAttribute` aggiunge un attributo di metadati personalizzato a un documento specificato nell'indice.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parametri:** Specifica il nodo, la chiave del documento e l'attributo da aggiungere.  
- **Scopo:** Estende la funzionalità di ricerca arricchendo i documenti con metadati aggiuntivi.

### Funzionalità 6: Recupero dei Documenti Indicizzati
**Panoramica:** Recuperare e elencare efficientemente i documenti indicizzati per garantire accuratezza e completezza dei dati.

#### Passaggi di Implementazione:
##### Passo 1: Ottenere i Documenti Indicizzati
```java
getIndexedDocuments(nodes[0]);
```  
- **Scopo:** Verifica l'indicizzazione corretta di tutti i documenti necessari nella tua rete di ricerca.

### Funzionalità 7: Chiusura dei Nodi della Rete
**Panoramica:** Chiudere correttamente i nodi è cruciale per la gestione delle risorse e per prevenire perdite di memoria.

#### Passaggi di Implementazione:
##### Passo 1: Chiudere Tutti i Nodi
`closeNodes` chiude tutti i nodi di ricerca attivi e rilascia le risorse allocate.  
```java
closeNodes(nodes);
```  
- **Scopo:** Rilascia le risorse occupate da ciascun nodo, garantendo un processo di spegnimento pulito.

## Perché usare una licenza temporanea per GroupDocs.Search?
Una licenza temporanea fornisce **accesso completo a tutte le funzionalità per 30 giorni** e supporta fino a **50.000 documenti indicizzati** senza limitazioni di prestazioni. Questo ti permette di misurare la velocità di indicizzazione, la latenza delle query e la scalabilità su dati reali prima di acquistare una licenza di produzione. Rimuove inoltre i watermark di valutazione, offrendoti una rappresentazione reale delle capacità del prodotto finale.

## Casi d'Uso Comuni
1. **Gestione Documentale Aziendale** – Indicizza milioni di file interni tra i dipartimenti, consentendo una ricerca full‑text istantanea.  
2. **Piattaforme E‑commerce** – Crea un catalogo di prodotti ricercabile che copre più magazzini e feed di terze parti.  
3. **Studi Legali** – Organizza fascicoli, contratti e prove con metadati personalizzati per un recupero rapido.

Le possibilità di integrazione con altri sistemi includono piattaforme CRM, sistemi di gestione dei contenuti (CMS) e strumenti di analisi dei dati, sfruttando le robuste funzionalità di indicizzazione e ricerca offerte da GroupDocs.Search per Java.

## Considerazioni sulle Prestazioni
Per ottimizzare le prestazioni quando usi GroupDocs.Search per Java:
- **Ottimizza la Configurazione** – Adatta le impostazioni di configurazione al tuo specifico ambiente di deployment.  
- **Monitora l'Uso delle Risorse** – Controlla regolarmente CPU, memoria e I/O per prevenire colli di bottiglia o perdite di memoria.  
- **Segui le Best Practices** – Rispetta le linee guida di gestione della memoria Java, garantendo un utilizzo efficiente delle risorse di sistema.

## Domande Frequenti

**Q: Quanto tempo rimane valida una licenza temporanea?**  
A: Le licenze temporanee sono tipicamente valide per 30 giorni, offrendoti ampio tempo per valutare il prodotto.

**Q: Posso passare da una licenza temporanea a una completa senza reinstallare?**  
A: Sì—sostituisci il file di licenza temporanea con quello completo e riavvia l'applicazione.

**Q: Devo re‑indicizzare i documenti dopo aver applicato una nuova licenza?**  
A: No, l'indice rimane intatto; la licenza regola solo i diritti di utilizzo.

**Q: Cosa succede se dimentico di chiudere i nodi?**  
A: Risorse non rilasciate possono causare perdite di memoria; invoca sempre `closeNodes` durante lo spegnimento.

**Q: È possibile aggiungere più di un attributo personalizzato per documento?**  
A: Assolutamente—chiama `addAttribute` più volte con nomi di attributi diversi.

---

**Last Updated:** 2026-07-02  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs

## Tutorial Correlati

- [Distribuisci un Nodo di Rete di Ricerca in .NET usando GroupDocs per l'Indicizzazione e il Recupero Efficiente dei Documenti](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Come Implementare una Rete di Ricerca con GroupDocs.Search in .NET per Sistemi di Gestione Documentale](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Configurazione della Rete Aspose.Search e Aggiunta di Attributi ai Documenti con GroupDocs.Redaction per .NET: Guida Completa](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)