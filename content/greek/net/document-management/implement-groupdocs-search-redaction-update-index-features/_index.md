---
date: '2026-06-07'
description: Μάθετε πώς να ενημερώνετε το ευρετήριο αποδοτικά με το GroupDocs.Search
  και το Redaction για .NET, βελτιώνοντας το σύστημα διαχείρισης εγγράφων σας.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: Πώς να ενημερώσετε το ευρετήριο με το GroupDocs.Search & Redaction (.NET)
type: docs
url: /el/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# Πώς να ενημερώσετε το ευρετήριο με το GroupDocs.Search & Redaction (.NET)

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “πώς να ενημερώσετε το ευρετήριο”;** Είναι η διαδικασία τροποποίησης ενός υπάρχοντος ευρετηρίου αναζήτησης ώστε τα νέα ή τροποποιημένα έγγραφα να γίνονται αναζητήσιμα χωρίς επαναδημιουργία από την αρχή.  
- **Ποιες βιβλιοθήκες απαιτούνται;** GroupDocs.Search και GroupDocs.Redaction για .NET (και οι δύο διαθέσιμες μέσω NuGet).  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για δοκιμές· μια άδεια παραγωγής ξεκλειδώνει πλήρη λειτουργικότητα.  
- **Μπορώ να το τρέξω σε .NET Core;** Ναι, οι βιβλιοθήκες υποστηρίζουν .NET Framework 4.5+, .NET Core 3.1+ και .NET 5/6+.  
- **Τι απόδοση μπορώ να περιμένω;** Η ενημέρωση ενός ευρετηρίου 1 GB με 2 νήματα ολοκληρώνεται σε λιγότερο από ένα λεπτό σε έναν τυπικό διακομιστή 4‑πυρήνων.

## Τι είναι το “πώς να ενημερώσετε το ευρετήριο”;
**How to update index** αναφέρεται στην τεχνική εφαρμογής επαυξητικών αλλαγών σε ένα υπάρχον ευρετήριο αναζήτησης αντί για την πλήρη επαναδημιουργία του. Αυτή η προσέγγιση μειώνει το χρόνο διακοπής, εξοικονομεί κύκλους CPU και διατηρεί τα αποτελέσματα αναζήτησης φρέσκα καθώς προστίθενται, επεξεργάζονται ή αφαιρούνται έγγραφα.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search & Redaction για ενημερώσεις ευρετηρίου;
Το GroupDocs.Search υποστηρίζει **πάνω από 50 τύπους αρχείων** (PDF, DOCX, XLSX, PPTX, HTML, εικόνες κ.λπ.) και μπορεί να επεξεργαστεί έγγραφα πολλαπλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Σε συνδυασμό με το GroupDocs.Redaction, μπορείτε αυτόματα να αφαιρέσετε ή να καλύψετε ευαίσθητα δεδομένα πριν από την ευρετηρίαση, εξασφαλίζοντας συμμόρφωση ενώ διατηρείτε τη σχετικότητα της αναζήτησης.

## Προαπαιτούμενα

- **GroupDocs.Search** – εγκατάσταση μέσω NuGet.  
- **GroupDocs.Redaction for .NET** – απαιτείται για δυνατότητες επεξεργασίας.  
- Visual Studio (ή οποιοδήποτε .NET IDE) με εγκατεστημένο .NET 6+.  
- Βασικές γνώσεις C# και εξοικείωση με έννοιες ευρετηρίου.

### Απαιτούμενες Βιβλιοθήκες και Εκδόσεις
- **GroupDocs.Search** – η πιο πρόσφατη σταθερή έκδοση από το NuGet.  
- **GroupDocs.Redaction for .NET** – η πιο πρόσφατη σταθερή έκδοση από το NuGet.

### Απαιτήσεις Ρύθμισης Περιβάλλοντος
- Ένα μηχάνημα Windows ή Linux με εγκατεστημένο .NET SDK.  
- Πρόσβαση σε φάκελο όπου θα αποθηκευτούν τα αρχεία ευρετηρίου.

### Προαπαιτούμενες Γνώσεις
- Κατανόηση των βασικών αρχών ευρετηρίου εγγράφων και αναζήτησης.  
- Επίγνωση της διαχείρισης κύκλου ζωής εγγράφων σε επιχειρησιακά συστήματα.

## Ρύθμιση του GroupDocs.Redaction για .NET

### Εγκατάσταση των Πακέτων

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Αναζητήστε “GroupDocs.Redaction” και εγκαταστήστε την πιο πρόσφατη έκδοση.

### Βήματα Απόκτησης Άδειας
1. **Free Trial** – ξεκινήστε με μια δοκιμή για να εξερευνήσετε όλες τις δυνατότητες.  
2. **Temporary License** – ζητήστε ένα προσωρινό κλειδί για εκτεταμένη δοκιμή.  
3. **Purchase** – αποκτήστε πλήρη άδεια για παραγωγικές αναπτύξεις.

### Βασική Αρχικοποίηση και Ρύθμιση
`Redactor` είναι η βασική κλάση που εφαρμόζει κανόνες επεξεργασίας σε έγγραφα.  
Για να ξεκινήσετε, αναφερθείτε στο namespace Redaction και δημιουργήστε ένα αντικείμενο `Redactor`:

```csharp
using GroupDocs.Redaction;
```

## Οδηγός Υλοποίησης

Θα καλύψουμε δύο βασικές δυνατότητες: την ενημέρωση των ευρετηριασμένων εγγράφων και τη διατήρηση του ελέγχου έκδοσης του ευρετηρίου.

### Πώς να ενημερώσετε το ευρετήριο χρησιμοποιώντας το GroupDocs.Search;

`Index` αντιπροσωπεύει τη συλλογή αναζητήσιμων δεδομένων αποθηκευμένης στο δίσκο.  
`UpdateOptions` ρυθμίζει πώς εκτελούνται οι επαυξητικές ενημερώσεις (π.χ., αριθμός νημάτων).  
`UpdateDocument` εφαρμόζει αλλαγές σε ένα μόνο έγγραφο, και `Commit` ολοκληρώνει όλες τις εκκρεμείς ενημερώσεις.

**Άμεση απάντηση (40‑70 λέξεις):** Δημιουργήστε ένα αντικείμενο `Index` που δείχνει στο φάκελο του ευρετηρίου σας, χρησιμοποιήστε `UpdateOptions` για να ορίσετε τον αριθμό νημάτων, καλέστε `UpdateDocument` για κάθε τροποποιημένο αρχείο και τέλος εκτελέστε `Commit` για να αποθηκεύσετε τις αλλαγές. Αυτή η επαυξητική προσέγγιση ενημερώνει μόνο τα τροποποιημένα τμήματα, διατηρώντας το ευρετήριο ενημερωμένο χωρίς πλήρη επαναδημιουργία.

#### Χαρακτηριστικό 1: Ενημέρωση Ευρετηριασμένων Εγγράφων

##### Επισκόπηση
Η ενημέρωση των ευρετηριασμένων εγγράφων εξασφαλίζει ότι τα αποτελέσματα αναζήτησης αντανακλούν το πιο πρόσφατο περιεχόμενο, ακόμη και όταν τα έγγραφα επεξεργάζονται ή αντικαθίστανται.

##### Βήμα 1: Δημιουργία Ευρετηρίου  
Η κλάση `Index` είναι το αντικείμενο υψηλότερου επιπέδου που αντιπροσωπεύει μια συλλογή αναζητήσιμων δεδομένων στο δίσκο.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### Βήμα 2: Προσθήκη Εγγράφων στο Ευρετήριο  
Προσθέστε αρχεία από έναν κατάλογο· η βιβλιοθήκη εξάγει αυτόματα το αναζητήσιμο κείμενο.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### Βήμα 3: Αναζήτηση και Ενημέρωση  
Εκτελέστε ένα ερώτημα, τροποποιήστε το αρχείο προέλευσης, στη συνέχεια καλέστε `UpdateDocument` με τις ίδιες `UpdateOptions` που χρησιμοποιήθηκαν κατά την ευρετηρίαση.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Γιατί Λειτουργεί:** Ορίζοντας `Threads = 2`, η ενημέρωση αξιοποιεί δύο πυρήνες CPU, μειώνοντας τον χρόνο επεξεργασίας περίπου στο ήμισυ σε μηχάνημα τετραπύρηνο.

### Πώς να διατηρήσετε τον έλεγχο έκδοσης του ευρετηρίου;

`IndexUpdater` είναι μια βοηθητική κλάση που αναβαθμίζει παλαιότερες μορφές ευρετηρίου στην πιο πρόσφατη έκδοση που υποστηρίζεται από τη βιβλιοθήκη.

**Άμεση απάντηση (40‑70 λέξεις):** Δημιουργήστε ένα αντικείμενο `IndexUpdater` με τη διαδρομή προς το υπάρχον ευρετήριο, καλέστε `CanUpdateVersion()` για να ελέγξετε τη συμβατότητα, και στη συνέχεια εκτελέστε `UpdateVersion()` εάν χρειάζεται. Μετά την αναβάθμιση, φορτώστε ξανά το ευρετήριο με τη νέα μορφή και πραγματοποιήστε αναζήτηση για να επιβεβαιώσετε ότι όλα λειτουργούν. Αυτό εξασφαλίζει ομαλή μετάβαση μεταξύ εκδόσεων της βιβλιοθήκης.

#### Χαρακτηριστικό 2: Διατήρηση Ελέγχου Έκδοσης Ευρετηρίου

##### Επισκόπηση
Ο έλεγχος έκδοσης εγγυάται ότι τα παλαιότερα ευρετήρια παραμένουν αναζητήσιμα μετά από αναβάθμιση της βιβλιοθήκης.

##### Βήμα 1: Έλεγχος Συμβατότητας  
`IndexUpdater` ελέγχει αν το τρέχον ευρετήριο μπορεί να αναβαθμιστεί στην πιο πρόσφατη μορφή.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### Βήμα 2: Φόρτωση και Αναζήτηση  
Μετά την αναβάθμιση, φορτώστε το ανανεωμένο ευρετήριο και εκτελέστε ένα ερώτημα για να επαληθεύσετε την ακεραιότητα.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Γιατί Λειτουργεί:** Η προειδοποίηση `CanUpdateVersion` αποτρέπει εξαιρέσεις χρόνου εκτέλεσης που προκύπτουν από ασυμφωνίες σχήματος ευρετηρίου, παρέχοντας ασφαλή διαδρομή αναβάθμισης.

## Πρακτικές Εφαρμογές

Πραγματικά σενάρια όπου το **πώς να ενημερώσετε το ευρετήριο** είναι σημαντικό:

1. **Διαχείριση Νομικών Εγγράφων** – Γρήγορη επανευρετηρίαση συμβάσεων μετά από τροποποιήσεις, ενώ καλύπτετε εμπιστευτικές ρήτρες.  
2. **Εταιρικά Αρχεία** – Διατηρήστε ιστορικά αρχεία αναζητήσιμα χωρίς επαναεπεξεργασία εκατομμυρίων αρχείων.  
3. **Συστήματα Διαχείρισης Περιεχομένου (CMS)** – Εφαρμόστε επαυξητικές ενημερώσεις στο ευρετήριο αναζήτησης καθώς οι συγγραφείς δημοσιεύουν νέα άρθρα.

## Σκέψεις Απόδοσης

- **Επιλογές Νημάτων:** Ρυθμίστε `UpdateOptions.Threads` ανάλογα με τους πυρήνες CPU· περισσότερα νήματα βελτιώνουν τη διαμεταγωγή αλλά αυξάνουν τη χρήση μνήμης.  
- **Χρήση Πόρων:** Παρακολουθήστε τη RAM· η βιβλιοθήκη μεταδίδει αρχεία, έτσι οι αυξήσεις μνήμης είναι ελάχιστες ακόμη και για PDF 500 σελίδων.  
- **Καλές Πρακτικές:** Προγραμματίστε τακτικές επαυξητικές ενημερώσεις και καθαρίστε παλιές εκδόσεις ευρετηρίου για να διατηρήσετε βέλτιστη απόδοση.

## Συχνά Προβλήματα και Λύσεις

| Πρόβλημα | Αιτία | Λύση |
|----------|-------|------|
| **Index not found** | Λάθος διαδρομή φακέλου | Επαληθεύστε ότι ο κατασκευαστής `Index` δείχνει στη σωστή διαδρομή. |
| **Version mismatch error** | Χρήση παλαιότερου ευρετηρίου με νεότερη βιβλιοθήκη | Εκτελέστε τη ροή `IndexUpdater` πριν από την κανονική ευρετηρίαση. |
| **Redaction not applied** | Κανόνες επεξεργασίας φορτώθηκαν μετά την ευρετηρίαση | Εφαρμόστε την επεξεργασία **πριν** την προσθήκη εγγράφων στο ευρετήριο. |

## Συχνές Ερωτήσεις

**Ε: Ποια είναι η διαφορά μεταξύ `UpdateDocument` και `Rebuild`;**  
Α: `UpdateDocument` τροποποιεί μόνο τα αλλαγμένα αρχεία, ενώ το `Rebuild` δημιουργεί ξανά ολόκληρο το ευρετήριο από την αρχή, καταναλώνοντας περισσότερο χρόνο και πόρους.

**Ε: Μπορώ να ενημερώσω πολλαπλά έγγραφα παράλληλα;**  
Α: Ναι, ορίστε `UpdateOptions.Threads` στον αριθμό πυρήνων που θέλετε να χρησιμοποιήσετε· η βιβλιοθήκη διαχειρίζεται την παράλληλη επεξεργασία εσωτερικά.

**Ε: Υποστηρίζει το GroupDocs.Search κρυπτογραφημένα PDF;**  
Α: Απόλυτα. Παρέχετε τον κωδικό πρόσβασης μέσω `SearchOptions.Password` κατά τη φόρτωση του εγγράφου.

**Ε: Πώς μπορώ να επαληθεύσω ότι η επεξεργασία ήταν επιτυχής πριν την ευρετηρίαση;**  
Α: Καλέστε `Redactor.Apply()` και ελέγξτε το μέγεθος του αρχείου εξόδου· ένα μειωμένο μέγεθος συχνά υποδεικνύει επιτυχημένη επεξεργασία.

**Ε: Ποιες εκδόσεις .NET υποστηρίζονται επίσημα;**  
Α: .NET Framework 4.5+, .NET Core 3.1+, .NET 5 και .NET 6+.

## Συμπέρασμα

Τώρα έχετε έναν πλήρη, έτοιμο για παραγωγή οδηγό για το **πώς να ενημερώσετε το ευρετήριο** χρησιμοποιώντας το GroupDocs.Search και πώς να διατηρήσετε αυτά τα ευρετήρια συμβατά με το GroupDocs.Redaction για .NET. Ακολουθώντας τα παραπάνω βήματα, μπορείτε να διασφαλίσετε ότι η στρώση αναζήτησης παραμένει γρήγορη, ακριβής και συμμορφωμένη με τους κανονισμούς προστασίας δεδομένων.

**Επόμενα Βήματα:**  
- Πειραματιστείτε με διαφορετικές ρυθμίσεις `Threads` για να βρείτε το βέλτιστο σημείο για το υλικό σας.  
- Εξερευνήστε προχωρημένα μοτίβα επεξεργασίας (π.χ., αφαίρεση SSN βάσει regex) πριν από την ευρετηρίαση.  
- Ενσωματώστε τη ρουτίνα ενημέρωσης ευρετηρίου στη CI/CD pipeline σας για πλήρως αυτοματοποιημένη διαχείριση εγγράφων.

---

**Τελευταία Ενημέρωση:** 2026-06-07  
**Δοκιμάστηκε Με:** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**Συγγραφέας:** GroupDocs  

## Πόροι
- [Τεκμηρίωση](https://docs.groupdocs.com/search/net/)
- [Αναφορά API](https://reference.groupdocs.com/redaction/net)
- [Λήψη GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Δωρεάν Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/search/10)
- [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)

## Σχετικά Μαθήματα

- [Κατάκτηση του GroupDocs.Redaction .NET: Αποτελεσματική Δημιουργία Ευρετηρίου και Διαχείριση Ψευδώνων για Προχωρημένη Αναζήτηση Εγγράφων](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Υλοποίηση Αναζήτησης Συνωνύμων με το GroupDocs.Redaction .NET για Βελτιωμένη Διαχείριση Εγγράφων](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [Κατάκτηση του GroupDocs Search και Redaction σε .NET: Προχωρημένη Διαχείριση Εγγράφων](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)