---
date: '2026-03-04'
description: Scopri come cercare con sinonimi in Java usando GroupDocs.Search, importa
  dizionari di sinonimi, gestisci gruppi di sinonimi e ottimizza il tuo indice di
  ricerca per ottenere risultati migliori.
keywords:
- synonym dictionaries java
- groupdocs.search synonym implementation
- java search functionality enhancement
title: Come cercare con sinonimi in Java usando GroupDocs.Search – Guida completa
type: docs
url: /it/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

# Come eseguire la ricerca con sinonimi in Java usando GroupDocs.Search

Se vuoi che i tuoi utenti trovino il contenuto giusto anche quando digitano parole diverse, **la ricerca con sinonimi** è la risposta. In questa guida esamineremo tutto ciò che devi sapere — creare un dizionario di sinonimi, importarlo/esportarlo, gestire i gruppi di sinonimi e, infine, eseguire una ricerca che espande automaticamente le query usando quei sinonimi. Che tu stia costruendo un CMS, un catalogo e‑commerce o un archivio di documenti legali, aggiungere il supporto ai sinonimi può aumentare drasticamente la pertinenza e i tassi di conversione.

## Risposte rapide
- **Qual è il passaggio principale per aggiungere sinonimi?** Inizializza un `Index` e utilizza l'API `SynonymDictionary`.  
- **Posso importare un dizionario di sinonimi?** Sì – usa `importDictionary(path)` per caricare un file pre‑costruito.  
- **Come abilito la ricerca con sinonimi?** Imposta `SearchOptions.setUseSynonymSearch(true)`.  
- **È possibile gestire i gruppi di sinonimi?** Assolutamente – puoi cancellare, aggiungere o recuperare gruppi tramite l'API del dizionario.  
- **Cosa devo considerare quando ottimizzo l'indice di ricerca?** Rimuovi regolarmente le voci inutilizzate e ottimizza l'heap JVM per grandi set di dati.  

## Cos'è la ricerca con sinonimi?
“Ricerca con sinonimi” significa che il motore tratta un insieme di parole o frasi come intercambiabili. Quando un utente digita **“better”**, il motore cerca anche **“improve”**, **“enhance”**, o qualsiasi altro termine che hai definito nello stesso gruppo di sinonimi, fornendo risultati più ricchi senza modificare la query dell'utente.

## Perché abilitare il supporto ai sinonimi in GroupDocs.Search?
- **Migliore esperienza utente:** I visitatori trovano documenti pertinenti anche se usano terminologia diversa.  
- **Tassi di conversione più alti:** Le piattaforme e‑commerce catturano più vendite abbinando termini di prodotto vari.  
- **Manutenzione semplificata:** Un unico dizionario centrale può servire più applicazioni, rendendo gli aggiornamenti indolori.  

## Prerequisiti
- GroupDocs.Search per Java versione 25.4 o più recente.  
- Un IDE Java (IntelliJ IDEA, Eclipse, ecc.) con supporto Maven.  
- Conoscenze di base di Java e familiarità con la struttura di progetto Maven.

### Librerie richieste e versioni
- GroupDocs.Search per Java versione 25.4 o superiore.

### Configurazione dell'ambiente
- IDE a tua scelta (IntelliJ IDEA, Eclipse, ecc.).  
- Maven per la gestione delle dipendenze.

### Requisiti di conoscenza
- Programmazione orientata agli oggetti in Java.  
- Operazioni di base I/O su file.

## Configurazione di GroupDocs.Search per Java

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

**Download diretto** – puoi anche scaricare l'ultimo JAR da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
- **Prova gratuita:** Prova le funzionalità principali senza licenza.  
- **Licenza temporanea:** Estendi le capacità della prova durante la valutazione.  
- **Acquisto:** Richiesto per l'uso in produzione e per l'intero set di funzionalità.

#### Inizializzazione e configurazione di base
Crea un'istanza `Index`, quindi aggiungi i documenti da indicizzare:

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

### Funzione 2: Recuperare i sinonimi per una parola
```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### Funzione 3: Recuperare i gruppi di sinonimi
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

## Come eseguire la ricerca con sinonimi
Abilitando `setUseSynonymSearch(true)`, il motore espande automaticamente la query usando il dizionario di sinonimi che hai creato o importato. Questo passaggio è fondamentale per fornire risultati più ricchi senza modificare il comportamento di ricerca dell'utente.

## Come importare il dizionario di sinonimi
Se hai già un file `.dat` preparato da un altro ambiente, chiama semplicemente `importDictionary(path)`. Questo è ideale per sincronizzare i dizionari tra server di sviluppo, staging e produzione.

## Come gestire i gruppi di sinonimi
I gruppi di sinonimi ti permettono di trattare un insieme di termini come una singola entità logica. Aggiungere, cancellare o recuperare gruppi avviene tramite l'API `SynonymDictionary`, come mostrato nei frammenti di codice sopra.

## Come ottimizzare l'indice di ricerca
- **Rimuovi regolarmente le voci inutilizzate:** Usa `clear()` prima di aggiornamenti massivi.  
- **Regola l'heap JVM:** I dizionari grandi possono richiedere più memoria.  
- **Mantieni la libreria aggiornata:** Le nuove versioni contengono miglioramenti delle prestazioni.

## Applicazioni pratiche
1. **Sistemi di gestione dei contenuti (CMS):** Gli utenti trovano articoli anche quando usano terminologia alternativa.  
2. **Piattaforme e‑commerce:** Le ricerche di prodotto diventano tolleranti ai sinonimi come “laptop” vs. “notebook”.  
3. **Repository di documenti:** Gli archivi legali o medici beneficiano di gruppi di sinonimi specifici per dominio.

## Considerazioni sulle prestazioni
- **Ottimizza l'archiviazione dell'indice:** Ricostruisci periodicamente l'indice per rimuovere dati obsoleti.  
- **Gestisci l'uso della memoria:** Monitora il consumo dell'heap quando carichi file di sinonimi di grandi dimensioni.  
- **Aggiornamenti regolari:** Rimani sulla versione più recente di GroupDocs.Search per correzioni di bug e miglioramenti di velocità.

## Problemi comuni e soluzioni
| Problema | Probabile causa | Soluzione |
|----------|-----------------|----------|
| Nessuna corrispondenza di sinonimi appare | `setUseSynonymSearch(true)` non impostato o dizionario non importato | Verifica che l'opzione sia abilitata e che il file del dizionario esista. |
| Errori out‑of‑memory durante l'importazione | File `.dat` molto grande supera l'heap JVM | Aumenta la dimensione dell'heap `-Xmx` o importa in batch più piccoli. |
| Voci duplicate nei risultati | Lo stesso termine appare in più gruppi di sinonimi | Consolidare i gruppi sovrapposti usando `clear()` poi `addRange()`. |

## Domande frequenti

**Q: Qual è il requisito di sistema minimo per utilizzare GroupDocs.Search?**  
**A:** Qualsiasi OS moderno con un JDK compatibile (Java 8 o più recente) è sufficiente.

**Q: Quanto spesso dovrei aggiornare il mio dizionario di sinonimi?**  
**A:** Aggiornalo ogni volta che emergono nuovi termini — usa `clear()` seguito da `addRange()` per un refresh pulito.

**Q: Posso eseguire GroupDocs.Search senza acquistare una licenza?**  
**A:** Una prova gratuita funziona per la valutazione, ma è necessaria una licenza per le distribuzioni in produzione.

**Q: Quali sono le migliori pratiche per indicizzare grandi set di dati?**  
**A:** Suddividi i dati in batch logici, monitora l'uso dell'heap e pianifica una manutenzione regolare dell'indice.

**Q: Non vedo le corrispondenze di sinonimi previste — cosa dovrei controllare?**  
**A:** Verifica che il dizionario sia stato importato correttamente, che `setUseSynonymSearch(true)` sia attivo e che i termini siano presenti nei gruppi di sinonimi.

**Risorse**  
- [Documentation](https://docs.groupdocs.com/search/java/)  
- [API Reference](https://reference.groupdocs.com/search/java)  
- [Download GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)  
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license/) 

---

**Ultimo aggiornamento:** 2026-03-04  
**Testato con:** GroupDocs.Search 25.4 per Java  
**Autore:** GroupDocs