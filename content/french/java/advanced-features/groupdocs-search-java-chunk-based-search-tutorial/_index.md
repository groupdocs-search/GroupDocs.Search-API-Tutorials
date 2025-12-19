---
date: '2025-12-19'
description: Apprenez à ajouter des documents à l'index et à activer la recherche
  par fragments en Java avec GroupDocs.Search, améliorant les performances pour de
  grands ensembles de documents.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Ajouter des documents à l'index avec une recherche basée sur les fragments
  en Java
type: docs
url: /fr/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Ajouter des documents à l'index avec la recherche par morceaux en Java

Dans le monde actuel axé sur les données, pouvoir **ajouter des documents à l'index** rapidement puis effectuer des recherches par morceaux est essentiel pour toute application qui gère de grandes collections de fichiers. Que vous travailliez avec des contrats juridiques, des archives de support client ou d'immenses bibliothèques de recherche, ce tutoriel vous montre exactement comment configurer GroupDocs.Search pour Java afin d'indexer les documents efficacement et de récupérer les informations pertinentes en morceaux faciles à gérer.

## Ce que vous allez apprendre
- Comment créer un index de recherche dans un dossier spécifié.  
- Étapes pour **ajouter des documents à l'index** depuis plusieurs emplacements.  
- Configuration des options de recherche pour activer la recherche par morceaux.  
- Réalisation de recherches initiales et ultérieures par morceaux.  
- Scénarios réels où la recherche de documents par morceaux fait la différence.

## Réponses rapides
- **Quelle est la première étape ?** Créez un dossier d'index de recherche.  
- **Comment inclure de nombreux fichiers ?** Utilisez `index.add()` pour chaque dossier de documents.  
- **Quelle option active la recherche par morceaux ?** `options.setChunkSearch(true)`.  
- **Puis-je continuer à rechercher après le premier morceau ?** Oui, appelez `index.searchNext()` avec le jeton.  
- **Ai‑je besoin d’une licence ?** Un essai gratuit ou une licence temporaire suffit pour le développement ; une licence complète est requise en production.

## Prérequis
Pour suivre ce guide, assurez‑vous d’avoir :

- **Bibliothèques requises** : GroupDocs.Search pour Java 25.4 ou version ultérieure.  
- **Configuration de l’environnement** : Un JDK compatible installé.  
- **Connaissances préalables** : Programmation Java de base et familiarité avec Maven.

## Installation de GroupDocs.Search pour Java
Pour commencer, intégrez GroupDocs.Search à votre projet avec Maven :

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

Vous pouvez également télécharger la dernière version depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
Pour essayer GroupDocs.Search :

- **Essai gratuit** – testez les fonctionnalités principales sans engagement.  
- **Licence temporaire** – accès prolongé pour le développement.  
- **Achat** – licence complète pour l’utilisation en production.

### Initialisation et configuration de base
Créez un index dans le dossier où vous souhaitez que les données recherchables résident :

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

## Comment ajouter des documents à l'index
Maintenant que l'index existe, l’étape logique suivante est de **ajouter des documents à l'index** depuis les emplacements où vos fichiers sont stockés.

### 1. Création d’un index
**Vue d’ensemble** : configurez un répertoire pour l’index de recherche.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Ajout de documents à l’index
**Vue d’ensemble** : importez les fichiers depuis plusieurs dossiers sources.

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

### 3. Configuration des options de recherche pour la recherche par morceaux
Activez la recherche par morceaux en ajustant l’objet options.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Exécution de la recherche initiale par morceaux
Lancez la première requête en utilisant les options activées pour les morceaux.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Poursuite de la recherche par morceaux
Itérez à travers les morceaux restants jusqu’à ce que la recherche soit terminée.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Pourquoi utiliser la recherche par morceaux ?
La recherche par morceaux découpe d’immenses collections de documents en parties gérables, réduisant la pression sur la mémoire et accélérant les temps de réponse. Elle est particulièrement utile lorsque :

1. **Les équipes juridiques** doivent localiser des clauses spécifiques parmi des milliers de contrats.  
2. **Les portails de support client** doivent afficher instantanément les articles pertinents de la base de connaissances.  
3. **Les chercheurs** parcourent d’importants ensembles de données sans charger les fichiers entiers en mémoire.

## Considérations de performance
- **Gestion de la mémoire** – Allouez suffisamment d’espace de tas (`-Xmx`) pour les gros index.  
- **Surveillance des ressources** – Gardez un œil sur l’utilisation du CPU pendant l’indexation et les opérations de recherche.  
- **Entretien de l’index** – Reconstruisez ou nettoyez périodiquement l’index pour éliminer les données obsolètes.

## Pièges courants & dépannage
| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| `OutOfMemoryError` pendant l’indexation | Taille du tas trop petite | Augmentez le tas JVM (`-Xmx2g` ou plus) |
| Aucun résultat retourné | Jeton de morceau non traité | Assurez‑vous que la boucle `while` s’exécute jusqu’à ce que `getNextChunkSearchToken()` soit `null` |
| Performances de recherche lentes | Index non optimisé | Exécutez `index.optimize()` après des ajouts en masse |

## FAQ

**Q : Qu’est‑ce que la recherche par morceaux ?**  
R : La recherche par morceaux divise le jeu de données en petites parties, permettant des requêtes efficaces sur de gros volumes de données sans charger les documents entiers en mémoire.

**Q : Comment mettre à jour mon index avec de nouveaux fichiers ?**  
R : Appelez simplement `index.add()` avec le chemin des nouveaux documents ; l’index les incorporera automatiquement.

**Q : GroupDocs.Search peut‑il gérer différents formats de fichiers ?**  
R : Oui, il prend en charge les PDF, DOCX, XLSX, PPTX et de nombreux autres formats courants.

**Q : Quels sont les goulets d’étranglement de performance typiques ?**  
R : Les contraintes de mémoire et les index non optimisés sont les plus fréquents ; allouez un tas suffisant et optimisez régulièrement l’index.

**Q : Où trouver une documentation plus détaillée ?**  
R : Consultez la documentation officielle [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) pour des guides approfondis et des références API.

## Ressources
- **Documentation** : [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Référence API** : [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Téléchargement** : [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub** : [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Support gratuit** : [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licence temporaire** : [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Dernière mise à jour :** 2025-12-19  
**Testé avec :** GroupDocs.Search 25.4 pour Java  
**Auteur :** GroupDocs  

---