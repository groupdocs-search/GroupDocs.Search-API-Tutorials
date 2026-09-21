---
date: '2026-09-21'
description: Μάθετε πώς να δημιουργήσετε logger, να ορίσετε το μέγιστο μέγεθος του
  log και να χρησιμοποιήσετε console logger στο GroupDocs.Search για Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Μάθετε πώς να δημιουργήσετε logger, να ορίσετε το μέγιστο μέγεθος
  του log και να χρησιμοποιήσετε console logger στο GroupDocs.Search για Java. Ακολουθήστε
  οδηγίες βήμα‑βήμα και συμβουλές βέλτιστων πρακτικών.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Πώς να δημιουργήσετε logger και να περιορίσετε το μέγεθος του log στο GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: Πώς να δημιουργήσετε logger και να περιορίσετε το μέγεθος του log στο GroupDocs.Search
  για Java
type: docs
url: /el/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Πώς να δημιουργήσετε καταγραφέα και να περιορίσετε το μέγεθος του αρχείου καταγραφής στο GroupDocs.Search για Java

Σε αυτό το μάθημα θα **πώς να δημιουργήσετε καταγραφέα** υλοποιήσεις για το GroupDocs.Search, θα διαμορφώσετε μέγιστο μέγεθος αρχείου καταγραφής και θα εναλλάξετε μεταξύ καταγραφής σε αρχείο και κονσόλα. Η σωστή διαχείριση των καταγραφών αποτρέπει τη γέμιση των δίσκων κατά τις μεγάλες εργασίες ευρετηρίασης, βελτιώνει την αντιμετώπιση προβλημάτων και σας παρέχει άμεση ανάδραση κατά την ανάπτυξη. Θα ξεκινήσουμε με τη ρύθμιση του Maven, θα περάσουμε από τη διαμόρφωση του καταγραφέα και θα ολοκληρώσουμε με ένα απλό ερώτημα αναζήτησης που δείχνει τον καταγραφέα σε δράση.

## Γρήγορες απαντήσεις
- **Τι σημαίνει “περιορισμός μεγέθους αρχείου καταγραφής”;** Περιορίζει το μέγιστο μέγεθος ενός αρχείου καταγραφής, αποτρέποντας ανεξέλεγκτη αύξηση στο δίσκο.  
- **Ποιος καταγραφέας σας επιτρέπει να περιορίσετε το μέγεθος του αρχείου καταγραφής;** Ο ενσωματωμένος `FileLogger` δέχεται μια παράμετρο μέγιστου μεγέθους.  
- **Πώς χρησιμοποιώ τον console logger σε Java;** Δημιουργήστε ένα αντικείμενο `ConsoleLogger` και ορίστε το στο `IndexSettings`.  
- **Χρειάζομαι άδεια για το GroupDocs.Search;** Μια δοκιμαστική άδεια λειτουργεί για αξιολόγηση· απαιτείται εμπορική άδεια για παραγωγή.  
- **Ποιο είναι το πρώτο βήμα;** Προσθέστε την εξάρτηση GroupDocs.Search στο Maven project σας.  

## Τι σημαίνει περιορισμός μεγέθους αρχείου καταγραφής;
Η ρύθμιση **περιορισμού μεγέθους αρχείου καταγραφής** λέει στον καταγραφέα να σταματήσει να γράφει νέες εγγραφές μόλις το αρχείο φτάσει σε ένα καθορισμένο όριο (π.χ., 4 MB). Όταν το όριο επιτευχθεί, ο καταγραφέας είτε απορρίπτει περαιτέρω μηνύματα είτε δημιουργεί νέο αρχείο, διατηρώντας τη χρήση του δίσκου προβλέψιμη.

## Γιατί να χρησιμοποιήσετε αρχείο και προσαρμοσμένους καταγραφείς με το GroupDocs.Search;
Οι καταγραφείς αρχείου και οι προσαρμοσμένοι καταγραφείς σας παρέχουν δυνατότητα ελέγχου, πληροφορίες εντοπισμού σφαλμάτων και ευελιξία. Σε περιβάλλοντα παραγωγής, τα αρχεία καταγραφής παρέχουν μόνιμο αρχείο κάθε λειτουργίας ευρετηρίασης και αναζήτησης, ενώ οι καταγραφές κονσόλας προσφέρουν άμεση ανάδραση κατά την ανάπτυξη. Αυτές οι καταγραφές βοηθούν τις ομάδες να παρακολουθούν την απόδοση, να εντοπίζουν σφάλματα και να ικανοποιούν τις απαιτήσεις συμμόρφωσης διατηρώντας λεπτομερή ίχνος δραστηριότητας.

## Προαπαιτούμενα
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 ή νεότερο, με IDE όπως IntelliJ IDEA ή Eclipse.  
- Βασική εξοικείωση με Maven και προγραμματισμό Java.  

## Ρύθμιση του GroupDocs.Search για Java

Προσθέστε τη βιβλιοθήκη στο project σας χρησιμοποιώντας μία από τις παρακάτω μεθόδους.

**Maven setup:**  

```text
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
```

**Άμεση λήψη:**  
Κατεβάστε το τελευταίο JAR από την επίσημη ιστοσελίδα: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση άδειας
Αποκτήστε δοκιμαστική άδεια ή αγοράστε άδεια μέσω της [σελίδας αδειοδότησης](https://purchase.groupdocs.com/temporary-license/).

## Πώς να δημιουργήσετε προσαρμοσμένο καταγραφέα για το GroupDocs.Search
Η δημιουργία προσαρμοσμένου καταγραφέα είναι απλή επειδή το GroupDocs.Search βασίζεται στη διεπαφή `ILogger`. Εφαρμόζοντας αυτή τη διεπαφή—ή επεκτείνοντας τους παρεχόμενους `FileLogger` ή `ConsoleLogger`—μπορείτε να ενσωματώσετε πρόσθετη συμπεριφορά όπως απομακρυσμένη προώθηση ή περιστροφή καταγραφών. Μπορείτε επίσης να προσθέσετε λογική εκκίνησης, όπως άνοιγμα δικτυακών συνδέσεων, και να διασφαλίσετε ότι οι πόροι κλείνουν στη μέθοδο τερματισμού του καταγραφέα. Αυτή η προσέγγιση σας επιτρέπει να ενσωματώσετε πλατφόρμες παρακολούθησης όπως ELK ή Splunk.

### Αγκύρωση ορισμού
`ILogger` είναι η βασική σύμβαση καταγραφής στο GroupDocs.Search· οποιαδήποτε κλάση που υλοποιεί τη μέθοδο `log(Level, String)` μπορεί να γίνει καταγραφέας.

### Παράδειγμα προσέγγισης (χωρίς μπλοκ κώδικα)
1. Δημιουργήστε μια κλάση που υλοποιεί το `ILogger`.  
2. Υπερκαλύψτε τη μέθοδο `log` ώστε να γράφει μηνύματα στον επιλεγμένο προορισμό σας (αρχείο, βάση δεδομένων, HTTP endpoint).  
3. Στη διαμόρφωση του ευρετηρίου, καλέστε `settings.setLogger(new YourCustomLogger())`.  

## Πώς να περιορίσετε το μέγεθος του αρχείου καταγραφής με τον File Logger
Η κλάση `FileLogger` γράφει καταγραφές σε αρχείο στο δίσκο και δέχεται ένα όρισμα μέγιστου μεγέθους. Καθορίζοντας το όριο μεγέθους, ο καταγραφέας σταματά αυτόματα την προσθήκη νέων εγγραφών ή δημιουργεί νέο αρχείο όταν το όριο επιτευχθεί, αποτρέποντας ανεξέλεγκτη αύξηση του δίσκου. Αυτή η συμπεριφορά εξασφαλίζει ότι η καταγραφή δεν επηρεάζει την απόδοση της ευρετηρίασης ενώ διατηρεί ένα συνοπτικό αρχείο γεγονότων.

### Αγκύρωση ορισμού
`FileLogger` είναι ένας ενσωματωμένος καταγραφέας που αποθηκεύει μηνύματα σε αρχείο κειμένου και υποστηρίζει ρυθμιζόμενο μέγιστο μέγεθος αρχείου.

### Οδηγός βήμα προς βήμα
1️⃣ **Εισαγωγή απαραίτητων πακέτων**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Διαμόρφωση ρυθμίσεων ευρετηρίου με File Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **Δημιουργία ή φόρτωση του ευρετηρίου**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Προσθήκη εγγράφων στο ευρετήριο**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Εκτέλεση ερωτήματος αναζήτησης**  
```text
```java
SearchResult result = index.search(query);
```
```

**Κύριο σημείο:** Το δεύτερο όρισμα του κατασκευαστή `FileLogger` (`4.0`) ορίζει το **set max log size** σε megabytes, αντιμετωπίζοντας άμεσα την απαίτηση **περιορισμού μεγέθους αρχείου καταγραφής**.

## Πώς να χρησιμοποιήσετε τον console logger σε Java
Όταν χρειάζεστε άμεση ορατότητα των γεγονότων καταγραφής, ο `ConsoleLogger` γράφει κάθε μήνυμα στο `System.out`. Αυτός ο καταγραφέας είναι ελαφρύς και thread‑safe, καθιστώντας τον κατάλληλο για συνεδρίες ανάπτυξης και εντοπισμού σφαλμάτων. Παρέχει άμεση ανάδραση για την πρόοδο της ευρετηρίασης, τα ερωτήματα αναζήτησης και τις συνθήκες σφάλματος χωρίς την ανάγκη αρχείων I/O, κάτι που μπορεί να επιταχύνει τη δοκιμή.

### Αγκύρωση ορισμού
`ConsoleLogger` είναι ένας ελαφρύς καταγραφέας που εξάγει τις καταγραφές στο τυπικό ρεύμα της κονσόλας, καθιστώντας τον ιδανικό για συνεδρίες εντοπισμού σφαλμάτων.

### Βήματα διαμόρφωσης
1️⃣ **Εισαγωγή του console logger**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Διαμόρφωση ρυθμίσεων ευρετηρίου με Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Δημιουργία ή φόρτωση του ευρετηρίου**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Προσθήκη εγγράφων και εκτέλεση αναζήτησης**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Συμβουλή:** Ο console logger είναι ιδανικός κατά την ανάπτυξη επειδή εκτυπώνει κάθε καταγραφή άμεσα, βοηθώντας σας να επαληθεύσετε ότι η ευρετηρίαση και η αναζήτηση λειτουργούν όπως αναμένεται.

## Πρακτικές εφαρμογές
1. **Συστήματα διαχείρισης εγγράφων:** Διατηρήστε ίχνη ελέγχου κάθε εγγράφου που ευρετηριάζεται, ικανοποιώντας τις απαιτήσεις συμμόρφωσης.  
2. **Εταιρικές μηχανές αναζήτησης:** Παρακολουθήστε την απόδοση των ερωτημάτων και τα ποσοστά σφαλμάτων σε πραγματικό χρόνο, επιτρέποντας γρήγορους ελέγχους συμμόρφωσης SLA.  
3. **Νομικό & λογισμικό συμμόρφωσης:** Καταγράψτε όρους αναζήτησης και χρονικές σφραγίδες για κανονιστική αναφορά, με καταγραφές που διατηρούνται για την απαιτούμενη περίοδο διατήρησης.

## Παράγοντες απόδοσης
- **Μέγεθος καταγραφής:** Με το **set max log size**, αποφεύγετε την υπερβολική χρήση δίσκου που θα μπορούσε διαφορετικά να επιβραδύνει τον garbage collector της JVM.  
- **Ασύγχρονη καταγραφή:** Για σενάρια υψηλής διαπερατότητας, τυλίξτε τον καταγραφέα σας σε μια ασύγχρονη ουρά για να αποσυνδέσετε το I/O από το νήμα ευρετηρίασης (η υλοποίηση βρίσκεται εκτός του πεδίου αυτού του οδηγού).  
- **Διαχείριση μνήμης:** Αποδεσμεύστε μεγάλα αντικείμενα `Index` με `index.close()` όταν δεν χρειάζονται πια, ώστε να διατηρείται μικρό το αποτύπωμα της JVM.

## Κοινά προβλήματα & λύσεις
- **Μη προσβάσιμο μονοπάτι καταγραφής:** Επαληθεύστε ότι ο φάκελος υπάρχει και ότι η εφαρμογή έχει δικαιώματα εγγραφής για το λογαριασμό χρήστη που εκτελεί τη JVM.  
- **Ο καταγραφέας δεν ενεργοποιείται:** Βεβαιωθείτε ότι καλείτε `settings.setLogger(...)` *πριν* δημιουργήσετε το αντικείμενο `Index`; διαφορετικά θα χρησιμοποιηθεί ο προεπιλεγμένος καταγραφέας.  
- **Λείπει η έξοδος κονσόλας:** Επιβεβαιώστε ότι εκτελείτε την εφαρμογή σε τερματικό που εμφανίζει το `System.out`, και ότι κανένα πλαίσιο καταγραφής (π.χ., SLF4J) δεν παρεμβάλλεται στην έξοδο.

## Συχνές ερωτήσεις

**Q: Τι ελέγχει η δεύτερη παράμετρος του `FileLogger`;**  
A: Ορίζει το μέγιστο μέγεθος του αρχείου καταγραφής σε megabytes, επιτρέποντας το **set max log size** και αποτρέποντας την ανεξέλεγκτη αύξηση.

**Q: Μπορώ να συνδυάσω καταγραφείς αρχείου και κονσόλας;**  
A: Ναι. Δημιουργήστε έναν προσαρμοσμένο καταγραφέα που προωθεί κάθε κλήση `log` τόσο σε `FileLogger` όσο και σε `ConsoleLogger`, και στη συνέχεια καταχωρίστε αυτόν τον σύνθετο καταγραφέα στο `IndexSettings`.

**Q: Πώς προσθέτω έγγραφα στο ευρετήριο μετά τη δημιουργία του;**  
A: Καλέστε `index.add(pathToNewDocs)` οποτεδήποτε· ο διαμορφωμένος καταγραφέας θα καταγράψει αυτόματα την προσθήκη.

**Q: Είναι το `ConsoleLogger` thread‑safe;**  
A: Γράφει απευθείας στο `System.out`, το οποίο η JVM συγχρονίζει εσωτερικά, καθιστώντας το ασφαλές για τυπικές πολυνηματικές περιπτώσεις.

**Q: Θα επηρεάσει ο περιορισμός του μεγέθους του αρχείου καταγραφής την ποσότητα των αποθηκευμένων πληροφοριών;**  
A: Μόλις το όριο μεγέθους επιτευχθεί, οι νέες εγγραφές είτε απορρίπτονται είτε ο καταγραφέας δημιουργεί νέο αρχείο, ανάλογα με την υλοποίηση που επιλέγετε.

## Πόροι
- [Τεκμηρίωση](https://docs.groupdocs.com/search/java/)
- [Αναφορά API](https://reference.groupdocs.com/search/java/)

---

**Τελευταία ενημέρωση:** 2026-09-21  
**Δοκιμάστηκε με:** GroupDocs.Search for Java 25.4  
**Συγγραφέας:** GroupDocs  

---

## Σχετικά μαθήματα

- [Πώς να υλοποιήσετε την καταγραφή - Μαθήματα διαχείρισης εξαιρέσεων και καταγραφής για το GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Υλοποίηση ασύγχρονης καταγραφής σε Java με το GroupDocs.Search – Οδηγός προσαρμοσμένου καταγραφέα](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Δημιουργία ευρετηρίου αναζήτησης Java – Μαθήματα GroupDocs.Search](/search/java/indexing/)