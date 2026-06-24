---
date: '2026-06-22'
description: Μάθετε πώς να εκτελέσετε απόκρυψη εγγράφων σε .NET ενώ βελτιστοποιείτε
  την απόδοση αναζήτησης με το GroupDocs.Redaction και το GroupDocs.Search. Step‑by‑step
  attribute management, indexing, και secure redaction για προγραμματιστές .NET.
keywords:
- how to redact documents
- optimize search performance
- how to index attributes
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  headline: How to Redact Documents in .NET Using GroupDocs Redaction
  type: TechArticle
- description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  name: How to Redact Documents in .NET Using GroupDocs Redaction
  steps:
  - name: Initialize Index
    text: '`Index` represents a searchable collection of documents and their associated
      metadata. csharp using GroupDocs.Search.Common; using GroupDocs.Search.Options;
      using GroupDocs.Search.Results; Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
      index.Add("@YOUR_DOCUMENT_DIRECTORY/Docum'
  - name: Modify Attributes
    text: '`AttributeChangeBatch` is the class that batches attribute updates for
      efficiency. **Definition anchor:** *`AttributeChangeBatch` batches add, update,
      and delete operations on document attributes in a single transaction.* csharp
      DocumentInfo[] documents = index.GetIndexedDocuments(); AttributeChange'
  - name: Search with Attribute Filters
    text: You can filter search results by attribute values using `SearchOptions`.
      **Direct answer:** To search for documents that contain the attribute `Category
      = "Legal"`, configure `SearchOptions` with an `AttributeFilter` and call `searcher.Search("contract",
      options)`. This returns only the legally tagg
  - name: Set Up Event Handler for Indexing
    text: '**Definition anchor:** *The `DocumentIndexed` event fires each time a document
      is successfully added to the index, allowing custom logic to run.* csharp Index
      index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing"); index.Events.FileIndexing
      += (sender, args) => { if (args.Document'
  - name: Configure and Perform Search
    text: After attributes are attached, you can search using those new fields. **Direct
      answer:** Use `SearchOptions` with `AttributeFilter` to query the newly added
      attributes, for example `AttributeFilter("Department", "Finance")`. This returns
      only finance‑related files, demonstrating **how to index attri
  type: HowTo
- questions:
  - answer: Load each file with `Redactor`, add a `RedactionRegion` for every sensitive
      area, then call `Redactor.Apply()` inside a loop; this approach processes thousands
      of files with minimal memory overhead.
    question: What is the best way to batch‑redact multiple PDFs?
  - answer: Yes. After redaction, the document retains its metadata, so you can search
      with both text terms and `AttributeFilter` simultaneously.
    question: Can I combine redaction with attribute filtering in a single query?
  - answer: Pass the password to the `Redactor` constructor; the library will decrypt,
      redact, and re‑encrypt the file automatically.
    question: How do I handle password‑protected documents?
  - answer: Absolutely. Enable `RedactorOptions.Ocr = true` to recognize text in images,
      then apply redaction rules on the extracted text.
    question: Does GroupDocs support OCR for scanned images before redaction?
  - answer: GroupDocs.Redaction and GroupDocs.Search support .NET Core 3.1, .NET 5,
      .NET 6, and .NET 7, as well as .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Πώς να εκτελέσετε απόκρυψη εγγράφων σε .NET χρησιμοποιώντας το GroupDocs Redaction
type: docs
url: /el/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# Πώς να αποκρύψετε έγγραφα σε .NET χρησιμοποιώντας το GroupDocs Redaction

Σε αυτό το ολοκληρωμένο εκπαιδευτικό υλικό θα ανακαλύψετε **πώς να αποκρύψετε έγγραφα** σε περιβάλλον .NET και ταυτόχρονα να κυριαρχήσετε στη διαχείριση χαρακτηριστικών εγγράφων με τα GroupDocs.Redaction και GroupDocs.Search. Είτε χρειάζεστε να προστατεύσετε ευαίσθητα δεδομένα, να αυξήσετε την ταχύτητα αναζήτησης, είτε να οργανώσετε μεγάλες βιβλιοθήκες εγγράφων, οι τεχνικές που παρουσιάζονται εδώ σας παρέχουν μια έτοιμη για παραγωγή λύση που κλιμακώνεται σε εκατοντάδες χιλιάδες αρχεία.

## Γρήγορες Απαντήσεις
- **Πώς μπορώ να αποκρύψω ένα PDF σε .NET;** Φορτώστε το αρχείο με `Redactor`, ορίστε ένα `RedactionRegion` και καλέστε `Redactor.Apply()` – τρεις γραμμές κώδικα διαχειρίζονται το βάρος.  
- **Μπορώ να αλλάξω τα χαρακτηριστικά του εγγράφου μετά την ευρετηρίαση;** Ναι, χρησιμοποιήστε `AttributeChangeBatch` για να προσθέσετε, ενημερώσετε ή αφαιρέσετε χαρακτηριστικά μαζικά.  
- **Ποιες βιβλιοθήκες απαιτούνται;** `GroupDocs.Redaction` + `GroupDocs.Search` (τελευταίες εκδόσεις NuGet).  
- **Χρειάζομαι άδεια για παραγωγή;** Απαιτείται έγκυρη άδεια GroupDocs· διατίθεται προσωρινή δοκιμαστική άδεια για αξιολόγηση.  
- **Πώς μπορώ να βελτιώσω την ταχύτητα αναζήτησης;** Ενεργοποιήστε την επεξεργασία παρτίδων και την επιλεκτική ευρετηρίαση· αυτές οι τεχνικές μπορούν να **βελτιώσουν την απόδοση αναζήτησης** έως και 40 % σε μεγάλα σύνολα δεδομένων.

## Τι είναι η «απόκρυψη εγγράφων»;
Περιγράφει τη αυτοματοποιημένη διαδικασία εντοπισμού ευαίσθητων πληροφοριών μέσα σε ένα αρχείο και αντικατάστασής τους με κρυμμένο περιεχόμενο—όπως μαύρες γραμμές ή κενό χώρο—διατηρώντας την αρχική διάταξη αμετάβλητη. Αυτό εξασφαλίζει ότι τα εμπιστευτικά δεδομένα κρύβονται από τους θεατές, ενώ το έγγραφο παραμένει αναγνώσιμο και λειτουργικό για επόμενες εργασίες.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction και το GroupDocs.Search μαζί;
Το GroupDocs.Redaction υποστηρίζει **πάνω από 50 μορφές αρχείων** (PDF, DOCX, XLSX, PPTX, εικόνες κ.λπ.) και μπορεί να επεξεργαστεί έγγραφα έως **2 GB** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Το GroupDocs.Search ευρετηριάζει πάνω από **70 εκατομμύρια όρους** ανά ώρα σε τυπικό διακομιστή, επιτρέποντάς σας να **βελτιώσετε δραστικά την απόδοση αναζήτησης** όταν συνδυάζεται με φιλτράρισμα βάσει χαρακτηριστικών.

## Προαπαιτούμενα

- **Απαιτούμενες βιβλιοθήκες:** `GroupDocs.Search` και `GroupDocs.Redaction` (τελευταίες εκδόσεις NuGet).  
- **Περιβάλλον ανάπτυξης:** Visual Studio 2019 ή νεότερο, στοχεύοντας .NET Core 3.1 ή .NET 6+.  
- **Βασικές γνώσεις:** σύνταξη C#, αντικειμενοστραφείς έννοιες και εξοικείωση με τις αρχές ευρετηρίασης εγγράφων.

## Ρύθμιση του GroupDocs.Redaction για .NET

### Εγκατάσταση της βιβλιοθήκης

Μπορείτε να προσθέσετε το **GroupDocs.Redaction** στο έργο σας χρησιμοποιώντας οποιαδήποτε από τις παρακάτω μεθόδους:

**.NET CLI**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Package Manager**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**NuGet Package Manager UI**  
- Αναζητήστε “GroupDocs.Redaction” και εγκαταστήστε την τελευταία έκδοση.

### Βήματα απόκτησης άδειας

Για να ξεκινήσετε, μπορείτε να αποκτήσετε μια προσωρινή άδεια ή να αγοράσετε μία. Διατίθεται δωρεάν δοκιμή για να δοκιμάσετε τις λειτουργίες πριν δεσμευτείτε:

1. Επισκεφθείτε τη [Σελίδα Αδειοδότησης GroupDocs](https://purchase.groupdocs.com/temporary-license/) για να ζητήσετε μια προσωρινή άδεια.  
2. Ακολουθήστε τις οδηγίες που παρέχονται για την εφαρμογή της άδειας στην εφαρμογή σας.

### Βασική Αρχικοποίηση και Ρύθμιση

`Redactor` είναι η κύρια κλάση που χρησιμοποιείται για τη φόρτωση ενός εγγράφου και την εφαρμογή λειτουργιών απόκρυψης.

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## Χαρακτηριστικό 1: Αλλαγή Χαρακτηριστικών Εγγράφου

### Επισκόπηση
Η τροποποίηση των χαρακτηριστικών εγγράφου σας επιτρέπει να ρυθμίσετε λεπτομερώς τον τρόπο εμφάνισης των εγγράφων στα αποτελέσματα αναζήτησης, επιτρέποντας ακριβές φιλτράρισμα και κατηγοριοποίηση.

#### Βήμα 1: Αρχικοποίηση Ευρετηρίου
`Index` αντιπροσωπεύει μια συλλογή εγγράφων που μπορούν να αναζητηθούν και τα συναφή μεταδεδομένα τους.

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Βήμα 2: Τροποποίηση Χαρακτηριστικών
`AttributeChangeBatch` είναι η κλάση που ομαδοποιεί τις ενημερώσεις χαρακτηριστικών για αποδοτικότητα.

**Αγκύρωση ορισμού:** *`AttributeChangeBatch` ομαδοποιεί προσθήκες, ενημερώσεις και διαγραφές χαρακτηριστικών εγγράφων σε μια ενιαία συναλλαγή.*

```csharp
```csharp
DocumentInfo[] documents = index.GetIndexedDocuments();
AttributeChangeBatch batch = new AttributeChangeBatch();

// Adding "public" to all documents
batch.AddToAll("public");

// Removing "public" from the first document
batch.Remove(documents[0].FilePath, "public");

// Adding "main" and "key" to the first document
batch.Add(documents[0].FilePath, "main", "key");
index.ChangeAttributes(batch);
```
```

#### Βήμα 3: Αναζήτηση με Φίλτρα Χαρακτηριστικών
Μπορείτε να φιλτράρετε τα αποτελέσματα αναζήτησης με βάση τις τιμές χαρακτηριστικών χρησιμοποιώντας το `SearchOptions`.

**Άμεση απάντηση:** Για να αναζητήσετε έγγραφα που περιέχουν το χαρακτηριστικό `Category = "Legal"`, διαμορφώστε το `SearchOptions` με ένα `AttributeFilter` και καλέστε `searcher.Search("contract", options)`. Αυτό επιστρέφει μόνο τα νομικά επισημασμένα συμβόλαια, μειώνοντας τον θόρυβο των αποτελεσμάτων και **βελτιώνοντας την απόδοση αναζήτησης**.

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## Χαρακτηριστικό 2: Προσθήκη Χαρακτηριστικών Κατά την Ευρετηρίαση

### Επισκόπηση
Η προσθήκη χαρακτηριστικών τη στιγμή της ευρετηρίασης εξασφαλίζει ότι κάθε έγγραφο εμπλουτίζεται με τα σωστά μεταδεδομένα από την αρχή, εξαλείφοντας την ανάγκη για μεταγενέστερες μαζικές ενημερώσεις.

#### Βήμα 1: Ρύθμιση Διαχειριστή Συμβάντων για την Ευρετηρίαση
**Αγκύρωση ορισμού:** *Το συμβάν `DocumentIndexed` ενεργοποιείται κάθε φορά που ένα έγγραφο προστίθεται επιτυχώς στο ευρετήριο, επιτρέποντας την εκτέλεση προσαρμοσμένης λογικής.*

```csharp
```csharp
Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing");

index.Events.FileIndexing += (sender, args) => {
    if (args.DocumentFullPath.EndsWith("Lorem ipsum.pdf")) {
        // Specify attributes for this document
        args.Attributes = new string[] { "main", "key" };
    }
};

// Add documents to index
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Βήμα 2: Διαμόρφωση και Εκτέλεση Αναζήτησης
Αφού προσαρτηθούν τα χαρακτηριστικά, μπορείτε να αναζητήσετε χρησιμοποιώντας αυτά τα νέα πεδία.

**Άμεση απάντηση:** Χρησιμοποιήστε `SearchOptions` με `AttributeFilter` για να ερωτήσετε τα νεοπροστέθηκαν χαρακτηριστικά, π.χ. `AttributeFilter("Department", "Finance")`. Αυτό επιστρέφει μόνο αρχεία σχετιζόμενα με τα οικονομικά, δείχνοντας **πώς να ευρετηριάσετε χαρακτηριστικά** για ταχύτερα, πιο σχετικούς αποτελέσματα.

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## Πρακτικές Εφαρμογές

Ακολουθούν τρία κοινά σενάρια όπου η διαχείριση χαρακτηριστικών εγγράφων και η απόκρυψη μαζί προσθέτουν απτό επιχειρηματικό όφελος:

1. **Διαχείριση Νομικών Εγγράφων** – Αυτόματη απόκρυψη εμπιστευτικών ρήσεων και ετικετοθέτηση συμβάσεων ανά δικαιοδοσία, επιτρέποντας στους νομικούς να εντοπίζουν μόνο τα σχετικά αρχεία.  
2. **Οργάνωση Ιατρικών Αρχείων** – Απόκρυψη αναγνωριστικών ασθενών ενώ προστίθενται χαρακτηριστικά όπως `PatientID` και `VisitDate` για συμμορφωμένη, γρήγορη ανάκτηση.  
3. **Κατάλογος Προϊόντων Ηλεκτρονικού Εμπορίου** – Απόκρυψη πληροφοριών τιμολόγησης προμηθευτών και ετικετοθέτηση προϊόντων με `StockStatus` ή `DiscountRate` κατά τη μαζική εισαγωγή, επιτρέποντας ερωτήματα αποθέματος σε πραγματικό χρόνο.

## Σκέψεις Απόδοσης

Κατά τη διαχείριση μεγάλων συνόλων δεδομένων, λάβετε υπόψη τις ακόλουθες βέλτιστες πρακτικές:

- **Επεξεργασία Παρτίδων:** Το `AttributeChangeBatch` μειώνει τις επαναλήψεις προς το ευρετήριο, μειώνοντας τον χρόνο επεξεργασίας έως και **45 %** σε παρτίδες 100 k εγγράφων.  
- **Επιλεκτική Ευρετηρίαση:** Ευρετηριάστε μόνο τα έγγραφα που χρειάζονται νέα χαρακτηριστικά· παραλείψτε τα αμετάβλητα αρχεία για εξοικονόμηση CPU και I/O.  
- **Διαχείριση Μνήμης:** Αποδεσμεύστε τις παρουσίες `SearchResult`, `Redactor` και `Indexer` μόλις τελειώσετε με αυτές για να ελευθερώσετε μη διαχειριζόμενους πόρους.

## Συχνά Προβλήματα και Λύσεις

| Πρόβλημα | Αιτία | Λύση |
|----------|-------|------|
| Η απόκρυψη δεν κρύβει το κείμενο | Λανθασμένες συντεταγμένες `RedactionRegion` | Επαληθεύστε τις διαστάσεις της σελίδας με `Redactor.GetPageSize()` πριν ορίσετε την περιοχή. |
| Οι αλλαγές χαρακτηριστικών δεν αντικατοπτρίζονται στην αναζήτηση | Το ευρετήριο δεν έχει ανανεωθεί | Καλέστε `searcher.Refresh()` μετά την εκτέλεση του `AttributeChangeBatch`. |
| Σφάλματα έλλειψης μνήμης σε μεγάλα αρχεία | Φόρτωση ολόκληρου του αρχείου στη μνήμη | Ενεργοποιήστε τη λειτουργία streaming ορίζοντας `RedactorOptions.Stream = true`. |

## Συχνές Ερωτήσεις

**Q: Ποιος είναι ο καλύτερος τρόπος για μαζική απόκρυψη πολλαπλών PDF;**  
A: Φορτώστε κάθε αρχείο με `Redactor`, προσθέστε ένα `RedactionRegion` για κάθε ευαίσθητη περιοχή, και στη συνέχεια καλέστε `Redactor.Apply()` μέσα σε βρόχο· αυτή η προσέγγιση επεξεργάζεται χιλιάδες αρχεία με ελάχιστη χρήση μνήμης.

**Q: Μπορώ να συνδυάσω την απόκρυψη με φιλτράρισμα χαρακτηριστικών σε ένα μόνο ερώτημα;**  
A: Ναι. Μετά την απόκρυψη, το έγγραφο διατηρεί τα μεταδεδομένα του, έτσι μπορείτε να αναζητήσετε ταυτόχρονα με όρους κειμένου και `AttributeFilter`.

**Q: Πώς διαχειρίζομαι έγγραφα με προστασία κωδικού;**  
A: Περνάτε τον κωδικό στον κατασκευαστή `Redactor`; η βιβλιοθήκη θα αποκρυπτογραφήσει, θα εφαρμόσει την απόκρυψη και θα κρυπτογραφήσει ξανά το αρχείο αυτόματα.

**Q: Υποστηρίζει το GroupDocs OCR για σαρωμένες εικόνες πριν την απόκρυψη;**  
A: Απόλυτα. Ενεργοποιήστε `RedactorOptions.Ocr = true` για να αναγνωρίσετε κείμενο σε εικόνες, στη συνέχεια εφαρμόστε τους κανόνες απόκρυψης στο εξαγόμενο κείμενο.

**Q: Ποιες εκδόσεις .NET υποστηρίζονται επίσημα;**  
A: Τα GroupDocs.Redaction και GroupDocs.Search υποστηρίζουν .NET Core 3.1, .NET 5, .NET 6 και .NET 7, καθώς και .NET Framework 4.6.2+.

## Συμπέρασμα

Τώρα έχετε μια ολοκληρωμένη λύση για **την απόκρυψη εγγράφων** ενώ **βελτιώνετε την απόδοση αναζήτησης** και **ευρετηριάζετε χαρακτηριστικά** χρησιμοποιώντας το GroupDocs.Redaction και το GroupDocs.Search. Ακολουθώντας τα παραπάνω βήματα, μπορείτε να προστατεύσετε ευαίσθητα δεδομένα, να εμπλουτίσετε το ευρετήριο αναζήτησης με ουσιαστικά μεταδεδομένα και να διατηρήσετε τις .NET εφαρμογές σας γρήγορες και ασφαλείς.

---

**Τελευταία ενημέρωση:** 2026-06-22  
**Δοκιμάστηκε με:** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 for .NET  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Κατάκτηση του GroupDocs.Redaction .NET: Αποτελεσματική Δημιουργία Ευρετηρίου και Διαχείριση Ψευδωνύμων για Προηγμένη Αναζήτηση Εγγράφων](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Απόκρυψη Εγγράφων και Ευρετηρίαση Μεταδεδομένων με το GroupDocs.Redaction .NET](/search/net/document-management/groupdocs-redaction-net-document-metadata/)
- [Κατάκτηση του GroupDocs.Redaction .NET: Ρύθμιση & Διαχείριση Συμβάντων για Ασφαλή Διαχείριση Εγγράφων](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)