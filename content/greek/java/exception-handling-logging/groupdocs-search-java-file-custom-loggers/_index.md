---
date: '2026-02-24'
description: Μάθετε πώς να δημιουργήσετε προσαρμοσμένο καταγραφέα, να ορίσετε το μέγιστο
  μέγεθος αρχείου καταγραφής και να διαμορφώσετε καταγραφέα κονσόλας ή αρχείου στο
  GroupDocs.Search για Java.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Πώς να δημιουργήσετε προσαρμοσμένο καταγραφέα και να περιορίσετε το μέγεθος
  του αρχείου καταγραφής με το GroupDocs.Search Java
type: docs
url: /el/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Περιορισμός μεγέθους αρχείου καταγραφής με τους GroupDocs.Search Java Loggers

Σε αυτόν τον οδηγό θα **δημιουργήσετε προσαρμοσμένες υλοποιήσεις logger** και θα μάθετε πώς να **περιορίζετε το μέγεθος του αρχείου καταγραφής** ενώ χρησιμοποιείτε το GroupDocs.Search για Java. Ο έλεγχος της ανάπτυξης των καταγραφών είναι κρίσιμος για την ευρετηρίαση εγγράφων μεγάλης κλίμακας, και οι ενσωματωμένοι logger σας επιτρέπουν να **ορίσετε μέγιστο μέγεθος καταγραφής**, **ανακυκλώσετε το αρχείο καταγραφής**, ή να χρησιμοποιήσετε **console logger** για άμεση ανάδραση. Ας περάσουμε από τη πλήρη ρύθμιση, από τη διαμόρφωση Maven μέχρι την εκτέλεση ερωτήματος αναζήτησης, και δούμε πώς να **προσθέσετε έγγραφα στο ευρετήριο** με τον logger σε λειτουργία.

## Quick Answers
- **Τι σημαίνει “limit log file size”;** Περιορίζει το μέγιστο μέγεθος ενός αρχείου καταγραφής, αποτρέποντας την ανεξέλεγκτη αύξηση στο δίσκο.  
- **Ποιος logger σας επιτρέπει να περιορίσετε το μέγεθος του αρχείου καταγραφής;** Ο ενσωματωμένος `FileLogger` δέχεται μια παράμετρο max‑size.  
- **Πώς χρησιμοποιώ το console logger java;** Δημιουργήστε ένα στιγμιότυπο του `ConsoleLogger` και ορίστε το στο `IndexSettings`.  
- **Χρειάζομαι άδεια για το GroupDocs.Search;** Μια δοκιμαστική έκδοση λειτουργεί για αξιολόγηση· απαιτείται εμπορική άδεια για παραγωγή.  
- **Ποιο είναι το πρώτο βήμα;** Προσθέστε την εξάρτηση GroupDocs.Search στο Maven project σας.  

## What is limit log file size?
Ο περιορισμός του μεγέθους του αρχείου καταγραφής σημαίνει τη διαμόρφωση του logger έτσι ώστε, όταν το αρχείο φτάσει σε ένα προκαθορισμένο όριο (π.χ., 4 MB), να σταματήσει να μεγαλώνει ή να ανακυκλώνεται. Αυτό διατηρεί το αποτύπωμα αποθήκευσης της εφαρμογής προβλέψιμο και αποτρέπει τη μείωση της απόδοσης.

## Why use file and custom loggers with GroupDocs.Search?
- **Auditability:** Διατηρεί μόνιμο αρχείο των γεγονότων ευρετηρίασης και αναζήτησης.  
- **Debugging:** Εντοπίζει γρήγορα προβλήματα εξετάζοντας συνοπτικές καταγραφές.  
- **Flexibility:** Επιλέξτε μεταξύ μόνιμων αρχείων καταγραφής και άμεσης εξόδου στην κονσόλα (`use console logger`).  

## Prerequisites
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 ή νεότερο, IDE (IntelliJ IDEA, Eclipse, κ.λπ.).  
- Βασικές γνώσεις Java και Maven.  

## Setting Up GroupDocs.Search for Java

Προσθέστε τη βιβλιοθήκη στο project σας χρησιμοποιώντας μία από τις παρακάτω μεθόδους.

**Maven Setup:**

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

**Direct Download:**  
Κατεβάστε το πιο πρόσφατο JAR από την επίσημη ιστοσελίδα: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
Αποκτήστε μια δοκιμαστική άδεια ή αγοράστε άδεια μέσω της [licensing page](https://purchase.groupdocs.com/temporary-license/).

## How to create custom logger for GroupDocs.Search
Το GroupDocs.Search σας επιτρέπει να ενσωματώσετε οποιαδήποτε υλοποίηση της διεπαφής `ILogger`. Επεκτείνοντας το `FileLogger` ή το `ConsoleLogger`, μπορείτε να προσθέσετε επιπλέον συμπεριφορά—όπως η ανακύκλωση του αρχείου καταγραφής ή η προώθηση μηνυμάτων σε απομακρυσμένη υπηρεσία παρακολούθησης. Αυτή η ευελιξία είναι ο λόγος που πολλές ομάδες **δημιουργούν προσαρμοσμένους logger** που ταιριάζουν στις επιχειρησιακές τους ανάγκες.

## How to limit log file size with File Logger
Παρακάτω βρίσκεται ένας οδηγός βήμα‑βήμα που δείχνει πώς να **διαμορφώσετε file logger** ώστε το αρχείο καταγραφής να μην υπερβαίνει ποτέ το μέγεθος που καθορίζετε.

### 1️⃣ Import Necessary Packages
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Set Up Index Settings with File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Create or Load the Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Add Documents to the Index
```java
index.add(documentsFolder);
```

### 5️⃣ Perform a Search Query
```java
SearchResult result = index.search(query);
```

**Key point:** Το δεύτερο όρισμα του κατασκευαστή `FileLogger` (`4.0`) ορίζει το **set max log size** σε megabytes, αντιμετωπίζοντας άμεσα την απαίτηση **limit log file size**.

## How to use console logger java
Αν προτιμάτε άμεση ανάδραση στο τερματικό, αντικαταστήστε τον file logger με έναν console logger.

### 1️⃣ Import the Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Set Up Index Settings with Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Create or Load the Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Add Documents and Perform a Search
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Tip:** Ο console logger είναι ιδανικός κατά την ανάπτυξη επειδή εκτυπώνει κάθε καταγραφή άμεσα, βοηθώντας σας να επαληθεύσετε ότι η ευρετηρίαση και η αναζήτηση λειτουργούν όπως αναμένεται.

## Practical Applications
1. **Document Management Systems:** Διατηρεί αρχεία ελέγχου για κάθε έγγραφο που ευρετηριάζεται.  
2. **Enterprise Search Engines:** Παρακολουθεί την απόδοση των ερωτημάτων και τα ποσοστά σφαλμάτων σε πραγματικό χρόνο.  
3. **Legal & Compliance Software:** Καταγράφει όρους αναζήτησης για κανονιστική αναφορά.

## Performance Considerations
- **Log Size:** Με το **set max log size**, αποφεύγετε την υπερβολική χρήση δίσκου που μπορεί να επιβραδύνει την εφαρμογή σας.  
- **Asynchronous Logging:** Αν χρειάζεστε υψηλότερη διαπερατότητα, σκεφτείτε να τυλίξετε τον logger σε μια async ουρά (εκτός του πεδίου αυτού του οδηγού).  
- **Memory Management:** Απελευθερώστε μεγάλα αντικείμενα `Index` όταν δεν χρειάζονται πια, ώστε το αποτύπωμα της JVM να παραμένει χαμηλό.

## Common Issues & Solutions
- **Log path not accessible:** Επαληθεύστε ότι ο φάκελος υπάρχει και ότι η εφαρμογή έχει δικαιώματα εγγραφής.  
- **Logger not firing:** Βεβαιωθείτε ότι καλείτε `settings.setLogger(...)` *πριν* δημιουργήσετε το αντικείμενο `Index`.  
- **Console output missing:** Επιβεβαιώστε ότι εκτελείτε την εφαρμογή σε τερματικό που εμφανίζει το `System.out`.

## Frequently Asked Questions

**Q: What does the second parameter of `FileLogger` control?**  
A: It sets the maximum size of the log file in megabytes, allowing you to **set max log size**.

**Q: Can I combine file and console loggers?**  
A: Yes, by creating a custom logger that forwards messages to both destinations.

**Q: How do I add documents to index after the initial creation?**  
A: Call `index.add(pathToNewDocs)` at any time; the logger will record the operation.

**Q: Is `ConsoleLogger` thread‑safe?**  
A: It writes directly to `System.out`, which is synchronized by the JVM, making it safe for most use cases.

**Q: Will limiting the log file size affect the amount of information stored?**  
A: Once the size limit is reached, new entries may be discarded or the file may **roll over log file**, depending on the logger implementation.

## Resources
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Last Updated:** 2026-02-24  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs  

---