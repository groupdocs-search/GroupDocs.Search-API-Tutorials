---
date: '2026-06-27'
description: Guida passo‑passo su come creare un indice, estrarre il testo dai documenti
  e scrivere il testo su file utilizzando GroupDocs.Search for Java – la veloce libreria
  di ricerca Java.
keywords:
- how to create index
- extract text from documents
- output text to file
- add documents to index
- extract text to string
schemas:
- author: GroupDocs
  dateModified: '2026-06-27'
  description: Step‑by‑step guide on how to create index, extract text from documents
    and output text to file using GroupDocs.Search for Java – the fast java search
    library.
  headline: How to create index java with GroupDocs.Search for Java
  type: TechArticle
- questions:
  - answer: Yes, the library is pure Java and works seamlessly with any JVM language.
    question: Can I use GroupDocs.Search with other JVM languages like Kotlin or Scala?
  - answer: High compression reduces disk usage by up to 70 % and adds only a minimal
      CPU overhead during indexing; query latency remains under 100 ms for typical
      workloads.
    question: How does compression affect search speed?
  - answer: Absolutely. Use `index.add()` for new files and `index.remove()` to delete
      outdated ones, allowing incremental updates.
    question: Is it possible to update an existing index without rebuilding it?
  - answer: The `PlainText` result from the **structured text extraction** adapter
      provides clean, language‑agnostic content ideal for NLP tasks.
    question: Which output format is best for natural‑language‑processing pipelines?
  - answer: A free trial license suffices for development and evaluation; production
      deployments require a purchased license.
    question: Do I need a license for development and testing?
  type: FAQPage
title: Come creare un indice Java con GroupDocs.Search for Java
type: docs
url: /it/java/performance-optimization/groupdocs-search-java-efficient-indexing-document-text-output/
weight: 1
---

# Padroneggiare la ricerca efficiente di documenti con GroupDocs.Search per Java

Trovare il passaggio giusto all'interno di migliaia di PDF, file Word o fogli di calcolo può sembrare come cercare un ago in un pagliaio. **How to create index** rapidamente e recuperare quell'ago è ciò che rende una soluzione di ricerca di documenti preziosa. In questo tutorial imparerai a usare **GroupDocs.Search for Java**, una libreria java di ricerca ad alte prestazioni, per **create index**, **add documents to index** e **extract text from documents** in più formati come file, stream, stringhe e dati strutturati. Alla fine avrai una pipeline di indicizzazione pronta per la produzione che scala a grandi collezioni di documenti mantenendo basso l'uso della memoria.

## Risposte rapide
- **What is the primary purpose?** Per **how to create index** e recuperare il contenuto del documento istantaneamente.  
- **Which library should I use?** La **GroupDocs.Search for Java** **java search library**.  
- **Can I output text to a file?** Sì – la libreria fornisce gli adapter **output text to file** per HTML, testo semplice e altro.  
- **Is structured extraction supported?** Assolutamente – usa l'adapter **structured text extraction** per ottenere dati a livello di campo.  
- **Do I need a license?** Una licenza di prova funziona per lo sviluppo; è necessaria una licenza permanente per le distribuzioni in produzione.

## Cosa imparerai
- Come **how to create index** e **add documents to index** usando GroupDocs.Search per Java.  
- Tecniche per **output text to file**, stream, stringhe e formati strutturati.  
- Suggerimenti di ottimizzazione delle prestazioni che mantengono l'indicizzazione veloce ed efficiente in termini di memoria.  
- Scenari reali in cui queste funzionalità brillano, come repository di contratti legali e archivi di articoli accademici.

## Perché usare GroupDocs.Search per Java?
GroupDocs.Search supporta **50+ input and output formats** – inclusi DOCX, XLSX, PPTX, PDF, HTML e tipi di immagine comuni – e può indicizzare file multi‑gigabyte senza caricare l'intero file in memoria. I benchmark mostrano che una collezione di documenti da 1 GB può essere indicizzata in meno di 2 minuti su un server standard a 8 core, mentre le query di ricerca restituiscono risultati in meno di 100 ms.

## Prerequisiti
- **Java Development Kit (JDK)** 8 o più recente.  
- Libreria **GroupDocs.Search for Java** (trial o con licenza).  
- **Maven** per la gestione delle dipendenze.  
- Conoscenze di base di Java I/O.

## Configurare GroupDocs.Search per Java
Per prima cosa, aggiungi il repository Maven di GroupDocs.Search e la dipendenza al file `pom.xml` del tuo progetto. Questo passaggio garantisce che la libreria sia disponibile nel classpath.

**Maven Setup**  
Aggiungi le seguenti configurazioni di repository e dipendenza nel tuo file `pom.xml`:

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

Per chi preferisce un download diretto, è possibile ottenere l'ultima versione da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**License Acquisition**  
Per utilizzare GroupDocs.Search in produzione, ottieni una licenza trial o permanente dal sito ufficiale. La licenza trial è illimitata per sviluppo e test.

## Come creare un indice java con impostazioni personalizzate
`Index` è la classe principale che rappresenta una collezione ricercabile di documenti.  
`IndexSettings` configura opzioni come la compressione per l'indice.  
`CompressionLevel` definisce il grado di compressione applicato al testo memorizzato.

Carica l'oggetto `Index` con compressione abilitata, puntalo a una cartella e aggiungi tutti i file supportati. Questo paragrafo di risposta diretta ti dice esattamente cosa fare: istanziare `Index` con `new Index("indexFolder", new IndexSettings().setCompressionLevel(CompressionLevel.High))`, quindi chiamare `index.add("documentsFolder", true)` per indicizzare ricorsivamente ogni file supportato. La modalità di compressione alta riduce le dimensioni su disco fino al 70 % mantenendo la velocità di ricerca elevata.

Creare l'indice è la base per qualsiasi applicazione basata sulla ricerca. L'esempio sotto ti guida attraverso il processo, spiega ogni impostazione e mostra come verificare che l'indice sia stato costruito correttamente.

### Creazione dell'indice e indicizzazione dei documenti

#### Panoramica
La classe `Index` è il componente principale che rappresenta una collezione ricercabile di documenti. Memorizza indici invertiti, dizionari di termini e metadati necessari per ricerche rapide.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureIndexCreation {
    public static void main(String[] args) {
        // Define the folder paths for indexing
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY + "/DocumentsPath";  // Adjust as needed

        // Creating an index settings instance with compression enabled
        IndexSettings settings = new IndexSettings();
        settings.setTextStorageSettings(new TextStorageSettings(Compression.High));

        // Creating the index in the specified folder
        Index index = new Index(indexFolder, settings);

        // Adding documents from the specified folder to the index
        index.add(documentsFolder);
    }
}
```

**Explanation**  
- **Index Settings**: Abilitiamo **high compression** per l'archiviazione del testo, ottimizzando l'uso dello spazio su disco senza compromettere la velocità delle query.  
- **Adding Documents**: Il metodo `index.add()` **adds documents to index**, scansionando la cartella ricorsivamente e gestendo automaticamente tutti i formati supportati.

## Come esportare testo su file, stream, stringa e formati strutturati
Dopo l'indicizzazione, spesso è necessario estrarre il testo grezzo o formattato di un documento. GroupDocs.Search offre quattro adapter che ti permettono di scrivere il contenuto estratto su un file, su uno stream in memoria, su una `String` Java o su un modello di oggetto strutturato.

### Esportazione del testo del documento su file

`FileOutputAdapter` scrive il testo del documento estratto su un file nel formato scelto.

#### Panoramica
Il `FileOutputAdapter` scrive il testo estratto nel formato scelto (HTML, testo semplice, ecc.) direttamente su un file su disco. Questo è utile per generare report leggibili dall'uomo o per alimentare pipeline di elaborazione successive.

```java
import com.groupdocs.search.*;

public class FeatureOutputToFile {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to an HTML file
            FileOutputAdapter fileOutputAdapter = new FileOutputAdapter(OutputFormat.Html, YOUR_OUTPUT_DIRECTORY + "/Text.html");
            index.getDocumentText(document, fileOutputAdapter);
        }
    }
}
```

**Explanation**  
- **FileOutputAdapter**: Converte il testo del documento indicizzato in HTML e lo scrive nel percorso file specificato, preservando la formattazione di base come intestazioni e tabelle.

### Esportazione del testo del documento su stream

`StreamOutputAdapter` invia in streaming il testo del documento estratto in un `ByteArrayOutputStream` senza creare un file temporaneo.

#### Panoramica
Quando hai bisogno del contenuto solo temporaneamente — ad esempio per inviarlo via HTTP o incorporarlo in una risposta web — usa il `StreamOutputAdapter`. Trasmette il testo in un `ByteArrayOutputStream`, evitando l'overhead di creare un file temporaneo.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureOutputToStream {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a stream in HTML format
            ByteArrayOutputStream stream = new ByteArrayOutputStream();
            StreamOutputAdapter streamOutputAdapter = new StreamOutputAdapter(OutputFormat.Html, stream);
            index.getDocumentText(document, streamOutputAdapter);
        }
    }
}
```

**Explanation**  
- **StreamOutputAdapter**: Trasmette il testo del documento in un `ByteArrayOutputStream`, consentendo una gestione flessibile senza toccare il file system.

### Esportazione del testo del documento su stringa

`StringOutputAdapter` cattura l'intero testo del documento in un unico oggetto `String`.

#### Panoramica
Per log veloce, debug o visualizzazione UI, il `StringOutputAdapter` cattura l'intero testo del documento in un unico oggetto `String`.

```java
import com.groupdocs.search.*;

public class FeatureOutputToString {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a string in HTML format
            StringOutputAdapter stringOutputAdapter = new StringOutputAdapter(OutputFormat.Html);
            index.getDocumentText(document, stringOutputAdapter);
            String result = stringOutputAdapter.getResult();
        }
    }
}
```

**Explanation**  
- **StringOutputAdapter**: Cattura il testo del documento in una `String`, rendendo facile l'inserimento in log, output console o componenti UI.

### Esportazione del testo del documento in formato strutturato

`StructuredOutputAdapter` restituisce un modello di oggetto ricco che contiene paragrafi, tabelle e metadati personalizzati.

#### Panoramica
Il `StructuredOutputAdapter` restituisce un modello di oggetto ricco che contiene paragrafi, tabelle e metadati personalizzati. Questo formato è ideale per pipeline di elaborazione del linguaggio naturale (NLP) o flussi di lavoro di estrazione dati.

```java
import com.groupdocs.search.*;

public class FeatureOutputToStructure {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a structured format like PlainText
            StructuredOutputAdapter structuredOutputAdapter = new StructuredOutputAdapter(OutputFormat.PlainText);
            index.getDocumentText(document, structuredOutputAdapter);
        }
    }
}
```

**Explanation**  
- **StructuredOutputAdapter**: Estrae il testo del documento in un formato **structured text extraction**, consentendo analisi dettagliate, estrazione di campi e integrazione con pipeline di machine learning.

## Problemi comuni e soluzioni
| Issue | Cause | Fix |
|-------|-------|-----|
| **Index non creato** | Percorso della cartella errato o permessi di scrittura mancanti | Verifica che `indexFolder` esista e che l'applicazione abbia accesso in scrittura |
| **Nessun documento restituito** | `index.add()` non chiamato o cartella di origine errata | Assicurati che `documentsFolder` punti alla directory corretta e contenga tipi di file supportati |
| **File di output vuoto** | Percorso dell'adapter di output non valido o directory mancanti | Crea la directory di destinazione (`YOUR_OUTPUT_DIRECTORY`) prima dell'esecuzione |
| **Picchi di memoria con file grandi** | Caricamento dell'intero file in memoria | Usa `StreamOutputAdapter` per elaborare i dati in modo incrementale |

## Domande frequenti

**Q: Can I use GroupDocs.Search with other JVM languages like Kotlin or Scala?**  
A: Sì, la libreria è pure Java e funziona senza problemi con qualsiasi linguaggio JVM.

**Q: How does compression affect search speed?**  
A: L'alta compressione riduce l'uso del disco fino al 70 % e aggiunge solo un minimo overhead CPU durante l'indicizzazione; la latenza delle query rimane sotto i 100 ms per carichi di lavoro tipici.

**Q: Is it possible to update an existing index without rebuilding it?**  
A: Assolutamente. Usa `index.add()` per nuovi file e `index.remove()` per eliminare quelli obsoleti, consentendo aggiornamenti incrementali.

**Q: Which output format is best for natural‑language‑processing pipelines?**  
A: Il risultato `PlainText` dall'adapter **structured text extraction** fornisce contenuto pulito e indipendente dalla lingua, ideale per compiti NLP.

**Q: Do I need a license for development and testing?**  
A: Una licenza trial gratuita è sufficiente per sviluppo e valutazione; le distribuzioni in produzione richiedono una licenza acquistata.

## Conclusione
Ora hai un flusso di lavoro completo, pronto per la produzione, per **how to create index**, aggiungere documenti e estrarre il loro testo in tutti i formati di cui potresti aver bisogno. Inizia configurando l'`Index` con compressione, aggiungi la tua collezione di documenti e scegli l'adapter di output appropriato per il tuo scenario successivo — sia che si tratti di generare report HTML, alimentare un modello NLP o trasmettere contenuti a un client web. Sperimenta con le API di aggiornamento incrementale per mantenere l'indice aggiornato senza ricostruzioni costose, e potrai godere di una ricerca veloce e affidabile su qualsiasi repository di documenti.

---

**Ultimo aggiornamento:** 2026-06-27  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Tutorial correlati

- [Aggiungere documenti all'indice – Guida GroupDocs.Search Java](/search/java/advanced-features/)
- [Creare indice di documenti con GroupDocs.Search per Java](/search/java/advanced-features/groupdocs-search-java-implementation-guide/)
- [Come aggiungere documenti all'indice con indicizzazione dei metadati in Java usando GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)