---
date: '2026-07-02'
description: Μάθετε πώς να αποκρύψετε ευαίσθητες πληροφορίες σε έγγραφα και να βελτιώσετε
  την απόδοση της αναζήτησης προσθέτοντας έγγραφα στο ευρετήριο χρησιμοποιώντας το
  GroupDocs.Redaction και το GroupDocs.Search για .NET.
keywords:
- how to redact documents
- optimize search performance
- add documents to index
- redact pdf c#
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to redact documents and optimize search performance by adding
    documents to index using GroupDocs.Redaction and GroupDocs.Search for .NET.
  headline: How to Redact Documents & Optimize Search Index in .NET with GroupDocs
  type: TechArticle
- description: Learn how to redact documents and optimize search performance by adding
    documents to index using GroupDocs.Redaction and GroupDocs.Search for .NET.
  name: How to Redact Documents & Optimize Search Index in .NET with GroupDocs
  steps:
  - name: '**Legal Document Management** – Redact client names before indexing case
      files, ensuring privacy while lawyers can still search case law.'
    text: '**Legal Document Management** – Redact client names before indexing case
      files, ensuring privacy while lawyers can still search case law.'
  - name: '**Healthcare Records** – Strip patient identifiers from medical PDFs, then
      index the sanitized versions for rapid audit queries.'
    text: '**Healthcare Records** – Strip patient identifiers from medical PDFs, then
      index the sanitized versions for rapid audit queries.'
  - name: '**Corporate Compliance** – Automate redaction of financial statements and
      immediately make the clean versions searchable for internal investigations.'
    text: '**Corporate Compliance** – Automate redaction of financial statements and
      immediately make the clean versions searchable for internal investigations.'
  type: HowTo
- questions:
  - answer: Yes—`RedactionEngine` works natively with PDF streams, so you can load
      a PDF, apply redaction objects, and save the result without any format conversion.
    question: Can I redact PDF C# files directly without converting them first?
  - answer: Incremental indexing adds only the new files, keeping the index size stable
      and query latency under 200 ms for typical workloads.
    question: How does adding documents to index affect search speed?
  - answer: Absolutely. Use a Windows Service or Azure Function to call `Index.AddDocument`
      on a timer, feeding newly uploaded files into the index.
    question: Is it possible to schedule automatic re‑indexing?
  - answer: Yes—redaction overwrites the original bytes, making recovery impossible
      even with forensic tools.
    question: Does redaction permanently remove the hidden data?
  - answer: Both .NET Framework 4.6.1+ and .NET Core 3.1+ (including .NET 5/6) are
      officially supported.
    question: What .NET versions are fully supported?
  type: FAQPage
title: Πώς να αποκρύψετε ευαίσθητες πληροφορίες σε έγγραφα & να βελτιστοποιήσετε το
  ευρετήριο αναζήτησης σε .NET με το GroupDocs
type: docs
url: /el/net/document-management/master-document-redaction-groupdocs-net/
weight: 1
---

# Αποκτώντας Δεξιότητες στη Διαγραφή Εγγράφων και τη Διαχείριση Δεικτοδότησης Αναζήτησης σε .NET με το GroupDocs

## Εισαγωγή

Αν χρειάζεστε **πώς να διαγράψετε έγγραφα** ενώ τα διατηρείτε αναζητήσιμα, βρίσκεστε στο σωστό μέρος. Αυτό το εκπαιδευτικό υλικό σας καθοδηγεί στη συνδυαστική χρήση των **GroupDocs.Redaction** και **GroupDocs.Search** για την ασφαλή απόκρυψη ευαίσθητων δεδομένων και στη συνέχεια **προσθήκη εγγράφων στο ευρετήριο** για γρήγορη ανάκτηση. Στο τέλος θα κατανοήσετε πώς να **βελτιστοποιήσετε την απόδοση της αναζήτησης**, να διαγράψετε αρχεία PDF σε C# και να δημιουργήσετε μια αξιόπιστη διαδικασία δεικτοδότησης που κλιμακώνεται με τα δεδομένα σας.

## Γρήγορες Απαντήσεις
- **Πώς μπορώ να διαγράψω ένα PDF σε C#;** Χρησιμοποιήστε το `RedactionEngine` για να φορτώσετε το αρχείο, να ορίσετε περιοχές διαγραφής και να καλέσετε το `Save`.  
- **Ποια κλάση δημιουργεί ένα ευρετήριο αναζήτησης;** Η κλάση `Index` από το GroupDocs.Search διαχειρίζεται όλες τις λειτουργίες δεικτοδότησης.  
- **Μπορώ να προσθέσω νέα αρχεία χωρίς να ξαναχτίσω ολόκληρο το ευρετήριο;** Ναι—καλέστε το `Index.AddDocument` για σταδιακές ενημερώσεις.  
- **Επηρεάζει η διαγραφή τα αποτελέσματα της αναζήτησης;** Το διαγραμμένο περιεχόμενο εξαιρείται από το ευρετήριο, διατηρώντας τις αναζητήσεις καθαρές.  
- **Ποιες εκδόσεις του .NET υποστηρίζονται;** .NET Framework 4.6.1+, .NET Core 3.1+ και .NET 5/6.

## Τι είναι το “πώς να διαγράψετε έγγραφα”;
**“Πώς να διαγράψετε έγγραφα”** αναφέρεται στη διαδικασία προγραμματιστικής αφαίρεσης ή κάλυψης εμπιστευτικών πληροφοριών από αρχεία ώστε τα κρυμμένα δεδομένα να μην μπορούν να ανακτηθούν ή να εμφανιστούν. Η διαγραφή είναι απαραίτητη για τη συμμόρφωση, το απόρρητο και τις νομικές ροές εργασίας όπου πρέπει να αποτραπεί η έκθεση δεδομένων.

## Γιατί να χρησιμοποιήσετε το GroupDocs για διαγραφή και αναζήτηση;
Το GroupDocs υποστηρίζει **πάνω από 50 μορφές αρχείων** (συμπεριλαμβανομένων PDF, DOCX, PPTX και τύπων εικόνων) και μπορεί να επεξεργαστεί έγγραφα πολλαπλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, επιτυγχάνοντας **ταχύτητα δεικτοδότησης έως 30 %** σε σύγκριση με γενικές βιβλιοθήκες. Η συνδυασμένη σουίτα Redaction + Search σας επιτρέπει να **διαγράψετε αρχεία PDF C#** και άμεσα να δεικτοδοτήσετε την καθαρή έκδοση, εξαλείφοντας την ανάγκη για ξεχωριστό βήμα προεπεξεργασίας.

## Προαπαιτούμενα

- **GroupDocs.Search** για .NET (v20.11 ή νεότερο)  
- **GroupDocs.Redaction** για .NET (v20.10 ή νεότερο)  
- Visual Studio 2017 ή νεότερο  
- .NET Framework 4.6.1 ή νεότερο (ή .NET Core 3.1+)

### Προαπαιτούμενα Γνώσης
Θα πρέπει να είστε άνετοι με τη βασική σύνταξη C#, τις αναφορές έργου και τις λειτουργίες του συστήματος αρχείων.

## Ρύθμιση του GroupDocs.Redaction για .NET

### Εγκατάσταση των βιβλιοθηκών

**.NET CLI**  
`dotnet add package` είναι η εντολή .NET CLI που εγκαθιστά ένα πακέτο NuGet στο έργο σας.  

```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
`Install-Package` είναι η εντολή PowerShell που χρησιμοποιείται από την κονσόλα NuGet Package Manager για την προσθήκη βιβλιοθηκών.  

```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
Αναζητήστε το “GroupDocs.Redaction” και κάντε κλικ στο **Install** για να κατεβάσετε την πιο πρόσφατη σταθερή έκδοση.

### Απόκτηση Άδειας
- **Free Trial** – δοκιμή πλήρους λειτουργικότητας για 30 ημέρες.  
- **Temporary License** – 15‑ήμερη εκτεταμένη πρόσβαση για αξιολόγηση.  
- **Purchase** – μόνιμη άδεια παραγωγής.

#### Βασική Αρχικοποίηση
`RedactionEngine` είναι η βασική κλάση που χρησιμοποιείται για τη φόρτωση, τροποποίηση και αποθήκευση εγγράφων μετά τη διαγραφή.  

```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Further configuration and initialization...
```

## Οδηγός Υλοποίησης

Ας χωρίσουμε τη λύση σε τρία λογικά μέρη: δημιουργία ευρετηρίου, προσθήκη εγγράφων (συμπεριλαμβανομένων των διαγραμμένων) και αναζήτηση στο ευρετήριο.

### Πώς να δημιουργήσετε ένα ευρετήριο αναζήτησης με το GroupDocs.Search;

`Index` είναι η κύρια κλάση που αντιπροσωπεύει ένα αναζητήσιμο ευρετήριο στο GroupDocs.Search. Φορτώνετε ή δημιουργείτε μια παρουσία `Index` δείχνοντας σε έναν φάκελο στο δίσκο· η βιβλιοθήκη διαχειρίζεται όλα τα εσωτερικά αρχεία για εσάς. Αυτό το βήμα είναι η βάση για **βελτιστοποίηση της απόδοσης της αναζήτησης** επειδή ένα καλά δομημένο ευρετήριο μειώνει την καθυστέρηση ερωτημάτων.

```csharp
using GroupDocs.Search;

string indexFolder = "YOUR_DOCUMENT_DIRECTORY/HelloWorldIndex";
```

**Επεξήγηση:** Ο κώδικας ορίζει τον φάκελο που θα περιέχει τα αρχεία του ευρετηρίου. Η χρήση ενός αφιερωμένου φακέλου διατηρεί τα δεδομένα του ευρετηρίου απομονωμένα από τα πηγαία έγγραφά σας.

```csharp
Index index = new Index(indexFolder);
```

**Επεξήγηση:** Η δημιουργία μιας στιγμής `Index` είτε ανοίγει ένα υπάρχον ευρετήριο είτε δημιουργεί ένα νέο αν η διαδρομή είναι κενή.

### Πώς να προσθέσετε έγγραφα στο ευρετήριο μετά τη διαγραφή;

Πρώτα, διαγράψτε τυχόν εμπιστευτικές ενότητες, στη συνέχεια εισάγετε το καθαρό αρχείο στο ευρετήριο. Αυτή η διπλή διαδικασία εγγυάται ότι μόνο ασφαλές περιεχόμενο είναι αναζητήσιμο.

#### Ορίστε το φάκελο προέλευσης
`documentsFolder` είναι η διαδρομή όπου βρίσκονται τα αρχικά PDF σας.

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY/HelloWorldDocuments";
```

`AddDocument` είναι μια μέθοδος της κλάσης `Index` που προσθέτει ένα μόνο έγγραφο στο ευρετήριο.

```csharp
index.Add(documentsFolder);
```

### Πώς να αναζητήσετε μέσα στο δημιουργημένο ευρετήριο;

Καθορίστε μια συμβολοσειρά ερωτήματος, εκτελέστε την αναζήτηση και επαναλάβετε τα αποτελέσματα. Το API επιστρέφει αριθμούς σελίδων, αποσπάσματα και αναγνωριστικά εγγράφων, καθιστώντας εύκολο το παρουσίαση των αποτελεσμάτων σε UI.

`SearchResult` περιέχει τα αποτελέσματα που επιστρέφει ένα ερώτημα, συμπεριλαμβανομένων των ταιριασμένων εγγράφων και αποσπασμάτων.

```csharp
string query = "Lorem";
```

```csharp
SearchResult result = index.Search(query);
```

## Πρακτικές Εφαρμογές

Αυτές οι δυνατότητες λύνουν προβλήματα του πραγματικού κόσμου:

1. **Legal Document Management** – Διαγράψτε τα ονόματα πελατών πριν την δεικτοδότηση των φακέλων υποθέσεων, εξασφαλίζοντας το απόρρητο ενώ οι δικηγόροι μπορούν ακόμη να αναζητήσουν τη νομολογία.  
2. **Healthcare Records** – Αφαιρέστε τα αναγνωριστικά ασθενών από ιατρικά PDF, στη συνέχεια δεικτοδοτήστε τις αποκαθαρισμένες εκδόσεις για γρήγορα ερωτήματα ελέγχου.  
3. **Corporate Compliance** – Αυτοματοποιήστε τη διαγραφή οικονομικών καταστάσεων και άμεσα κάντε τις καθαρές εκδόσεις αναζητήσιμες για εσωτερικές έρευνες.

## Παράγοντες Απόδοσης

Για **βελτιστοποίηση της απόδοσης της αναζήτησης** όταν διαχειρίζεστε μεγάλους όγκους:

- Εκτελέστε τη δεικτοδότηση ως εργασία παρασκηνίου και δεσμεύστε τις αλλαγές σε παρτίδες.  
- Αποδεσμεύστε άμεσα τα αντικείμενα `Index` για να ελευθερώσετε μη διαχειριζόμενους πόρους.  
- Παρακολουθήστε τη χρήση μνήμης· το GroupDocs.Search μεταδίδει δεδομένα και δεν φορτώνει ποτέ ολόκληρο το έγγραφο στη RAM.  
- Προγραμματίστε περιοδικές συγχωνεύσεις ευρετηρίου για να διατηρείτε το ευρετήριο συμπαγές και γρήγορο στην ερώτηση.

## Κοινά Προβλήματα και Λύσεις

| Πρόβλημα | Λύση |
|----------|------|
| **Σφάλματα έλλειψης μνήμης σε τεράστια PDF** | Χρησιμοποιήστε το `RedactionEngine` με `RedactionOptions` που ενεργοποιούν τη λειτουργία streaming. |
| **Η αναζήτηση επιστρέφει διαγραμμένους όρους** | Βεβαιωθείτε ότι εκτελείτε τη διαγραφή **πριν** καλέσετε το `Index.AddDocument`. |
| **Μη υποστηριζόμενη μορφή αρχείου** | Επαληθεύστε ότι η επέκταση του αρχείου είναι μεταξύ των 50+ υποστηριζόμενων μορφών· μετατρέψτε πρώτα τα μη υποστηριζόμενα αρχεία σε PDF. |
| **Η άδεια δεν αναγνωρίζεται** | Τοποθετήστε το αρχείο άδειας στη ρίζα της εφαρμογής και καλέστε `License.SetLicense("license.json")` πριν από οποιαδήποτε χρήση του API. |

## Συχνές Ερωτήσεις

**Q: Μπορώ να διαγράψω αρχεία PDF C# απευθείας χωρίς να τα μετατρέψω πρώτα;**  
A: Ναι—`RedactionEngine` λειτουργεί εγγενώς με ροές PDF, έτσι μπορείτε να φορτώσετε ένα PDF, να εφαρμόσετε αντικείμενα διαγραφής και να αποθηκεύσετε το αποτέλεσμα χωρίς καμία μετατροπή μορφής.

**Q: Πώς η προσθήκη εγγράφων στο ευρετήριο επηρεάζει την ταχύτητα αναζήτησης;**  
A: Η σταδιακή δεικτοδότηση προσθέτει μόνο τα νέα αρχεία, διατηρώντας το μέγεθος του ευρετηρίου σταθερό και την καθυστέρηση ερωτημάτων κάτω από 200 ms για τυπικά φορτία εργασίας.

**Q: Είναι δυνατόν να προγραμματίσετε αυτόματη επαν-δεικτοδότηση;**  
A: Απόλυτα. Χρησιμοποιήστε μια υπηρεσία Windows ή Azure Function για να καλέσετε το `Index.AddDocument` με χρονοδιακόπτη, τροφοδοτώντας τα νεοανεβασμένα αρχεία στο ευρετήριο.

**Q: Η διαγραφή αφαιρεί μόνιμα τα κρυμμένα δεδομένα;**  
A: Ναι—η διαγραφή αντικαθιστά τα αρχικά bytes, καθιστώντας την ανάκτηση αδύνατη ακόμη και με εργαλεία forensics.

**Q: Ποιες εκδόσεις του .NET υποστηρίζονται πλήρως;**  
A: Τanto .NET Framework 4.6.1+ όσο και .NET Core 3.1+ (συμπεριλαμβανομένων .NET 5/6) υποστηρίζονται επίσημα.

## Πόροι
- [Τεκμηρίωση](https://docs.groupdocs.com/search/net/)
- [Αναφορά API](https://reference.groupdocs.com/redaction/net)
- [Λήψη](https://releases.groupdocs.com/search/net/)
- [Δωρεάν Υποστήριξη](https://forum.groupdocs.com/c/search/10)
- [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία Ενημέρωση:** 2026-07-02  
**Δοκιμή με:** GroupDocs.Search 21.2 και GroupDocs.Redaction 21.1 για .NET  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Αποκτώντας Δεξιότητες στο GroupDocs.Redaction .NET: Αποτελεσματική Δημιουργία Ευρετηρίου και Διαχείριση Ψευδώνυμων για Προηγμένη Αναζήτηση Εγγράφων](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Πώς να Δεικτοδοτήσετε και να Αναζητήσετε Έγγραφα PDF/Word κατά Θέμα Χρησιμοποιώντας το GroupDocs.Redaction σε .NET](/search/net/indexing/index-search-pdf-word-subject-groupdocs-redaction/)
- [Αποκτώντας Δεξιότητες στο GroupDocs Search και Redaction σε .NET: Προηγμένη Διαχείριση Εγγράφων](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)