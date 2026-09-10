---
date: '2026-09-06'
description: Μάθετε πώς να φιλτράρετε τις επεκτάσεις αρχείων java χρησιμοποιώντας
  το GroupDocs.Search για Java, καλύπτοντας τους λογικούς τελεστές AND, OR, NOT, τα
  φίλτρα εύρους ημερομηνίας και τα φίλτρα διαδρομής.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: Φιλτράρετε τις επεκτάσεις αρχείων java χρησιμοποιώντας το GroupDocs.Search.
  Μάθετε πώς να συνδυάσετε τα φίλτρα επεκτάσεων, εύρους ημερομηνίας και διαδρομής
  με λογικούς τελεστές σε Java.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: Φιλτράρετε τις επεκτάσεις αρχείων java με το GroupDocs.Search – Πλήρης Οδηγός
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: Πώς να φιλτράρετε τις επεκτάσεις αρχείων java με το GroupDocs.Search
type: docs
url: /el/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Φιλτράρισμα επεκτάσεων αρχείων java με το GroupDocs.Search

Σε αυτό το ολοκληρωμένο εκπαιδευτικό υλικό θα μάθετε πώς να **φιλτράρετε επεκτάσεις αρχείων java** κατά την ευρετηρίαση εγγράφων με το GroupDocs.Search. Στο τέλος του οδηγού θα μπορείτε να συμπεριλάβετε μόνο τους τύπους αρχείων που χρειάζεστε, να εξαιρέσετε ανεπιθύμητες μορφές και να συνδυάσετε αυτούς τους κανόνες με φίλτρα εύρους ημερομηνίας και διαδρομής χρησιμοποιώντας λογικούς τελεστές AND, OR και NOT. Αυτή η προσέγγιση διατηρεί το ευρετήριο ελαφρύ, επιταχύνει τις αναζητήσεις και σας βοηθά να συμμορφωθείτε με τις πολιτικές διαχείρισης δεδομένων.

## Σύντομες απαντήσεις
- **Τι είναι το φίλτρο επεκτάσεων αρχείων java;** Είναι ένας κανόνας που λέει στο GroupDocs.Search ποιες επεκτάσεις αρχείων να συμπεριλάβει ή να εξαιρέσει κατά την ευρετηρίαση.  
- **Ποια βιβλιοθήκη παρέχει αυτή τη δυνατότητα;** GroupDocs.Search for Java.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται πλήρης άδεια για παραγωγή.  
- **Μπορώ να συνδυάσω φίλτρα;** Ναι – μπορείτε να αλυσίδωση επεκτάσεων, ημερομηνίας, μεγέθους και διαδρομής φίλτρων με λογική AND, OR, NOT.  
- **Είναι συμβατό με Maven;** Απόλυτα – προσθέστε την εξάρτηση GroupDocs.Search στο `pom.xml` σας.

## Τι είναι ένα φίλτρο επεκτάσεων αρχείων java;
Ένα **java file extension filter** είναι ένα σύνολο κανόνων που αξιολογεί την επέκταση κάθε αρχείου πριν το στείλει στη μηχανή ευρετηρίασης. Καθορίζοντας επεκτάσεις όπως `.txt`, `.pdf` ή `.epub`, μπορείτε να **συμπεριλάβετε αρχεία με βάση την επέκταση** ή να **εξαιρέσετε αρχεία με βάση την επέκταση** ώστε το ευρετήριό σας να παραμένει εστιασμένο και τα αποτελέσματα αναζήτησης σχετικοί.

## Γιατί να χρησιμοποιήσετε φιλτράρισμα επεκτάσεων αρχείων με το GroupDocs.Search;
Το φιλτράρισμα επεκτάσεων αρχείων βελτιώνει την αποδοτικότητα της ευρετηρίασης εξαιρώντας άσχετες μορφές, μειώνει τις απαιτήσεις αποθήκευσης και βοηθά στην τήρηση κανόνων συμμόρφωσης αποτρέποντας την εισαγωγή ανεπιθύμητου περιεχομένου στο ευρετήριο. Επίσης, επιτρέπει ταχύτερες απαντήσεις σε ερωτήματα επειδή η μηχανή αναζήτησης επεξεργάζεται ένα μικρότερο, πιο σχετικό σύνολο δεδομένων.

- **Απόδοση:** Η παράλειψη ανεπιθύμητων αρχείων μειώνει το I/O και επιταχύνει την ευρετηρίαση έως και 40 % σε μεγάλα αποθετήρια.  
- **Εξοικονόμηση αποθήκευσης:** Μόνο τα σχετικά έγγραφα αποθηκεύονται στο ευρετήριο, μειώνοντας τη χρήση δίσκου κατά μέσο όρο 30 %.  
- **Συμμόρφωση:** Αποτρέπει την τυχαία ευρετηρίαση εμπιστευτικών ή μη υποστηριζόμενων τύπων αρχείων.  
- **Ευελιξία:** Συνδυάστε με τις δυνατότητες **date range filter java** για να στοχεύσετε αρχεία που δημιουργήθηκαν ή τροποποιήθηκαν σε συγκεκριμένες περιόδους.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

### Απαιτούμενες βιβλιοθήκες και εξαρτήσεις
- **GroupDocs.Search for Java** – έκδοση 25.4 ή νεότερη (υποστηρίζει 60+ μορφές εισόδου).  
- **Java Development Kit (JDK)** – οποιαδήποτε συμβατή έκδοση (8 ή νεότερη).

### Ρύθμιση περιβάλλοντος
- Ολοκληρωμένο Περιβάλλον Ανάπτυξης (IDE): IntelliJ IDEA, Eclipse ή οποιοδήποτε IDE συμβατό με Maven.

### Προαπαιτούμενες γνώσεις
- Βασικός προγραμματισμός Java.  
- Εξοικείωση με file I/O σε Java.  
- Κατανόηση των κανονικών εκφράσεων και της διαχείρισης ημερομηνίας‑ώρας.

## Ρύθμιση του GroupDocs.Search για Java
Για να αρχίσετε να χρησιμοποιείτε το GroupDocs.Search, πρέπει να το συμπεριλάβετε ως εξάρτηση στο έργο σας.

### Διαμόρφωση Maven
Προσθέστε την παρακάτω διαμόρφωση αποθετηρίου και εξάρτησης στο αρχείο `pom.xml` σας:

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
Εναλλακτικά, κατεβάστε την τελευταία έκδοση απευθείας από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Απόκτηση άδειας
- **Δωρεάν δοκιμή** – εξερευνήστε τις δυνατότητες χωρίς κόστος.  
- **Προσωρινή άδεια** – αποκτήστε πλήρη λειτουργικότητα για περιορισμένο χρονικό διάστημα.  
- **Αγορά** – αποκτήστε μόνιμη άδεια για χρήση σε παραγωγή.

### Βασική αρχικοποίηση και ρύθμιση
Μόλις προστεθεί η βιβλιοθήκη, αρχικοποιήστε το περιβάλλον ευρετηρίασής σας. Η κλάση `IndexSettings` περιέχει όλες τις επιλογές διαμόρφωσης, συμπεριλαμβανομένων των φίλτρων.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Οδηγός υλοποίησης
Παρακάτω εμβαθύνουμε σε κάθε τύπο φίλτρου, εξηγώντας **γιατί είναι σημαντικό** και παρέχοντας βήμα‑βήμα οδηγίες που μπορείτε να αντιγράψετε στο έργο σας.

### Φιλτράρισμα επεκτάσεων αρχείων
Φιλτράρετε αρχεία με βάση τις επεκτάσεις τους κατά την ευρετηρίαση. Αυτό είναι ιδανικό όταν θέλετε να επεξεργαστείτε μόνο e‑books (`.fb2`, `.epub`) και αρχεία απλού κειμένου (`.txt`).

#### Επισκόπηση
`DocumentFilter.createFileExtension` δημιουργεί μια λευκή λίστα επεκτάσεων.

#### Βήματα υλοποίησης
1. **Δημιουργία φίλτρου** – ορίστε τις επεκτάσεις που θέλετε να διατηρήσετε.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Αρχικοποίηση ευρετηρίου και προσθήκη εγγράφων** – εφαρμόστε το φίλτρο κατά τη δημιουργία του `IndexSettings`.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Λογικό φίλτρο NOT
Εξαίρεση συγκεκριμένων επεκτάσεων, όπως ιστοσελίδες και PDF, όταν δεν χρειάζονται για το σενάριο αναζήτησής σας.

#### Βήματα υλοποίησης
1. **Δημιουργία φίλτρου αποκλεισμού** – καθορίστε τις επεκτάσεις που θα απορρίψετε.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Εφαρμογή στις ρυθμίσεις ευρετηρίου** – συνδυάστε το φίλτρο NOT με άλλους κανόνες.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Προσθήκη εγγράφων** – μόνο τα αρχεία που περνούν το συνδυασμένο φίλτρο ευρετηριάζονται.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Λογικό φίλτρο AND
Συνδυάστε πολλαπλές συνθήκες—ημερομηνία δημιουργίας, επέκταση και μέγεθος αρχείου—ώστε **μόνο τα αρχεία που πληρούν όλα τα κριτήρια** να ευρετηριάζονται.

#### Επισκόπηση
`DocumentFilter.createAnd` συνδυάζει πολλαπλά φίλτρα σε έναν ενιαίο κανόνα.

#### Βήματα υλοποίησης
1. **Ορισμός φίλτρων** – δημιουργήστε ξεχωριστά φίλτρα για κάθε συνθήκη.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Συνδυασμός φίλτρων** – χρησιμοποιήστε τον τελεστή AND για να απαιτήσετε όλες τις συνθήκες.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Ευρετηρίαση εγγράφων** – περάστε το συνδυασμένο φίλτρο στη διαδικασία ευρετηρίασης.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Λογικό φίλτρο OR
Συμπεριλάβετε αρχεία που ικανοποιούν **οποιαδήποτε** από τις καθορισμένες συνθήκες—χρήσιμο όταν θέλετε να καταγράψετε τόσο μικρά αρχεία κειμένου όσο και μεγαλύτερα μη‑κειμενικά αρχεία.

#### Βήματα υλοποίησης
1. **Ορισμός φίλτρων** – δημιουργήστε ξεχωριστά φίλτρα για κάθε εναλλακτική συνθήκη.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Συνδυασμός φίλτρων με λογικές συνθήκες** – χρησιμοποιήστε τον τελεστή OR.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Ολοκλήρωση φίλτρου OR** – συνδέστε το συνδυασμένο φίλτρο στη διαμόρφωση του ευρετηρίου.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Φίλτρα χρόνου δημιουργίας
Στοχεύστε αρχεία που δημιουργήθηκαν μέσα σε συγκεκριμένη περίοδο—ένα κλασικό σενάριο **date range filter java**.

#### Βήματα υλοποίησης
1. **Ορισμός φίλτρου εύρους ημερομηνίας** – καθορίστε ημερομηνίες έναρξης και λήξης.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Ευρετηρίαση εγγράφων** – μόνο τα αρχεία των οποίων τα χρονικά σήματα δημιουργίας εμπίπτουν στο εύρος ευρετηριάζονται.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Φίλτρα χρόνου τροποποίησης
Εξαίρεση αρχείων που τροποποιήθηκαν μετά από μια συγκεκριμένη ημερομηνία αποκοπής.

#### Βήματα υλοποίησης
1. **Ορισμός φίλτρου** – ορίστε το μέγιστο χρονικό σήμα τροποποίησης.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Ευρετηρίαση εγγράφων** – τα αρχεία νεότερα από την ημερομηνία αποκοπής αγνοούνται.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Φιλτράρισμα διαδρομής αρχείου
Περιορίστε την ευρετηρίαση σε αρχεία που βρίσκονται σε συγκεκριμένους φακέλους ή ταιριάζουν με ένα μοτίβο—ιδανικό για **include files by extension** μέσα σε συγκεκριμένη ιεραρχία καταλόγων.

#### Βήματα υλοποίησης
1. **Ορισμός φίλτρου διαδρομής αρχείου** – χρησιμοποιήστε μοτίβα glob ή regex για να ταιριάξετε καταλόγους.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Αρχικοποίηση ευρετηρίου και προσθήκη εγγράφων** – εφαρμόστε το φίλτρο διαδρομής μαζί με άλλους κανόνες.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Συνηθισμένα προβλήματα & συμβουλές

- **Ποτέ μην αναμειγνύετε απόλυτες και σχετικές διαδρομές** στην ίδια διαμόρφωση φίλτρου – μπορεί να οδηγήσει σε απροσδόκητες εξαιρέσεις.  
- **Επαναφέρετε το `IndexSettings`** όταν αλλάζετε σύνολα φίλτρων· διαφορετικά τα προηγούμενα φίλτρα μπορεί να παραμείνουν.  
- **Συνδυάστε ένα άνω όριο μήκους με φίλτρο επέκτασης** για μεγάλες συλλογές ώστε να διατηρείται η χρήση μνήμης χαμηλή.  
- Το LoggingOptions ελέγχει τη διαμόρφωση καταγραφής για το GroupDocs.Search.  
- **Ενεργοποιήστε την καταγραφή** (`LoggingOptions.setEnabled(true)`) για να δείτε γιατί απορρίφθηκε ένα αρχείο.  

## Συχνές ερωτήσεις

**Q: Μπορώ να αλλάξω τα κριτήρια φίλτρου μετά τη δημιουργία του ευρετηρίου;**  
A: Ναι. Ανακατασκευάστε το ευρετήριο με νέο `DocumentFilter` ή χρησιμοποιήστε την επαυξητική ευρετηρίαση με ενημερωμένες ρυθμίσεις.

**Q: Λειτουργεί το φίλτρο επεκτάσεων αρχείων java σε συμπιεσμένα αρχεία (π.χ., ZIP);**  
A: Το GroupDocs.Search μπορεί να ευρετηριάσει υποστηριζόμενες μορφές αρχείων συμπιεσμένων, αλλά το φίλτρο επέκτασης εφαρμόζεται στο ίδιο το αρχείο συμπιεσμού, όχι στα εσωτερικά αρχεία. Χρησιμοποιήστε ένθετα φίλτρα για πιο λεπτομερή έλεγχο.

**Q: Πώς μπορώ να εντοπίσω γιατί ένα συγκεκριμένο αρχείο αποκλείστηκε;**  
A: Ενεργοποιήστε την καταγραφή της βιβλιοθήκης (`LoggingOptions.setEnabled(true)`) και εξετάστε το αρχείο καταγραφής – αναφέρει ποιο φίλτρο απέριψε κάθε αρχείο.

**Q: Είναι δυνατόν να συνδυάσω το φίλτρο επεκτάσεων αρχείων java με προσαρμοσμένα regex φίλτρα;**  
A: Απόλυτα. Ενσωματώστε ένα regex φίλτρο μέσα στο `DocumentFilter.createAnd()` μαζί με το φίλτρο επέκτασης.

**Q: Ποιος είναι ο αντίκτυπος στην απόδοση όταν προστίθενται πολλά φίλτρα;**  
A: Κάθε φίλτρο προσθέτει μια ήπια επιβάρυνση κατά την ευρετηρίαση, αλλά η μείωση των δεδομένων που ευρετηριάζονται συνήθως υπερβαίνει το κόστος. Δοκιμάστε με ένα αντιπροσωπευτικό δείγμα για να βρείτε την ιδανική ισορροπία.

---

**Τελευταία ενημέρωση:** 2026-09-06  
**Δοκιμή με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Προσαρμοσμένη μορφή ημερομηνίας Java | Αναζήτηση εύρους ημερομηνίας με το GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: Κύριες Boolean Αναζητήσεις με GroupDocs.Search for Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Βελτιστοποίηση Απόδοσης Αναζήτησης με Προηγμένες Τεχνικές Ευρετηρίασης στο GroupDocs.Search for Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)

