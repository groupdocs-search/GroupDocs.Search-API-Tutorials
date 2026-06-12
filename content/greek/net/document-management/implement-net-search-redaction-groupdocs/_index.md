---
date: '2026-06-12'
description: Μάθετε πώς να κάνετε αναζήτηση και απόκρυψη εγγράφων στο .NET με το GroupDocs.Search
  και το GroupDocs.Redaction, βελτιώνοντας την απόδοση της αναζήτησης και αντιμετωπίζοντας
  σφάλματα ευρετηρίου.
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Πώς να κάνετε αναζήτηση και απόκρυψη εγγράφων στο .NET χρησιμοποιώντας το GroupDocs.Search
  και το GroupDocs.Redaction
type: docs
url: /el/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# Αναζήτηση και Απόκρυψη Εγγράφων σε .NET με GroupDocs.Search & GroupDocs.Redaction

Σε σύγχρονα επιχειρηματικά περιβάλλοντα, οι δυνατότητες **search and redact** είναι απαραίτητες για την προστασία ευαίσθητων πληροφοριών ενώ τα έγγραφα παραμένουν εύκολα αναγνώσιμα. Αυτό το εκπαιδευτικό υλικό σας καθοδηγεί στη δημιουργία μιας ισχυρής λύσης .NET που συνδυάζει το GroupDocs.Search για γρήγορη πλήρη‑κείμενο αναζήτηση με το GroupDocs.Redaction για ασφαλή αφαίρεση εμπιστευτικών δεδομένων. Στο τέλος, θα γνωρίζετε πώς να ρυθμίσετε τις βιβλιοθήκες, να δημιουργήσετε έναν προσαρμοσμένο διαχωριστή κειμένου, να εκτελείτε υψηλής απόδοσης αναζητήσεις και να εφαρμόζετε αποκαλύψεις με ασφάλεια.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “search and redact”;** Σημαίνει την εύρεση κειμένου σε έγγραφα και τη μόνιμη απόκρυψή του.  
- **Ποιες βιβλιοθήκες απαιτούνται;** GroupDocs.Search και GroupDocs.Redaction για .NET.  
- **Μπορώ να διαχειριστώ πολυγλωσσικό περιεχόμενο;** Ναι—χρησιμοποιήστε έναν προσαρμοσμένο διαχωριστή κειμένου για σωστό διαχωρισμό των λέξεων.  
- **Πώς βελτιώνω την ταχύτητα αναζήτησης;** Δημιουργήστε το ευρετήριο μία φορά, επαναχρησιμοποιήστε το και ενεργοποιήστε τις ρυθμίσεις `optimize search performance`.  
- **Τι γίνεται αν η δημιουργία ευρετηρίου αποτύχει;** Ακολουθήστε τις οδηγίες “handle indexing errors” στην ενότητα αντιμετώπισης προβλημάτων.

## Τι είναι το “search and redact”;
Η διαδικασία “search and redact” εντοπίζει συγκεκριμένους όρους μέσα σε μια συλλογή εγγράφων και στη συνέχεια τους αποκρύπτει ή αφαιρεί μόνιμα για την προστασία της ιδιωτικότητας ή τη συμμόρφωση με κανονισμούς. Συνδυάζει την πλήρη‑κείμενο αναζήτηση για την εύρεση ευαίσθητων πληροφοριών με εργαλεία απόκρυψης που αντικαθιστούν το περιεχόμενο διατηρώντας τη διάταξη του εγγράφου.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search και το GroupDocs.Redaction μαζί;
Το GroupDocs.Search υποστηρίζει **πάνω από 50 μορφές αρχείων** και μπορεί να ευρετηριάσει **πάνω από 100.000 έγγραφα** σε λιγότερο από ένα λεπτό σε τυπικό εξοπλισμό διακομιστή, ενώ το GroupDocs.Redaction μπορεί να εφαρμόσει αποκαλύψεις σε **PDF, DOCX, PPTX και άλλα** χωρίς να αλλάξει την αρχική διάταξη. Η συνδυαστική χρήση τους προσφέρει μια ενιαία λύση που **βελτιστοποιεί την απόδοση της αναζήτησης** και **χειρίζεται τα σφάλματα ευρετηρίου** με ευελιξία.

## Προαπαιτούμενα
- Visual Studio 2022 ή νεότερο με υποστήριξη .NET 6+.  
- Πακέτα NuGet: **GroupDocs.Search** και **GroupDocs.Redaction** (τελευταίες σταθερές εκδόσεις).  
- Ένα έγκυρο άδεια GroupDocs (δοκιμαστική ή αγορασμένη).  

### Απαιτούμενες Βιβλιοθήκες
- **GroupDocs.Search** – Παρέχει ευρετηρίαση, ερωτήματα και προσαρμοσμένη τμηματοποίηση.  
- **GroupDocs.Redaction** – Προσφέρει απόκρυψη κειμένου, εικόνας και μεταδεδομένων σε υποστηριζόμενες μορφές.

### Απαιτήσεις Ρύθμισης Περιβάλλοντος
Βεβαιωθείτε ότι ο υπολογιστής ανάπτυξης έχει δικαιώματα εγγραφής στον φάκελο όπου θα αποθηκευτεί το ευρετήριο.

### Προαπαιτούμενες Γνώσεις
- Εξοικείωση με C# και τη δομή έργων .NET.  
- Βασική κατανόηση των εννοιών επεξεργασίας εγγράφων (προαιρετικό αλλά χρήσιμο).

## Πώς να εγκαταστήσω το GroupDocs.Redaction για .NET;
Μπορείτε να προσθέσετε το πακέτο Redaction στο έργο σας χρησιμοποιώντας είτε το .NET CLI είτε το NuGet Package Manager. Η εντολή κατεβάζει την πιο πρόσφατη σταθερή έκδοση και την καταχωρεί στο αρχείο του έργου, καθιστώντας το API άμεσα διαθέσιμο.

```bash
dotnet add package GroupDocs.Redaction
```  

## Πώς να αποκτήσω άδεια για το GroupDocs;
Το GroupDocs προσφέρει τρεις επιλογές αδειοδότησης: δωρεάν δοκιμαστική άδεια για αξιολόγηση, προσωρινή άδεια για εκτεταμένη δοκιμή ανάπτυξης και πλήρη εμπορική άδεια για παραγωγική χρήση. Η δοκιμαστική άδεια παρέχει περιορισμένη λειτουργικότητα, ενώ το προσωρινό κλειδί επεκτείνει την περίοδο αξιολόγησης, και η αγορασμένη άδεια ξεκλειδώνει όλες τις δυνατότητες και την προτεραιότητα υποστήριξης.

## Πώς να αρχικοποιήσω το GroupDocs.Redaction στην εφαρμογή μου;
Η κλάση `Redaction` είναι το κύριο σημείο εισόδου για την εφαρμογή αποκαλύψεων σε υποστηριζόμενα έγγραφα. Φορτώνει ένα αρχείο, προετοιμάζει αντικείμενα αποκαλύψεων και εκτελεί τη διαδικασία, επιστρέφοντας ένα τροποποιημένο έγγραφο ενώ διατηρεί την αρχική διάταξη. Μπορείτε επίσης να ρυθμίσετε επιλογές αποκαλύψεων όπως χρώμα, επικάλυψη και αφαίρεση μεταδεδομένων για να καλύψετε συγκεκριμένες απαιτήσεις συμμόρφωσης.

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## Πώς να δημιουργήσω ένα ευρετήριο χρησιμοποιώντας το GroupDocs.Search;
Η κλάση `Index` αντιπροσωπεύει ένα αποθηκευμένο αποθετήριο που μπορεί να αναζητηθεί. Διαχειρίζεται τη δημιουργία, την ενημέρωση και την ερώτηση του ευρετηρίου, επιτρέποντάς σας να προσθέτετε έγγραφα, να ξαναχτίζετε το ευρετήριο και να εκτελείτε γρήγορες αναζητήσεις σε μεγάλες συλλογές. Ο φάκελος του ευρετηρίου μπορεί να βρίσκεται σε τοπική ή δικτυακή αποθήκευση, και μπορείτε να ρυθμίσετε συμπίεση και κρυπτογράφηση για την προστασία των δεδομένων.

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## Τι είναι ένας προσαρμοσμένος διαχωριστής κειμένου και γιατί πρέπει να τον χρησιμοποιήσω;
Ένας προσαρμοσμένος διαχωριστής κειμένου καθορίζει πώς το ακατέργαστο κείμενο θα χωριστεί σε αναζητήσιμα tokens. Προσαρμόζοντας τους κανόνες τμηματοποίησης για συγκεκριμένες γλώσσες ή τομείς, βελτιώνετε την ακρίβεια της τμηματοποίησης, οδηγώντας σε υψηλότερη ανάκληση και συνάφεια στα αποτελέσματα αναζήτησης. Αυτό είναι ιδιαίτερα χρήσιμο για γλώσσες με σύνθετα όρια λέξεων, όπως τα ιαπωνικά ή τα αραβικά, όπου οι προεπιλεγμένοι διαχωριστές μπορεί να χωρίζουν λανθασμένα τις λέξεις.

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## Πώς να εκτελέσω αναζήτηση πλήρους κειμένου με τον προσαρμοσμένο διαχωριστή;
Το αντικείμενο `SearchQuery` ενσωματώνει το ερώτημα του χρήστη και συνεργάζεται με τον προσαρμοσμένο διαχωριστή για την εύρεση αντιστοιχιών. Υποστηρίζει fuzzy matching, φράσεις ερωτημάτων και βαρύτητα, επιστρέφοντας ένα σύνολο αποτελεσμάτων με IDs εγγράφων, θέσεις εμφάνισης και βαθμολογίες συνάφειας. Μπορείτε επίσης να εφαρμόσετε φίλτρα όπως τύπο αρχείου ή χρονικό εύρος για να περιορίσετε τα αποτελέσματα και να στοχεύσετε πιο ακριβώς.

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## Πώς να εφαρμόσω αποκαλύψεις μετά την εύρεση ευαίσθητου κειμένου;
Το API `Redaction` σας επιτρέπει να αντικαταστήσετε ή να αφαιρέσετε κείμενο, εικόνες και μεταδεδομένα σε υποστηριζόμενα έγγραφα. Αφού εντοπίσετε τους ευαίσθητους όρους, δημιουργείτε αντικείμενα αποκαλύψεων, τα εφαρμόζετε και αποθηκεύετε το αρχείο με αποκαλύψεις, διασφαλίζοντας ότι οι εμπιστευτικές πληροφορίες κρύβονται μόνιμα. Οι επιλογές αποκαλύψεων περιλαμβάνουν επικάλυψη με μαύρα κουτιά, προσαρμοσμένα χρώματα ή αφαίρεση ολόκληρων αντικειμένων διατηρώντας τη δομή του εγγράφου.

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## Συνηθισμένα προβλήματα και πώς να αντιμετωπίσετε σφάλματα ευρετηρίου
- **Index Not Found:** Επαληθεύστε ότι η διαδρομή του ευρετηρίου υπάρχει και ότι η εφαρμογή έχει δικαιώματα ανάγνωσης/εγγραφής.  
- **Search Returns No Results:** Εκτελέστε ξανά τη διαδικασία ευρετηρίου και βεβαιωθείτε ότι ο προσαρμοσμένος διαχωριστής είναι σωστά καταχωρημένος.  
- **Redaction Fails on Certain Formats:** Επιβεβαιώστε ότι ο τύπος αρχείου υποστηρίζεται· για PDF, χρησιμοποιήστε την πιο πρόσφατη έκδοση Redaction για να διαχειριστείτε τις δυνατότητες PDF 2.0.

## Πρακτικές Εφαρμογές
1. **Διαχείριση νομικών εγγράφων:** Αναζητήστε συμβάσεις για “non‑disclosure” και αυτόματα αποκρύψτε τις σχετικές ρήτρες πριν την εξωτερική κοινοποίηση.  
2. **Ακαδημαϊκή έρευνα:** Εντοπίστε αδημοσίευτα δεδομένα σε χειρόγραφα και κρύψτε τα για διαδικασίες αξιολόγησης από ομοτίμους.  
3. **Επιχειρηματικές συμβάσεις:** Επεξεργαστείτε χιλιάδες συμφωνίες μαζικά, αποκρύπτοντας προσωπικά αναγνωριστικά ενώ διατηρείτε τη νομική γλώσσα.

## Πώς μπορώ να βελτιστοποιήσω την απόδοση της αναζήτησης για μεγάλα σύνολα εγγράφων;
Για μέγιστη απόδοση, ευρετηριάστε τα έγγραφα μία φορά και επαναχρησιμοποιήστε το ίδιο ευρετήριο για επόμενα ερωτήματα. Ενεργοποιήστε την παράλληλη επεξεργασία, ρυθμίστε την προσωρινή αποθήκευση (caching) και βελτιστοποιήστε τις ρυθμίσεις του ευρετηρίου ώστε να μειώσετε την καθυστέρηση και να αυξήσετε το throughput σε διακομιστές πολλαπλών πυρήνων. Επιπλέον, ορίστε τη σημαία `EnableMemoryMapping` για να επιτρέψετε τη μνήμη‑χαρτογράφηση του ευρετηρίου, κάτι που επιταχύνει τις λειτουργίες ανάγνωσης για μεγάλα σύνολα δεδομένων.

## Πώς να διαχειριστώ τη μνήμη .NET όταν εργάζομαι με μεγάλα αρχεία;
Η αποδοτική διαχείριση μνήμης είναι κρίσιμη όταν επεξεργάζεστε μεγάλα έγγραφα. Περιβάλλετε τα αντικείμενα `Index` και `Redaction` σε δηλώσεις `using` ώστε να εξασφαλίζετε καθοριστική απελευθέρωση, και επεξεργαστείτε τα αρχεία ως streams αντί να φορτώνετε ολόκληρα τα έγγραφα στη μνήμη. Η παρακολούθηση μετρητών απόδοσης βοηθά στον εντοπισμό αυξήσεων μνήμης νωρίς, επιτρέποντάς σας να προσαρμόσετε το μέγεθος παρτίδων ή να ρυθμίσετε το garbage collection.

## Συχνές Ερωτήσεις
**Ε: Μπορώ να χρησιμοποιήσω το GroupDocs.Search με μη‑κειμενικά μεταδεδομένα;**  
Α: Ναι—τα πεδία μεταδεδομένων μπορούν να ευρετηριαστούν μαζί με το περιεχόμενο του εγγράφου, επιτρέποντας αναζητήσεις όπως “author:JohnDoe”.

**Ε: Το GroupDocs.Redaction υποστηρίζει αποκαλύψεις σε πραγματικό χρόνο σε web API;**  
Α: Ναι· μπορείτε να καλέσετε το Redaction API συγχρονισμένα για μικρά αρχεία ή να βάλετε σε ουρά μεγαλύτερες εργασίες για ασύγχρονη επεξεργασία.

**Ε: Τι πρέπει να κάνω αν το ευρετήριο καταστραφεί;**  
Α: Διαγράψτε τον φάκελο του κατεστραμμένου ευρετηρίου και ξαναχτίστε το χρησιμοποιώντας την ίδια διαδικασία ευρετηρίου· η βιβλιοθήκη καταγράφει λεπτομερή μηνύματα σφάλματος για να σας βοηθήσει να εντοπίσετε την αιτία.

**Ε: Είναι δυνατόν να προεπισκοπήσετε τα έγγραφα με αποκαλύψεις πριν την αποθήκευση;**  
Α: Απόλυτα—καλέστε `redaction.Apply()` με τη σημαία `preview` για να δημιουργήσετε μια προσωρινή έκδοση προς έλεγχο.

**Ε: Ποιες εκδόσεις .NET υποστηρίζονται επίσημα;**  
Α: Το GroupDocs.Search και το GroupDocs.Redaction υποστηρίζουν .NET 6, .NET 5, .NET Core 3.1 και .NET Framework 4.6.2+.

## Πόροι
- **Τεκμηρίωση:** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **Αναφορά API:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Λήψη:** [GroupDocs Releases](https://releases.groupdocs.com/search/net/)
- **Δωρεάν Υποστήριξη:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Προσωρινή Άδεια:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία ενημέρωση:** 2026-06-12  
**Δοκιμάστηκε με:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**Συγγραφέας:** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## Σχετικά Μαθήματα
- [Απόκτηση δεξιοτήτων GroupDocs Search και Redaction σε .NET: Προηγμένη Διαχείριση Εγγράφων](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
- [Υλοποίηση GroupDocs.Search & Redaction: Ενημέρωση και Διαχείριση Ευρετηρίων Εγγράφων σε .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [Βελτιστοποίηση Ευρετηρίου Εγγράφων σε .NET με GroupDocs.Redaction: Ακύρωση, Ασύγχρονη Επεξεργασία και Νήματα](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)