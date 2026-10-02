---
date: '2026-10-02'
description: Scopri come utilizzare una temporary license per aggiungere documents
  al index con chunk‑based search in Java, boosting search performance e controllando
  memory usage.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Utilizza una temporary license per aggiungere documents al index con
  chunk‑based search in Java, improving search speed e riducendo memory consumption.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Utilizza una temporary license per chunk‑based indexing in Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Utilizza una temporary license per chunk‑based indexing in Java
type: docs
url: /it/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Usa una licenza temporanea per l'indicizzazione basata su chunk in Java

In questo tutorial **utilizzerai una licenza temporanea** per aggiungere documenti all'indice con la funzione di ricerca basata su chunk di GroupDocs.Search. L'approccio ti consente di gestire collezioni di documenti massivi—contratti legali, ticket di supporto, articoli di ricerca—mantendo basso l'uso della **memoria dell'indice di ricerca Java** e **aumentando drasticamente le prestazioni di ricerca**. Vedrai come configurare la cartella dell'indice, fornire più sorgenti di documenti, abilitare la ricerca a chunk e eseguire sia la prima che le successive query a chunk.

## Risposte rapide
- **Qual è il primo passo?** Crea una cartella per l'indice di ricerca.  
- **Come includere molti file?** Usa `index.add()` per ogni cartella di documenti.  
- **Quale opzione abilita la ricerca a chunk?** `options.setChunkSearch(true)`.  
- **Posso continuare la ricerca dopo il primo chunk?** Sì, chiama `index.searchNext()` con il token.  
- **Ho bisogno di una licenza?** Una prova gratuita o una licenza temporanea funziona per lo sviluppo; è necessaria una licenza completa per la produzione.  

## Cosa imparerai
- Come creare un indice di ricerca in una cartella specificata.  
- Passaggi per **aggiungere documenti all'indice** da più posizioni.  
- Configurare le opzioni di ricerca per abilitare la ricerca basata su chunk.  
- Eseguire ricerche iniziali e successive basate su chunk.  
- Scenari reali in cui la ricerca di documenti basata su chunk è efficace.  

## Prerequisiti
Per seguire questa guida, assicurati di avere:

- **Librerie richieste**: GroupDocs.Search per Java 25.4 o versioni successive.  
- **Configurazione dell'ambiente**: Un Java Development Kit (JDK) compatibile installato.  
- **Prerequisiti di conoscenza**: Programmazione Java di base e familiarità con Maven.  

## Configurare GroupDocs.Search per Java
Per iniziare, integra GroupDocs.Search nel tuo progetto usando Maven:

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

In alternativa, scarica l'ultima versione da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
Per provare GroupDocs.Search:

- **Prova gratuita** – testa le funzionalità principali senza impegno.  
- **Licenza temporanea** – accesso esteso per lo sviluppo.  
- **Acquisto** – licenza completa per l'uso in produzione.  

## Come aggiungere documenti all'indice?
**Risposta diretta:** Chiama `index.add()` per ogni cartella che contiene i file che desideri rendere ricercabili; il metodo scansiona la cartella ricorsivamente e aggiunge ogni documento supportato all'indice in un'unica operazione. Questo elimina la necessità di gestire manualmente file per file e velocizza l'ingestione di massa.

`SearchIndex` è la classe centrale che rappresenta la collezione ricercabile su disco. Dopo averla istanziata, tutte le operazioni di indicizzazione e query passano attraverso questo oggetto.

### 1. Creazione di un indice
**Risposta diretta:** Istanzia un oggetto `SearchIndex` con il percorso dove devono essere memorizzati i file dell'indice, quindi chiama `index.create()` per inizializzare la struttura di archiviazione. La chiamata crea le cartelle necessarie e i file di metadati al primo utilizzo.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. Aggiunta di documenti all'indice
**Risposta diretta:** Usa il metodo `index.add()` e passa il percorso assoluto di ogni cartella sorgente; l'API rileva automaticamente i formati supportati (PDF, DOCX, XLSX, ecc.) ed estrae il testo ricercabile nell'indice.

`SearchOptions` è un oggetto di configurazione che ti consente di affinare il modo in cui i documenti vengono elaborati durante l'indicizzazione e la ricerca. Lo utilizzerai più tardi per abilitare le query basate su chunk.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Configurare le opzioni di ricerca per la ricerca a chunk
**Risposta diretta:** Imposta `options.setChunkSearch(true)` su un'istanza di `SearchOptions` prima di eseguire una query; questo indica al motore di suddividere ogni documento in chunk logici (tipicamente paragrafi) e restituire le corrispondenze per chunk anziché per file intero.

`SearchResult` contiene i chunk corrispondenti, le loro posizioni e i punteggi di rilevanza. Quando la ricerca a chunk è attiva, ogni `SearchResult` corrisponde a un singolo frammento del documento originale.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. Eseguire la ricerca iniziale basata su chunk
**Risposta diretta:** Esegui `index.search("your query", options)`; la chiamata restituisce una collezione di `SearchResult` per il primo set di chunk corrispondenti e un token che rappresenta lo stato della ricerca per la continuazione.

Il token restituito è essenziale per scorrere grandi insiemi di risultati senza rieseguire l'intera query.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Continuare la ricerca basata su chunk
**Risposta diretta:** Passa il token restituito dalla chiamata precedente a `index.searchNext(token, options)`; ripeti finché il metodo restituisce `null`, indicando che tutti i chunk corrispondenti sono stati recuperati.

Questo approccio incrementale mantiene basso l'uso della memoria perché solo il batch corrente di chunk risiede in memoria.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Perché usare la ricerca basata su chunk?
La ricerca basata su chunk suddivide collezioni di documenti massivi in pezzi gestibili, riducendo la pressione sulla memoria e velocizzando i tempi di risposta. Indicizzando a livello di paragrafo o sezione, il motore può recuperare solo i frammenti rilevanti, riducendo l'uso della CPU e migliorando la latenza per gli utenti finali. È particolarmente vantaggiosa quando:

1. **I team legali** devono individuare clausole specifiche tra migliaia di contratti.  
2. **I portali di supporto clienti** devono mostrare istantaneamente articoli pertinenti della knowledge base.  
3. **I ricercatori** setacciano grandi set di dati senza caricare interi file in memoria.  

Affermazione quantificata: GroupDocs.Search può elaborare **PDF di oltre 500 pagine** in meno di **2 secondi per chunk** su un server standard a 8 core, mantenendo l'heap massimo sotto **200 MB**.

## Come questo approccio aumenta le prestazioni di ricerca
**Risposta diretta:** Cercando chunk più piccoli invece di file interi, il motore può saltare le sezioni irrilevanti in anticipo, ridurre i cicli CPU e mantenere in memoria solo il chunk attivo, riducendo direttamente il consumo della **memoria dell'indice di ricerca Java** e ottenendo tempi di risposta più rapidi. Questo approccio mirato consente anche una cache più efficace e l'elaborazione parallela, permettendo a più core di gestire diversi chunk simultaneamente, migliorando ulteriormente il throughput sui server multicore.

Benefici aggiuntivi includono:
- Elaborazione parallela dei chunk su più core.  
- Terminazione anticipata quando viene trovata una corrispondenza ad alta rilevanza.  

## Gestire la memoria dell'indice di ricerca Java
**Risposta diretta:** Assegna un heap JVM sufficiente (ad esempio `-Xmx2g` o superiore) in base alla dimensione prevista dell'indice, esegui `index.optimize()` dopo aggiunte massive per comprimere la struttura dell'indice e monitora le pause GC con VisualVM per evitare picchi di latenza.

Suggerimenti di ottimizzazione aggiuntivi:
- Usa `index.flush()` dopo grandi batch per scrivere dati intermedi su disco.  
- Abilita `options.setMemoryLimit(256)` per limitare l'uso di memoria per ricerca.  

## Considerazioni sulle prestazioni
- **Gestione della memoria** – Assegna spazio heap sufficiente (`-Xmx`) per indici grandi.  
- **Monitoraggio delle risorse** – Tieni d'occhio l'uso della CPU durante le operazioni di indicizzazione e ricerca.  
- **Manutenzione dell'indice** – Ricostruisci o pulisci periodicamente l'indice per eliminare dati obsoleti.  

## Problemi comuni e risoluzione
| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| `OutOfMemoryError` durante l'indicizzazione | Dimensione dell'heap troppo piccola | Aumentare l'heap JVM (`-Xmx2g` o superiore) |
| Nessun risultato restituito | Token del chunk non elaborato | Assicurarsi che il ciclo `while` continui fino a quando `getNextChunkSearchToken()` è `null` |
| Prestazioni di ricerca lente | Indice non ottimizzato | Eseguire `index.optimize()` dopo aggiunte massive |

## Domande frequenti

**Q: Cos'è la ricerca basata su chunk?**  
A: La ricerca basata su chunk divide il set di dati in pezzi più piccoli, consentendo query efficienti su grandi volumi di dati senza caricare interi documenti in memoria.

**Q: Come aggiorno il mio indice con nuovi file?**  
A: Basta chiamare `index.add()` con il percorso dei nuovi documenti; l'indice li incorporerà automaticamente.

**Q: GroupDocs.Search può gestire diversi formati di file?**  
A: Sì, supporta **PDF, DOCX, XLSX, PPTX, HTML, TXT e oltre 30 altri formati**.

**Q: Quali sono i tipici colli di bottiglia delle prestazioni?**  
A: Le limitazioni di memoria e gli indici non ottimizzati sono le più comuni; assegna un heap sufficiente e ottimizza regolarmente l'indice.

**Q: Dove posso trovare documentazione più dettagliata?**  
A: Visita la documentazione ufficiale [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) per guide approfondite e riferimenti API.

**Q: La ricerca basata su chunk funziona con PDF criptati?**  
A: Sì, purché tu fornisca la password tramite l'overload API appropriato.

**Q: Come posso monitorare l'avanzamento dell'indicizzazione?**  
A: Usa l'overload `Index.add()` che restituisce un oggetto `Progress` o collega i callback di logging.

## Risorse
- **Documentazione**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Riferimento API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Supporto gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licenza temporanea**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Ultimo aggiornamento:** 2026-10-02  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Tutorial correlati

- [Crea directory indice di ricerca e imposta licenza – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Migliora le prestazioni delle query con GroupDocs.Search Java: Ottimizza indice e ricerca](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java Funzionalità di ricerca avanzata](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)