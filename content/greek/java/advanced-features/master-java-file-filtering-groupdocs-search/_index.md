---
date: '2026-02-21'
description: Μάθετε πώς να υλοποιήσετε ένα φίλτρο επέκτασης αρχείων Java χρησιμοποιώντας
  το GroupDocs.Search για Java, καλύπτοντας λογικούς τελεστές, ημερομηνίες δημιουργίας/τροποποίησης
  και φίλτρα διαδρομής.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: Φίλτρο επέκτασης αρχείου Java με το GroupDocs.Search – Οδηγός
type: docs
url: /el/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

ρίασης, αλλά η μείωση των δεδομένων που ευρετηριάζονται συνήθως υπερβαίνει το κόστος. Δοκιμάστε με ένα αντιπροσωπευτικό δείγμα για να βρείτε την ιδανική ισορροπία."

After that:

---

**Last Updated:** 2026-02-21  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

Translate:

"---  

**Τελευταία Ενημέρωση:** 2026-02-21  
**Δοκιμάστηκε Με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs"

Make sure to keep the horizontal rule and bold formatting.

Now produce final markdown with Greek translations, preserving placeholders.

Check for any missed shortcodes: none.

Check for markdown links: only one link, kept.

Check for code fences: placeholders only, no actual code fences.

All good.

Now output.# Κατακτώντας το φίλτρο επέκτασης αρχείων java με το GroupDocs.Search

Η διαχείριση ενός αυξανόμενου αποθετηρίου εγγράφων μπορεί γρήγορα να γίνει καταπιεστική, ειδικά όταν χρειάζεται να ευρετηριάσετε μόνο ορισμένους τύπους αρχείων. **Το φίλτρο επέκτασης αρχείων java** σας επιτρέπει να ενημερώσετε το GroupDocs.Search ακριβώς ποιες επεκτάσεις να συμπεριλάβετε ή να εξαιρέσετε, παρέχοντας ακριβή έλεγχο στη διαδικασία ευρετηρίασης. Σε αυτόν τον οδηγό θα περάσουμε από τη ρύθμιση του GroupDocs.Search για Java και θα σας δείξουμε πώς να συνδυάσετε το φιλτράρισμα κατά επέκταση αρχείου με λογικούς τελεστές AND, OR και NOT, καθώς και με φίλτρα εύρους ημερομηνίας και διαδρομής.

## Γρήγορες Απαντήσεις
- **Τι είναι το φίλτρο επέκτασης αρχείων java;** Μια διαμόρφωση που ενημερώνει το GroupDocs.Search ποιες επεκτάσεις αρχείων να συμπεριλάβει ή να εξαιρέσει κατά τη διαδικασία ευρετηρίασης.  
- **Ποια βιβλιοθήκη παρέχει αυτή τη δυνατότητα;** GroupDocs.Search for Java.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται πλήρης άδεια για παραγωγή.  
- **Μπορώ να συνδυάσω φίλτρα;** Ναι – μπορείτε να συνδέσετε φίλτρα επέκτασης, ημερομηνίας, μεγέθους και διαδρομής με λογική AND, OR, NOT.  
- **Είναι συμβατό με Maven;** Απόλυτα – προσθέστε την εξάρτηση GroupDocs.Search στο `pom.xml` σας.

## Τι είναι ένα φίλτρο επέκτασης αρχείων java;
Ένα **φίλτρο επέκτασης αρχείων java** είναι ένα σύνολο κανόνων που αξιολογεί την επέκταση κάθε αρχείου πριν το στείλει στη μηχανή ευρετηρίασης. Καθορίζοντας επεκτάσεις όπως `.txt`, `.pdf` ή `.epub`, μπορείτε να **συμπεριλάβετε αρχεία κατά επέκταση** ή να **εξαιρέσετε αρχεία κατά επέκταση** ώστε το ευρετήριο να παραμένει εστιασμένο και τα αποτελέσματα αναζήτησης σχετικοί.

## Γιατί να χρησιμοποιήσετε φιλτράρισμα κατά επέκταση αρχείου με το GroupDocs.Search;
- **Απόδοση:** Η παράλειψη ανεπιθύμητων αρχείων μειώνει το I/O και επιταχύνει τη διαδικασία ευρετηρίασης.  
- **Εξοικονόμηση αποθήκευσης:** Μόνο τα σχετικά έγγραφα αποθηκεύονται στο ευρετήριο, μειώνοντας τη χρήση του δίσκου.  
- **Συμμόρφωση:** Αποτρέπει την τυχαία ευρετηρίαση εμπιστευτικών ή μη υποστηριζόμενων τύπων αρχείων.  
- **Ευελιξία:** Συνδυάστε με τις δυνατότητες **date range filter java** για να στοχεύσετε αρχεία που δημιουργήθηκαν ή τροποποιήθηκαν μέσα σε συγκεκριμένες περιόδους.

## Προαπαιτούμενα

### Απαιτούμενες Βιβλιοθήκες και Εξαρτήσεις
- **GroupDocs.Search for Java**: Έκδοση 25.4 ή νεότερη  
- **Java Development Kit (JDK)**: Εγκατεστημένη συμβατή έκδοση  

### Ρύθμιση Περιβάλλοντος
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse ή οποιοδήποτε IDE συμβατό με Maven.

### Προαπαιτούμενες Γνώσεις
- Βασικός προγραμματισμός σε Java  
- Εξοικείωση με file I/O σε Java  
- Κατανόηση των κανονικών εκφράσεων και της διαχείρισης ημερομηνίας‑ώρας  

## Ρύθμιση του GroupDocs.Search για Java
Για να αρχίσετε να χρησιμοποιείτε το GroupDocs.Search, πρέπει να το συμπεριλάβετε ως εξάρτηση στο έργο σας.

### Διαμόρφωση Maven
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
Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση απευθείας από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Απόκτηση Άδειας
1. **Δωρεάν Δοκιμή** – εξερευνήστε τις δυνατότητες χωρίς κόστος.  
2. **Προσωρινή Άδεια** – αποκτήστε πλήρη λειτουργικότητα για περιορισμένο χρονικό διάστημα.  
3. **Αγορά** – αποκτήστε μόνιμη άδεια για χρήση σε παραγωγή.  

### Βασική Αρχικοποίηση και Ρύθμιση
```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Οδηγός Υλοποίησης
Παρακάτω εμβαθύνουμε σε κάθε τύπο φίλτρου, εξηγώντας **γιατί είναι σημαντικό** και παρέχοντας κώδικα βήμα‑βήμα που μπορείτε να αντιγράψετε στο έργο σας.

### Φιλτράρισμα Κατά Επέκταση Αρχείου
Φιλτράρετε αρχεία με βάση τις επεκτάσεις τους κατά τη διαδικασία ευρετηρίασης. Αυτό είναι ιδανικό όταν θέλετε να επεξεργαστείτε μόνο e‑books (`.fb2`, `.epub`) και αρχεία απλού κειμένου (`.txt`).

#### Επισκόπηση
Χρησιμοποιήστε το `DocumentFilter.createFileExtension` για να ορίσετε λευκή λίστα επεκτάσεων.

#### Βήματα Υλοποίησης
1. **Δημιουργία Φίλτρου**:

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Αρχικοποίηση Ευρετηρίου και Προσθήκη Εγγράφων**:

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Λογικό Φίλτρο NOT
Εξαιρέστε συγκεκριμένες επεκτάσεις, όπως ιστοσελίδες και PDF, όταν δεν χρειάζονται για το σενάριο αναζήτησής σας.

#### Βήματα Υλοποίησης
1. **Δημιουργία Φίλτρου Εξαίρεσης**:

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Εφαρμογή στις Ρυθμίσεις Ευρετηρίου**:

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Προσθήκη Εγγράφων**:

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Λογικό Φίλτρο AND
Συνδυάστε πολλές συνθήκες—ημερομηνία δημιουργίας, επέκταση και μέγεθος αρχείου—ώστε **μόνο τα αρχεία που ικανοποιούν όλα τα κριτήρια** να ευρετηριαστούν.

#### Επισκόπηση
Το `DocumentFilter.createAnd` συγχωνεύει πολλαπλά φίλτρα σε έναν ενιαίο κανόνα.

#### Βήματα Υλοποίησης
1. **Ορισμός Φίλτρων**:

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Συνδυασμός Φίλτρων**:

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Ευρετηρίαση Εγγράφων**:

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Λογικό Φίλτρο OR
Συμπεριλάβετε αρχεία που ικανοποιούν **οποιαδήποτε** από τις καθορισμένες συνθήκες—χρήσιμο όταν θέλετε να καταγράψετε τόσο μικρά αρχεία κειμένου όσο και μεγαλύτερα μη‑κειμενικά αρχεία.

#### Βήματα Υλοποίησης
1. **Ορισμός Φίλτρων**:

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Συνδυασμός Φίλτρων με Λογικές Συνθήκες**:

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Ολοκλήρωση Φίλτρου OR**:

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Φίλτρα Χρόνου Δημιουργίας
Στοχεύστε αρχεία που δημιουργήθηκαν μέσα σε συγκεκριμένη περίοδο—ένα κλασικό σενάριο **date range filter java**.

#### Βήματα Υλοποίησης
1. **Ορισμός Φίλτρου Εύρους Ημερομηνίας**:

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Ευρετηρίαση Εγγράφων**:

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Φίλτρα Χρόνου Τροποποίησης
Εξαιρέστε αρχεία που τροποποιήθηκαν μετά από μια συγκεκριμένη ημερομηνία αποκοπής.

#### Βήματα Υλοποίησης
1. **Ορισμός Φίλτρου**:

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Ευρετηρίαση Εγγράφων**:

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Φιλτράρισμα Διαδρομής Αρχείου
Περιορίστε την ευρετηρίαση σε αρχεία που βρίσκονται σε συγκεκριμένους φακέλους ή ταιριάζουν σε ένα μοτίβο—ιδανικό για **include files by extension** μέσα σε συγκεκριμένη ιεραρχία καταλόγων.

#### Βήματα Υλοποίησης
1. **Ορισμός Φίλτρου Διαδρομής Αρχείου**:

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Αρχικοποίηση Ευρετηρίου και Προσθήκη Εγγράφων**:

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Συνηθισμένα Πιθανά Προβλήματα & Συμβουλές
- **Ποτέ μην αναμειγνύετε απόλυτες και σχετικές διαδρομές** στην ίδια διαμόρφωση φίλτρου – μπορεί να οδηγήσει σε ανεπιθύμητες εξαιρέσεις.  
- **Επαναφέρετε το `IndexSettings`** όταν αλλάζετε σύνολα φίλτρων· διαφορετικά τα προηγούμενα φίλτρα μπορεί να παραμείνουν.  
- **Συνδυάστε ένα άνω όριο μήκους με φίλτρο επέκτασης** για μεγάλες συλλογές ώστε η χρήση μνήμης να παραμένει χαμηλή.  
- **Ενεργοποιήστε την καταγραφή** (`LoggingOptions.setEnabled(true)`) για να δείτε γιατί απορρίφθηκε ένα αρχείο.  

## Συχνές Ερωτήσεις

**Ε: Μπορώ να αλλάξω τα κριτήρια του φίλτρου μετά τη δημιουργία του ευρετηρίου;**  
Α: Ναι. Αναδημιουργήστε το ευρετήριο με νέο `DocumentFilter` ή χρησιμοποιήστε την επαυξητική ευρετηρίαση με ενημερωμένες ρυθμίσεις.

**Ε: Λειτουργεί το φίλτρο επέκτασης αρχείων java σε συμπιεσμένα αρχεία (π.χ., ZIP);**  
Α: Το GroupDocs.Search μπορεί να ευρετηριάσει υποστηριζόμενες μορφές αρχείων συμπιεσμένων, αλλά το φίλτρο επέκτασης εφαρμόζεται στο ίδιο το αρχείο συμπιεσμού, όχι στα εσωτερικά αρχεία. Χρησιμοποιήστε ένθετα φίλτρα για πιο λεπτομερή έλεγχο.

**Ε: Πώς μπορώ να εντοπίσω το λόγο για τον οποίο ένα συγκεκριμένο αρχείο αποκλείστηκε;**  
Α: Ενεργοποιήστε την καταγραφή της βιβλιοθήκης (`LoggingOptions.setEnabled(true)`) και εξετάστε το αρχείο καταγραφής – αναφέρει ποιο φίλτρο απέριψε κάθε αρχείο.

**Ε: Είναι δυνατόν να συνδυάσω το φίλτρο επέκτασης αρχείων java με προσαρμοσμένα regex φίλτρα;**  
Α: Απόλυτα. Τοποθετήστε ένα regex φίλτρο μέσα στο `DocumentFilter.createAnd()` μαζί με το φίλτρο επέκτασης.

**Ε: Ποια είναι η επίδραση στην απόδοση όταν προστίθενται πολλά φίλτρα;**  
Α: Κάθε φίλτρο προσθέτει μια μέτρια επιβάρυνση κατά τη διαδικασία ευρετηρίασης, αλλά η μείωση των δεδομένων που ευρετηριάζονται συνήθως υπερβαίνει το κόστος. Δοκιμάστε με ένα αντιπροσωπευτικό δείγμα για να βρείτε την ιδανική ισορροπία.

---

**Τελευταία Ενημέρωση:** 2026-02-21  
**Δοκιμάστηκε Με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs