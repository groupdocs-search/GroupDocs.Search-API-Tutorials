---
date: '2025-12-19'
description: Μάθετε πώς να προσθέτετε έγγραφα στο ευρετήριο και να ενεργοποιείτε την
  αναζήτηση με βάση τα τμήματα στην Java χρησιμοποιώντας το GroupDocs.Search, ενισχύοντας
  την απόδοση για μεγάλα σύνολα εγγράφων.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Προσθήκη εγγράφων στο ευρετήριο με αναζήτηση κατά τμήματα σε Java
type: docs
url: /el/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Προσθήκη εγγράφων στο ευρετήριο με αναζήτηση βάσει τμημάτων σε Java

## Τι θα μάθετε
- Πώς να δημιουργήσετε ένα ευρετήριο αναζήτησης σε συγκεκριμένο φάκελο.  
- Βήματα για **προσθήκη εγγράφων στο ευρετήριο** από πολλαπλές τοποθεσίες.  
- Διαμόρφωση επιλογών αναζήτησης για ενεργοποίηση της αναζήτησης βάσει τμημάτων.  
- Διενέργεια αρχικών και επόμενων αναζητήσεων βάσει τμημάτων.  
- Πραγματικά σενάρια όπου η αναζήτηση εγγράφων βάσει τμημάτων ξεχωρίζει.

## Γρήγορες Απαντήσεις
- **Ποιο είναι το πρώτο βήμα;** Δημιουργήστε έναν φάκελο ευρετηρίου αναζήτησης.  
- **Πώς μπορώ να συμπεριλάβω πολλά αρχεία;** Χρησιμοποιήστε `index.add()` για κάθε φάκελο εγγράφων.  
- **Ποια επιλογή ενεργοποιεί την αναζήτηση τμημάτων;** `options.setChunkSearch(true)`.  
- **Μπορώ να συνεχίσω την αναζήτηση μετά το πρώτο τμήμα;** Ναι, καλέστε `index.searchNext()` με το token.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή ή προσωρινή άδεια λειτουργεί για ανάπτυξη· απαιτείται πλήρης άδεια για παραγωγή.

## Προαπαιτούμενα
- **Απαιτούμενες βιβλιοθήκες**: GroupDocs.Search for Java 25.4 ή νεότερη.  
- **Ρύθμιση περιβάλλοντος**: Ένα συμβατό Java Development Kit (JDK) εγκατεστημένο.  
- **Προαπαιτούμενη γνώση**: Βασικός προγραμματισμός Java και εξοικείωση με Maven.

## Ρύθμιση του GroupDocs.Search για Java
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

### Απόκτηση Άδειας
Για να δοκιμάσετε το GroupDocs.Search:

- **Δωρεάν δοκιμή** – δοκιμάστε τις βασικές λειτουργίες χωρίς δέσμευση.  
- **Προσωρινή άδεια** – εκτεταμένη πρόσβαση για ανάπτυξη.  
- **Αγορά** – πλήρης άδεια για χρήση σε παραγωγή.

### Βασική Αρχικοποίηση και Ρύθμιση
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

## Πώς να προσθέσετε έγγραφα στο ευρετήριο
Τώρα που το ευρετήριο υπάρχει, το επόμενο λογικό βήμα είναι η **προσθήκη εγγράφων στο ευρετήριο** από τις τοποθεσίες όπου αποθηκεύονται τα αρχεία σας.

### 1. Δημιουργία Ευρετηρίου
**Επισκόπηση**: Ρυθμίστε έναν κατάλογο για το ευρετήριο αναζήτησης.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Προσθήκη Εγγράφων στο Ευρετήριο
**Επισκόπηση**: Φέρτε αρχεία από πολλαπλούς φακέλους προέλευσης.

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

### 3. Διαμόρφωση Επιλογών Αναζήτησης για Αναζήτηση Τμημάτων
Ενεργοποιήστε την αναζήτηση βάσει τμημάτων τροποποιώντας το αντικείμενο επιλογών.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Διενέργεια Αρχικής Αναζήτησης Βάσει Τμημάτων
Εκτελέστε το πρώτο ερώτημα χρησιμοποιώντας τις επιλογές με ενεργοποιημένη αναζήτηση τμημάτων.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Συνέχιση Αναζήτησης Βάσει Τμημάτων
Επαναλάβετε τη διαδικασία για τα υπόλοιπα τμήματα μέχρι η αναζήτηση να ολοκληρωθεί.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Γιατί να χρησιμοποιήσετε αναζήτηση βάσει τμημάτων;
Η αναζήτηση βάσει τμημάτων χωρίζει τεράστιες συλλογές εγγράφων σε διαχειρίσιμα κομμάτια, μειώνοντας την πίεση στη μνήμη και επιταχύνοντας τους χρόνους απόκρισης. Είναι ιδιαίτερα ωφέλιμη όταν:

1. **Νομικές ομάδες** χρειάζονται να εντοπίσουν συγκεκριμένες ρήτρες σε χιλιάδες συμβάσεις.  
2. **Πύλες εξυπηρέτησης πελατών** πρέπει να εμφανίζουν σχετικά άρθρα βάσης γνώσεων άμεσα.  
3. **Ερευνητές** διασχίζουν εκτενείς σύνολα δεδομένων χωρίς να φορτώνουν ολόκληρα αρχεία στη μνήμη.

## Σκέψεις για την Απόδοση
- **Διαχείριση μνήμης** – Κατανείμετε επαρκή χώρο heap (`-Xmx`) για μεγάλα ευρετήρια.  
- **Παρακολούθηση πόρων** – Παρακολουθείτε τη χρήση CPU κατά τη διάρκεια της δημιουργίας ευρετηρίου και των λειτουργιών αναζήτησης.  
- **Συντήρηση ευρετηρίου** – Επανακατασκευάστε ή καθαρίστε περιοδικά το ευρετήριο για την απομάκρυνση παλαιών δεδομένων.

## Συνηθισμένα Προβλήματα & Επίλυση
| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| `OutOfMemoryError` during indexing | Heap size too low | Increase JVM heap (`-Xmx2g` or higher) |
| No results returned | Chunk token not processed | Ensure the `while` loop runs until `getNextChunkSearchToken()` is `null` |
| Slow search performance | Index not optimized | Run `index.optimize()` after bulk additions |

## Συχνές Ερωτήσεις

**Q: Τι είναι η αναζήτηση βάσει τμημάτων;**  
A: Η αναζήτηση βάσει τμημάτων διαιρεί το σύνολο δεδομένων σε μικρότερα κομμάτια, επιτρέποντας αποδοτικά ερωτήματα σε μεγάλους όγκους δεδομένων χωρίς να φορτώνει ολόκληρα έγγραφα στη μνήμη.

**Q: Πώς ενημερώνω το ευρετήριο με νέα αρχεία;**  
A: Απλώς καλέστε `index.add()` με τη διαδρομή προς τα νέα έγγραφα· το ευρετήριο θα τα ενσωματώσει αυτόματα.

**Q: Μπορεί το GroupDocs.Search να διαχειριστεί διαφορετικές μορφές αρχείων;**  
A: Ναι, υποστηρίζει PDFs, DOCX, XLSX, PPTX και πολλές άλλες κοινές μορφές.

**Q: Ποια είναι τα τυπικά bottlenecks απόδοσης;**  
A: Περιορισμοί μνήμης και μη βελτιστοποιημένα ευρετήρια είναι τα πιο συχνά· κατανείμετε επαρκή heap και βελτιστοποιείτε τακτικά το ευρετήριο.

**Q: Πού μπορώ να βρω πιο λεπτομερή τεκμηρίωση;**  
A: Επισκεφθείτε την επίσημη [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) για εκτενείς οδηγούς και αναφορές API.

## Πόροι
- **Documentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2025-12-19  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs