---
date: '2026-08-10'
description: Μάθετε πώς να δημιουργήσετε searchable index java και να ενεργοποιήσετε
  case‑sensitive search με GroupDocs.Search, βελτιώνοντας την ακρίβεια για εφαρμογές
  Java.
keywords:
- create searchable index java
- case sensitive search java
- groupdocs search java tutorial
- java text query search
lastmod: '2026-08-10'
og_description: Μάθετε πώς να δημιουργήσετε searchable index java και να ενεργοποιήσετε
  case‑sensitive search με GroupDocs.Search. Οδηγός βήμα‑βήμα για προγραμματιστές
  Java.
og_image_alt: Guide to creating a searchable index in Java using GroupDocs with case‑sensitive
  search
og_title: 'Δημιουργία searchable index java: προσθήκη εγγράφων case‑sensitive search'
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to create searchable index java and enable case‑sensitive
    search with GroupDocs.Search, boosting accuracy for Java applications.
  headline: 'Create searchable index java: add docs case‑sensitive search'
  type: TechArticle
- description: Learn how to create searchable index java and enable case‑sensitive
    search with GroupDocs.Search, boosting accuracy for Java applications.
  name: 'Create searchable index java: add docs case‑sensitive search'
  steps:
  - name: create an index and add your documents
    text: The `Index` class represents a searchable storage area on disk where documents
      are indexed. > **Pro tip:** You can call `index.add()` multiple times to **search
      across multiple directories** in a single index.
  - name: enable case‑sensitive search
    text: '`SearchOptions` configures how queries are processed, including case sensitivity
      and other search behaviors.'
  - name: execute a case‑sensitive text query
    text: '`SearchQuery` builds the query object that the engine evaluates against
      the index. The loop prints the full path of each document that contains the
      exact case‑matched term.'
  - name: initialize a second index (optional)
    text: A second `Index` instance can be created to isolate object‑based searches
      from plain‑text searches.
  - name: re‑use the case‑sensitive option
    text: '`SearchOptions` can be reused across different query types to maintain
      consistent case handling.'
  - name: build and run an object query
    text: '`WordQuery` represents a word‑level search that can be combined with other
      query types for complex searches. Using `createWordQuery` lets you later combine
      it with phrase, wildcard, or Boolean queries for more complex scenarios.'
  type: HowTo
- questions:
  - answer: Add documents to an index with `index.add(...)`.
    question: What is the primary step to start searching?
  - answer: Set `options.setUseCaseSensitiveSearch(true)`.
    question: How do you enable case‑sensitive search?
  - answer: Yes – call `index.add()` for each folder you want to include.
    question: Can you search across multiple directories?
  - answer: Use `SearchQuery.createWordQuery(...)`.
    question: Which method lets you search with objects?
  - answer: A temporary license is available for trial purposes.
    question: Do you need a license for testing?
  type: FAQPage
tags:
- create searchable index
- case-sensitive search
- groupdocs search
- java document processing
title: 'Δημιουργία searchable index java: προσθήκη εγγράφων case‑sensitive search'
type: docs
url: /el/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Δημιουργία ευρετηρίου αναζήτησης java: προσθήκη εγγράφων με διάκριση πεζών-κεφαλαίων

Σε σύγχρονες εφαρμογές Java, **creating a searchable index java** είναι το θεμέλιο για γρήγορη, ακριβή ανάκτηση πληροφοριών από μεγάλες συλλογές εγγράφων. Αυτό το tutorial δείχνει πώς να προσθέσετε έγγραφα σε ένα ευρετήριο, να ενεργοποιήσετε την αναζήτηση με διάκριση πεζών-κεφαλαίων και να βελτιώσετε τη διαδικασία με το GroupDocs.Search. Είτε δημιουργείτε ένα νομικό αποθετήριο, έναν κατάλογο e‑commerce ή ένα σύστημα διαχείρισης περιεχομένου, αυτά τα βήματα θα σας βοηθήσουν να παρέχετε ακριβή αποτελέσματα που ικανοποιούν τους χρήστες.

## Γρήγορες απαντήσεις
- **Ποιο είναι το κύριο βήμα για να ξεκινήσετε την αναζήτηση;** Add documents to an index with `index.add(...)`.  
- **Πώς ενεργοποιείτε την αναζήτηση με διάκριση πεζών-κεφαλαίων;** Set `options.setUseCaseSensitiveSearch(true)`.  
- **Μπορείτε να αναζητήσετε σε πολλαπλούς καταλόγους;** Yes – call `index.add()` for each folder you want to include.  
- **Ποια μέθοδος σας επιτρέπει να αναζητήσετε με αντικείμενα;** Use `SearchQuery.createWordQuery(...)`.  
- **Χρειάζεστε άδεια για δοκιμές;** A temporary license is available for trial purposes.

## Τι σημαίνει η “add documents to index”;
Η προσθήκη εγγράφων σε ένα ευρετήριο σημαίνει την τροφοδότηση των αρχείων πηγής (PDF, έγγραφα Word, απλό κείμενο κ.λπ.) στο GroupDocs.Search ώστε να δημιουργήσει μια δομή δεδομένων αναζήτησης. Το ευρετήριο αποθηκεύει διαχωρισμένους όρους, θέσεις και μεταδεδομένα, επιτρέποντας στη μηχανή να εκτελεί γρήγορα ερωτήματα, συμπεριλαμβανομένων αυτών με διάκριση πεζών-κεφαλαίων, και να ταξινομεί αποτελέσματα αποδοτικά.

## Γιατί να ενεργοποιήσετε την αναζήτηση με διάκριση πεζών-κεφαλαίων σε Java;
Η ενεργοποίηση της αναζήτησης με διάκριση πεζών-κεφαλαίων διασφαλίζει ότι η μηχανή διακρίνει μεταξύ όρων που διαφέρουν μόνο στην πεζοκεφαλαία, κάτι που είναι κρίσιμο για τομείς όπου η κεφαλαία γράμματα έχουν σημασία. Επιτρέπει ακριβή αντιστοίχιση όρων, υποστηρίζει απαιτήσεις συμμόρφωσης με κανονισμούς και βελτιώνει τη συνάφεια επιστρέφοντας αποτελέσματα που ταιριάζουν ακριβώς με την πεζοκεφαλαία του ερωτήματος του χρήστη.

- **Ακριβής αντιστοίχιση όρων** – π.χ., “Apple” (εταιρεία) vs. “apple” (φρούτο).  
- **Συμμόρφωση με κανονισμούς** – πολλές βιομηχανίες απαιτούν ακριβή αντιστοίχιση φράσεων.  
- **Βελτιωμένη συνάφεια** – τεχνικοί και νομικοί χρήστες συχνά αναμένουν αποτελέσματα με συγκεκριμένη πεζοκεφαλαία.

## Προαπαιτούμενα
- JDK 17 ή νεότερο (συνιστάται)  
- Maven για διαχείριση εξαρτήσεων  
- IDE όπως IntelliJ IDEA ή Eclipse  
- Βασική εξοικείωση με προγραμματισμό Java  

## Ρύθμιση του GroupDocs.Search για Java
Το παρακάτω απόσπασμα Maven προσθέτει το αποθετήριο GroupDocs.Search και την απαιτούμενη εξάρτηση στο έργο σας.

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

Εναλλακτικά, μπορείτε να κατεβάσετε την πιο πρόσφατη έκδοση απευθείας από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Άδεια
Για να ξεκινήσετε με μια δοκιμαστική έκδοση, επισκεφθείτε το GroupDocs για να αποκτήσετε προσωρινή άδεια. Αυτό θα σας επιτρέψει να δοκιμάσετε όλες τις λειτουργίες χωρίς περιορισμούς.

## Πώς να δημιουργήσετε ευρετήριο αναζήτησης java – αναζήτηση κειμένου

### Βήμα 1: δημιουργήστε ένα ευρετήριο και προσθέστε τα έγγραφά σας
Η κλάση `Index` αντιπροσωπεύει μια αποθηκευτική περιοχή αναζήτησης στον δίσκο όπου τα έγγραφα ευρετηριάζονται.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Συμβουλή:** Μπορείτε να καλέσετε `index.add()` πολλές φορές για **αναζήτηση σε πολλαπλούς καταλόγους** σε ένα ενιαίο ευρετήριο.

### Βήμα 2: ενεργοποιήστε την αναζήτηση με διάκριση πεζών-κεφαλαίων
`SearchOptions` ρυθμίζει πώς επεξεργάζονται τα ερωτήματα, συμπεριλαμβανομένης της διάκρισης πεζών-κεφαλαίων και άλλων συμπεριφορών αναζήτησης.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Βήμα 3: εκτελέστε ένα ερώτημα κειμένου με διάκριση πεζών-κεφαλαίων
`SearchQuery` δημιουργεί το αντικείμενο ερωτήματος που η μηχανή αξιολογεί έναντι του ευρετηρίου.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Ο βρόχος εκτυπώνει τη πλήρη διαδρομή κάθε εγγράφου που περιέχει τον ακριβή όρο με τη σωστή πεζοκεφαλαία.

## Πώς να δημιουργήσετε ευρετήριο αναζήτησης java – αναζήτηση με αντικείμενα

### Βήμα 1: αρχικοποιήστε ένα δεύτερο ευρετήριο (προαιρετικό)
Ένα δεύτερο αντικείμενο `Index` μπορεί να δημιουργηθεί για να απομονώσει τις αναζητήσεις με αντικείμενα από τις αναζητήσεις απλού κειμένου.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Βήμα 2: επαναχρησιμοποιήστε την επιλογή διάκρισης πεζών-κεφαλαίων
`SearchOptions` μπορεί να επαναχρησιμοποιηθεί σε διαφορετικούς τύπους ερωτημάτων για να διατηρηθεί η συνεπής διαχείριση πεζοκεφαλαίων.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Βήμα 3: δημιουργήστε και εκτελέστε ένα ερώτημα αντικειμένου
`WordQuery` αντιπροσωπεύει μια αναζήτηση επιπέδου λέξης που μπορεί να συνδυαστεί με άλλους τύπους ερωτημάτων για σύνθετες αναζητήσεις.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Η χρήση του `createWordQuery` σας επιτρέπει να το συνδυάσετε αργότερα με ερωτήματα φράσης, μπαλαντέρ ή Boolean για πιο σύνθετα σενάρια.

## Πρακτικές εφαρμογές
- **Διαχείριση νομικών εγγράφων:** Ανάκτηση νόμων συγκεκριμένων περιπτώσεων όπου η κεφαλαία γράμματα έχουν σημασία.  
- **Πλατφόρμες e‑commerce:** Διαχωρισμός SKU προϊόντων όπως “PRO‑X” vs. “pro‑x”.  
- **Συστήματα διαχείρισης περιεχομένου (CMS):** Διασφαλίζετε ότι οι συγγραφείς βρίσκουν ακριβείς τίτλους ή ετικέτες.

## Παράγοντες απόδοσης
- **Διατηρήστε το ευρετήριο ενημερωμένο** – επαναευρετηρίαση όταν προστίθενται νέα αρχεία ή αλλάζουν υπάρχοντα.  
- **Παρακολουθήστε τη χρήση μνήμης** – μεγάλα σώματα κειμένου ωφελούνται από σταδιακή ευρετηρίαση και σωστή ρύθμιση του heap της JVM.  
- **Εκμεταλλευτείτε τον garbage collector της Java** – απελευθερώστε αντικείμενα `Index` όταν δεν χρειάζονται πια.

## Κοινά προβλήματα και λύσεις
| Πρόβλημα | Λύση |
|-------|----------|
| `useCaseSensitiveSearch` φαίνεται να αγνοείται | Επαληθεύστε ότι χρησιμοποιείτε την πιο πρόσφατη έκδοση του GroupDocs.Search και ότι το ευρετήριο έχει ξαναχτιστεί μετά την αλλαγή της επιλογής. |
| Δεν επιστρέφονται αποτελέσματα για έναν γνωστό όρο | Βεβαιωθείτε ότι η πεζοκεφαλαία του όρου ταιριάζει ακριβώς και ότι το έγγραφο προστέθηκε επιτυχώς στο ευρετήριο. |
| Η αναζήτηση σε πολλούς φακέλους επιβραδύνει | Προσθέστε κάθε φάκελο ξεχωριστά με `index.add()` και εξετάστε το διαχωρισμό του ευρετηρίου σε shards για πολύ μεγάλα σύνολα δεδομένων. |

## Συχνές ερωτήσεις

**Q:** Πώς διαχειρίζομαι μεγάλα σύνολα δεδομένων με το GroupDocs.Search;  
**A:** Χρησιμοποιήστε διαμέριση ευρετηρίου, ρυθμίστε τις ρυθμίσεις μνήμης της JVM και περιοδικά συμπιέστε το ευρετήριο για να διατηρήσετε την απόδοση βέλτιστη.

**Q:** Μπορώ να αναζητήσω σε πολλαπλούς καταλόγους ταυτόχρονα;  
**A:** Ναι – καλέστε `index.add()` για κάθε φάκελο που θέλετε να συμπεριλάβετε, έπειτα εκτελέστε ένα ενιαίο ερώτημα στο συνδυασμένο ευρετήριο.

**Q:** Ποια είναι τα κοινά προβλήματα κατά τη ρύθμιση της αναζήτησης με διάκριση πεζών-κεφαλαίων;  
**A:** Η παράλειψη επαναευρετηρίασης μετά την ενεργοποίηση του `useCaseSensitiveSearch`, ή η χρήση λανθασμένης πεζοκεφαλαίας στη συμβολοσειρά ερωτήματος.

**Q:** Πώς μπορώ να εντοπίσω σφάλματα αναζήτησης;  
**A:** Ελέγξτε τα αρχεία καταγραφής που δημιουργεί το GroupDocs.Search για stack traces και βεβαιωθείτε ότι όλες οι εξαρτήσεις Maven έχουν επιλυθεί σωστά.

**Q:** Είναι το GroupDocs.Search κατάλληλο για εφαρμογές σε πραγματικό χρόνο;  
**A:** Με τις κατάλληλες στρατηγικές ευρετηρίασης (αυξομειούμενες ενημερώσεις και caching στη μνήμη), μπορεί να παρέχει σχεδόν πραγματικού χρόνου αποτελέσματα αναζήτησης.

## Πόροι
- **Τεκμηρίωση:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **Αναφορά API:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Λήψη:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **Αποθετήριο GitHub:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Φόρουμ υποστήριξης:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Προσωρινή άδεια:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία ενημέρωση:** 2026-08-10  
**Δοκιμή με:** GroupDocs.Search 25.4  
**Συγγραφέας:** GroupDocs  

## Σχετικά μαθήματα

- [Δημιουργία ευρετηρίου αναζήτησης Java – Οδηγίες GroupDocs.Search](/search/java/indexing/)
- [Πώς να προσθέσετε έγγραφα στο ευρετήριο με το GroupDocs.Search για Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Πώς να προσθέσετε έγγραφα στο ευρετήριο με μεταδεδομένα (Metadata Indexing) σε Java χρησιμοποιώντας το GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)