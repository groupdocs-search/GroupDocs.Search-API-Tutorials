---
date: '2026-06-07'
description: Μάθετε πώς να υλοποιήσετε υψηλή συμπίεση .NET για αποθήκευση κειμένου
  και να αφαιρέσετε εμπιστευτικά δεδομένα χρησιμοποιώντας το GroupDocs.Search και
  το GroupDocs.Redaction σε εφαρμογές .NET.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'Υλοποίηση Υψηλής Συμπίεσης .NET με GroupDocs: Οδηγός Κειμένου & Redaction'
type: docs
url: /el/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Υλοποίηση Υψηλής Συμπίεσης .NET με GroupDocs: Οδηγός Κειμένου & Αποκόλλησης

Σε σύγχρονες λύσεις .NET, η **implement high compression .net** είναι απαραίτητη όταν χρειάζεται να αποθηκεύσετε τεράστιες συλλογές κειμένου χωρίς να αυξήσετε την χρήση δίσκου. Ταυτόχρονα, η προστασία ευαίσθητων πληροφοριών—όπως προσωπικά αναγνωριστικά ή οικονομικά στοιχεία—απαιτεί αξιόπιστη αποκόλληση. Αυτό το εκπαιδευτικό υλικό σας δείχνει, βήμα‑βήμα, πώς να ρυθμίσετε την αποθήκευση κειμένου με υψηλή συμπίεση χρησιμοποιώντας το **GroupDocs.Search** και πώς να αφαιρέσετε με ασφάλεια εμπιστευτικά δεδομένα χρησιμοποιώντας το **GroupDocs.Redaction**. Στο τέλος, θα μπορείτε να συμπιέσετε το ευρετηριασμένο κείμενο έως και 90 % και να αφαιρέσετε ιδιωτικό περιεχόμενο από PDFs, αρχεία Word και πολλές άλλες μορφές.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη παρέχει ευρετηρίαση υψηλής συμπίεσης;** GroupDocs.Search for .NET.  
- **Ποιο εργαλείο αποκόπτει ευαίσθητα δεδομένα;** GroupDocs.Redaction for .NET.  
- **Μπορώ να προσθέσω έγγραφα στο ευρετήριο αυτόματα;** Yes—use the `AddDocument` API inside a folder‑scan loop.  
- **Είναι η συμπίεση χωρίς απώλειες για την αναζήτηση;** Yes, the text remains fully searchable after compression.  
- **Χρειάζομαι άδεια για παραγωγή;** A permanent GroupDocs license is required for commercial use.

## Τι είναι το “implement high compression .net”;
Το “implement high compression .net” σημαίνει τη διαμόρφωση της μηχανής ευρετηρίασης GroupDocs.Search ώστε να αποθηκεύει το εξαγόμενο κειμενικό περιεχόμενο σε συμπιεσμένη μορφή. Αυτό μειώνει δραστικά το μέγεθος του ευρετηρίου στον δίσκο, διατηρώντας το κείμενο πλήρως αναζητήσιμο. Η συμπίεση είναι χωρίς απώλειες, έτσι η συνάφεια των ερωτημάτων και η εξαγωγή αποσπασμάτων λειτουργούν ακριβώς όπως σε ένα μη συμπιεσμένο ευρετήριο.

## Γιατί να χρησιμοποιήσετε το GroupDocs για συμπίεση και αποκόλληση;
Το GroupDocs.Search υποστηρίζει περισσότερες από πενήντα μορφές εισόδου και μπορεί να συμπιέσει το ευρετηριασμένο κείμενο έως και το ενενήντα τοις εκατό, επιτρέποντας σε μεγάλες συλλογές εγγράφων να καταλαμβάνουν μόνο ένα κλάσμα του αρχικού μεγέθους. Το GroupDocs.Redaction συμπληρώνει αυτό το σενάριο διαγράφοντας μόνιμα ή καλύπτοντας ευαίσθητες πληροφορίες σε πάνω από τριάντα τύπους αρχείων, βοηθώντας σας να τηρήσετε αυστηρούς κανονισμούς συμμόρφωσης όπως GDPR και HIPAA χωρίς πρόσθετα εργαλεία.

## Προαπαιτούμενα
- **Περιβάλλον ανάπτυξης:** Visual Studio 2022 ή νεότερο, .NET 6+ (ή .NET Framework 4.7.2).  
- **Βιβλιοθήκες:** `GroupDocs.Search` και `GroupDocs.Redaction` NuGet packages.  
- **Δικαιώματα:** Read/write access to the folders that contain source documents and the index output location.  
- **Βασικές γνώσεις:** C# syntax, file I/O, and familiarity with .NET project structure.

## Πώς να υλοποιήσετε υψηλή συμπίεση .NET με το GroupDocs;
Για να υλοποιήσετε υψηλή συμπίεση .NET με το GroupDocs, πρώτα δημιουργήστε ένα αντικείμενο `TextStorageSettings` και ορίστε το `CompressionLevel` του σε `High`. Στη συνέχεια, δημιουργήστε ένα αντικείμενο `Index`, περνώντας τις ρυθμίσεις και το φάκελο όπου θα αποθηκευτεί το ευρετήριο. Μόλις το ευρετήριο είναι έτοιμο, προσθέστε έγγραφα χρησιμοποιώντας το `AddDocument`, και τέλος εκτελέστε αναζητήσεις με τη μέθοδο `Search`, ενώ η μηχανή διαχειρίζεται διαφανώς τη συμπίεση και αποσυμπίεση.

### Βήμα 1: Εγκατάσταση των απαιτούμενων πακέτων NuGet
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Αναζητήστε το “GroupDocs.Search” και κάντε κλικ στο **Install**.  

### Βήμα 2: Εγκατάσταση του GroupDocs.Redaction (για αποκόλληση δεδομένων)
- Ανοίξτε το **NuGet Package Manager**.  
- Αναζητήστε το **GroupDocs.Redaction** και εγκαταστήστε την πιο πρόσφατη σταθερή έκδοση.  

### Βήμα 3: Απόκτηση και εφαρμογή άδειας
- **Δωρεάν δοκιμή:** Register on the GroupDocs portal for a 30‑day trial key.  
- **Προσωρινή άδεια:** Request a temporary key for development environments.  
- **Μόνιμη άδεια:** Purchase a production license to remove evaluation limitations.

### Βήμα 4: Βασική αρχικοποίηση και των δύο βιβλιοθηκών
The `Search` and `Redaction` engines share a common licensing model. Initialize them at application startup:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Χαρακτηριστικό 1: Ρυθμίσεις Αποθήκευσης Κειμένου Υψηλής Συμπίεσης

### Ρύθμιση Διαμόρφωσης Ευρετηρίασης
`TextStorageSettings` είναι η κλάση που λέει στο GroupDocs.Search πώς να διατηρεί το εξαγόμενο κείμενο. Η ενεργοποίηση υψηλής συμπίεσης μειώνει το μέγεθος του ευρετηρίου έως και **10×** χωρίς να επηρεάζει την ταχύτητα αναζήτησης.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Επεξήγηση:**  
- `CompressionLevel.High` ενεργοποιεί έναν αλγόριθμο βασισμένο σε ZSTD που συμπιέζει τα μπλοκ κειμένου αποδοτικά.  
- `UseMemoryCache = false` αναγκάζει τη μηχανή να μεταδίδει δεδομένα από το δίσκο, κάτι που είναι ιδανικό για μεγάλες εγκαταστάσεις.

### Δημιουργία και Διαχείριση του Ευρετηρίου
Το αντικείμενο `Index` αντιπροσωπεύει το αποθετήριο αναζήτησης στον δίσκο. Καθορίζετε το φάκελο όπου θα αποθηκευτούν τα αρχεία του ευρετηρίου και περνάτε τις ρυθμίσεις συμπίεσης που ορίστηκαν παραπάνω.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Επεξήγηση:**  
- `indexFolder` καθορίζει πού βρίσκονται τα συμπιεσμένα αρχεία ευρετηρίου.  
- `settings` ενσωματώνει τη διαμόρφωση υψηλής συμπίεσης, εξασφαλίζοντας ότι κάθε προστιθέμενο έγγραφο ωφελείται από αυτήν.

## Χαρακτηριστικό 2: Προσθήκη Εγγράφων στο Ευρετήριο

### Προσθήκη Εγγράφων στο Ευρετήριό σας
`AddDocument` προσθέτει ένα μεμονωμένο αρχείο στο ευρετήριο, εξάγοντας το κείμενό του, το συμπιέζει σύμφωνα με τις ρυθμίσεις και αποθηκεύει το αποτέλεσμα. Το GroupDocs.Search μπορεί να επεξεργαστεί αρχεία από ένα δέντρο καταλόγων. Ο παρακάτω βρόχος διασχίζει το `documentsFolder`, προσθέτει κάθε αρχείο και καταγράφει την πρόοδο.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Επεξήγηση:**  
- `AddDocument` αναλύει το αρχείο, εξάγει το αναζητήσιμο κείμενο, το συμπιέζει σύμφωνα με το `TextStorageSettings` και το αποθηκεύει στο ευρετήριο.  
- Αυτή η προσέγγιση λειτουργεί για **PDF, DOCX, TXT, HTML** και περισσότερα από **30** άλλα μορφότυπα.

## Χαρακτηριστικό 3: Εκτέλεση Ερωτήματος Αναζήτησης

### Εκτέλεση Αναζήτησης
`Search` εκτελεί ένα ερώτημα στο συμπιεσμένο ευρετήριο και επιστρέφει μια συλλογή από αντικείμενα `DocumentResult` που ταιριάζουν, με βαθμολογίες συνάφειας και επισημασμένα αποσπάσματα. Μόλις το ευρετήριο είναι γεμάτο, μπορείτε να εκτελείτε γρήγορα ερωτήματα. Η μέθοδος `Search` επιστρέφει μια συλλογή από αντικείμενα `DocumentResult` που περιλαμβάνουν διαδρομές αρχείων και επισημασμένα αποσπάσματα.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Επεξήγηση:**  
- Η μηχανή αναζήτησης σαρώνει το συμπιεσμένο κείμενο άμεσα, έτσι η καθυστέρηση του ερωτήματος παραμένει χαμηλή ακόμη και για ευρετήρια που περιέχουν **εκατομμύρια σελίδες**.  
- `Score` υποδεικνύει τη συνάφεια· υψηλότερες τιμές σημαίνουν καλύτερη αντιστοίχιση.

## Πώς να αποκόψετε εμπιστευτικά δεδομένα με το GroupDocs.Redaction;
Η αποκόλληση εμπιστευτικών δεδομένων με το GroupDocs.Redaction ξεκινά με τη δημιουργία μιας παρουσίας `Redactor` για το αρχείο-στόχο. Ορίστε ένα ή περισσότερα αντικείμενα `SearchPattern` που περιγράφουν το κείμενο που πρέπει να αφαιρεθεί, όπως κανονικές εκφράσεις για αριθμούς κοινωνικής ασφάλισης. Εφαρμόστε κάθε μοτίβο χρησιμοποιώντας το `Redact`, καθορίζοντας έναν `RedactionType` όπως `BlackOut`, και αποθηκεύστε το αποτέλεσμα ως νέο έγγραφο, διασφαλίζοντας ότι το αρχικό παραμένει αμετάβλητο.

`Redactor` είναι η κύρια κλάση στο GroupDocs.Redaction που χρησιμοποιείται για τη φόρτωση ενός εγγράφου και την εκτέλεση λειτουργιών αποκόλλησης.  
`SearchPattern` ορίζει μια κανονική έκφραση που εντοπίζει το κείμενο προς αποκόλληση.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Επεξήγηση:**  
- `SearchPattern` χρησιμοποιεί μια κανονική έκφραση για τον εντοπισμό αριθμών κοινωνικής ασφάλισης.  
- `RedactionType.BlackOut` αντικαθιστά το ταιριαστό κείμενο με ένα συμπαγές μαύρο ορθογώνιο, εξασφαλίζοντας ότι τα δεδομένα δεν μπορούν να ανακτηθούν.

## Πρακτικές Εφαρμογές
1. **Διαχείριση Νομικών Εγγράφων:** Automatically compress massive case files and redact client identifiers before archiving.  
2. **Ιατρικά Αρχεία:** Store years of patient notes in a compressed index and remove PHI (Protected Health Information) before sharing with research partners.  
3. **Οικονομική Αναφορά:** Secure quarterly reports by redacting account numbers while keeping the searchable text for audit queries.

## Παράγοντες Απόδοσης
- **Επίδραση Συμπίεσης:** High compression reduces index size by up to **90 %**, which lowers SSD wear and speeds up backup operations.  
- **Χρήση Μνήμης:** Disable in‑memory caching for very large indexes to keep the process footprint under **500 MB**.  
- **Βελτιστοποίηση I/O:** Batch document addition in groups of 100 to minimize disk thrashing.  
- **Ασύγχρονη επεξεργασία:** Wrap `AddDocument` calls in `Task.Run` to keep UI threads responsive in desktop apps.

## Συνηθισμένα Προβλήματα & Επίλυση
- **Λανθασμένες διαδρομές αρχείων:** Verify that `documentsFolder` and `indexFolder` are absolute paths and that the application has read/write permissions.  
- **Σφάλματα άδειας:** Ensure the `.lic` files are deployed alongside the executable or embedded as resources.  
- **Η αναζήτηση δεν επιστρέφει αποτελέσματα:** Check that the `TextStorageSettings` compression level matches the one used during indexing; mismatched settings can cause deserialization failures.  

## Συχνές Ερωτήσεις

**Q: Μπορώ να προσθέσω έγγραφα στο ευρετήριο μετά την αρχική δημιουργία;**  
A: Ναι—απλώς καλέστε `index.AddDocument` για νέα αρχεία· η μηχανή ενημερώνει το συμπιεσμένο ευρετήριο προοδευτικά.

**Q: Η αποκόλληση αλλάζει το αρχικό αρχείο;**  
A: Όχι—το αρχικό αρχείο παραμένει αμετάβλητο· η αποκοπείσα έκδοση αποθηκεύεται ως νέο αρχείο, διατηρώντας την ακεραιότητα του εγγράφου.

**Q: Ποιες μορφές υποστηρίζει το GroupDocs.Redaction;**  
A: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG), and plain text.

**Q: Πώς η υψηλή συμπίεση επηρεάζει τη συνάφεια της αναζήτησης;**  
A: It does not. The compression is loss‑less for text, so relevance scores are identical to an uncompressed index.

**Q: Υπάρχει όριο στο μέγεθος των εγγράφων που μπορώ να ευρετηριάσω;**  
A: GroupDocs.Search can handle multi‑gigabyte files by streaming content; however, ensure sufficient disk space for the compressed index (approximately 10 % of the original size).

## Πόροι
- [Τεκμηρίωση](https://docs.groupdocs.com/search/net/)
- [Αναφορά API](https://reference.groupdocs.com/redaction/net)
- [Λήψη GroupDocs.Redaction για .NET](https://releases.groupdocs.com/search/net/)
- [Δωρεάν Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/search/10)
- [Απόκτηση Προσωρινής Άδειας](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία Ενημέρωση:** 2026-06-07  
**Δοκιμασμένο Με:** GroupDocs.Search 23.12 and GroupDocs.Redaction 23.12 for .NET  
**Συγγραφέας:** GroupDocs

## Σχετικές Οδηγίες

- [Υλοποίηση GroupDocs.Search και Redaction σε .NET για Διαχείριση Εγγράφων](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Πώς να Βελτιστοποιήσετε το GroupDocs.Redaction για .NET: Οδηγός Αποτελεσματικής Διαχείρισης Ευρετηρίου & Ορθογραφίας](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Απόκτηση Εξέλιξης GroupDocs Redaction και Search σε .NET: Αποτελεσματική Διαχείριση Εγγράφων και Ασφαλής Αναζήτηση](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)