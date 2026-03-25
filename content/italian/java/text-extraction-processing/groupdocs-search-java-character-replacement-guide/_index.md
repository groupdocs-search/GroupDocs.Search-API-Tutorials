---
date: '2026-03-25'
description: Scopri come creare un array di sostituzione dei caratteri ed eseguire
  una ricerca sensibile al maiuscolo/minuscolo in Java utilizzando GroupDocs.Search
  Java. Questa guida copre l'installazione, le migliori pratiche e le applicazioni
  pratiche per migliorare la precisione della ricerca.
keywords:
- character replacement
- text indexing
- search optimization
- GroupDocs.Search Java
title: Crea un array di sostituzione dei caratteri con GroupDocs.Search Java
type: docs
url: /it/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/
weight: 1
---

# Crea un array di sostituzione dei caratteri con GroupDocs.Search Java: Guida completa

In questo tutorial **creerai un array di sostituzione dei caratteri** per normalizzare il testo durante l'indicizzazione e scoprirai come eseguire una query di **case sensitive search java** con GroupDocs.Search. Che tu stia pulendo dati incoerenti, standardizzando documenti legacy o semplicemente migliorando la pertinenza della ricerca, queste funzionalità ti consentono di perfezionare la pipeline di indicizzazione senza riscrivere i file sorgente.

## Risposte rapide
- **Che cosa fa un array di sostituzione dei caratteri?** Mappa i caratteri originali a quelli di sostituzione prima dell'indicizzazione, garantendo una tokenizzazione coerente.  
- **Ho bisogno di una licenza per provare?** Una prova gratuita o una licenza temporanea è sufficiente per lo sviluppo e i test.  
- **Posso sostituire più caratteri contemporaneamente?** Sì – puoi popolare l'array con le mappature per ogni carattere Unicode di cui hai bisogno.  
- **La ricerca case‑sensitive è supportata?** Assolutamente; abilita `setUseCaseSensitiveSearch(true)` in `SearchOptions`.  
- **Dove vengono memorizzate le regole di sostituzione?** Possono essere esportate o importate da un file `.dat` per il riutilizzo tra progetti.

## Introduzione

La sostituzione dei caratteri è una funzionalità fondamentale per qualsiasi soluzione di ricerca che deve gestire testo rumoroso o eterogeneo. Configurando GroupDocs.Search Java per **creare un array di sostituzione dei caratteri**, garantisci che caratteri come trattini, underscore o simboli specifici della locale siano trattati in modo uniforme, migliorando notevolmente la qualità delle corrispondenze. Inoltre, abbinare questa configurazione a una **case sensitive search java** ti permette di distinguere tra “Apple” e “apple” quando tale distinzione è importante.

## Prerequisiti

- **Librerie e dipendenze:** Libreria GroupDocs.Search Java versione 25.4 o successiva.  
- **Ambiente:** Java 8+ con Maven per la gestione delle dipendenze.  
- **Base di conoscenza:** Programmazione Java di base e familiarità con i concetti di indicizzazione.

## Configurazione di GroupDocs.Search per Java

### Configurazione Maven

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

In alternativa, scarica l'ultima versione direttamente da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione licenza

Inizia con una prova gratuita o richiedi una licenza temporanea per esplorare tutte le funzionalità di GroupDocs.Search. Per un utilizzo a lungo termine, considera l'acquisto di un abbonamento.

### Inizializzazione e configurazione di base

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

// Define the folder where your index will be stored
String indexFolder = "YOUR_OUTPUT_DIRECTORY/CharacterReplacements/Index";

// Initialize IndexSettings and set up character replacements
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Create an index with specified settings
Index index = new Index(indexFolder, settings);
```

## Come creare un array di sostituzione dei caratteri

Abilitare le sostituzioni dei caratteri nelle impostazioni dell'indice è solo il primo passo. Di seguito vediamo come cancellare le mappature esistenti, aggiungere coppie personalizzate e infine costruire un array completo che sostituisce ogni carattere con la sua equivalente minuscola.

### Abilitare le sostituzioni dei caratteri nelle impostazioni dell'indice

#### Cancellare le sostituzioni esistenti

```java
if (index.getDictionaries().getCharacterReplacements().getCount() > 0) {
    index.getDictionaries().getCharacterReplacements().clear();
}
```

#### Aggiungere una sostituzione di carattere

```java
index.getDictionaries().getCharacterReplacements().addRange(
    new CharacterReplacementPair[] { new CharacterReplacementPair('-', '~') }
);
```

### Creare nuove sostituzioni di caratteri

#### Inizializzare l'array di sostituzione

```java
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char)i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}
```

#### Aggiungere le sostituzioni al dizionario

```java
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Esportare e importare le sostituzioni di caratteri

#### Esportare le sostituzioni di caratteri

```java
String fileName = "YOUR_OUTPUT_DIRECTORY/CharacterReplacements/CharacterReplacements.dat";
index.getDictionaries().getCharacterReplacements().exportDictionary(fileName);
```

#### Importare le sostituzioni di caratteri

```java
index.getDictionaries().getCharacterReplacements().importDictionary(fileName);
```

## Aggiungere documenti ed eseguire una case sensitive search java

### Aggiungere documenti all'indice

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

### Eseguire una case sensitive search java

```java
String query = "Elliot";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
SearchResult result = index.search(query, options);
```

## Applicazioni pratiche

- **Standardizzazione dei dati:** Sostituire uniformemente la punteggiatura o i simboli specifici della locale prima dell'indicizzazione.  
- **Correzione errori:** Correggere automaticamente errori tipografici comuni (ad esempio, “‑” → “~”).  
- **Localizzazione:** Regolare i set di caratteri per diverse lingue senza modificare i file sorgente.  
- **Analisi di dati storici:** Normalizzare documenti legacy che usano convenzioni di caratteri obsolete.  
- **Integrazione di sistema:** Mantenere i dati CRM/ERP coerenti applicando le stesse regole di sostituzione lungo le pipeline.

## Considerazioni sulle prestazioni

- **Ottimizzare la dimensione dell'indice:** Rimuovere periodicamente le voci obsolete per mantenere l'indice snello.  
- **Gestione delle risorse:** Ottimizzare la garbage collection della JVM e monitorare l'uso dell'heap durante l'indicizzazione di massa.  
- **Elaborazione batch:** Indicizzare i documenti in batch per ridurre l'overhead I/O e migliorare il throughput.

## Conclusione

Imparando a **creare un array di sostituzione dei caratteri** e combinandolo con una configurazione **case sensitive search java**, puoi aumentare notevolmente la pertinenza e l'affidabilità delle tue soluzioni di ricerca. Sperimenta con diverse mappature, esportale per il riutilizzo e esplora dizionari aggiuntivi come i sinonimi per esperienze di ricerca ancora più ricche.

**Prossimi passi**

- Testa varie strategie di sostituzione su un dataset di esempio per vedere il loro impatto sui tassi di hit.  
- Approfondisci altre funzionalità di GroupDocs.Search come i dizionari di sinonimi, lo stemming e la ricerca fuzzy.

## Domande frequenti

**D: Qual è il principale vantaggio dell'utilizzare le sostituzioni di caratteri nell'indicizzazione?**  
R: Standardizza le voci di testo, migliorando l'accuratezza della ricerca e la coerenza tra documenti diversi.

**D: Posso sostituire più di un carattere alla volta?**  
R: Sì, puoi popolare l'array di sostituzione con quanti oggetti `CharacterReplacementPair` desideri.

**D: Come gestisco caratteri o simboli speciali?**  
R: Includili nel tuo array di sostituzione con mappature esplicite, ad esempio mappa “©” a “c”.

**D: È possibile esportare e importare le sostituzioni tra progetti diversi?**  
R: Assolutamente. Usa i metodi `exportDictionary` e `importDictionary` per condividere le mappature.

**D: Quali sono gli errori comuni nella configurazione delle sostituzioni di caratteri?**  
R: Dimenticare di cancellare le sostituzioni esistenti prima di aggiungerne di nuove, o impostare in modo errato le impostazioni dell'indice (`setUseCharacterReplacements(true)`) può portare a risultati inattesi.

## Risorse

- [Documentazione](https://docs.groupdocs.com/search/java/)
- [Riferimento API](https://reference.groupdocs.com/search/java)
- [Download GroupDocs.Search per Java](https://releases.groupdocs.com/search/java/)
- [Repository GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/search/10)
- [Acquisizione licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

Seguendo questa guida, sarai ben attrezzato per implementare le sostituzioni di caratteri e perfezionare il comportamento della ricerca nelle tue applicazioni Java.

---

**Ultimo aggiornamento:** 2026-03-25  
**Testato con:** GroupDocs.Search Java 25.4  
**Autore:** GroupDocs