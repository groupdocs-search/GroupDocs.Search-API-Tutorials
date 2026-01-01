---
date: '2025-12-20'
description: Apprenez comment activer la correction orthographique en Java avec GroupDocs.Search,
  ajouter des documents à l'index et définir le nombre maximal d’erreurs pour améliorer
  la précision de la recherche.
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: Comment activer l'orthographe en Java avec GroupDocs.Search
type: docs
url: /fr/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Comment activer la correction orthographique en Java avec GroupDocs.Search

Des résultats de recherche précis sont essentiels pour toute application moderne. Dans ce tutoriel, vous apprendrez **comment activer la correction orthographique** en Java avec GroupDocs.Search, afin que les utilisateurs obtiennent les bons résultats même lorsqu'ils saisissent mal leurs requêtes. Nous parcourrons la création d'un index, **l'ajout de documents à l'index**, la configuration des options d'orthographe et l'exécution d'une recherche qui corrige automatiquement les erreurs.

## Réponses rapides
- **Que signifie « comment activer la correction orthographique » ?** Cela active le correcteur orthographique intégré qui corrige les fautes de frappe des utilisateurs pendant une recherche.  
- **Quelle bibliothèque fournit cette fonctionnalité ?** GroupDocs.Search pour Java.  
- **Ai‑je besoin d’une licence ?** Une licence d'essai gratuite suffit pour l'évaluation ; une licence complète est requise pour la production.  
- **Puis‑je contrôler la tolérance ?** Oui – utilisez `setMaxMistakeCount` pour définir le nombre de fautes autorisées.  
- **Est‑elle adaptée aux gros index ?** Absolument – le moteur est optimisé pour l'indexation et la recherche haute performance.

## Qu’est‑ce que « comment activer la correction orthographique » dans GroupDocs.Search ?
Activer la correction orthographique indique au moteur de recherche de rechercher les termes corrects les plus proches lorsqu'une requête contient des erreurs. Cette fonctionnalité améliore considérablement l'expérience utilisateur en renvoyant des résultats pertinents même avec une saisie mal orthographiée.

## Pourquoi activer la correction orthographique dans les applications Java ?
- **Améliore la satisfaction des utilisateurs** – les utilisateurs n'ont pas besoin de taper parfaitement.  
- **Réduit le taux de rebond** – des résultats plus précis maintiennent les visiteurs engagés.  
- **Fonctionne dans tous les domaines** – des catalogues de bibliothèques aux recherches de produits e‑commerce.

## Prérequis
- Java Development Kit (JDK) installé.  
- Connaissances de base en Java et Maven.  
- Compréhension des concepts d'indexation.  
- Une version d'essai ou une clé de licence GroupDocs.Search.

### Configuration de GroupDocs.Search pour Java
Intégrez la bibliothèque dans votre projet Maven.

**Maven Setup**  
Ajoutez le référentiel et la dépendance à votre fichier `pom.xml` :

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

### Obtention de licence
Obtenez une licence d'essai gratuite pour l'évaluation. Pour une utilisation en production, achetez une licence complète ou demandez une clé temporaire sur le site officiel.

## Comment ajouter des documents à l'index
Créer un index est la base de toute application avec recherche. Voici un exemple minimal qui **ajoute des documents à l'index** depuis un dossier.

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

*Astuce :* Vérifiez que les chemins sont corrects et que l'application possède les permissions d'écriture sur le dossier d'index.

## Comment configurer la correction orthographique (définir le nombre maximal d'erreurs)
Vous pouvez affiner le correcteur orthographique en l'activant et en définissant la tolérance aux erreurs.

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

*Pourquoi `setMaxMistakeCount` est important :* Il définit le nombre de fautes que le moteur tolérera. Ajustez cette valeur en fonction des schémas d'erreurs typiques de votre domaine.

## Comment effectuer une recherche avec correction orthographique
Avec l'index prêt et les options d'orthographe configurées, lancez une requête pouvant contenir des erreurs.

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

L'appel `search()` renvoie un `SearchResult` qui contient les termes corrigés et les documents les plus pertinents.

## Applications pratiques
1. **Systèmes de bibliothèque :** Corriger les titres de livres ou les noms d'auteurs mal orthographiés.  
2. **Plateformes e‑commerce :** Corriger les fautes de frappe des utilisateurs dans les recherches de produits pour augmenter les conversions.  
3. **Systèmes de gestion de contenu :** Améliorer la récupération d'articles pour le personnel éditorial.

## Considérations de performance
- **Maintenez l'index à jour** – ré‑indexez régulièrement les fichiers nouveaux ou modifiés.  
- **Ajustez les paramètres de mémoire JVM** – allouez un tas suffisant pour les gros index.  
- **Surveillez l'utilisation des ressources** – ajustez les options du ramasse‑miettes si nécessaire.

## Questions fréquentes

**Q : Qu’est‑ce que GroupDocs.Search ?**  
R : C’est une bibliothèque Java qui offre une indexation rapide, des fonctionnalités de recherche avancées et une correction orthographique intégrée.

**Q : Comment obtenir une licence pour GroupDocs.Search ?**  
R : Visitez le site officiel pour télécharger une version d'essai gratuite ou acheter une licence complète.

**Q : Puis‑je intégrer GroupDocs.Search avec d’autres frameworks Java ?**  
R : Oui, il fonctionne avec Spring, Jakarta EE et toute application Java standard.

**Q : Quels sont les problèmes courants lors de la configuration d’un index ?**  
R : Chemins de dossiers incorrects, permissions de fichiers insuffisantes, ou dépendances manquantes dans `pom.xml`.

**Q : Comment la correction orthographique améliore‑t‑elle les résultats de recherche ?**  
R : Elle réécrit automatiquement les requêtes mal orthographiées en leurs termes corrects les plus proches, renvoyant des correspondances plus pertinentes.

## Ressources supplémentaires
- [Documentation](https://docs.groupdocs.com/search/java/)
- [Référence API](https://reference.groupdocs.com/search/java)
- [Téléchargement](https://releases.groupdocs.com/search/java/)
- [Référentiel GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Forum d'assistance gratuit](https://forum.groupdocs.com/c/search/10)
- [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)

---

**Dernière mise à jour :** 2025-12-20  
**Testé avec :** GroupDocs.Search 25.4  
**Auteur :** GroupDocs