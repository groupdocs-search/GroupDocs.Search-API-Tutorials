---
date: '2026-08-26'
description: Scopri come i boolean operators Java ti consentono di creare un fast
  search index, eseguire content search Java e avviare faceted queries con GroupDocs.Search.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: Scopri come i boolean operators Java ti consentono di costruire un
  fast search index, eseguire content search Java e avviare faceted queries con GroupDocs.Search.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – costruisci un search index e una faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – crea un search index & faceted search
type: docs
url: /it/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Operatori booleani Java – creare indice di ricerca e ricerca a faccette

Implementare un'esperienza di **ricerca** potente in Java può sembrare opprimente, soprattutto quando è necessario **creare un search index Java** che supporti **boolean operators Java** per ricerche a faccette e complesse. In questo tutorial vedremo come configurare **GroupDocs.Search for Java**, costruire un indice, aggiungere documenti e creare sia ricerche a faccette semplici sia query multi‑criterio sofisticate che utilizzano la logica booleana. Alla fine comprenderai come sfruttare le operazioni **content search Java**, **filename search Java** e persino **update index Java** per mantenere i dati aggiornati.

## Risposte rapide
- **Cos'è una ricerca a faccette?** Un modo per filtrare i risultati per categorie predefinite come tipo di file o data.  
- **Come creo un indice di ricerca Java?** Inizializza un oggetto `Index` che punta a una cartella e aggiungi i documenti.  
- **Posso combinare più criteri con operatori booleani?** Sì—usa query basate su oggetti o operatori Boolean nei query di testo.  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per lo sviluppo; una licenza commerciale rimuove i limiti.  
- **Quale IDE funziona meglio?** Qualsiasi IDE Java (IntelliJ IDEA, Eclipse, NetBeans) va bene.

## Cos'è “create search index java”?
Creare un search index Java significa costruire una struttura basata su disco che memorizza il testo dei documenti e i metadati, consentendo il recupero istantaneo dei documenti corrispondenti tramite query. L'indice mappa i termini agli identificatori dei documenti, supporta ricerche rapide e può essere aggiornato in modo incrementale man mano che i file cambiano, fornendo la base per funzionalità di ricerca potenti.

## Perché usare GroupDocs.Search per query a faccette e complesse?
GroupDocs.Search for Java fornisce faceting integrato, supporto per query Boolean e indicizzazione ad alte prestazioni in grado di gestire fino a 10 milioni di documenti mantenendo la latenza delle query sotto i 200 ms su hardware server tipico. Offre filtri di campo pronti all'uso, un linguaggio di query ricco e compatibilità pure‑Java, rendendolo ideale per scenari di ricerca su scala aziendale.

## Prerequisiti
- **JDK 8 o successivo** installato e configurato nel tuo IDE.  
- **Maven** (o Gradle) per la gestione delle dipendenze.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Familiarità di base con i concetti OOP di Java e la struttura di progetto Maven.

## Configurazione di GroupDocs.Search per Java

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
In alternativa, scarica l'ultimo JAR dalla pagina di rilascio ufficiale:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Acquisizione della licenza
Per sbloccare tutte le funzionalità:

1. **Free trial** – perfetto per sviluppo e test.  
2. **Temporary evaluation license** – estende i limiti della prova.  
3. **Commercial license** – rimuove tutte le restrizioni per l'uso in produzione.

### Inizializzazione e configurazione di base
La classe `Index` è il componente principale che rappresenta un indice ricercabile memorizzato su disco. Il frammento seguente mostra come **creare un search index Java** istanziando la classe `Index`:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

Con l'indice pronto, possiamo passare a query a faccette e complesse nel mondo reale.

## Come usare boolean operators java – Ricerca a faccette semplice

Carica il tuo indice, aggiungi documenti ed esegui una query di campo; il modello a due passaggi ti consente di recuperare i conteggi delle faccette e i risultati filtrati in una singola chiamata. Questo approccio offre agli utenti un modo intuitivo per restringere i risultati per categorie come tipo di file, autore o metadati personalizzati.

### Passo 1: Creare un indice
Per prima cosa, punta il `Index` a una cartella dove verranno memorizzati i file dell'indice.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Passo 2: Aggiungere documenti all'indice
Indica a GroupDocs.Search dove si trovano i tuoi documenti sorgente. Tutti i tipi di file supportati (PDF, DOCX, TXT, ecc.) saranno indicizzati automaticamente.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Passo 3: Eseguire una ricerca nel campo content con una query di testo
Una rapida query di testo filtra per il campo `content`. La sintassi `content: Pellentesque` limita i risultati ai documenti che contengono la parola *Pellentesque* nel loro testo.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Passo 4: Eseguire una ricerca usando una query oggetto
Le query basate su oggetti ti danno un controllo fine. Qui costruiamo una query di parola, la avvolgiamo in una query di campo e la eseguiamo.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Come usare boolean operators java – Ricerca con query complessa

Per eseguire una query complessa, combina più condizioni di campo con operatori AND/OR/NOT e, facoltativamente, includi ricerche di frasi. Puoi specificare ogni condizione usando query di campo, annidarle con operatori Boolean e controllare la rilevanza con il boosting, consentendoti di recuperare solo i documenti più pertinenti che soddisfano tutti i criteri richiesti.

### Passo 1: Creare un indice per query complesse
Riutilizza la stessa struttura di cartelle; puoi condividere l'indice sia per scenari semplici che complessi.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Passo 2: Eseguire una ricerca con una query di testo
La query seguente cerca file chiamati *lorem* **e** *ipsum* **o** contenuto che contiene una delle due frasi esatte.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Passo 3: Eseguire una ricerca con una query oggetto
La costruzione basata su oggetti rispecchia la query testuale ma offre sicurezza di tipo e assistenza IDE.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Applicazioni pratiche di ricerche a faccette e complesse

| Scenario | Come aiuta il faceting | Query di esempio |
|----------|------------------------|-------------------|
| **Catalogo e‑commerce** | Filtra per categoria, prezzo, marca | `category: Electronics AND price:[100 TO 500]` |
| **Repository di documenti legali** | Restringi per numero di caso, giurisdizione | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Archivi di ricerca** | Combina autore, anno di pubblicazione, parole chiave | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Intranet aziendale** | Cerca per tipo di file e dipartimento | `filetype: pdf AND department: HR` |

## Problemi comuni e risoluzione
L'oggetto `SearchResult` contiene i documenti che corrispondono a una query e fornisce l'accesso ai loro punteggi di rilevanza e ai frammenti evidenziati.  
La classe `CommonFieldNames` definisce i nomi di campo standard come `Content` e `FileName` usati in tutta l'API.

- **Risultati vuoti** – Verifica che i documenti siano stati aggiunti correttamente (`index.getDocumentCount()` può aiutare).  
- **Indice obsoleto** – Dopo aver aggiunto o rimosso file, chiama `index.update()` per **update index java** e mantenere l'indice sincronizzato.  
- **Nomi di campo errati** – Usa le costanti `CommonFieldNames` (`Content`, `FileName`, ecc.) per evitare errori di battitura.  
- **Collo di bottiglia delle prestazioni** – Per collezioni enormi, considera l'abilitazione di `index.setCacheSize()` o l'uso di un SSD dedicato per la cartella dell'indice.  
- **Evidenziazioni mancanti** – Per **highlight search results java**, recupera i frammenti corrispondenti tramite `SearchResult.getFragments()` (non mostrato qui ma disponibile nell'API).  

## Domande frequenti
**D: Posso usare GroupDocs.Search con Spring Boot?**  
R: Assolutamente. Aggiungi la dipendenza Maven, configura l'indice come bean Spring e iniettalo ovunque ti servano capacità di ricerca.

**D: La libreria supporta campi di metadati personalizzati?**  
R: Sì – puoi aggiungere campi definiti dall'utente durante l'indicizzazione e poi effettuare faceting su di essi.

**D: Quanto può crescere l'indice?**  
R: L'indice basato su disco può gestire fino a 10 milioni di documenti; basta assicurarsi di avere spazio di archiviazione sufficiente e monitorare le impostazioni della cache.

**D: Esiste un modo per ordinare i risultati per rilevanza?**  
R: GroupDocs.Search assegna automaticamente un punteggio alle corrispondenze; puoi recuperare il punteggio tramite `SearchResult.getDocument(i).getScore()`.

**D: Cosa succede se indicizzo PDF criptati?**  
R: Fornisci la password quando aggiungi il documento: `index.add(filePath, password)`.

## Conclusione
A questo punto dovresti sentirti a tuo agio nel **creare un search index Java** con GroupDocs.Search, aggiungere documenti e creare sia query a faccette semplici sia ricerche Boolean sofisticate usando **boolean operators java**. Queste capacità ti permettono di offrire esperienze di ricerca rapide, accurate e user‑friendly in una vasta gamma di applicazioni—dalle piattaforme e‑commerce alle basi di conoscenza aziendali.

Pronto per il passo successivo? Esplora le funzionalità avanzate di **GroupDocs.Search** come **highlighting**, **suggestions** e **real‑time indexing** per potenziare ulteriormente la ricerca nella tua applicazione.

---

**Ultimo aggiornamento:** 2026-08-26  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs

## Tutorial correlati
- [Ricerca wildcard Java con GroupDocs.Search – Funzionalità avanzate](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Come aggiornare l'indice Java con GroupDocs.Search – Guida completa](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Come implementare la ricerca full text java: creare directory indice con GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)