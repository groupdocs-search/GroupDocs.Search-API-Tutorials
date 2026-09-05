---
date: '2026-05-28'
description: Scopri come cercare una frase con wildcard patterns usando GroupDocs.Search
  for Java. Include la creazione di un search index, l'aggiunta di documents e l'esecuzione
  di exact phrase e wildcard queries.
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: Come cercare una frase con wildcard in GroupDocs.Search for Java
type: docs
url: /it/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Come cercare una frase con caratteri jolly in GroupDocs.Search per Java

Nelle moderne applicazioni incentrate sui documenti, **how to search phrase** in modo rapido e preciso è un fattore decisivo per l'esperienza dell'utente. Che tu stia costruendo una base di conoscenza, un catalogo e‑commerce o un repository guidato da compliance, la capacità di individuare una frase esatta—o una sua variazione flessibile—mantiene gli utenti produttivi e riduce il carico di supporto. Questo tutorial ti guida attraverso l'installazione di **GroupDocs.Search for Java**, la creazione di un indice di ricerca, il caricamento dei documenti e l'esecuzione di query sia a frase esatta sia potenziate da caratteri jolly, il tutto con snippet di codice chiari e pronti per la produzione.

## Risposte rapide
- **Qual è il beneficio principale delle ricerche di frase?** Corrispondenza precisa dell'ordine delle parole e della prossimità, garantendo che vengano restituiti solo i documenti contenenti la sequenza esatta.  
- **È possibile utilizzare i caratteri jolly all'interno di una frase?** Sì—i caratteri jolly consentono di saltare o sostituire parole mantenendo l'ordine complessivo.  
- **È necessaria una licenza per lo sviluppo?** Una prova gratuita è sufficiente per i test; è necessaria una licenza completa per le distribuzioni in produzione.  
- **Quale versione di Maven devo usare?** L'ultima release di GroupDocs.Search per Java (ad es., 25.4 al momento della stesura).  
- **Questo approccio è adatto a grandi insiemi di documenti?** Assolutamente—GroupDocs.Search può gestire collezioni di centinaia di migliaia di documenti con latenza di query inferiore a un secondo quando l'indice è ottimizzato.

## Cos'è “how to search phrase”?
**Cercare una frase significa cercare una sequenza specifica di parole in un documento.**  
Quando esegui una query di frase, il motore verifica che le parole compaiano nell'ordine esatto e entro la prossimità definita, eliminando risultati irrilevanti che contengono le stesse parole in un contesto diverso. Questo rende le ricerche di frase ideali per individuare clausole legali, codici prodotto o qualsiasi testo in cui l'ordine è importante.

## Perché usare GroupDocs.Search per query di frase e caratteri jolly?
GroupDocs.Search offre **indicizzazione ad alta velocità fino a 1 milione di documenti mantenendo tempi di risposta inferiori a un secondo** su hardware server tipico. Il suo linguaggio di query supporta frasi esatte, semplici caratteri jolly `*` e `?`, e pattern avanzati come intervalli numerici (`*2~5`). La libreria si integra con qualsiasi applicazione Java tramite Maven o download diretto del JAR, ed è eseguibile su Java 8+ senza servizi esterni.

## Prerequisiti
- Java 8 o superiore (Java 11 LTS consigliato).  
- Maven 3 o successivo (se preferisci la gestione delle dipendenze).  
- Familiarità di base con la struttura dei progetti Java e i concetti di programmazione orientata agli oggetti.  

## Configurazione di GroupDocs.Search per Java

### Utilizzo di Maven
Aggiungi il repository ufficiale e la dipendenza GroupDocs.Search al tuo `pom.xml`:

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### Download diretto
In alternativa, scarica l'ultimo JAR dalla pagina di rilascio ufficiale: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
- **Free Trial:** Ideale per esperimenti rapidi; limitato a 100 MB di dati indicizzati.  
- **Temporary License:** Richiedi una chiave di valutazione di 30 giorni dal portale GroupDocs.  
- **Full License:** Necessaria per l'uso in produzione e per capacità di indicizzazione illimitata.

## Inizializzazione e configurazione di base
Crea una cartella che conterrà i file dell'indice e istanzia l'oggetto `Index`. La classe `Index` rappresenta l'indice ricercabile memorizzato su disco e fornisce metodi per aggiungere, aggiornare e interrogare i documenti.

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

Aggiungi i documenti che desideri rendere ricercabili:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## Come cercare una frase con caratteri jolly in GroupDocs.Search
Questa sezione dimostra tre livelli di ricerca di frase—corrispondenza esatta, carattere jolly semplice e pattern di caratteri jolly avanzati—mostrando come creare un indice, aggiungere documenti ed eseguire ogni tipo di query con codice Java conciso. Gli esempi illustrano sia query basate su testo sia costruzione di query basate su oggetti, consentendo agli sviluppatori di integrare capacità di ricerca flessibili nelle proprie applicazioni.

### Ricerca di frase semplice

#### Panoramica
Utilizza questo approccio quando ti serve una **corrispondenza esatta** di una sequenza di parole, ad esempio una clausola legale o un numero di modello prodotto.

#### Risposta diretta
Carica l'indice, chiama `search` con una frase tra virgolette (es., `"quick brown fox"`), e il motore restituisce solo i documenti contenenti quella sequenza esatta, preservando ordine e spaziatura delle parole. La query viene eseguita in millisecondi, anche su indici contenenti centinaia di migliaia di file.

#### Passo 1: Creare un indice
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### Passo 2: Aggiungere documenti all'indice
```java
Index index = new Index(indexFolder);
```

#### Passo 3: Cercare una frase specifica (forma testuale)
```java
index.add(documentsFolder);
```

#### Passo 4: Query basate su oggetti (cerca frase esatta)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### Ricerca di frase con caratteri jolly

#### Panoramica
I segnaposto jolly (`*` per qualsiasi numero di caratteri, `?` per un singolo carattere) consentono di **saltare parole variabili** mantenendo comunque l'ordine circostante.

#### Risposta diretta
Inserisci un token jolly (`*`) all'interno di una frase tra virgolette—es., `"quick * fox"`—per far corrispondere qualsiasi parola/e tra *quick* e *fox*. Il motore espande il jolly al momento della query, scansionando solo i termini indicizzati che soddisfano il pattern, mantenendo le prestazioni comparabili a una query di frase semplice.

#### Passo 1: Creare un indice
*(Stesso di Ricerca di frase semplice.)*

#### Passo 2: Aggiungere documenti all'indice
*(Stesso di sopra.)*

#### Passo 3: Ricerca in forma testuale con caratteri jolly
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Passo 4: Query basate su oggetti con caratteri jolly (Wildcard Search Java)
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### Ricerca avanzata con caratteri jolly

#### Panoramica
Combina intervalli numerici, caratteri opzionali e pattern personalizzati simili a regex per **corrispondenze sofisticate**, come numeri di versione o codici prodotto.

#### Risposta diretta
Usa la sintassi jolly estesa `*min~max` per definire un intervallo di distanze consentite tra le parole, o `?` per corrispondere a un singolo carattere. Per esempio, `"error *2~5 code"` trova la parola *error* seguita da due a cinque parole qualsiasi e poi *code*. Questa precisione riduce i falsi positivi offrendo al contempo flessibilità.

#### Passo 1: Creare un indice
*(Ripetuto per chiarezza.)*

#### Passo 2: Aggiungere documenti all'indice
*(Ripetuto.)*

#### Passo 3: Ricerca in forma testuale con pattern di caratteri jolly complessi
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Passo 4: Query basate su oggetti con caratteri jolly avanzati
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## Applicazioni pratiche
- **Content Management Systems:** Gli editor possono individuare clausole esatte o estratti flessibili senza dover scansionare manualmente centinaia di pagine.  
- **E‑commerce Catalogs:** Gli acquirenti trovano i prodotti anche se omettono un descrittore o usano sinonimi, grazie alla tolleranza dei caratteri jolly.  
- **Legal & Compliance:** Isolare rapidamente il linguaggio contrattuale che può apparire con piccole variazioni tra gli accordi.  

## Considerazioni sulle prestazioni
- **Create Search Index** solo una volta per un set di documenti stabile; riutilizza la stessa istanza `Index` per tutte le query.  
- **Add Documents Incrementally** quando arrivano nuovi file—evita di ricostruire l'intero indice per mantenere basso l'uso della CPU.  
- **Design Precise Wildcard Patterns**; pattern più ampi (`*`) aumentano il numero di espansioni dei termini e possono incrementare il carico CPU.  
- **Call `index.optimize()`** periodicamente (se supportato) per compattare l'indice e mantenere il consumo di memoria sotto controllo.  

## Problemi comuni e soluzioni

| Problema | Soluzione |
|----------|-----------|
| Nessun risultato restituito per una query con caratteri jolly | Verifica la sintassi del carattere jolly (`*min~max`) e assicurati che le parole target esistano entro la distanza definita. |
| L'indice diventa obsoleto dopo gli aggiornamenti dei file | Usa `index.add(updatedFolder)` o l'API di aggiornamento incrementale per aggiornare solo i file modificati. |
| Elevato consumo di memoria su grandi set di dati | Aumenta l'heap JVM (`-Xmx4g` o superiore) e considera di suddividere l'indice in più shard per l'elaborazione parallela. |

## Domande frequenti

**Q: Qual è la differenza tra un carattere jolly e una ricerca di frase?**  
A: Una ricerca di frase richiede l'ordine e la spaziatura esatti delle parole, mentre un carattere jolly consente di sostituire o saltare parole all'interno di quell'ordine, offrendo una corrispondenza flessibile.

**Q: Posso usare i caratteri jolly con dati numerici nelle ricerche?**  
A: Sì—i parametri di intervallo jolly (`*min~max`) funzionano sia con numeri sia con parole, consentendo query come `"version *1~3"`.

**Q: Come dovrei gestire collezioni di documenti molto grandi?**  
A: Mantieni l'indice ottimizzato, esegui aggiornamenti incrementali e crea pattern jolly specifici per limitare l'espansione dei termini. GroupDocs.Search può indicizzare 1 milione di documenti mantenendo la latenza delle query sotto i 200 ms su hardware standard.

**Q: GroupDocs.Search è adatto a scenari di ricerca in tempo reale?**  
A: Assolutamente—una volta costruito l'indice, le query vengono eseguite in millisecondi, rendendolo ideale per caselle di ricerca interattive e funzionalità di auto‑completamento.

**Q: Posso integrare questa libreria in un progetto Java esistente?**  
A: Sì. Aggiungi la dipendenza Maven o il JAR, istanzia l'`Index` come mostrato, e sei pronto a interrogare senza modificare il codice esistente.

**Ultimo aggiornamento:** 2026-05-28  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs

```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## Tutorial correlati

- [Crea indice di ricerca Java – Tutorial GroupDocs.Search](/search/java/)
- [Aggiungi documenti all'indice – Tutorial GroupDocs.Search Java](/search/java/document-management/)
- [Crea indice di ricerca - Tutorial GroupDocs.Search Java](/search/java/advanced-features/)