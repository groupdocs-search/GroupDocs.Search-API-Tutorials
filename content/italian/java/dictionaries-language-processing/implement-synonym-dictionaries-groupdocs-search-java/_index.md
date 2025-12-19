---
date: '2025-12-19'
description: Scopri come aggiungere sinonimi, cercare con i sinonimi e gestire i gruppi
  di sinonimi in Java usando GroupDocs.Search. Migliora le prestazioni e l'affidabilità
  del tuo indice di ricerca.
keywords:
- synonym dictionaries java
- groupdocs.search synonym implementation
- java search functionality enhancement
title: Come aggiungere sinonimi in Java usando GroupDocs.Search – Guida completa
type: docs
url: /it/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

# Come aggiungere sinonimi in Java usando GroupDocs.Search

Benvenuti alla nostra guida completa su **come aggiungere sinonimi** in Java con GroupDocs.Search. Che tu stia costruendo un CMS ricco di contenuti, un catalogo e‑commerce o un repository di documenti, abilitare il supporto ai sinonimi può migliorare drasticamente la reperibilità dei tuoi dati. In questo tutorial imparerai a creare e gestire dizionari di sinonimi, importare file di dizionari di sinonimi e ottimizzare il tuo indice di ricerca per risultati rapidi e accurati.

## Risposte rapide
- **Qual è il passaggio principale per aggiungere sinonimi?** Inizializzare un `Index` e utilizzare l'API `SynonymDictionary`.  
- **Posso importare un dizionario di sinonimi?** Sì – usa `importDictionary(path)` per caricare un file pre‑costruito.  
- **Come abilito la ricerca con i sinonimi?** Imposta `SearchOptions.setUseSynonymSearch(true)`.  
- **È possibile gestire gruppi di sinonimi?** Assolutamente – è possibile cancellare, aggiungere o recuperare gruppi tramite l'API del dizionario.  
- **Cosa devo considerare quando ottimizzo l'indice di ricerca?** Rimuovere regolarmente le voci inutilizzate e ottimizzare l'heap JVM per grandi set di dati.  

## Che cosa significa “Come aggiungere sinonimi”?
Aggiungere sinonimi significa definire parole o frasi alternative che il motore di ricerca tratta come equivalenti. Questo consente a una query come **“better”** di corrispondere anche a documenti contenenti **“improve”**, **“enhance”** o **“upgrade”**.

## Perché usare il supporto ai sinonimi in GroupDocs.Search?
- **Esperienza utente migliorata:** Gli utenti trovano contenuti pertinenti anche se usano una terminologia diversa.  
- **Tassi di conversione più alti:** I siti e‑commerce catturano più vendite abbinando query di prodotto diverse.  
- **Manutenzione ridotta:** Un unico dizionario può servire più applicazioni, semplificando gli aggiornamenti.  

## Prerequisiti
- **GroupDocs.Search for Java** versione 25.4 o successiva.  
- Un IDE Java (IntelliJ IDEA, Eclipse, ecc.) con supporto Maven.  
- Conoscenze di base di Java e familiarità con la struttura di progetto Maven.

### Librerie richieste e versioni
- GroupDocs.Search for Java versione 25.4 o superiore.

### Configurazione dell'ambiente
- IDE a tua scelta (IntelliJ IDEA, Eclipse, ecc.).  
- Maven per la gestione delle dipendenze.

### Requisiti di conoscenza
- Programmazione orientata agli oggetti in Java.  
- Operazioni di base I/O su file.

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

**Download diretto** – è anche possibile scaricare l'ultimo JAR da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
- **Prova gratuita:** Prova le funzionalità principali senza licenza.  
- **Licenza temporanea:** Estendi le capacità della prova durante la valutazione.  
- **Acquisto:** Necessario per l'uso in produzione e per l'intero set di funzionalità.

#### Inizializzazione e configurazione di base
Crea un'istanza di `Index`, quindi aggiungi i documenti da indicizzare:

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
Creare un indice è la base. Di seguito percorriamo i passaggi essenziali, ciascuno accompagnato dal codice esatto di cui hai bisogno.

### Funzione 1: Creare e indicizzare un indice
```java
// Create an index in the specified folder
Index index = new Index(indexFolder);

// Add documents from the given folder to the index
index.add(documentsFolder);
```

### Funzione 2: Recuperare sinonimi per una parola
```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### Funzione 3: Recuperare gruppi di sinonimi
```java
String[][] synonymGroups = index.getDictionaries().getSynonymDictionary().getSynonymGroups("make");
```

### Funzione 4: Gestire le voci del dizionario di sinonimi
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

### Funzione 5: Esportare i sinonimi in un file
```java
String exportFilePath = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.getDictionaries().getSynonymDictionary().exportDictionary(exportFilePath);
```

### Funzione 6: Importare i sinonimi da un file
```java
index.getDictionaries().getSynonymDictionary().importDictionary(exportFilePath);
```

### Funzione 7: Eseguire la ricerca con supporto ai sinonimi
```java
String query = "better";
SearchOptions options = new SearchOptions();
options.setUseSynonymSearch(true);

SearchResult result = index.search(query, options);
```

## Come cercare con i sinonimi
Abilitando `setUseSynonymSearch(true)`, il motore espande automaticamente la query utilizzando il dizionario di sinonimi che hai creato o importato. Questo passaggio è fondamentale per fornire risultati più ricchi senza modificare il comportamento di ricerca dell'utente.

## Come importare il dizionario di sinonimi
Se disponi già di un file `.dat` preparato in un altro ambiente, chiama semplicemente `importDictionary(path)`. È l'ideale per sincronizzare i dizionari tra server di sviluppo, staging e produzione.

## Come gestire i gruppi di sinonimi
I gruppi di sinonimi ti permettono di trattare un insieme di termini come un'unica entità logica. Aggiungere, cancellare o recuperare gruppi avviene tramite l'API `SynonymDictionary`, come mostrato negli snippet di codice sopra.

## Come ottimizzare l'indice di ricerca
- **Rimuovere regolarmente le voci inutilizzate:** Usa `clear()` prima di aggiornamenti massivi.  
- **Regolare l'heap JVM:** Dizionari grandi possono richiedere più memoria.  
- **Mantenere la libreria aggiornata:** Le nuove versioni contengono miglioramenti delle prestazioni.

## Applicazioni pratiche
1. **Sistemi di gestione dei contenuti (CMS):** Gli utenti trovano articoli anche quando usano una terminologia alternativa.  
2. **Piattaforme e‑commerce:** Le ricerche di prodotto diventano tolleranti ai sinonimi come “laptop” vs. “notebook”.  
3. **Repository di documenti:** Archivi legali o medici beneficiano di gruppi di sinonimi specifici del dominio.

## Considerazioni sulle prestazioni
- **Ottimizzare l'archiviazione dell'indice:** Ricostruisci periodicamente l'indice per rimuovere dati obsoleti.  
- **Gestire l'uso della memoria:** Monitora il consumo dell'heap durante il caricamento di grandi file di sinonimi.  
- **Aggiornamenti regolari:** Rimani sulla versione più recente di GroupDocs.Search per correzioni di bug e miglioramenti di velocità.

## Conclusione
Ora disponi di una roadmap completa, passo‑per‑passo, per **come aggiungere sinonimi**, importare file di dizionari di sinonimi, gestire gruppi di sinonimi e **cercare con i sinonimi** usando GroupDocs.Search per Java. Applica queste tecniche per aumentare la pertinenza, migliorare la soddisfazione degli utenti e mantenere il tuo indice di ricerca al massimo delle prestazioni.

## Domande frequenti

**Q: Qual è il requisito di sistema minimo per usare GroupDocs.Search?**  
A: Qualsiasi OS moderno con un JDK compatibile (Java 8 o superiore) è sufficiente.

**Q: Quanto spesso dovrei aggiornare il mio dizionario di sinonimi?**  
A: Aggiornalo ogni volta che emergono nuove terminologie — usa `clear()` seguito da `addRange()` per un refresh pulito.

**Q: Posso eseguire GroupDocs.Search senza acquistare una licenza?**  
A: Una prova gratuita funziona per la valutazione, ma è necessaria una licenza per le distribuzioni in produzione.

**Q: Quali sono le migliori pratiche per indicizzare grandi set di dati?**  
A: Suddividi i dati in batch logici, monitora l'uso dell'heap e programma manutenzioni regolari dell'indice.

**Q: Non vedo corrispondenze di sinonimi previste — cosa dovrei controllare?**  
A: Verifica che il dizionario sia stato importato correttamente, che `setUseSynonymSearch(true)` sia attivo e che i termini siano presenti nei gruppi di sinonimi.

---

**Last Updated:** 2025-12-19  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

**Risorse**  
- [Documentazione](https://docs.groupdocs.com/search/java/)  
- [Riferimento API](https://reference.groupdocs.com/search/java)  
- [Scarica GroupDocs.Search per Java](https://releases.groupdocs.com/search/java/)  
- [Repository GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/search/10)  
- [Acquisizione licenza temporanea](https://purchase.groupdocs.com/temporary-license/)