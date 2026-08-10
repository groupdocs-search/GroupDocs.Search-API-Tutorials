---
date: '2026-08-10'
description: Scopri come indicizzare documenti e aggiungere documenti all'indice utilizzando
  GroupDocs.Search per Java. Crea app di ricerca potenti con query di testo e di oggetto.
keywords:
- how to index documents
- create search index
- index pdf files
- search word documents
- update search index
lastmod: '2026-08-10'
og_description: Scopri come indicizzare documenti con GroupDocs.Search per Java. Guida
  passo‑passo per creare un indice di ricerca, aggiungere file PDF, Word, Excel e
  eseguire query rapide.
og_image_alt: Code example showing Java indexing with GroupDocs.Search
og_title: Come indicizzare documenti con GroupDocs.Search per Java – Guida rapida
  alla ricerca
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to index documents and add documents to index using GroupDocs.Search
    for Java. Build powerful search apps with text and object queries.
  headline: How to index documents with GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to index documents and add documents to index using GroupDocs.Search
    for Java. Build powerful search apps with text and object queries.
  name: How to index documents with GroupDocs.Search for Java
  steps:
  - name: '**Free trial** – explore the library without cost.'
    text: '**Free trial** – explore the library without cost.'
  - name: '**Temporary license** – request a short‑term key for extended evaluation.'
    text: '**Temporary license** – request a short‑term key for extended evaluation.'
  - name: '**Purchase** – obtain a full license for production use.'
    text: '**Purchase** – obtain a full license for production use.'
  - name: '**Legal document management** – locate clauses, case numbers, or dates
      across thousands of contracts in seconds.'
    text: '**Legal document management** – locate clauses, case numbers, or dates
      across thousands of contracts in seconds.'
  - name: '**Financial reporting** – pull transactions that fall within a specific
      monetary range without scanning each spreadsheet.'
    text: '**Financial reporting** – pull transactions that fall within a specific
      monetary range without scanning each spreadsheet.'
  - name: '**Inventory tracking** – find items by serial numbers, batch codes, or
      SKU ranges across a distributed file system.'
    text: '**Inventory tracking** – find items by serial numbers, batch codes, or
      SKU ranges across a distributed file system.'
  type: HowTo
- questions:
  - answer: Call `index.add("NEW_DOCUMENT_PATH")` again; the library merges the new
      entries without recreating the whole index.
    question: How do I update an existing index with new documents?
  - answer: Yes, it supports 30+ formats—including PDF, DOCX, XLSX, PPTX, TXT, and
      HTML—so you can index virtually any business document.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Java 8+ runtime, at least 2 GB RAM for modest collections (larger sets
      benefit from 4 GB+), and read/write access to the index folder.
    question: What are the system requirements for using GroupDocs.Search?
  - answer: Keep the index up‑to‑date, profile your queries, and review JVM memory
      settings. Reducing the number of indexed fields or using object queries can
      also speed up execution.
    question: How can I troubleshoot search performance issues?
  - answer: Yes, you can enable synonym dictionaries and fuzzy search via the `SearchOptions`
      class to broaden matching without sacrificing relevance. The `SearchOptions`
      class configures advanced search behavior such as synonyms and fuzzy matching.
    question: Is there support for synonyms or fuzzy matching?
  type: FAQPage
tags:
- document indexing
- GroupDocs.Search
- Java search library
- search API
- indexing tutorial
title: Come indicizzare documenti con GroupDocs.Search per Java
type: docs
url: /it/java/searching/master-document-search-groupdocs-java/
weight: 1
---

# Come indicizzare documenti con GroupDocs.Search per Java

Nel mondo odierno guidato dai dati, **come indicizzare documenti** in modo efficiente è una competenza fondamentale per qualsiasi sviluppatore Java che gestisce grandi collezioni di file. Che tu stia elaborando contratti legali, bilanci finanziari o report interni, un indice di ricerca ben costruito ti consente di trovare l'esatta informazione in pochi secondi anziché ore di scansione manuale. Questo tutorial ti guida nella creazione di un indice di ricerca, nell'aggiunta di documenti e nell'esecuzione di query sia basate su testo sia basate su oggetti con GroupDocs.Search per Java.

## Risposte rapide
- **Qual è il primo passo per indicizzare i documenti?** Crea un'istanza `Index` che punti a una cartella dove verranno memorizzati i file dell'indice.  
- **Quale metodo aggiunge documenti a un indice?** Chiama `index.add("PATH_TO_DOCUMENTS")` per scansionare una directory e importare i file supportati.  
- **Posso cercare intervalli numerici?** Sì – utilizza una query testuale come `"400 ~~ 4000"` o una query oggetto tramite `SearchQuery.createNumericRangeQuery`. Il metodo `createNumericRangeQuery` crea un oggetto di query per intervalli numerici.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per la valutazione; una licenza commerciale sblocca l'intero set di funzionalità e rimuove i limiti di utilizzo.  
- **Quale versione di Java è richiesta?** È supportato JDK 8 o superiore.

## Cos'è indicizzare documenti con GroupDocs.Search?
Indicizzare i documenti crea un archivio di token ricercabili per ogni file, consentendo al motore di recuperare le corrispondenze senza leggere i file originali ogni volta. Questa fase di pre‑elaborazione trasforma il contenuto grezzo in un indice ottimizzato che può essere interrogato in millisecondi. L'indice memorizza termini, posizioni e metadati, permettendo ricerche rapide di frasi e prossimità su tutti i tipi di documento supportati.

## Perché usare GroupDocs.Search per Java?
Le operazioni di ricerca si completano tipicamente in meno di 50 ms su una collezione di 10 000 file (media 1 KB ciascuno) in esecuzione su una VM standard 2‑CPU, 8 GB. La libreria supporta **oltre 30 formati di input e output**—inclusi PDF, DOCX, XLSX, PPTX, TXT e HTML—così puoi indicizzare praticamente qualsiasi documento aziendale senza convertitori aggiuntivi. La sua API flessibile ti consente di combinare query di testo semplice, intervalli numerici e query oggetto complesse, mentre gli aggiornamenti incrementali ti permettono di aggiungere nuovi file senza ricostruire l'intero indice.

## Prerequisiti
- Maven installato per la gestione delle dipendenze.  
- Un IDE come IntelliJ IDEA o Eclipse.  
- Conoscenze di base di Java (concetti OOP, gestione delle eccezioni).  

## Configurazione di GroupDocs.Search per Java
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

### Download diretto
Puoi anche scaricare l'ultimo JAR da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Passaggi per l'acquisizione della licenza
1. **Prova gratuita** – esplora la libreria senza costi.  
2. **Licenza temporanea** – richiedi una chiave a breve termine per una valutazione estesa.  
3. **Acquisto** – ottieni una licenza completa per l'uso in produzione.

## Inizializzazione e configurazione di base
Per **aggiungere documenti all'indice**, devi prima creare un oggetto `Index` che punti alla cartella dove verranno memorizzati i file dell'indice:

`Index` è la classe principale che rappresenta un indice ricercabile su disco.  
```java
import com.groupdocs.search.Index;

// Initialize the index by specifying a directory path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");
```

Questa riga crea (o apre) un indice pronto a ricevere documenti.

## Guida all'implementazione
### Creazione e indicizzazione di documenti
#### Come aggiungere documenti all'indice
Il metodo `add` scansiona una cartella e memorizza i dati ricercabili per ogni file. Processa ricorsivamente tutti i documenti supportati, estrae testo e metadati e scrive i token nella cartella dell'indice specificata in precedenza.

```java
import com.groupdocs.search.Index;

// Initialize an index at the specified path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");

// Add documents from a directory for indexing
index.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Parametri:** La stringa del percorso indica la cartella contenente i file da indicizzare.  
- **Scopo:** Dopo questo passaggio, l'indice contiene token da tutti i tipi di documento supportati, consentendo ricerche rapide su tutta la collezione.

## Ricerca con query testuale
#### Come eseguire una ricerca di intervallo numerico basata su testo
Puoi cercare usando una semplice stringa che definisce un intervallo. Il motore interpreta l'operatore `~~` come “tra” e restituisce tutti i documenti contenenti numeri entro i limiti specificati.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define a query for numeric values within a specific range
String query1 = "400 ~~ 4000";

// Execute text-based search on indexed data
SearchResult result1 = index.search(query1);
```

- **Parametri:** La stringa di query `"400 ~~ 4000"` indica al motore di trovare numeri tra 400 e 4000.  
- **Valore di ritorno:** `SearchResult` contiene l'elenco dei documenti corrispondenti e evidenzia i frammenti corrispondenti.

## Ricerca con query oggetto
#### Come utilizzare una query oggetto per intervalli numerici
Le query basate su oggetti ti offrono un controllo programmatico sui criteri di ricerca, consentendo di combinare più condizioni o costruire query dinamicamente a runtime.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Create a numeric range query object
SearchQuery query2 = SearchQuery.createNumericRangeQuery(400, 4000);

// Perform search using the query object
SearchResult result2 = index.search(query2);
```

- **Parametri:** `createNumericRangeQuery` riceve gli interi di inizio e fine.  
- **Scopo:** Questo metodo è ideale quando è necessario filtrare i risultati per campi numerici come totali di fatture, età o codici prodotto.

## Applicazioni pratiche
Ecco alcuni scenari reali in cui **indicizzare documenti** diventa un elemento decisivo:

1. **Gestione di documenti legali** – individua clausole, numeri di caso o date su migliaia di contratti in pochi secondi.  
2. **Reportistica finanziaria** – estrai transazioni che rientrano in un intervallo monetario specifico senza scansionare ogni foglio di calcolo.  
3. **Tracciamento dell'inventario** – trova articoli per numeri di serie, codici lotto o intervalli SKU su un file system distribuito.  

Integrare GroupDocs.Search con database, archiviazione cloud o code di messaggi può automatizzare ulteriormente i flussi di lavoro dei documenti.

## Considerazioni sulle prestazioni
- **Aggiornamenti regolari dell'indice:** Esegui nuovamente `index.add` per i nuovi file per mantenere l'indice aggiornato.  
- **Gestione delle risorse:** Monitora l'uso dell'heap; gli indici di grandi dimensioni beneficiano di impostazioni di garbage‑collection della JVM ottimizzate.  
- **Ottimizzazione delle query:** Usa query oggetto per filtri complessi per ridurre scansioni non necessarie e migliorare i tempi di risposta.

## Problemi comuni e soluzioni
| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **La ricerca non restituisce risultati** | Indice non costruito o percorso della cartella errato | Verifica che `index.add` sia stato eseguito nella directory corretta e che la cartella dell'indice sia scrivibile. |
| **OutOfMemoryError durante l'indicizzazione** | File molto grandi o heap insufficiente | Aumenta il valore JVM `-Xmx` o indicizza i file in batch più piccoli. |
| **Formato file non supportato** | Tipo di file non riconosciuto da GroupDocs.Search | Assicurati che l'estensione sia nella lista dei formati supportati (PDF, DOCX, XLSX, PPTX, TXT, HTML, ecc.). |

## Domande frequenti
**Q: Come aggiornare un indice esistente con nuovi documenti?**  
A: Chiama nuovamente `index.add("NEW_DOCUMENT_PATH")`; la libreria unisce le nuove voci senza ricreare l'intero indice.

**Q: GroupDocs.Search può gestire diversi formati di file?**  
A: Sì, supporta oltre 30 formati—tra cui PDF, DOCX, XLSX, PPTX, TXT e HTML—così puoi indicizzare praticamente qualsiasi documento aziendale.

**Q: Quali sono i requisiti di sistema per utilizzare GroupDocs.Search?**  
A: Runtime Java 8+, almeno 2 GB di RAM per collezioni modeste (insiemi più grandi beneficiano di 4 GB+), e accesso in lettura/scrittura alla cartella dell'indice.

**Q: Come posso risolvere i problemi di prestazioni della ricerca?**  
A: Mantieni l'indice aggiornato, profila le tue query e rivedi le impostazioni di memoria della JVM. Ridurre il numero di campi indicizzati o utilizzare query oggetto può anche velocizzare l'esecuzione.

**Q: È disponibile il supporto per sinonimi o corrispondenza fuzzy?**  
A: Sì, puoi abilitare dizionari di sinonimi e ricerca fuzzy tramite la classe `SearchOptions` per ampliare le corrispondenze senza sacrificare la rilevanza. La classe `SearchOptions` configura comportamenti di ricerca avanzati come sinonimi e corrispondenza fuzzy.

---

**Ultimo aggiornamento:** 2026-08-10  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Come aggiungere documenti all'indice con indicizzazione dei metadati in Java usando GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Come aggiungere documenti all'indice e gestire alias in GroupDocs.Search per Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
- [Come aggiornare l'indice Java con GroupDocs.Search – Guida completa](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)