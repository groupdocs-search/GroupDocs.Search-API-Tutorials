---
date: '2026-04-21'
description: Μάθετε πώς να φιλτράρετε αρχεία χρησιμοποιώντας το GroupDocs.Redaction
  για .NET, συμπεριλαμβανομένου του φιλτραρίσματος κατά ημερομηνία δημιουργίας, μέγεθος
  αρχείου, ημερομηνία τροποποίησης και πώς να εφαρμόζετε φίλτρα NOT.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Πώς να φιλτράρετε αρχεία με το GroupDocs.Redaction για .NET
type: docs
url: /el/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Πώς να Φιλτράρετε Αρχεία με το GroupDocs.Redaction για .NET

Στο σημερινό ταχύτατο ψηφιακό περιβάλλον, **πώς να φιλτράρετε αρχεία** αποδοτικά μπορεί να καθορίσει την παραγωγικότητά σας. Είτε χρειάζεστε να απομονώσετε έγγραφα κατά επέκταση, ημερομηνία δημιουργίας, μέγεθος ή ημερομηνία τροποποίησης, μια ισχυρή στρατηγική φιλτραρίσματος εξοικονομεί χρόνο, μειώνει το κόστος αποθήκευσης και διατηρεί το ευρετήριο αναζήτησης καθαρό. Σε αυτό το tutorial θα περάσουμε από πραγματικά παραδείγματα χρησιμοποιώντας το GroupDocs.Redaction για .NET, δείχνοντάς σας ακριβώς πώς να φιλτράρετε αρχεία ώστε να καλύψετε κοινές επιχειρηματικές ανάγκες.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη χρειάζομαι;** GroupDocs.Redaction for .NET (install via NuGet).  
- **Μπορώ να φιλτράρω κατά ημερομηνία δημιουργίας;** Yes – use `CreateCreationTimeRange`.  
- **Πώς μπορώ να εξαιρέσω ορισμένους τύπους;** Apply a NOT filter with `DocumentFilter.CreateNot`.  
- **Υποστηρίζεται το φιλτράρισμα κατά μέγεθος αρχείου;** Absolutely, via `CreateFileLengthRange` or upper/lower bounds.  
- **Χρειάζομαι άδεια;** A trial or full license is required for production use.

## Τι είναι το φιλτράρισμα αρχείων με το GroupDocs.Redaction;
Το φιλτράρισμα αρχείων σας επιτρέπει να υποδείξετε στη μηχανή ευρετηρίασης ποια έγγραφα να συμπεριληφθούν ή να αγνοηθούν βάσει μεταδεδομένων όπως επέκταση, ημερομηνίες, μοτίβα διαδρομής ή μέγεθος. Ορίζοντας ακριβείς κανόνες `DocumentFilter`, διατηρείτε το ευρετήριό σας ελαφρύ και τις αναζητήσεις γρήγορες.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction για .NET;
- **Ενσωματωμένοι βοηθοί φιλτραρίσματος** – δεν χρειάζεται να γράψετε κώδικα συστήματος αρχείων.  
- **Λογικοί τελεστές** – συνδυάστε πολλαπλά κριτήρια με AND, OR και NOT.  
- **Βελτιστοποιημένη απόδοση** – τα φίλτρα εφαρμόζονται κατά την ευρετηρίαση, όχι μετά.  
- **Διαπλατφορμικό** – λειτουργεί με .NET Framework, .NET Core και .NET 5/6+.

## Προαπαιτούμενα
- .NET Framework 4.6+ ή .NET Core 3.1+ εγκατεστημένα.  
- Visual Studio ή το προτιμώμενο IDE C#.  
- Βασικές γνώσεις C#.  

### Απαιτούμενες Βιβλιοθήκες & Ρύθμιση
Εγκαταστήστε το πακέτο NuGet χρησιμοποιώντας την προτιμώμενη μέθοδο σας:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Συμβουλή επαγγελματία:** Μετά την εγκατάσταση, προσθέστε το αρχείο άδειας στη ρίζα του έργου και καλέστε `License.SetLicense("license-file-path")` πριν δημιουργήσετε οποιαδήποτε αντικείμενα Redactor ή Index.

## Ρύθμιση του GroupDocs.Redaction για .NET

Πρώτα, δημιουργήστε μια παρουσία `Redactor` που δείχνει στο έγγραφο που θέλετε να επεξεργαστείτε:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Γιατί είναι σημαντικό:** Η αρχικοποίηση του Redactor εγγυάται ότι η βιβλιοθήκη είναι έτοιμη να εφαρμόσει φίλτρα και κανόνες σήμανσης αργότερα στη ροή εργασίας.

## Πώς να φιλτράρετε αρχεία κατά επέκταση
Το φιλτράρισμα κατά επέκταση αρχείου είναι ο πιο κοινός τρόπος να περιορίσετε ένα σύνολο εγγράφων. Παρακάτω κρατάμε μόνο αρχεία FB2, EPUB και TXT.

### Φιλτράρισμα κατά επέκταση αρχείου

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Πώς να εφαρμόσετε φίλτρο NOT για να εξαιρέσετε ανεπιθύμητους τύπους
Αν χρειάζεστε **εφαρμόσετε φίλτρο NOT** λογική—π.χ., να εξαιρέσετε αρχεία HTML και PDF—χρησιμοποιήστε `CreateNot`.

### Εξαίρεση αρχείων HTM, HTML και PDF

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Πώς να φιλτράρετε αρχεία κατά ημερομηνία δημιουργίας
Όταν χρειάζεται **να φιλτράρετε κατά ημερομηνία δημιουργίας**, καθορίστε μια αρχική και τελική `DateTime`.

### Φιλτράρισμα κατά εύρος ημερομηνίας δημιουργίας

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Πώς να φιλτράρετε αρχεία κατά ημερομηνία τροποποίησης
Παρόμοια με τις ημερομηνίες δημιουργίας, μπορείτε να περιορίσετε τα αποτελέσματα σε αρχεία που τροποποιήθηκαν πριν από ένα συγκεκριμένο σημείο.

### Φιλτράρισμα κατά ημερομηνία τροποποίησης

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Πώς να φιλτράρετε αρχεία κατά διαδρομή χρησιμοποιώντας κανονικές εκφράσεις
Αν η δομή των φακέλων σας ακολουθεί ονομαστικά πρότυπα, ένα regex μπορεί να στοχεύσει συγκεκριμένες διαδρομές.

### Φιλτράρισμα κατά μοτίβο διαδρομής αρχείου

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Πώς να φιλτράρετε αρχεία κατά μέγεθος
Ο έλεγχος του μεγέθους των εγγράφων είναι απαραίτητος όταν αντιμετωπίζετε περιορισμούς εύρους ζώνης ή αποθήκευσης.

### Φιλτράρισμα κατά μέγεθος αρχείου (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Πώς να συνδυάσετε πολλαπλές συνθήκες με AND
Όταν χρειάζεται **πώς να φιλτράρετε αρχεία** χρησιμοποιώντας αρκετά κριτήρια ταυτόχρονα, συνδυάστε τα με `CreateAnd`.

### Παράδειγμα λογικού AND

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Πώς να συνδυάσετε πολλαπλές συνθήκες με OR
Χρησιμοποιήστε `CreateOr` όταν οποιοσδήποτε από τους πολλούς κανόνες πρέπει να περάσει.

### Παράδειγμα λογικού OR

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Συχνά Προβλήματα και Λύσεις
- **Το φίλτρο δεν εφαρμόζεται:** Βεβαιωθείτε ότι έχετε ορίσει `settings.DocumentFilter` **πριν** δημιουργήσετε την παρουσία `Index`.  
- **Εμφανίζονται απρόσμενα αρχεία:** Ελέγξτε ξανά ότι οι επεκτάσεις αρχείων περιλαμβάνουν την αρχική τελεία (`.txt`).  
- **Μείωση απόδοσης:** Συνδυάστε φίλτρα με AND για να μειώσετε τον αριθμό των αρχείων που σαρώνονται νωρίς στη διαδικασία ευρετηρίασης.  
- **Σφάλματα regex:** Διαφύγετε ειδικούς χαρακτήρες στο μοτίβο διαδρομής ή χρησιμοποιήστε `RegexOptions.IgnoreCase` για αντιστοιχίες χωρίς διάκριση πεζών‑κεφαλαίων.

## Συχνές Ερωτήσεις

**Q: Μπορώ να συνδυάσω ένα φίλτρο NOT με ένα φίλτρο AND;**  
A: Ναι. Δημιουργήστε πρώτα το φίλτρο NOT (`DocumentFilter.CreateNot`) και στη συνέχεια συμπεριλάβετε το ως ένα από τα ορίσματα του `DocumentFilter.CreateAnd`.

**Q: Πώς φιλτράρω αρχεία μεγαλύτερα από 10 MB;**  
A: Χρησιμοποιήστε `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` για να συμπεριλάβετε μόνο αρχεία που υπερβαίνουν αυτό το μέγεθος.

**Q: Είναι δυνατόν να φιλτράρω ταυτόχρονα κατά ημερομηνία δημιουργίας και τροποποίησης;**  
A: Απόλυτα. Δημιουργήστε κάθε φίλτρο ξεχωριστά και συνδυάστε τα με `CreateAnd`.

**Q: Λειτουργούν αυτά τα φίλτρα με διαδρομές αποθήκευσης στο cloud;**  
A: Τα φίλτρα λειτουργούν στο τοπικό σύστημα αρχείων. Για πηγές cloud, κατεβάστε τα αρχεία σε έναν προσωρινό φάκελο πρώτα, μετά εφαρμόστε τα ίδια φίλτρα.

**Q: Θα απαιτηθεί επανευρετηρίαση αν αλλάξω το φίλτρο;**  
A: Ναι. Τα φίλτρα αξιολογούνται όταν καλείτε `index.Add`. Η αλλαγή ενός φίλτρου σημαίνει ότι πρέπει να ξαναχτίσετε το ευρετήριο για να αντικατοπτριστούν τα νέα κριτήρια.

## Συμπέρασμα

Με την εξοικείωση με **πώς να φιλτράρετε αρχεία** με το GroupDocs.Redaction για .NET—είτε κατά επέκταση, ημερομηνία δημιουργίας, ημερομηνία τροποποίησης, μέγεθος αρχείου ή χρησιμοποιώντας λογική NOT—μπορείτε να βελτιστοποιήσετε τη διαχείριση εγγράφων, να διατηρήσετε τα ευρετήρια αποδοτικά και να εστιάσετε στο περιεχόμενο που πραγματικά έχει σημασία. Πειραματιστείτε με τους λογικούς τελεστές για να προσαρμόσετε το φιλτράρισμα στις ακριβείς επιχειρηματικές σας πολιτικές και θα δείτε άμεσες βελτιώσεις στην ταχύτητα και την αποδοτικότητα αποθήκευσης.

---

**Τελευταία Ενημέρωση:** 2026-04-21  
**Δοκιμή Με:** GroupDocs.Redaction 24.11 for .NET  
**Συγγραφέας:** GroupDocs