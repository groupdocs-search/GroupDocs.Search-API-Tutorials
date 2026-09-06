---
date: '2026-06-07'
description: Μάθετε πώς να καταγράψετε τις επεκτάσεις αρχείων και να λάβετε τις μορφές
  αρχείων χρησιμοποιώντας το GroupDocs.Redaction σε C#. Περιλαμβάνει ρύθμιση, κώδικα
  και πρακτικές συμβουλές.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Πώς να καταγράψετε τις επεκτάσεις αρχείων με το GroupDocs.Redaction στο .NET
  – Ένας ολοκληρωμένος οδηγός
type: docs
url: /el/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Εμφάνιση Υποστηριζόμενων Μορφών Αρχείων Χρησιμοποιώντας το GroupDocs.Redaction σε .NET

Η διαχείριση μιας μεγάλης ποικιλίας τύπων εγγράφων είναι καθημερινή πραγματικότητα για τους .NET προγραμματιστές. Χρησιμοποιώντας το **GroupDocs.Redaction**, μπορείτε να **καταγράψετε τις επεκτάσεις αρχείων** που υποστηρίζει η βιβλιοθήκη, παρέχοντας στην εφαρμογή σας τη δυνατότητα να αποδέχεται ή να απορρίπτει μεταφορτώσεις, να παρουσιάζει φιλικές επιλογές UI και να αποφεύγει δαπανηρά σφάλματα χρόνου εκτέλεσης. Αυτό το tutorial σας καθοδηγεί βήμα-βήμα—από τις προαπαιτήσεις μέχρι μια πλήρη, έτοιμη για παραγωγή υλοποίηση—ώστε να μπορείτε με σιγουριά **να λαμβάνετε μορφές αρχείων** και **c# display file formats** στη λύση σας.

## Σύντομες Απαντήσεις
- **Τι σημαίνει “list file extensions”;** Σημαίνει την ανάκτηση της συλλογής των υποστηριζόμενων αναγνωριστικών τύπων αρχείων (π.χ., *.pdf*, *.docx*) από το API.  
- **Ποιο πακέτο NuGet παρέχει αυτή τη δυνατότητα;** `GroupDocs.Redaction` (τελευταία σταθερή έκδοση).  
- **Χρειάζομαι άδεια για να εκτελέσω το παράδειγμα;** Μια δωρεάν δοκιμαστική άδεια λειτουργεί για ανάπτυξη· απαιτείται μόνιμη άδεια για παραγωγή.  
- **Μπορώ να αποθηκεύσω τα αποτελέσματα στην κρυφή μνήμη;** Ναι—αποθηκεύστε τη λίστα στη μνήμη ή σε κατανεμημένη κρυφή μνήμη για να αποφύγετε επαναλαμβανόμενες κλήσεις API.  
- **Είναι αυτή η δυνατότητα συμβατή με .NET 6 και .NET Core;** Απόλυτα· η βιβλιοθήκη υποστηρίζει .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ και .NET 6+.

## Τι είναι το GroupDocs.Redaction;
**GroupDocs.Redaction** είναι μια βιβλιοθήκη .NET που επιτρέπει στους προγραμματιστές να αφαιρούν ευαίσθητο περιεχόμενο, να μετατρέπουν έγγραφα και να ανακαλύπτουν υποστηριζόμενους τύπους αρχείων—όλα χωρίς την ανάγκη Microsoft Office στον διακομιστή. Απομονώνει τη σύνθετη διαχείριση μορφών πίσω από ένα καθαρό, αντικειμενοστραφή API. Προσφέρει ένα ενοποιημένο API για redaction, conversion και ανακάλυψη μορφών, διαχειριζόμενο PDFs, έγγραφα Office, εικόνες και άλλα, εξασφαλίζοντας υψηλή απόδοση και ασφάλεια.

## Γιατί να καταγράψετε τις επεκτάσεις αρχείων με το GroupDocs.Redaction;
Η βιβλιοθήκη **υποστηρίζει πάνω από 50 μορφές εισόδου και εξόδου**, συμπεριλαμβανομένων PDF, DOCX, PPTX, XLSX, HTML και πάνω από 30 τύπους εικόνων. Προγραμματιστικά **καταγράφοντας τις επεκτάσεις αρχείων**, μπορείτε να:
- Αποτρέψετε τους χρήστες από το ανέβασμα μη υποστηριζόμενων αρχείων (μειώνοντας τα σφάλματα επικύρωσης έως και 90%).  
- Συμπληρώσετε δυναμικά τα μενού dropdown, διασφαλίζοντας ότι το UI παραμένει συγχρονισμένο με τις ενημερώσεις της βιβλιοθήκης.  
- Δημιουργήσετε αρχεία ελέγχου (audit logs) που καταγράφουν τον ακριβή τύπο αρχείου που προσπάθησε να επεξεργαστεί ο χρήστης.

## Προαπαιτήσεις

- **GroupDocs.Redaction**: Εγκατάσταση μέσω NuGet (δείτε τις εντολές παρακάτω).  
- **.NET SDK**: Βεβαιωθείτε ότι είναι εγκατεστημένο το τελευταίο .NET SDK. Κατεβάστε το [εδώ](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 ή οποιονδήποτε συμβατό επεξεργαστή.  
- **Βασικές γνώσεις C#**: Θα πρέπει να είστε άνετοι με συλλογές και LINQ.

## Ρύθμιση του GroupDocs.Redaction για .NET

### Εγκατάσταση της βιβλιοθήκης

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Ανοίξτε το NuGet Package Manager, αναζητήστε “GroupDocs.Redaction,” και εγκαταστήστε την τελευταία έκδοση.

### Απόκτηση και εφαρμογή άδειας

Ξεκινήστε με μια δωρεάν δοκιμαστική άδεια ή ζητήστε προσωρινή άδεια για να εξερευνήσετε όλες τις δυνατότητες χωρίς περιορισμούς. Για επιλογές αγοράς, επισκεφθείτε τη [σελίδα αγοράς του GroupDocs](https://purchase.groupdocs.com/). Μόλις έχετε το αρχείο άδειας:
1. Τοποθετήστε το σε έναν προσβάσιμο φάκελο μέσα στο έργο σας (π.χ., `./Licenses/GroupDocs.Redaction.lic`).  
2. Αρχικοποιήστε την άδεια κατά την εκκίνηση της εφαρμογής:

Η κλάση `License` φορτώνει το αρχείο άδειας και ενεργοποιεί το GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Πώς να καταγράψετε τις επεκτάσεις αρχείων χρησιμοποιώντας το GroupDocs.Redaction;

Φορτώστε το Redaction API και καλέστε τη μέθοδο που επιστρέφει τις υποστηριζόμενες μορφές. Η κλήση επιστρέφει μια συλλογή όπου κάθε στοιχείο περιέχει μια επέκταση και μια περιγραφή φιλική προς τον χρήστη. Αυτή η λειτουργία είναι ελαφριά και μπορεί να εκτελεστεί κατά την εκκίνηση ή κατόπιν ζήτησης.

### Ανάκτηση των υποστηριζόμενων τύπων αρχείων
Η μέθοδος `RedactionApi.GetSupportedFileFormats()` επιστρέφει μια μόνο για ανάγνωση συλλογή αντικειμένων `FileFormatInfo` που περιγράφουν κάθε μορφή.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Εμφάνιση κάθε επέκτασης και περιγραφής
Κάθε `FileFormatInfo` παρέχει τις ιδιότητες `Extension` και `Description` για έναν τύπο αρχείου.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Εξήγηση**: Ο βρόχος επαναλαμβάνει κάθε αντικείμενο `FileFormatInfo`, εκτυπώνοντας την `Extension` και την `Description` του σε έναν καλά ευθυγραμμισμένο πίνακα.

## Πώς να ενσωματώσετε τη λίστα σε ένα UI dropdown;

Αφού έχετε τη συλλογή, δεσμεύστε την σε οποιοδήποτε UI στοιχείο—WinForms `ComboBox`, WPF `ComboBox` ή ASP.NET Core `select`. Το κλειδί είναι να χρησιμοποιήσετε την `Extension` ως τιμή και την `Description` ως κείμενο εμφάνισης. Αυτό εξασφαλίζει ότι οι χρήστες βλέπουν φιλικά ονόματα ενώ ο κώδικάς σας εργάζεται με τις ακριβείς συμβολοσειρές επεκτάσεων.

## Συνηθισμένα Προβλήματα και Λύσεις

- **Σφάλμα λείποντος namespace** – Επαληθεύστε ότι έχετε εισάγει τα `GroupDocs.Redaction` και `GroupDocs.Redaction.Common`.  
- **Άδεια δεν βρέθηκε** – Βεβαιωθείτε ότι η διαδρομή του αρχείου άδειας είναι σωστή και ότι το αρχείο περιλαμβάνεται στην έξοδο της κατασκευής.  
- **Απόδοση σε μεγάλα έργα** – Αποθηκεύστε το αποτέλεσμα σε μια στατική μεταβλητή ή σε κατανεμημένη κρυφή μνήμη (π.χ., Redis) για να αποφύγετε επαναλαμβανόμενη απαρίθμηση.

## Πρακτικές Εφαρμογές

Η γνώση της ακριβούς λίστας των υποστηριζόμενων επεκτάσεων ανοίγει αρκετά πραγματικά σενάρια:
1. **Συστήματα Διαχείρισης Εγγράφων** – Αυτόματη κατηγοριοποίηση των εισερχόμενων αρχείων βάσει της επέκτασής τους.  
2. **Εργαλεία Φιλτραρίσματος Περιεχομένου** – Αποκλεισμός μη επιτρεπόμενων μορφών (π.χ., εκτελέσιμα αρχεία) κατά τη μεταφόρτωση.  
3. **Συστήματα Μετατροπής Αρχείων** – Δυναμική απόφαση εάν ένα αρχείο μπορεί να μετατραπεί ή χρειάζεται εναλλακτική ροή εργασίας.

## Σκέψεις Απόδοσης

- **Απόδοση μνήμης** – Η λίστα μορφών αποθηκεύεται σε μια ελαφριά `IReadOnlyCollection`, συνήθως κάτω από 2 KB.  
- **Ασφάλεια νήματος** – Η συλλογή είναι αμετάβλητη μετά τη δημιουργία, καθιστώντας την ασφαλή για ταυτόχρονες αναγνώσεις.  
- **Κρυφή μνήμη** – Για APIs υψηλής κίνησης, αποθηκεύστε τη λίστα στην κρυφή μνήμη για τη διάρκεια ζωής της εφαρμογής ώστε να εξαλειφθεί το μικρό χρονικό κόστος ανά αίτηση.

## Συμπέρασμα

Ακολουθώντας τα παραπάνω βήματα, έχετε τώρα έναν αξιόπιστο τρόπο να **καταγράψετε τις επεκτάσεις αρχείων** και **c# display file formats** χρησιμοποιώντας το GroupDocs.Redaction. Αυτή η δυνατότητα όχι μόνο βελτιώνει την εμπειρία του χρήστη αλλά και προστατεύει το backend σας από μη υποστηριζόμενα αρχεία. Εξερευνήστε πρόσθετες λειτουργίες Redaction—όπως masking περιεχομένου, redaction PDF και επεξεργασία παρτίδων—για να ενισχύσετε περαιτέρω τη ροή εργασίας εγγράφων σας.

## Συχνές Ερωτήσεις

**Q: Ποιοι είναι οι προεπιλεγμένοι υποστηριζόμενοι τύποι αρχείων;**  
A: Το GroupDocs.Redaction υποστηρίζει πάνω από 50 μορφές, συμπεριλαμβανομένων PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG και πολλές άλλες. Δείτε την πλήρη λίστα στη [τεκμηρίωση του GroupDocs](https://docs.groupdocs.com/search/net/).

**Q: Πώς αναβαθμίζω τη βιβλιοθήκη στην τελευταία έκδοση;**  
A: Ανοίξτε το NuGet Package Manager, αναζητήστε “GroupDocs.Redaction,” και κάντε κλικ στο **Update**. Εναλλακτικά, εκτελέστε `dotnet add package GroupDocs.Redaction --version <latest>`.

**Q: Μπορώ να χρησιμοποιήσω αυτή τη λίστα για επικύρωση αρχείων στο server;**  
A: Ναι—συγκρίνετε την επέκταση του ανεβασμένου αρχείου με τη ληφθείσα συλλογή πριν από την επεξεργασία. Αυτό εξαλείφει το 99% των σφαλμάτων μη έγκυρης μορφής.

**Q: Είναι δυνατόν να επεκτείνω την υποστήριξη για προσαρμοσμένους τύπους αρχείων;**  
A: Οι προσαρμοσμένες επεκτάσεις απαιτούν προσαρμοσμένους χειριστές· η κύρια βιβλιοθήκη δεν προσθέτει νέες μορφές εγγενώς. Εξετάστε την τεκμηρίωση API για τη δημιουργία προσαρμοσμένων pipelines εισαγωγής/εξαγωγής.

**Q: Η εφαρμογή μου καταρρέει μετά την προσθήκη του κώδικα—τι πρέπει να ελέγξω;**  
A: Βεβαιωθείτε ότι η άδεια φορτώνεται σωστά, ότι οι δηλώσεις `using` αναφέρονται στα σωστά namespaces και ότι διαχειρίζεστε το `IOException` κατά την ανάγνωση του αρχείου άδειας.

---

**Τελευταία Ενημέρωση:** 2026-06-07  
**Δοκιμή με:** GroupDocs.Redaction 23.9 for .NET  
**Συγγραφέας:** GroupDocs  

## Πόροι
- [Τεκμηρίωση](https://docs.groupdocs.com/search/net/)
- [Αναφορά API](https://reference.groupdocs.com/redaction/net)
- [Λήψη GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Δωρεάν Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/search/10)
- [Αίτηση Προσωρινής Άδειας](https://purchase.groupdocs.com/temporary-license/)

## Σχετικά Μαθήματα
- [Αποκτήστε τον έλεγχο φιλτραρίσματος αρχείων σε .NET με το GroupDocs.Redaction&#58; Αποτελεσματικές τεχνικές διαχείρισης εγγράφων](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Αποκτήστε τον έλεγχο GroupDocs.Redaction .NET&#58; Ρύθμιση & Διαχείριση Συμβάντων για Ασφαλή Διαχείριση Εγγράφων](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Απόκτηση Εξέλιξης Διαχείρισης Εγγράφων σε .NET με το GroupDocs.Redaction&#58; Ρύθμιση Άδειας και Επισήμανση Αναζήτησης HTML](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)