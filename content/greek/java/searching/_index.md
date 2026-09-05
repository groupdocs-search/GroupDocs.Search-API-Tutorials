---
date: 2026-05-22
description: Εξερευνήστε τα tutorials full text search java χρησιμοποιώντας το GroupDocs.Search
  για Java, καλύπτοντας case insensitive search java, highlight search results java,
  wildcard search java example και regex search java tutorial.
keywords:
- full text search java
- case insensitive search java
- regex search java
- boolean search java
- fuzzy search java
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Explore full text search java tutorials using GroupDocs.Search for
    Java, covering case insensitive search java, highlight search results java, wildcard
    search java example, and regex search java tutorial.
  headline: Full Text Search Java Tutorials with GroupDocs.Search
  type: TechArticle
- description: Explore full text search java tutorials using GroupDocs.Search for
    Java, covering case insensitive search java, highlight search results java, wildcard
    search java example, and regex search java tutorial.
  name: Full Text Search Java Tutorials with GroupDocs.Search
  steps:
  - name: '**Enterprise document portals** – Quickly locate policies, contracts, or
      manuals across thousands of files.'
    text: '**Enterprise document portals** – Quickly locate policies, contracts, or
      manuals across thousands of files.'
  - name: '**E‑learning platforms** – Enable students to search course materials,
      PDFs, and slide decks.'
    text: '**E‑learning platforms** – Enable students to search course materials,
      PDFs, and slide decks.'
  - name: '**Legal discovery tools** – Perform case‑insensitive and regex searches
      to surface relevant evidence.'
    text: '**Legal discovery tools** – Perform case‑insensitive and regex searches
      to surface relevant evidence.'
  - name: '**Customer support knowledge bases** – Highlight matching snippets to improve
      self‑service experiences.'
    text: '**Customer support knowledge bases** – Highlight matching snippets to improve
      self‑service experiences.'
  type: HowTo
- questions:
  - answer: Yes – provide the password via `SearchOptions.setPassword("yourPassword")`
      before adding the document.
    question: Does GroupDocs.Search support indexing of encrypted PDFs?
  - answer: Absolutely – use `searchEngine.updateDocument(filePath)` to modify or
      replace a single document while preserving the rest of the index.
    question: Can I update an existing index without rebuilding it from scratch?
  - answer: The engine can handle files up to **2 GB** per document; larger files
      are processed in streaming mode to avoid memory pressure.
    question: What is the maximum file size that can be indexed?
  - answer: Yes – configure a `SynonymMap` in `SearchOptions` and the engine will
      automatically expand queries with defined synonyms.
    question: Is there built‑in support for synonym expansion?
  - answer: Subscribe to the `IndexingProgressListener` event; it reports percentage
      completion and elapsed time for each batch.
    question: How do I monitor indexing progress in a large batch job?
  type: FAQPage
title: Πλήρης Αναζήτηση Κειμένου Java Μαθήματα με GroupDocs.Search
type: docs
url: /el/java/searching/
weight: 3
---

# Πλήρης Αναζήτηση Κειμένου Java Μαθήματα με GroupDocs.Search

Αν χρειάζεστε δυνατότητες **full text search java** σε οποιαδήποτε εφαρμογή Java, βρίσκεστε στο σωστό μέρος. Σε αυτό το κέντρο περπατάμε μέσα από παραδείγματα πραγματικού κόσμου—boolean, fuzzy, phrase, wildcard, regex και case‑insensitive αναζητήσεις—χρησιμοποιώντας το GroupDocs.Search for Java API. Είτε δημιουργείτε έναν ελαφρύ προβολέα εγγράφων είτε μια υψηλής απόδοσης επιχειρησιακή μηχανή αναζήτησης, αυτά τα βήμα‑βήμα οδηγίες σας δίνουν τον κώδικα, τις συμβουλές και τις βέλτιστες πρακτικές για γρήγορα, ακριβή αποτελέσματα που κλιμακώνονται.

## Γρήγορες Απαντήσεις
- **Ποιο είναι το σημείο εισόδου για την ευρετηρίαση;** `SearchEngine` class – δημιουργήστε μια παρουσία, προσθέστε έγγραφα, στη συνέχεια καλέστε `save()`.  
- **Πόσες μορφές εγγράφων υποστηρίζονται;** Πάνω από 50 μορφές εισόδου και εξόδου, συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX και απλού κειμένου.  
- **Μπορώ να εκτελέσω αναζητήσεις χωρίς διάκριση πεζών‑κεφαλαίων;** Ναι—χρησιμοποιήστε `SearchOptions.setIgnoreCase(true)` ή διαμορφώστε τον αναλυτή κατά την ευρετηρίαση.  
- **Είναι η αναζήτηση με μπαλαντέρ διαθέσιμη έτοιμη προς χρήση;** Απόλυτα—χρησιμοποιήστε `*` και `?` στις συμβολοσειρές ερωτήματος, π.χ., `doc*ment`.  
- **Χρειάζομαι άδεια για παραγωγή;** Απαιτείται εμπορική άδεια για παραγωγικές εγκαταστάσεις· μια δωρεάν προσωρινή άδεια είναι διαθέσιμη για αξιολόγηση.

## Τι είναι η Πλήρης Αναζήτηση Κειμένου Java;
**Full text search java** είναι η διαδικασία ευρετηρίασης και ερωτήματος του ακατέργαστου κειμένου των εγγράφων απευθείας από κώδικα Java. Σας επιτρέπει να εντοπίζετε λέξεις, φράσεις ή μοτίβα σε μεγάλες συλλογές χωρίς να φορτώνετε κάθε αρχείο στη μνήμη. **Λειτουργεί δημιουργώντας έναν ανεστραμμένο ευρετήριο που αντιστοιχίζει κάθε όρο στα έγγραφα που το περιέχουν, επιτρέποντας γρήγορη αναζήτηση ακόμη και σε τεράστιες συλλογές.**

## Τι είναι το GroupDocs.Search για Java;
Η κλάση `SearchEngine` είναι το βασικό στοιχείο του GroupDocs.Search που αντιπροσωπεύει ένα αποθετήριο ευρετηρίου και παρέχει μεθόδους για ευρετηρίαση, ενημέρωση και ερώτημα εγγράφων. Απομονώνει τη διαχείριση αρχείων, την τοκενικοποίηση και την ανάλυση ερωτημάτων ώστε να εστιάσετε στη λογική της επιχείρησης. **Η μηχανή διαχειρίζεται επίσης γλωσσική‑συγκεκριμένη τοκενικοποίηση, αφαίρεση stop‑words και επέκταση συνωνύμων για βελτίωση της σχετικότητας των αναζητήσεων.**

## Γιατί να Χρησιμοποιήσετε την Πλήρης Αναζήτηση Κειμένου Java με το GroupDocs.Search;
Το GroupDocs.Search επεξεργάζεται **έως 100 εκατομμύρια έγγραφα** και μπορεί να ερωτήσει ένα αρχείο 2 GB σε λιγότερο από 500 ms σε τυπικό εξοπλισμό διακομιστή—χάρη στο βελτιστοποιημένο ανεστραμμένο ευρετήριο και την αρχιτεκτονική lazy loading. Η βιβλιοθήκη υποστηρίζει **50+ μορφές αρχείων**, προσφέρει ενσωματωμένα **boolean, fuzzy, phrase, wildcard, και regex** είδη ερωτημάτων, και σας επιτρέπει να ρυθμίζετε λεπτομερώς την τοκενικοποίηση, τα stop‑words και τη διαχείριση συνωνύμων ανά τομέα.

## Προαπαιτούμενα
- Java 17 ή νεότερη (συμβατή και με Java 8+)  
- Σύστημα κατασκευής Maven ή Gradle  
- Βιβλιοθήκη GroupDocs.Search for Java (λήψη από την επίσημη ιστοσελίδα)  
- Προσωρινό ή εμπορικό κλειδί άδειας  

## Πώς να Υλοποιήσετε την Πλήρης Αναζήτηση Κειμένου Java – Βήμα προς Βήμα
Φορτώστε το `SearchEngine`, προσθέστε έγγραφα και εκτελέστε ένα ερώτημα—όλα σε λίγες συνοπτικές γραμμές.

### Πώς δημιουργείτε και διαμορφώνετε ένα στιγμιότυπο SearchEngine;
Δημιουργήστε ένα `SearchEngine` με διαδρομή φακέλου για το ευρετήριο, στη συνέχεια ορίστε προαιρετικές `SearchOptions` όπως η αδιαφορία πεζών‑κεφαλαίων ή η fuzzy αντιστοίχιση. Αυτό προετοιμάζει τη μηχανή τόσο για ευρετηρίαση όσο και για ερωτήματα. **Μπορείτε επίσης να καθορίσετε προσαρμοσμένο αναλυτή ή να ορίσετε την έκδοση του ευρετηρίου για διατήρηση συμβατότητας με παλαιότερες δομές δεδομένων.**

### Πώς ευρετηριάζετε έγγραφα για full text search java;
Καλέστε `searchEngine.addDocument(filePath)` για κάθε αρχείο που θέλετε να είναι αναζητήσιμο. Η μηχανή εξάγει κείμενο, το τοκενικοποιεί και ενημερώνει αυτόματα το ανεστραμμένο ευρετήριο. Μπορείτε επίσης να ευρετηριάσετε ροές ή byte arrays εάν χρειάζεστε επεξεργασία στη μνήμη. **Το API εντοπίζει αυτόματα τον τύπο του αρχείου, εξάγει κείμενο χρησιμοποιώντας ενσωματωμένους αναλυτές και ενημερώνει το ευρετήριο χωρίς χειροκίνητη προεπεξεργασία.**

### Πώς εκτελείτε ένα boolean ερώτημα java;
Χρησιμοποιήστε τη μέθοδο `searchEngine.search("term1 AND term2 NOT term3")`. Ο αναλυτής ερωτημάτων ερμηνεύει λογικούς τελεστές και επιστρέφει λίστα ταυτοτήτων εγγράφων με βαθμολογίες σχετικότητας. **Πολύπλοκες εκφράσεις μπορούν να συνδυάσουν πολλαπλούς τελεστές και παρενθέσεις για έλεγχο προτεραιότητας, επιτρέποντας ακριβή έλεγχο των συνόλων αποτελεσμάτων.**

### Πώς εκτελείτε αναζήτηση χωρίς διάκριση πεζών‑κεφαλαίων java;
Ορίστε `searchEngine.getOptions().setIgnoreCase(true)` πριν από την ευρετηρίαση ή το ερώτημα. Αυτό λέει στον αναλυτή να κανονικοποιεί όλα τα τοκενά σε πεζά, εξασφαλίζοντας ότι το “Invoice” και το “invoice” αντιμετωπίζονται ταυτόσημα. **Αυτή η ρύθμιση επηρεάζει τόσο την ευρετηρίαση όσο και το χρόνο ερωτήματος, διασφαλίζοντας συνεπή συμπεριφορά ανεξάρτητα από την αρχική περίπτωση του κειμένου.**

### Πώς εκτελείτε ερώτημα regex java;
Περάστε μια συμβολοσειρά κανονικής έκφρασης προεξοφλημένη με `regex:` στη μέθοδο `search`, π.χ., `searchEngine.search("regex:\\d{4}-\\d{2}-\\d{2}")`. Η μηχανή μεταγλωττίζει το μοτίβο και σαρώνει το ευρετήριο αποδοτικά. **Τα ερωτήματα regex μεταγλωττίζονται μία φορά ανά αναζήτηση, και η μηχανή βελτιστοποιεί τη σάρωση περιορίζοντάς την σε σχετικούς όρους του ευρετηρίου.**

### Πώς επισημαίνετε τα αποτελέσματα αναζήτησης java στο UI;
Αφού λάβετε τα ταιριάσματα, καλέστε `searchEngine.getSnippet(documentId, query, HighlightOptions)` για να λάβετε ένα κείμενο απόσπασμα με ετικέτες `<b>` γύρω από τους ταιριαστούς όρους. Απεικονίστε το απόσπασμα στο front‑end για να δώσετε στους χρήστες οπτικό πλαίσιο. **Το απόσπασμα σέβεται την αρχική διάταξη του εγγράφου και μπορεί να προσαρμοστεί ώστε να περιλαμβάνει περιβάλλον κείμενο για καλύτερη κατανόηση από τον χρήστη.**

## Πλήρης Αναζήτηση Κειμένου Java – Διαθέσιμα Μαθήματα

### [GroupDocs.Search Java&#58; Υλοποίηση Αναζήτησης Ομόφωνα για Βελτιωμένη Ανάκτηση Εγγράφων](./groupdocs-search-java-homophone-guide/)
Μάθετε πώς να υλοποιήσετε το GroupDocs.Search σε Java με δυνατότητες αναζήτησης ομόφωνων. Βελτιώστε αποτελεσματικά τη διαδικασία ανάκτησης εγγράφων.

### [Υλοποίηση Πλήρους Αναζήτησης Κειμένου σε Java με GroupDocs.Search&#58; Ένας Πλήρης Οδηγός](./implement-full-text-search-java-groupdocs-search/)
Μάθετε πώς να υλοποιήσετε πλήρη αναζήτηση κειμένου σε Java χρησιμοποιώντας το GroupDocs.Search. Αυτός ο πλήρης οδηγός καλύπτει εγκατάσταση, υλοποίηση και βελτιστοποίηση για αποδοτική ανάκτηση εγγράφων.

### [Υλοποίηση GroupDocs.Search Java για Αποδοτική Αναζήτηση Εγγράφων και Επισημάνσεις](./implement-groupdocs-search-java-document-search/)
Μάθετε πώς να υλοποιήσετε το GroupDocs.Search σε Java για εξαγωγή και επισημάνσεις αποτελεσμάτων αναζήτησης αποδοτικά, ενισχύοντας τη διαχείριση εγγράφων.

### [Κατακτήστε τις Boolean Αναζητήσεις σε Java&#58; Υλοποίηση GroupDocs.Search για Βελτιωμένη Ανάκτηση Εγγράφων](./implement-boolean-searches-groupdocs-java/)
Μάθετε πώς να υλοποιήσετε boolean αναζητήσεις AND, OR, NOT χρησιμοποιώντας το GroupDocs.Search για Java. Ενισχύστε τις δυνατότητες αναζήτησής σας και διαχειριστείτε έγγραφα αποδοτικά.

### [Κατακτήστε την Αναζήτηση χωρίς Διάκριση Πεζών‑Κεφαλαίων σε Java Χρησιμοποιώντας GroupDocs.Search&#58; Ένας Πλήρης Οδηγός](./master-case-insensitive-search-java-groupdocs-search/)
Μάθετε πώς να εκτελείτε αποδοτικές, case‑insensitive αναζητήσεις σε Java με το GroupDocs.Search. Κατακτήστε την αντικατάσταση χαρακτήρων κατά την ευρετηρίαση για απρόσκοπτη λειτουργία αναζήτησης.

### [Κατακτήστε τις Αναζητήσεις με Διάκριση Πεζών‑Κεφαλαίων σε Java Χρησιμοποιώντας GroupDocs&#58; Ένας Πλήρης Οδηγός](./master-case-sensitive-searches-java-groupdocs/)
Μάθετε πώς να υλοποιήσετε ακριβείς case‑sensitive αναζητήσεις κειμένου και αντικειμένων σε Java με το GroupDocs.Search. Ενισχύστε τη λειτουργικότητα αναζήτησης της εφαρμογής σας για μεγαλύτερη ακρίβεια δεδομένων.

### [Κατακτήστε την Αναζήτηση Εγγράφων με GroupDocs.Search Java&#58; Ένας Πλήρης Οδηγός για Αποδοτική Ευρετηρίαση και Αναζήτηση Αρχείων](./master-document-search-groupdocs-java/)
Μάθετε πώς να χρησιμοποιήσετε το GroupDocs.Search για Java ώστε να δημιουργήσετε ισχυρές εφαρμογές αναζήτησης. Κατακτήστε τις αναζητήσεις κειμένου και αντικειμένων στα Java projects σας.

### [Κατακτήστε την Αναζήτηση Εγγράφων με GroupDocs.Search για Java&#58; Ένας Πλήρης Οδηγός](./mastering-document-search-groupdocs-java/)
Μάθετε πώς να ρυθμίσετε και να αναπτύξετε αποδοτικά δίκτυα αναζήτησης εγγράφων χρησιμοποιώντας το GroupDocs.Search για Java, βελτιστοποιώντας τις διαδικασίες ανάκτησης εγγράφων.

### [Κατακτήστε την Πλήρη Αναζήτηση Κειμένου σε Java με GroupDocs&#58; Υλοποίηση Προσαρμοσμένων Εξαγωγέων Κειμένου](./java-full-text-search-groupdocs-custom-extractor/)
Μάθετε πώς να υλοποιήσετε πλήρη αναζήτηση κειμένου σε Java χρησιμοποιώντας το GroupDocs.Search. Δημιουργήστε προσαρμοσμένους εξαγωγείς κειμένου, ευρετηριάστε έγγραφα αποδοτικά και βελτιστοποιήστε τις δυνατότητες διαχείρισης εγγράφων της εφαρμογής σας.

### [Κατακτήστε την Fuzzy Αναζήτηση σε Java Χρησιμοποιώντας GroupDocs.Search&#58; Ένας Πλήρης Οδηγός](./master-fuzzy-search-java-groupdocs/)
Μάθετε πώς να υλοποιήσετε fuzzy αναζήτηση με το GroupDocs.Search για Java, ενισχύοντας τις δυνατότητες αναζήτησης της εφαρμογής σας με προσαρμογή σε ορθογραφικές παραλλαγές.

### [Κατακτήστε το GroupDocs.Search Java&#58; Προηγμένες Τεχνικές Αναζήτησης Κειμένου](./groupdocs-search-java-advanced-text-search-guide/)
Μάθετε πώς να υλοποιήσετε προχωρημένες αναζητήσεις κειμένου με το GroupDocs.Search για Java. Δημιουργήστε ευρετήρια, διαμορφώστε επιλογές αναζήτησης και βελτιστοποιήστε την απόδοση στις εφαρμογές σας.

### [Κατακτήστε το GroupDocs.Search Java&#58; Αποδοτική Αναζήτηση Εγγράφων και Διαχείριση Ευρετηρίων](./groupdocs-search-java-efficient-document-search/)
Μάθετε πώς να ρυθμίσετε, να διαχειριστείτε και να βελτιστοποιήσετε την αναζήτηση εγγράφων χρησιμοποιώντας το GroupDocs.Search για Java. Ενισχύστε τις δυνατότητες αναζήτησής σας με προσαρμοσμένη διαχείριση μορφών λέξεων.

### [Κατακτήστε το GroupDocs.Search Java&#58; Αποδοτική Ευρετηρίαση & Αναζήτηση για Μεγάλες Συλλογές Δεδομένων](./master-groupdocs-search-java-indexing-search/)
Μάθετε πώς να χρησιμοποιήσετε το GroupDocs.Search σε Java για αποδοτική ευρετηρίαση εγγράφων και αναζήτηση. Κατακτήστε τη δημιουργία αποθετηρίων ευρετηρίου, την εγγραφή σε συμβάντα και την εκτέλεση ισχυρών ερωτημάτων.

### [Κατακτώντας την Αναζήτηση Εγγράφων σε Java&#58; Συγχρονική και Ασύγχρονη Ευρετηρίαση με GroupDocs.Search](./master-groupdocs-search-java-document-indexing/)
Βελτιώστε τις Java εφαρμογές σας κατακτώντας την αναζήτηση εγγράφων με συγχρονική και ασύγχρονη ευρετηρίαση χρησιμοποιώντας το GroupDocs.Search για Java. Μάθετε ρυθμίσεις, υλοποίηση και τεχνικές βελτιστοποίησης.

### [Κατακτώντας το GroupDocs.Search Java&#58; Οδηγός Fuzzy Αναζήτησης & Ευρετηρίασης Εγγράφων](./groupdocs-search-java-fuzzy-document-indexing/)
Μάθετε πώς να διαχειρίζεστε και να αναζητάτε έγγραφα αποδοτικά χρησιμοποιώντας το GroupDocs.Search για Java με δυνατότητες fuzzy αναζήτησης. Ανακαλύψτε βέλτιστες πρακτικές ευρετηρίασης εγγράφων.

### [Κατακτώντας τις Phrase Αναζητήσεις με Wildcards στο GroupDocs.Search για Java&#58; Ένας Πλήρης Οδηγός](./groupdocs-search-java-phrase-wildcard/)
Μάθετε πώς να υλοποιήσετε phrase αναζητήσεις χρησιμοποιώντας μοτίβα wildcard στο GroupDocs.Search για Java. Ενισχύστε τις δυνατότητες αναζήτησής σας με αυτό το λεπτομερές μάθημα.

### [Κατακτώντας τις Regex Αναζητήσεις σε Java&#58; Ένας Πλήρης Οδηγός για το GroupDocs.Search για Ανάλυση Κειμένων Εγγράφων](./groupdocs-search-java-regex-tutorial/)
Μάθετε πώς να εκτελείτε αποδοτικά regex αναζητήσεις χρησιμοποιώντας το GroupDocs.Search για Java. Αυτός ο οδηγός καλύπτει τη ρύθμιση του περιβάλλοντος, τη δημιουργία ευρετηρίων και την εκτέλεση ερωτημάτων κειμένου και αντικειμένων.

### [Κατακτώντας την Αναζήτηση Αρχείων Κειμένου σε Java με GroupDocs.Search&#58; Ένας Πλήρης Οδηγός](./master-text-searching-java-groupdocs/)
Μάθετε πώς να αναζητάτε αποδοτικά αρχεία κειμένου σε Java χρησιμοποιώντας το GroupDocs.Search. Αυτός ο οδηγός καλύπτει ευρετηρίαση, ρύθμιση κωδικοποιήσεων αρχείων και εκτέλεση ερωτημάτων για βέλτιστη απόδοση.

### [Κατακτώντας τις Wildcard Αναζητήσεις σε Java με GroupDocs.Search&#58; Ένας Πλήρης Οδηγός](./wildcard-searches-groupdocs-java-guide/)
Μάθετε πώς να υλοποιήσετε ισχυρές wildcard αναζητήσεις σε Java χρησιμοποιώντας το GroupDocs.Search. Ενισχύστε τις δυνατότητες αναζήτησης της εφαρμογής σας με αυτό το λεπτομερές μάθημα.

## Γιατί να Χρησιμοποιήσετε την Πλήρης Αναζήτηση Κειμένου Java με το GroupDocs.Search;

- **Κλιμακούμενη απόδοση** – Διαχειρίζεται εκατομμύρια έγγραφα με χαμηλή λανθάνουσα καθυστέρηση· απόκριση ερωτήματος υποδευτερόλεπτο για ευρετήρια 100 M‑εγγραφών.  
- **Πλούσια γλώσσα ερωτημάτων** – Υποστηρίζει boolean, fuzzy, phrase, wildcard και regex ερωτήματα έτοιμα προς χρήση.  
- **Εύκολη ενσωμάτωση** – Η απλή Java API σας επιτρέπει να προσθέσετε ισχυρή αναζήτηση σε οποιαδήποτε εφαρμογή σε λίγα λεπτά.  
- **Προσαρμόσιμη ευρετηρίαση** – Ρυθμίστε λεπτομερώς την τοκενικοποίηση, τα stop‑words και τη διαχείριση συνωνύμων ώστε να ταιριάζει στον τομέα σας.  

## Συνηθισμένες Περιπτώσεις Χρήσης για Πλήρης Αναζήτηση Κειμένου Java

1. **Εταιρικές πύλες εγγράφων** – Εντοπίστε γρήγορα πολιτικές, συμβάσεις ή εγχειρίδια σε χιλιάδες αρχεία.  
2. **Πλατφόρμες e‑learning** – Επιτρέψτε στους φοιτητές να αναζητούν υλικό μαθημάτων, PDF και παρουσιάσεις.  
3. **Εργαλεία νομικής ανακάλυψης** – Εκτελέστε case‑insensitive και regex αναζητήσεις για την ανάδειξη σχετικών αποδείξεων.  
4. **Γνωστικές βάσεις υποστήριξης πελατών** – Επισημάνετε τμήματα κειμένου για βελτίωση της αυτοεξυπηρέτησης.  

## Πρόσθετοι Πόροι

- [GroupDocs.Search for Java Documentation](https://docs.groupdocs.com/search/java/)
- [GroupDocs.Search for Java API Reference](https://reference.groupdocs.com/search/java/)
- [Download GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- [GroupDocs.Search Forum](https://forum.groupdocs.com/c/search)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

## Συχνές Ερωτήσεις

**Ε: Υποστηρίζει το GroupDocs.Search ευρετηρίαση κρυπτογραφημένων PDF;**  
Α: Ναι – παρέχετε τον κωδικό πρόσβασης μέσω `SearchOptions.setPassword("yourPassword")` πριν προσθέσετε το έγγραφο.

**Ε: Μπορώ να ενημερώσω ένα υπάρχον ευρετήριο χωρίς να το ξαναχτίσω από την αρχή;**  
Α: Απόλυτα – χρησιμοποιήστε `searchEngine.updateDocument(filePath)` για να τροποποιήσετε ή να αντικαταστήσετε ένα μόνο έγγραφο διατηρώντας το υπόλοιπο ευρετήριο.

**Ε: Ποιο είναι το μέγιστο μέγεθος αρχείου που μπορεί να ευρετηριαστεί;**  
Α: Η μηχανή μπορεί να χειριστεί αρχεία έως **2 GB** ανά έγγραφο· μεγαλύτερα αρχεία επεξεργάζονται σε λειτουργία streaming για αποφυγή πίεσης μνήμης.

**Ε: Υπάρχει ενσωματωμένη υποστήριξη για επέκταση συνωνύμων;**  
Α: Ναι – διαμορφώστε ένα `SynonymMap` στο `SearchOptions` και η μηχανή θα επεκτείνει αυτόματα τα ερωτήματα με τις καθορισμένες συνώνυμες λέξεις.

**Ε: Πώς παρακολουθώ την πρόοδο ευρετηρίασης σε μια μεγάλη παρτίδα εργασιών;**  
Α: Εγγραφείτε στο γεγονός `IndexingProgressListener`; αναφέρει το ποσοστό ολοκλήρωσης και τον χρόνο που πέρασε για κάθε παρτίδα.

---

**Τελευταία Ενημέρωση:** 2026-05-22  
**Δοκιμασμένο Με:** GroupDocs.Search for Java 23.11  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Πώς να Διαμορφώσετε το GroupDocs.Search - Εκπαιδευτικά Μαθήματα Έναρξης για Java](/search/java/getting-started/)
- [Δημιουργία Ευρετηρίου Αναζήτησης Java – Μαθήματα GroupDocs.Search](/search/java/indexing/)
- [Υλοποίηση Πλήρης Αναζήτησης Κειμένου σε Java με GroupDocs.Search: Ένας Πλήρης Οδηγός](/search/java/searching/implement-full-text-search-java-groupdocs-search/)