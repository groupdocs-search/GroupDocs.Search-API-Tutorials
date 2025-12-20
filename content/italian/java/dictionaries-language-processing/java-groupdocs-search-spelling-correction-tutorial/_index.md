---
date: '2025-12-20'
description: Scopri come abilitare la correzione ortografica in Java usando GroupDocs.Search,
  aggiungere documenti all'indice e impostare il conteggio massimo di errori per una
  migliore precisione di ricerca.
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: Come abilitare l'ortografia in Java con GroupDocs.Search
type: docs
url: /it/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Come abilitare il controllo ortografico in Java usando GroupDocs.Search

Risultati di ricerca accurati sono essenziali per qualsiasi applicazione moderna. In questo tutorial imparerai **come abilitare il controllo ortografico** in Java con GroupDocs.Search, così gli utenti otterranno i risultati corretti anche quando digitano query con errori. Vedremo come creare un indice, **aggiungere documenti all'indice**, configurare le opzioni di ortografia e eseguire una ricerca che corregge automaticamente gli errori.

## Risposte rapide
- **Cosa significa “come abilitare il controllo ortografico”?** Attiva il correttore ortografico integrato che corregge gli errori di battitura dell'utente durante una ricerca.  
- **Quale libreria fornisce questa funzionalità?** GroupDocs.Search per Java.  
- **È necessaria una licenza?** Una licenza di prova gratuita è sufficiente per la valutazione; è necessaria una licenza completa per la produzione.  
- **Posso controllare la tolleranza?** Sì – usa `setMaxMistakeCount` per definire quanti errori di battitura sono consentiti.  
- **È adatto a indici di grandi dimensioni?** Assolutamente – il motore è ottimizzato per indicizzazione e ricerca ad alte prestazioni.

## Cos'è “come abilitare il controllo ortografico” in GroupDocs.Search?
Abilitare il controllo ortografico indica al motore di ricerca di cercare i termini corretti più vicini quando una query contiene errori. Questa funzionalità migliora notevolmente l'esperienza dell'utente restituendo risultati pertinenti anche con input errati.

## Perché abilitare il controllo ortografico nelle applicazioni Java?
- **Aumenta la soddisfazione degli utenti** – gli utenti non devono digitare in modo perfetto.  
- **Riduce i tassi di rimbalzo** – risultati più accurati mantengono i visitatori coinvolti.  
- **Funziona in diversi domini** – dai cataloghi di biblioteche alle ricerche di prodotti e‑commerce.

## Prerequisiti
- Java Development Kit (JDK) installato.  
- Conoscenze di base di Java e Maven.  
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

## Come aggiungere documenti all'indice
Creare un indice è la base per qualsiasi applicazione con ricerca. Di seguito è riportato un esempio minimale che **aggiunge documenti all'indice** da una cartella.

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

*Suggerimento:* Verifica che i percorsi siano corretti e che l'applicazione abbia i permessi di scrittura sulla cartella dell'indice.

## Come configurare il controllo ortografico (imposta il conteggio massimo di errori)
Puoi perfezionare il correttore ortografico abilitandolo e impostando la tolleranza per gli errori.

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

*Perché `setMaxMistakeCount` è importante:* Definisce quanti errori di battitura il motore tollererà. Regola questo valore in base ai tipici pattern di errore del tuo dominio.

## Come eseguire una ricerca con correzione ortografica
Con l'indice pronto e le opzioni ortografiche configurate, esegui una query che può contenere errori.

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

La chiamata `search()` restituisce un `SearchResult` che contiene i termini corretti e i documenti più pertinenti.

## Applicazioni pratiche
1. **Sistemi di biblioteca:** Correggi titoli di libri o nomi di autori digitati erroneamente.  
2. **Piattaforme e‑commerce:** Correggi gli errori di battitura degli utenti nelle ricerche di prodotti per aumentare le conversioni.  
3. **Sistemi di gestione dei contenuti:** Migliora il recupero degli articoli per il personale editoriale.

## Considerazioni sulle prestazioni
- **Mantieni l'indice aggiornato** – reindicizza regolarmente i file nuovi o modificati.  
- **Regola le impostazioni di memoria della JVM** – assegna un heap sufficiente per indici di grandi dimensioni.  
- **Monitora l'utilizzo delle risorse** – regola i flag del garbage collector se necessario.

## Domande frequenti

**D: Cos'è GroupDocs.Search?**  
R: È una libreria Java che offre indicizzazione rapida, funzionalità di ricerca avanzate e correzione ortografica integrata.

**D: Come posso ottenere una licenza per GroupDocs.Search?**  
R: Visita il sito ufficiale per scaricare una prova gratuita o acquistare una licenza completa.

**D: Posso integrare GroupDocs.Search con altri framework Java?**  
R: Sì, funziona con Spring, Jakarta EE e qualsiasi applicazione Java standard.

**D: Quali sono i problemi comuni nella configurazione di un indice?**  
R: Percorsi di cartelle errati, permessi di file insufficienti o dipendenze mancanti in `pom.xml`.

**D: Come la correzione ortografica migliora i risultati di ricerca?**  
R: Riscrive automaticamente le query errate con i termini corretti più vicini, restituendo risultati più pertinenti.

## Risorse aggiuntive
- [Documentazione](https://docs.groupdocs.com/search/java/)
- [Riferimento API](https://reference.groupdocs.com/search/java)
- [Download](https://releases.groupdocs.com/search/java/)
- [Repository GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/search/10)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2025-12-20  
**Testato con:** GroupDocs.Search 25.4  
**Autore:** GroupDocs