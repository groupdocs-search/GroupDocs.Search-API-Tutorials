---
date: '2026-08-05'
description: Scopri come creare un estrattore di log file per la full-text search
  in Java usando GroupDocs.Search. Aggiungi documenti all'index, ottimizza le search
  performance e gestisci grandi log file in modo efficiente.
keywords:
- full text search java
- optimize search performance
- add documents to index
- java full text search
lastmod: '2026-08-05'
og_description: Il tutorial Full text search java mostra come costruire un estrattore
  di log file personalizzato usando GroupDocs.Search, aggiungere documenti all'index
  e ottimizzare le search performance per enormi archivi di log.
og_image_alt: Diagram of log file extractor workflow in Java using GroupDocs.Search
og_title: 'Full text search java: estrattore di log file con GroupDocs'
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  headline: 'Full text search java: log file extractor with GroupDocs'
  type: TechArticle
- description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  name: 'Full text search java: log file extractor with GroupDocs'
  steps:
  - name: define the custom extractor
    text: '`TextExtractorBase` is the abstract base class you extend to create a custom
      extractor. It declares which file extensions the extractor supports and contains
      the core extraction logic. **Key points** - `getFileExtensions()` registers
      the extractor for `.log` files. - `extractText` is where you can s'
  - name: configure index settings with the extractor
    text: Add your extractor to the `IndexSettings` and enable `autoReindex` so new
      logs are indexed automatically without manual intervention. `IndexSettings`
      configures index behavior such as memory limits and custom extractors. `autoReindex`
      automatically updates the index when source files change.
  - name: add documents to the index
    text: Now that the index recognises log files, you can **add documents to index**
      just like any other supported format.
  - name: search the index
    text: Perform plain‑text queries. The custom extractor guarantees that every log
      entry is searchable.
  type: HowTo
- questions:
  - answer: The default extractor handles common formats (PDF, DOCX, etc.). A custom
      log file extractor lets you define exactly how plain‑text log entries are parsed
      and indexed.
    question: How does a log file extractor differ from the default extractor?
  - answer: Yes, by adding a pre‑processing step that extracts files from the archive
      before feeding them to the index.
    question: Can I index compressed log archives (e.g., .zip)?
  - answer: Enable `autoReindex` and schedule a background watcher that calls `index.add(newLogFile)`
      whenever a new file appears.
    question: What’s the best way to keep the index up‑to‑date with continuously generated
      logs?
  - answer: Practically, the limit is bound by available memory. Splitting very large
      logs into smaller chunks before indexing is recommended.
    question: Is there a limit to the size of a single log file that can be indexed?
  - answer: Yes, the search API includes fuzzy matching, wildcards, and proximity
      queries to improve result relevance.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs
- Java search
- log file extractor
- indexing
title: 'Full text search java: estrattore di log file con GroupDocs'
type: docs
url: /it/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# Ricerca full‑text java: estrattore di file di log con GroupDocs

La ricerca full‑text java è una pietra miliare per qualsiasi sistema che deve individuare rapidamente informazioni all'interno di collezioni massive di documenti. In questo tutorial imparerai a configurare GroupDocs.Search, creare un estrattore di file di log personalizzato, aggiungere documenti all'indice e ottimizzare le prestazioni di ricerca quando si gestiscono gigabyte di dati di log.

## Cosa imparerai
- Imposta e configura GroupDocs.Search per Java.  
- Implementa un **estrattore di file di log** che analizza i log di testo semplice nel modo necessario.  
- **Aggiungi documenti all'indice** insieme a PDF, DOCX e altri formati.  
- Scenari reali in cui un **estrattore di file di log** aggiunge valore misurabile.  
- Consigli comprovati per **ottimizzare le prestazioni di ricerca** per archivi di log multi‑gigabyte.

## Risposte rapide
- **Che cos'è un estrattore di file di log?** Un componente personalizzato che indica a GroupDocs.Search come leggere e indicizzare i file di log di testo semplice.  
- **Perché usare GroupDocs.Search?** Supporta l'indicizzazione di oltre 50 formati, fornisce il re‑indicizzazione automatica e gestisce indici fino a 10 GB con meno di 2 GB di RAM.  
- **È necessaria una licenza?** Sì – è necessaria una licenza di prova o completa per abilitare la libreria.  
- **Posso indicizzare altri tipi di file contemporaneamente?** Assolutamente; mescola PDF, DOCX e file di log personalizzati nello stesso indice.  
- **Come migliorare le prestazioni?** Usa l'indicizzazione incrementale, regola `IndexSettings` e abilita il flag `autoReindex`.

## Prerequisiti

Prima di iniziare, assicurati di avere quanto segue:

### Librerie richieste
Aggiungi la dipendenza Maven di GroupDocs.Search al tuo `pom.xml`. Usa l'ultima versione che corrisponde al livello Java del tuo progetto.

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

### Configurazione dell'ambiente
- JDK 8 o superiore.  
- Familiarità con la programmazione Java e i concetti di base della gestione dei file.

### Acquisizione della licenza
Inizia scaricando una licenza di prova gratuita per esplorare le funzionalità di GroupDocs.Search. Per l'uso in produzione, acquista una licenza completa o richiedi una temporanea tramite [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).

## Configurazione di GroupDocs.Search per Java

Per iniziare, inizializza la libreria e applica il tuo file di licenza:

1. **Configurazione Maven** – conferma che la dipendenza del passaggio precedente sia presente.  
2. **Inizializzazione della licenza** – carica il file di licenza prima di qualsiasi altra chiamata API.

```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

Con l'ambiente pronto, puoi passare alla creazione dell'**estrattore di file di log** personalizzato.

## Che cos'è un estrattore di file di log?

Un estrattore di file di log è un pezzo di codice che indica a GroupDocs.Search come leggere i file di log grezzi (solitamente `.log`) e trasformare il loro contenuto in testo ricercabile. Fornendo il tuo estrattore ottieni il pieno controllo sulle regole di parsing, sul filtraggio del rumore e sull'estrazione solo delle informazioni rilevanti per il tuo caso d'uso di ricerca.

## Crea un estrattore di file di log

GroupDocs.Search ti permette di collegare estrattori di testo personalizzati per qualsiasi tipo di file. Segui questi passaggi per crearne uno per i file di log.

### Passo 1: definire l'estrattore personalizzato
`TextExtractorBase` è la classe base astratta che estendi per creare un estrattore personalizzato. Dichiarare quali estensioni di file supporta l'estrattore e contiene la logica di estrazione principale.

```java
import com.groupdocs.search.extractors.TextExtractorBase;

public class LogExtractor extends TextExtractorBase {
    @Override
    public String[] getFileExtensions() {
        return new String[]{"log"};
    }

    @Override
    public String extractText(String documentContent) {
        // Custom logic for extracting text from log files.
        return documentContent; // Implement your custom extraction here.
    }
}
```

**Punti chiave**  
- `getFileExtensions()` registra l'estrattore per i file `.log`.  
- `extractText` è dove puoi rimuovere i timestamp, filtrare le linee di debug o applicare qualsiasi pre‑elaborazione necessaria per **cercare grandi file di log**.

### Passo 2: configurare le impostazioni dell'indice con l'estrattore
Aggiungi il tuo estrattore a `IndexSettings` e abilita `autoReindex` così i nuovi log vengono indicizzati automaticamente senza intervento manuale.

`IndexSettings` configura il comportamento dell'indice, come i limiti di memoria e gli estrattori personalizzati.  
`autoReindex` aggiorna automaticamente l'indice quando i file sorgente cambiano.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

public class CustomTextExtractorFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        IndexSettings settings = new IndexSettings();
        
        // Adding the custom text extractor to the settings.
        settings.getCustomExtractors().addItem(new LogExtractor());
        
        // Creating or loading an index with specified settings and enabling auto-reindexing.
        Index index = new Index(indexFolder, settings, true);
    }
}
```

### Passo 3: aggiungere documenti all'indice
Ora che l'indice riconosce i file di log, puoi **aggiungere documenti all'indice** proprio come per qualsiasi altro formato supportato.

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Loading or creating an index in the specified directory.
        Index index = new Index(indexFolder);
        
        // Adding documents from the folder to the index.
        index.add(documentsFolder);
    }
}
```

### Passo 4: cercare nell'indice
Esegui query di testo semplice. L'estrattore personalizzato garantisce che ogni voce di log sia ricercabile.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchDocumentsFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        
        // Loading the existing index.
        Index index = new Index(indexFolder);
        
        // Define search queries
        String query1 = "objection";
        String query2 = "log";
        
        // Performing searches and retrieving results.
        SearchResult result1 = index.search(query1);
        SearchResult result2 = index.search(query2);
    }
}
```

## Consigli per ottimizzare le prestazioni di ricerca

- **Indicizzazione incrementale** – aggiungi solo i file di log nuovi o modificati invece di ricostruire l'intero indice.  
- **Gestione della memoria** – il flag `autoReindex` mantiene basso l'uso della RAM svuotando i dati intermedi su disco.  
- **Impostazioni dell'indice** – regola `setMaxMemoryUsage` in base alla capacità del tuo server; un'impostazione tipica è 1 GB per un indice da 10 GB.  
- **Ottimizzazione delle query** – usa query di frase, wildcard o filtri per restringere i risultati durante la ricerca in enormi archivi di log.

## Applicazioni pratiche

GroupDocs.Search può essere applicato in molti scenari reali, come:

- **Gestione dei log** – individua messaggi di errore, azioni degli utenti o timestamp specifici attraverso gigabyte di dati di log in pochi secondi.  
- **Sistemi di recupero documenti** – mantieni un unico repository ricercabile che includa PDF, documenti Word, fogli di calcolo e file di log personalizzati.  
- **Analisi dei contenuti** – genera report di frequenza delle parole chiave o rileva anomalie nei dati di log in streaming.

## Considerazioni sulle prestazioni

Quando distribuisci GroupDocs.Search su larga scala, tieni presente queste best practice:

- Memorizza gli indici su SSD veloci per ridurre al minimo la latenza di lettura/scrittura.  
- Monitora l'uso dell'heap JVM; considera di spostare gli indici grandi in un processo separato se la memoria diventa un collo di bottiglia.  
- Abilita `autoReindex` (come mostrato) per mantenere l'indice aggiornato senza ricostruzione manuale.

## Conclusione

A questo punto hai costruito un **estrattore di file di log**, imparato a **aggiungere documenti all'indice** e scoperto come **ottimizzare le prestazioni di ricerca** per grandi archivi di log. Questa combinazione consente alle tue applicazioni Java di fornire una ricerca full‑text veloce e accurata su qualsiasi tipo di documento.

Per approfondire, consulta la documentazione ufficiale di [GroupDocs documentation](https://docs.groupdocs.com/search/java/) o sperimenta con diverse implementazioni di estrattori per adattarle al tuo caso d'uso unico.

## Sezione FAQ
1. **Quali tipi di file posso indicizzare usando GroupDocs.Search?**  
   - Puoi indicizzare PDF, documenti Word, fogli di calcolo e molti altri formati, oltre a file di log personalizzati tramite estrattori di testo.  
2. **Come gestisco collezioni di documenti molto grandi in modo efficiente?**  
   - Usa aggiornamenti incrementali, partiziona gli indici e regola `IndexSettings` per gestire le risorse in modo efficace.  
3. **GroupDocs.Search può essere integrato con altri sistemi?**  
   - Sì, offre un'API Java pulita che può essere incorporata in servizi esistenti, micro‑servizi o applicazioni web.  
4. **Cos'è una licenza temporanea e come posso ottenerne una?**  
   - Una licenza temporanea garantisce la piena funzionalità per la valutazione senza limiti di tempo. Richiedila tramite [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).

## Domande frequenti

**Q: In che modo un estrattore di file di log differisce dall'estrattore predefinito?**  
A: L'estrattore predefinito gestisce i formati comuni (PDF, DOCX, ecc.). Un estrattore di file di log personalizzato ti consente di definire esattamente come le voci di log di testo semplice vengono analizzate e indicizzate.

**Q: Posso indicizzare archivi di log compressi (ad es., .zip)?**  
A: Sì, aggiungendo un passaggio di pre‑elaborazione che estrae i file dall'archivio prima di passarli all'indice.

**Q: Qual è il modo migliore per mantenere l'indice aggiornato con log generati continuamente?**  
A: Abilita `autoReindex` e programma un watcher in background che chiama `index.add(newLogFile)` ogni volta che appare un nuovo file.

**Q: Esiste un limite alla dimensione di un singolo file di log che può essere indicizzato?**  
A: Praticamente, il limite è determinato dalla memoria disponibile. Si consiglia di suddividere i log molto grandi in blocchi più piccoli prima dell'indicizzazione.

**Q: GroupDocs.Search supporta ricerche fuzzy o con wildcard?**  
A: Sì, l'API di ricerca include corrispondenza fuzzy, wildcard e query di prossimità per migliorare la rilevanza dei risultati.

---

**Ultimo aggiornamento:** 2026-08-05  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Java Full Text Search: Build Index with GroupDocs.Search](/search/java/dictionaries-language-processing/master-alphabet-dictionary-indexing-groupdocs-search-java/)
- [How to Add Documents to Index with GroupDocs.Search for Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Improve Query Performance with GroupDocs.Search Java: Optimize Index & Search](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)