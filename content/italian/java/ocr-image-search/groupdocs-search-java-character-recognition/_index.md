---
date: '2026-11-02'
description: Crea un indice di ricerca personalizzato in java usando GroupDocs.Search
  per gestire caratteri regolari e misti, ottimizzare la ricerca di immagini OCR e
  migliorare il recupero dei numeri di causa legale.
keywords:
- custom search index java
- GroupDocs.Search Java
- character recognition java
- OCR search Java
- search library Java
lastmod: '2026-11-02'
og_description: Crea un indice di ricerca personalizzato in java usando GroupDocs.Search
  per gestire caratteri regolari e misti, ottimizzare la ricerca di immagini OCR e
  migliorare il recupero dei numeri di causa legale.
og_image_alt: Guide showing custom search index creation in Java with GroupDocs.Search
og_title: Crea un indice di ricerca personalizzato in java con GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Create a custom search index java using GroupDocs.Search to handle
    regular and blended characters, optimize OCR image search, and improve legal case
    number retrieval.
  headline: Create a custom search index java with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It means configuring an index to treat specific symbols as letters or
      blended characters, rather than ignoring them.
    question: What does “create custom search index” mean?
  - answer: GroupDocs.Search for Java (v25.4 at the time of writing).
    question: Which library is used?
  - answer: A free trial works for development; a paid license is required for production.
    question: Do I need a license?
  - answer: Yes—GroupDocs.Search supports OCR on images and PDFs when properly configured.
    question: Can I index both PDFs and images?
  - answer: Maven is the recommended way to manage dependencies, but you can also
      use Gradle or manual JARs.
    question: Is Maven required?
  type: FAQPage
tags:
- custom search index
- GroupDocs.Search
- Java OCR
- character recognition
- search library
title: Crea un indice di ricerca personalizzato in java con GroupDocs.Search
type: docs
url: /it/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Crea un indice di ricerca personalizzato java con GroupDocs.Search

Nelle moderne applicazioni con molti documenti, creare un **custom search index java** che rispetti le sfumature del tuo testo — come trattini, underscore o simboli specifici della lingua — è essenziale per un recupero veloce e preciso. Questo tutorial ti guida nella configurazione del riconoscimento dei caratteri in **GroupDocs.Search for Java**, coprendo sia i caratteri regolari (lettere, cifre, underscore) sia i caratteri misti (ad es., trattini). Alla fine, sarai in grado di personalizzare un indice che soddisfi le esigenze precise di scenari OCR o di ricerca di immagini, sia che tu stia indicizzando numeri di casi legali, repository di codice sorgente o PDF multilingue.

## Risposte rapide
- **Che cosa significa “create custom search index”?** Significa configurare un indice per trattare simboli specifici come lettere o caratteri misti, invece di ignorarli.  
- **Quale libreria viene utilizzata?** GroupDocs.Search for Java (v25.4 al momento della stesura).  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per lo sviluppo; è necessaria una licenza a pagamento per la produzione.  
- **Posso indicizzare sia PDF che immagini?** Sì — GroupDocs.Search supporta l'OCR su immagini e PDF quando configurato correttamente.  
- **È necessario Maven?** Maven è il metodo consigliato per gestire le dipendenze, ma è possibile utilizzare anche Gradle o JAR manuali.  

## Cos'è un custom search index java?
Il **custom search index java** è una struttura dati ricercabile che puoi modellare definendo quali caratteri sono trattati come lettere, cifre o simboli misti. Per impostazione predefinita, molti simboli vengono ignorati, il che può causare mancati risultati per identificatori come numeri di caso (`2023-AB-456`) o frammenti di codice (`my_variable`). Regolare il dizionario dell'alfabeto ti dà il pieno controllo sulla tokenizzazione, portando a una maggiore rilevanza e a un'esecuzione più rapida delle query.

## Perché configurare caratteri regolari e misti per i numeri di casi legali?
Trattare i trattini e le barre oblique come caratteri misti mantiene i token correlati insieme, evitando la divisione indesiderata di identificatori come numeri di caso, codici prodotto o percorsi di file. Questa configurazione **ottimizza le prestazioni dell'indice di ricerca** riducendo la frammentazione dei token e migliora la rilevanza per i contenuti generati da OCR, specialmente quando si gestiscono documenti legali che dipendono fortemente da identificatori strutturati.

## Prerequisiti
- **JDK 8** o versioni successive installate.  
- **Maven** per la gestione delle dipendenze.  
- Accesso alla libreria **GroupDocs.Search for Java** (scaricata tramite Maven o dal sito ufficiale).  

### Librerie e dipendenze richieste
Aggiungi le voci del repository e delle dipendenze al tuo `pom.xml` (come mostrato di seguito). Il blocco XML deve rimanere invariato.

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

Puoi anche scaricare gli ultimi JAR da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
- **Prova gratuita** – perfetta per le prime sperimentazioni.  
- **Licenza temporanea** – utile per cicli di sviluppo più lunghi.  
- **Licenza di produzione** – necessaria per il dispiegamento commerciale.  

Ottieni una licenza dal portale ufficiale: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Inizializzazione di base
Il frammento di codice qui sotto mostra il codice minimo necessario per avviare un indice vuoto. La classe `Index` è il componente centrale che memorizza e gestisce i dati ricercabili. Mantienila così com'è; la utilizzeremo più avanti.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Configurazione di GroupDocs.Search per Java

### Installazione tramite Maven
La configurazione Maven dalla sezione *Prerequisiti* è tutto ciò di cui hai bisogno. Dopo averla aggiunta, esegui `mvn clean install` per scaricare i binari.

### Requisiti di configurazione dell'ambiente
- Assicurati che la **cartella dell'indice** e la **cartella dei documenti** esistano su disco.  
- Usa percorsi assoluti o configura il tuo IDE per risolvere correttamente i percorsi relativi.  

## Guida all'implementazione

Di seguito esaminiamo due funzionalità distinte: **caratteri regolari** e **caratteri misti**. Ogni funzionalità segue lo stesso schema — definire i percorsi, creare l'indice, impostare il dizionario dei caratteri e infine indicizzare i documenti.

### Funzione 1 – caratteri regolari

#### Panoramica
I caratteri regolari sono trattati come token indipendenti. Questo è ideale quando si desidera che cifre, lettere e underscore siano ricercabili esattamente come appaiono.

#### Implementazione passo‑passo

**1️⃣ Configura i percorsi**  
Definisci dove verrà memorizzato l'indice e dove si trovano i documenti sorgente.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Crea e configura l'indice**  
Istanzia l'indice e cancella qualsiasi configurazione dell'alfabeto preesistente.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Definisci i caratteri regolari**  
Crea un array di caratteri che includa cifre, lettere latine e l'underscore.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Indicizza i documenti**  
Aggiungi tutti i file dalla cartella sorgente al nuovo indice configurato.

```java
index.add(documentFolder);
```

### Funzione 2 – caratteri misti

#### Panoramica
I caratteri misti (come i trattini) collegano spesso due parole. Segnarli come *misti* indica al motore di mantenere insieme i token circostanti durante l'indicizzazione.

#### Implementazione passo‑passo

**1️⃣ Configura i percorsi**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Crea e configura l'indice**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Definisci i caratteri misti**  
Qui indichiamo al dizionario che il trattino deve essere trattato come carattere misto.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Indicizza i documenti**  

```java
index.add(documentFolder);
```

## Applicazioni pratiche

### Caso d'uso 1 – gestione di documenti legali
I file legali spesso contengono numeri di caso come `2023-AB-456`. Configurando underscore e trattini, le ricerche restituiscono corrispondenze esatte senza dividere l'identificatore, aiutandoti a **cercare numeri di casi legali** in modo efficiente.

### Caso d'uso 2 – repository di codice sorgente
Gli sviluppatori hanno bisogno di cercare frammenti di codice dove underscore (`my_variable`) e trattini (`my-function`) sono significativi. Il riconoscimento personalizzato dei caratteri garantisce che il motore di ricerca rispetti questi simboli.

### Caso d'uso 3 – set di dati multilingue
Quando si lavora con lingue che utilizzano alfabeti aggiuntivi, è possibile **estendere il set di caratteri Unicode** per includere tali intervalli, garantendo risultati di ricerca accurati tra più lingue.

### Caso d'uso 4 – indicizzare immagini PDF
Se stai indicizzando PDF scansionati o file immagine, l'output OCR contiene spesso caratteri misti. Configurare correttamente i caratteri regolari e misti **ottimizza le prestazioni dell'indice di ricerca** per contenuti basati su immagini.

## Considerazioni sulle prestazioni

- **Gestione delle risorse** – monitora l'uso dell'heap; gli indici di grandi dimensioni beneficiano di commit incrementali.  
- **Garbage collection** – rilascia gli oggetti `Index` al termine per consentire alla JVM di recuperare memoria.  
- **Ottimizzazione dell'indice** – chiama periodicamente `index.optimize()` (se disponibile) per compattare l'indice e migliorare la velocità delle query.  

## Conclusione

Ora sai **come creare un custom search index java** che distingue tra caratteri regolari e misti usando GroupDocs.Search per Java. Questo controllo fine ti permette di costruire soluzioni di ricerca ad alte prestazioni, consapevoli dell'OCR, personalizzate per ambienti legali, di sviluppo o multilingue.

### Prossimi passi
- Sperimenta con intervalli Unicode aggiuntivi per alfabeti non latini.  
- Combina la configurazione dei caratteri con altre funzionalità di GroupDocs.Search come stemming o sinonimi.  
- Esporre l'indice tramite un'API REST per consentire alle applicazioni front‑end di eseguire ricerche via HTTP.  

## Domande frequenti

**Q:** *Qual è lo scopo di `CharacterType.Letter`?*  
**A:** Indica all'indice di trattare i caratteri forniti come lettere regolari, così vengono tokenizzati separatamente durante l'indicizzazione.

**Q:** *Posso mescolare caratteri regolari e misti nello stesso indice?*  
**A:** Sì — basta chiamare `setRange` per ciascun tipo; il dizionario gestirà entrambe le configurazioni contemporaneamente.

**Q:** *Devo ricostruire l'indice dopo aver modificato l'alfabeto?*  
**A:** Assolutamente. Le modifiche al dizionario dei caratteri influenzano la tokenizzazione, quindi è necessario re‑indicizzare i documenti per applicare le nuove regole.

**Q:** *Esiste un limite al numero di caratteri personalizzati che posso definire?*  
**A:** La libreria supporta l'intero intervallo Unicode; le prestazioni potrebbero degradare se aggiungi un set estremamente grande, quindi limitati ai caratteri realmente necessari.

**Q:** *Come influisce questo sulla precisione dell'OCR?*  
**A:** Allineando il set di caratteri dell'indice con l'output del motore OCR, riduci i falsi negativi e migliori la rilevanza complessiva della ricerca.

---

**Ultimo aggiornamento:** 2026-11-02  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Crea Gestisci Indice Groupdocs Search Java](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Crea Directory Indice di Ricerca & Imposta Licenza – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Libreria Java Full Text Search – Ottimizza Indice con GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)