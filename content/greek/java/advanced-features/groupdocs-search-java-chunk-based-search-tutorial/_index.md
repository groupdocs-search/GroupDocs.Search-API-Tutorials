---
date: '2026-02-21'
description: Μάθετε πώς να προσθέτετε έγγραφα στο ευρετήριο και να αυξάνετε την απόδοση
  της αναζήτησης με αναζήτηση βασισμένη σε τμήματα (chunk‑based) σε Java χρησιμοποιώντας
  το GroupDocs.Search, βελτιστοποιώντας τη μνήμη του ευρετηρίου αναζήτησης Java για
  μεγάλα σύνολα εγγράφων.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Προσθήκη εγγράφων στο ευρετήριο με αναζήτηση κατά τμήματα σε Java
type: docs
url: /el/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Προσθήκη εγγράφων στο ευρετήριο με αναζήτηση βασισμένη σε τμήματα σε Java

Σε σύγχρονες εφαρμογές που χρειάζεται να **προσθέσουν έγγραφα στο ευρετήριο** γρήγορα και στη συνέχεια να εκτελούν γρήγορα ερωτήματα βασισμένα σε τμήματα, θα θέλετε μια λύση που κλιμακώνεται χωρίς να καταναλώνει υπερβολική μνήμη. Αυτό το σεμινάριο σας καθοδηγεί στη ρύθμιση του GroupDocs.Search για Java, στην προσθήκη πολλαπλών φακέλων εγγράφων και στη διαμόρφωση της μηχανής για **αύξηση της απόδοσης αναζήτησης** ενώ διατηρεί τη χρήση **java search index memory** υπό έλεγχο. Είτε ευρετηριάζετε νομικά συμβόλαια, αιτήματα υποστήριξης ή ερευνητικές εργασίες, τα παρακάτω βήματα θα σας δώσουν μια υλοποίηση έτοιμη για παραγωγή.

## Quick Answers
- **Ποιο είναι το πρώτο βήμα;** Δημιουργήστε έναν φάκελο ευρετηρίου αναζήτησης.  
- **Πώς μπορώ να συμπεριλάβω πολλά αρχεία;** Χρησιμοποιήστε `index.add()` για κάθε φάκελο εγγράφων.  
- **Ποια επιλογή ενεργοποιεί την αναζήτηση τμημάτων;** `options.setChunkSearch(true)`.  
- **Μπορώ να συνεχίσω την αναζήτηση μετά το πρώτο τμήμα;** Ναι, καλέστε `index.searchNext()` με το token.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή ή προσωρινή άδεια λειτουργεί για ανάπτυξη· απαιτείται πλήρης άδεια για παραγωγή.  

## What You’ll Learn
- Πώς να δημιουργήσετε ένα ευρετήριο αναζήτησης σε συγκεκριμένο φάκελο.  
- Βήματα για **προσθήκη εγγράφων στο ευρετήριο** από πολλαπλές τοποθεσίες.  
- Διαμόρφωση επιλογών αναζήτησης για ενεργοποίηση της αναζήτησης βασισμένης σε τμήματα.  
- Διενέργεια αρχικών και επόμενων αναζητήσεων βασισμένων σε τμήματα.  
- Πραγματικά σενάρια όπου η αναζήτηση εγγράφων βασισμένη σε τμήματα διαπρέπει.  

## Prerequisites
Για να ακολουθήσετε αυτόν τον οδηγό, βεβαιωθείτε ότι έχετε:

- **Απαιτούμενες βιβλιοθήκες**: GroupDocs.Search for Java 25.4 ή νεότερη.  
- **Ρύθμιση περιβάλλοντος**: Εγκατεστημένο συμβατό Java Development Kit (JDK).  
- **Προαπαιτούμενες γνώσεις**: Βασικός προγραμματισμός Java και εξοικείωση με Maven.

## Setting Up GroupDocs.Search for Java
Για να ξεκινήσετε, ενσωματώστε το GroupDocs.Search στο έργο σας χρησιμοποιώντας Maven:

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

Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
Για να δοκιμάσετε το GroupDocs.Search:

- **Δωρεάν δοκιμή** – δοκιμάστε τις βασικές λειτουργίες χωρίς δέσμευση.  
- **Προσωρινή άδεια** – εκτεταμένη πρόσβαση για ανάπτυξη.  
- **Αγορά** – πλήρης άδεια για χρήση σε παραγωγή.

### Basic Initialization and Setup
Δημιουργήστε ένα ευρετήριο στον φάκελο όπου θέλετε να αποθηκευτούν τα δεδομένα αναζήτησης:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## How to add documents to index
Τώρα που υπάρχει το ευρετήριο, το επόμενο λογικό βήμα είναι η **προσθήκη εγγράφων στο ευρετήριο** από τις τοποθεσίες όπου αποθηκεύονται τα αρχεία σας.

### 1. Creating an Index
**Επισκόπηση**: Ρυθμίστε έναν κατάλογο για το ευρετήριο αναζήτησης.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Adding Documents to Index
**Επισκόπηση**: Φέρτε αρχεία από πολλούς φακέλους προέλευσης.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Configuring Search Options for Chunk Search
Ενεργοποιήστε την αναζήτηση βασισμένη σε τμήματα ρυθμίζοντας το αντικείμενο επιλογών.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Performing Initial Chunk‑Based Search
Εκτελέστε το πρώτο ερώτημα χρησιμοποιώντας τις επιλογές με ενεργοποιημένα τμήματα.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Continuing Chunk‑Based Search
Επαναλάβετε μέσω των υπόλοιπων τμημάτων μέχρι να ολοκληρωθεί η αναζήτηση.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Why use chunk‑based search?
Η αναζήτηση βασισμένη σε τμήματα χωρίζει τεράστιες συλλογές εγγράφων σε διαχειρίσιμα κομμάτια, μειώνοντας την πίεση στη μνήμη και επιταχύνοντας τους χρόνους απόκρισης. Είναι ιδιαίτερα ωφέλιμη όταν:

1. **Οι νομικές ομάδες** χρειάζονται να εντοπίσουν συγκεκριμένες ρήτρες σε χιλιάδες συμβόλαια.  
2. **Οι πύλες εξυπηρέτησης πελατών** πρέπει να εμφανίζουν σχετικά άρθρα βάσης γνώσεων άμεσα.  
3. **Οι ερευνητές** διασχίζουν εκτεταμένα σύνολα δεδομένων χωρίς να φορτώνουν ολόκληρα αρχεία στη μνήμη.

## How this approach **increases search performance**
Αναζητώντας μικρότερα τμήματα αντί ολόκληρων αρχείων, η μηχανή μπορεί:

- Να παραλείπει άσχετες ενότητες νωρίς, μειώνοντας τους κύκλους CPU.  
- Να διατηρεί μόνο το ενεργό τμήμα στη μνήμη, κάτι που μειώνει άμεσα την κατανάλωση **java search index memory**.  
- Να παράλληλο επεξεργάζεται τα τμήματα σε πολυπύρηνες μηχανές για ταχύτερα αποτελέσματα.

## Managing **java search index memory**
Ενώ η αναζήτηση βασισμένη σε τμήματα μειώνει ήδη το αποτύπωμα μνήμης, μπορείτε να ρυθμίσετε περαιτέρω το JVM:

- Κατανείμετε επαρκή heap (`-Xmx2g` ή μεγαλύτερο) ανάλογα με το μέγεθος του ευρετηρίου.  
- Χρησιμοποιήστε `index.optimize()` μετά από μαζικές προσθήκες για συμπίεση της δομής του ευρετηρίου.  
- Παρακολουθήστε τις παύσεις GC με εργαλεία όπως το VisualVM για να αποφύγετε αιχμές καθυστέρησης.

## Performance Considerations
- **Διαχείριση μνήμης** – Κατανείμετε επαρκή χώρο heap (`-Xmx`) για μεγάλα ευρετήρια.  
- **Παρακολούθηση πόρων** – Παρακολουθείτε τη χρήση CPU κατά τη διάρκεια της ευρετηρίασης και των λειτουργιών αναζήτησης.  
- **Συντήρηση ευρετηρίου** – Επανακατασκευάστε ή καθαρίστε περιοδικά το ευρετήριο για να απορρίψετε παλαιά δεδομένα.

## Common Pitfalls & Troubleshooting
| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|-----------------|----------|
| `OutOfMemoryError` κατά την ευρετηρίαση | Το μέγεθος heap είναι πολύ μικρό | Αυξήστε το heap του JVM (`-Xmx2g` ή μεγαλύτερο) |
| Δεν επιστρέχονται αποτελέσματα | Το token τμήματος δεν επεξεργάστηκε | Βεβαιωθείτε ότι ο βρόχος `while` εκτελείται μέχρι το `getNextChunkSearchToken()` να είναι `null` |
| Αργή απόδοση αναζήτησης | Το ευρετήριο δεν είναι βελτιστοποιημένο | Εκτελέστε `index.optimize()` μετά από μαζικές προσθήκες |

## Frequently Asked Questions

**Ε: Τι είναι η αναζήτηση βασισμένη σε τμήματα;**  
Η αναζήτηση βασισμένη σε τμήματα διαιρεί το σύνολο δεδομένων σε μικρότερα κομμάτια, επιτρέποντας αποδοτικά ερωτήματα σε μεγάλα όγκους δεδομένων χωρίς να φορτώνει ολόκληρα έγγραφα στη μνήμη.

**Ε: Πώς ενημερώνω το ευρετήριό μου με νέα αρχεία;**  
Απλώς καλέστε `index.add()` με τη διαδρομή προς τα νέα έγγραφα· το ευρετήριο θα τα ενσωματώσει αυτόματα.

**Ε: Μπορεί το GroupDocs.Search να διαχειριστεί διαφορετικές μορφές αρχείων;**  
Ναι, υποστηρίζει PDFs, DOCX, XLSX, PPTX και πολλές άλλες κοινές μορφές.

**Ε: Ποια είναι τα τυπικά εμπόδια στην απόδοση;**  
Οι περιορισμοί μνήμης και τα μη βελτιστοποιημένα ευρετήρια είναι τα πιο συνηθισμένα· κατανείμετε επαρκές heap και βελτιστοποιήστε τακτικά το ευρετήριο.

**Ε: Πού μπορώ να βρω πιο λεπτομερή τεκμηρίωση;**  
Επισκεφθείτε την επίσημη [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) για αναλυτικούς οδηγούς και αναφορές API.

**Ε: Λειτουργεί η αναζήτηση βασισμένη σε τμήματα με κρυπτογραφημένα PDFs;**  
Ναι, εφόσον παρέχετε τον κωδικό πρόσβασης μέσω του κατάλληλου υπερφορτωμένου API.

**Ε: Πώς μπορώ να παρακολουθήσω την πρόοδο της ευρετηρίασης;**  
Χρησιμοποιήστε το υπερφορτωμένο `Index.add()` που επιστρέφει ένα αντικείμενο `Progress` ή συνδέστε σε callbacks καταγραφής.

## Resources
- **Τεκμηρίωση**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Αναφορά API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Λήψη**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Δωρεάν υποστήριξη**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Προσωρινή άδεια**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Τελευταία ενημέρωση:** 2026-02-21  
**Δοκιμάστηκε με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs  

---