---
date: '2026-05-12'
description: 'Impara java full text search con GroupDocs.Search: aggiungi documenti
  all''indice, configura le opzioni di unione e annulla l''operazione di unione. Ideale
  per soluzioni java di gestione documenti.'
keywords:
- java full text search
- document management java
- GroupDocs.Search merging
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: 'Learn java full text search with GroupDocs.Search: add documents to
    index, configure merge options, and cancel merge operation. Ideal for document
    management java solutions.'
  headline: java full text search – add docs & merge with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It tells GroupDocs.Search to scan a folder, extract searchable tokens,
      and store metadata for each file.
    question: What does “add documents to index” mean?
  - answer: Yes—use the `Cancellation` object to abort a merge after a configurable
      timeout.
    question: Can I stop a long merge?
  - answer: A free trial or temporary license works for testing; a commercial license
      unlocks full features.
    question: Do I need a license?
  - answer: JDK 8 or newer.
    question: Which Java version is required?
  - answer: Absolutely—GroupDocs.Search can handle multi‑hundred‑page documents with
      incremental indexing.
    question: Is this suitable for large datasets?
  type: FAQPage
title: java full text search – aggiungi documenti e unisci con GroupDocs.Search
type: docs
url: /it/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# java full text search – aggiungi documenti e unisci con GroupDocs.Search

Negli ambienti aziendali moderni, **java full text search** è la spina dorsale di qualsiasi sistema di gestione documentale java robusto. Che tu debba indicizzare contratti, fatture o report interni, un indice ben progettato ti consente di recuperare le informazioni corrette in millisecondi. Questo tutorial ti guida nella creazione di un indice, nell'aggiunta di documenti, nella configurazione delle opzioni di merge e nell'annullamento sicuro di un'operazione di merge—tutto utilizzando GroupDocs.Search per Java.

## Risposte rapide
- **Cosa significa “add documents to index”?** Indica a GroupDocs.Search di scansionare una cartella, estrarre token ricercabili e memorizzare i metadati per ogni file.  
- **Posso interrompere un merge lungo?** Sì—usa l'oggetto `Cancellation` per abortire un merge dopo un timeout configurabile.  
- **Ho bisogno di una licenza?** Una prova gratuita o una licenza temporanea è sufficiente per i test; una licenza commerciale sblocca tutte le funzionalità.  
- **Quale versione di Java è richiesta?** JDK 8 o successivo.  
- **È adatto a grandi set di dati?** Assolutamente—GroupDocs.Search può gestire documenti di centinaia di pagine con indicizzazione incrementale.

## Cos'è “add documents to index” in GroupDocs.Search?
**Aggiungere documenti a un indice significa fornire una collezione di file a GroupDocs.Search affinché la libreria possa analizzarne il contenuto, estrarre token e costruire una struttura dati ricercabile.** Il processo crea una rappresentazione compatta che consente query full‑text fulminee su tutti i file indicizzati.

## Perché usare GroupDocs.Search per la gestione documentale java?
GroupDocs.Search offre **indicizzazione scalabile per oltre 50 formati di input** (PDF, DOCX, XLSX, PPTX, HTML, immagini, ecc.) e può elaborare **documenti fino a 2 GB senza caricare l'intero file in memoria**. La sua API ti dà un controllo dettagliato su indicizzazione, unione e annullamento, rendendola una scelta primaria per soluzioni enterprise‑grade di java full text search.

## Prerequisiti
- **GroupDocs.Search for Java** versione 25.4 o successiva.  
- Maven (o download manuale del JAR).  
- Conoscenza base di Java e un ambiente JDK 8+.

## Configurazione di GroupDocs.Search per Java

### Installazione con Maven
Se gestisci le dipendenze con Maven, aggiungi il repository e la dipendenza al tuo `pom.xml`:

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
In alternativa, scarica l'ultimo JAR dal sito ufficiale: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
- **Free Trial:** Registrati sul sito GroupDocs per una licenza di prova.  
- **Temporary License:** Richiedi una chiave temporanea se hai bisogno di una valutazione estesa.  
- **Commercial License:** Acquista per uso in produzione.

Dopo aver ottenuto il file di licenza, posizionalo nel tuo progetto e inizializza la libreria come mostrato più avanti.

## Guida all'implementazione

### Come aggiungere documenti all'indice – Creazione del primo indice
**Carica o crea un indice vuoto istanziando la classe `Index`, che rappresenta un contenitore ricercabile su disco.** Questo passaggio prepara una posizione di archiviazione per tutti i token che saranno generati dai tuoi documenti.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **Perché:** Questo passaggio imposta un contenitore di archiviazione dove i token indicizzati saranno salvati.

#### Aggiunta di documenti all'indice
**Chiama `index.add` con un percorso di cartella; il metodo scansiona ogni file, estrae il testo e memorizza i metadati ricercabili nell'indice.** L'operazione viene eseguita in un unico passaggio e rispetta le `IndexSettings` configurate.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **Perché:** La libreria legge ogni file, estrae il testo e lo memorizza in `index1`.

### Creazione di un secondo indice per flussi di lavoro flessibili
**Istanzia un altro oggetto `Index` per contenere un set di documenti separato, consentendo una elaborazione isolata prima di un merge.** Questo schema è utile per scenari multi‑tenant o indicizzazione a fasi.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Perché:** Indici multipli ti permettono di gestire set di documenti distinti e combinarli successivamente.

### Come configurare le opzioni di merge e annullare l'operazione di merge
**Crea un'istanza `MergeOptions`, imposta i parametri desiderati e allega un token `Cancellation` che abortisce il merge dopo un timeout specificato.** Questo ti dà il pieno controllo sull'uso delle risorse durante merge di grandi dimensioni.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **Perché:** `Cancellation` ti consente di **annullare l'operazione di merge** automaticamente, evitando attività incontrollate.

### Unione degli indici
**Invoca `index1.merge(index2, mergeOptions)`; l'indice primario assorbe tutti i documenti dall'indice secondario mantenendo l'integrità dei token.** Dopo l'unione, disponi di un repository ricercabile unificato.

```java
index1.merge(index2, options);
```

- **Perché:** Dopo questa chiamata, `index1` contiene tutti i documenti di entrambe le fonti, offrendoti un'esperienza di ricerca unificata.

## Applicazioni pratiche per la gestione documentale Java
- **Legal firms:** Consolidare i fascicoli dei casi da più uffici in un unico indice ricercabile.  
- **Financial institutions:** Unire i report trimestrali in un repository unificato per query di audit rapide.  
- **Enterprises:** Combinare politiche HR, manuali di conformità e guide interne per una ricerca a livello aziendale.

## Considerazioni sulle prestazioni
- **Incremental indexing:** Aggiungi nuovi file periodicamente invece di ricostruire l'intero indice.  
- **Memory monitoring:** Lotti grandi possono consumare RAM; elabora i file in blocchi più piccoli o abilita la modalità streaming.  
- **Garbage collection:** Rilascia prontamente gli oggetti `Index` non utilizzati per liberare risorse.  
- **SSD storage:** Conservare i file di indice su SSD può migliorare la velocità di merge fino a 2×.

## Problemi comuni e soluzioni

| Problema | Soluzione |
|----------|-----------|
| **Percorso della cartella errato** | Verifica il percorso assoluto e assicurati che l'applicazione abbia i permessi di lettura. |
| **Memoria insufficiente** | Aumenta l'heap JVM (`-Xmx`) o indicizza i file in batch. |
| **Annullamento non attivato** | Assicurati che `cancelAfter` sia impostato prima di chiamare `merge`. |
| **Formato file non supportato** | Installa plugin di formato aggiuntivi da GroupDocs se necessario. |

## Domande frequenti

**Q:** *Perché dovrei creare più indici invece di uno solo?*  
**A:** Indici separati ti permettono di isolare domini di dati, applicare politiche di sicurezza distinte e unire solo quando necessario, migliorando prestazioni e organizzazione.

**Q:** *Posso annullare un'operazione di indicizzazione allo stesso modo in cui annullo un merge?*  
**A:** Sì—usa l'oggetto `Cancellation` con il metodo `add` per fermare le operazioni di indicizzazione a lungo termine.

**Q:** *Come garantire prestazioni ottimali con collezioni di documenti molto grandi?*  
**A:** Esegui indicizzazione incrementale, monitora la memoria JVM e conserva l'indice su SSD. Considera l'uso dell'impostazione `BatchSize` per limitare i documenti in memoria.

**Q:** *Cosa devo fare se ricevo errori “Access denied”?*  
**A:** Verifica i permessi della cartella per l'utente che esegue il processo Java e assicurati che il file di licenza sia leggibile.

**Q:** *GroupDocs.Search è compatibile con altre librerie GroupDocs?*  
**A:** Assolutamente—puoi integrarlo con GroupDocs.Viewer, GroupDocs.Conversion e altri per costruire una soluzione documentale full‑stack.

## Conclusione
Seguendo questa guida ora sai come **add documents to index**, configurare il comportamento di merge e **annullare in modo sicuro l'operazione di merge** quando necessario—tutto all'interno di un flusso di lavoro robusto di **java full text search**. Sperimenta con set di dati più grandi, esplora tokenizer personalizzati o combina GroupDocs.Search con altri prodotti GroupDocs per costruire una soluzione di livello enterprise.

**Risorse**
- **Documentazione:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **Riferimento API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **Repository GitHub:** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Forum di supporto gratuito:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Applicazione licenza temporanea:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**Ultimo aggiornamento:** 2026-05-12  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Come aggiungere documenti all'indice con indicizzazione dei metadati in Java usando GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Aggiungere documenti all'indice e disabilitare le stop words in GroupDocs.Search Java per una maggiore precisione di ricerca](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)
- [Aggiungere documenti all'indice – Tutorial GroupDocs.Search Java](/search/java/document-management/)