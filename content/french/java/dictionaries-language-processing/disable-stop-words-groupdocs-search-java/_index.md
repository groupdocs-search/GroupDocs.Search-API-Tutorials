---
date: '2026-02-19'
description: Apprenez comment désactiver les mots vides dans la recherche et ajouter
  des documents à l'index avec GroupDocs.Search pour Java, améliorant la précision
  des requêtes.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 'Mots vides dans la recherche : ajouter des documents à l''index avec GroupDocs.Search
  Java'
type: docs
url: /fr/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Mots vides dans la recherche : Ajouter des documents à l'index avec GroupDocs.Search Java

Si vous devez **ajouter des documents à l'index** tout en vous assurant qu'aucun terme important—en particulier les termes courants—n'est ignoré, vous êtes au bon endroit. Dans ce guide, nous vous montrerons comment **désactiver les mots vides dans la recherche** en utilisant GroupDocs.Search pour Java, afin que chaque jeton (même « on », « by » ou « the ») devienne recherchable et que vos résultats soient beaucoup plus précis.

## Réponses rapides
- **Que signifie « ajouter des documents à l'index » ?** Cela consiste à charger vos fichiers source dans un index searchable afin qu'ils puissent être interrogés efficacement.  
- **Pourquoi désactiver les mots vides ?** Pour inclure les mots courants (par ex., « on », « the ») dans les recherches lorsque ces termes sont pertinents pour votre domaine.  
- **Quelle version de la bibliothèque est requise ?** GroupDocs.Search pour Java 25.4 ou ultérieure.  
- **Ai‑je besoin d’une licence ?** Un essai gratuit suffit pour l’évaluation ; une licence permanente est requise pour la production.  
- **Puis‑je l’utiliser dans un projet Maven ?** Oui – il suffit d’ajouter le dépôt et la dépendance indiqués ci‑dessous.

## Que sont les mots vides dans la recherche et pourquoi voudriez‑vous les désactiver ?
Les mots vides sont des termes fréquents que de nombreux moteurs de recherche filtrent automatiquement afin d’accélérer les requêtes. Si cela améliore les performances pour les recherches Web génériques, cela peut nuire à la précision dans des domaines spécialisés—contrats juridiques, catalogues e‑commerce ou manuels techniques—où des mots comme « on », « by » ou « as » ont une réelle signification. Désactiver les mots vides vous permet de considérer chaque mot comme significatif, garantissant qu’aucun document pertinent ne soit omis.

## Comment fonctionne l’ajout de documents à l’index dans GroupDocs.Search ?
Lorsque vous ajoutez des documents, la bibliothèque lit chaque fichier, le tokenise et stocke les jetons dans une structure de données optimisée (l’index). Une fois indexé, le moteur peut récupérer les documents correspondants en millisecondes, même pour de grandes collections.

## Prérequis

- **Bibliothèques requises** : GroupDocs.Search pour Java 25.4 (ou plus récent).  
- **Environnement de développement** : IntelliJ IDEA, Eclipse ou tout IDE Java de votre choix.  
- **Connaissances de base** : Familiarité avec la syntaxe Java et le concept d’indexation.

## Installation de GroupDocs.Search pour Java

### Installation Maven

Si vous utilisez Maven, ajoutez ce qui suit dans votre `pom.xml` :

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

### Téléchargement direct

Sinon, téléchargez la dernière version depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Étapes d’obtention de licence
- **Essai gratuit** – commencez les tests immédiatement.  
- **Licence temporaire** – obtenez une clé à durée limitée pour toutes les fonctionnalités.  
- **Achat** – procurez‑vous une licence permanente pour la production.

## Initialisation de base et configuration

Créez une instance de `IndexSettings` pour contrôler le comportement de l’index :

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Comment désactiver les mots vides dans la recherche (Java)

La ligne suivante désactive le filtre intégré des mots vides :

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Paramètres* : `setUseStopWords` accepte un booléen.  
*Objectif* : Garantir que chaque mot—y compris les mots vides courants—soit indexé et recherchable.

## Comment ajouter des documents à l’index

### Définition du répertoire de sortie

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Spécification du répertoire des documents

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Désormais, chaque fichier dans `YOUR_DOCUMENT_DIRECTORY` est **ajouté à l'index** et prêt à être interrogé.

## Exécution d’une requête de recherche

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Comme les mots vides sont désactivés, le terme « on » sera pris en compte lors de la recherche, renvoyant des correspondances qui seraient autrement ignorées.

## Applications pratiques

1. **Recherche de documents d’entreprise** – S’assurer que la terminologie critique n’est pas filtrée.  
2. **Plateformes e‑commerce** – Améliorer la découverte de produits en indexant chaque mot des descriptions.  
3. **Outils de recherche juridique** – Capturer chaque terme juridique, même ceux habituellement traités comme mots vides.

## Considérations de performance

- **Conseils d’optimisation** : Mettez régulièrement à jour et purgez votre index pour maintenir une vitesse de recherche élevée.  
- **Utilisation des ressources** : Surveillez la taille du tas JVM ; les index volumineux peuvent nécessiter un réglage des paramètres de collecte des déchets.  
- **Gestion de la mémoire Java** : Utilisez des structures de données efficaces et envisagez le stockage hors‑tas pour des corpus très grands.

## Problèmes courants et solutions

| Symptom | Cause probable | Solution |
|---|---|---|
| Aucun résultat pour les mots courants | `setUseStopWords(true)` (par défaut) | Appelez `setUseStopWords(false)` comme indiqué ci‑dessus. |
| Erreurs de mémoire insuffisante lors de l’indexation | Indexation de trop nombreux fichiers volumineux en même temps | Indexez les fichiers par lots ; augmentez l’option JVM `-Xmx`. |
| La recherche renvoie des données obsolètes | L’index n’est pas rafraîchi après l’ajout de nouveaux fichiers | Appelez `index.update()` ou ré‑ajoutez les documents modifiés. |

## Questions fréquentes

**Q : Que sont les mots vides ?**  
R : Les mots vides sont des termes courants (par ex., « the », « is », « on ») que de nombreux moteurs de recherche ignorent pour accélérer les requêtes. Les désactiver vous permet de traiter chaque jeton comme recherchable.

**Q : Pourquoi désactiver les mots vides dans les index de recherche ?**  
R : Lorsque la correspondance exacte de phrase est requise—comme dans les documents juridiques ou techniques—chaque mot a du sens, il faut donc inclure les mots vides.

**Q : Comment GroupDocs.Search gère‑t‑il les grands ensembles de données ?**  
R : La bibliothèque utilise des structures de données optimisées et une indexation incrémentale pour garder la consommation de mémoire faible, même avec des millions de documents.

**Q : Puis‑je intégrer GroupDocs.Search à d’autres applications Java ?**  
R : Oui, l’API est conçue pour être facilement embarquée dans tout système basé sur Java, des services web aux applications de bureau.

**Q : Que faire si mes résultats de recherche ne sont pas précis ?**  
R : Vérifiez que l’index contient tous les documents requis (`add documents to index`), assurez‑vous que le filtrage des mots vides est désactivé si nécessaire, et envisagez de reconstruire l’index après des modifications majeures.

## Ressources supplémentaires

- **Documentation** : [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **Référence API** : [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Téléchargement** : [Obtenir la dernière version de GroupDocs.Search pour Java](https://releases.groupdocs.com/search/java/)  
- **Dépôt GitHub** : [Explorer sur GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Support gratuit** : [Rejoindre le forum GroupDocs](https://forum.groupdocs.com/c/search/10)  
- **Licence temporaire** : [Demander une licence temporaire](https://purchase.groupdocs.com/temporary-license/)

En suivant ce guide, vous savez maintenant comment **ajouter des documents à l'index** et **désactiver les mots vides dans la recherche** pour fournir des résultats plus précis dans vos applications Java.

---

**Dernière mise à jour :** 2026-02-19  
**Testé avec :** GroupDocs.Search pour Java 25.4  
**Auteur :** GroupDocs  

---