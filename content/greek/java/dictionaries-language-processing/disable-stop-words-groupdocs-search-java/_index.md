---
date: '2026-02-19'
description: Μάθετε πώς να απενεργοποιήσετε τις λέξεις‑σταματημα στην αναζήτηση και
  να προσθέσετε έγγραφα στο ευρετήριο με το GroupDocs.Search για Java, ενισχύοντας
  την ακρίβεια των ερωτημάτων.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 'Λέξεις-απόρριψης στην αναζήτηση: Προσθήκη εγγράφων στο ευρετήριο με το GroupDocs.Search
  Java'
type: docs
url: /el/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

 code block placeholders: they remain.

Now produce final content.# Λέξεις‑Στάσης στην Αναζήτηση: Προσθήκη Εγγράφων στο Ευρετήριο με το GroupDocs.Search Java

Αν χρειάζεστε να **προσθέσετε έγγραφα στο ευρετήριο** εξασφαλίζοντας ότι κανένας σημαντικός όρος—ιδιαίτερα οι συνηθισμένοι—δεν θα αγνοηθεί, βρίσκεστε στο σωστό μέρος. Σε αυτόν τον οδηγό θα σας δείξουμε πώς να **απενεργοποιήσετε τις stop words στην αναζήτηση** χρησιμοποιώντας το GroupDocs.Search για Java, ώστε κάθε token (ακόμη και “on”, “by”, ή “the”) να γίνεται αναζητήσιμο και τα αποτελέσματά σας να είναι πολύ πιο ακριβή.

## Quick Answers
- **Τι σημαίνει “add documents to index”;** Σημαίνει τη φόρτωση των αρχικών αρχείων σας σε ένα αναζητήσιμο ευρετήριο ώστε να μπορούν να ερωτηθούν αποδοτικά.  
- **Γιατί θα ήθελα να απενεργοποιήσω τις stop words;** Για να συμπεριλάβετε κοινές λέξεις (π.χ., “on”, “the”) στις αναζητήσεις όταν αυτοί οι όροι έχουν νόημα για τον τομέα σας.  
- **Ποια έκδοση της βιβλιοθήκης απαιτείται;** GroupDocs.Search for Java 25.4 ή νεότερη.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται μόνιμη άδεια για παραγωγή.  
- **Μπορώ να το χρησιμοποιήσω σε έργο Maven;** Ναι – απλώς προσθέστε το αποθετήριο και την εξάρτηση που φαίνονται παρακάτω.

## What are stop words in search and why might you want to disable them?
Οι stop words είναι συχνά όροι που πολλές μηχανές αναζήτησης φιλτράρουν αυτόματα για να επιταχύνουν τα ερωτήματα. Ενώ αυτό βελτιώνει την απόδοση για γενικές αναζητήσεις στο web, μπορεί να μειώσει την ακρίβεια σε εξειδικευμένους τομείς—νομικά συμβόλαια, καταλόγους e‑commerce ή τεχνικά εγχειρίδια—όπου λέξεις όπως “on”, “by”, ή “as” έχουν πραγματικό νόημα. Η απενεργοποίηση των stop words σας επιτρέπει να θεωρείτε κάθε λέξη σημαντική, διασφαλίζοντας ότι κανένα σχετικό έγγραφο δεν θα παραλειφθεί.

## How does adding documents to index work in GroupDocs.Search?
Όταν προσθέτετε έγγραφα, η βιβλιοθήκη διαβάζει κάθε αρχείο, το διαχωρίζει σε tokens και αποθηκεύει τα tokens σε μια βελτιστοποιημένη δομή δεδομένων (το ευρετήριο). Μόλις ευρετηριαστεί, η μηχανή μπορεί να ανακτήσει τα αντίστοιχα έγγραφα σε χιλιοστά του δευτερολέπτου, ακόμη και για μεγάλες συλλογές.

## Prerequisites

- **Απαιτούμενες Βιβλιοθήκες**: GroupDocs.Search for Java 25.4 (ή νεότερη).  
- **Περιβάλλον Ανάπτυξης**: IntelliJ IDEA, Eclipse ή οποιοδήποτε Java IDE προτιμάτε.  
- **Βασικές Γνώσεις**: Εξοικείωση με τη σύνταξη της Java και την έννοια του ευρετηρίου.

## Setting Up GroupDocs.Search for Java

### Maven Installation

Αν χρησιμοποιείτε Maven, προσθέστε το ακόλουθο στο `pom.xml` σας:

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

### Direct Download

Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### License Acquisition Steps
- **Δωρεάν Δοκιμή** – ξεκινήστε τη δοκιμή αμέσως.  
- **Προσωρινή Άδεια** – αποκτήστε ένα κλειδί περιορισμένου χρόνου για πλήρη λειτουργικότητα.  
- **Αγορά** – εξασφαλίστε μόνιμη άδεια για χρήση σε παραγωγή.

## Basic Initialization and Setup

Δημιουργήστε μια παρουσία του `IndexSettings` για να ελέγξετε τη συμπεριφορά του ευρετηρίου:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## How to disable stop words in search (Java)

Η παρακάτω γραμμή απενεργοποιεί το ενσωματωμένο φίλτρο stop‑word:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Παράμετροι*: Η `setUseStopWords` δέχεται μια boolean τιμή.  
*Σκοπός*: Εγγυάται ότι κάθε λέξη—συμπεριλαμβανομένων των κοινών stop words—είναι ευρετηριασμένη και αναζητήσιμη.

## How to add documents to index

### Ορισμός του Καταλόγου Εξόδου

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Καθορισμός του Καταλόγου Εγγράφων

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Τώρα κάθε αρχείο στο `YOUR_DOCUMENT_DIRECTORY` είναι **προστέθηκε στο ευρετήριο** και έτοιμο για ερωτήματα.

## Performing a Search Query

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Επειδή οι stop words είναι απενεργοποιημένες, ο όρος `"on"` θα ληφθεί υπόψη κατά την αναζήτηση, επιστρέφοντας αποτελέσματα που διαφορετικά θα αγνοούνταν.

## Practical Applications

1. **Αναζήτηση Εγγράφων Επιχειρήσεων** – Διασφαλίστε ότι η κρίσιμη ορολογία δεν φιλτράρεται.  
2. **Πλατφόρμες Ηλεκτρονικού Εμπορίου** – Βελτιώστε την ανακάλυψη προϊόντων ευρετηριάζοντας κάθε λέξη στις περιγραφές των προϊόντων.  
3. **Εργαλεία Νομικής Έρευνας** – Καταγράψτε κάθε νομικό όρο, ακόμη και αυτούς που συνήθως θεωρούνται stop words.

## Performance Considerations

- **Συμβουλές Βελτιστοποίησης**: Ενημερώνετε και καθαρίζετε τακτικά το ευρετήριο σας για να διατηρείτε υψηλή ταχύτητα αναζήτησης.  
- **Χρήση Πόρων**: Παρακολουθείτε το μέγεθος του heap της JVM· μεγάλα ευρετήρια μπορεί να απαιτούν ρύθμιση των ρυθμίσεων garbage collection.  
- **Διαχείριση Μνήμης Java**: Χρησιμοποιήστε αποδοτικές δομές δεδομένων και σκεφτείτε αποθήκευση εκτός heap για πολύ μεγάλα corpora.

## Common Issues and Solutions

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|---|---|---|
| Δεν υπάρχουν αποτελέσματα για κοινές λέξεις | `setUseStopWords(true)` (προεπιλογή) | Καλέστε `setUseStopWords(false)` όπως φαίνεται παραπάνω. |
| Σφάλματα out‑of‑memory κατά την ευρετηρίαση | Ευρετηρίαση πάρα πολλών μεγάλων αρχείων ταυτόχρονα | Ευρετηριάστε τα αρχεία σε παρτίδες· αυξήστε την επιλογή JVM `-Xmx`. |
| Η αναζήτηση επιστρέφει παλιά δεδομένα | Το ευρετήριο δεν έχει ενημερωθεί μετά την προσθήκη νέων αρχείων | Καλέστε `index.update()` ή προσθέστε ξανά τα τροποποιημένα έγγραφα. |

## Frequently Asked Questions

**Q: What are stop words?**  
A: Οι stop words είναι κοινές λέξεις (π.χ., “the”, “is”, “on”) που πολλές μηχανές αναζήτησης αγνοούν για να επιταχύνουν τα ερωτήματα. Η απενεργοποίησή τους σας επιτρέπει να θεωρείτε κάθε token αναζητήσιμο.

**Q: Why disable stop words in search indexes?**  
A: Όταν απαιτείται ακριβής αντιστοίχιση φράσεων—όπως σε νομικά ή τεχνικά έγγραφα—κάθε λέξη έχει νόημα, επομένως πρέπει να συμπεριλαμβάνονται και οι stop words.

**Q: How does GroupDocs.Search handle large datasets?**  
A: Η βιβλιοθήκη χρησιμοποιεί βελτιστοποιημένες δομές δεδομένων και σταδιακή ευρετηρίαση για να διατηρεί τη χρήση μνήμης χαμηλή, ακόμη και με εκατομμύρια έγγραφα.

**Q: Can I integrate GroupDocs.Search with other Java applications?**  
A: Ναι, το API έχει σχεδιαστεί για εύκολη ενσωμάτωση σε οποιοδήποτε σύστημα βασισμένο σε Java, από web services μέχρι desktop εφαρμογές.

**Q: What should I do if my search results are not accurate?**  
A: Επαληθεύστε ότι το ευρετήριο περιλαμβάνει όλα τα απαιτούμενα έγγραφα (`add documents to index`), βεβαιωθείτε ότι το φιλτράρισμα stop‑word είναι απενεργοποιημένο εάν χρειάζεται, και σκεφτείτε την επανέκδοση του ευρετηρίου μετά από σημαντικές αλλαγές.

## Additional Resources

- **Τεκμηρίωση**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Αναφορά API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Λήψη**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **Αποθετήριο GitHub**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Δωρεάν Υποστήριξη**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Προσωρινή Άδεια**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Ακολουθώντας αυτόν τον οδηγό, τώρα γνωρίζετε πώς να **προσθέσετε έγγραφα στο ευρετήριο** και **να απενεργοποιήσετε τις stop words στην αναζήτηση** για να παρέχετε πιο ακριβή αποτελέσματα στις Java εφαρμογές σας.

---

**Τελευταία Ενημέρωση:** 2026-02-19  
**Δοκιμάστηκε Με:** GroupDocs.Search for Java 25.4  
**Συγγραφέας:** GroupDocs