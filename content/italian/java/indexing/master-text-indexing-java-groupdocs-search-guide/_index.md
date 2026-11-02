---
date: '2026-11-02'
description: Scopri come aggiungere una cartella all'indice con GroupDocs.Search in
  Java, configurare un'alta compressione e eseguire query full-text veloci.
keywords:
- add folder to index
- java full text search
- groupdocs search compression
lastmod: '2026-11-02'
og_description: Scopri come aggiungere una cartella all'indice con GroupDocs.Search
  in Java, configurare la compressione e eseguire ricerche full-text rapide. Ideale
  per grandi insiemi di documenti.
og_image_alt: Guide showing Java code for adding a folder to a GroupDocs.Search index
og_title: Come aggiungere una cartella all'indice con GroupDocs.Search in Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  headline: How to add folder to index with GroupDocs.Search in Java
  type: TechArticle
- description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  name: How to add folder to index with GroupDocs.Search in Java
  steps:
  - name: define the index folder
    text: 'Choose a directory where the index files will reside:'
  - name: configure index settings
    text: '`TextStorageSettings` configures how text is stored in the index, including
      compression level. `Compression` is an enum that specifies the desired compression
      algorithm.'
  - name: create the index with custom settings
    text: 'Instantiate the index using the configuration defined above:'
  type: HowTo
- questions:
  - answer: It is a robust Java library that provides advanced full‑text search capabilities,
      including indexing, compression, and complex query support.
    question: What is GroupDocs.Search?
  - answer: Enable high compression (`Compression.High`) and periodically commit changes
      to keep the index lean. Also, allocate sufficient heap memory (e.g., 4 GB for
      indexes over 20 GB).
    question: How do I handle large datasets with GroupDocs.Search?
  - answer: Yes, the library can be embedded in any Java‑based backend, REST services,
      or micro‑services architecture.
    question: Can I integrate GroupDocs.Search with existing enterprise systems?
  - answer: Use the `index.add()` method to append new files and `index.delete()`
      to remove obsolete ones, then re‑run `index.optimize()` if needed.
    question: What if my index becomes outdated?
  - answer: Visit the community forum at [GroupDocs forums](https://forum.groupdocs.com/c/search/10)
      for troubleshooting and best‑practice tips.
    question: Where can I get help or support?
  type: FAQPage
tags:
- add folder to index
- groupdocs search
- java search indexing
title: Come aggiungere una cartella all'indice con GroupDocs.Search in Java
type: docs
url: /it/java/indexing/master-text-indexing-java-groupdocs-search-guide/
weight: 1
---

# Come aggiungere una cartella all'indice con GroupDocs.Search in Java

Se hai bisogno di **java full text search** che possa scalare a milioni di documenti, sei nel posto giusto. In questo tutorial imparerai come **add folder to index** usando GroupDocs.Search, configurare l'archiviazione ad alta compressione e eseguire query fulminee. Alla fine avrai una soluzione pronta per la produzione che potrai inserire in qualsiasi progetto Java.

## Risposte rapide
- **Qual è la libreria principale?** GroupDocs.Search for Java  
- **Come aggiungere una cartella all'indice?** Use `index.add(folderPath)`  
- **Posso configurare la compressione del testo?** Yes, via `TextStorageSettings(Compression.High)`  
- **Quale versione di Java è richiesta?** JDK 8 or higher  
- **Dove ottenere una licenza di prova?** From the GroupDocs website or the repository page  

## Che cos'è la ricerca full text java e perché è importante?
La ricerca full text java converte i documenti grezzi in un indice invertito, consentendo il recupero in meno di un secondo di qualsiasi termine su migliaia di file. Questa capacità è essenziale per repository legali, biblioteche di ricerca e basi di conoscenza aziendali dove gli utenti si aspettano risultati istantanei. Inoltre migliora la produttività nelle applicazioni moderne.

## Perché usare groupdocs.search per la ricerca full text java?
GroupDocs.Search offre indicizzazione ad alta velocità e esecuzione di query, fornendo al contempo compressione integrata ad alta efficienza. Supporta **50+ input and output formats** — inclusi PDF, DOCX, EML e HTML — e può elaborare documenti di centinaia di pagine senza caricare l'intero file in memoria, mantenendo l'impronta di memoria sotto i 200 MB per carichi di lavoro tipici.

## Prerequisiti
- **GroupDocs.Search for Java** (version 25.4 o successiva) – la libreria core che alimenta l'indicizzazione e la ricerca.  
- **JDK 8+** installato e configurato – il runtime minimo richiesto per l'SDK.  
- **Maven** per la gestione delle dipendenze – semplifica l'aggiunta della libreria al tuo progetto.  
- Un IDE come **IntelliJ IDEA** o **Eclipse** – per scrivere e fare il debug del codice Java.  

## Configurare GroupDocs.Search per java

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
In alternativa, scarica l'ultima versione da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Acquisizione della licenza
- **Free trial** – esplora tutte le funzionalità senza impegno.  
- **Temporary license** – periodo di test esteso.  
- **Purchase** – sblocca tutte le capacità di produzione.  

### Inizializzazione e configurazione di base
`Index` è la classe core usata per creare, aprire e gestire un indice di ricerca.

```java
import com.groupdocs.search.Index;

public class InitializeSearch {
    public static void main(String[] args) {
        // Path to store index data
        String indexPath = "path/to/index";
        
        // Creating an index at specified location
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## Indicizzare testo con compressione personalizzata

### Passo 1: definire la cartella dell'indice
Scegli una directory dove risiederanno i file dell'indice:

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\StoringTextOfIndexedDocuments";
```

### Passo 2: configurare le impostazioni dell'indice
`TextStorageSettings` configura come il testo è memorizzato nell'indice, includendo il livello di compressione. `Compression` è un enum che specifica l'algoritmo di compressione desiderato.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.options.TextStorageSettings;
import com.groupdocs.search.compression.Compression;

IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Passo 3: creare l'indice con impostazioni personalizzate
Istanzia l'indice usando la configurazione definita sopra:

```java
Index index = new Index(indexFolder, settings);
System.out.println("Index created with high compression.");
```

## Come aggiungere una cartella all'indice

`Index` è la classe principale che rappresenta l'indice ricercabile.

Carica l'indice esistente (o creane uno nuovo) e poi chiama il metodo `add` sull'oggetto `Index`. L'operazione `add` scansiona la directory fornita, estrae il testo da ogni file supportato e lo memorizza nell'indice compresso, pronto per la ricerca istantanea.

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual document path.
Index index = new Index(indexFolder);
```

## Come cercare documenti indicizzati

`SearchResult` rappresenta una singola corrispondenza con il percorso del documento e la rilevanza.

Definisci una stringa di query di ricerca che rappresenta il termine o la frase che desideri trovare, quindi invoca il metodo `search` sull'istanza `Index`. Il metodo restituisce una collezione di oggetti `SearchResult`, ognuno dei quali contiene il percorso del documento, il punteggio di rilevanza e un frammento che evidenzia la corrispondenza.

```java
index.add(documentsFolder);
System.out.println("Documents added successfully.");
```

## Applicazioni pratiche

Scenari reali in cui **java full text search** eccelle:

1. **Legal document management** – recupero istantaneo dei fascicoli di caso.  
2. **Academic research libraries** – ricerca rapida di articoli e tesi.  
3. **Enterprise knowledge bases** – accesso veloce a manuali e FAQ.  
4. **Content management systems** – scoperta efficiente dei contenuti per siti di grandi dimensioni.  
5. **Customer service archives** – ricerca rapida di ticket e chat passati.  

## Considerazioni sulle prestazioni
- **Compression vs. speed**: L'alta compressione salva fino al 70 % di spazio su disco ma aggiunge un modesto overhead di indicizzazione; esegui test di benchmark per il volume dei tuoi dati.  
- **Memory management**: Assegna almeno 2 GB di heap per indici più grandi di 10 GB per evitare `OutOfMemoryError`.  
- **Index updates**: Aggiungi incrementalmente nuovi documenti con `index.add()` e chiama periodicamente `index.optimize()` per mantenere l'indice compatto.  
- **Query optimization**: Usa la sintassi avanzata di query (wildcard, prossimità, fuzzy search) per restringere i risultati e ridurre il tempo di risposta.  

## Errori comuni e consigli professionali
- **Pitfall:** Dimenticare di chiamare `index.optimize()` dopo aggiunte massive.  
  **Pro tip:** Esegui `index.optimize()` ogni notte per mantenere l'indice compatto.  

- **Pitfall:** Usare la compressione predefinita (bassa) su dataset massivi.  
  **Pro tip:** Passa a `Compression.High` per gli ambienti di produzione per ridurre i costi di archiviazione.  

- **Pitfall:** Non gestire `IOException` quando si aggiungono file da una condivisione di rete.  
  **Pro tip:** Avvolgi `index.add()` in un blocco try‑catch e registra eventuali errori per una revisione successiva.  

## Domande frequenti
**Q: Cos'è GroupDocs.Search?**  
A: È una robusta libreria Java che fornisce capacità avanzate di ricerca full‑text, includendo indicizzazione, compressione e supporto a query complesse.

**Q: Come gestisco grandi dataset con GroupDocs.Search?**  
A: Abilita l'alta compressione (`Compression.High`) e commetti periodicamente le modifiche per mantenere l'indice snello. Inoltre, assegna sufficiente memoria heap (ad esempio, 4 GB per indici superiori a 20 GB).

**Q: Posso integrare GroupDocs.Search con i sistemi aziendali esistenti?**  
A: Sì, la libreria può essere integrata in qualsiasi backend basato su Java, servizi REST o architettura micro‑services.

**Q: Cosa succede se il mio indice diventa obsoleto?**  
A: Usa il metodo `index.add()` per aggiungere nuovi file e `index.delete()` per rimuovere quelli obsoleti, quindi riesegui `index.optimize()` se necessario.

**Q: Dove posso ottenere aiuto o supporto?**  
A: Visita il forum della community su [GroupDocs forums](https://forum.groupdocs.com/c/search/10) per risolvere problemi e consigli sulle migliori pratiche.

## Risorse aggiuntive
- Guida dettagliata all'uso: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- Riferimento API completo: [API Reference Guide](https://reference.groupdocs.com/search/java)  
- Rimani aggiornato con le nuove funzionalità: [Latest Releases](https://releases.groupdocs.com/search/java/)  

---

**Ultimo aggiornamento:** 2026-11-02  
**Testato con:** GroupDocs.Search 25.4  
**Autore:** GroupDocs  

```java
String query = "sample";  
```

```java
import com.groupdocs.search.results.SearchResult;

SearchResult result = index.search(query);
System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## Tutorial correlati
- [Groupdocs Search Java Create Index Guide](/search/java/indexing/groupdocs-search-java-create-index-guide/)
- [Mastering Groupdocs Search Java Index Management Guide](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Java Full Text Search Library – Optimize Index with GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)