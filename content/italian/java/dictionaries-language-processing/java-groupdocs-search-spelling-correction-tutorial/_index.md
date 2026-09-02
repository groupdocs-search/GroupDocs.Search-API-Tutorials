---
date: '2026-09-02'
description: Scopri come creare un search index java e abilitare lo spelling correction
  usando GroupDocs.Search. Segui le istruzioni passo‑passo per aggiungere documenti,
  configurare il max mistake count e migliorare la search accuracy.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: Scopri come creare un search index java e abilitare lo spelling correction
  usando GroupDocs.Search. Segui le istruzioni passo‑passo per aggiungere documenti,
  configurare il max mistake count e migliorare la search accuracy.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: Come creare un search index java e abilitare lo spelling
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: Come creare un search index java e abilitare lo spelling
type: docs
url: /it/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Come creare un indice di ricerca java e abilitare l'ortografia

Nelle moderne applicazioni Java, fornire risultati di ricerca accurati è una caratteristica indispensabile. Questo tutorial mostra **come creare un indice di ricerca java** e attivare la correzione ortografica con GroupDocs.Search, così gli utenti ricevono risultati pertinenti anche quando digitano query errate. Vedrai come configurare la libreria, aggiungere documenti, impostare il conteggio massimo di errori e eseguire una ricerca tollerante ai typo — il tutto senza scrivere una sola riga di codice di configurazione aggiuntivo.

## Risposte rapide
- **Cosa fa “enable spelling”?** Attiva il correttore ortografico integrato che riscrive i termini errati nella loro forma corretta più vicina durante una ricerca.  
- **Quale libreria fornisce questa funzionalità?** GroupDocs.Search per Java.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per la valutazione; è necessaria una licenza completa per l'uso in produzione.  
- **Posso controllare la tolleranza?** Sì – usa `setMaxMistakeCount` per definire quanti errori di battitura sono consentiti per query.  
- **È adatto a indici di grandi dimensioni?** Assolutamente – il motore gestisce indici con milioni di record mantenendo la latenza delle query sotto i 100 ms su hardware server tipico.

## Cos'è GroupDocs.Search?
GroupDocs.Search è una libreria Java che fornisce indicizzazione full‑text veloce e funzionalità di ricerca avanzate, inclusa la correzione ortografica integrata. Supporta oltre 50 formati di input e può elaborare documenti di centinaia di pagine senza caricare l'intero file in memoria.

## Perché abilitare la correzione ortografica nelle applicazioni Java?
- **Aumenta la soddisfazione degli utenti** – i visitatori ottengono risultati corretti anche con una digitazione imperfetta.  
- **Riduce i tassi di rimbalzo** – risultati accurati mantengono gli utenti più coinvolti.  
- **Funziona in tutti i domini** – dai cataloghi di biblioteche alle ricerche di prodotti e‑commerce, la correzione ortografica migliora la pertinenza ovunque.

## Prerequisiti
- Java Development Kit (JDK) installato.  
- Conoscenza di base di Java e Maven.  
- Comprensione dei concetti di indicizzazione.  
- Una prova o chiave licenza di GroupDocs.Search.

### Configurazione di GroupDocs.Search per Java
Integra la libreria nel tuo progetto Maven.

**Configurazione Maven**  
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

**Download diretto**  
In alternativa, scarica l'ultima versione da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
Ottieni una licenza di prova gratuita per la valutazione. Per l'uso in produzione, acquista una licenza completa o richiedi una chiave temporanea dal sito ufficiale.

## Come creo un indice di ricerca in Java?
`SearchIndex` è la classe principale che rappresenta un indice ricercabile memorizzato su disco.  
Crea un'istanza di `SearchIndex` che punta a una cartella su disco, quindi aggiungi documenti da una directory di origine. Il motore costruisce un indice invertito che consente ricerche rapide. Puoi chiamare `index.add()` per ogni file; la libreria estrae il testo automaticamente in base al tipo di file.

## Come posso abilitare la correzione ortografica?
`getSpellingOptions()` restituisce l'oggetto di configurazione ortografica per l'indice, consentendoti di abilitare o modificare le funzionalità di correzione.  
Abilita l'ortografia chiamando `index.getSpellingOptions().setEnabled(true)`. Questo indica al motore di analizzare i termini della query e suggerire alternative corrette quando vengono rilevate discrepanze. La funzionalità funziona subito per tutte le lingue indicizzate supportate dalla libreria.

## Qual è l'impostazione del conteggio massimo di errori?
`setMaxMistakeCount` configura il numero massimo di modifiche di caratteri che il correttore ortografico tollererà per termine.  
`setMaxMistakeCount(int)` definisce il numero massimo di modifiche di caratteri (inserimenti, cancellazioni, sostituzioni) che il correttore ortografico tollererà per termine. Impostandolo a **2** consente al motore di correggere i typo comuni di due caratteri evitando correzioni eccessivamente aggressive che potrebbero restituire risultati non correlati.

## Come eseguire una ricerca con correzione ortografica
`search()` esegue una query contro l'indice e restituisce un oggetto `SearchResult` contenente i risultati e eventuali termini corretti.  
Esegui una query di ricerca usando il metodo `search()`. Se la query contiene parole errate, il motore restituisce un `SearchResult` che include i termini corretti e un elenco dei documenti più pertinenti. Puoi mostrare sia la query originale sia la versione corretta all'utente per trasparenza.  
`SearchResult` contiene l'elenco dei documenti corrispondenti e le informazioni sulle correzioni della query.

## Applicazioni pratiche
1. **Sistemi di biblioteca** – corregge automaticamente i titoli dei libri o i nomi degli autori digitati erroneamente.  
2. **Piattaforme e‑commerce** – corregge i typo nei nomi dei prodotti per aumentare i tassi di conversione.  
3. **Gestione dei contenuti** – aiuta il personale editoriale a trovare articoli anche con parole chiave imperfette.

## Considerazioni sulle prestazioni
- **Mantieni l'indice aggiornato** – reindicizza regolarmente i file nuovi o modificati.  
- **Regola le impostazioni di memoria della JVM** – assegna un heap sufficiente per indici di grandi dimensioni (es., `-Xmx4g`).  
- **Monitora l'utilizzo delle risorse** – regola i flag del garbage collector se noti pause durante l'indicizzazione di massa.

## Problemi comuni e risoluzione
| Sintomo | Causa probabile | Risoluzione |
|---------|-----------------|-------------|
| Nessun risultato dopo aver abilitato l'ortografia | Il percorso della cartella dell'indice è errato o vuoto | Verifica che `indexFolder` punti a un indice valido e che `index.add()` sia riuscito |
| Il correttore ortografico non corregge typo evidenti | `setMaxMistakeCount` è impostato troppo basso | Aumenta il conteggio a 2 o 3 per una correzione più tollerante |
| L'applicazione si arresta con set di documenti di grandi dimensioni | Heap JVM insufficiente | Aumenta l'opzione `-Xmx` (es., `-Xmx4g`) |

## Domande frequenti
**Q: Cos'è GroupDocs.Search?**  
A: GroupDocs.Search è una libreria Java che fornisce indicizzazione veloce, capacità di query avanzate e correzione ortografica integrata per qualsiasi applicazione Java.

**Q: Come posso ottenere una licenza per GroupDocs.Search?**  
A: Visita il sito ufficiale per scaricare una prova gratuita o acquistare una licenza completa; è disponibile anche una chiave temporanea per test a breve termine.

**Q: Posso integrare GroupDocs.Search con altri framework Java?**  
A: Sì, funziona senza problemi con Spring, Jakarta EE e qualsiasi applicazione Java standard.

**Q: Quali sono i problemi comuni nella configurazione di un indice?**  
A: Percorsi di cartelle errati, permessi di file mancanti o dipendenze Maven assenti sono le cause tipiche.

**Q: Come migliora la correzione ortografica i risultati di ricerca?**  
A: Riscrive automaticamente le query errate nei termini corretti più vicini, restituendo risultati più pertinenti e riducendo la frustrazione dell'utente.

## Risorse aggiuntive
- [Documentazione](https://docs.groupdocs.com/search/java/)
- [Riferimento API](https://reference.groupdocs.com/search/java)
- [Download](https://releases.groupdocs.com/search/java/)
- [Repository GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/search/10)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2026-09-02  
**Testato con:** GroupDocs.Search 25.4  
**Autore:** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## Tutorial correlati

- [Come creare un indice di documenti e aggiungere documenti usando l'API GroupDocs.Search per Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Elaborazione linguistica Java – Creare dizionario dei sinonimi con GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Parole stop nella ricerca: aggiungere documenti all'indice con GroupDocs.Search Java](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)