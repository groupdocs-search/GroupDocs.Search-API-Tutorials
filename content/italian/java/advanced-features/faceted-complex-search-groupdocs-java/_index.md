---
date: '2025-12-16'
description: Impara a creare un indice di ricerca Java e a implementare ricerche faccettate
  e complesse usando GroupDocs.Search, migliorando le prestazioni di ricerca e l'esperienza
  dell'utente.
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: Crea indice di ricerca Java – Ricerche faccettate e complesse
type: docs
url: /it/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Crea un indice di ricerca Java – Ricerche a faccette e complesse

Implementare un'esperienza di **ricerca** potente in Java può sembrare opprimente, soprattutto quando è necessario **creare un indice di ricerca Java** per progetti che gestiscono grandi collezioni di documenti. Fortunatamente, **GroupDocs.Search for Java** offre un'API ricca che consente di costruire query a faccette e complesse con poche righe di codice. In questo tutorial scoprirai come configurare la libreria, **creare un indice di ricerca Java**, aggiungere documenti e eseguire sia ricerche faccettate semplici sia query sofisticate a più criteri.

## Risposte rapide
- **Che cos'è una ricerca a faccette?** Un modo per filtrare i risultati per categorie predefinite (ad es., tipo di file, data).  
- **Come creo un indice di ricerca Java?** Inizializza un oggetto `Index` che punta a una cartella e aggiungi i documenti.  
- **Posso combinare più criteri?** Sì—usa query basate su oggetti o operatori Booleani in una query di testo.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per lo sviluppo; una licenza commerciale rimuove i limiti.  
- **Quale IDE è il migliore?** Qualsiasi IDE Java (IntelliJ IDEA, Eclipse, NetBeans) funziona bene.

## Che cos'è “create search index java”?
Creare un indice di ricerca in Java significa costruire una struttura dati ricercabile che memorizza i metadati e il contenuto dei documenti, consentendo un recupero rapido basato sulle query degli utenti. Con GroupDocs.Search, l'indice risiede su disco, può essere aggiornato in modo incrementale e supporta funzionalità avanzate come le faccette e la logica Boolean complessa.

## Perché usare GroupDocs.Search per query a faccette e complesse?
- **Faceting pronta all'uso** – filtra per campi come nome file, dimensione o metadati personalizzati.  
- **Linguaggio di query ricco** – combina query di testo, frase e campo usando gli operatori AND/OR/NOT.  
- **Prestazioni scalabili** – indicizza milioni di documenti mantenendo bassa la latenza di ricerca.  
- **Pure Java** – nessuna dipendenza nativa, funziona su qualsiasi piattaforma che esegue JDK 8+.

## Prerequisiti

Prima di iniziare, assicurati di avere quanto segue:

- **JDK 8 o superiore** installato e configurato nel tuo IDE.  
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
In alternativa, scarica l'ultimo JAR dalla pagina ufficiale di rilascio:  
[Rilasci di GroupDocs.Search per Java](https://releases.groupdocs.com/search/java/)

### Acquisizione della licenza
Per sbloccare tutte le funzionalità:

1. **Prova gratuita** – perfetta per sviluppo e test.  
2. **Licenza di valutazione temporanea** – estende i limiti della prova.  
3. **Licenza commerciale** – rimuove tutte le restrizioni per l'uso in produzione.

### Inizializzazione e configurazione di base
Il frammento seguente mostra come **creare un indice di ricerca Java** istanziando la classe `Index`:

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

Con l'indice pronto, possiamo passare a query faccettate e complesse nel mondo reale.

## Come creare un indice di ricerca Java – Ricerca faccettata semplice

La ricerca a faccette consente agli utenti finali di restringere i risultati selezionando valori da categorie predefinite (faccette). Di seguito una guida passo‑passo.

### Passo 1: Crea un indice
Per prima cosa, punta il `Index` a una cartella dove verranno memorizzati i file dell'indice.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Passo 2: Aggiungi documenti all'indice
Indica a GroupDocs.Search dove si trovano i tuoi documenti sorgente. Tutti i tipi di file supportati (PDF, DOCX, TXT, ecc.) saranno indicizzati automaticamente.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Passo 3: Esegui una ricerca nel campo Content con una query di testo
Una rapida query di testo filtra per il campo `content`. La sintassi `content: Pellentesque` limita i risultati ai documenti che contengono la parola *Pellentesque* nel loro testo.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Passo 4: Esegui una ricerca usando una query oggetto
Le query basate su oggetti offrono un controllo granulare. Qui costruiamo una query di parola, la avvolgiamo in una query di campo e la eseguiamo.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Come creare un indice di ricerca Java – Ricerca con query complesse

Le query complesse combinano più campi, operatori Booleani e ricerche di frasi. Questo è ideale per scenari come filtri e‑commerce o ricerca di documenti legali.

### Passo 1: Crea un indice per query complesse
Riutilizza la stessa struttura di cartelle; puoi condividere l'indice sia per scenari semplici che complessi.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Passo 2: Esegui una ricerca con una query di testo
La query seguente cerca file chiamati *lorem* **e** *ipsum* **o** contenuti che contengono una delle due frasi esatte.

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

### Passo 3: Esegui una ricerca con una query oggetto
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

| Scenario | Come aiuta la faccettatura | Query di esempio |
|----------|----------------------------|------------------|
| **Catalogo e‑commerce** | Filtra per categoria, prezzo, marca | `category: Electronics AND price:[100 TO 500]` |
| **Repository di documenti legali** | Restringi per numero di caso, giurisdizione | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Archivi di ricerca** | Combina autore, anno di pubblicazione, parole chiave | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Intranet aziendale** | Cerca per tipo di file e dipartimento | `filetype: pdf AND department: HR` |

## Problemi comuni e risoluzione

- **Risultati vuoti** – Verifica che i documenti siano stati aggiunti correttamente (`index.getDocumentCount()` può aiutare).  
- **Indice obsoleto** – Dopo aver aggiunto o rimosso file, chiama `index.update()` per mantenere l'indice sincronizzato.  
- **Nomi di campo errati** – Usa le costanti `CommonFieldNames` (`Content`, `FileName`, ecc.) per evitare errori di battitura.  
- **Collo di bottiglia delle prestazioni** – Per collezioni enormi, considera l'abilitazione di `index.setCacheSize()` o l'uso di un SSD dedicato per la cartella dell'indice.  

## Domande frequenti

**Q: Posso usare GroupDocs.Search con Spring Boot?**  
**A: Assolutamente. Basta aggiungere la dipendenza Maven, configurare l'indice come bean Spring e iniettarlo dove necessario.**

**Q: La libreria supporta campi di metadati personalizzati?**  
**A: Sì – è possibile aggiungere campi definiti dall'utente durante l'indicizzazione e poi usarli per le faccette.**

**Q: Quanto può crescere l'indice?**  
**A: L'indice è basato su disco e può gestire milioni di documenti; basta garantire spazio di archiviazione sufficiente e monitorare le impostazioni della cache.**

**Q: Esiste un modo per ordinare i risultati per rilevanza?**  
**A: GroupDocs.Search assegna automaticamente un punteggio alle corrispondenze; è possibile recuperare il punteggio tramite `SearchResult.getDocument(i).getScore()`.**

**Q: Cosa succede se indicizzo PDF criptati?**  
**A: Fornisci la password quando aggiungi il documento: `index.add(filePath, password)`.**

## Conclusione

A questo punto dovresti sentirti a tuo agio nel **creare un indice di ricerca Java** con GroupDocs.Search, aggiungere documenti e costruire sia query faccettate semplici sia ricerche Boolean sofisticate. Queste capacità ti consentono di offrire esperienze di ricerca rapide, accurate e user‑friendly in una vasta gamma di applicazioni, dalle piattaforme e‑commerce alle basi di conoscenza aziendali.

Pronto per il passo successivo? Esplora le funzionalità avanzate di **GroupDocs.Search**, come **highlighting**, **suggestions** e **real‑time indexing**, per potenziare ulteriormente la capacità di ricerca della tua applicazione.

---

**Ultimo aggiornamento:** 2025-12-16  
**Testato con:** GroupDocs.Search 25.4 per Java  
**Autore:** GroupDocs