---
date: '2026-07-31'
description: Μάθετε πώς να υλοποιήσετε case insensitive search java προσθέτοντας έγγραφα
  σε ένα ευρετήριο με το GroupDocs.Search, χρησιμοποιώντας αντικατάσταση χαρακτήρων
  για την κανονικοποίηση του κειμένου κατά την ευρετηρίαση.
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: Case insensitive search java σας επιτρέπει να προσθέτετε έγγραφα σε
  ένα ευρετήριο και να τα ερωτάτε χωρίς να ανησυχείτε για το γράμμα-περίπτωση. Αυτός
  ο οδηγός δείχνει πώς το GroupDocs.Search κανονικοποιεί το κείμενο κατά την ευρετηρίαση
  για γρήγορα, αξιόπιστα αποτελέσματα.
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Case Insensitive Search Java – Ευρετηρίαση Εγγράφων με GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: Προσθήκη εγγράφων στο ευρετήριο για Case‑Insensitive Search σε Java
type: docs
url: /el/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# Προσθήκη Εγγράφων στο Ευρετήριο για Αναζήτηση χωρίς Διάκριση Πεζών‑Κεφαλαίων σε Java

Όταν χρειάζεστε **case insensitive search java** που βρίσκει αξιόπιστα πληροφορίες ανεξάρτητα από το πώς τις πληκτρολογούν οι χρήστες, το κλειδί είναι η προσθήκη εγγράφων σε ένα ευρετήριο ενώ κανονικοποιείται το κείμενο. Σε αυτό το σεμινάριο θα σας καθοδηγήσουμε στη διαμόρφωση του GroupDocs.Search για Java ώστε κάθε έγγραφο που ευρετηριάζετε να μετατρέπεται αυτόματα σε πεζά (ή με άλλη μετατροπή) κατά τη διαδικασία ευρετηρίασης, εξασφαλίζοντας αποτελέσματα χωρίς διάκριση πεζών‑κεφαλαίων χωρίς πρόσθετη λογική κατά το ερώτημα.

## Γρήγορες Απαντήσεις
- **What does “add documents to index” mean?** Σημαίνει τη φόρτωση των αρχικών αρχείων σε μια δομή δεδομένων αναζήτησης ώστε να μπορούν να ερωτηθούν αργότερα.  
- **Why use character replacement?** Κανονικοποιεί κάθε χαρακτήρα — συνήθως σε πεζά — ώστε οι αναζητήσεις να αγνοούν αυτόματα τις διαφορές πεζών‑κεφαλαίων.  
- **Do I need a license?** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται πλήρης άδεια για παραγωγικές εγκαταστάσεις.  
- **Which Java version is required?** Η έκδοση Java 8 ή νεότερη· η βιβλιοθήκη στοχεύει σε Java 11+ για βέλτιστη απόδοση.  
- **Can I switch to case‑sensitive search when needed?** Ναι—οι επιλογές αναζήτησης σας επιτρέπουν να εναλλάσσετε τη διάκριση πεζών‑κεφαλαίων ανά ερώτημα.

## Τι σημαίνει “add documents to index” στο GroupDocs.Search;
Φορτώστε τα αρχεία προέλευσης (PDF, DOCX, TXT κ.λπ.) σε ένα αναζητήσιμο ευρετήριο ώστε η μηχανή να μπορεί να τα ανακτήσει γρήγορα. Η προσθήκη εγγράφων σε ένα ευρετήριο αναλύει κάθε αρχείο, εξάγει απλό κείμενο και το αποθηκεύει σε μια βελτιστοποιημένη δομή δεδομένων που επιτρέπει γρήγορες αναζητήσεις.

## Γιατί να ενεργοποιήσετε την αντικατάσταση χαρακτήρων κατά την ευρετηρίαση;
Η αντικατάσταση χαρακτήρων μετατρέπει κάθε χαρακτήρα σε ένα προκαθορισμένο ισοδύναμο — συνήθως σε πεζά — κατά τη δημιουργία του ευρετηρίου. Αυτό εξασφαλίζει ότι οι διαφορές στην κεφαλαιοποίηση, τα διακριτικά ή τα σύμβολα ειδικά για την περιοχή δεν επηρεάζουν τα αποτελέσματα αναζήτησης. Κανονικοποιώντας το κείμενο κατά τη φάση ευρετηρίασης, η μηχανή μπορεί να ταιριάζει τα ερωτήματα με ένα συνεπές σύνολο διακριτικών, παρέχοντας γρήγορη, αξιόπιστη συμπεριφορά χωρίς διάκριση πεζών‑κεφαλαίων χωρίς επιπλέον επεξεργασία σε κάθε αναζήτηση.

## Προαπαιτούμενα
- **GroupDocs.Search for Java** έκδοση 25.4 ή νεότερη (η βιβλιοθήκη υποστηρίζει πάνω από 30 μορφές αρχείων και μπορεί να ευρετηριάσει έγγραφα πολλαπλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη).  
- **Java Development Kit (JDK)** 8 ή νεότερο εγκατεστημένο.  
- Βασική εξοικείωση με **Maven** (ή δυνατότητα προσθήκης JAR χειροκίνητα).  

## Ρύθμιση του GroupDocs.Search για Java

### Ρύθμιση Maven
Προσθέστε το αποθετήριο GroupDocs και την εξάρτηση στο `pom.xml` σας:

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

### Άμεση Λήψη
Αν προτιμάτε να μην χρησιμοποιήσετε Maven, κατεβάστε το τελευταίο JAR από την επίσημη ιστοσελίδα: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση Άδειας
- **Free Trial** – κατεβάστε μια δοκιμαστική άδεια για να ξεκινήσετε πειραματισμό.  
- **Temporary License** – ζητήστε μια εκτεταμένη δοκιμαστική άδεια από το portal του GroupDocs.  
- **Full License** – αγοράστε μια παραγωγική άδεια όταν είστε έτοιμοι να ξεκινήσετε.

### Βασική Αρχικοποίηση (Δημιουργία του ευρετηρίου)
Το παρακάτω απόσπασμα δημιουργεί έναν φάκελο ευρετηρίου και ενεργοποιεί τις αντικαταστάσεις χαρακτήρων:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Οδηγός Υλοποίησης

### Ενεργοποίηση Αντικατάστασης Χαρακτήρων στις Ρυθμίσεις Ευρετηρίου
Η ενεργοποίηση αυτής της λειτουργίας ενημερώνει τη μηχανή να αντικαθιστά χαρακτήρες κατά την ευρετηρίαση, που αποτελεί το βασικό βήμα για τη συμπεριφορά χωρίς διάκριση πεζών‑κεφαλαίων.

#### Βήμα 1: Διαμόρφωση του `IndexSettings`
`IndexSettings` είναι το αντικείμενο διαμόρφωσης που ελέγχει πώς το ευρετήριο αποθηκεύει και επεξεργάζεται το κείμενο. Ορίζοντας το `useCharacterReplacements` σε **true**, ενεργοποιείτε την αυτόματη μετατροπή σε πεζά (ή οποιονδήποτε προσαρμοσμένο χάρτη παρέχετε).

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### Διαμόρφωση Αντικατάστασης Χαρακτήρων
Αντιστοιχίστε κάθε χαρακτήρα με το αντίστοιχο πεζό (ή οποιονδήποτε προσαρμοσμένο χάρτη χρειάζεστε).

#### Βήμα 2: Ορισμός και Προσθήκη Ζευγών Αντικατάστασης
Το λεξικό αντικατάστασης περιέχει ζεύγη όπως `'A' → 'a'`, `'É' → 'e'`, κ.λπ. Η προσθήκη αυτών των ζευγών πριν την ευρετηρίαση εξασφαλίζει ότι κάθε διακριτικό είναι κανονικοποιημένο.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Ευρετηρίαση Εγγράφων
Τώρα που το ευρετήριο είναι έτοιμο, μπορείτε να **add documents to index** από οποιονδήποτε φάκελο.

#### Βήμα 3: Προσθήκη Εγγράφων για Ευρετηρίαση
Το GroupDocs.Search σαρώει τον προορισμό, εξάγει κείμενο από κάθε υποστηριζόμενο τύπο αρχείου, εφαρμόζει τον χάρτη αντικατάστασης και γράφει τα διακριτικά στην αποθήκη του ευρετηρίου.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Εκτέλεση Αναζήτησης με Διάκριση Πεζών‑Κεφαλαίων (Προαιρετικό)

#### Βήμα 4: Εκτέλεση Αναζητήσεων με Διάκριση Πεζών‑Κεφαλαίων
`SearchOptions` διαμορφώνει τη συμπεριφορά του ερωτήματος, όπως η εναλλαγή της διάκρισης πεζών‑κεφαλαίων, επιτρέποντας λεπτομερή έλεγχο του τρόπου εκτέλεσης των αναζητήσεων.  
`SearchOptions.setUseCaseSensitiveSearch(true)` αναγκάζει τη μηχανή να αντιμετωπίζει τους κεφαλαίους και πεζούς χαρακτήρες ως διαφορετικούς κατά ένα συγκεκριμένο ερώτημα, παρακάμπτοντας τη προεπιλεγμένη συμπεριφορά χωρίς διάκριση πεζών‑κεφαλαίων.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## Πρακτικές Εφαρμογές
1. **Marketing Campaigns** – Κανονικοποιήστε τα ονόματα προϊόντων ώστε οι ομάδες πωλήσεων να μπορούν να εντοπίζουν τα περιουσιακά στοιχεία χωρίς να ανησυχούν για την κεφαλαιοποίηση.  
2. **Customer Support** – Ενισχύστε τα πλαίσια αναζήτησης του help‑desk που επιστρέφουν το σωστό άρθρο είτε ο χρήστης πληκτρολογήσει “login” είτε “Login”.  
3. **E‑commerce Catalogs** – Διασφαλίστε ότι οι αγοραστές βρίσκουν τα προϊόντα ανεξάρτητα από το πώς πληκτρολογούν τους τίτλους, βελτιώνοντας τα ποσοστά μετατροπής.

## Σκέψεις Απόδοσης
- **Organize Source Files** – Μια τακτοποιημένη ιεραρχία φακέλων μειώνει το χρόνο σάρωσης κατά το βήμα **add documents to index**.  
- **Monitor Memory** – Η ευρετηρίαση μεγάλων σωμάτων κειμένου μπορεί να καταναλώσει σημαντική μνήμη RAM· η επεξεργασία αρχείων σε παρτίδες των 500 – 1 000 στοιχείων διατηρεί τη χρήση του σωρού υπό έλεγχο.  
- **Asynchronous Indexing** – Όταν υποστηρίζεται, εκτελέστε την ευρετηρίαση σε νήμα παρασκηνίου για να διατηρήσετε το UI ανταποκρινόμενο και να αποφύγετε το μπλοκάρισμα των λειτουργιών του χρήστη.

## Συχνά Προβλήματα & Επίλυση
| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Δεν επιστρέφονται αποτελέσματα για γνωστό όρο | Οι αντικαταστάσεις χαρακτήρων δεν είναι ενεργοποιημένες | Επαληθεύστε ότι το `settings.setUseCharacterReplacements(true)` είναι ενεργό και ότι ο χάρτης αντικατάστασης περιέχει τους απαιτούμενους χαρακτήρες. |
| Σφάλμα έλλειψης μνήμης (Out‑of‑memory) κατά την ευρετηρίαση | Ευρετηρίαση πάρα πολλών μεγάλων αρχείων ταυτόχρονα | Ευρετηρίαση σε μικρότερες παρτίδες ή αύξηση του heap της JVM (`-Xmx4g`). |
| Η αναζήτηση επιστρέφει αποτελέσματα με διάκριση πεζών‑κεφαλαίων απροσδόκητα | Το `SearchOptions.setUseCaseSensitiveSearch(true)` είχε οριστεί | Αφαιρέστε ή ορίστε σε `false` για την προεπιλεγμένη συμπεριφορά χωρίς διάκριση πεζών‑κεφαλαίων. |
| Ο χρόνος φόρτωσης του ευρετηρίου υπερβαίνει τις προσδοκίες | Αναποτελεσματική διάταξη φακέλων ή μη χρήση SSD | Αναδιοργανώστε τα αρχεία, αφαιρέστε αχρησιμοποίητα έγγραφα και αποθηκεύστε το ευρετήριο σε γρήγορο SSD. |
| Οι ειδικοί χαρακτήρες αγνοούνται | Ο χάρτης αντικατάστασης δεν περιέχει εγγραφές Unicode | Προσθέστε αντιστοιχίες για χαρακτήρες όπως “é”, “ß”, “ø” στα επιθυμητά ισοδύναμα. |

## Συχνές Ερωτήσεις

**Q: Πώς να διαχειριστώ ειδικούς χαρακτήρες (π.χ., “é”, “ß”) κατά την ευρετηρίαση;**  
A: Συμπεριλάβετε αυτούς τους χαρακτήρες στο χάρτη αντικατάστασης, αντιστοιχίζοντάς τους στα ισοδύναμα ASCII ή διατηρώντας τους αμετάβλητους ανάλογα με τις απαιτήσεις αναζήτησης.

**Q: Μπορώ να περιορίσω την αντικατάσταση χαρακτήρων σε συγκεκριμένη γλώσσα;**  
A: Ναι. Δημιουργήστε έναν προσαρμοσμένο πίνακα αντικατάστασης που περιέχει μόνο τους χαρακτήρες της επιλεγμένης γλώσσας πριν τον προσθέσετε στο λεξικό.

**Q: Τι πρέπει να κάνω αν η φόρτωση του ευρετηρίου διαρκεί πολύ;**  
A: Βελτιστοποιήστε τη δομή των φακέλων, αφαιρέστε περιττά αρχεία και αποθηκεύστε το ευρετήριο σε γρήγορο SSD. Η επαυξητική (incremental) ευρετηρίαση μειώνει επίσης το φορτίο φόρτωσης.

**Q: Είναι δυνατόν να αναιρέσω τις αντικαταστάσεις χαρακτήρων μετά την ευρετηρίαση;**  
A: Όχι. Οι αντικαταστάσεις ενσωματώνονται στα δεδομένα του ευρετηρίου· πρέπει να ξαναδημιουργήσετε το ευρετήριο με νέες ρυθμίσεις για να τις αλλάξετε.

**Q: Πού μπορώ να βρω πιο αναλυτική τεκμηρίωση API;**  
A: Η επίσημη τεκμηρίωση και η αναφορά API παρέχουν λεπτομερείς πληροφορίες (δείτε τους Πόρους παρακάτω).

## Πόροι
- [Τεκμηρίωση](https://docs.groupdocs.com/search/java/)
- [Αναφορά API](https://reference.groupdocs.com/search/java)
- [Λήψη GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [Αποθετήριο GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Δωρεάν Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/search/10)
- [Πληροφορίες Προσωρινής Άδειας](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία Ενημέρωση:** 2026-07-31  
**Δοκιμάστηκε Με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs  

## Σχετικά Μαθήματα

- [Αντικατάσταση Χαρακτήρων στο GroupDocs.Search Java: Ένας Πλήρης Οδηγός για τη Βελτίωση της Αναζήτησης Κειμένου και της Ευρετηρίασης](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [Προσθήκη εγγράφων στο ευρετήριο: αναζήτηση Java με διάκριση πεζών‑κεφαλαίων με το GroupDocs](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [Πώς να Προσθέσετε Έγγραφα στο Ευρετήριο με το GroupDocs.Search για Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)