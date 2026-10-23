---
date: '2026-10-17'
description: Scopri come usare i synonyms in Java con GroupDocs.Search, importa i
  synonym dictionaries, gestisci i synonym groups e ottimizza il tuo search index
  per una migliore rilevanza.
keywords:
- how to use synonyms
- add synonym support
- manage synonym groups
- import synonym dictionary
- optimize search index
lastmod: '2026-10-17'
og_description: Scopri come usare i synonyms in Java con GroupDocs.Search, importa
  i synonym dictionaries, gestisci i synonym groups e ottimizza il tuo search index
  per una migliore rilevanza.
og_image_alt: Developer guide showing synonym dictionary integration in GroupDocs.Search
  for Java
og_title: Come usare i synonyms in Java con GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-10-17'
  description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  headline: How to use synonyms in Java with GroupDocs.Search
  type: TechArticle
- description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  name: How to use synonyms in Java with GroupDocs.Search
  steps:
  - name: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
    text: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
  - name: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
    text: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
  - name: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
    text: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
  type: HowTo
- questions:
  - answer: Any modern OS with a compatible JDK (Java 8 or newer) is sufficient.
    question: What is the minimum system requirement for using GroupDocs.Search?
  - answer: Update it whenever new terminology emerges—use `clear()` followed by `addRange()`
      for a clean refresh.
    question: How often should I refresh my synonym dictionary?
  - answer: A free trial works for evaluation, but a license is required for production
      deployments.
    question: Can I run GroupDocs.Search without purchasing a license?
  - answer: Split data into logical batches, monitor heap usage, and schedule regular
      index maintenance.
    question: What are best practices for indexing large data sets?
  - answer: Verify that the dictionary is correctly imported, that `setUseSynonymSearch(true)`
      is active, and that the terms are present in the synonym groups.
    question: I’m not seeing expected synonym matches—what should I check?
  type: FAQPage
tags:
- synonym search
- GroupDocs.Search
- Java search indexing
- document retrieval
title: Come usare i synonyms in Java con GroupDocs.Search
type: docs
url: /it/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

# Come utilizzare i sinonimi in Java con GroupDocs.Search

Se desideri che i tuoi utenti trovino il contenuto giusto anche quando digitano parole diverse, **la ricerca con sinonimi** è la risposta. In questa guida imparerai a creare un dizionario di sinonimi, importarlo o esportarlo, gestire i gruppi di sinonimi e eseguire una ricerca che espande automaticamente le query usando quei sinonimi. Che tu stia costruendo un CMS, un catalogo e‑commerce o un repository di documenti legali, aggiungere il supporto ai sinonimi può aumentare notevolmente la pertinenza e i tassi di conversione.

## Risposte rapide
- **Qual è il primo passo per aggiungere sinonimi?** Crea un'istanza `Index` e lavora con l'API `SynonymDictionary`.  
- **Posso importare un dizionario di sinonimi già pronto?** Sì – chiama `importDictionary(path)` indicando la posizione del file.  
- **Come attivo la ricerca consapevole dei sinonimi?** Abilita `SearchOptions.setUseSynonymSearch(true)`.  
- **È possibile modificare i gruppi di sinonimi a runtime?** Assolutamente – puoi cancellare, aggiungere o recuperare gruppi tramite l'API del dizionario.  
- **Cosa devo monitorare quando scala l'indice?** Pulisci regolarmente le voci inutilizzate e regola l'heap JVM per file di sinonimi di grandi dimensioni.

## Cos'è la ricerca con sinonimi?
**La ricerca con sinonimi** significa che il motore tratta un insieme di parole o frasi come intercambiabili. Quando un utente digita **“better”**, il motore cerca anche **“improve”**, **“enhance”** o qualsiasi altro termine definito nello stesso gruppo di sinonimi, fornendo risultati più ricchi senza modificare la query dell'utente.

## Perché abilitare il supporto ai sinonimi in GroupDocs.Search?
Abilitare il supporto ai sinonimi consente al motore di ampliare automaticamente le query includendo termini equivalenti, migliorando la pertinenza dei risultati, aumentando la soddisfazione degli utenti e potenzialmente incrementando i tassi di conversione per siti e‑commerce o basati su contenuti. Inoltre centralizza la gestione della terminologia, riducendo il carico di manutenzione su più applicazioni.

## Prerequisiti
- GroupDocs.Search per Java versione **25.4** o successiva.  
- Un IDE Java (IntelliJ IDEA, Eclipse, ecc.) con supporto Maven.  
- Conoscenze di base di Java e familiarità con la struttura di progetto Maven.

### Librerie richieste e versioni
- GroupDocs.Search per Java **25.4** o superiore.

### Configurazione dell'ambiente
- IDE a tua scelta (IntelliJ IDEA, Eclipse, ecc.).  
- Maven per la gestione delle dipendenze.

### Conoscenze richieste
- Programmazione orientata agli oggetti in Java.  
- Operazioni di I/O di base sui file.

## Configurare GroupDocs.Search per Java

### Informazioni sull'installazione
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

**Download diretto** – puoi anche scaricare l'ultimo JAR da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
- **Prova gratuita:** Testa le funzionalità principali senza licenza.  
- **Licenza temporanea:** Estendi le capacità della prova durante la valutazione.  
- **Acquisto:** Necessario per l'uso in produzione e per l'intero set di funzionalità.

#### Inizializzazione e configurazione di base
Crea un'istanza `Index`, quindi aggiungi i documenti da indicizzare:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Index";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Adding documents from a specific folder to the index
index.add(documentsFolder);
```

## Come aggiungere sinonimi al tuo indice di ricerca

### Funzionalità 1: creazione e indicizzazione di un indice
La classe `Index` rappresenta una collezione ricercabile di documenti memorizzati su disco o in memoria.  

```java
// Create an index in the specified folder
Index index = new Index(indexFolder);

// Add documents from the given folder to the index
index.add(documentsFolder);
```

### Funzionalità 2: recuperare sinonimi per una parola
`SynonymDictionary` gestisce i gruppi di sinonimi e fornisce metodi per interrogare i sinonimi di un termine.  

```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### Funzionalità 3: recuperare i gruppi di sinonimi
`SynonymDictionary.getGroups()` restituisce un elenco di tutti i gruppi di sinonimi definiti con i relativi identificatori.  

```java
String[][] synonymGroups = index.getDictionaries().getSynonymDictionary().getSynonymGroups("make");
```

### Funzionalità 4: gestire le voci del dizionario di sinonimi
`add(word, synonym)` inserisce una nuova relazione di sinonimo nel dizionario. `clear()` rimuove tutte le voci, e `remove(word)` elimina un termine specifico dal dizionario.  

```java
if (index.getDictionaries().getSynonymDictionary().getCount() > 0) {
    index.getDictionaries().getSynonymDictionary().clear();
}

String[][] newSynonymGroups = new String[][]{
    new String[] { "achieve", "accomplish", "attain", "reach" },
    new String[] { "accept", "take", "have" },
    new String[] { "improve", "better" }
};

index.getDictionaries().getSynonymDictionary().addRange(newSynonymGroups);
```

### Funzionalità 5: esportare i sinonimi in un file
`exportDictionary(path)` scrive il dizionario di sinonimi corrente in un file binario .dat nella posizione specificata.  

```java
String exportFilePath = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.getDictionaries().getSynonymDictionary().exportDictionary(exportFilePath);
```

### Funzionalità 6: importare i sinonimi da un file
`importDictionary(path)` carica un file .dat precedentemente esportato nel dizionario di sinonimi.  

```java
index.getDictionaries().getSynonymDictionary().importDictionary(exportFilePath);
```

### Funzionalità 7: eseguire la ricerca con supporto ai sinonimi
`SearchOptions` configura il comportamento della query, inclusa l'abilitazione dell'espansione dei sinonimi. `setUseSynonymSearch(true)` attiva la ricerca consapevole dei sinonimi per la query successiva.  

```java
String query = "better";
SearchOptions options = new SearchOptions();
options.setUseSynonymSearch(true);

SearchResult result = index.search(query, options);
```

## Come effettuare una ricerca con sinonimi
Carica il tuo `Index`, abilita la ricerca con sinonimi ed esegui una query. Il motore espande automaticamente la query usando il dizionario di sinonimi che hai creato o importato, restituendo corrispondenze per tutti i termini correlati.

## Come importare un dizionario di sinonimi
Se disponi già di un file `.dat` preparato in un altro ambiente, chiama semplicemente `importDictionary(path)`. È l'ideale per sincronizzare i dizionari tra server di sviluppo, staging e produzione.

## Come gestire i gruppi di sinonimi
I gruppi di sinonimi ti permettono di trattare un insieme di termini come un'unica entità logica. Aggiungere, cancellare o recuperare gruppi avviene tramite l'API `SynonymDictionary`, come mostrato negli snippet di codice sopra.

## Come ottimizzare l'indice di ricerca
- **Pulisci regolarmente le voci inutilizzate:** Usa `clear()` prima di aggiornamenti massivi.  
- **Regola l'heap JVM:** Dizionari di grandi dimensioni possono richiedere più memoria; aumenta il parametro `-Xmx` di conseguenza.  
- **Mantieni la libreria aggiornata:** Le nuove versioni contengono miglioramenti di performance e correzioni di bug.

## Applicazioni pratiche
1. **Sistemi di gestione dei contenuti (CMS):** Gli utenti trovano gli articoli anche quando usano terminologia alternativa.  
2. **Piattaforme e‑commerce:** Le ricerche di prodotto diventano tolleranti ai sinonimi, ad esempio “laptop” vs. “notebook”.  
3. **Repository di documenti:** Archivi legali o medici beneficiano di gruppi di sinonimi specifici del dominio, migliorando la scoperta per i professionisti.

## Considerazioni sulle prestazioni
- **Ottimizza lo storage dell'indice:** Ricostruisci periodicamente l'indice per rimuovere dati obsoleti.  
- **Gestisci l'uso della memoria:** Monitora il consumo di heap quando carichi file di sinonimi di grandi dimensioni; un dizionario da 500 MB tipicamente richiede un heap da 2 GB su una JVM a 64 bit.  
- **Aggiornamenti regolari:** Rimani sulla versione più recente di GroupDocs.Search per correzioni di bug e miglioramenti di velocità.

## Problemi comuni e soluzioni
| Problema | Probabile causa | Soluzione |
|----------|----------------|-----------|
| Nessuna corrispondenza di sinonimi | `setUseSynonymSearch(true)` non impostato o dizionario non importato | Verifica che l'opzione sia abilitata e che il file del dizionario esista. |
| Errori di out‑of‑memory durante l'importazione | File `.dat` molto grande supera l'heap JVM | Aumenta la dimensione dell'heap `-Xmx` o importa in batch più piccoli. |
| Voci duplicate nei risultati | Lo stesso termine appare in più gruppi di sinonimi | Consolidare i gruppi sovrapposti usando `clear()` poi `addRange()`. |

## Domande frequenti

**D: Qual è il requisito minimo di sistema per usare GroupDocs.Search?**  
R: Qualsiasi OS moderno con una JDK compatibile (Java 8 o superiore) è sufficiente.

**D: Quanto spesso devo aggiornare il mio dizionario di sinonimi?**  
R: Aggiornalo ogni volta che emergono nuovi termini – usa `clear()` seguito da `addRange()` per un refresh pulito.

**D: Posso usare GroupDocs.Search senza acquistare una licenza?**  
R: Una prova gratuita è valida per la valutazione, ma è necessaria una licenza per le distribuzioni in produzione.

**D: Quali sono le best practice per indicizzare grandi set di dati?**  
R: Suddividi i dati in batch logici, monitora l'uso dell'heap e programma una manutenzione regolare dell'indice.

**D: Non vedo le corrispondenze di sinonimi previste – cosa controllare?**  
R: Verifica che il dizionario sia stato importato correttamente, che `setUseSynonymSearch(true)` sia attivo e che i termini siano presenti nei gruppi di sinonimi.

**Risorse**  
- [Documentation](https://docs.groupdocs.com/search/java/)  
- [API Reference](https://reference.groupdocs.com/search/java)  
- [Download GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)  
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license/) 

---

**Ultimo aggiornamento:** 2026-10-17  
**Testato con:** GroupDocs.Search 25.4 per Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Create Manage Groupdocs Search Java Index](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Java Full Text Search Library – Optimize Index with GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Java Fuzzy Search: Add Documents to Index with GroupDocs.Search](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)
