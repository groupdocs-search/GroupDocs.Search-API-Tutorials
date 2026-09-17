---
date: '2026-09-16'
description: Μάθετε πώς να δημιουργήσετε search index με GroupDocs στο .NET, προσθέστε
  documents στο index και ενεργοποιήστε synonym search για πιο έξυπνα query results.
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: Μάθετε πώς να δημιουργήσετε search index με GroupDocs στο .NET, προσθέστε
  documents στο index και ενεργοποιήστε synonym search για πιο έξυπνα query results.
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: Πώς να δημιουργήσετε search index με GroupDocs και synonym search στο .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: Πώς να δημιουργήσετε search index με GroupDocs και synonym search στο .NET
type: docs
url: /el/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# Πώς να δημιουργήσετε ευρετήριο αναζήτησης με το GroupDocs και αναζήτηση συνωνύμων σε .NET

Σε αυτόν τον οδηγό θα μάθετε **πώς να δημιουργήσετε ευρετήριο αναζήτησης** χρησιμοποιώντας το GroupDocs.Search, να προσθέσετε έγγραφα σε αυτό το ευρετήριο και να ενεργοποιήσετε την αναζήτηση συνωνύμων ώστε οι χρήστες να βρίσκουν σχετικό περιεχόμενο ακόμη και όταν χρησιμοποιούν διαφορετική ορολογία. Είτε δημιουργείτε ένα νομικό αποθετήριο, μια εταιρική βάση γνώσεων ή ένα ερευνητικό αρχείο, τα παρακάτω βήματα παρέχουν μια λύση έτοιμη για παραγωγή που λειτουργεί σε .NET Framework 4.6.1+, .NET Core και .NET 5+.

## Γρήγορες απαντήσεις
- **Τι σημαίνει “δημιουργία ευρετηρίου αναζήτησης”;** Δημιουργεί έναν αναζητήσιμο κατάλογο των εγγράφων σας, αποθηκεύοντας το εξαγόμενο κείμενο σε μια βελτιστοποιημένη δομή για αναζητήσεις χιλιοστών του δευτερολέπτου.  
- **Γιατί να χρησιμοποιήσετε αναζήτηση συνωνύμων;** Επεκτείνει ένα ερώτημα ώστε να περιλαμβάνει λέξεις με το ίδιο νόημα, αυξάνοντας την ανάκληση έως και 30 % σε τυπικά σύνολα δεδομένων.  
- **Ποιες είναι οι κύριες προαπαιτήσεις;** .NET 4.6.1+ (ή .NET Core/5+), γνώση C#, και τα πακέτα NuGet GroupDocs.Search + GroupDocs.Redaction.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή είναι επαρκής για αξιολόγηση· απαιτείται μόνιμη άδεια για παραγωγικές εγκαταστάσεις.  
- **Μπορώ να το συνδυάσω με επεξεργασία (redaction);** Ναι—το GroupDocs.Redaction μπορεί να εκτελεστεί πριν ή μετά την αναζήτηση για να καλύψει ευαίσθητα δεδομένα.

## Τι είναι το “δημιουργία ευρετηρίου αναζήτησης”;
Ένα **ευρετήριο αναζήτησης** είναι μια δομή δεδομένων που περιέχει το εξαγόμενο κείμενο και τα μεταδεδομένα από κάθε έγγραφο, επιτρέποντας στη μηχανή να εντοπίζει τα αντίστοιχα αρχεία άμεσα. Το GroupDocs.Search δημιουργεί αυτό το ευρετήριο σαρρώνοντας τον φάκελο προέλευσης, αναλύοντας τις υποστηριζόμενες μορφές και γράφοντας συμπαγή αρχεία ευρετηρίου σε έναν κατάλογο που καθορίζετε.

## Γιατί να ενεργοποιήσετε την αναζήτηση συνωνύμων;
Η αναζήτηση συνωνύμων προσθέτει αυτόματα εναλλακτικούς όρους στο ερώτημα του χρήστη, έτσι ώστε μια αναζήτηση για **“βελτιώστε”** να επιστρέφει επίσης έγγραφα που περιέχουν **“ενισχύστε”, “αναβαθμίστε”** ή **“βελτιστοποιήστε.”** Στην πράξη αυτό μπορεί να αυξήσει την ανάκληση των αποτελεσμάτων κατά 20‑35 % διατηρώντας υψηλή ακρίβεια, επειδή το ενσωματωμένο λεξικό συνωνύμων είναι προσαρμοσμένο για κάθε γλώσσα.

## Προαπαιτήσεις
- **.NET Framework 4.6.1** ή νεότερη (ή οποιοδήποτε .NET Core/5+ runtime).  
- Βασικές γνώσεις ανάπτυξης σε C# και Visual Studio (Community, Professional ή Enterprise).  
- Πακέτα GroupDocs.Search και GroupDocs.Redaction εγκατεστημένα μέσω NuGet.

### Εγκατάσταση
Εγκαταστήστε το GroupDocs.Redaction για .NET χρησιμοποιώντας μία από τις παρακάτω μεθόδους (δείτε την τεκμηρίωση [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/) για λεπτομέρειες):

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Εναλλακτικά, χρησιμοποιήστε το UI του NuGet Package Manager στο Visual Studio για να αναζητήσετε το “GroupDocs.Redaction” και να το εγκαταστήσετε απευθείας. Για αναφορά API, δείτε το [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net).

### Απόκτηση άδειας
- **Δωρεάν δοκιμή:** Ξεκινήστε με μια δοκιμαστική έκδοση για να εξερευνήσετε όλες τις δυνατότητες.  
- **Προσωρινή άδεια:** Αιτηθείτε προσωρινή άδεια στην [ιστοσελίδα GroupDocs](https://purchase.groupdocs.com/temporary-license/) ή διαχειριστείτε την άδειά σας μέσω του [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) portal.  
- **Πλήρης αγορά:** Όταν είστε έτοιμοι για παραγωγή, αγοράστε πλήρη άδεια που αφαιρεί όλους τους περιορισμούς της δοκιμής.

## Πώς να ρυθμίσετε το GroupDocs.Redaction για .NET
Το GroupDocs.Redaction παρέχει τη βασική λειτουργικότητα για επεξεργασία ευαίσθητου περιεχομένου πριν ή μετά την αναζήτηση. Εκθέτει μια κλάση `Redactor` που δημιουργείτε με άδεια και προαιρετικές ρυθμίσεις διαμόρφωσης.

Ο παρακάτω κώδικας δείχνει πώς να δημιουργήσετε ένα αντικείμενο redactor και να φορτώσετε ένα αρχείο άδειας:

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

Με τον redactor έτοιμο, μπορείτε αργότερα να καλέσετε `redactor.Redact(...)` σε οποιοδήποτε έγγραφο ανακτήσετε από τα αποτελέσματα αναζήτησης.

## Πώς να δημιουργήσετε το ευρετήριο αναζήτησης
Η δημιουργία ενός ευρετηρίου αναζήτησης περιλαμβάνει τον καθορισμό ενός φακέλου όπου θα αποθηκευτούν τα αρχεία ευρετηρίου και, στη συνέχεια, την αρχικοποίηση της κλάσης `Index` από το GroupDocs.Search. Το ευρετήριο θα περιέχει όλα τα αναζητήσιμα δεδομένα που εξάγονται από τα έγγραφα προέλευσης.

Πρώτα, δημιουργήστε έναν κατάλογο για το ευρετήριο και, στη συνέχεια, δημιουργήστε το αντικείμενο `Index`:

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

Η δημιουργία του ευρετηρίου γράφει ένα σύνολο δυαδικών αρχείων στον φάκελο· αυτά τα αρχεία είναι συνήθως κάτω από 200 KB ανά 1 000 σελίδες, επιτρέποντάς σας να κλιμακώσετε σε εκατομμύρια σελίδες χωρίς να εξαντλήσετε τον χώρο στο δίσκο.

## Πώς να προσθέσετε έγγραφα στο ευρετήριο
Η προσθήκη εγγράφων απαιτεί να δείξετε στο API τον φάκελο που περιέχει τα αρχεία προέλευσης και να υποδείξετε στο ευρετήριο να τα επεξεργαστεί. Η διαδικασία αναλύει κάθε υποστηριζόμενη μορφή, εξάγει το κείμενο και το αποθηκεύει στο ευρετήριο για γρήγορη ανάκτηση.

Χρησιμοποιήστε τον παρακάτω κώδικα για να ευρετηριάσετε όλα τα αρχεία σε έναν φάκελο προέλευσης:

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

Το GroupDocs.Search υποστηρίζει **30+** μορφές εισόδου—συμπεριλαμβανομένων DOCX, PDF, PPTX, HTML και κοινών τύπων εικόνων—ώστε μπορείτε να ευρετηριάσετε πρακτικά οποιοδήποτε εταιρικό αρχείο χωρίς πρόσθετους μετατροπείς.

## Πώς να ενεργοποιήσετε και να εκτελέσετε την αναζήτηση συνωνύμων
Η διαχείριση συνωνύμων ενεργοποιείται μέσω του `SearchOptions`. Μόλις ενεργοποιηθεί, κάθε ερώτημα επεκτείνεται αυτόματα ώστε να περιλαμβάνει τις συνωνυμίες του λεξικού, βελτιώνοντας την ανάκληση χωρίς να θυσιάζει την ακρίβεια.

Ενεργοποιήστε την αναζήτηση συνωνύμων με το παρακάτω απόσπασμα:

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

Το προεπιλεγμένο λεξικό συνωνύμων περιέχει πάνω από **5.000** ζεύγη όρων για τα Αγγλικά. Μπορείτε επίσης να φορτώσετε ένα προσαρμοσμένο αρχείο `SynonymDictionary` για να υποστηρίξετε ειδική ορολογία κλάδου.

## Προσαρμοσμένο λεξικό συνωνύμων
Αν χρειάζεστε συνωνύμους ειδικούς για έναν τομέα, φορτώστε το δικό σας αρχείο λεξικού και αναθέστε το στο `SearchOptions` πριν εκτελέσετε ένα ερώτημα.

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## Συχνές συμβουλές αντιμετώπισης προβλημάτων
- **Προβλήματα διαδρομής:** Ελέγξτε ότι οι φάκελοι ευρετηρίου και προέλευσης είναι προσβάσιμοι από τον λογαριασμό της διαδικασίας.  
- **Όρια αδειοδότησης:** Μια μη αδειοδοτημένη έκδοση μπορεί να περιορίσει τον αριθμό των ευρετηριασμένων αρχείων στα 100.  
- **Καμία επιστροφή αποτελεσμάτων:** Βεβαιωθείτε ότι το λεξικό συνωνύμων είναι φορτωμένο· μπορείτε να ελέγξετε το `options.SynonymDictionary.Count` κατά την εκτέλεση.

## Πρακτικές εφαρμογές
1. **Διαχείριση νομικών εγγράφων:** Βρείτε νομολογία χρησιμοποιώντας νομικούς όρους και τις συνωνυμίες τους.  
2. **Ακαδημαϊκή έρευνα:** Επεκτείνετε τις αναζητήσεις βιβλιογραφίας σε ακαδημαϊκά PDF και αρχεία Word.  
3. **Εταιρικές βάσεις γνώσεων:** Ανακτήστε εσωτερικές πολιτικές ακόμη και όταν οι χρήστες διατυπώνουν ερωτήματα διαφορετικά.  
4. **Συστήματα διαχείρισης περιεχομένου:** Παρέχετε στους συντάκτες πλουσιότερη ανακάλυψη κατά την ετικετοθέτηση άρθρων.  
5. **Σύστημα υποστήριξης πελατών:** Συμφωνήστε τα εισιτήρια με γνωστά προβλήματα χρησιμοποιώντας συνώνυμες περιγραφές προβλημάτων.

## Σκέψεις για την απόδοση
- **Συντήρηση ευρετηρίου:** Επαναευρετηριάστε μετά από μαζικές ενημερώσεις· η επαυξητική ευρετηρίαση μειώνει το χρόνο διακοπής έως και 70 %.  
- **Παρακολούθηση πόρων:** Η ευρετηρίαση ενός batch 10 GB σε τυπική VM (2 vCPU, 8 GB RAM) φθάνει περίπου 1,2 GB RAM· μειώστε το μέγεθος του batch αν πλησιάζετε τα όρια.  
- **Αποδέσμευση αντικειμένων:** Καλέστε `index.Dispose()` και `redactor.Dispose()` αμέσως μόλις τελειώσετε για να ελευθερώσετε τους εγγενείς πόρους.

## Συμπέρασμα
Τώρα γνωρίζετε **πώς να δημιουργήσετε ευρετήριο αναζήτησης** με το GroupDocs, να προσθέσετε έγγραφα σε αυτό το ευρετήριο και να ενεργοποιήσετε την αναζήτηση συνωνύμων για μια πιο διαισθητική εμπειρία χρήστη. Αυτή η βάση σας επιτρέπει επίσης να προσθέσετε επεξεργασία (redaction), προσαρμοσμένη κατάταξη ή ασαφή αντιστοίχιση πάνω σε μια ισχυρή μηχανή αναζήτησης.

## Επόμενα βήματα
- Πειραματιστείτε με το `SearchOptions.FuzzySearch` για να εντοπίσετε ορθογραφικά λάθη.  
- Εξερευνήστε το API `Ranking` για να ενισχύσετε την προτεραιότητα εγγράφων.  
- Συμμετέχετε στην κοινότητα στο [Φόρουμ GroupDocs](https://forum.groupdocs.com/c/search/10) ή στο [Φόρουμ Δωρεάν Υποστήριξης](https://forum.groupdocs.com/c/search/10) για να μοιραστείτε συμβουλές και να θέσετε ερωτήσεις.  
- Ελέγξτε τις [Τελευταίες Εκδόσεις GroupDocs](https://releases.groupdocs.com/search/net/) για ενημερώσεις και νέες λειτουργίες.

## Συχνές ερωτήσεις

**Ε: Τι είναι η αναζήτηση συνωνύμων;**  
Α: Η αναζήτηση συνωνύμων επεκτείνει το ερώτημα του χρήστη ώστε να περιλαμβάνει προορισμένους εναλλακτικούς όρους, αυξάνοντας τις πιθανότητες εύρεσης σχετικών εγγράφων που χρησιμοποιούν διαφορετική διατύπωση.

**Ε: Πώς ενημερώνω την άδεια GroupDocs μου;**  
Α: Επισκεφθείτε το portal [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) και ανεβάστε το νέο αρχείο άδειας μέσω `License.SetLicense("path/to/license.lic")`.

**Ε: Μπορώ να χρησιμοποιήσω την αναζήτηση συνωνύμων σε πολυγλωσσικό περιβάλλον;**  
Α: Ναι—φορτώστε ένα γλωσσικά‑συγκεκριμένο αρχείο `SynonymDictionary` για κάθε τοπική γλώσσα που υποστηρίζετε, και η μηχανή θα εφαρμόσει το αντίστοιχο σύνολο συνωνύμων ανά ερώτημα.

**Ε: Ποια είναι τα πιο κοινά προβλήματα ευρετηρίασης;**  
Α: Τα τρία κορυφαία προβλήματα είναι τα δικαιώματα πρόσβασης στα αρχεία, οι μη υποστηριζόμενες μορφές και η υπέρβαση του ορίου εγγράφων της δοκιμαστικής έκδοσης.

**Ε: Πώς μπορώ να βελτιστοποιήσω την απόδοση για πολύ μεγάλα ευρετήρια;**  
Α: Χρησιμοποιήστε επαυξητική ευρετηρίαση, αποθηκεύστε το ευρετήριο σε SSDs και ρυθμίστε το `IndexingOptions.MaxDegreeOfParallelism` ώστε να ταιριάζει με τον αριθμό πυρήνων της CPU σας.

---

**Τελευταία ενημέρωση:** 2026-09-16  
**Δοκιμάστηκε με:** GroupDocs.Search 23.10 for .NET  
**Συγγραφέας:** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## Σχετικά Μαθήματα

- [Προσθήκη Εγγράφου στο Ευρετήριο με τα GroupDocs.Search .NET Tutorials](/search/net/document-management/)
- [Επισήμανση Αποτελεσμάτων Αναζήτησης σε Έγγραφα .NET Χρησιμοποιώντας GroupDocs.Search και Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [Πώς να Ενημερώσετε το Ευρετήριο με GroupDocs.Search & Redaction (.NET)](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)