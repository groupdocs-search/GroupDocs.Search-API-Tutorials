---
date: '2026-10-12'
description: Μάθετε πώς να δημιουργήσετε ευρετήριο και να εκτελέσετε αναζήτηση regex
  java χρησιμοποιώντας το GroupDocs.Search for Java, καλύπτοντας τη ρύθμιση, την προσθήκη
  εγγράφων στο ευρετήριο, fuzzy, wildcard και regex queries.
keywords:
- how to create index
- regex search java
- how to add documents
- fuzzy search java
- java search library
lastmod: '2026-10-12'
og_description: Πώς να δημιουργήσετε ευρετήριο με το GroupDocs.Search for Java. Ανακαλύψτε
  την αναζήτηση regex java, προσθέστε έγγραφα στο ευρετήριο και χρησιμοποιήστε fuzzy
  ή wildcard queries σε λίγα βήματα.
og_image_alt: Guide to creating a searchable index with GroupDocs.Search for Java
og_title: Πώς να δημιουργήσετε ευρετήριο με το GroupDocs.Search for Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: Learn how to create index and perform regex search java using GroupDocs.Search
    for Java, covering setup, adding documents to index, fuzzy, wildcard, and regex
    queries.
  headline: How to create index with GroupDocs.Search for Java
  type: TechArticle
- questions:
  - answer: Yes—use `index.add()` to append new files or `index.update()` to refresh
      changed documents.
    question: Can I update an existing index without rebuilding it from scratch?
  - answer: The built‑in fuzzy algorithm works on Unicode characters, so it supports
      most languages out of the box.
    question: How does fuzzy search handle different languages?
  - answer: Practically, the limit is governed by available disk space and JVM memory;
      the library is designed for millions of documents.
    question: Is there a limit to the number of documents I can index?
  - answer: No—search options are applied per query, so you can adjust them on the
      fly.
    question: Do I need to restart the application after changing search options?
  - answer: The official GroupDocs.Search documentation and API reference provide
      extensive examples for complex scenarios.
    question: Where can I find more advanced query examples?
  type: FAQPage
tags:
- GroupDocs.Search
- Java indexing
- document search
- regex search
- fuzzy search
title: Πώς να δημιουργήσετε ευρετήριο με το GroupDocs.Search for Java
type: docs
url: /el/java/document-management/mastering-groupdocs-search-java-index-management-guide/
weight: 1
---

# Πώς να δημιουργήσετε ευρετήριο με το GroupDocs.Search για Java

Αν χρειάζεστε **πώς να δημιουργήσετε ευρετήριο** για χιλιάδες νομικά, ακαδημαϊκά ή επιχειρηματικά αρχεία, το GroupDocs.Search για Java σας παρέχει μια έτοιμη μηχανή που εξάγει κείμενο, δημιουργεί μια συμπαγή δομή αναζήτησης και σας επιτρέπει να εκτελείτε ερωτήματα regex, fuzzy ή wildcard σε χιλιοστά του δευτερολέπτου. Σε αυτό το tutorial θα δείτε πώς να ρυθμίσετε το SDK, να δημιουργήσετε ένα ευρετήριο, να προσθέσετε έγγραφα σε αυτό και να εκτελέσετε ισχυρές αναζητήσεις βασισμένες σε μοτίβα.

## Γρήγορες απαντήσεις
- **Ποιος είναι ο κύριος σκοπός του GroupDocs.Search;** Να δημιουργεί αναζητήσιμα ευρετήρια για ένα ευρύ φάσμα μορφών εγγράφων.  
- **Μπορώ να προσθέσω έγγραφα στο ευρετήριο μετά τη δημιουργία του;** Ναι—χρησιμοποιήστε τη μέθοδο `index.add()` για να συμπεριλάβετε νέα αρχεία.  
- **Υποστηρίζει το GroupDocs.Search fuzzy αναζήτηση σε Java;** Απολύτως· ενεργοποιήστε την μέσω `SearchOptions`.  
- **Πώς εκτελώ ένα ερώτημα wildcard σε Java;** Δημιουργήστε το με `SearchQuery.createWildcardQuery()`.  
- **Απαιτείται άδεια για παραγωγική χρήση;** Απαιτείται έγκυρη άδεια GroupDocs.Search για εμπορικές εγκαταστάσεις.

Το `SearchOptions` ρυθμίζει τη συμπεριφορά της αναζήτησης, όπως το fuzzy matching.  
Το `SearchQuery.createWildcardQuery()` δημιουργεί ένα αντικείμενο ερωτήματος wildcard.

## Τι σημαίνει «πώς να δημιουργήσετε ευρετήριο» στο πλαίσιο του GroupDocs.Search;
Η δημιουργία ενός ευρετηρίου σημαίνει σάρωση ενός ή περισσότερων πηγαίων εγγράφων, εξαγωγή αναζητήσιμου κειμένου και αποθήκευση αυτών των πληροφοριών σε μια δομημένη μορφή που μπορεί να ερωτηθεί αποδοτικά. Αυτή η διαδικασία δημιουργεί μια συμπαγή δομή δεδομένων στο δίσκο που επιτρέπει εξαιρετικά γρήγορες αναζητήσεις σε χιλιάδες αρχεία, ακόμη και όταν τα αρχικά έγγραφα είναι μεγάλα ή αποθηκευμένα σε διαφορετικές μορφές.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για Java;
Το GroupDocs.Search προσφέρει μια αποδεδειγμένη, επιχειρηματικού επιπέδου λύση που υποστηρίζει **πάνω από 30 μορφές εισόδου και εξόδου**—συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX, HTML και αρχείων απλού κειμένου—ενώ παρέχει χρόνους απόκρισης ερωτημάτων κάτω από ένα δευτερόλεπτο για ευρετήρια που περιέχουν εκατομμύρια σελίδες. Οι ενσωματωμένες δυνατότητες fuzzy, wildcard και **regex search java** σας επιτρέπουν να διαχειρίζεστε ορθογραφικά λάθη, αντιστοίχιση μοτίβων και σύνθετα σενάρια αναζήτησης χωρίς να γράφετε προσαρμοσμένους αναλυτές.

## Προαπαιτούμενα
- Έκδοση GroupDocs.Search for Java 25.4 ή νεότερη.  
- Ένα IDE όπως IntelliJ IDEA ή Eclipse με υποστήριξη Maven.  
- JDK 11 ή νεότερο εγκατεστημένο στο μηχάνημά σας.  
- Βασικές γνώσεις σύνταξης Java και εννοιών αναζήτησης.

## Ρύθμιση του GroupDocs.Search για Java

Μπορείτε να προσθέσετε τη βιβλιοθήκη μέσω Maven ή να την κατεβάσετε χειροκίνητα.

**Ρύθμιση Maven**

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

**Άμεση λήψη**  
Εναλλακτικά, κατεβάστε την τελευταία έκδοση από [GroupDocs.Search για Java εκδόσεις](https://releases.groupdocs.com/search/java/).

### Απόκτηση άδειας
- **Δωρεάν δοκιμή:** Εξερευνήστε όλες τις λειτουργίες χωρίς κόστος.  
- **Προσωρινή άδεια:** Επεκτείνετε τη δοκιμή για έργα αξιολόγησης.  
- **Πλήρης άδεια:** Απαιτείται για παραγωγικές εγκαταστάσεις και για την άνοιξη απεριόριστης δημιουργίας ευρετηρίων.

Μόλις η βιβλιοθήκη είναι διαθέσιμη, αρχικοποιήστε την στον κώδικα Java:

```java
import com.groupdocs.search.*;

public class InitializeSearch {
    public static void main(String[] args) {
        // Create an index instance
        Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Πώς να δημιουργήσετε ευρετήριο με το GroupDocs.Search

Φορτώστε τα πηγαία αρχεία σας, δείξτε το SDK σε έναν φάκελο και αφήστε το να δημιουργήσει τη δομή αναζήτησης με μία κλήση. Αυτή η προσέγγιση δημιουργεί το ευρετήριο σε λιγότερο από ένα λεπτό για μια τυπική συλλογή εγγράφων 10 GB σε έναν τυπικό διακομιστή.

### Ορισμός διαδρομών

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\CreateAndIndexDocuments";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```

### Δημιουργία του ευρετηρίου

```java
Index index = new Index(indexFolder);
System.out.println("Index created at: " + indexFolder);
```

### Προσθήκη εγγράφων στο ευρετήριο

```java
index.add(documentsFolder);
System.out.println("Documents added to the index.");
```

> **Συμβουλή:** Βεβαιωθείτε ότι οι κατάλογοι υπάρχουν και περιέχουν μόνο τα αρχεία που θέλετε να είναι αναζητήσιμα· άσχετα αρχεία μπορούν να αυξήσουν το μέγεθος του ευρετηρίου.

## Απλό ερώτημα λέξης με επιλογές fuzzy αναζήτησης (fuzzy search java)

Η fuzzy αναζήτηση βοηθά όταν οι χρήστες πληκτρολογούν λανθασμένα μια λέξη ή όταν το OCR εισάγει σφάλματα. Το SDK αυτόματα επεκτείνει το ερώτημα ώστε να περιλαμβάνει παρόμοιους όρους βάσει της απόστασης επεξεργασίας.

```java
SearchQuery subquery = SearchQuery.createWordQuery("future");
```

```java
subquery.setSearchOptions(new SearchOptions());
subquery.getSearchOptions().getFuzzySearch().setEnabled(true);
subquery.getSearchOptions().getFuzzySearch()
        .setFuzzyAlgorithm(new TableDiscreteFunction(3));
System.out.println("Fuzzy search enabled with a tolerance of 3.");
```

## Ερώτημα μπαλαντέρ Java

Τα ερωτήματα μπαλαντέρ σας επιτρέπουν να ταιριάζετε μοτίβα όπως οποιαδήποτε λέξη που αρχίζει με συγκεκριμένο πρόθεμα, χρησιμοποιώντας τους χαρακτήρες `*` ή `?`.

`SearchQuery.createWildcardQuery()` δημιουργεί ένα αντικείμενο ερωτήματος μπαλαντέρ.

```java
SearchQuery subquery = SearchQuery.createWildcardQuery(1);
System.out.println("Wildcard query created.");
```

## Αναζήτηση regex Java

Οι κανονικές εκφράσεις σας δίνουν λεπτομερή έλεγχο της αντιστοίχισης μοτίβων, ιδανικό για την εύρεση επαναλαμβανόμενων χαρακτήρων ή σύνθετων δομών token.

`SearchQuery.createRegexQuery()` δημιουργεί ένα αντικείμενο ερωτήματος regex για αντιστοίχιση μοτίβου.

```java
SearchQuery subquery = SearchQuery.createRegexQuery("(.)\\1");
System.out.println("Regex query created to find repeated characters.");
```

## Συνδυασμός υποερωτημάτων σε ερώτημα φράσης

Μπορείτε να συνδυάσετε υποερωτήματα λέξης, μπαλαντέρ και regex για να δημιουργήσετε σύνθετες αναζητήσεις φράσεων που σέβονται τη σειρά και την εγγύτητα.

```java
SearchQuery subquery1 = SearchQuery.createWordQuery("future");
SearchQuery subquery2 = SearchQuery.createWildcardQuery(1);
SearchQuery subquery3 = SearchQuery.createRegexQuery("(.)\\1");
```

```java
SearchQuery combinedQuery = SearchQuery.createPhraseSearchQuery(subquery1, subquery2, subquery3);
System.out.println("Combined phrase search query created.");
```

## Διαμόρφωση και εκτέλεση αναζήτησης με προσαρμοσμένες επιλογές

Η προσαρμογή των επιλογών αναζήτησης σας επιτρέπει να ελέγχετε πόσες εμφανίσεις επιστρέφονται, κάτι που είναι χρήσιμο για μεγάλα σώματα κειμένου. Μπορείτε επίσης να ρυθμίσετε την βαθμολόγηση, να επισημάνετε τα αποτελέσματα και να περιορίσετε τα αποτελέσματα ανά έγγραφο.

```java
SearchOptions options = new SearchOptions();
options.setMaxOccurrenceCountPerTerm(1000000);
options.setMaxTotalOccurrenceCount(10000000);
System.out.println("Custom search options configured.");
```

```java
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\ConfigureAndPerformSearch");
SearchQuery query = SearchQuery.createWordQuery("future");

SearchResult result = index.search(query, options);
System.out.println("Search performed with custom options.");
```

## Αναζήτηση regex java – κοινές περιπτώσεις χρήσης
- **Νομική έρευνα:** Εντοπίστε ρήτρες που ακολουθούν συγκεκριμένο μοτίβο, όπως ημερομηνίες μορφοποιημένες ως `DD/MM/YYYY`.  
- **Επαλήθευση δεδομένων:** Ανιχνεύστε εσφαλμένα αναγνωριστικά ή επαναλαμβανόμενους χαρακτήρες στα αρχεία καταγραφής.  
- **Διαχείριση περιεχομένου:** Βρείτε βωμολοχίες ή απαγορευμένα μοτίβα χρησιμοποιώντας regex.  
- **Οικονομική ανάλυση:** Εξάγετε κωδικούς συναλλαγών που ταιριάζουν σε γνωστό πρότυπο regex.

## Παράγοντες απόδοσης
- **Βελτιστοποίηση ευρετηρίου:** Επανα‑ευρετηρίαση περιοδικά και αφαίρεση παλαιών αρχείων για να διατηρείται το ευρετήριο ελαφρύ· ένα καλά συντηρημένο ευρετήριο 1 εκατομμυρίου σελίδων καταλαμβάνει λιγότερο από 2 GB στο δίσκο.  
- **Χρήση πόρων:** Παρακολουθήστε το μέγεθος της μνήμης heap της JVM· μεγάλα ευρετήρια μπορεί να απαιτούν έως 8 GB heap ή αποθήκευση εκτός heap για βέλτιστη απόδοση.  
- **Συλλογή απορριμμάτων:** Ρυθμίστε τις ρυθμίσεις GC (π.χ., G1GC) για υπηρεσίες αναζήτησης μακράς διάρκειας ώστε να αποφεύγετε αιχμές χρόνου παύσης.

## Συχνές ερωτήσεις
**Q: Μπορώ να ενημερώσω ένα υπάρχον ευρετήριο χωρίς να το ξαναχτίσω από την αρχή;**  
A: Ναι—χρησιμοποιήστε `index.add()` για να προσθέσετε νέα αρχεία ή `index.update()` για να ενημερώσετε τα τροποποιημένα έγγραφα.

**Q: Πώς η fuzzy αναζήτηση διαχειρίζεται διαφορετικές γλώσσες;**  
A: Ο ενσωματωμένος αλγόριθμος fuzzy λειτουργεί με χαρακτήρες Unicode, επομένως υποστηρίζει τις περισσότερες γλώσσες αμέσως.

**Q: Υπάρχει όριο στον αριθμό των εγγράφων που μπορώ να ευρετηριάσω;**  
A: Στην πράξη, το όριο καθορίζεται από τον διαθέσιμο χώρο στο δίσκο και τη μνήμη της JVM· η βιβλιοθήκη έχει σχεδιαστεί για εκατομμύρια έγγραφα.

**Q: Πρέπει να επανεκκινήσω την εφαρμογή μετά την αλλαγή των επιλογών αναζήτησης;**  
A: Όχι—οι επιλογές αναζήτησης εφαρμόζονται ανά ερώτημα, έτσι μπορείτε να τις προσαρμόζετε άμεσα.

**Q: Πού μπορώ να βρω πιο προχωρημένα παραδείγματα ερωτημάτων;**  
A: Η επίσημη τεκμηρίωση του GroupDocs.Search και η αναφορά API παρέχουν εκτενή παραδείγματα για σύνθετα σενάρια.

---

**Τελευταία ενημέρωση:** 2026-10-12  
**Δοκιμάστηκε με:** GroupDocs.Search for Java 25.4  
**Συγγραφέας:** GroupDocs

## Σχετικά μαθήματα

- [Πώς να δημιουργήσετε ευρετήριο εγγράφων και να προσθέσετε έγγραφα χρησιμοποιώντας το GroupDocs.Search API για Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Java Fuzzy Search: Προσθήκη εγγράφων στο ευρετήριο με το GroupDocs.Search](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)
- [Πώς να προσθέσετε πολλαπλά ψευδώνυμα και να προσθέσετε έγγραφα στο ευρετήριο στο GroupDocs.Search για Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)