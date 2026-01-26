---
date: '2026-01-26'
description: Scopri come cercare frasi usando i pattern wildcard in GroupDocs.Search
  per Java. Questa guida copre la creazione di un indice di ricerca, l'aggiunta di
  documenti all'indice e l'esecuzione di ricerche wildcard in Java.
keywords:
- GroupDocs.Search for Java
- phrase searches
- wildcard patterns
title: Come cercare una frase con caratteri jolly in GroupDocs.Search Java
type: docs
url: /it/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Come cercare una frase con caratteri jolly in GroupDocs.Search per Java

Nel mondo frenetico della gestione dei documenti di oggi, **come cercare una frase** in modo efficiente può fare la differenza nell'usabilità di un'applicazione. Che tu stia costruendo un sistema di gestione dei contenuti, un catalogo e‑commerce o un archivio di documenti legali, la capacità di individuare frasi esatte—o variazioni flessibili di esse—è fondamentale. In questo tutorial vedremo come impostare **GroupDocs.Search per Java**, creare un indice di ricerca, aggiungere documenti all'indice e padroneggiare sia le ricerche di frase semplici sia le potenti tecniche di ricerca con caratteri jolly in Java.

## Risposte rapide
- **Qual è il beneficio principale delle ricerche di frase?** Corrispondenza precisa dell'ordine delle parole e della prossimità.  
- **È possibile usare caratteri jolly all'interno di una frase?** Sì, puoi combinare caratteri jolly con parole esatte per una corrispondenza flessibile.  
- **Ho bisogno di una licenza per lo sviluppo?** Una prova gratuita è sufficiente per i test; è necessaria una licenza completa per la produzione.  
- **Quale versione di Maven dovrei usare?** L'ultima release di GroupDocs.Search per Java (ad es. 25.4 al momento della scrittura).  
- **Questo approccio è adatto a grandi insiemi di documenti?** Assolutamente—basta mantenere l'indice ottimizzato e usare pattern di caratteri jolly mirati.

## Cos'è “come cercare una frase”?
Cercare una frase significa cercare una sequenza specifica di parole in un documento. Quando aggiungi i caratteri jolly, permetti al motore di ricerca di saltare o sostituire parole, offrendoti la flessibilità di corrispondere a variazioni senza sacrificare la rilevanza.

## Perché usare GroupDocs.Search per query di frase e caratteri jolly?
- **Alte prestazioni** su collezioni di grandi dimensioni grazie a un indice invertito ottimizzato.  
- **Linguaggio di query ricco** che supporta frase esatta, caratteri jolly semplici e pattern avanzati.  
- **Facile integrazione** con qualsiasi applicazione Java tramite Maven o download diretto.  

## Prerequisiti
- Java 8 o versioni successive installate.  
- Maven 3 o successivo (se preferisci la gestione delle dipendenze con Maven).  
- Familiarità di base con la sintassi Java e la struttura del progetto.  

## Configurazione di GroupDocs.Search per Java

### Utilizzo di Maven
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
In alternativa, scarica l'ultimo JAR da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
- **Prova gratuita:** Ideale per esperimenti rapidi.  
- **Licenza temporanea:** Richiedila tramite il portale GroupDocs per test estesi.  
- **Acquisto completo:** Consigliato per le distribuzioni in produzione.

### Inizializzazione e configurazione di base
Crea una cartella per l'indice e inizializzala:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

Aggiungi i documenti che desideri rendere ricercabili:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

## Come cercare una frase con caratteri jolly in GroupDocs.Search
Di seguito analizziamo tre scenari progressivi: ricerca di frase esatta, uso semplice dei caratteri jolly e pattern avanzati di caratteri jolly.

### Ricerca di frase semplice

#### Panoramica
Usa questa modalità quando ti serve una corrispondenza esatta di una sequenza di parole.

##### Passo 1: Creare un indice
```java
Index index = new Index(indexFolder);
```

##### Passo 2: Aggiungere documenti all'indice
```java
index.add(documentsFolder);
```

##### Passo 3: Cercare una frase specifica (forma testuale)

```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Passo 4: Query basate su oggetti (Search Exact Phrase)

```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Ricerca di frase con caratteri jolly

#### Panoramica
I segnaposto jolly ti consentono di saltare un numero variabile di parole tra termini esatti.

##### Passo 1: Creare un indice
*(Stesso dei passi della Ricerca di frase semplice.)*

##### Passo 2: Aggiungere documenti all'indice
*(Stesso di sopra.)*

##### Passo 3: Ricerca in forma testuale con caratteri jolly

```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Passo 4: Query basate su oggetti con caratteri jolly (Wildcard Search Java)

```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Ricerca avanzata con caratteri jolly

#### Panoramica
Combina intervalli numerici, caratteri opzionali e pattern personalizzati per corrispondenze sofisticate.

##### Passo 1: Creare un indice
*(Ripetuto per chiarezza.)*

##### Passo 2: Aggiungere documenti all'indice
*(Ripetuto.)*

##### Passo 3: Ricerca in forma testuale con pattern di caratteri jolly complessi

```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

##### Passo 4: Query basate su oggetti con caratteri jolly avanzati

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

## Applicazioni pratiche
- **Sistemi di gestione dei contenuti:** Consentono agli editori di individuare clausole esatte o estratti flessibili.  
- **Cataloghi e‑commerce:** Permettono agli acquirenti di trovare prodotti anche se mancano parole o usano sinonimi.  
- **Legale e conformità:** Isolano rapidamente il linguaggio contrattuale che può apparire con lievi variazioni.

## Considerazioni sulle prestazioni
- **Crea l'indice di ricerca** una sola volta per l'insieme di documenti, poi riutilizzalo.  
- **Aggiungi documenti all'indice** in modo incrementale quando arrivano nuovi file—non ricostruire l'intero indice ogni volta.  
- Usa **pattern di caratteri jolly precisi** per evitare scansioni inutili; pattern più ampi aumentano il carico CPU.  
- Chiama periodicamente `index.optimize()` (se disponibile) per mantenere basso l'uso di memoria.

## Problemi comuni e soluzioni
| Problema | Soluzione |
|----------|-----------|
| Nessun risultato restituito per una query con caratteri jolly | Verifica la sintassi del carattere jolly (`*min~~max`) e assicurati che le parole esistano entro la distanza specificata. |
| L'indice diventa obsoleto dopo aggiornamenti dei file | Riesegui `index.add(updatedFolder)` o utilizza l'API di aggiornamento incrementale. |
| Elevato consumo di memoria su grandi dataset | Aumenta la dimensione dell'heap JVM e considera di suddividere l'indice in più shard. |

## Domande frequenti

**D: Qual è la differenza tra un carattere jolly e una ricerca di frase?**  
R: Una ricerca di frase cerca un ordine esatto delle parole, mentre un carattere jolly ti permette di sostituire o saltare parole all'interno di quell'ordine.

**D: Posso usare i caratteri jolly con dati numerici nelle ricerche?**  
R: Sì, i parametri di intervallo del carattere jolly funzionano sia con numeri sia con parole.

**D: Come gestire collezioni di documenti molto grandi?**  
R: Mantieni l'indice ottimizzato, usa aggiornamenti incrementali e progetta i pattern di caratteri jolly il più specifici possibile.

**D: GroupDocs.Search è adatto a scenari di ricerca in tempo reale?**  
R: Assolutamente—una volta costruito l'indice, le query vengono eseguite in millisecondi, rendendolo adatto ad applicazioni interattive.

**D: Posso integrare questa libreria in un progetto Java esistente?**  
R: Sì. Aggiungi la dipendenza Maven o il JAR, inizializza l'indice come mostrato, e sei pronto a partire.

---

**Ultimo aggiornamento:** 2026-01-26  
**Testato con:** GroupDocs.Search 25.4 per Java  
**Autore:** GroupDocs