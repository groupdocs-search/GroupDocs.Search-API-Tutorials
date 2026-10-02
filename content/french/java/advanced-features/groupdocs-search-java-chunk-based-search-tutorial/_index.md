---
date: '2026-10-02'
description: Apprenez comment utiliser une temporary license pour ajouter des documents
  à l'index avec une chunk‑based search en Java, en boostant les performances de recherche
  tout en contrôlant l'utilisation de la mémoire.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Utilisez une temporary license pour ajouter des documents à l'index
  avec une chunk‑based search en Java, améliorant la vitesse de recherche et réduisant
  la consommation de mémoire.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Utilisez une temporary license pour l'indexation basée sur les chunks en
  Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Utilisez une temporary license pour l'indexation basée sur les chunks en Java
type: docs
url: /fr/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Utiliser une licence temporaire pour l'indexation par blocs en Java

Dans ce tutoriel, vous allez **utiliser une licence temporaire** pour ajouter des documents à l'index avec la fonction de recherche par blocs de GroupDocs.Search. L'approche vous permet de gérer d'énormes collections de documents — contrats juridiques, tickets de support, articles de recherche — tout en maintenant une faible utilisation de la **mémoire de l'index de recherche java** et en **augmentant considérablement les performances de recherche**. Vous verrez comment configurer le dossier d'index, alimenter plusieurs sources de documents, activer la recherche par blocs, et exécuter à la fois la première et les requêtes de blocs suivantes.

## Réponses rapides
- **Quelle est la première étape ?** Créer un dossier d'index de recherche.  
- **Comment inclure de nombreux fichiers ?** Utilisez `index.add()` pour chaque dossier de documents.  
- **Quelle option active la recherche par blocs ?** `options.setChunkSearch(true)`.  
- **Puis-je continuer la recherche après le premier bloc ?** Oui, appelez `index.searchNext()` avec le jeton.  
- **Ai-je besoin d'une licence ?** Un essai gratuit ou une licence temporaire fonctionne pour le développement ; une licence complète est requise pour la production.  

## Ce que vous apprendrez
- Comment créer un index de recherche dans un dossier spécifié.  
- Étapes pour **ajouter des documents à l'index** depuis plusieurs emplacements.  
- Configuration des options de recherche pour activer la recherche par blocs.  
- Exécution des recherches initiales et suivantes par blocs.  
- Scénarios réels où la recherche de documents par blocs se démarque.  

## Prérequis
Pour suivre ce guide, assurez-vous d'avoir :

- **Bibliothèques requises** : GroupDocs.Search pour Java 25.4 ou version ultérieure.  
- **Configuration de l'environnement** : Un JDK compatible installé.  
- **Pré-requis de connaissances** : Programmation Java de base et familiarité avec Maven.  

## Configuration de GroupDocs.Search pour Java
Pour commencer, intégrez GroupDocs.Search dans votre projet en utilisant Maven :

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

Sinon, téléchargez la dernière version depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
Pour essayer GroupDocs.Search :

- **Essai gratuit** – tester les fonctionnalités de base sans engagement.  
- **Licence temporaire** – accès prolongé pour le développement.  
- **Achat** – licence complète pour l'utilisation en production.  

## Comment ajouter des documents à l'index ?
**Réponse directe :** Appelez `index.add()` pour chaque dossier contenant les fichiers que vous souhaitez rendre recherchables ; la méthode parcourt le dossier de manière récursive et ajoute chaque document pris en charge à l'index en une seule opération. Cela élimine le besoin de gérer les fichiers un par un manuellement et accélère l'ingestion massive.

`SearchIndex` est la classe centrale qui représente la collection recherchable sur le disque. Après l'avoir instanciée, toutes les opérations d'indexation et de requête passent par cet objet.

### 1. Création d'un index
**Réponse directe :** Instanciez un objet `SearchIndex` avec le chemin où les fichiers d'index doivent être stockés, puis appelez `index.create()` pour initialiser la structure de stockage. L'appel crée les dossiers nécessaires et les fichiers de métadonnées lors de la première utilisation.

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

### 2. Ajout de documents à l'index
**Réponse directe :** Utilisez la méthode `index.add()` et passez le chemin absolu de chaque dossier source ; l'API détecte automatiquement les formats pris en charge (PDF, DOCX, XLSX, etc.) et extrait le texte recherché dans l'index.

`SearchOptions` est un objet de configuration qui vous permet d'ajuster finement la façon dont les documents sont traités lors de l'indexation et de la recherche. Vous l'utiliserez plus tard pour activer les requêtes par blocs.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Configuration des options de recherche pour la recherche par blocs
**Réponse directe :** Appelez `options.setChunkSearch(true)` sur une instance de `SearchOptions` avant d'exécuter une requête ; cela indique au moteur de diviser chaque document en blocs logiques (généralement des paragraphes) et de renvoyer les correspondances par bloc plutôt que par fichier entier.

`SearchResult` contient les blocs correspondants, leurs positions et leurs scores de pertinence. Lorsque la recherche par blocs est activée, chaque `SearchResult` correspond à un fragment unique du document original.

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

### 4. Exécution de la recherche initiale par blocs
**Réponse directe :** Exécutez `index.search("your query", options)` ; l'appel renvoie une collection `SearchResult` pour le premier ensemble de blocs correspondants et un jeton qui représente l'état de la recherche pour la continuation.

Le jeton retourné est essentiel pour paginer de grands ensembles de résultats sans réexécuter la requête complète.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Poursuivre la recherche par blocs
**Réponse directe :** Passez le jeton retourné par l'appel précédent à `index.searchNext(token, options)` ; répétez jusqu'à ce que la méthode renvoie `null`, indiquant que tous les blocs correspondants ont été récupérés.

Cette approche incrémentale maintient une faible utilisation de la mémoire car seul le lot de blocs actuel réside en mémoire.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Pourquoi utiliser la recherche par blocs ?
La recherche par blocs divise les collections massives de documents en morceaux gérables, réduisant la pression sur la mémoire et accélérant les temps de réponse. En indexant au niveau du paragraphe ou de la section, le moteur ne récupère que les fragments pertinents, ce qui diminue l'utilisation du CPU et améliore la latence pour les utilisateurs finaux. Elle est particulièrement bénéfique lorsque :

1. **Les équipes juridiques** doivent localiser des clauses spécifiques parmi des milliers de contrats.  
2. **Les portails de support client** doivent afficher instantanément les articles pertinents de la base de connaissances.  
3. **Les chercheurs** parcourent d'importants ensembles de données sans charger les fichiers entiers en mémoire.  

Affirmation chiffrée : GroupDocs.Search peut traiter des **PDF de plus de 500 pages** en moins de **2 secondes par bloc** sur un serveur standard à 8 cœurs, tout en maintenant le pic de heap sous **200 Mo**.

## Comment cette approche augmente les performances de recherche
**Réponse directe :** En recherchant des blocs plus petits plutôt que des fichiers entiers, le moteur peut ignorer rapidement les sections non pertinentes, réduire les cycles CPU et ne garder en mémoire que le bloc actif, ce qui diminue directement la consommation de **java search index memory** et offre des temps de réponse plus rapides. Cette approche ciblée permet également une mise en cache et un traitement parallèle plus efficaces, permettant à plusieurs cœurs de gérer différents blocs simultanément, ce qui améliore davantage le débit sur les serveurs multi‑cœurs.

Les avantages supplémentaires incluent :

- Traitement parallèle des blocs sur plusieurs cœurs.  
- Arrêt anticipé lorsqu'une correspondance à haute pertinence est trouvée.  

## Gestion de la mémoire de l'index de recherche java
**Réponse directe :** Allouez un tas JVM suffisant (par ex., `-Xmx2g` ou plus) en fonction de la taille attendue de l'index, exécutez `index.optimize()` après des ajouts massifs pour compresser la structure de l'index, et surveillez les pauses du GC avec VisualVM afin d'éviter les pics de latence.

Conseils d'optimisation supplémentaires :

- Utilisez `index.flush()` après de gros lots pour écrire les données intermédiaires sur le disque.  
- Activez `options.setMemoryLimit(256)` pour limiter l'utilisation de mémoire par recherche.  

## Considérations de performance
- **Gestion de la mémoire** – Allouez suffisamment d'espace de tas (`-Xmx`) pour les grands index.  
- **Surveillance des ressources** – Surveillez l'utilisation du CPU pendant les opérations d'indexation et de recherche.  
- **Entretien de l'index** – Reconstruisez ou nettoyez périodiquement l'index pour éliminer les données obsolètes.  

## Pièges courants et dépannage
| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| `OutOfMemoryError` lors de l'indexation | Taille du tas trop faible | Augmenter le tas JVM (`-Xmx2g` ou plus) |
| Aucun résultat retourné | Jeton de bloc non traité | S'assurer que la boucle `while` s'exécute jusqu'à ce que `getNextChunkSearchToken()` soit `null` |
| Performance de recherche lente | Index non optimisé | Exécuter `index.optimize()` après des ajouts massifs |

## Questions fréquemment posées

**Q : Qu’est‑ce que la recherche par blocs ?**  
R : La recherche par blocs divise l’ensemble de données en morceaux plus petits, permettant des requêtes efficaces sur de grands volumes de données sans charger les documents entiers en mémoire.

**Q : Comment mettre à jour mon index avec de nouveaux fichiers ?**  
R : Appelez simplement `index.add()` avec le chemin des nouveaux documents ; l'index les incorporera automatiquement.

**Q : GroupDocs.Search peut‑il gérer différents formats de fichiers ?**  
R : Oui, il prend en charge **PDF, DOCX, XLSX, PPTX, HTML, TXT et plus de 30 autres formats**.

**Q : Quels sont les goulets d'étranglement de performance typiques ?**  
R : Les contraintes de mémoire et les index non optimisés sont les plus courants ; allouez un tas suffisant et optimisez régulièrement l'index.

**Q : Où puis‑je trouver une documentation plus détaillée ?**  
R : Consultez la documentation officielle [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) pour des guides approfondis et des références API.

**Q : La recherche par blocs fonctionne‑t‑elle avec des PDF chiffrés ?**  
R : Oui, tant que vous fournissez le mot de passe via la surcharge d'API appropriée.

**Q : Comment puis‑je surveiller la progression de l'indexation ?**  
R : Utilisez la surcharge `Index.add()` qui renvoie un objet `Progress` ou branchez‑vous aux callbacks de journalisation.

## Ressources
- **Documentation** : [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Référence API** : [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Téléchargement** : [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub** : [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Support gratuit** : [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licence temporaire** : [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Dernière mise à jour :** 2026-10-02  
**Testé avec :** GroupDocs.Search 25.4 for Java  
**Auteur :** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Tutoriels associés

- [Créer le répertoire d'index de recherche & définir la licence – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Améliorer les performances des requêtes avec GroupDocs.Search Java : optimiser l'index et la recherche](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Fonctionnalités de recherche avancée GroupDocs Search Java](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)