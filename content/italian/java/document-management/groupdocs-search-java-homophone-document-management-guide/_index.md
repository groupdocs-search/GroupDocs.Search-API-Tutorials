---
date: '2026-09-21'
description: Scopri come creare un indice di ricerca full text java usando GroupDocs.Search,
  aggiungere documenti e abilitare il supporto homophone per risultati più accurati.
keywords:
- java full text search
- homophone search java
- GroupDocs.Search Java
- document indexing java
- search index java
lastmod: '2026-09-21'
og_description: Scopri come creare un indice di ricerca full text java con GroupDocs.Search,
  aggiungere documenti e abilitare il supporto homophone per ricerche più veloci e
  più accurate.
og_image_alt: Illustration of a Java full text search index with homophone support
og_title: Come creare un indice di ricerca full text java con homophones
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create a java full text search index using GroupDocs.Search,
    add documents, and enable homophone support for more accurate results.
  headline: How to build a java full text search index with homophones
  type: TechArticle
- description: Learn how to create a java full text search index using GroupDocs.Search,
    add documents, and enable homophone support for more accurate results.
  name: How to build a java full text search index with homophones
  steps:
  - name: '**Install via Maven** or download directly from the provided links.'
    text: '**Install via Maven** or download directly from the provided links.'
  - name: '**Acquire a license:** You can start with a free trial or obtain a temporary
      license by visiting [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Acquire a license:** You can start with a free trial or obtain a temporary
      license by visiting [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Initialize the library:** The snippet below shows the minimal code required
      to start using GroupDocs.Search.'
    text: '**Initialize the library:** The snippet below shows the minimal code required
      to start using GroupDocs.Search.'
  - name: '**Legal document management:** Distinguish between similar‑sounding legal
      terms such as “lease” vs. “least”.'
    text: '**Legal document management:** Distinguish between similar‑sounding legal
      terms such as “lease” vs. “least”.'
  - name: '**Educational content creation:** Ensure teaching materials are free from
      ambiguous wording that could confuse learners.'
    text: '**Educational content creation:** Ensure teaching materials are free from
      ambiguous wording that could confuse learners.'
  - name: '**Customer support systems:** Improve knowledge‑base search accuracy, helping
      agents locate the right articles faster.'
    text: '**Customer support systems:** Improve knowledge‑base search accuracy, helping
      agents locate the right articles faster.'
  type: HowTo
- questions:
  - answer: A data structure that enables fast full‑text search across documents.
    question: What is a search index?
  - answer: It improves recall by matching words that sound alike, e.g., “mail” vs.
      “male”.
    question: Why use homophone recognition?
  - answer: GroupDocs.Search for Java (v25.4).
    question: Which library provides this in Java?
  - answer: A free trial works for evaluation; a permanent license is required for
      production.
    question: Do I need a license?
  - answer: JDK 8 or higher.
    question: What Java version is required?
  type: FAQPage
tags:
- java full text search
- homophone search
- GroupDocs.Search
- document indexing
- search index
title: Come creare un indice di ricerca full text java con homophones
type: docs
url: /it/java/document-management/groupdocs-search-java-homophone-document-management-guide/
weight: 1
---

# Come creare un indice di ricerca full text java con omofoni

In questa guida imparerai a creare un indice di **java full text search** utilizzando GroupDocs.Search, aggiungere documenti e abilitare il supporto agli omofoni in modo che le ricerche comprendano parole che suonano allo stesso modo. Alla fine del tutorial avrai un indice veloce, consapevole della lingua, che può essere interrogato in millisecondi, rendendo le tue applicazioni più user‑friendly e precise.

## Risposte rapide
- **Cos'è un indice di ricerca?** Una struttura dati che consente una ricerca full‑text veloce tra i documenti.  
- **Perché utilizzare il riconoscimento degli omofoni?** Migliora il recall abbinando parole che suonano allo stesso modo, ad es., “mail” vs. “male”.  
- **Quale libreria fornisce questo in Java?** GroupDocs.Search for Java (v25.4).  
- **È necessaria una licenza?** Una prova gratuita è sufficiente per la valutazione; è richiesta una licenza permanente per la produzione.  
- **Quale versione di Java è richiesta?** JDK 8 o superiore.

## Cos'è java full text search?
`java full text search` è il processo di indicizzazione del contenuto dei documenti in modo da poter interrogare il testo rapidamente e recuperare file pertinenti in tempo reale. L'indice memorizza termini tokenizzati, posizioni e metadati, consentendo risposte di ricerca inferiori al secondo anche su collezioni di grandi dimensioni.

## Perché usare GroupDocs.Search per Java?
GroupDocs.Search supporta **oltre 50 formati di file** — inclusi PDF, DOCX, XLSX, PPTX e HTML — fornendo al contempo un dizionario di omofoni integrato che aumenta il recall fino al **30 %** per termini ambigui. L'API astrae i dettagli di indicizzazione a basso livello, permettendoti di concentrarti sulla logica di business. Offre anche un'integrazione semplice con progetti Maven e una documentazione chiara per uno sviluppo rapido.

## Prerequisiti

Prima di immergerti nel codice, assicurati di avere quanto segue:

- **GroupDocs.Search for Java** (disponibile via Maven o download diretto).  
- Un **JDK compatibile** (8 o più recente).  
- Un IDE come **IntelliJ IDEA** o **Eclipse**.  
- Conoscenze di base di Java e Maven.

### Librerie e dipendenze richieste
Avrai bisogno di GroupDocs.Search for Java. Includilo usando Maven o scaricalo direttamente.

**Installazione Maven:**  
Aggiungi il seguente al tuo file `pom.xml`:

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

**Download diretto:**  
In alternativa, scarica l'ultima versione da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Requisiti di configurazione dell'ambiente
Assicurati di avere un JDK compatibile installato (JDK 8 o superiore) e un IDE come IntelliJ IDEA o Eclipse configurato sulla tua macchina.

### Prerequisiti di conoscenza
Familiarità con i concetti di programmazione Java e esperienza nell'uso di Maven per la gestione delle dipendenze sarà utile. Una comprensione di base dell'indicizzazione dei documenti e degli algoritmi di ricerca può inoltre aiutare.

## Configurare GroupDocs.Search per Java

Una volta sistemati i prerequisiti, configurare GroupDocs.Search è semplice:

1. **Installa via Maven** o scarica direttamente dai link forniti.  
2. **Ottieni una licenza:** Puoi iniziare con una prova gratuita o ottenere una licenza temporanea visitando [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).  
3. **Inizializza la libreria:** Lo snippet qui sotto mostra il codice minimo necessario per iniziare a usare GroupDocs.Search.

```java
import com.groupdocs.search.*;

public class SetupExample {
    public static void main(String[] args) {
        // Define the directory for storing index files.
        String indexFolder = "path/to/index/directory";
        
        // Initialize an Index instance.
        Index index = new Index(indexFolder);
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Guida all'implementazione

Ora che l'ambiente è pronto, esploriamo le funzionalità principali di cui avrai bisogno per **creare un indice di java full text search** e gestire gli omofoni.

### Creazione e gestione di un indice
#### Panoramica
Creare un indice di ricerca è il primo passo per gestire efficacemente i documenti. Questo consente un recupero rapido delle informazioni basato sul contenuto dei tuoi documenti.

#### Passaggi per creare un indice
**Passo 1:** Specifica la directory per i file del tuo indice.

```java
String indexFolder = "YOUR_INDEX_DIRECTORY";
Index index = new Index(indexFolder);
```

*La classe `Index` rappresenta il contenitore ricercabile che contiene termini tokenizzati e metadati per ogni documento, fornendo la struttura centrale che consente l'esecuzione rapida delle query e l'archiviazione efficiente delle informazioni dei documenti in tutto l'indice.*

**Passo 2:** Aggiungi documenti da una cartella specificata a questo indice.

```java
String documentsFolder = "YOUR_DOCUMENTS_SOURCE_DIRECTORY";
index.add(documentsFolder);
System.out.println("Documents added to the index.");
```

*Chiamare `index.add()` importa ogni file, estrae il testo e popola le strutture interne necessarie per query rapide, garantendo che ogni documento sia completamente indicizzato e immediatamente ricercabile senza richiedere un passaggio di elaborazione separato.*

### Come aggiungere documenti all'indice
Puoi aggiungere programmaticamente altri file in seguito chiamando nuovamente `index.add()` con un nuovo percorso di cartella o percorsi di file individuali. Questo approccio incrementale mantiene l'indice aggiornato senza una ricostruzione completa. Aggiungere documenti in questo modo ti consente di mantenere un indice live che riflette le ultime modifiche di contenuto, supportando la disponibilità continua della ricerca per gli utenti finali e riducendo i tempi di inattività associati alle operazioni di reindicizzazione batch.

### Recuperare gli omofoni per una parola
Recuperare gli omofoni per un termine specifico aiuta il motore di ricerca a considerare ortografie alternative che suonano allo stesso modo, migliorando il recall per le query in cui gli utenti possono digitare erroneamente o usare varianti diverse. Espandendo la query con equivalenti fonetici, il motore può corrispondere a documenti che contengono qualsiasi forma omofonica, fornendo risultati più completi.

*La classe `HomophoneDictionary` memorizza gruppi di parole che condividono la stessa pronuncia, fungendo da repository centrale a cui il motore di ricerca fa riferimento quando espande le query con alternative fonetiche, migliorando così la pertinenza dei risultati di ricerca.*

```java
String[] homophones = index.getDictionaries().getHomophoneDictionary().getHomophones("braid");
```

### Recuperare gruppi di omofoni
Raggruppare gli omofoni fornisce un modo strutturato per gestire parole con più significati, consentendo agli sviluppatori di recuperare interi insiemi di equivalenti fonetici in un'unica operazione. Questo può essere utile per analisi, gestione di dizionari personalizzati o aggiornamenti massivi della lista degli omofoni.

*Ogni gruppo restituito da `getGroups()` contiene parole intercambiabili nelle ricerche fonetiche, e il metodo fornisce una collezione completa di questi gruppi così da poter ispezionare, modificare o esportare l'intero set di relazioni omofoniche mantenute dal dizionario.*

```java
String[][] groups = index.getDictionaries().getHomophoneDictionary().getHomophoneGroups("braid");
```

### Cancellare il dizionario degli omofoni
Cancellare voci obsolete o non necessarie garantisce che il tuo dizionario rimanga rilevante e non introduca rumore nei risultati di ricerca. Questa operazione viene solitamente eseguita quando è necessario ripristinare il dizionario al suo stato predefinito prima di caricare un nuovo set personalizzato.

*Il metodo `clear()` rimuove tutte le voci personalizzate, tornando al set predefinito, e garantisce che tutti i gruppi di omofoni aggiunti in precedenza siano completamente scartati, fornendo una base pulita per la successiva configurazione del dizionario.*

```java
if (index.getDictionaries().getHomophoneDictionary().getCount() > 0) {
    index.getDictionaries().getHomophoneDictionary().clear();
}
System.out.println("Homophone dictionary cleared.");
```

### Aggiungere omofoni al dizionario
Personalizzare il tuo dizionario di omofoni consente capacità di ricerca su misura che riflettono terminologia specifica del dominio, slang o nomi di brand. Aggiungendo nuovi gruppi, puoi garantire che le ricerche riconoscano le relazioni fonetiche desiderate uniche per la tua applicazione.

*Usa `addGroup()` per inserire una lista di parole con suono sinonimo, migliorando il recall per la terminologia specifica del dominio, e il metodo valida ogni voce per prevenire duplicati integrando il nuovo gruppo senza soluzione di continuità nella struttura del dizionario esistente.*

```java
String[][] homophoneGroups = {
    new String[] { "awe", "oar", "or", "ore" },
    new String[] { "aye", "eye", "i" },
    new String[] { "call", "caul" }
};
index.getDictionaries().getHomophoneDictionary().addRange(homophoneGroups);
System.out.println("Homophones added to the dictionary.");
```

### Esportare e importare dizionari di omofoni
Esportare e importare dizionari può essere utile per scopi di backup o migrazione, permettendoti di preservare configurazioni personalizzate tra ambienti o condividerle con i membri del team. Questa funzionalità supporta il formato JSON per una facile leggibilità e integrazione con altri strumenti.

*Questi metodi ti consentono di persistere dizionari personalizzati come file JSON per un facile riutilizzo, e il processo di esportazione cattura lo stato completo del dizionario mentre la routine di importazione valida la struttura JSON prima di applicarla all'istanza del dizionario attivo.*

```java
String fileName = "path/to/exported/dictionary.file";
index.getDictionaries().getHomophoneDictionary().exportDictionary(fileName);
```

**Passo 2:** Re‑importa da un file se necessario.

```java
index.getDictionaries().getHomophoneDictionary().importDictionary(fileName);
System.out.println("Homophone dictionary imported successfully.");
```

*L'operazione di importazione legge il file JSON, ricostruisce ogni gruppo di omofoni e lo unisce al dizionario corrente, garantendo che tutte le voci personalizzate siano accuratamente ripristinate e pronte per l'uso immediato nelle query di ricerca.*

### Ricerca usando gli omofoni
Sfrutta la ricerca con omofoni per un recupero completo dei documenti, consentendo agli utenti di trovare contenuti pertinenti anche quando usano ortografie diverse che suonano allo stesso modo. Questa funzionalità può migliorare notevolmente l'esperienza utente in domini multilingue o con forte componente fonetica.

*Impostare `setUseHomophoneSearch(true)` indica al motore di espandere le query con equivalenti fonetici prima dell'esecuzione, e questa opzione funziona in combinazione con altre impostazioni di ricerca come il fuzzy matching per fornire un'esperienza di ricerca robusta e flessibile che cattura un'ampia gamma di risultati pertinenti.*

```java
String query = "caul";
SearchOptions options = new SearchOptions();
options.setUseHomophoneSearch(true);
SearchResult result = index.search(query, options);

System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## Applicazioni pratiche

Comprendere come implementare queste funzionalità apre un mondo di applicazioni pratiche:

1. **Gestione di documenti legali:** Distinguere tra termini legali simili nel suono come “lease” vs. “least”.  
2. **Creazione di contenuti educativi:** Garantire che i materiali didattici siano privi di formulazioni ambigue che potrebbero confondere gli studenti.  
3. **Sistemi di supporto clienti:** Migliorare l'accuratezza della ricerca nella knowledge‑base, aiutando gli operatori a trovare gli articoli giusti più rapidamente.

## Considerazioni sulle prestazioni

Per mantenere la tua **java full text search** performante:

- **Aggiorna l'indice regolarmente** per riflettere le modifiche ai documenti.  
- **Monitora l'uso della memoria** e regola le impostazioni dell'heap Java per grandi set di dati.  
- **Chiudi tempestivamente le risorse inutilizzate** (ad es., chiama `index.close()` al termine).  

## Conclusione

A questo punto dovresti avere una solida comprensione di **come indicizzare i documenti** con GroupDocs.Search, gestire gli omofoni e perfezionare la tua esperienza di ricerca. Questi strumenti sono inestimabili per fornire risultati precisi e aumentare l'efficienza complessiva della gestione dei documenti.

## Domande frequenti

**Q:** Posso usare il dizionario degli omofoni con lingue non‑English?  
**A:** Sì, puoi popolare il dizionario con qualsiasi lingua purché tu fornisca i gruppi di parole appropriati.

**Q:** È necessaria una licenza per i test di sviluppo?  
**A:** Una licenza di prova gratuita è sufficiente per sviluppo e test; è necessaria una licenza a pagamento per le distribuzioni in produzione.

**Q:** Quanto può essere grande il mio indice?  
**A:** La dimensione dell'indice è limitata solo dalle risorse hardware; assegna spazio su disco e memoria sufficienti per prestazioni ottimali.

**Q:** È possibile combinare la ricerca di omofoni con il fuzzy matching?  
**A:** Assolutamente. Abilita sia `setUseHomophoneSearch(true)` sia `setFuzzySearch(true)` in `SearchOptions` per ottenere il meglio di entrambi.

**Q:** Cosa succede se aggiungo gruppi di omofoni duplicati?  
**A:** Le voci duplicate vengono ignorate; il dizionario mantiene un set unico di gruppi di parole.

---

**Last Updated:** 2026-09-21  
**Tested with:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Tutorial correlati

- [Come implementare java full text search: creare la directory dell'indice con GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Come aggiungere documenti all'indice con indicizzazione dei metadati in Java usando GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Libreria Java Full Text Search – Ottimizzare l'indice con GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)