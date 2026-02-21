---
date: '2026-02-21'
description: Scopri come generare forme singolari e plurali in Java utilizzando l'API
  GroupDocs.Search. Crea un provider personalizzato di forme di parole per una ricerca
  e un'analisi del testo accurate.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Genera forme singolari e plurali in Java con GroupDocs.Search
type: docs
url: /it/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Generare forme singolari/plurali in Java con GroupDocs.Search

Se hai bisogno di **generare forme singolari/plurali in Java**, un provider di forme di parole personalizzato è la chiave per far comprendere al tuo motore di ricerca o di analisi del testo ogni variazione di un termine. In questo tutorial ti guideremo nella creazione di un provider con l'API Java di GroupDocs.Search, così la tua applicazione potrà corrispondere automaticamente a “cat”, “cats”, “city” e “citis” senza sforzo aggiuntivo.

## Risposte Rapide
- **Cosa fa un provider di forme di parole?** Genera forme alternative (singolare, plurale, ecc.) di una parola data in modo che le ricerche possano corrispondere a tutte le varianti.  
- **Quale libreria è necessaria?** GroupDocs.Search per Java (versione 25.4 o successiva).  
- **È necessaria una licenza?** Una prova gratuita è sufficiente per la valutazione; è necessaria una licenza permanente per la produzione.  
- **Quale versione di Java è supportata?** JDK 8 o superiore.  
- **Quante righe di codice sono necessarie?** Circa 30 righe per un'implementazione semplice del provider.

## Cos'è la funzionalità “Create Word Forms Provider”?
Un componente **create word forms provider** è una classe personalizzata che implementa `IWordFormsProvider`. Riceve una parola e restituisce un array di possibili forme — singolare, plurale o altre variazioni linguistiche — basate su regole che definisci. Questo consente all'indice di ricerca di trattare “cat” e “cats” come equivalenti, migliorando il richiamo senza sacrificare la precisione.

## Perché usare GroupDocs.Search per la generazione di forme di parole?
- **Estensibilità integrata:** Inserisci il tuo provider direttamente nella pipeline di indicizzazione.  
- **Ottimizzato per le prestazioni:** Gestisce grandi indici in modo efficiente e puoi memorizzare nella cache i risultati per una velocità aggiuntiva.  
- **Supporto cross‑language:** I concetti si applicano anche a .NET e ad altre piattaforme.

## Prerequisiti
Prima di implementare il **create word forms provider**, assicurati di avere:

- **Maven** installato e un JDK 8 o più recente configurato sulla tua macchina.  
- Familiarità di base con lo sviluppo Java e la configurazione `pom.xml` di Maven.  
- Accesso alla libreria GroupDocs.Search per Java (versione 25.4 o successiva).  

## Configurazione di GroupDocs.Search per Java

### Configurazione Maven

Aggiungi il repository e la dipendenza al tuo file `pom.xml` esattamente come mostrato di seguito:

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

### Download Diretto

In alternativa, scarica l'ultimo JAR dalla pagina ufficiale delle release: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Passaggi per Ottenere la Licenza

1. **Prova gratuita:** Registrati per una prova per esplorare le funzionalità principali.  
2. **Licenza temporanea:** Richiedi una chiave temporanea per test più estesi.  
3. **Acquisto:** Ottieni una licenza commerciale per un uso di produzione senza restrizioni.

### Inizializzazione e Configurazione di Base

Il frammento seguente dimostra come creare un indice — il tuo punto di partenza per aggiungere documenti e logica di forme di parole:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Guida all'Implementazione

Di seguito percorriamo i passaggi per **create word forms provider** che gestisce semplici trasformazioni da singolare a plurale e da plurale a singolare.

### Implementazione di SimpleWordFormsProvider

#### Panoramica
Il nostro provider personalizzato:

- Rimuovere il suffisso finale “es” o “s” per indovinare una forma singolare.  
- Cambiare un finale “y” in “is” per produrre una forma plurale (es., “city” → “citis”).  
- Aggiungere “s” e “es” per generare candidati plurali di base.

#### Passo 1 – Creare lo Scheletro della Classe
Start by defining a class that implements `IWordFormsProvider`. Keep the import statements unchanged:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Passo 2 – Implementare `getWordForms`
Aggiungi il metodo che costruisce l'elenco delle possibili forme. Questo blocco contiene la logica principale; potrai estenderlo in seguito per coprire regole più complesse.

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### Spiegazione della Logica
- **Singolarizzazione:** Rileva i suffissi plurali comuni (`es`, `s`) e li rimuove per approssimare la parola base.  
- **Pluralizzazione:** Gestisce i sostantivi che terminano in `y` sostituendolo con `is`, una regola semplice che funziona per molte parole inglesi.  
- **Aggiunta di suffissi:** Aggiunge `s` e `es` per coprire le forme plurali regolari che potrebbero non essere catturate dai controlli precedenti.

#### Suggerimenti per la Risoluzione dei Problemi
- **Sensibilità al caso:** Il metodo utilizza `toLowerCase()` per il confronto, garantendo che “Cats” e “cats” si comportino allo stesso modo.  
- **Casi limite:** Le parole più corte della lunghezza del suffisso vengono ignorate per evitare di restituire stringhe vuote.  
- **Prestazioni:** Per vocabolari di grandi dimensioni, considera di memorizzare nella cache i risultati in un `ConcurrentHashMap`.

## Applicazioni Pratiche
Implementare un **create word forms provider** può migliorare diversi scenari reali:

1. **Motori di ricerca:** Gli utenti che digitano “mouse” dovrebbero trovare anche i documenti contenenti “mice”. Un provider può generare tali forme irregolari.  
2. **Strumenti di analisi del testo:** L'analisi del sentimento o l'estrazione di entità diventa più affidabile quando tutte le varianti di parole sono riconosciute.  
3. **Sistemi di gestione dei contenuti:** La generazione automatica di tag può includere sinonimi plurali, migliorando SEO e collegamenti interni.

## Considerazioni sulle Prestazioni
Quando integri il provider in un sistema di produzione, tieni presente questi consigli:

- **Cache delle forme usate frequentemente:** Memorizza i risultati in memoria per evitare di ricalcolare la stessa parola più volte.  
- **Monitora l'heap JVM:** Indici di grandi dimensioni possono aumentare la pressione sulla memoria; regola `-Xmx` di conseguenza.  
- **Usa collezioni efficienti:** `ArrayList` funziona per piccoli insiemi, ma per migliaia di forme considera `HashSet` per eliminare rapidamente i duplicati.

**Best Practices**
- Mantieni la libreria aggiornata per beneficiare delle correzioni di prestazioni.  
- Profilare il provider con carichi di query realistici per individuare i colli di bottiglia in anticipo.  

## Conclusione
Ora sai come **generare forme singolari/plurali in Java** usando un `SimpleWordFormsProvider` personalizzato con GroupDocs.Search. Questo componente leggero può migliorare notevolmente la rilevanza dei risultati di ricerca e l'accuratezza dell'analisi linguistica in molte applicazioni.

**Passi successivi:**  
- Sperimenta regole linguistiche più sofisticate (plurali irregolari, stemming).  
- Integra il provider in una pipeline di indicizzazione e misura i miglioramenti del richiamo.  
- Esplora altre funzionalità di GroupDocs.Search come dizionari di sinonimi e analizzatori personalizzati.

**Call to Action:** Prova ad aggiungere il `SimpleWordFormsProvider` al tuo progetto oggi stesso e scopri come arricchisce la tua esperienza di ricerca!

## Sezione FAQ

**1. Cos'è GroupDocs.Search per Java?**  
È una potente libreria che offre ricerca full‑text, indicizzazione e funzionalità linguistiche — inclusa la possibilità di collegare provider di forme di parole personalizzati.

**2. Come funziona SimpleWordFormsProvider?**  
Genera forme alternative applicando semplici regole basate sui suffissi (rimuovendo “s/es”, convertendo “y” in “is” e aggiungendo “s/es”).

**3. Posso personalizzare le regole di generazione delle forme di parole?**  
Assolutamente. Modifica il metodo `getWordForms` per includere forme irregolari, regole specifiche per locale o integrazione con dizionari esterni.

**4. Quali sono alcune applicazioni comuni per questa funzionalità?**  
I motori di ricerca, le pipeline di analisi del testo e le piattaforme CMS beneficiano del riconoscimento delle varianti singolari/plurali.

**5. È necessaria una licenza commerciale per l'uso in produzione?**  
Sì — mentre una prova ti consente di esplorare l'API, una licenza acquistata rimuove i limiti di utilizzo e garantisce supporto.

---

**Ultimo aggiornamento:** 2026-02-21  
**Testato con:** GroupDocs.Search 25.4 (Java)  
**Autore:** GroupDocs