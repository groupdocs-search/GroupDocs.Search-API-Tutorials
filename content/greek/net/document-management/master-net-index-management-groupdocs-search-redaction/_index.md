---
date: '2026-07-26'
description: Μάθετε πώς να δημιουργήσετε index σε .NET χρησιμοποιώντας GroupDocs.Search
  και να ενσωματώσετε redaction με GroupDocs.Redaction, επιτρέποντας γρήγορη αναζήτηση
  εγγράφων και διαχείριση δεδομένων.
keywords:
- how to create index
- how to add documents
- how to delete document
- search index .net
lastmod: '2026-07-26'
og_description: Μάθετε πώς να δημιουργήσετε index σε .NET χρησιμοποιώντας GroupDocs.Search
  και να ενσωματώσετε redaction με GroupDocs.Redaction, επιτρέποντας γρήγορη αναζήτηση
  εγγράφων και διαχείριση δεδομένων.
og_image_alt: Guide showing GroupDocs Search index creation and Redaction integration
  in .NET
og_title: Πώς να δημιουργήσετε index σε .NET με GroupDocs Search API
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  headline: How to Create Index in .NET with GroupDocs Search API
  type: TechArticle
- description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  name: How to Create Index in .NET with GroupDocs Search API
  steps:
  - name: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
    text: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
  - name: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
    text: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
  - name: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
    text: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
  - name: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
    text: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
  - name: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
    text: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search can index over 150 formats—including PDFs, DOCX,
      PPTX, XLSX, and image types—by extracting embedded text via OCR where necessary.
    question: Can I index non‑text files with GroupDocs?
  - answer: Use `AddFolder` with a configurable batch size, run indexing in a background
      service, and periodically call `Optimize()` to merge small index segments.
    question: How do I handle large volumes of documents?
  - answer: Redaction removes personally identifiable information before it ever reaches
      the index, guaranteeing that search results never expose protected data.
    question: What are the benefits of using redaction with indexing?
  - answer: GroupDocs.Search provides synonym dictionaries, custom tokenizers, and
      regular‑expression filters, allowing you to fine‑tune relevance scoring.
    question: Is it possible to customize search algorithms?
  - answer: Verify folder permissions, ensure the .NET runtime matches the library’s
      target, and check the log file generated in the index folder for detailed error
      messages.
    question: How do I troubleshoot common indexing issues?
  type: FAQPage
tags:
- index management
- GroupDocs.Search
- GroupDocs.Redaction
- C# document indexing
- document redaction .NET
title: Πώς να δημιουργήσετε index σε .NET με GroupDocs Search API
type: docs
url: /el/net/document-management/master-net-index-management-groupdocs-search-redaction/
weight: 1
---

# Πώς να δημιουργήσετε ευρετήριο σε .NET με το GroupDocs Search API

Σε αυτό το σεμινάριο θα ανακαλύψετε **πώς να δημιουργήσετε ευρετήριο** για τις .NET εφαρμογές σας χρησιμοποιώντας το GroupDocs.Search και στη συνέχεια να προστατεύσετε ευαίσθητο περιεχόμενο με το GroupDocs.Redaction. Στο τέλος του οδηγού θα μπορείτε να δημιουργήσετε, να ενημερώσετε και να καθαρίσετε ένα αναζητήσιμο ευρετήριο, και θα καταλάβετε γιατί ο συνδυασμός αναζήτησης και επεξεργασίας είναι μια βέλτιστη πρακτική για ασφαλή διαχείριση εγγράφων.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “πώς να δημιουργήσετε ευρετήριο”;** Σημαίνει τη δημιουργία μιας αναζητήσιμης δομής δεδομένων που αντιστοιχίζει το περιεχόμενο του εγγράφου σε γρήγορα κλειδιά αναζήτησης.  
- **Ποιες βιβλιοθήκες απαιτούνται;** GroupDocs.Search και GroupDocs.Redaction για .NET (πακέτα NuGet).  
- **Μπορώ να ευρετήσω PDF, Word και εικόνες;** Ναι—υποστηρίζονται πάνω από 150 μορφές από προεπιλογή.  
- **Πώς διαγράφω ένα έγγραφο από το ευρετήριο;** Καλέστε τη μέθοδο `Delete` με τη διαδρομή ή το αναγνωριστικό του εγγράφου.  
- **Εκτελείται η επεξεργασία πριν ή μετά την ευρετηρίαση;** Η επεξεργασία πρέπει να γίνεται πρώτα ώστε τα προστατευμένα δεδομένα να μην εισέλθουν ποτέ στο ευρετήριο.

## Τι είναι το “πώς να δημιουργήσετε ευρετήριο”;
Η φράση **πώς να δημιουργήσετε ευρετήριο** αναφέρεται στη διαδικασία δημιουργίας μιας αναζητήσιμης δομής δεδομένων που αποθηκεύει αντιστοιχίσεις όρων‑σε‑έγγραφα για γρήγορη ανάκτηση. Στο GroupDocs, αυτή η δομή βρίσκεται στο δίσκο και μπορεί να ενημερώνεται σταδιακά χωρίς την ανάγκη επαναδημιουργίας ολόκληρης της συλλογής.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search και το GroupDocs.Redaction μαζί;
Το GroupDocs.Search υποστηρίζει ευρετηρίαση **150+ μορφών αρχείων** και μπορεί να διαχειριστεί ευρετήρια μεγαλύτερα από **10 GB**, διατηρώντας τη χρήση μνήμης κάτω από 200 MB, επειδή μεταδίδει τα αρχεία αντί να τα φορτώνει εντελώς. Η προσθήκη του GroupDocs.Redaction εξασφαλίζει ότι οποιοδήποτε εμπιστευτικό κείμενο, εικόνες ή μεταδεδομένα αφαιρούνται πριν το περιεχόμενο φτάσει στο ευρετήριο, εγγυώμενη συμμόρφωση με GDPR, HIPAA και άλλους κανονισμούς.

## Προαπαιτούμενα

- **Βιβλιοθήκες & Εκδόσεις** – Εγκαταστήστε τα πιο πρόσφατα πακέτα NuGet **GroupDocs.Search** και **GroupDocs.Redaction** που είναι συμβατά με .NET 6 ή νεότερο.  
- **IDE** – Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει .NET 6).  
- **Γνώση** – Βασικές δεξιότητες C#, εξοικείωση με το αρχείο I/O, και κατανόηση των εννοιών ευρετηρίασης.

## Ρύθμιση του GroupDocs.Redaction για .NET

### Εγκατάσταση

**Χρήση .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Χρήση του Package Manager Console στο Visual Studio:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Μπορείτε επίσης να βρείτε το “GroupDocs.Redaction” στο UI του NuGet Package Manager και να εγκαταστήσετε την πιο πρόσφατη σταθερή έκδοση.

### Απόκτηση Άδειας

Μπορείτε να αποκτήσετε δωρεάν δοκιμή ή να ζητήσετε προσωρινή άδεια για να εξερευνήσετε όλες τις δυνατότητες χωρίς περιορισμούς. Επισκεφθείτε τη [Σελίδα Αγοράς του GroupDocs](https://purchase.groupdocs.com/temporary-license/) για περισσότερες λεπτομέρειες σχετικά με την απόκτηση άδειας.

### Βασική Αρχικοποίηση

Η κλάση Redactor είναι η κύρια κλάση που εκτελεί λειτουργίες επεξεργασίας σε ένα έγγραφο.  
Το παρακάτω απόσπασμα δείχνει τον ελάχιστο κώδικα που απαιτείται για να ξεκινήσετε τη χρήση του GroupDocs.Redaction:  
```csharp
// Initialize the Redactor with a file path or stream
using (Redactor redactor = new Redactor("input.docx"))
{
    // Your redaction code here
}
```  

Αυτή η απλή ρύθμιση είναι ό,τι χρειάζεστε για να αρχίσετε να χρησιμοποιείτε το GroupDocs.Redaction.

## Οδηγός Υλοποίησης

### Πώς να δημιουργήσετε ευρετήριο;

`Index` αντιπροσωπεύει το αναζητήσιμο κοντέινερ που περιέχει λεξικά όρων και μεταδεδομένα εγγράφων. Φορτώστε ή δημιουργήστε ένα αντικείμενο `Index`, ορίστε το σε έναν φάκελο όπου θα αποθηκευτούν τα αρχεία του ευρετηρίου και καλέστε το `Create`. Η λειτουργία γράφει τα απαραίτητα αρχεία μεταδεδομένων και προετοιμάζει τη μηχανή για την εισαγωγή εγγράφων.  
```text
// Direct answer (40‑70 words):
Create a new `Index` instance by specifying the folder path where the index will reside, then invoke `Create()` to initialise the storage structures. The method writes index headers, term dictionaries, and a lock file, making the folder ready for document addition. This step is required only once per index location.
```

#### Βήμα 1: Δημιουργία του Ευρετηρίου
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/DeleteIndexedPaths";
Index index = new Index(indexFolder);
// This line initializes an index at the provided folder path.
```  

### Πώς να προσθέσετε έγγραφα στο ευρετήριο;

`Add` εισάγει ένα μόνο έγγραφο στο ευρετήριο, ενώ το `AddFolder` επεξεργάζεται όλα τα αρχεία σε έναν κατάλογο. Προσθέτετε αρχεία καλώντας το `Add` ή το `AddFolder`. Η μηχανή διαβάζει κάθε υποστηριζόμενο αρχείο, εξάγει το κείμενο και ενημερώνει το λεξικό όρων.  
```text
// Direct answer (40‑70 words):
Use `index.AddFolder("C:\\Docs")` or `index.Add("C:\\Docs\\file.pdf")` to feed documents into the index. The API streams each file, extracts searchable text, and stores term‑frequency data without loading the entire file into memory, which lets you index thousands of large PDFs efficiently.
```

#### Βήμα 2: Προσθήκη Φακέλων Εγγράφων
```csharp
string documentsFolder1 = @"YOUR_DOCUMENT_DIRECTORY";
string documentsFolder2 = @"YOUR_DOCUMENT_DIRECTORY2";

index.Add(documentsFolder1);  // Adding the first folder of documents to the index
index.Add(documentsFolder2);  // Adding the second folder of documents to the index
```  

### Πώς να ανακτήσετε τις ευρετηριασμένες διαδρομές;

`GetIndexedPaths` επιστρέφει μια συλλογή όλων των διαδρομών εγγράφων που αποθηκεύονται στο ευρετήριο. Η ανάκτηση της λίστας των ευρετηριασμένων διαδρομών αρχείων σας επιτρέπει να επαληθεύσετε ποια έγγραφα είναι αυτή τη στιγμή αναζητήσιμα.  
```text
// Direct answer (40‑70 words):
Call `index.GetIndexedDocuments()` to obtain a collection of `IndexedDocumentInfo` objects, each containing the original file path, document ID, and indexing timestamp. Loop through the collection and output the `FilePath` property to confirm that every expected file has been successfully added.
```

#### Βήμα 3: Εμφάνιση Ευρετηριασμένων Διαδρομών
```csharp
string[] indexedPaths1 = index.GetIndexedPaths();
foreach (string path in indexedPaths1)
{
    Console.WriteLine(path); // Outputs the document paths
}
```  

### Πώς να διαγράψετε έγγραφο από το ευρετήριο;

`Delete` αφαιρεί ένα έγγραφο από το ευρετήριο με τη διαδρομή ή το αναγνωριστικό του. Όταν ένα αρχείο αφαιρεθεί ή καταστεί παρωχημένο, πρέπει να διαγράψετε την καταχώρησή του για να διατηρήσετε τα αποτελέσματα αναζήτησης ακριβή.  
```text
// Direct answer (40‑70 words):
Invoke `index.Delete("C:\\Docs\\obsolete.pdf")` or `index.Delete(documentId)` to purge a specific document from the index. The method removes all term entries linked to that file, updates the term dictionary, and frees the space on disk, ensuring that future queries no longer return the deleted content.
```

#### Βήμα 4: Διαγραφή Συγκεκριμένων Διαδρομών
```csharp
using GroupDocs.Search.Options;

string[] pathsToDelete = { @"YOUR_DOCUMENT_DIRECTORY" };
DeleteResult deleteResult = index.Delete(pathsToDelete, new UpdateOptions());
// This deletes specified document paths from the index.
```  

### Πώς να επαληθεύσετε τις υπόλοιπες ευρετηριασμένες διαδρομές μετά τη διαγραφή;

Μετά την αφαίρεση, μπορείτε να εκτελέσετε ξανά τη μέθοδο ανάκτησης για να διασφαλίσετε ότι το ευρετήριο αντανακλά την τρέχουσα κατάσταση.  
```text
// Direct answer (40‑70 words):
Run `index.GetIndexedDocuments()` again and compare the resulting list with the pre‑deletion list. The missing file path confirms successful deletion, while the remaining entries confirm the index’s integrity. This verification step is especially important in automated pipelines.
```

#### Βήμα 5: Επαλήθευση Υπόλοιπων Διαδρομών
```csharp
string[] indexedPaths2 = index.GetIndexedPaths();
foreach (string path in indexedPaths2)
{
    Console.WriteLine(path); // Displays remaining paths after deletion
}
```  

## Πρακτικές Εφαρμογές

1. **Συστήματα Διαχείρισης Εγγράφων** – Εντοπίστε γρήγορα συμβάσεις, τιμολόγια ή εγχειρίδια σε εκατομμύρια αρχεία.  
2. **Νομική Ανασκόπηση Εγγράφων** – Επεξεργαστείτε προνομιούσες πληροφορίες πριν την ευρετηρίαση για να αποφύγετε τυχαία αποκάλυψη.  
3. **Αρχειακές Λύσεις** – Διατηρήστε αναζητήσιμα μεταδεδομένα για ιστορικά αρχεία χωρίς να φορτώνετε ολόκληρα τα αρχεία στη μνήμη.  
4. **Πλατφόρμες Διαχείρισης Περιεχομένου** – Ενεργοποιήστε αναζήτηση σε όλο τον ιστότοπο για blogs, βάσεις γνώσης και βιβλιοθήκες πολυμέσων.  
5. **Έλεγχοι Συμμόρφωσης Δεδομένων** – Διασφαλίστε ότι μόνο καθαρισμένο περιεχόμενο είναι αναζητήσιμο, καλύπτοντας τις απαιτήσεις των κανονισμών.

## Σκέψεις για την Απόδοση

- **Βελτιστοποίηση Ευρετηρίασης** – Προγραμματίστε σταδιακή ευρετηρίαση κάθε βράδυ· χρησιμοποιήστε το `AddFolder` με μέγεθος παρτίδας 100 αρχείων για να μειώσετε τις αιχμές I/O.  
- **Διαχείριση Πόρων** – Παρακολουθήστε CPU και RAM· το GroupDocs.Search επεξεργάζεται αρχεία με ροή, διατηρώντας τη μέγιστη μνήμη κάτω από 200 MB ακόμη και για ευρετήρια 10 GB.  
- **Καλές Πρακτικές** – Αποθηκεύστε το ευρετήριο σε SSD για απόκριση ερωτημάτων κάτω του δευτερολέπτου, και ενεργοποιήστε τη συμπίεση (`index.Compression = true`) για να μειώσετε τη χρήση δίσκου στο μισό.

## Συχνές Ερωτήσεις

**Q: Μπορώ να ευρετήσω μη‑κείμενα αρχεία με το GroupDocs;**  
A: Ναι, το GroupDocs.Search μπορεί να ευρετήσει πάνω από 150 μορφές—συμπεριλαμβανομένων PDF, DOCX, PPTX, XLSX και τύπων εικόνων—εξάγοντας το ενσωματωμένο κείμενο μέσω OCR όπου χρειάζεται.

**Q: Πώς διαχειρίζομαι μεγάλα όγκους εγγράφων;**  
A: Χρησιμοποιήστε το `AddFolder` με ρυθμιζόμενο μέγεθος παρτίδας, εκτελέστε την ευρετηρίαση σε υπηρεσία παρασκηνίου και καλέστε περιοδικά το `Optimize()` για συγχώνευση μικρών τμημάτων ευρετηρίου.

**Q: Ποια είναι τα οφέλη της χρήσης επεξεργασίας με την ευρετηρίαση;**  
A: Η επεξεργασία αφαιρεί προσωπικά αναγνωρίσιμες πληροφορίες πριν φτάσουν στο ευρετήριο, εγγυώμενη ότι τα αποτελέσματα αναζήτησης δεν εκθέτουν προστατευμένα δεδομένα.

**Q: Είναι δυνατόν να προσαρμόσετε τους αλγόριθμους αναζήτησης;**  
A: Το GroupDocs.Search παρέχει λεξικά συνωνύμων, προσαρμοσμένους διαχωριστές (tokenizers) και φίλτρα κανονικών εκφράσεων, επιτρέποντάς σας να ρυθμίσετε με ακρίβεια τη βαθμολογία συνάφειας.

**Q: Πώς αντιμετωπίζω κοινά προβλήματα ευρετηρίασης;**  
A: Επαληθεύστε τα δικαιώματα φακέλου, βεβαιωθείτε ότι το .NET runtime ταιριάζει με τον στόχο της βιβλιοθήκης, και ελέγξτε το αρχείο καταγραφής που δημιουργείται στον φάκελο του ευρετηρίου για λεπτομερή μηνύματα σφάλματος.

## Πόροι

- **Τεκμηρίωση**: [Τεκμηρίωση](https://docs.groupdocs.com/search/net/)  
- **Αναφορά API**: [Αναφορά API](https://reference.groupdocs.com/redaction/net)  
- **Τελευταίες Εκδόσεις GroupDocs**: [Τελευταίες Εκδόσεις GroupDocs](https://releases.groupdocs.com/search/net/)  
- **Δωρεάν Υποστήριξη**: [Δωρεάν Υποστήριξη](https://forum.groupdocs.com/c/search/10)  
- **Αίτηση για Προσωρινή Άδεια**: [Αίτηση για Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)  

Εξερευνήστε αυτούς τους πόρους για να εμβαθύνετε την κατανόησή σας και να βελτιώσετε την υλοποίησή σας του GroupDocs.Search και Redaction σε .NET. Καλή προγραμματιστική!

---

**Τελευταία Ενημέρωση:** 2026-07-26  
**Δοκιμάστηκε Με:** GroupDocs.Search 23.10, GroupDocs.Redaction 23.10 for .NET  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Δημιουργία και Συγχώνευση Ευρετηρίου με το GroupDocs.Redaction .NET για Αποτελεσματική Διαχείριση Εγγράφων](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [Απόκτηση Εξέλιξης στο GroupDocs.Redaction .NET: Αποτελεσματική Δημιουργία Ευρετηρίου και Διαχείριση Ψευδώνυμων για Προηγμένη Αναζήτηση Εγγράφων](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Αριστεία στο GroupDocs Search και Redaction σε .NET: Ένας Πλήρης Οδηγός για Διαχείριση Εγγράφων](/search/net/document-management/groupdocs-search-redaction-net-tutorial/)