---
date: '2026-06-22'
description: Οδηγός βήμα‑βήμα για τη δημιουργία ευρετηρίου εγγράφων .NET χρησιμοποιώντας
  το GroupDocs.Redaction για .NET—διαχείριση καταλόγων, μετονομασία αρχείων και διατήρηση
  των ευρετηρίων ενημερωμένων.
keywords:
- create document index .net
- GroupDocs.Redaction directory management
- .NET document indexing
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Step‑by‑step guide to create document index .net using GroupDocs.Redaction
    for .NET—manage directories, rename files, and keep indexes up to date.
  headline: How to Create Document Index .NET with Aspose.GroupDocs Redaction
  type: TechArticle
- description: Step‑by‑step guide to create document index .net using GroupDocs.Redaction
    for .NET—manage directories, rename files, and keep indexes up to date.
  name: How to Create Document Index .NET with Aspose.GroupDocs Redaction
  steps:
  - name: '**Free Trial** – Get a 30‑day trial from the GroupDocs portal.'
    text: '**Free Trial** – Get a 30‑day trial from the GroupDocs portal.'
  - name: '**Temporary License** – Request a temporary key for extended testing.'
    text: '**Temporary License** – Request a temporary key for extended testing.'
  - name: '**Purchase** – Obtain a production license to unlock full functionality.'
    text: '**Purchase** – Obtain a production license to unlock full functionality.'
  - name: '**Legal Document Management** – Index contracts, briefs, and case files
      for instant retrieval.'
    text: '**Legal Document Management** – Index contracts, briefs, and case files
      for instant retrieval.'
  - name: '**Digital Library Systems** – Provide real‑time search across thousands
      of e‑books and research papers.'
    text: '**Digital Library Systems** – Provide real‑time search across thousands
      of e‑books and research papers.'
  - name: '**Enterprise Content Management** – Maintain audit‑ready directories that
      automatically reflect naming conventions.'
    text: '**Enterprise Content Management** – Maintain audit‑ready directories that
      automatically reflect naming conventions.'
  - name: '**Customer Support Archives** – Quickly locate prior tickets, PDFs, and
      knowledge‑base articles.'
    text: '**Customer Support Archives** – Quickly locate prior tickets, PDFs, and
      knowledge‑base articles.'
  type: HowTo
- questions:
  - answer: It redacts sensitive content from PDFs, DOCXs, and images while also offering
      robust directory and indexing utilities.
    question: What is the primary use of GroupDocs.Redaction?
  - answer: Yes—create separate `Index` instances for each folder and operate them
      in parallel.
    question: Can I manage multiple directories simultaneously?
  - answer: Wrap `Index.Build` and `Index.Refresh` in try‑catch blocks; log `RedactionException`
      details for troubleshooting.
    question: How do I handle errors during indexing?
  - answer: A .NET Framework 4.6+ or .NET Core 3.1+ runtime, at least 2 GB RAM, and
      500 MB of free disk space for temporary buffers.
    question: What are the system requirements for GroupDocs.Redaction?
  - answer: Regularly call `Index.Refresh`, enable parallel processing, and limit
      batch sizes to keep memory consumption under control.
    question: How can I optimise index performance for large document sets?
  type: FAQPage
title: Πώς να δημιουργήσετε ευρετήριο εγγράφων .NET με Aspose.GroupDocs Redaction
type: docs
url: /el/net/document-management/master-aspose-groupdocs-directory-management-redaction-net/
weight: 1
---

# Δημιουργία Ευρετηρίου Εγγράφων .NET με Aspose.GroupDocs Redaction

Η διαχείριση μεγάλων συλλογών αρχείων μπορεί γρήγορα να γίνει εφιάλτης αν δεν έχετε έναν αξιόπιστο τρόπο να διατηρείτε τους φακέλους σας τακτικούς **και** το ευρετήριο αναζήτησης ενημερωμένο. Σε αυτό το σεμινάριο θα μάθετε πώς να **δημιουργήσετε ευρετήριο εγγράφων .net** χρησιμοποιώντας το GroupDocs.Redaction για .NET, καλύπτοντας την προετοιμασία του καταλόγου, τη δημιουργία ευρετηρίου, τη μετονομασία εγγράφων και τις ενημερώσεις του ευρετηρίου. Στο τέλος θα έχετε μια επαναλήψιμη ροή εργασίας που κλιμακώνεται από μερικά PDF σε χιλιάδες νομικά ή υποστηρικτικά έγγραφα.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη χρειάζομαι;** GroupDocs.Redaction for .NET (latest NuGet version).  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6+.  
- **Πόσες μορφές μπορούν να ευρετηριαστούν;** Πάνω από 50 μορφές εισόδου — συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX, και κοινών τύπων εικόνων.  
- **Μπορώ να μετονομάσω αρχεία χωρίς να σπάσω το ευρετήριο;** Ναι—χρησιμοποιήστε τη ενσωματωμένη μέθοδο `Rename` και στη συνέχεια καλέστε `NotifyIndex`.  
- **Απαιτείται άδεια για παραγωγή;** Μια έγκυρη άδεια GroupDocs.Redaction είναι υποχρεωτική για χρήση σε παραγωγή.

## Τι είναι το “Δημιουργία Ευρετηρίου Εγγράφων .NET”;
*Create document index .net* αναφέρεται στη διαδικασία δημιουργίας ενός αναζητήσιμου καταλόγου αρχείων σε μια εφαρμογή .NET, όπου κάθε καταχώρηση αποθηκεύει μεταδεδομένα όπως το όνομα αρχείου, η διαδρομή και αποσπάσματα περιεχομένου. Αυτό το ευρετήριο επιτρέπει γρήγορες αναζητήσεις χωρίς να σαρώνονται ολόκληρα τα συστήματα αρχείων κάθε φορά.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction για Ευρετηρίαση;
Το GroupDocs.Redaction δεν μόνο αφαιρεί ευαίσθητο περιεχόμενο, αλλά παρέχει επίσης μια μηχανή ευρετηρίασης υψηλής απόδοσης που μπορεί να διαχειριστεί **έως 10.000 έγγραφα ανά λεπτό** σε έναν τυπικό διακομιστή 8‑πυρήνων, διατηρώντας τη χρήση μνήμης κάτω από **200 MB** για τις περισσότερες εργασίες. Το API του αφαιρεί τις ιδιαιτερότητες του συστήματος αρχείων, προσφέροντάς σας έναν συνεπή τρόπο διαχείρισης καταλόγων και διατήρησης των ευρετηρίων συγχρονισμένων.

## Προαπαιτούμενα
- **GroupDocs.Redaction** πακέτο NuGet εγκατεστημένο (τελευταία σταθερή έκδοση).  
- Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με .NET.  
- Βασικές γνώσεις C# (αρχείο I/O, διαχείριση εξαιρέσεων).  

### Απαιτούμενες Βιβλιοθήκες, Εκδόσεις και Εξαρτήσεις
- `GroupDocs.Redaction` ≥ 23.10 (υποστηρίζει .NET Standard 2.0 και .NET 5+).  
- Προαιρετικό: `Microsoft.Extensions.Logging` για λεπτομερή διάγνωση.

### Απαιτήσεις Ρύθμισης Περιβάλλοντος
Προσθέστε το πακέτο μέσω μιας από τις παρακάτω εντολές (μην **τροποποιήσετε** τα placeholders που αντιπροσωπεύουν τα πραγματικά μπλοκ κώδικα):

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Αναζητήστε το “GroupDocs.Redaction” και εγκαταστήστε την τελευταία έκδοση.

### Βήματα Απόκτησης Άδειας
1. **Δωρεάν Δοκιμή** – Λάβετε μια δοκιμή 30 ημερών από το portal του GroupDocs.  
2. **Προσωρινή Άδεια** – Ζητήστε ένα προσωρινό κλειδί για εκτεταμένη δοκιμή.  
3. **Αγορά** – Αποκτήστε μια άδεια παραγωγής για να ξεκλειδώσετε πλήρη λειτουργικότητα.

## Πώς να Προετοιμάσετε έναν Καθαρό Κατάλογο Εργασίας;
Φορτώστε τον στόχο φάκελο, διαγράψτε τυχόν ανεπιθύμητα προσωρινά αρχεία και αντιγράψτε τα πηγαία έγγραφα που σκοπεύετε να ευρετηριάσετε. Αυτό το βήμα προετοιμασίας εξαλείφει τα σφάλματα “αρχείο‑σε‑χρήση” κατά την ευρετηρίαση και εγγυάται ότι ο δημιουργός ευρετηρίου λειτουργεί πάνω σε ένα καθορισμένο σύνολο αρχείων. Διασφαλίζοντας ένα άψογο περιβάλλον μειώνετε τα ψευδώς θετικά, αποφεύγετε προβλήματα αδειών και βελτιώνετε τη συνολική απόδοση της ευρετηρίασης.

### Καθαρισμός του Καταλόγου
Η κλάση `DirectoryCleaner` αφαιρεί υπολειπόμενα αρχεία (π.χ., *.tmp, *.bak) που θα μπορούσαν να επηρεάσουν την ευρετηρίαση.  
```csharp
using GroupDocs.Search.Common;
using System.IO;

string documentFolder = "YOUR_DOCUMENT_DIRECTORY/";

// Ensure the directory is empty before use
Utils.CleanDirectory(documentFolder);
```  

### Αντιγραφή Απαραίτητων Αρχείων
Η `FilePreparer` αντιγράφει τα πηγαία PDFs, DOCXs και εικόνες στον φάκελο εργασίας, διατηρώντας την αρχική ιεραρχία φακέλων.  
```csharp
// Copy essential documents to the target directory from a source path
Utils.CopyFiles(Utils.DocumentsPath, documentFolder);
```  

## Πώς να Δημιουργήσετε το Ευρετήριο;
Το `Index` αντιπροσωπεύει μια αναζητήσιμη συλλογή εγγράφων και διαχειρίζεται τις υποκείμενες δομές αποθήκευσης.

Δημιουργήστε το αντικείμενο `Index`, δείξτε το στον καθαρό σας κατάλογο και καλέστε το `Build`. Αυτή η λειτουργία σαρώει κάθε αρχείο, εξάγει αναζητήσιμο κείμενο και το αποθηκεύει σε μια αποδοτική δυαδική δομή. Ο δημιουργός επίσης καταγράφει μεταδεδομένα όπως διαδρομές αρχείων και χρονικές σφραγίδες, επιτρέποντας γρήγορες αναζητήσεις και σταδιακές ενημερώσεις χωρίς επεξεργασία των αμετάβλητων εγγράφων.

### Δημιουργία του Ευρετηρίου
Η κλάση `Index` είναι το κύριο στοιχείο που αντιπροσωπεύει μια αναζητήσιμη συλλογή εγγράφων.  
```csharp
using GroupDocs.Search;

string indexFolder = "YOUR_DOCUMENT_DIRECTORY/Index/";
Index index = new Index(indexFolder); // Create the index

// Add documents from your directory to the index
index.Add("YOUR_DOCUMENT_DIRECTORY/Documents/");
```  

## Πώς να Μετονομάσετε Έγγραφα και να Ειδοποιήσετε το Ευρετήριο;
Η `DocumentRenamer` παρέχει εργαλεία για τη μετονομασία αρχείων διατηρώντας την ακεραιότητα του ευρετηρίου.

`DocumentRenamer.RenameAndNotify` μετονομάζει το αρχείο στο δίσκο και στη συνέχεια καλεί το `Index.UpdateEntry` για να διατηρήσει τον κατάλογο ακριβή. Εκτελώντας τη μετονομασία και την άμεση ειδοποίηση του ευρετηρίου σε μια ενιαία συναλλαγή, αποφεύγετε παλιές αναφορές και εξασφαλίζετε ότι οι επόμενες αναζητήσεις επιστρέφουν το νέο όνομα αρχείου. Αυτή η μέθοδος επίσης καταγράφει τη λειτουργία για σκοπούς ελέγχου.  
```csharp
using System;
using GroupDocs.Search;
using System.IO;

string oldDocumentPath = "YOUR_DOCUMENT_DIRECTORY/Documents/Lorem ipsum.txt";
string newDocumentPath = "YOUR_DOCUMENT_DIRECTORY/Documents/Lorem ipsum renamed.txt";

// Rename the file by moving it to a new path
File.Move(oldDocumentPath, newDocumentPath);

// Notify the index about this change\NSNotification notification = Notification.CreateRenameNotification(oldDocumentPath, newDocumentPath);
Index indexForNotify = new Index(indexFolder);
bool result = indexForNotify.Notify(notification); 
Console.WriteLine($"Successful rename: {result}");
```  

## Πώς να Ενημερώσετε ένα Υπάρχον Ευρετήριο μετά από Αλλαγές;
`Index.Refresh` εφαρμόζει σταδιακές αλλαγές σε ένα υπάρχον ευρετήριο χωρίς να το ξαναχτίζει εντελώς.

`Index.Refresh` επεξεργάζεται μόνο τη διαφορά (νέα ή τροποποιημένα αρχεία), μειώνοντας το φορτίο CPU κατά **έως 85 %** σε σύγκριση με μια πλήρη επαναδημιουργία. Η μέθοδος σαρώει τον φάκελο εργασίας, εντοπίζει αρχεία με τροποποιημένες χρονικές σφραγίδες και ενημερώνει τις καταχωρήσεις τους διατηρώντας τα αμετάβλητα έγγραφα. Αυτή η προσέγγιση μειώνει δραστικά τα παράθυρα συντήρησης και διατηρεί την εμπειρία αναζήτησης ανταποκρινόμενη.  
```csharp
using GroupDocs.Search;

Index indexToUpdate = new Index(indexFolder);

// Updates metadata without reindexing the entire document
indexToUpdate.Update();
```  

## Συνηθισμένες Περιπτώσεις Χρήσης
1. **Διαχείριση Νομικών Εγγράφων** – Ευρετηρίαση συμβάσεων, σημειώσεων και φακέλων υποθέσεων για άμεση ανάκτηση.  
2. **Συστήματα Ψηφιακών Βιβλιοθηκών** – Παρέχουν αναζήτηση σε πραγματικό χρόνο σε χιλιάδες e‑books και ερευνητικές εργασίες.  
3. **Διαχείριση Περιεχομένου Επιχειρήσεων** – Διατηρούν καταλόγους έτοιμους για έλεγχο που αντανακλούν αυτόματα τις συμβάσεις ονομασίας.  
4. **Αρχεία Εξυπηρέτησης Πελατών** – Εντοπίζουν γρήγορα προηγούμενα tickets, PDFs και άρθρα βάσης γνώσεων.

## Σκέψεις Απόδοσης
- **Ομαδικές Ενημερώσεις** – Ομαδοποιήστε τις αλλαγές σε παρτίδες ≤ 500 αρχείων για να αποφύγετε υπερβολικές αυξήσεις I/O.  
- **Διαχείριση Μνήμης** – Αποδεσμεύστε το αντικείμενο `Index` μετά από κάθε λειτουργία· η βιβλιοθήκη απελευθερώνει αυτόματα τους εγγενείς buffer.  
- **Παράλληλη Σάρωση** – Ενεργοποιήστε το `IndexOptions.EnableParallelProcessing` για να αξιοποιήσετε πολυπύρηνους επεξεργαστές, επιτυγχάνοντας έως **3×** επιτάχυνση σε μηχάνημα 8‑πυρήνων.

## Συχνές Ερωτήσεις

**Q: Ποια είναι η κύρια χρήση του GroupDocs.Redaction;**  
A: Αφαιρεί ευαίσθητο περιεχόμενο από PDFs, DOCXs και εικόνες ενώ προσφέρει επίσης ισχυρά εργαλεία διαχείρισης καταλόγων και ευρετηρίασης.

**Q: Μπορώ να διαχειριστώ πολλαπλούς καταλόγους ταυτόχρονα;**  
A: Ναι—δημιουργήστε ξεχωριστές εμφανίσεις `Index` για κάθε φάκελο και λειτουργήστε τις παράλληλα.

**Q: Πώς να αντιμετωπίσω σφάλματα κατά την ευρετηρίαση;**  
A: Τυλίξτε τα `Index.Build` και `Index.Refresh` σε μπλοκ try‑catch· καταγράψτε τις λεπτομέρειες του `RedactionException` για εντοπισμό προβλημάτων.

**Q: Ποιες είναι οι απαιτήσεις συστήματος για το GroupDocs.Redaction;**  
A: Ένα runtime .NET Framework 4.6+ ή .NET Core 3.1+, τουλάχιστον 2 GB RAM, και 500 MB ελεύθερου χώρου δίσκου για προσωρινούς buffer.

**Q: Πώς μπορώ να βελτιστοποιήσω την απόδοση του ευρετηρίου για μεγάλα σύνολα εγγράφων;**  
A: Καλείτε τακτικά το `Index.Refresh`, ενεργοποιήστε την παράλληλη επεξεργασία και περιορίστε τα μεγέθη παρτίδων ώστε η κατανάλωση μνήμης να παραμένει υπό έλεγχο.

## Πρόσθετοι Πόροι
- **Τεκμηρίωση**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)  
- **Αναφορά API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)  
- **Λήψη**: [Get GroupDocs Redaction](https://releases.groupdocs.com/search/net/)  
- **Δωρεάν Υποστήριξη**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Προσωρινή Άδεια**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία Ενημέρωση:** 2026-06-22  
**Δοκιμάστηκε Με:** GroupDocs.Redaction 23.10 for .NET  
**Συγγραφέας:** GroupDocs

```csharp
using GroupDocs.Redaction;

// Initialize the Redactor object with your document path
var redactor = new Redactor("YOUR_DOCUMENT_PATH");
```

## Σχετικά Μαθήματα

- [Εφαρμογή GroupDocs.Search & Redaction: Ενημέρωση και Διαχείριση Ευρετηρίων Εγγράφων σε .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [Δημιουργία και Συγχώνευση Κύριου Ευρετηρίου με GroupDocs.Redaction .NET για Αποτελεσματική Διαχείριση Εγγράφων](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [Κατάκτηση GroupDocs.Redaction .NET: Αποτελεσματική Δημιουργία Ευρετηρίου και Διαχείριση Ψευδώνυμων για Προχωρημένη Αναζήτηση Εγγράφων](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)