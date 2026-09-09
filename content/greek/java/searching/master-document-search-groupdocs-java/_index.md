---
date: '2026-08-10'
description: Μάθετε πώς να δημιουργείτε ευρετήριο εγγράφων και να προσθέτετε έγγραφα
  στο ευρετήριο χρησιμοποιώντας το GroupDocs.Search for Java. Δημιουργήστε ισχυρές
  εφαρμογές αναζήτησης με ερωτήματα κειμένου και αντικειμένων.
keywords:
- how to index documents
- create search index
- index pdf files
- search word documents
- update search index
lastmod: '2026-08-10'
og_description: Μάθετε πώς να δημιουργείτε ευρετήριο εγγράφων με το GroupDocs.Search
  for Java. Οδηγός βήμα‑βήμα για τη δημιουργία ενός search index, την προσθήκη αρχείων
  PDFs, Word, Excel και την εκτέλεση γρήγορων queries.
og_image_alt: Code example showing Java indexing with GroupDocs.Search
og_title: Πώς να δημιουργήσετε ευρετήριο εγγράφων με το GroupDocs.Search for Java
  – Οδηγός γρήγορης αναζήτησης
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to index documents and add documents to index using GroupDocs.Search
    for Java. Build powerful search apps with text and object queries.
  headline: How to index documents with GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to index documents and add documents to index using GroupDocs.Search
    for Java. Build powerful search apps with text and object queries.
  name: How to index documents with GroupDocs.Search for Java
  steps:
  - name: '**Free trial** – explore the library without cost.'
    text: '**Free trial** – explore the library without cost.'
  - name: '**Temporary license** – request a short‑term key for extended evaluation.'
    text: '**Temporary license** – request a short‑term key for extended evaluation.'
  - name: '**Purchase** – obtain a full license for production use.'
    text: '**Purchase** – obtain a full license for production use.'
  - name: '**Legal document management** – locate clauses, case numbers, or dates
      across thousands of contracts in seconds.'
    text: '**Legal document management** – locate clauses, case numbers, or dates
      across thousands of contracts in seconds.'
  - name: '**Financial reporting** – pull transactions that fall within a specific
      monetary range without scanning each spreadsheet.'
    text: '**Financial reporting** – pull transactions that fall within a specific
      monetary range without scanning each spreadsheet.'
  - name: '**Inventory tracking** – find items by serial numbers, batch codes, or
      SKU ranges across a distributed file system.'
    text: '**Inventory tracking** – find items by serial numbers, batch codes, or
      SKU ranges across a distributed file system.'
  type: HowTo
- questions:
  - answer: Call `index.add("NEW_DOCUMENT_PATH")` again; the library merges the new
      entries without recreating the whole index.
    question: How do I update an existing index with new documents?
  - answer: Yes, it supports 30+ formats—including PDF, DOCX, XLSX, PPTX, TXT, and
      HTML—so you can index virtually any business document.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Java 8+ runtime, at least 2 GB RAM for modest collections (larger sets
      benefit from 4 GB+), and read/write access to the index folder.
    question: What are the system requirements for using GroupDocs.Search?
  - answer: Keep the index up‑to‑date, profile your queries, and review JVM memory
      settings. Reducing the number of indexed fields or using object queries can
      also speed up execution.
    question: How can I troubleshoot search performance issues?
  - answer: Yes, you can enable synonym dictionaries and fuzzy search via the `SearchOptions`
      class to broaden matching without sacrificing relevance. The `SearchOptions`
      class configures advanced search behavior such as synonyms and fuzzy matching.
    question: Is there support for synonyms or fuzzy matching?
  type: FAQPage
tags:
- document indexing
- GroupDocs.Search
- Java search library
- search API
- indexing tutorial
title: Πώς να δημιουργήσετε ευρετήριο εγγράφων με το GroupDocs.Search for Java
type: docs
url: /el/java/searching/master-document-search-groupdocs-java/
weight: 1
---

# Πώς να δημιουργήσετε ευρετήριο εγγράφων με το GroupDocs.Search για Java

Στον σημερινό κόσμο που βασίζεται στα δεδομένα, η **πώς να δημιουργήσετε ευρετήριο εγγράφων** αποτελεσματικά είναι μια κρίσιμη δεξιότητα για κάθε προγραμματιστή Java που διαχειρίζεται μεγάλες συλλογές αρχείων. Είτε επεξεργάζεστε νομικές συμβάσεις, οικονομικές καταστάσεις ή εσωτερικές αναφορές, ένα καλά κατασκευασμένο ευρετήριο αναζήτησης σας επιτρέπει να εντοπίζετε το ακριβές κομμάτι πληροφορίας σε δευτερόλεπτα αντί για ώρες χειροκίνητης σάρωσης. Αυτό το σεμινάριο σας καθοδηγεί στη δημιουργία ευρετηρίου αναζήτησης, την προσθήκη εγγράφων και την εκτέλεση ερωτημάτων κειμένου και αντικειμένου με το GroupDocs.Search για Java.

## Γρήγορες απαντήσεις
- **Ποιο είναι το πρώτο βήμα για τη δημιουργία ευρετηρίου εγγράφων;** Δημιουργήστε ένα αντικείμενο `Index` που δείχνει σε ένα φάκελο όπου θα αποθηκευτούν τα αρχεία του ευρετηρίου.  
- **Ποια μέθοδος προσθέτει έγγραφα σε ένα ευρετήριο;** Κλήστε `index.add("PATH_TO_DOCUMENTS")` για να σαρώσετε έναν κατάλογο και να εισάγετε τα υποστηριζόμενα αρχεία.  
- **Μπορώ να αναζητήσω αριθμητικές περιοχές;** Ναι – χρησιμοποιήστε ένα ερώτημα κειμένου όπως `"400 ~~ 4000"` ή ένα ερώτημα αντικειμένου μέσω `SearchQuery.createNumericRangeQuery`. Η μέθοδος `createNumericRangeQuery` δημιουργεί ένα αντικείμενο ερωτήματος αριθμητικής περιοχής.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· μια εμπορική άδεια ξεκλειδώνει το πλήρες σύνολο λειτουργιών και αφαιρεί τους περιορισμούς χρήσης.  
- **Ποια έκδοση Java απαιτείται;** Υποστηρίζεται το JDK 8 ή νεότερο.

## Τι είναι η δημιουργία ευρετηρίου εγγράφων με το GroupDocs.Search;
Η δημιουργία ευρετηρίου εγγράφων δημιουργεί ένα αποθηκευτικό χώρο διακριτικών αναζητήσιμων για κάθε αρχείο, επιτρέποντας στη μηχανή να ανακτά τα αποτελέσματα χωρίς να διαβάζει τα αρχικά αρχεία κάθε φορά. Αυτό το βήμα προεπεξεργασίας μετατρέπει το ακατέργαστο περιεχόμενο σε ένα βελτιστοποιημένο ευρετήριο που μπορεί να ερωτηθεί σε χιλιοστά του δευτερολέπτου. Το ευρετήριο αποθηκεύει όρους, θέσεις και μεταδεδομένα, επιτρέποντας γρήγορες αναζητήσεις φράσεων και εγγύτητας σε όλους τους υποστηριζόμενους τύπους εγγράφων.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για Java;
Οι λειτουργίες αναζήτησης ολοκληρώνονται συνήθως σε λιγότερο από 50 ms σε μια συλλογή 10 000 αρχείων (μέσο όγκο 1 KB το καθένα) που τρέχει σε μια τυπική VM με 2‑CPU και 8 GB RAM. Η βιβλιοθήκη υποστηρίζει **30+ μορφές εισόδου και εξόδου**—συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX, TXT και HTML—ώστε να μπορείτε να δημιουργήσετε ευρετήριο σχεδόν οποιουδήποτε επιχειρηματικού εγγράφου χωρίς πρόσθετους μετατροπείς. Το ευέλικτο API της επιτρέπει να συνδυάζετε ερωτήματα απλού κειμένου, αριθμητικές περιοχές και σύνθετα ερωτήματα αντικειμένου, ενώ οι επαυξομενικές ενημερώσεις σας επιτρέπουν να προσθέτετε νέα αρχεία χωρίς να ξαναδημιουργήσετε ολόκληρο το ευρετήριο.

## Προαπαιτούμενα
- Maven εγκατεστημένο για διαχείριση εξαρτήσεων.  
- Ένα IDE όπως IntelliJ IDEA ή Eclipse.  
- Βασικές γνώσεις Java (έννοιες OOP, διαχείριση εξαιρέσεων).  

## Ρύθμιση του GroupDocs.Search για Java
### Ρύθμιση Maven
Προσθέστε το αποθετήριο και την εξάρτηση στο `pom.xml` σας:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

### Άμεση λήψη
Μπορείτε επίσης να κατεβάσετε το τελευταίο JAR από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Βήματα απόκτησης άδειας
1. **Δωρεάν δοκιμή** – εξερευνήστε τη βιβλιοθήκη χωρίς κόστος.  
2. **Προσωρινή άδεια** – ζητήστε ένα βραχυπρόθεσμο κλειδί για εκτεταμένη αξιολόγηση.  
3. **Αγορά** – αποκτήστε πλήρη άδεια για παραγωγική χρήση.

## Βασική αρχικοποίηση και ρύθμιση
Για **προσθήκη εγγράφων στο ευρετήριο**, πρώτα δημιουργείτε ένα αντικείμενο `Index` που δείχνει στο φάκελο όπου θα αποθηκευτούν τα αρχεία του ευρετηρίου:

`Index` είναι η βασική κλάση που αντιπροσωπεύει ένα αναζητήσιμο ευρετήριο στο δίσκο.  
```java
import com.groupdocs.search.Index;

// Initialize the index by specifying a directory path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");
```

Αυτή η γραμμή δημιουργεί (ή ανοίγει) ένα ευρετήριο έτοιμο να λάβει έγγραφα.

## Οδηγός υλοποίησης
### Δημιουργία και ευρετηρίαση εγγράφων
#### Πώς να προσθέσετε έγγραφα στο ευρετήριο
Η μέθοδος `add` σαρώει έναν φάκελο και αποθηκεύει αναζητήσιμα δεδομένα για κάθε αρχείο. Επεξεργάζεται αναδρομικά κάθε υποστηριζόμενο έγγραφο, εξάγει κείμενο και μεταδεδομένα, και γράφει διακριτικά στο φάκελο ευρετηρίου που καθορίσατε νωρίτερα.

```java
import com.groupdocs.search.Index;

// Initialize an index at the specified path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");

// Add documents from a directory for indexing
index.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Παράμετροι:** Η συμβολοσειρά διαδρομής δείχνει στο φάκελο που περιέχει τα αρχεία που θέλετε να ευρετηριάσετε.  
- **Σκοπός:** Μετά από αυτό το βήμα, το ευρετήριο περιέχει διακριτικά από όλους τους υποστηριζόμενους τύπους εγγράφων, επιτρέποντας γρήγορες αναζητήσεις σε ολόκληρη τη συλλογή.

## Αναζήτηση με ερώτημα κειμένου
#### Πώς να εκτελέσετε αναζήτηση αριθμητικής περιοχής με κείμενο
Μπορείτε να αναζητήσετε χρησιμοποιώντας μια απλή συμβολοσειρά που ορίζει μια περιοχή. Η μηχανή ερμηνεύει τον τελεστή `~~` ως “μεταξύ” και επιστρέφει όλα τα έγγραφα που περιέχουν αριθμούς εντός των καθορισμένων ορίων.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define a query for numeric values within a specific range
String query1 = "400 ~~ 4000";

// Execute text-based search on indexed data
SearchResult result1 = index.search(query1);
```

- **Παράμετροι:** Η συμβολοσειρά ερωτήματος `"400 ~~ 4000"` λέει στη μηχανή να βρει αριθμούς μεταξύ 400 και 4000.  
- **Τιμή επιστροφής:** Το `SearchResult` περιέχει τη λίστα των ταιριασμένων εγγράφων και επισημαίνει τα ταιριαστά τμήματα.

## Αναζήτηση με ερώτημα αντικειμένου
#### Πώς να χρησιμοποιήσετε ερώτημα αντικειμένου για αριθμητικές περιοχές
Τα ερωτήματα βασισμένα σε αντικείμενα σας δίνουν προγραμματιστικό έλεγχο στα κριτήρια αναζήτησης, επιτρέποντας να συνδυάσετε πολλαπλές συνθήκες ή να δημιουργήσετε ερωτήματα δυναμικά κατά την εκτέλεση.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Create a numeric range query object
SearchQuery query2 = SearchQuery.createNumericRangeQuery(400, 4000);

// Perform search using the query object
SearchResult result2 = index.search(query2);
```

- **Παράμετροι:** Η `createNumericRangeQuery` λαμβάνει τους αρχικούς και τελικούς ακέραιους.  
- **Σκοπός:** Αυτή η μέθοδος είναι ιδανική όταν χρειάζεται να φιλτράρετε τα αποτελέσματα με βάση αριθμητικά πεδία όπως σύνολα τιμολογίων, ηλικίες ή κωδικούς προϊόντων.

## Πρακτικές εφαρμογές
Ακολουθούν μερικά πραγματικά σενάρια όπου η **δημιουργία ευρετηρίου εγγράφων** γίνεται καθοριστική:

1. **Διαχείριση νομικών εγγράφων** – εντοπίστε ρήτρες, αριθμούς υποθέσεων ή ημερομηνίες σε χιλιάδες συμβάσεις σε δευτερόλεπτα.  
2. **Οικονομική αναφορά** – εξάγετε συναλλαγές που εμπίπτουν σε συγκεκριμένο χρηματικό εύρος χωρίς να σαρώσετε κάθε λογιστικό φύλλο.  
3. **Παρακολούθηση αποθεμάτων** – βρείτε αντικείμενα με βάση σειριακούς αριθμούς, κωδικούς παρτίδας ή εύρη SKU σε ένα κατανεμημένο σύστημα αρχείων.  

Η ενσωμάτωση του GroupDocs.Search με βάσεις δεδομένων, αποθήκευση στο cloud ή ουρές μηνυμάτων μπορεί να αυτοματοποιήσει περαιτέρω τις ροές εργασίας εγγράφων.

## Σκέψεις απόδοσης
- **Τακτικές ενημερώσεις ευρετηρίου:** Εκτελέστε ξανά `index.add` για νέα αρχεία ώστε το ευρετήριο να παραμένει ενημερωμένο.  
- **Διαχείριση πόρων:** Παρακολουθήστε τη χρήση heap· μεγάλα ευρετήρια ωφελούνται από ρυθμισμένες ρυθμίσεις συλλογής απορριμμάτων JVM.  
- **Βελτιστοποίηση ερωτημάτων:** Χρησιμοποιήστε ερωτήματα αντικειμένου για σύνθετα φίλτρα ώστε να μειώσετε την περιττή σάρωση και να βελτιώσετε τον χρόνο απόκρισης.

## Συνηθισμένα προβλήματα και λύσεις
| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| **Η αναζήτηση δεν επιστρέφει αποτελέσματα** | Το ευρετήριο δεν έχει δημιουργηθεί ή η διαδρομή φακέλου είναι λανθασμένη | Επαληθεύστε ότι το `index.add` εκτελέστηκε στον σωστό κατάλογο και ότι ο φάκελος του ευρετηρίου είναι εγγράψιμος. |
| **OutOfMemoryError κατά την ευρετηρίαση** | Πολύ μεγάλα αρχεία ή ανεπαρκής heap | Αυξήστε την τιμή JVM `-Xmx` ή ευρετηριάστε τα αρχεία σε μικρότερες παρτίδες. |
| **Μη υποστηριζόμενη μορφή αρχείου** | Ο τύπος αρχείου δεν αναγνωρίζεται από το GroupDocs.Search | Βεβαιωθείτε ότι η επέκταση βρίσκεται στη λίστα υποστηριζόμενων (PDF, DOCX, XLSX, PPTX, TXT, HTML, κ.λπ.). |

## Συχνές ερωτήσεις
**Ε: Πώς ενημερώνω ένα υπάρχον ευρετήριο με νέα έγγραφα;**  
Α: Κλήστε ξανά `index.add("NEW_DOCUMENT_PATH")`; η βιβλιοθήκη συγχωνεύει τις νέες καταχωρήσεις χωρίς να δημιουργήσει ξανά ολόκληρο το ευρετήριο.

**Ε: Μπορεί το GroupDocs.Search να διαχειριστεί διαφορετικές μορφές αρχείων;**  
Α: Ναι, υποστηρίζει 30+ μορφές—συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX, TXT και HTML—ώστε να μπορείτε να ευρετηριάσετε σχεδόν οποιοδήποτε επιχειρηματικό έγγραφο.

**Ε: Ποιες είναι οι απαιτήσεις συστήματος για τη χρήση του GroupDocs.Search;**  
Α: Περιβάλλον εκτέλεσης Java 8+, τουλάχιστον 2 GB RAM για μικρές συλλογές (μεγαλύτερα σύνολα ωφελούνται από 4 GB+), και πρόσβαση ανάγνωσης/εγγραφής στον φάκελο του ευρετηρίου.

**Ε: Πώς μπορώ να αντιμετωπίσω προβλήματα απόδοσης αναζήτησης;**  
Α: Διατηρήστε το ευρετήριο ενημερωμένο, προφίλ τις ερωτήσεις σας και ελέγξτε τις ρυθμίσεις μνήμης JVM. Η μείωση του αριθμού των ευρετηριζόμενων πεδίων ή η χρήση ερωτημάτων αντικειμένου μπορεί επίσης να επιταχύνει την εκτέλεση.

**Ε: Υπάρχει υποστήριξη για συνώνυμα ή ασαφή αντιστοίχιση;**  
Α: Ναι, μπορείτε να ενεργοποιήσετε λεξικά συνωνύμων και ασαφή αναζήτηση μέσω της κλάσης `SearchOptions` για να επεκτείνετε την αντιστοίχιση χωρίς να θυσιάσετε τη συνάφεια. Η κλάση `SearchOptions` διαμορφώνει προχωρημένη συμπεριφορά αναζήτησης όπως συνώνυμα και ασαφή αντιστοίχιση.

---

**Τελευταία ενημέρωση:** 2026-08-10  
**Δοκιμάστηκε με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά μαθήματα

- [Πώς να προσθέσετε έγγραφα στο ευρετήριο με μεταδεδομένα ευρετηρίαση σε Java χρησιμοποιώντας το GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Πώς να προσθέσετε έγγραφα στο ευρετήριο και να διαχειριστείτε ψευδώνυμα στο GroupDocs.Search για Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
- [Πώς να ενημερώσετε το ευρετήριο Java με το GroupDocs.Search – Ένας ολοκληρωμένος οδηγός](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)