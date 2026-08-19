---
date: '2026-03-17'
description: Scopri come creare un indice con GroupDocs.Search per Java, configurare
  caratteri regolari e misti e ottimizzare la ricerca per numeri di cause legali e
  immagini OCR.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: How to Create Index with Character Recognition in Java
type: docs
url: /it/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Come creare un indice con riconoscimento dei caratteri usando GroupDocs.Search per Java

Nelle moderne applicazioni ricche di documenti, **come creare un indice** che rispetti le sfumature del tuo testo — come trattini, underscore o simboli specifici della lingua — è essenziale per un recupero rapido e accurato. In questo tutorial vedremo come configurare il riconoscimento dei caratteri in **GroupDocs.Search per Java**, coprendo sia i caratteri regolari (lettere, cifre, underscore) sia i caratteri misti (ad esempio i trattini). Alla fine, sarai in grado di personalizzare un indice che soddisfi le esigenze precise del tuo scenario OCR o di ricerca di immagini, sia che tu stia indicizzando numeri di cause legali, repository di codice sorgente o PDF multilingue.

## Risposte rapide
- **Cosa significa “create custom search index”?** Significa configurare un indice per trattare simboli specifici come lettere o caratteri misti, invece di ignorarli.  
- **Quale libreria viene usata?** GroupDocs.Search for Java (v25.4 al momento della stesura).  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per lo sviluppo; è necessaria una licenza a pagamento per la produzione.  
- **Posso indicizzare sia PDF che immagini?** Sì — GroupDocs.Search supporta OCR su immagini e PDF quando configurato correttamente.  
- **Maven è obbligatorio?** Maven è il metodo consigliato per gestire le dipendenze, ma è possibile usare anche Gradle o JAR manuali.  

## Cos'è un indice di ricerca personalizzato?
Un indice di ricerca personalizzato ti consente di definire come il motore di ricerca interpreta i caratteri. Per impostazione predefinita, molti simboli vengono ignorati, il che può portare a corrispondenze mancate per elementi come i numeri di caso (`2023-AB-456`) o frammenti di codice (`my_variable`). Modificando il dizionario dell'alfabeto ottieni il pieno controllo su ciò che il motore considera testo ricercabile.

## Perché configurare caratteri regolari e misti per i numeri di causa legale?
- **Caratteri regolari** (lettere, cifre, underscore) vengono tokenizzati separatamente, consentendo ricerche a corrispondenza esatta per gli identificatori.  
- **Caratteri misti** (trattini, slash) mantengono i token correlati insieme, evitando divisioni indesiderate di numeri di caso, codici prodotto o percorsi di file.  
- Questa configurazione **ottimizza le prestazioni dell'indice di ricerca** riducendo la frammentazione dei token e migliorando la pertinenza per contenuti generati da OCR.  

## Prerequisiti
- **JDK 8** o versioni successive installate.  
- **Maven** per la gestione delle dipendenze.  
- Accesso alla libreria **GroupDocs.Search for Java** (scaricata via Maven o dal sito ufficiale).  

### Librerie e dipendenze richieste
Aggiungi il repository e le voci di dipendenza al tuo `pom.xml` (come mostrato di seguito). Il blocco XML deve rimanere invariato.

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
- **Free Trial** – perfetta per le prime sperimentazioni.  
- **Temporary License** – utile per cicli di sviluppo più lunghi.  
- **Production License** – necessaria per il deployment commerciale.  

Ottieni una licenza dal portale ufficiale: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Inizializzazione di base
Il frammento di codice qui sotto mostra il codice minimo necessario per avviare un indice vuoto. Mantienilo così com'è; lo estenderemo in seguito.

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

### Installazione via Maven
La configurazione Maven dalla sezione *Prerequisiti* è tutto ciò di cui hai bisogno. Dopo averla aggiunta, esegui `mvn clean install` per scaricare i binari.

### Requisiti per la configurazione dell'ambiente
- Assicurati che la **cartella dell'indice** e la **cartella dei documenti** esistano su disco.  
- Usa percorsi assoluti o configura il tuo IDE per risolvere correttamente i percorsi relativi.  

## Guida all'implementazione

Di seguito esaminiamo due funzionalità distinte: **caratteri regolari** e **caratteri misti**. Ogni funzionalità segue lo stesso schema — definisci i percorsi, crea l'indice, imposta il dizionario dei caratteri e infine indicizza i documenti.

### Funzione 1 – Caratteri regolari

#### Panoramica
I caratteri regolari sono trattati come token indipendenti. Questo è ideale quando vuoi che cifre, lettere e underscore siano ricercabili esattamente come appaiono.

#### Implementazione passo‑passo

**1️⃣ Configura i percorsi**  
Definisci dove verrà memorizzato l'indice e dove si trovano i tuoi documenti sorgente.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Crea e configura l'indice**  
Istanzia l'indice e cancella qualsiasi configurazione dell'alfabeto pre‑esistente.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Definisci i caratteri regolari**  
Costruisci un array di caratteri che includa cifre, lettere latine e l'underscore.

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

### Funzione 2 – Caratteri misti

#### Panoramica
I caratteri misti (come i trattini) spesso collegano due parole. Contrassegnarli come *misti* indica al motore di mantenere i token circostanti insieme durante l'indicizzazione.

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

### Caso d'uso 1 – Gestione documenti legali
I file legali spesso contengono numeri di caso come `2023-AB-456`. Configurando underscore e trattini, le ricerche restituiscono corrispondenze esatte senza dividere l'identificatore, aiutandoti a **cercare numeri di causa legali** in modo efficiente.

### Caso d'uso 2 – Repository di codice sorgente
Gli sviluppatori hanno bisogno di cercare frammenti di codice dove underscore (`my_variable`) e trattini (`my-function`) sono significativi. Il riconoscimento personalizzato dei caratteri garantisce che il motore di ricerca rispetti questi simboli.

### Caso d'uso 3 – Set di dati multilingue
Quando si lavora con lingue che usano alfabeti aggiuntivi, è possibile **estendere il set di caratteri Unicode** per includere quegli intervalli, garantendo risultati di ricerca accurati tra più lingue.

### Caso d'uso 4 – Indicizzare immagini PDF
Se stai indicizzando PDF scansionati o file immagine, l'output OCR contiene spesso caratteri misti. Configurare correttamente caratteri regolari e misti **ottimizza le prestazioni dell'indice di ricerca** per contenuti basati su immagini.

## Considerazioni sulle prestazioni

- **Gestione delle risorse** – Tieni sotto controllo l'utilizzo dell'heap; gli indici di grandi dimensioni beneficiano di commit incrementali.  
- **Garbage Collection** – Rilascia gli oggetti `Index` al termine per consentire alla JVM di recuperare la memoria.  
- **Ottimizzazione dell'indice** – Chiama periodicamente `index.optimize()` (se disponibile) per compattare l'indice e migliorare la velocità delle query.  

## Conclusione

Ora sai **come creare un indice** che distingue tra caratteri regolari e misti usando GroupDocs.Search per Java. Questo controllo fine ti permette di costruire soluzioni di ricerca ad alte prestazioni, consapevoli dell'OCR, adatte a contesti legali, di sviluppo o multilingue.

### Prossimi passi
- Sperimenta con intervalli Unicode aggiuntivi per alfabeti non latini.  
- Combina la configurazione dei caratteri con altre funzionalità di GroupDocs.Search come stemming o sinonimi.  
- Integra l'indice in un'API REST per esporre le capacità di ricerca alle applicazioni front‑end.  

## Domande frequenti

**Q:** *Qual è lo scopo di `CharacterType.Letter`?*  
**A:** Indica all'indice di trattare i caratteri forniti come lettere regolari, così vengono tokenizzati separatamente durante l'indicizzazione.

**Q:** *Posso mescolare caratteri regolari e misti nello stesso indice?*  
**A:** Sì — basta chiamare `setRange` per ciascun tipo; il dizionario gestirà entrambe le configurazioni contemporaneamente.

**Q:** *Devo ricostruire l'indice dopo aver modificato l'alfabeto?*  
**A:** Assolutamente. Le modifiche al dizionario dei caratteri influenzano la tokenizzazione, quindi è necessario re‑indicizzare i documenti per applicare le nuove regole.

**Q:** *Esiste un limite al numero di caratteri personalizzati che posso definire?*  
**A:** La libreria supporta l'intero intervallo Unicode; le prestazioni possono degradare se aggiungi un set estremamente grande, quindi limitati ai caratteri realmente necessari.

**Q:** *Come influisce questo sull'accuratezza dell'OCR?*  
**A:** Allineando il set di caratteri dell'indice con l'output del motore OCR, riduci i falsi negativi e migliori la pertinenza complessiva della ricerca.

---

**Ultimo aggiornamento:** 2026-03-17  
**Testato con:** GroupDocs.Search 25.4 per Java  
**Autore:** GroupDocs