---
date: '2026-04-27'
description: Impara a redigere dati sensibili in .NET utilizzando GroupDocs.Search
  e Redaction e scopri come aggiungere documenti all'indice per la ricerca di documenti
  di grandi dimensioni.
keywords:
- redact sensitive data
- add documents to index
- search large documents
title: GroupDocs.Search e Redaction in .NET – censura dati sensibili
type: docs
url: /it/net/document-management/groupdocs-search-redaction-net-guide/
weight: 1
---

# GroupDocs.Search & Redaction in .NET – redigere dati sensibili

Gestire enormi quantità di documenti può essere scoraggiante, soprattutto quando è necessario **redigere dati sensibili** mantenendo al contempo capacità di ricerca rapide. In questa guida illustreremo come configurare GroupDocs.Search insieme a GroupDocs.Redaction, mostrandoti come **aggiungere documenti all'indice**, eseguire operazioni efficienti di **ricerca di documenti di grandi dimensioni**, e mantenere tutto conforme ai requisiti di privacy.

## Risposte rapide
- **Cosa significa “redact sensitive data”?** Significa rimuovere o mascherare permanentemente le informazioni riservate dai documenti.  
- **Quali librerie sono necessarie?** GroupDocs.Search e GroupDocs.Redaction per .NET (disponibili via NuGet).  
- **Posso indicizzare progetti .NET automaticamente?** Sì – vedi la sezione “How to index .NET” per una guida passo‑passo.  
- **Come gestisco file di grandi dimensioni?** Usa la ricerca basata su chunk per elaborare i dati in porzioni gestibili.  
- **È necessaria una licenza per la produzione?** È necessaria una licenza valida di GroupDocs per l'uso in produzione; sono disponibili versioni di prova gratuite.

## Cos'è la redazione di dati sensibili?
La redazione di dati sensibili è il processo di rimozione permanente o di oscuramento di informazioni personali, finanziarie o classificate da un documento, in modo che non possano essere recuperate o visualizzate da utenti non autorizzati.

## Perché combinare GroupDocs.Search con Redaction?
- **Velocità:** Crea indici ricercabili che restituiscono risultati in millisecondi.  
- **Sicurezza:** Applica regole di redazione prima che i documenti vengano condivisi o archiviati.  
- **Scalabilità:** La ricerca a chunk ti consente di lavorare con terabyte di testo senza esaurire la memoria.  
- **Conformità:** Rispetta GDPR, HIPAA e altre normative garantendo che i dati riservati non vengano mai divulgati.

## Prerequisiti
- Ambiente di sviluppo .NET (Visual Studio consigliato).  
- Conoscenza di base di C#.  
- Accesso a NuGet per installare i pacchetti richiesti.

## Configurazione di GroupDocs.Redaction per .NET

### Installazione tramite .NET CLI
```bash
dotnet add package GroupDocs.Redaction
```

### Installazione tramite Package Manager
```powershell
Install-Package GroupDocs.Redaction
```

### Interfaccia utente di NuGet Package Manager
Cerca **"GroupDocs.Redaction"** e installa l'ultima versione.

### Passaggi per l'acquisizione della licenza
- **Prova gratuita:** Inizia con una prova gratuita per esplorare le funzionalità.  
- **Licenza temporanea:** Richiedi una licenza temporanea per accesso esteso.  
- **Acquisto:** Considera l'acquisto per un utilizzo di produzione a lungo termine.

### Inizializzazione e configurazione di base
```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Initialize with desired options or default ones
```

## Guida all'implementazione

### Come indicizzare progetti .NET con GroupDocs.Search
Di seguito suddividiamo l'implementazione in passaggi chiari e numerati così da poterla seguire facilmente.

#### Passo 1: Specificare la cartella dell'indice
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SearchByChunks";
```
*Perché?* Definire una cartella dedicata mantiene il tuo indice organizzato e isolato dai documenti grezzi.

#### Passo 2: Creare e configurare l'indice
```csharp
Index index = new Index(indexFolder);
```
*Scopo:* Istanzia un nuovo indice ricercabile nella posizione che hai definito.

#### Passo 3: **Aggiungere documenti all'indice**
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath1");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath3");
```
*Spiegazione:* Ogni chiamata aggiunge un file (o una cartella) all'indice, rendendo il suo contenuto ricercabile.

### Ricerca di documenti di grandi dimensioni con Chunk Search
La ricerca a chunk ti consente di suddividere file massivi in pezzi più piccoli, mantenendo basso l'uso della memoria.

#### Passo 1: Definire la query di ricerca
```csharp
string query = "invitation";
```
*Scopo:* Il termine che stai cercando in tutti i file indicizzati.

#### Passo 2: Configurare le opzioni di Chunk Search
```csharp
SearchOptions options = new SearchOptions();
options.IsChunkSearch = true;
```
*Spiegazione:* Abilitare `IsChunkSearch` indica al motore di elaborare i dati a chunk.

#### Passo 3: Eseguire la ricerca iniziale
```csharp
SearchResult result = index.Search(query, options);
Console.WriteLine("Document count: " + result.DocumentCount);
Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
```
*Risultato:* Mostra quanti documenti contengono il termine e quante occorrenze totali sono state trovate.

#### Passo 4: Continuare con i chunk successivi
```csharp
while (result.NextChunkSearchToken != null)
{
    result = index.SearchNext(result.NextChunkSearchToken);
    Console.WriteLine("Document count: " + result.DocumentCount);
    Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
}
```
*Perché questo ciclo?* Garantisce di recuperare i risultati da ogni chunk fino a quando l'intero set di dati è stato elaborato.

### Come redigere dati sensibili con GroupDocs.Redaction
Dopo aver individuato le informazioni da proteggere, applica le regole di redazione.

#### Passo 1: Inizializzare le impostazioni di redazione
```csharp
RedactorSettings settings = new RedactorSettings();
```

#### Passo 2: Applicare le redazioni
Utilizza la classe `Redactor` (non mostrata qui per mantenere intatto il codice originale) per definire pattern, testo o immagini da mascherare.  
*Consiglio professionale:* Testa le tue regole di redazione su una copia del documento prima per evitare perdite accidentali di dati.

## Applicazioni pratiche
Queste capacità brillano in molti settori:

1. **Gestione documenti legali** – Cerca rapidamente i fascicoli dei casi mentre redigi i dettagli riservati dei clienti.  
2. **Gestione dati sanitari** – Proteggi le informazioni sanitarie dei pazienti (PHI) consentendo ai clinici di trovare i record pertinenti.  
3. **Audit finanziario** – Indicizza enormi log di transazioni e redigi numeri di conto o identificatori personali.

## Considerazioni sulle prestazioni
- **Ottimizza l'indicizzazione:** Reindicizza solo i file modificati per mantenere l'indice aggiornato senza lavoro inutile.  
- **Gestisci le risorse:** Regola le dimensioni dei chunk (`options.ChunkSize`) in base alla RAM del tuo server.  
- **Operazioni asincrone:** Per grandi batch, utilizza l'indicizzazione asincrona per mantenere l'interfaccia utente reattiva.

## Domande frequenti

**D: Come gestisco i file di grandi dimensioni in modo efficiente?**  
R: Usa ricerche basate su chunk (`IsChunkSearch = true`) per elaborare i dati in pezzi più piccoli, riducendo la pressione sulla memoria.

**D: GroupDocs.Redaction può funzionare con documenti criptati?**  
R: Sì – decripta prima il file, applica la redazione, poi ricifra se necessario.

**D: Quali opzioni di licenza sono disponibili?**  
R: Prova gratuita, licenza temporanea per valutazione e licenze commerciali complete per la produzione.

**D: Come posso risolvere gli errori di indicizzazione?**  
R: Verifica che il percorso della cartella dell'indice sia corretto, assicurati che l'applicazione abbia permessi di lettura/scrittura e controlla che tutti i formati di documento siano supportati.

**D: È possibile personalizzare ulteriormente le query di ricerca?**  
R: Assolutamente. Puoi combinare operatori booleani, wildcard e ricerche di prossimità usando l'API `SearchOptions`.

## Risorse
- **Documentazione:** [GroupDocs Redaction .NET](https://docs.groupdocs.com/search/net/)  
- **Riferimento API:** [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/net/)  
- **Supporto gratuito:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licenza temporanea:** [Request Here](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2026-04-27  
**Testato con:** GroupDocs.Search 23.9 and GroupDocs.Redaction 23.9 for .NET  
**Autore:** GroupDocs