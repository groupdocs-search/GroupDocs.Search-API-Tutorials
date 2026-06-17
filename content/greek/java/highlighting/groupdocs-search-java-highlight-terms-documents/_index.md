---
date: '2026-02-27'
description: Μάθετε πώς να επισημαίνετε κείμενο Java χρησιμοποιώντας το GroupDocs.Search
  για Java, καλύπτοντας την αναζήτηση εγγράφων Java, την ευρετηρίαση εγγράφων Java
  και την επισήμανση τμημάτων.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Επισήμανση κειμένου Java με το GroupDocs.Search
type: docs
url: /el/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Επισήμανση Κειμένου Java με το GroupDocs.Search

Στο σημερινό γρήγορα εξελισσόμενο ψηφιακό περιβάλλον, η δυνατότητα **highlight text java** σε μεγάλες συλλογές αρχείων αποτελεί απαραίτητο χαρακτηριστικό. Είτε δημιουργείτε μια πλατφόρμα νομικής ανασκόπησης, μια μηχανή ακαδημαϊκής έρευνας ή μια κονσόλα εξυπηρέτησης πελατών, η άμεση εντόπιση των όρων που αναζητούν οι χρήστες κάνει την εμπειρία πολύ πιο αποδοτική. Αυτό το tutorial σας καθοδηγεί στη χρήση του **GroupDocs.Search for Java** για **search documents java**, **index documents java**, και την εφαρμογή πλούσιας επισήμανσης — τόσο για ολόκληρα έγγραφα όσο και για συγκεκριμένα τμήματα.

## Quick Answers
- **Τι σημαίνει “search and highlight text”;** Αναφέρεται στην εντόπιση όρων ερωτήματος σε ένα έγγραφο και στην οπτική τους επισήμανση (π.χ., με χρώμα φόντου).  
- **Ποια βιβλιοθήκη παρέχει αυτή τη δυνατότητα;** GroupDocs.Search for Java.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται πλήρης άδεια για παραγωγική χρήση.  
- **Μπορώ να προσαρμόσω τα χρώματα επισήμανσης;** Ναι — οποιοδήποτε χρώμα RGB μπορεί να οριστεί μέσω του `HighlightOptions`.  
- **Υποστηρίζεται η επισήμανση τμημάτων;** Απολύτως· μπορείτε να ορίσετε όρους πριν/μετά το ταίριασμα για να δημιουργήσετε σύντομες αποσπάσεις.

## How to Highlight Text Java in Documents
Η επισήμανση κειμένου Java περιλαμβάνει τρία βασικά βήματα:

1. **Δημιουργία ευρετηρίου των πηγαίων αρχείων** ώστε να μπορούν να αναζητηθούν γρήγορα.  
2. **Εκτέλεση ερωτήματος** στο ευρετήριο για την εύρεση των ταιριαστών εγγράφων.  
3. **Απόδοση των αποτελεσμάτων με οπτικές ενδείξεις** χρησιμοποιώντας το API του highlighter.  

Παρακάτω εξετάζουμε κάθε βήμα λεπτομερώς, πρώτα για έξοδο ολόκληρου εγγράφου και στη συνέχεια για αποσπάσματα επιπέδου τμήματος.

## What Is Search and Highlight Text?
Το search and highlight text είναι η διαδικασία σάρωσης ενός ευρετηρίου εγγράφων για ένα συγκεκριμένο ερώτημα, ανάκτησης των ταιριαστών εγγράφων και στη συνέχεια επισήμανσης κάθε εμφάνισης του όρου ερωτήματος μέσα στην έξοδο του εγγράφου (HTML, PDF κ.λπ.). Αυτή η οπτική ένδειξη βοηθά τους τελικούς χρήστες να εντοπίζουν άμεσα τις σχετικές πληροφορίες.

## Why Use GroupDocs.Search for Java?
- **Υψηλής απόδοσης ευρετηρίαση** με ρυθμιζόμενη συμπίεση (`index documents java`).  
- **Πλούσιο API επισήμανσης** που λειτουργεί σε ολόκληρα έγγραφα και σε προσαρμοσμένα τμήματα (`highlight search terms java`).  
- **Υποστήριξη πολλαπλών μορφών** (DOCX, PDF, PPTX, TXT και άλλα).  
- **Απλή ενσωμάτωση Maven** και καθαρός σχεδιασμός προσανατολισμένος στη Java.

## Prerequisites
- Java Development Kit (JDK) 8 ή νεότερο.  
- Maven για διαχείριση εξαρτήσεων.  
- Ένα IDE όπως IntelliJ IDEA ή Eclipse.  
- Βασική εξοικείωση με τη σύνταξη της Java.

## Setting Up GroupDocs.Search for Java

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

### License Acquisition
Ξεκινήστε με μια δωρεάν δοκιμή ή αποκτήστε προσωρινή άδεια για αξιολόγηση. Για παραγωγικές εγκαταστάσεις, αγοράστε πλήρη άδεια για να ξεκλειδώσετε όλες τις δυνατότητες.

## Implementation Guide

Η υλοποίηση χωρίζεται σε δύο πρακτικές ενότητες: **επισήμανση σε ολόκληρα έγγραφα** και **επισήμανση σε τμήματα**. Και οι δύο ενότητες περιλαμβάνουν τα απαραίτητα βήματα για **πώς να επισημάνετε έγγραφα Java** χρησιμοποιώντας το GroupDocs.Search.

### Configuring Index Settings
Πριν τη δημιουργία ευρετηρίου, ρυθμίστε την αποθήκευση για χρήση υψηλής συμπίεσης — αυτό μειώνει τη χρήση δίσκου ενώ διατηρεί την ταχύτητα αναζήτησης.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Highlighting in Entire Documents

#### Step 1: Create and Populate the Index
Δημιουργήστε έναν φάκελο ευρετηρίου και προσθέστε όλα τα πηγαία αρχεία που θέλετε να αναζητήσετε.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Step 2: Perform Search and Apply Highlighting
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

**Key options explained**  
- **Compression** – η υψηλή συμπίεση εξοικονομεί χώρο αποθήκευσης.  
- **HighlightColor** – ορίστε οποιαδήποτε τιμή RGB για να ταιριάζει με την παλέτα UI σας.  
- **UseInlineStyles** – `false` δημιουργεί καθαρό HTML που μπορεί να στιλιζαριστεί παγκοσμίως με CSS.  

### Highlighting in Fragments

#### Step 1: Index and Search (same as above)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Step 2: Define Fragment Context and Highlight
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

#### Step 3: Retrieve and Write Highlighted Fragments
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

## Practical Applications
1. **Ανασκόπηση Νομικών Εγγράφων** – άμεση επισήμανση νόμων, ρητρών ή αναφορών υποθέσεων.  
2. **Ακαδημαϊκή Έρευνα** – ανάδειξη βασικής ορολογίας σε δεκάδες αρχεία PDF και Word.  
3. **Εξυπηρέτηση Πελατών** – εντοπισμός αριθμών παραγγελιών ή κωδικών σφάλματος μέσα σε ιστορικά αιτημάτων.

## Performance Considerations
- **Μέγεθος Ευρετηρίου** – η υψηλή συμπίεση (`Compression.High`) μειώνει το αποτύπωμα στο δίσκο.  
- **Πλαίσιο Τμημάτων** – μεγαλύτερες τιμές `termsBefore/After` αυξάνουν την ακρίβεια αλλά μπορεί να επηρεάσουν την ταχύτητα.  
- **Διαχείριση Μνήμης** – παρακολουθήστε τη μνήμη heap της JVM κατά την ευρετηρίαση μεγάλων σωμάτων δεδομένων· σκεφτείτε την επαναληπτική ευρετηρίαση για πολύ μεγάλα σύνολα.

## Common Issues and Solutions
- **Σφάλματα Ευρετηρίου** – ελέγξτε τις διαδρομές αρχείων και βεβαιωθείτε ότι η εφαρμογή έχει δικαιώματα ανάγνωσης/εγγραφής.  
- **Δεν Εμφανίζονται Επισήμανση** – επιβεβαιώστε ότι το `UseInlineStyles` ταιριάζει με τη μορφή εξόδου (HTML vs. PDF).  
- **Το Χρώμα Δεν Εφαρμόζεται** – βεβαιωθείτε ότι οι τιμές RGB είναι εντός του εύρους 0‑255 και ότι ο προβολέας HTML υποστηρίζει το στυλ.

## Frequently Asked Questions

**Q: Ποια είναι τα οφέλη της χρήσης του GroupDocs.Search for Java;**  
A: Παρέχει γρήγορη, κλιμακώσιμη ευρετηρίαση, προσαρμόσιμη επισήμανση και υποστήριξη πολλών μορφών εγγράφων.

**Q: Πώς μπορώ να ενσωματώσω το GroupDocs.Search με ένα REST API;**  
A: Εκθέστε τις μεθόδους αναζήτησης και επισήμανσης μέσω ελεγκτών Spring Boot, επιστρέφοντας φορτία HTML ή JSON.

**Q: Η βιβλιοθήκη διαχειρίζεται αρχεία με κωδικό πρόσβασης;**  
A: Ναι — παρέχετε τον κωδικό πρόσβασης κατά την προσθήκη του εγγράφου στο ευρετήριο.

**Q: Μπορώ να προσαρμόσω το markup της επισήμανσης πέρα από το χρώμα;**  
A: Απόλυτα· μπορείτε να ενσωματώσετε κλάσεις CSS μέσω του `HighlightOptions` ή να τροποποιήσετε το HTML μετά τη δημιουργία.

**Q: Ποια έκδοση δοκιμάστηκε για αυτόν τον οδηγό;**  
A: Ο κώδικας επαληθεύτηκε με το GroupDocs.Search 25.4.

**Q: Πώς μπορώ να ρυθμίσω τις επιλογές επισήμανσης java για χρήση κλάσης CSS αντί για ενσωματωμένα στυλ;**  
A: Ορίστε `options.setUseInlineStyles(false)` και προσθέστε έναν κανόνα CSS για την κλάση που ορίζετε μέσω `options.setCssClass("myHighlight")`.

**Q: Υπάρχει τρόπος να επισήμανση όρων pdf java γίνεται απευθείας όταν η πηγή είναι PDF;**  
A: Ναι — το GroupDocs.Search λειτουργεί με είσοδο PDF, και ο highlighter θα παραγάγει HTML που μπορείτε να ενσωματώσετε σε προβολέα PDF ή να μετατρέψετε ξανά σε PDF χρησιμοποιώντας το GroupDocs.Conversion.

---

**Τελευταία ενημέρωση:** 2026-02-27  
**Δοκιμή με:** GroupDocs.Search 25.4  
**Συγγραφέας:** GroupDocs