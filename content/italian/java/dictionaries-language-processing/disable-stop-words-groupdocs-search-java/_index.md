---
date: '2026-02-19'
description: Scopri come disabilitare le parole stop nella ricerca e aggiungere documenti
  all'indice con GroupDocs.Search per Java, migliorando la precisione delle query.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 'Parole di arresto nella ricerca: aggiungere documenti all''indice con GroupDocs.Search
  Java'
type: docs
url: /it/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Stop Words nella ricerca: aggiungere documenti all'indice con GroupDocs.Search Java

Se hai bisogno di **add documents to index** assicurandoti che nessun termine importante — soprattutto quelli comuni — venga ignorato, sei nel posto giusto. In questa guida ti mostreremo come **disable stop words in search** usando GroupDocs.Search per Java, così ogni token (anche “on”, “by” o “the”) diventa ricercabile e i risultati saranno molto più accurati.

## Risposte rapide
- **What does “add documents to index” mean?** Significa caricare i tuoi file sorgente in un indice ricercabile in modo che possano essere interrogati in modo efficiente.  
- **Why would I disable stop words?** Per includere parole comuni (ad es., “on”, “the”) nelle ricerche quando tali termini sono significativi per il tuo dominio.  
- **Which library version is required?** GroupDocs.Search for Java 25.4 o successiva.  
- **Do I need a license?** Una prova gratuita è sufficiente per la valutazione; è necessaria una licenza permanente per la produzione.  
- **Can I use this in a Maven project?** Sì – basta aggiungere il repository e la dipendenza mostrati di seguito.

## Cosa sono le stop words nella ricerca e perché potresti volerle disabilitare?
Le stop words sono termini frequenti che molti motori di ricerca filtrano automaticamente per velocizzare le query. Sebbene ciò migliori le prestazioni per ricerche web generiche, può compromettere la precisione in domini specializzati — contratti legali, cataloghi e‑commerce o manuali tecnici — dove parole come “on”, “by” o “as” hanno un reale significato. Disabilitare le stop words ti consente di trattare ogni parola come significativa, garantendo che nessun documento rilevante venga perso.

## Come funziona l'aggiunta di documenti all'indice in GroupDocs.Search?
Quando aggiungi documenti, la libreria legge ogni file, ne tokenizza il contenuto e memorizza i token in una struttura dati ottimizzata (l'indice). Una volta indicizzati, il motore può recuperare i documenti corrispondenti in millisecondi, anche per collezioni di grandi dimensioni.

## Prerequisiti

- **Librerie richieste**: GroupDocs.Search for Java 25.4 (or newer).  
- **Ambiente di sviluppo**: IntelliJ IDEA, Eclipse o qualsiasi IDE Java tu preferisca.  
- **Conoscenze di base**: Familiarità con la sintassi Java e il concetto di indicizzazione.

## Configurazione di GroupDocs.Search per Java

### Installazione con Maven

Se stai usando Maven, includi quanto segue nel tuo `pom.xml`:

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

In alternativa, scarica l'ultima versione da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Passaggi per l'acquisizione della licenza
- **Free Trial** – inizia a testare subito.  
- **Temporary License** – ottieni una chiave a tempo limitato per la piena funzionalità.  
- **Purchase** – assicurati una licenza permanente per l'uso in produzione.

## Inizializzazione e configurazione di base

Crea un'istanza di `IndexSettings` per controllare il comportamento dell'indice:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Come disabilitare le stop words nella ricerca (Java)

La riga seguente disattiva il filtro di stop‑word integrato:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Parametri*: `setUseStopWords` accetta un valore booleano.  
*Scopo*: Garantisce che ogni parola — incluse le stop words comuni — sia indicizzata e ricercabile.

## Come aggiungere documenti all'indice

### Definizione della directory di output

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Specifica della directory dei documenti

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Ora ogni file in `YOUR_DOCUMENT_DIRECTORY` è **added documents to index** e pronto per le query.

## Esecuzione di una query di ricerca

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Poiché le stop words sono disabilitate, il termine `"on"` verrà considerato durante la ricerca, restituendo corrispondenze che altrimenti verrebbero ignorate.

## Applicazioni pratiche

1. **Enterprise Document Search** – Assicurati che la terminologia critica non venga filtrata.  
2. **E‑commerce Platforms** – Migliora la scoperta dei prodotti indicizzando ogni parola nelle descrizioni dei prodotti.  
3. **Legal Research Tools** – Cattura ogni termine legale, anche quelli comunemente trattati come stop words.

## Considerazioni sulle prestazioni

- **Optimization Tips**: Aggiorna e pota regolarmente il tuo indice per mantenere alta la velocità di ricerca.  
- **Resource Usage**: Monitora la dimensione dell'heap JVM; indici di grandi dimensioni potrebbero richiedere la messa a punto delle impostazioni di garbage collection.  
- **Java Memory Management**: Usa strutture dati efficienti e considera lo storage off‑heap per corpora molto grandi.

## Problemi comuni e soluzioni

| Sintomo | Causa probabile | Soluzione |
|---|---|---|
| Nessun risultato per parole comuni | `setUseStopWords(true)` (default) | Chiama `setUseStopWords(false)` come mostrato sopra. |
| Errori out‑of‑memory durante l'indicizzazione | Indicizzare troppi file di grandi dimensioni contemporaneamente | Indicizza i file in batch; aumenta l'opzione JVM `-Xmx`. |
| La ricerca restituisce dati obsoleti | Indice non aggiornato dopo l'aggiunta di nuovi file | Chiama `index.update()` o ri‑aggiungi i documenti modificati. |

## Domande frequenti

**Q: What are stop words?**  
A: Le stop words sono termini comuni (ad es., “the”, “is”, “on”) che molti motori di ricerca ignorano per velocizzare le query. Disabilitarle ti consente di trattare ogni token come ricercabile.

**Q: Why disable stop words in search indexes?**  
A: Quando è necessario un matching preciso di frasi — ad esempio in documenti legali o tecnici — ogni parola ha un significato, quindi è necessario includere le stop words.

**Q: How does GroupDocs.Search handle large datasets?**  
A: La libreria utilizza strutture dati ottimizzate e indicizzazione incrementale per mantenere basso l'uso di memoria, anche con milioni di documenti.

**Q: Can I integrate GroupDocs.Search with other Java applications?**  
A: Sì — l'API è progettata per un facile embedding in qualsiasi sistema basato su Java, dai servizi web alle applicazioni desktop.

**Q: What should I do if my search results are not accurate?**  
A: Verifica che l'indice includa tutti i documenti necessari (**add documents to index**), assicurati che il filtro di stop‑word sia disabilitato se necessario, e considera di ricostruire l'indice dopo modifiche importanti.

## Risorse aggiuntive

- **Documentazione**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **Riferimento API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- **Repository GitHub**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Supporto gratuito**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licenza temporanea**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Seguendo questa guida, ora sai come **add documents to index** e **disable stop words in search** per fornire risultati più accurati nelle tue applicazioni Java.

---

**Last Updated:** 2026-02-19  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs