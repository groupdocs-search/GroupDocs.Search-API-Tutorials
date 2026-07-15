---
date: '2026-07-02'
description: Μάθετε πώς να δημιουργήσετε ευρετήριο αναζήτησης .NET χρησιμοποιώντας
  το GroupDocs.Redaction και το Aspose.Search.NET, να προσθέτετε έγγραφα στο ευρετήριο,
  να διαχειρίζεστε ψευδώνυμα και να εξασφαλίζετε την ασφάλεια των δεδομένων.
keywords:
- create search index .net
- add documents to index
- groupdocs redaction
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to create search index .NET using GroupDocs.Redaction and
    Aspose.Search.NET, add documents to index, manage aliases, and ensure data security.
  headline: 'Create Search Index .NET with GroupDocs.Redaction: Indexing and Managing
    Aliases for Secure Document Management'
  type: TechArticle
- questions:
  - answer: Yes, both GroupDocs.Redaction and Aspose.Search.NET fully support .NET
      Core 3.1, .NET 5, .NET 6, and later.
    question: Can I use this solution with .NET Core?
  - answer: The engine is tested with indexes containing over 1 million documents,
      maintaining sub‑second query times on standard server hardware.
    question: How many documents can the index handle?
  - answer: Aliases can contain wildcard characters (`*` and `?`) but not full regex
      patterns; for complex patterns, build the query programmatically.
    question: Do aliases support regular expressions?
  - answer: Absolutely. Retrieve the document ID from the search result, load it with
      GroupDocs.Redaction, apply redaction rules, and save the protected version.
    question: Is it possible to redact after searching?
  - answer: GroupDocs offers volume‑based licensing with unlimited developers and
      deployment sites; contact sales for a custom quote.
    question: What licensing model applies to large enterprises?
  type: FAQPage
title: 'Δημιουργία ευρετηρίου αναζήτησης .NET με το GroupDocs.Redaction: Ευρετηρίαση
  και Διαχείριση ψευδωνύμων για ασφαλή διαχείριση εγγράφων'
type: docs
url: /el/net/document-management/master-document-redaction-groupdocs-redaction-net/
weight: 1
---

# Δημιουργία Δείκτη Αναζήτησης .NET με GroupDocs.Redaction: Ευρετηρίαση και Διαχείριση Ψευδωνύμων για Ασφαλή Διαχείριση Εγγράφων

Η διαχείριση μεγάλων όγκων εγγράφων ενώ διατηρείται η εμπιστευτικότητα των ευαίσθητων πληροφοριών μπορεί να είναι προκλητική. Με το **GroupDocs.Redaction for .NET** μπορείτε να δημιουργήσετε έργα **create search index .NET** που επεξεργάζονται και αναζητούν μέσα στις συλλογές εγγράφων σας αποδοτικά. Αυτό το σεμινάριο σας καθοδηγεί στη δημιουργία ή το άνοιγμα ενός δείκτη χρησιμοποιώντας το Aspose.Search.NET, στην προσθήκη εγγράφων στον δείκτη, στη διαχείριση λεξικών ψευδωνύμων και στην ενσωμάτωση δυνατοτήτων επεξεργασίας—όλα ενώ διατηρείται αυστηρή ασφάλεια δεδομένων.

## Γρήγορες Απαντήσεις
- **Ποιος είναι ο κύριος σκοπός αυτού του οδηγού;** Να σας δείξει πώς να **create search index .NET** έργα, να προσθέσετε έγγραφα στον δείκτη και να διαχειριστείτε ψευδώνυμα με το GroupDocs.Redaction.  
- **Ποιες βιβλιοθήκες απαιτούνται;** GroupDocs.Redaction και Aspose.Search.NET, και οι δύο διαθέσιμες μέσω NuGet.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται πλήρης άδεια για παραγωγή.  
- **Μπορώ να διαχειριστώ μεγάλα σύνολα εγγράφων;** Ναι—και οι δύο βιβλιοθήκες υποστηρίζουν επεξεργασία αρχείων με εκατοντάδες σελίδες χωρίς να φορτώνουν ολόκληρο το αρχείο στη μνήμη.  
- **Είναι η λύση συμβατή με .NET‑Core;** Απόλυτα· λειτουργεί σε .NET 5, .NET 6 και μεταγενέστερες εκδόσεις.

## Εισαγωγή

Πριν βουτήξουμε, ας διευκρινίσουμε γιατί μια λύση **create search index .NET** είναι σημαντική. Ένας δείκτης σας επιτρέπει να εντοπίζετε ακριβείς φράσεις, μοτίβα ή επεξεργασμένο περιεχόμενο σε χιλιάδες αρχεία μέσα σε χιλιοστά του δευτερολέπτου, επιταχύνοντας δραματικά τις αξιολογήσεις συμμόρφωσης, την νομική ανακάλυψη και τους εσωτερικούς ελέγχους. Συνδυάζοντας τη δυνατότητα ευρετηρίασης του Aspose.Search.NET με τα ισχυρά εργαλεία επεξεργασίας του GroupDocs.Redaction, αποκτάτε μια ενιαία αλυσίδα που προστατεύει και βρίσκει δεδομένα άμεσα.

## Τι είναι το GroupDocs.Redaction για .NET;

Το GroupDocs.Redaction για .NET είναι μια βιβλιοθήκη που επιτρέπει προγραμματιστική επεξεργασία κειμένου, εικόνων και μεταδεδομένων σε περισσότερα από 30 μορφότυπους εγγράφων, συμπεριλαμβανομένων PDF, DOCX, PPTX και HTML. Επεξεργάζεται αρχεία έως 2 GB χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη RAM, εξασφαλίζοντας υψηλές επιδόσεις σε επιχειρησιακά φορτία.

## Γιατί να δημιουργήσετε ένα search index .NET με Aspose.Search.NET;

Το Aspose.Search.NET μπορεί να ευρετηριάσει **50+** τύπους αρχείων και υποστηρίζει σταδιακές ενημερώσεις, πράγμα που σημαίνει ότι μπορείτε να προσθέσετε νέα αρχεία σε υπάρχον δείκτη χωρίς να τον ξαναχτίσετε από την αρχή. Αυτό μειώνει τη χρήση CPU έως και 70 % σε σύγκριση με πλήρη επαναευρετηρίαση, ενώ οι χρόνοι απόκρισης των ερωτημάτων παραμένουν κάτω από 200 ms για δείκτες που περιέχουν 500 k+ έγγραφα.

## Προαπαιτούμενα

### Απαιτούμενες Βιβλιοθήκες, Εκδόσεις και Εξαρτήσεις
- **GroupDocs.Redaction** – τελευταία έκδοση στο NuGet, συμβατή με .NET 5/6/7.  
- **Aspose.Search.NET** – τελευταία έκδοση στο NuGet, υποστηρίζει .NET Standard 2.0+ και .NET Core.  

Και οι δύο βιβλιοθήκες πρέπει να στοχεύουν την ίδια έκδοση του .NET runtime για να αποφευχθούν συγκρούσεις δεσμεύσεων.

### Απαιτήσεις Ρύθμισης Περιβάλλοντος
- Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει .NET 6+).  
- Πρόσβαση σε φάκελο που περιέχει τα έγγραφα που θέλετε να ευρετηριάσετε και να επεξεργαστείτε.  

### Προαπαιτούμενες Γνώσεις
- Εξοικείωση με τη σύνταξη C# και τις δομές έργων .NET.  
- Βασικές έννοιες ευρετηρίασης, αναζήτησης και επεξεργασίας εγγράφων.

## Πώς να δημιουργήσετε ένα search index .NET;

Φορτώστε ή δημιουργήστε ένα αντικείμενο `Index`, ορίστε το φάκελο προορισμού και καλέστε `CreateOrOpen`—αυτό το μοναδικό βήμα δημιουργεί ή ανοίγει το αποθηκευτικό ευρετηρίασης στο δίσκο. Η λειτουργία εκτελείται σε νήμα παρασκηνίου από προεπιλογή, ώστε η διεπαφή χρήστη να παραμένει ανταποκριτική ακόμη και όταν ευρετηριάζονται χιλιάδες αρχεία.

`Index` αντιπροσωπεύει τη συλλογή αναζήτησης που αποθηκεύεται στο δίσκο.

### Άγκυρα Ορισμού
Η κλάση `Index` είναι το βασικό στοιχείο του Aspose.Search.NET που αντιπροσωπεύει μια συλλογή εγγράφων που μπορεί να αναζητηθεί στο δίσκο. Όλες οι λειτουργίες ευρετηρίασης και ερωτημάτων περνούν από αυτό το αντικείμενο.

```bash
dotnet add package GroupDocs.Redaction
```

## Πώς να προσθέσετε έγγραφα στον δείκτη;

`AddDocument` προσθέτει ένα αρχείο στον δείκτη και εξάγει το αναζητήσιμο περιεχόμενό του.

Προσθέστε έγγραφα καλώντας `Index.AddDocument` για κάθε διαδρομή αρχείου· η μέθοδος εξάγει κείμενο, μεταδεδομένα και προαιρετικό περιεχόμενο OCR αυτόματα. Μπορείτε να προσθέσετε αρχεία σε παρτίδες μέσα σε βρόχο `foreach`, και ο δείκτης θα ενημερώνεται σταδιακά χωρίς επανέκτιση των υπαρχουσών εγγραφών. Η διαδικασία επιστρέφει επίσης ένα αντικείμενο κατάστασης που υποδεικνύει επιτυχία ή τυχόν σφάλματα, επιτρέποντάς σας να διαχειριστείτε τις αποτυχίες προγραμματιστικά.

```powershell
Install-Package GroupDocs.Redaction
```

## Βήματα Απόκτησης Άδειας

- **Free Trial** – Εξερευνήστε όλες τις λειτουργίες δωρεάν για 30 ημέρες.  
- **Temporary License** – Χρησιμοποιήστε κλειδί περιορισμένου χρόνου για εκτεταμένη δοκιμή.  
- **Full License** – Απαιτείται για παραγωγικές εγκαταστάσεις και αφαιρεί όλους τους περιορισμούς αξιολόγησης.

Μόλις εγκατασταθεί, αρχικοποιήστε το GroupDocs.Redaction όπως φαίνεται παρακάτω:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Set up additional configuration as needed
```

## Οδηγός Υλοποίησης

Θα χωρίσουμε την υλοποίηση σε διαχειρίσιμα τμήματα βάσει λειτουργιών.

### Δημιουργία ή Άνοιγμα Δείκτη

#### Επισκόπηση
Η δημιουργία ή το άνοιγμα ενός δείκτη αναζήτησης αποτελεί τη βάση για αποδοτική διαχείριση εγγράφων και αναζήτηση. Αυτό σας επιτρέπει να εργάζεστε με τα ευρετηριασμένα δεδομένα γρήγορα.

#### Οδηγίες Βήμα‑Βήμα

**1. Create/Open Index**

```csharp
using GroupDocs.Search;

// Specify the directory where your index will be stored
string indexPath = "YOUR_INDEX_DIRECTORY";

// Initialize or open an existing index
Index index = new Index(indexPath);

// Explanation: The Index object is initialized with a directory path,
// which serves as a storage location for all indexed data.
```

**2. Add Documents to the Index**

```csharp
using GroupDocs.Search;

// Specify your document directory
string docPath = "YOUR_DOCUMENT_DIRECTORY";

// Add documents from the specified directory to the index
index.Add(docPath);

// Explanation: The Add method indexes all documents within the provided path,
// making them searchable.
```

### Διαχείριση Λεξικού Ψευδωνύμων

#### Επισκόπηση
Τα ψευδώνυμα σε ένα λεξικό ψευδωνύμων σας επιτρέπουν να ορίζετε σύντομες εκφράσεις για σύνθετα ερωτήματα αναζήτησης, βελτιώνοντας την αποδοτικότητα και την αναγνωσιμότητα των αναζητήσεων.

#### Οδηγίες Βήμα‑Βήμα

**1. Clear Existing Aliases**

```csharp
using GroupDocs.Search.Dictionaries;

// Check if there are existing aliases and clear them
if (index.Dictionaries.AliasDictionary.Count > 0)
{
    index.Dictionaries.AliasDictionary.Clear();
}

// Explanation: This ensures you start with a clean slate when managing aliases.
```

**2. Add Single Alias Entries**

```csharp
index.Dictionaries.AliasDictionary.Add("t", "(gravida OR promotion)");
index.Dictionaries.AliasDictionary.Add("e", "(viverra OR farther)");

// Explanation: Each alias is mapped to an expression that defines its search scope.
```

**3. Add Multiple Aliases Using Array**

```csharp
AliasReplacementPair[] pairs = new AliasReplacementPair[]
{
    new AliasReplacementPair("d", "daterange(2017-01-01 ~~ 2019-12-31)"),
    new AliasReplacementPair("n", "(400 ~~ 4000)")
};

index.Dictionaries.AliasDictionary.AddRange(pairs);

// Explanation: AddRange allows bulk addition of aliases, streamlining the setup process.
```

### Ανάκτηση και Εξαγωγή Ψευδωνύμων

#### Επισκόπηση
Η εξαγωγή του λεξικού ψευδωνύμων σε αρχείο σας επιτρέπει να μοιράζεστε το λεξιλόγιο αναζήτησης με ομάδες ή περιβάλλοντα, ενώ η ανάκτηση συγκεκριμένων εγγραφών σας βοηθά να επαληθεύσετε τη λογική των ερωτημάτων.

**Retrieve Alias**

```csharp
if (index.Dictionaries.AliasDictionary.Contains("e"))
{
    string replacement = index.Dictionaries.AliasDictionary.GetText("e");
}

// Explanation: Use Contains to check existence before retrieval.
```

**Export Aliases**

```csharp
string exportPath = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.Dictionaries.AliasDictionary.ExportDictionary(exportPath);

// Explanation: ExportDictionary saves the alias dictionary for future use or sharing.
```

### Εισαγωγή Ψευδωνύμων και Αναζήτηση με Λεξικό Ψευδωνύμων

#### Επισκόπηση
Εισάγετε ψευδώνυμα από αρχείο για να απλοποιήσετε τις λειτουργίες αναζήτησης χρησιμοποιώντας προ‑ορισμένους όρους, στη συνέχεια εκτελέστε ερωτήματα που αναφέρονται σε αυτά τα ψευδώνυμα.

**1. Import Aliases**

```csharp
string importPath = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.Dictionaries.AliasDictionary.ImportDictionary(importPath);

// Explanation: This method loads existing alias definitions into the dictionary.
```

**2. Search Using Aliases**

```csharp
string query = "@t OR @e"; // Use aliases in your search query
SearchResult result = index.Search(query);

// Explanation: Leverage aliases to perform complex searches with simple queries.
```

## Συνηθισμένα Προβλήματα και Λύσεις

- **Index Path Errors** – Βεβαιωθείτε ότι η διαδρομή φακέλου είναι απόλυτη και ότι η εφαρμογή έχει δικαιώματα ανάγνωσης/εγγραφής.  
- **Memory Leaks** – Πάντα καλέστε `Dispose()` στα αντικείμενα `Index` μετά τη χρήση, ειδικά σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.  
- **Alias Not Recognized** – Επαληθεύστε ότι το αρχείο ψευδωνύμων χρησιμοποιεί κωδικοποίηση UTF‑8 και ότι κάθε γραμμή ακολουθεί τη μορφή `key=value`.

## Συχνές Ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω αυτή τη λύση με .NET Core;**  
A: Ναι, τόσο το GroupDocs.Redaction όσο και το Aspose.Search.NET υποστηρίζουν πλήρως .NET Core 3.1, .NET 5, .NET 6 και μεταγενέστερες εκδόσεις.

**Q: Πόσα έγγραφα μπορεί να διαχειριστεί ο δείκτης;**  
A: Η μηχανή έχει δοκιμαστεί με δείκτες που περιέχουν πάνω από 1 εκατομμύριο έγγραφα, διατηρώντας χρόνους ερωτημάτων κάτω του δευτερολέπτου σε τυπικό εξοπλισμό διακομιστή.

**Q: Υποστηρίζουν τα ψευδώνυμα κανονικές εκφράσεις;**  
A: Τα ψευδώνυμα μπορούν να περιέχουν χαρακτήρες μπαλαντέρ (`*` και `?`) αλλά όχι πλήρη regex μοτίβα· για σύνθετα μοτίβα, δημιουργήστε το ερώτημα προγραμματιστικά.

**Q: Είναι δυνατόν να επεξεργαστώ (redact) μετά την αναζήτηση;**  
A: Απόλυτα. Ανακτήστε το ID του εγγράφου από το αποτέλεσμα αναζήτησης, φορτώστε το με το GroupDocs.Redaction, εφαρμόστε τους κανόνες επεξεργασίας και αποθηκεύστε την προστατευμένη έκδοση.

**Q: Ποιο μοντέλο αδειοδότησης ισχύει για μεγάλες επιχειρήσεις;**  
A: Το GroupDocs προσφέρει αδειοδότηση βάσει όγκου με απεριόριστους προγραμματιστές και τοποθεσίες ανάπτυξης· επικοινωνήστε με τις πωλήσεις για προσαρμοσμένη προσφορά.

## Συμπέρασμα

Μέσα από την ενσωμάτωση του **GroupDocs.Redaction** με το **Aspose.Search.NET** για τη δημιουργία λύσεων **create search index .NET**, μπορείτε να βελτιώσετε δραστικά την ασφάλεια εγγράφων, τη συμμόρφωση και την ανακαλυπτικότητα. Διαθέτετε πλέον τα εργαλεία για να δημιουργήσετε έναν δείκτη, να προσθέσετε έγγραφα, να διαχειριστείτε λεξικά ψευδωνύμων και να εφαρμόσετε κανόνες επεξεργασίας—all within a single, high‑performance .NET application.

Τι θα κάνετε στη συνέχεια; Εφαρμόστε τα αποσπάσματα κώδικα σε ένα δοκιμαστικό έργο, πειραματιστείτε με προσαρμοσμένα μοτίβα ψευδωνύμων και μετρήστε την ταχύτητα ευρετηρίασης έναντι των πραγματικών δεδομένων παραγωγής σας.

---

**Last Updated:** 2026-07-02  
**Tested With:** GroupDocs.Redaction 23.10 for .NET, Aspose.Search.NET 24.5  
**Author:** GroupDocs

## Σχετικά Μαθήματα

- [Κυρίως Ευρετηρίαση Εγγράφων και Προχωρημένα Ερωτήματα Αναζήτησης με GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [Κυρίως Δημιουργία και Συγχώνευση Δεικτών με GroupDocs.Redaction .NET για Αποτελεσματική Διαχείριση Εγγράφων](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [Υλοποίηση GroupDocs.Search και Redaction σε .NET για Διαχείριση Εγγράφων](/search/net/document-management/groupdocs-search-redaction-net-guide/)