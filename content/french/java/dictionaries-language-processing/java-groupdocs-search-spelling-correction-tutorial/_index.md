---
date: '2026-09-02'
description: Apprenez à créer un index de recherche Java et à activer la correction
  orthographique à l'aide de GroupDocs.Search. Suivez les instructions étape par étape
  pour ajouter des documents, configurer le nombre maximal d'erreurs, et améliorer
  la précision de la recherche.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: Apprenez à créer un index de recherche Java et à activer la correction
  orthographique à l'aide de GroupDocs.Search. Suivez les instructions étape par étape
  pour ajouter des documents, configurer le nombre maximal d'erreurs, et améliorer
  la précision de la recherche.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: Comment créer un index de recherche Java et activer la correction orthographique
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: Comment créer un index de recherche Java et activer la correction orthographique
type: docs
url: /fr/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Comment créer un index de recherche java et activer la correction orthographique

Dans les applications Java modernes, fournir des résultats de recherche précis est une fonctionnalité indispensable. Ce tutoriel montre **comment créer un index de recherche java** et activer la correction orthographique avec GroupDocs.Search, afin que les utilisateurs obtiennent des résultats pertinents même lorsqu'ils tapent mal leurs requêtes. Vous verrez comment configurer la bibliothèque, ajouter des documents, définir le nombre maximal d'erreurs, et exécuter une recherche tolérante aux fautes de frappe — le tout sans écrire une seule ligne de code de configuration supplémentaire.

## Réponses rapides
- **Que fait « enable spelling » ?** Il active le correcteur orthographique intégré qui réécrit les termes mal orthographiés en leurs formes correctes les plus proches lors d’une recherche.  
- **Quelle bibliothèque fournit cette fonctionnalité ?** GroupDocs.Search for Java.  
- **Ai‑je besoin d’une licence ?** Un essai gratuit suffit pour l’évaluation ; une licence complète est requise pour une utilisation en production.  
- **Puis‑je contrôler la tolérance ?** Oui – utilisez `setMaxMistakeCount` pour définir le nombre de fautes autorisées par requête.  
- **Est‑il adapté aux gros index ?** Absolument – le moteur gère des index contenant des millions d’enregistrements tout en maintenant la latence des requêtes sous 100 ms sur du matériel serveur typique.

## Qu’est‑ce que GroupDocs.Search ?
GroupDocs.Search est une bibliothèque Java qui offre un indexage plein texte rapide et des fonctionnalités de recherche avancées, y compris la correction orthographique intégrée. Elle prend en charge plus de 50 formats d’entrée et peut traiter des documents de plusieurs centaines de pages sans charger le fichier complet en mémoire.

## Pourquoi activer la correction orthographique dans les applications Java ?
- **Améliore la satisfaction des utilisateurs** – les visiteurs obtiennent des résultats corrects même avec une saisie imparfaite.  
- **Réduit le taux de rebond** – des résultats précis maintiennent les utilisateurs engagés plus longtemps.  
- **Fonctionne dans tous les domaines** – des catalogues de bibliothèques aux recherches de produits e‑commerce, la correction orthographique améliore la pertinence partout.

## Prérequis
- Java Development Kit (JDK) installé.  
- Connaissances de base en Java et Maven.  
- Compréhension des concepts d’indexation.  
- Un essai ou une clé de licence GroupDocs.Search.

### Configuration de GroupDocs.Search pour Java
Intégrez la bibliothèque à votre projet Maven.

**Configuration Maven**  
Ajoutez le dépôt et la dépendance à votre fichier `pom.xml` :

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

**Téléchargement direct**  
Sinon, téléchargez la dernière version depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
Obtenez une licence d’essai gratuite pour l’évaluation. Pour une utilisation en production, achetez une licence complète ou demandez une clé temporaire sur le site officiel.

## Comment créer un index de recherche en Java ?
`SearchIndex` est la classe principale qui représente un index consultable stocké sur disque.  
Créez une instance `SearchIndex` pointant vers un dossier sur le disque, puis ajoutez des documents depuis un répertoire source. Le moteur construit un index inversé qui permet des recherches rapides. Vous pouvez appeler `index.add()` pour chaque fichier ; la bibliothèque extrait le texte automatiquement en fonction du type de fichier.

## Comment activer la correction orthographique ?
`getSpellingOptions()` renvoie l’objet de configuration orthographique de l’index, vous permettant d’activer ou d’ajuster les fonctionnalités de correction.  
Activez la correction en appelant `index.getSpellingOptions().setEnabled(true)`. Cela indique au moteur d’analyser les termes de la requête et de proposer des alternatives corrigées lorsqu’une discordance est détectée. La fonctionnalité fonctionne immédiatement pour toutes les langues indexées prises en charge par la bibliothèque.

## Quelle est la configuration du nombre maximal d’erreurs ?
`setMaxMistakeCount` configure le nombre maximal de modifications de caractères que le correcteur orthographique tolérera par terme.  
`setMaxMistakeCount(int)` définit le nombre maximal de modifications de caractères (insertions, suppressions, substitutions) que le correcteur orthographique tolérera par terme. Le régler à **2** permet au moteur de corriger les fautes de deux caractères courantes tout en évitant des corrections trop agressives qui pourraient renvoyer des résultats non pertinents.

## Comment effectuer une recherche avec correction orthographique
`search()` exécute une requête sur l’index et renvoie un objet `SearchResult` contenant les correspondances et les termes corrigés éventuels.  
Exécutez une requête de recherche en utilisant la méthode `search()`. Si la requête contient des mots mal orthographiés, le moteur renvoie un `SearchResult` qui inclut les termes corrigés et une liste des documents les plus pertinents. Vous pouvez afficher à l’utilisateur à la fois la requête originale et la version corrigée pour plus de transparence.  
`SearchResult` contient la liste des documents correspondants et les informations sur les corrections de la requête.

## Applications pratiques
1. **Systèmes de bibliothèque** – corrige automatiquement les titres de livres ou les noms d’auteurs mal orthographiés.  
2. **Plateformes e‑commerce** – corrige les fautes de frappe dans les noms de produits pour augmenter les taux de conversion.  
3. **Gestion de contenu** – aide le personnel éditorial à trouver des articles même avec des mots‑clés imparfaits.

## Considérations de performance
- **Maintenez l’index à jour** – ré‑indexez régulièrement les fichiers nouveaux ou modifiés.  
- **Ajustez les paramètres de mémoire JVM** – allouez un tas suffisant pour les gros index (par ex., `-Xmx4g`).  
- **Surveillez l’utilisation des ressources** – ajustez les paramètres du ramasse‑miettes si vous constatez des pauses lors d’un indexage en masse.

## Problèmes courants & dépannage
| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Aucun résultat après l’activation de la correction orthographique | Le chemin du dossier d’index est incorrect ou vide | Vérifiez que `indexFolder` pointe vers un index valide et que `index.add()` a réussi |
| Le correcteur orthographique ne corrige pas les fautes évidentes | `setMaxMistakeCount` est réglé trop bas | Augmentez le nombre à 2 ou 3 pour une correction plus tolérante |
| L’application plante avec de grands ensembles de documents | Mémoire JVM insuffisante | Augmentez l’option `-Xmx` (par ex., `-Xmx4g`) |

## Questions fréquemment posées

**Q : Qu’est‑ce que GroupDocs.Search ?**  
R : GroupDocs.Search est une bibliothèque Java qui offre un indexage rapide, des capacités de requête avancées et une correction orthographique intégrée pour toute application Java.

**Q : Comment obtenir une licence pour GroupDocs.Search ?**  
R : Visitez le site officiel pour télécharger un essai gratuit ou acheter une licence complète ; une clé temporaire est également disponible pour des tests à court terme.

**Q : Puis‑je intégrer GroupDocs.Search avec d’autres frameworks Java ?**  
R : Oui, il fonctionne parfaitement avec Spring, Jakarta EE et toute application Java standard.

**Q : Quels sont les problèmes courants lors de la configuration d’un index ?**  
R : Des chemins de dossiers incorrects, des permissions de fichiers manquantes ou des dépendances Maven absentes sont les causes habituelles.

**Q : Comment la correction orthographique améliore‑t‑elle les résultats de recherche ?**  
R : Elle réécrit automatiquement les requêtes mal orthographiées en leurs termes corrects les plus proches, renvoyant des résultats plus pertinents et réduisant la frustration des utilisateurs.

## Ressources supplémentaires
- [Documentation](https://docs.groupdocs.com/search/java/)
- [Référence API](https://reference.groupdocs.com/search/java)
- [Téléchargement](https://releases.groupdocs.com/search/java/)
- [Dépôt GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Forum d’assistance gratuit](https://forum.groupdocs.com/c/search/10)
- [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)

---

**Dernière mise à jour :** 2026-09-02  
**Testé avec :** GroupDocs.Search 25.4  
**Auteur :** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## Tutoriels associés

- [Comment créer un index de documents et ajouter des documents en utilisant l’API GroupDocs.Search pour Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Traitement du langage Java – Créer un dictionnaire de synonymes avec GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Mots vides dans la recherche : ajouter des documents à l’index avec GroupDocs.Search Java](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)