---
date: '2026-01-03'
description: Scopri come aggiungere documenti all'indice e annullare l'operazione
  di merge in Java usando GroupDocs.Search. Una guida completa per la gestione dei
  documenti in Java.
keywords:
- document indexing in Java
- merging documents with GroupDocs
- GroupDocs.Search Java tutorial
title: Aggiungi documenti all'indice e unisci in Java usando GroupDocs.Search
type: docs
url: /it/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# Aggiungere documenti all'indice e unire in Java usando GroupDocs.Search

Nell'odierno ambiente digitale frenetico, apprendere **come aggiungere documenti all'indice** in modo efficiente è essenziale per qualsiasi soluzione di **document management java**. Che tu stia gestendo contratti, fatture o report interni, un indice ben strutturato ti consente di recuperare informazioni in millisecondi. Questo tutorial ti guida nella creazione di indici, nell'aggiunta di documenti, nella configurazione delle opzioni di merge e persino nella **cancellazione dell'operazione di merge** se necessario—tutto con GroupDocs.Search per Java.

## Risposte rapide
- **Cosa significa “add documents to index”?** Indica a GroupDocs.Search di scansionare una cartella e memorizzare i metadati ricercabili per ogni file.  
- **Posso interrompere un merge lungo?** Sì—usa l'oggetto `Cancellation` per **cancel merge operation** dopo un timeout.  
- **Ho bisogno di una licenza?** Una licenza di prova gratuita o temporanea funziona per i test; una licenza commerciale sblocca tutte le funzionalità.  
- **Quale versione di Java è richiesta?** JDK 8 o successivo.  
- **È adatto a grandi set di dati?** Assolutamente—basta monitorare la memoria e utilizzare l'indicizzazione incrementale.  

## Cos'è “add documents to index” in GroupDocs.Search?
Aggiungere documenti a un indice significa fornire una collezione di file a GroupDocs.Search affinché la libreria possa analizzarne il contenuto, estrarre i token e costruire una struttura dati ricercabile. Una volta indicizzati, è possibile eseguire ricerche full‑text rapide su tutti i document.

## Perché usare GroupDocs.Search per document management java?
- **Indicizzazione scalabile** – Gestisce migliaia di file senza degradare le prestazioni.  
- **API ricca** – Offre un controllo fine sull'indicizzazione, l'unione e la cancellazione.  
- **Supporto multi‑formato** – Funziona con PDF, Word, Excel e molti altri formati subito pronto all'uso.  

## Prerequisiti
- **GroupDocs.Search Java** versione 25.4 o successiva.  
- Maven (o download manuale del JAR).  
- Conoscenza di base di Java e un ambiente JDK 8+.  

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
- **Commercial License:** Acquista per l'uso in produzione.  

Dopo aver ottenuto il file di licenza, posizionalo nel tuo progetto e inizializza la libreria come mostrato più avanti.

## Guida all'implementazione

### Come aggiungere documenti all'indice – Creare il primo indice
Per prima cosa, crea un indice vuoto che conterrà i tuoi dati ricercabili.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **Perché:** Questo passaggio crea un contenitore di storage dove verranno salvati i token indicizzati.

#### Aggiungere documenti all'indice
Ora indica a GroupDocs.Search di scansionare una cartella e **add documents to index**.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **Perché:** La libreria legge ogni file, estrae il testo e lo memorizza in `index1`.

### Creare un secondo indice per flussi di lavoro flessibili
A volte sono necessari indici separati—ad esempio, per isolare i dati di un cliente.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Perché:** Indici multipli ti permettono di gestire set di documenti distinti e combinarli successivamente.

### Come configurare le opzioni di merge e cancellare l'operazione di merge
Prima di unire, puoi affinare il processo e persino interromperlo se dura troppo.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **Perché:** `Cancellation` ti dà il controllo per **cancel merge operation** automaticamente, evitando attività incontrollate.

### Unire gli indici
Infine, unisci l'indice secondario a quello primario.

```java
index1.merge(index2, options);
```

- **Perché:** Dopo questa chiamata, `index1` contiene tutti i documenti di entrambe le fonti, offrendoti un'esperienza di ricerca unificata.

## Applicazioni pratiche per Document Management Java
- **Studi legali:** Consolidare i fascicoli dei casi da più uffici.  
- **Istituzioni finanziarie:** Unire i report trimestrali in un unico repository ricercabile.  
- **Aziende:** Combinare documenti HR, di conformità e di policy per una ricerca a livello aziendale.

## Considerazioni sulle prestazioni
- **Indicizzazione incrementale:** Aggiungere nuovi file periodicamente invece di ricostruire l'intero indice.  
- **Monitoraggio della memoria:** Lotti grandi possono consumare RAM; considera di processare in blocchi più piccoli.  
- **Garbage collection:** Rilascia prontamente gli oggetti `Index` non più utilizzati per liberare risorse.

## Problemi comuni e soluzioni

| Problema | Soluzione |
|----------|-----------|
| **Percorso cartella errato** | Verifica il percorso assoluto e assicurati che l'applicazione abbia i permessi di lettura. |
| **Memoria insufficiente** | Aumenta l'heap JVM (`-Xmx`) o indicizza i file in batch. |
| **Cancellazione non avviata** | Assicurati che `cancelAfter` sia impostato prima di chiamare `merge`. |
| **Formato file non supportato** | Installa plugin di formato aggiuntivi da GroupDocs se necessario. |

## Domande frequenti

**Q:** *Perché dovrei creare più indici invece di uno solo?*  
A: Gli indici separati ti permettono di isolare domini di dati, applicare diverse politiche di sicurezza e unire solo quando necessario, migliorando prestazioni e organizzazione.

**Q:** *Posso annullare un'operazione di indicizzazione allo stesso modo in cui annullo un merge?*  
A: Sì—usa l'oggetto `Cancellation` con il metodo `add` per fermare le attività di indicizzazione a lungo termine.

**Q:** *Come garantisco prestazioni ottimali con collezioni di documenti molto grandi?*  
A: Esegui indicizzazione incrementale, monitora la memoria JVM e considera l'uso di storage SSD per la directory dell'indice.

**Q:** *Cosa devo fare se ricevo errori “Access denied”?*  
A: Controlla i permessi della cartella per l'utente che esegue il processo Java e assicurati che il file di licenza sia leggibile.

**Q:** *GroupDocs.Search è compatibile con altre librerie GroupDocs?*  
A: Assolutamente—puoi integrarlo con GroupDocs.Viewer, GroupDocs.Conversion, ecc., per una soluzione documentale completa.

## Conclusione
Seguendo questa guida ora sai come **add documents to index**, configurare il comportamento del merge e annullare in modo sicuro **cancel merge operation** quando necessario—tutto all'interno di un flusso di lavoro robusto di **document management java**. Sperimenta con set di dati più grandi, esplora tokenizzatori personalizzati o combina GroupDocs.Search con altri prodotti GroupDocs per costruire una soluzione davvero di livello enterprise.

**Risorse**
- **Documentazione:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Forum di supporto gratuito:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Applicazione licenza temporanea:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2026-01-03  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs  
