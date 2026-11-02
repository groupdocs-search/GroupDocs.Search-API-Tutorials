---
date: '2026-11-02'
description: Δημιουργήστε προσαρμοσμένο ευρετήριο αναζήτησης java χρησιμοποιώντας
  GroupDocs.Search για τη διαχείριση κανονικών και μεικτών χαρακτήρων, τη βελτιστοποίηση
  της αναζήτησης εικόνων OCR και τη βελτίωση της ανάκτησης αριθμών νομικών υποθέσεων.
keywords:
- custom search index java
- GroupDocs.Search Java
- character recognition java
- OCR search Java
- search library Java
lastmod: '2026-11-02'
og_description: Δημιουργήστε προσαρμοσμένο ευρετήριο αναζήτησης java χρησιμοποιώντας
  GroupDocs.Search για τη διαχείριση κανονικών και μεικτών χαρακτήρων, τη βελτιστοποίηση
  της αναζήτησης εικόνων OCR και τη βελτίωση της ανάκτησης αριθμών νομικών υποθέσεων.
og_image_alt: Guide showing custom search index creation in Java with GroupDocs.Search
og_title: Δημιουργία προσαρμοσμένου ευρετηρίου αναζήτησης java με GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Create a custom search index java using GroupDocs.Search to handle
    regular and blended characters, optimize OCR image search, and improve legal case
    number retrieval.
  headline: Create a custom search index java with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It means configuring an index to treat specific symbols as letters or
      blended characters, rather than ignoring them.
    question: What does “create custom search index” mean?
  - answer: GroupDocs.Search for Java (v25.4 at the time of writing).
    question: Which library is used?
  - answer: A free trial works for development; a paid license is required for production.
    question: Do I need a license?
  - answer: Yes—GroupDocs.Search supports OCR on images and PDFs when properly configured.
    question: Can I index both PDFs and images?
  - answer: Maven is the recommended way to manage dependencies, but you can also
      use Gradle or manual JARs.
    question: Is Maven required?
  type: FAQPage
tags:
- custom search index
- GroupDocs.Search
- Java OCR
- character recognition
- search library
title: Δημιουργία προσαρμοσμένου ευρετηρίου αναζήτησης java με GroupDocs.Search
type: docs
url: /el/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Δημιουργία προσαρμοσμένου ευρετηρίου αναζήτησης java με το GroupDocs.Search

Σε σύγχρονες εφαρμογές με μεγάλο όγκο εγγράφων, η δημιουργία ενός **custom search index java** που σέβεται τις λεπτομέρειες του κειμένου σας—όπως παύλες, κάτω παύλες ή σύμβολα ειδικά για γλώσσες—είναι απαραίτητη για γρήγορη, ακριβή ανάκτηση. Αυτό το σεμινάριο σας καθοδηγεί στη διαμόρφωση της αναγνώρισης χαρακτήρων στο **GroupDocs.Search for Java**, καλύπτοντας τόσο τους κανονικούς χαρακτήρες (γράμματα, ψηφία, κάτω παύλες) όσο και τους συνδυαστικούς χαρακτήρες (π.χ., παύλες). Στο τέλος, θα μπορείτε να προσαρμόσετε ένα ευρετήριο που ανταποκρίνεται στις ακριβείς ανάγκες σεναρίων OCR ή αναζήτησης εικόνων, είτε ευρετηριάζετε νομικούς αριθμούς υποθέσεων, αποθετήρια κώδικα ή πολυγλωσσικά PDF.

## Γρήγορες απαντήσεις
- **Τι σημαίνει “create custom search index”;** Σημαίνει τη διαμόρφωση ενός ευρετηρίου ώστε να αντιμετωπίζει συγκεκριμένα σύμβολα ως γράμματα ή συνδυαστικούς χαρακτήρες, αντί να τα αγνοεί.  
- **Ποια βιβλιοθήκη χρησιμοποιείται;** GroupDocs.Search for Java (v25.4 at the time of writing).  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται πληρωμένη άδεια για παραγωγή.  
- **Μπορώ να ευρετηριάσω τόσο PDF όσο και εικόνες;** Ναι—το GroupDocs.Search υποστηρίζει OCR σε εικόνες και PDF όταν διαμορφωθεί σωστά.  
- **Απαιτείται το Maven;** Το Maven είναι η προτεινόμενη μέθοδος διαχείρισης εξαρτήσεων, αλλά μπορείτε επίσης να χρησιμοποιήσετε Gradle ή χειροκίνητα JARs.

## Τι είναι ένα custom search index java;
Το **custom search index java** είναι μια δομή δεδομένων αναζήτησης που μπορείτε να διαμορφώσετε ορίζοντας ποιοι χαρακτήρες θα θεωρούνται γράμματα, ψηφία ή συνδυαστικά σύμβολα. Από προεπιλογή, πολλά σύμβολα αγνοούνται, κάτι που μπορεί να προκαλέσει χαμένες αντιστοιχίες για αναγνωριστικά όπως αριθμούς υποθέσεων (`2023-AB-456`) ή αποσπάσματα κώδικα (`my_variable`). Η προσαρμογή του λεξικού αλφαβήτου σας δίνει πλήρη έλεγχο της τοκενικοποίησης, οδηγώντας σε μεγαλύτερη συνάφεια και ταχύτερη εκτέλεση ερωτημάτων.

## Γιατί να διαμορφώσετε κανονικούς και συνδυαστικούς χαρακτήρες για νομικούς αριθμούς υποθέσεων;
Η αντιμετώπιση των παύλων και των καθέτων ως συνδυαστικών χαρακτήρων διατηρεί τα σχετιζόμενα tokens μαζί, αποτρέποντας ανεπιθύμητο διαχωρισμό αναγνωριστικών όπως αριθμοί υποθέσεων, κωδικοί προϊόντων ή διαδρομές αρχείων. Αυτή η διαμόρφωση **βελτιστοποιεί την απόδοση του ευρετηρίου αναζήτησης** μειώνοντας τη θραύση των tokens και βελτιώνει τη συνάφεια για περιεχόμενο που παράγεται από OCR, ειδικά όταν χειρίζεστε νομικά έγγραφα που βασίζονται έντονα σε δομημένα αναγνωριστικά.

## Προαπαιτούμενα
- **JDK 8** ή νεότερο εγκατεστημένο.  
- **Maven** για διαχείριση εξαρτήσεων.  
- Πρόσβαση στη βιβλιοθήκη **GroupDocs.Search for Java** (κατεβασμένη μέσω Maven ή του επίσημου ιστότοπου).  

### Απαιτούμενες βιβλιοθήκες και εξαρτήσεις
Προσθέστε τις καταχωρίσεις αποθετηρίου και εξαρτήσεων στο `pom.xml` σας (όπως φαίνεται παρακάτω). Το μπλοκ XML πρέπει να παραμείνει αμετάβλητο.

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

Μπορείτε επίσης να κατεβάσετε τα πιο πρόσφατα JARs από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση άδειας
- **Free trial** – ιδανική για πρώιμες δοκιμές.  
- **Temporary license** – χρήσιμη για μεγαλύτερους κύκλους ανάπτυξης.  
- **Production license** – απαιτείται για εμπορική ανάπτυξη.  

Αποκτήστε άδεια από το επίσημο portal: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Βασική αρχικοποίηση
Το παρακάτω απόσπασμα κώδικα δείχνει τον ελάχιστο κώδικα που απαιτείται για τη δημιουργία ενός κεντρικού ευρετηρίου. Η κλάση `Index` είναι το κύριο συστατικό που αποθηκεύει και διαχειρίζεται τα δεδομένα αναζήτησης. Διατηρήστε το όπως είναι· θα το επεκτείνουμε αργότερα.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Ρύθμιση GroupDocs.Search για Java

### Εγκατάσταση μέσω Maven
Η διαμόρφωση Maven από την ενότητα *Prerequisites* είναι ό,τι χρειάζεστε. Μετά την προσθήκη, εκτελέστε `mvn clean install` για να κατεβάσετε τα δυαδικά αρχεία.

### Απαιτήσεις ρύθμισης περιβάλλοντος
- Βεβαιωθείτε ότι ο **index folder** και ο **document folder** υπάρχουν στο δίσκο.  
- Χρησιμοποιήστε απόλυτες διαδρομές ή διαμορφώστε το IDE σας ώστε να επιλύει σωστά τις σχετικές διαδρομές.

## Οδηγός υλοποίησης

Παρακάτω περπατάμε μέσα από δύο ξεχωριστά χαρακτηριστικά: **regular characters** και **blended characters**. Κάθε χαρακτηριστικό ακολουθεί το ίδιο μοτίβο—ορίζετε διαδρομές, δημιουργείτε το ευρετήριο, ορίζετε το λεξικό χαρακτήρων και τέλος ευρετηριάζετε τα έγγραφά σας.

### Χαρακτηριστικό 1 – regular characters

#### Επισκόπηση
Οι κανονικοί χαρακτήρες αντιμετωπίζονται ως ανεξάρτητα tokens. Αυτό είναι ιδανικό όταν θέλετε ψηφία, γράμματα και κάτω παύλες να είναι αναζητήσιμα ακριβώς όπως εμφανίζονται.

#### Υλοποίηση βήμα‑βήμα

**1️⃣ Ορισμός διαδρομών**  
Ορίστε πού θα αποθηκευτεί το ευρετήριο και πού βρίσκονται τα πηγαία έγγραφά σας.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Δημιουργία και διαμόρφωση ευρετηρίου**  
Δημιουργήστε ένα αντικείμενο του ευρετηρίου και καθαρίστε τυχόν προϋπάρχουσα διαμόρφωση αλφαβήτου.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Ορισμός κανονικών χαρακτήρων**  
Δημιουργήστε έναν πίνακα χαρακτήρων που περιλαμβάνει ψηφία, λατινικά γράμματα και την κάτω παύλα.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Ευρετηρίαση εγγράφων**  
Προσθέστε όλα τα αρχεία από το φάκελο πηγής στο νεοδιαμορφωμένο ευρετήριο.

```java
index.add(documentFolder);
```

### Χαρακτηριστικό 2 – blended characters

#### Επισκόπηση
Οι συνδυαστικοί χαρακτήρες (όπως οι παύλες) συχνά συνδέουν δύο λέξεις. Η σήμανσή τους ως *blended* λέει στη μηχανή να διατηρεί τα γύρω tokens μαζί κατά την ευρετηρίαση.

#### Υλοποίηση βήμα‑βήμα

**1️⃣ Ορισμός διαδρομών**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Δημιουργία και διαμόρφωση ευρετηρίου**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Ορισμός συνδυαστικών χαρακτήρων**  
Εδώ ενημερώνουμε το λεξικό ότι η παύλα πρέπει να αντιμετωπίζεται ως συνδυαστικός χαρακτήρας.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Ευρετηρίαση εγγράφων**  

```java
index.add(documentFolder);
```

## Πρακτικές εφαρμογές

### Περίπτωση χρήσης 1 – διαχείριση νομικών εγγράφων
Τα νομικά αρχεία συχνά περιέχουν αριθμούς υποθέσεων όπως `2023-AB-456`. Με τη διαμόρφωση των κάτω παυλών και των παύλων, οι αναζητήσεις επιστρέφουν ακριβείς αντιστοιχίες χωρίς να χωρίζουν το αναγνωριστικό, βοηθώντας σας να **αναζητήσετε νομικούς αριθμούς υποθέσεων** αποδοτικά.

### Περίπτωση χρήσης 2 – αποθετήρια κώδικα
Οι προγραμματιστές χρειάζονται να αναζητούν αποσπάσματα κώδικα όπου οι κάτω παύλες (`my_variable`) και οι παύλες (`my-function`) έχουν σημασία. Η προσαρμοσμένη αναγνώριση χαρακτήρων διασφαλίζει ότι η μηχανή αναζήτησης σέβεται αυτά τα σύμβολα.

### Περίπτωση χρήσης 3 – πολυγλωσσικά σύνολα δεδομένων
Όταν εργάζεστε με γλώσσες που χρησιμοποιούν πρόσθετα αλφάβητα, μπορείτε να **επεκτείνετε το σύνολο χαρακτήρων Unicode** ώστε να περιλαμβάνει αυτά τα εύρη, εξασφαλίζοντας ακριβή αποτελέσματα αναζήτησης μεταξύ γλωσσών.

### Περίπτωση χρήσης 4 – ευρετηρίαση εικόνων PDF
Εάν ευρετηριάζετε σαρωμένα PDF ή αρχεία εικόνας, η έξοδος OCR συχνά περιέχει μικτούς χαρακτήρες. Η σωστή διαμόρφωση κανονικών και συνδυαστικών χαρακτήρων **βελτιστοποιεί την απόδοση του ευρετηρίου αναζήτησης** για περιεχόμενο βασισμένο σε εικόνες.

## Σκέψεις για την απόδοση

- **Διαχείριση πόρων** – παρακολουθήστε τη χρήση heap· μεγάλα ευρετήρια ωφελούνται από σταδιακές υποβολές.  
- **Garbage collection** – απελευθερώστε αντικείμενα `Index` όταν τελειώσετε ώστε η JVM να ανακτήσει μνήμη.  
- **Βελτιστοποίηση ευρετηρίου** – καλείτε περιοδικά το `index.optimize()` (αν είναι διαθέσιμο) για να συμπιέσετε το ευρετήριο και να βελτιώσετε την ταχύτητα ερωτημάτων.  

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να δημιουργήσετε ένα custom search index java** που διακρίνει μεταξύ κανονικών και συνδυαστικών χαρακτήρων χρησιμοποιώντας το GroupDocs.Search for Java. Αυτός ο λεπτομερής έλεγχος σας δίνει τη δυνατότητα να δημιουργήσετε λύσεις αναζήτησης υψηλής απόδοσης, ευαίσθητες στο OCR, προσαρμοσμένες σε νομικά, προγραμματιστικά ή πολυγλωσσικά περιβάλλοντα.

### Επόμενα βήματα
- Πειραματιστείτε με πρόσθετα εύρη Unicode για μη λατινικά αλφάβητα.  
- Συνδυάστε τη διαμόρφωση χαρακτήρων με άλλες δυνατότητες του GroupDocs.Search όπως stemming ή synonyms.  
- Εκθέστε το ευρετήριο μέσω REST API ώστε οι εφαρμογές front‑end να εκτελούν αναζητήσεις μέσω HTTP.  

## Συχνές ερωτήσεις

**Q:** *Ποιος είναι ο σκοπός του `CharacterType.Letter`;*  
**A:** Λέει στο ευρετήριο να αντιμετωπίζει τους παρεχόμενους χαρακτήρες ως κανονικά γράμματα, ώστε να τοκενικοποιούνται ξεχωριστά κατά την ευρετηρίαση.

**Q:** *Μπορώ να συνδυάσω κανονικούς και συνδυαστικούς χαρακτήρες στο ίδιο ευρετήριο;*  
**A:** Ναι—απλώς καλέστε `setRange` για κάθε τύπο· το λεξικό θα διαχειριστεί και τις δύο διαμορφώσεις ταυτόχρονα.

**Q:** *Πρέπει να ξαναχτίσω το ευρετήριο μετά την αλλαγή του αλφαβήτου;*  
**A:** Απόλυτα. Οι αλλαγές στο λεξικό χαρακτήρων επηρεάζουν την τοκενικοποίηση, επομένως πρέπει να επανευρετηριάσετε τα έγγραφα για να εφαρμοστούν οι νέοι κανόνες.

**Q:** *Υπάρχει όριο στον αριθμό των προσαρμοσμένων χαρακτήρων που μπορώ να ορίσω;*  
**A:** Η βιβλιοθήκη υποστηρίζει ολόκληρο το εύρος Unicode· η απόδοση μπορεί να μειωθεί αν προσθέσετε ένα εξαιρετικά μεγάλο σύνολο, οπότε περιορίστε το σε χαρακτήρες που χρειάζεστε πραγματικά.

**Q:** *Πώς αυτό επηρεάζει την ακρίβεια του OCR;*  
**A:** Ευθυγραμμίζοντας το σύνολο χαρακτήρων του ευρετηρίου με την έξοδο του OCR, μειώνετε τα ψευδώς αρνητικά και βελτιώνετε τη συνολική συνάφεια της αναζήτησης.

---

**Τελευταία ενημέρωση:** 2026-11-02  
**Δοκιμή με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Δημιουργία και διαχείριση Groupdocs Search Java Index](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Δημιουργία καταλόγου ευρετηρίου αναζήτησης & ορισμός άδειας – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Βιβλιοθήκη Java Full Text Search – Βελτιστοποίηση ευρετηρίου με GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)