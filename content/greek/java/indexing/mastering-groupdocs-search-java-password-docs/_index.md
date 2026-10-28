---
date: '2026-10-28'
description: Μάθετε πώς να αναζητήσετε πολλαπλούς τύπους αρχείων και να δημιουργήσετε
  ένα ευρετήριο αναζήτησης για έγγραφα με προστασία κωδικού πρόσβασης σε Java χρησιμοποιώντας
  το GroupDocs.Search. Step‑by‑step guide with code, tips, and performance tricks.
keywords:
- search multiple file types
- build searchable index
- password protected document indexing java
- groupdocs.search java api
lastmod: '2026-10-28'
og_description: Μάθετε πώς να αναζητήσετε πολλαπλούς τύπους αρχείων και να δημιουργήσετε
  ένα ευρετήριο αναζήτησης για έγγραφα με προστασία κωδικού πρόσβασης σε Java χρησιμοποιώντας
  το GroupDocs.Search. Step‑by‑step guide with code, tips, and performance tricks.
og_image_alt: Guide showing Java code to search multiple file types and index password‑protected
  documents with GroupDocs.Search
og_title: Πώς να αναζητήσετε πολλαπλούς τύπους αρχείων και να δημιουργήσετε ευρετήριο
  εγγράφων σε Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-28'
  description: Learn how to search multiple file types and build a searchable index
    for password‑protected documents in Java using GroupDocs.Search. Step‑by‑step
    guide with code, tips, and performance tricks.
  headline: How to search multiple file types and index docs in Java
  type: TechArticle
- questions:
  - answer: GroupDocs.Search supports 120+ formats including PDF, DOCX, XLSX, PPTX,
      and common image types. Install format plugins if required.
    question: How do I handle different file formats?
  - answer: The document is skipped and a warning is logged; verify your password
      dictionary or event handler.
    question: What happens if a password is wrong?
  - answer: Yes, but they must be downloaded to a local temporary folder first because
      the engine works with file‑system paths.
    question: Can I index files stored in the cloud?
  - answer: Adjust scoring with `IndexOptions`, add synonyms, and use advanced query
      syntax such as `field:term~` for fuzzy matching. `IndexOptions` is a configuration
      object that controls scoring and indexing behavior.
    question: How can I improve search relevance?
  - answer: Review the log output; common causes are missing passwords, corrupted
      files, or unsupported formats.
    question: What should I do if indexing fails for some files?
  type: FAQPage
tags:
- search multiple file types
- GroupDocs.Search
- Java indexing
- password‑protected docs
- document search
title: Πώς να αναζητήσετε πολλαπλούς τύπους αρχείων και να δημιουργήσετε ευρετήριο
  εγγράφων σε Java
type: docs
url: /el/java/indexing/mastering-groupdocs-search-java-password-docs/
weight: 1
---

# Πώς να αναζητήσετε πολλαπλούς τύπους αρχείων και να δημιουργήσετε ευρετήριο εγγράφων σε Java

Σε σύγχρονες επιχειρήσεις συχνά χρειάζεται να **αναζητήσετε πολλαπλούς τύπους αρχείων** ενώ τα εμπιστευτικά αρχεία παραμένουν κλειδωμένα με κωδικούς πρόσβασης. Αυτό το σεμινάριο δείχνει πώς να δημιουργήσετε ένα ευρετήριο αναζήτησης για έγγραφα με κωδικό πρόσβασης σε Java χρησιμοποιώντας το GroupDocs.Search. Θα δείτε πώς να διαμορφώσετε ένα λεξικό κωδικών, να διαχειριστείτε συμβάντα που απαιτούν κωδικό πρόσβασης και να βελτιστοποιήσετε την απόδοση για μεγάλες παρτίδες—όλα χωρίς να γράψετε προσαρμοσμένο κώδικα αποκρυπτογράφησης.

## Σύντομες απαντήσεις
- **Τι καλύπτει αυτό το σεμινάριο;** Δημιουργία ευρετηρίου εγγράφων με κωδικό πρόσβασης χρησιμοποιώντας λεξικό κωδικών και ακροατή συμβάντων.  
- **Ποια βιβλιοθήκη απαιτείται;** GroupDocs.Search για Java (τελευταία έκδοση).  
- **Χρειάζομαι άδεια;** Διατίθεται προσωρινή δωρεάν δοκιμαστική άδεια για αξιολόγηση.  
- **Μπορώ να δημιουργήσω ευρετήριο άλλων τύπων αρχείων;** Ναι, το GroupDocs.Search υποστηρίζει πάνω από 120 μορφές, συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX και εικόνων.  
- **Ποια έκδοση Java απαιτείται;** JDK 8 ή νεότερη.  

## Τι είναι το “create document index java”;

`create document index java` αναφέρεται στη διαδικασία δημιουργίας μιας δομής δεδομένων αναζήτησης που αντιστοιχεί όρους στις θέσεις των αρχείων που διαχειρίζεται η Java. Με το GroupDocs.Search, η μηχανή εξάγει αυτόματα κείμενο από υποστηριζόμενες μορφές—συμπεριλαμβανομένων κρυπτογραφημένων PDF, εγγράφων Office και εικόνων—ώστε να εκτελείτε αναζητήσεις πλήρους κειμένου χωρίς να γράψετε κώδικα αποκρυπτογράφησης. Αυτή η προσέγγιση απλοποιεί την υλοποίηση της αναζήτησης διατηρώντας την ασφάλεια των εγγράφων.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για αρχεία με κωδικό πρόσβασης;

Το GroupDocs.Search παρέχει μηδενική παρέμβαση στην αποκρυπτογράφηση εφαρμόζοντας κωδικούς από λεξικό ή από διαχειριστή συμβάντων, επιτρέποντάς σας να δημιουργήσετε ευρετήριο κρυπτογραφημένων αρχείων σε μία μόνο διαδικασία. Επεξεργάζεται έως και 2 εκατομμύρια έγγραφα ανά ώρα σε τυπικό διακομιστή 8‑πυρήνων, υποστηρίζει πάνω από 120 τύπους αρχείων και προσφέρει πλούσια γλώσσα ερωτημάτων με Boolean, wildcard και fuzzy τελεστές—όλα απαραίτητα για τη δημιουργία ενός ευρετηρίου που καλύπτει ποικίλο περιεχόμενο.

## Προαπαιτούμενα
- Java Development Kit (JDK) 8+ εγκατεστημένο και προστιθέμενο στο `PATH`.
- Ένα IDE όπως IntelliJ IDEA ή Eclipse.
- Maven για διαχείριση εξαρτήσεων.
- GroupDocs.Search για Java – προσθέστε τη βιβλιοθήκη μέσω Maven (δείτε την ενότητα ρύθμισης).

## Ρύθμιση του GroupDocs.Search για java

### Χρήση Maven
Προσθέστε το αποθετήριο και την εξάρτηση στο αρχείο `pom.xml`:

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
Εναλλακτικά, μπορείτε να κατεβάσετε την τελευταία έκδοση απευθείας από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

Για να ξεκινήσετε με δοκιμαστική άδεια, επισκεφθείτε τη [σελίδα προσωρινής άδειας του GroupDocs](https://purchase.groupdocs.com/temporary-license/) και ακολουθήστε τις οδηγίες για να αποκτήσετε τη δωρεάν δοκιμή.

## Πώς να δημιουργήσετε ευρετήριο εγγράφων με λεξικό κωδικών πρόσβασης

Μπορείτε **να δημιουργήσετε ένα ευρετήριο αναζήτησης** παρέχοντας ένα λεξικό που αντιστοιχίζει διαδρομές αρχείων σε κωδικούς πρόσβασης. Η μηχανή θα ανακτήσει αυτόματα τον σωστό κωδικό κατά τη δημιουργία του ευρετηρίου.

### Επισκόπηση
Αποθηκεύστε τους κωδικούς πρόσβασης των εγγράφων σε έναν απλό χάρτη κλειδί‑τιμής ώστε η μηχανή ευρετηρίου να μπορεί να ξεκλειδώνει τα αρχεία κατά απαίτηση.

### Βήμα 1: ορίστε το ευρετήριο και το φάκελο εγγράφων
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordDictionary";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Βήμα 2: δημιουργήστε ένα ευρετήριο
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Βήμα 3: προσθέστε κωδικούς πρόσβασης εγγράφων
```java
// Add passwords for specific files using their absolute paths
String path1 = new File(documentsFolder + "/English.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path1, "123456");

String path2 = new File(documentsFolder + "/SampleDocument.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path2, "123456");
```

### Βήμα 4: δημιουργήστε ευρετήριο εγγράφων
```java
// Automatically retrieve passwords from the dictionary during indexing
index.add(documentsFolder);
```

### Βήμα 5: αναζητήστε στο ευρετήριο
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

**Συμβουλή:** Για παραγωγικά σενάρια, φορτώστε τους κωδικούς από ασφαλές vault (π.χ., Azure Key Vault ή AWS Secrets Manager) αντί για ενσωμάτωση στον κώδικα.

#### Επίλυση προβλημάτων
- Βεβαιωθείτε ότι κάθε κωδικός ταιριάζει με τον πραγματικό κωδικό προστασίας του αρχείου.  
- Ελέγξτε τις διαδρομές αρχείων· λανθασμένη διαδρομή προκαλεί `FileNotFoundException`.

## Πώς να δημιουργήσετε ευρετήριο εγγράφων με ακροατή συμβάντος για απαίτηση κωδικού πρόσβασης;

Μπορείτε να παρέχετε κωδικούς μόνο όταν η μηχανή ενεργοποιεί ένα συμβάν που απαιτεί κωδικό, διατηρώντας τα διαπιστευτήρια εκτός μνήμης και επιτρέποντας δυναμική ανάλυση κωδικού.

Όταν η μηχανή ευρετηρίου συναντά ένα κρυπτογραφημένο αρχείο, ενεργοποιεί μια κλήση επιστροφής όπου μπορείτε να αναζητήσετε τον κωδικό από ασφαλή αποθήκη ή να τον υπολογίσετε επί τόπου. Αυτή η μέθοδος μειώνει την επιφάνεια επίθεσης σε σύγκριση με την αποθήκευση όλων των κωδικών σε λεξικό.

### Επισκόπηση
Παρέχετε κωδικούς σε πραγματικό χρόνο μέσω ενός συμβάντος, διατηρώντας το αποθετήριο διαπιστευτηρίων απομονωμένο.

### Βήμα 1: ορίστε το ευρετήριο και το φάκελο εγγράφων
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordEvent";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Βήμα 2: δημιουργήστε ένα ευρετήριο
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Βήμα 3: εγγραφείτε στο συμβάν που απαιτεί κωδικό
```java
index.getEvents().PasswordRequired.add(new EventHandler<PasswordRequiredEventArgs>() {
    @Override
    public void invoke(Object sender, PasswordRequiredEventArgs args) {
        // Provide password for DOCX files when needed
        if (args.getDocumentFullPath().endsWith(".docx")) {
            args.setPassword("123456");
        }
    }
});
```

### Βήμα 4: δημιουργήστε ευρετήριο εγγράφων
```java
// The event handler will supply passwords as required during indexing
index.add(documentsFolder);
```

### Βήμα 5: αναζητήστε στο ευρετήριο
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

#### Επίλυση προβλημάτων
- Βεβαιωθείτε ότι ο διαχειριστής συμβάντων καλύπτει όλες τις επεκτάσεις αρχείων που χρειάζεστε να ευρετηριάσετε.  
- Δοκιμάστε πρώτα με λίγα δείγματα αρχείων για να επιβεβαιώσετε ότι εφαρμόζεται ο κωδικός.

## Πρακτικές εφαρμογές

1. **Διαχείριση επιχειρησιακών εγγράφων** – αυτοματοποιήστε το ευρετήριο εμπιστευτικών συμβάσεων, αρχείων HR και οικονομικών εκθέσεων ενώ παραμένουν κρυπτογραφημένα κατά την αποθήκευση.  
2. **Νομικά αρχεία** – ανακτήστε γρήγορα φακέλους υποθέσεων χωρίς να εκθέτετε ευαίσθητο περιεχόμενο.  
3. **Ιατρικά αρχεία** – ευρετήρια PDF και Word ασθενών συμμορφώνονται με τις απαιτήσεις HIPAA.

## Σκέψεις για την απόδοση

- **Κατανομή μνήμης** – διανείμετε επαρκή heap memory (`-Xmx2g` ή περισσότερο) για μεγάλες παρτίδες.  
- **Παράλληλη δημιουργία ευρετηρίου** – χρησιμοποιήστε `index.addAsync(...)` ή εκτελέστε πολλαπλά νήματα δημιουργίας ευρετηρίου για να πετύχετε έως και **2 εκατομμύρια έγγραφα ανά ώρα** σε μηχάνημα 8‑πυρήνων. Η μέθοδος `index.addAsync(...)` ουσιωδώς τοποθετεί έγγραφα σε ουρά για ασύγχρονη επεξεργασία.  
- **Συντήρηση ευρετηρίου** – καλέστε περιοδικά `index.optimize()` για συμπίεση του ευρετηρίου και βελτίωση της ταχύτητας ερωτημάτων.

## Συνηθισμένα προβλήματα και λύσεις

- **Λάθος κωδικός** – το έγγραφο παραλείπεται και καταγράφεται προειδοποίηση. Ελέγξτε την πηγή κωδικού.  
- **Μη υποστηριζόμενη μορφή** – εγκαταστήστε τα απαραίτητα plugins μορφής ή μετατρέψτε τα αρχεία σε υποστηριζόμενη μορφή πριν το ευρετήριο.  
- **Μεγάλα αρχεία** – αυξήστε το μέγεθος heap και σκεφτείτε να τα ευρετηριάσετε σε μικρότερες παρτίδες για να αποφύγετε `OutOfMemoryError`.

## Συχνές ερωτήσεις

**Ε: Πώς διαχειρίζομαι διαφορετικούς τύπους αρχείων;**  
Α: Το GroupDocs.Search υποστηρίζει πάνω από 120 μορφές, συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX και κοινών τύπων εικόνων. Εγκαταστήστε plugins μορφής αν χρειάζεται.

**Ε: Τι συμβαίνει αν ο κωδικός είναι λανθασμένος;**  
Α: Το έγγραφο παραλείπεται και καταγράφεται προειδοποίηση· ελέγξτε το λεξικό κωδικών ή τον διαχειριστή συμβάντων.

**Ε: Μπορώ να ευρετηριάσω αρχεία που αποθηκεύονται στο cloud;**  
Α: Ναι, αλλά πρέπει να ληφθούν σε τοπικό προσωρινό φάκελο πρώτα, επειδή η μηχανή λειτουργεί με διαδρομές συστήματος αρχείων.

**Ε: Πώς μπορώ να βελτιώσω τη σχετικότητα των αναζητήσεων;**  
Α: Ρυθμίστε το scoring με `IndexOptions`, προσθέστε συνώνυμα και χρησιμοποιήστε προχωρημένη σύνταξη ερωτημάτων όπως `field:term~` για fuzzy matching. Το `IndexOptions` είναι αντικείμενο ρύθμισης που ελέγχει το scoring και τη συμπεριφορά ευρετηρίου.

**Ε: Τι πρέπει να κάνω αν η δημιουργία ευρετηρίου αποτύχει για κάποια αρχεία;**  
Α: Εξετάστε το αρχείο καταγραφής· συνήθεις αιτίες είναι ελλιπείς κωδικοί, κατεστραμμένα αρχεία ή μη υποστηριζόμενες μορφές.

## Πόροι
- [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)

Ακολουθώντας αυτόν τον οδηγό, γνωρίζετε πλέον **πώς να αναζητήσετε πολλαπλούς τύπους αρχείων** και **να δημιουργήσετε ευρετήριο εγγράφων με κωδικό πρόσβασης** σε Java, ενισχύοντας τόσο την ασφάλεια όσο και την ανακαλυπτικότητα στις εφαρμογές σας.

---

**Τελευταία ενημέρωση:** 2026-10-28  
**Δοκιμάστηκε με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Σεμινάρια

- [How to index password‑protected documents in Java using GroupDocs.Search](/search/java/indexing/mastering-groupdocs-search-java-password-docs/)
- [Improve Query Performance with GroupDocs.Search Java: Optimize Index & Search](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)