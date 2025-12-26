---
date: '2025-12-26'
description: Μάθετε πώς να αναζητάτε και να επισημαίνετε κείμενο σε έγγραφα χρησιμοποιώντας
  το GroupDocs.Search για Java. Εξερευνήστε τεχνικές για επισημάνσεις ολόκληρου εγγράφου
  και τμημάτων.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Αναζήτηση και επισήμανση κειμένου με το GroupDocs.Search για Java
type: docs
url: /el/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Αναζήτηση και Επισήμανση Κειμένου σε Έγγραφα Χρησιμοποιώντας το GroupDocs.Search για Java

Στην ψηφιακή εποχή μας, **search and highlight text** σε τεράστιες συλλογές εγγράφων αποτελεί κοινή απαίτηση. Είτε δημιουργείτε ένα εργαλείο νομικής ανασκόπησης, μια ακαδημαϊκή ερευνητική πύλη ή έναν πίνακα ελέγχου εξυπηρέτησης πελατών, η δυνατότητα άμεσης εντοπισμού και επισήμανσης βασικών όρων βελτιώνει δραστικά τη χρηστικότητα. Σε αυτόν τον ολοκληρωμένο οδηγό, θα ανακαλύψετε πώς να υλοποιήσετε **search and highlight text** με το GroupDocs.Search για Java—καλύπτοντας τόσο την επισήμανση ολόκληρων εγγράφων όσο και την επισήμανση σε επίπεδο τμημάτων για εστιασμένο περιεχόμενο.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει το “search and highlight text”;** Αναφέρεται στον εντοπισμό όρων ερωτήματος σε ένα έγγραφο και στην οπτική τους επισήμανση (π.χ., με χρώμα φόντου).  
- **Ποια βιβλιοθήκη παρέχει αυτή τη δυνατότητα;** GroupDocs.Search for Java.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται πλήρης άδεια για παραγωγή.  
- **Μπορώ να προσαρμόσω τα χρώματα επισήμανσης;** Ναι—οποιοδήποτε χρώμα RGB μπορεί να οριστεί μέσω του `HighlightOptions`.  
- **Υποστηρίζεται η επισήμανση τμημάτων;** Απόλυτα· μπορείτε να ορίσετε όρους πριν/μετά το ταίριασμα για να δημιουργήσετε σύντομες αποσπάσεις.

## Τι Είναι η Αναζήτηση και Επισήμανση Κειμένου;
Η **search and highlight text** είναι η διαδικασία σάρωσης ενός ευρετηρίου εγγράφων για ένα δεδομένο ερώτημα, ανάκτησης των ταιριαστών εγγράφων και στη συνέχεια επισήμανσης κάθε εμφάνισης του όρου ερωτήματος μέσα στην έξοδο του εγγράφου (HTML, PDF κ.λπ.). Αυτό το οπτικό σήμα βοηθά τους τελικούς χρήστες να εντοπίζουν σχετικές πληροφορίες άμεσα.

## Γιατί να Χρησιμοποιήσετε το GroupDocs.Search για Java;
- **High‑performance indexing** με ρυθμιζόμενη συμπίεση.  
- **Rich highlighting API** που λειτουργεί σε ολόκληρα έγγραφα και σε προσαρμοσμένα τμήματα.  
- **Cross‑format support** (DOCX, PDF, PPTX, TXT και άλλα).  
- **Easy Maven integration** και σαφής Java‑centric API.

## Προαπαιτούμενα
- Java Development Kit (JDK) 8 ή νεότερο.  
- Maven για διαχείριση εξαρτήσεων.  
- Ένα IDE όπως IntelliJ IDEA ή Eclipse.  
- Βασική εξοικείωση με τη σύνταξη της Java.

## Ρύθμιση του GroupDocs.Search για Java

Προσθέστε το αποθετήριο GroupDocs και την εξάρτηση στο `pom.xml` σας:

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

Μπορείτε επίσης να κατεβάσετε το πιο πρόσφατο JAR απευθείας από την επίσημη ιστοσελίδα: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση Άδειας
Ξεκινήστε με μια δωρεάν δοκιμή ή αποκτήστε προσωρινή άδεια για αξιολόγηση. Για παραγωγικές εγκαταστάσεις, αγοράστε πλήρη άδεια για να ξεκλειδώσετε όλες τις λειτουργίες.

## Οδηγός Υλοποίησης

Η υλοποίηση χωρίζεται σε δύο πρακτικές ενότητες: **highlighting in entire documents** και **highlighting in fragments**. Και οι δύο ενότητες περιλαμβάνουν τα βασικά βήματα για **how to highlight Java** έγγραφα χρησιμοποιώντας το GroupDocs.Search.

### Διαμόρφωση Ρυθμίσεων Ευρετηρίου
Πριν από την ευρετηρίαση, διαμορφώστε την αποθήκευση ώστε να χρησιμοποιεί υψηλή συμπίεση—αυτό μειώνει τη χρήση δίσκου ενώ διατηρεί την ταχύτητα αναζήτησης.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Επισήμανση σε Ολόκληρα Έγγραφα

#### Βήμα 1: Δημιουργία και Συμπλήρωση του Ευρετηρίου
Δημιουργήστε έναν φάκελο ευρετηρίου και προσθέστε όλα τα αρχεία προέλευσης που θέλετε να αναζητήσετε.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Βήμα 2: Εκτέλεση Αναζήτησης και Εφαρμογή Επισήμανσης
Αναζητήστε τον όρο (π.χ., `ipsum`) και δημιουργήστε ένα αρχείο HTML με τις επισημασμένες αντιστοιχίες.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Επεξήγηση βασικών επιλογών**
- **Compression** – η υψηλή συμπίεση εξοικονομεί χώρο αποθήκευσης.  
- **HighlightColor** – ορίστε οποιαδήποτε τιμή RGB για να ταιριάζει με την παλέτα UI σας.  
- **UseInlineStyles** – `false` δημιουργεί καθαρό HTML που μπορεί να στιλιζαριστεί παγκοσμίως με CSS.

### Επισήμανση σε Τμήματα

#### Βήμα 1: Ευρετηρίαση και Αναζήτηση (όπως παραπάνω)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Βήμα 2: Ορισμός Περιβάλλοντος Τμήματος και Επισήμανση
Καθορίστε πόσοι όροι πριν και μετά το ταίριασμα πρέπει να εμφανίζονται σε κάθε τμήμα.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### Βήμα 3: Ανάκτηση και Γραφή Επισημασμένων Τμημάτων
Συλλέξτε τα παραγόμενα τμήματα και γράψτε τα σε ένα αρχείο HTML.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Πρακτικές Εφαρμογές
1. **Legal Document Review** – άμεση επισήμανση νόμων, ρητρών ή αναφορών υποθέσεων.  
2. **Academic Research** – εμφάνιση βασικής ορολογίας σε δεκάδες PDF και αρχεία Word.  
3. **Customer Support** – εντοπισμός αριθμών παραγγελιών ή κωδικών σφάλματος μέσα σε ιστορικά αιτημάτων.

## Σκέψεις για την Απόδοση
- **Index Size** – η υψηλή συμπίεση (`Compression.High`) μειώνει το αποτύπωμα στο δίσκο.  
- **Fragment Context** – μεγαλύτερες τιμές `termsBefore/After` αυξάνουν την ακρίβεια αλλά μπορεί να επηρεάσουν την ταχύτητα.  
- **Memory Management** – παρακολουθήστε τη μνήμη heap της JVM κατά την ευρετηρίαση μεγάλων σωμάτων δεδομένων· σκεφτείτε την επαναληπτική ευρετηρίαση για πολύ μεγάλα σύνολα.

## Συχνά Προβλήματα και Λύσεις
- **Indexing Errors** – επαληθεύστε τις διαδρομές αρχείων και βεβαιωθείτε ότι η εφαρμογή έχει δικαιώματα ανάγνωσης/εγγραφής.  
- **No Highlights Appear** – επιβεβαιώστε ότι το `UseInlineStyles` ταιριάζει με τη μορφή εξόδου (HTML vs. PDF).  
- **Color Not Applied** – βεβαιωθείτε ότι οι τιμές RGB είναι εντός του εύρους 0‑255 και ότι ο προβολέας HTML υποστηρίζει το στυλ.

## Συχνές Ερωτήσεις

**Q: Ποια είναι τα οφέλη της χρήσης του GroupDocs.Search για Java;**  
A: Παρέχει γρήγορη, κλιμακώσιμη ευρετηρίαση, προσαρμόσιμη επισήμανση και υποστήριξη για πολλές μορφές εγγράφων.

**Q: Πώς μπορώ να ενσωματώσω το GroupDocs.Search με ένα REST API;**  
A: Εκθέστε τις μεθόδους αναζήτησης και επισήμανσης μέσω ελεγκτών Spring Boot, επιστρέφοντας φορτία HTML ή JSON.

**Q: Η βιβλιοθήκη διαχειρίζεται αρχεία με κωδικό πρόσβασης;**  
A: Ναι—παρέχετε τον κωδικό όταν προσθέτετε το έγγραφο στο ευρετήριο.

**Q: Μπορώ να προσαρμόσω το markup της επισήμανσης πέρα από το χρώμα;**  
A: Απόλυτα· μπορείτε να ενσωματώσετε κλάσεις CSS μέσω του `HighlightOptions` ή να τροποποιήσετε το HTML μετά τη δημιουργία.

**Q: Ποια έκδοση δοκιμάστηκε για αυτόν τον οδηγό;**  
A: Ο κώδικας επικυρώθηκε ενάντια στο GroupDocs.Search 25.4.

---

**Τελευταία Ενημέρωση:** 2025-12-26  
**Δοκιμάστηκε Με:** GroupDocs.Search 25.4  
**Συγγραφέας:** GroupDocs