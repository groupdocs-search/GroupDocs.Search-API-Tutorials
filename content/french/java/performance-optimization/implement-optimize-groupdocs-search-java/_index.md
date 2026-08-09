---
date: '2026-07-07'
description: Apprenez comment supprimer l'index, réaliser une full text search Java,
  et optimiser les performances de recherche en utilisant GroupDocs.Search for Java.
  Guide étape par étape avec le network setup et l'indexation.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: Comment supprimer l'index et réaliser une full text search Java avec
  GroupDocs.Search. Suivez ce guide pour configurer un search network, créer un searchable
  index, et optimiser les performances de recherche.
og_title: Comment supprimer l'index et effectuer une recherche de texte avec GroupDocs.Search
  for Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: Comment supprimer l'index et effectuer une recherche de texte avec GroupDocs.Search
  for Java
type: docs
url: /fr/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Comment supprimer l'index et effectuer une recherche de texte avec GroupDocs.Search pour Java

Dans le monde actuel axé sur les données, **how to delete index** rapidement tout en offrant des capacités de recherche plein texte Java ultra‑rapides constitue un avantage concurrentiel. Que vous construisiez une base de connaissances interne, un référentiel de dossiers juridiques ou un catalogue de produits e‑commerce, un réseau de recherche bien optimisé peut améliorer considérablement la satisfaction des utilisateurs. Dans ce guide, vous apprendrez à **set up a search network**, **create a searchable index**, **optimize search performance**, et **delete documents from the index** lorsque cela est nécessaire — le tout en utilisant GroupDocs.Search pour Java.

## Réponses rapides
- **Quel est le principal objectif de GroupDocs.Search pour Java ?** Il fournit full‑text search sur plus de 50 formats de documents, permettant une récupération rapide des mots‑clés.  
- **Comment effectuer une recherche de texte dans un environnement distribué ?** Déployez un search network, indexez les documents sur un nœud maître, puis interrogez n’importe quel nœud.  
- **Puis‑je supprimer des documents de l'index sans le reconstruire ?** Oui, utilisez l'API Delete pour supprimer les fichiers sélectionnés, effectuant ainsi *how to delete index* sans re‑indexation complète.  
- **Quelle version de Java est requise ?** JDK 8 ou supérieur.  
- **Une licence est‑elle nécessaire pour la production ?** Une licence valide GroupDocs.Search est requise ; un essai gratuit est disponible.

## Qu'est‑ce que “perform text search” ?
Effectuer une recherche de texte signifie interroger un index full‑text pour récupérer les documents contenant les mots‑clés ou expressions spécifiés. GroupDocs.Search construit un index inversé qui rend ces recherches extrêmement rapides, même sur des milliers de fichiers.

## Pourquoi configurer un search network ?
Un search network répartit les charges d'indexation et de requêtes sur plusieurs nœuds, vous permettant de **optimize search performance**, de mettre à l'échelle horizontalement et de maintenir une haute disponibilité. Cette architecture est idéale pour les référentiels de documents de niveau entreprise où la latence et le débit sont importants.

## Comment implémenter et optimiser un Search Network avec GroupDocs.Search pour Java
Chargez votre configuration, démarrez un nœud maître, puis ajoutez des nœuds worker qui partagent le même chemin de base et le même port. Déployer le réseau de cette manière permet à n’importe quel nœud de gérer les requêtes d'indexation ou de recherche, offrant des temps de réponse cohérents même lorsque le nombre de documents atteint plusieurs centaines de milliers.

### Vue d'ensemble étape par étape
1. **Define a base configuration** qui inclut un répertoire partagé et un port TCP.  
2. **Start the master node** pour gérer l'index et coordonner les nœuds worker.  
3. **Add worker nodes** qui se connectent au maître, permettant une indexation et une recherche parallèles.  
4. **Monitor resource usage** et ajustez les paramètres du tas JVM pour maintenir une latence faible.

## Comment supprimer l'index dans GroupDocs.Search pour Java
`SearchNode` représente un nœud du réseau GroupDocs.Search qui gère les opérations d'indexation et de requête. La méthode `delete` supprime les documents spécifiés de l'index.

### Étapes de suppression directe
- Appelez la méthode `delete` sur l'instance `SearchNode`.  
- Fournissez un tableau de chemins de fichiers relatifs.  
- Validez les modifications ; l'index est rafraîchi instantanément et les recherches ultérieures ne renvoient plus les fichiers supprimés.

## Qu'est‑ce qu'un Search Network ?
Un **search network** est un cluster de nœuds interconnectés qui partagent un référentiel d'index commun, permettant l'indexation distribuée et l'exécution de requêtes. Il permet la mise à l'échelle horizontale et la tolérance aux pannes pour des collections de documents à grande échelle.

## Comment créer un index searchable (index documents java)
La méthode `add` indexe un document dans l'index de recherche. Ajoutez des documents au nœud maître en utilisant la méthode `add` ; le réseau propage les modifications à tous les nœuds worker. Cette approche garantit que chaque nœud peut répondre aux requêtes contre l'index le plus récent sans étapes de synchronisation supplémentaires.

### Actions clés
- Pointez le nœud maître vers le dossier contenant les fichiers source.  
- Invitez la routine d'indexation ; le réseau traite chaque fichier et met à jour l'index inversé.  
- Vérifiez que les fichiers d'index apparaissent dans le répertoire de stockage désigné.

## Comment supprimer les fichiers indexés (remove indexed files)
Lorsqu'un document devient obsolète, appelez l'API `delete` avec son chemin. Le système supprime les entrées du fichier de l'index inversé, libérant de l'espace de stockage et évitant les résultats obsolètes.

## Configuration de GroupDocs.Search pour Java
Pour commencer, intégrez GroupDocs.Search dans votre projet Java en utilisant la configuration suivante :

### Configuration Maven
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

### Téléchargement direct
Alternativement, vous pouvez [télécharger la dernière version directement depuis GroupDocs](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
GroupDocs propose un essai gratuit, qui vous permet d'évaluer ses fonctionnalités avant l'achat. Vous pouvez obtenir une licence temporaire en suivant les étapes sur leur [page d'achat](https://purchase.groupdocs.com/temporary-license/). Cela activera toutes les fonctionnalités pendant votre phase de test.

### Initialisation de base et configuration
Initialisez GroupDocs.Search dans votre application Java avec :

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## Guide d'implémentation

### Configuration du Search Network
**Overview:** Établissez un chemin de base et un port pour votre search network, permettant aux nœuds de communiquer efficacement.

#### Étape 1 : Définir la configuration de base
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parameters:**  
  - `basePath` : Chemin du répertoire pour les opérations du réseau.  
  - `basePort` : Numéro de port utilisé par le search network.

#### Étape 2 : Dépannage
Assurez‑vous que le port spécifié n’est pas bloqué par le pare‑feu ou utilisé par une autre application. Ajustez-le si nécessaire pour éviter les conflits.

### Déploiement des nœuds du Search Network
**Overview:** En utilisant votre configuration, déployez des nœuds à travers votre réseau pour l'indexation et la recherche distribuées.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Key Configuration Options:**  
  - **Base Path & Port** : Ces valeurs doivent correspondre à celles utilisées dans votre configuration initiale pour assurer la cohérence.

### Indexation des documents (`create searchable index`)
**Overview:** Ajoutez des documents à l'index de recherche efficacement en utilisant un nœud maître.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Purpose:**  
  - `masterNode` : Le nœud principal gérant l'indexation des documents.  
  - `documentsPath` : Chemin du répertoire contenant les documents.

#### Conseils de dépannage
Vérifiez que les chemins de vos documents sont corrects et accessibles. Assurez‑vous que les permissions permettent la lecture de ces répertoires.

### Recherche de texte dans le réseau (`perform text search`)
**Overview:** Effectuez des recherches de texte complètes à travers votre réseau indexé.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parameters:**  
  - `query` : Le texte que vous recherchez.  
  - `masterNode` : Nœud effectuant la recherche.

### Suppression de documents de l'index (`delete documents index`)
**Overview:** Supprimez des documents spécifiques de votre index en utilisant leurs chemins de fichier.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Method Purpose:**  
  - `node` : Le nœud cible pour les opérations de suppression.  
  - `filePaths` : Chemins des documents à retirer de l'index.

#### Dépannage
Assurez‑vous que les chemins de fichiers sont précis et que les fichiers existent dans votre répertoire. Si les problèmes persistent, vérifiez les permissions réseau et la connectivité.

## Applications pratiques
1. **Gestion de documents d'entreprise** : Rationalisez la récupération de connaissances internes.  
2. **Analyse de dossiers juridiques** : Localisez rapidement les dossiers pertinents à travers plusieurs référentiels.  
3. **Plateformes e‑commerce** : Accélérez la recherche de produits en indexant les descriptions et les avis.  
4. **Recherche académique** : Recherchez efficacement de grandes bibliothèques numériques de papiers et de thèses.  
5. **Systèmes de support client** : Réduisez le temps de réponse en permettant aux agents de rechercher instantanément les tickets précédents.

## Considérations de performance
- **Optimiser la vitesse d'indexation** : Ajoutez de nouveaux documents de façon incrémentale pendant les heures creuses pour maintenir une latence faible.  
- **Directives d'utilisation des ressources** : Surveillez le CPU et la mémoire, surtout lors de la mise à l'échelle du nombre de nœuds.  
- **Gestion de la mémoire Java** : Ajustez les paramètres du tas JVM en fonction de votre charge de travail (par ex., `-Xmx2g` pour des index de taille moyenne).

## Conclusion
En suivant ce guide, vous avez appris comment **set up a search network**, **create a searchable index**, **perform text search**, et **delete documents index** en utilisant GroupDocs.Search pour Java. Ces capacités permettent une récupération de documents rapide et fiable dans des environnements distribués.

**Prochaines étapes**
- Expérimentez différentes configurations de nœuds pour trouver l'équilibre optimal pour votre charge de travail.  
- Approfondissez les options d'indexation avancées telles que les analyseurs personnalisés et le réglage de la pertinence.  
- Explorez l'intégration avec d'autres produits GroupDocs pour un traitement de documents de bout en bout.

## Questions fréquentes

**Q : Quel est le cas d'utilisation principal de GroupDocs.Search pour Java ?**  
R : Il fournit full‑text search sur de nombreux formats de documents, vous permettant de **perform text search** dans de grands référentiels.

**Q : Comment améliorer la vitesse de recherche dans un grand réseau ?**  
R : Déployez des nœuds supplémentaires, ajustez le tas JVM, et planifiez l'indexation pendant les périodes de faible trafic pour **optimize search performance**.

**Q : Est‑il possible de supprimer un seul document sans ré‑indexer toute la collection ?**  
R : Oui, utilisez l'API **delete documents index** comme illustré dans l'exemple de code pour supprimer des fichiers spécifiques.

**Q : Ai‑je besoin d’une licence pour le développement ?**  
R : Une licence d'essai gratuite suffit pour les tests ; une licence commerciale est requise pour les déploiements en production.

**Q : Puis‑je indexer des PDFs, des fichiers Word et des e‑mails ensemble ?**  
R : Absolument—GroupDocs.Search prend en charge un large éventail de formats dès le départ.

**Dernière mise à jour :** 2026-07-07  
**Testé avec :** GroupDocs.Search pour Java 25.4  
**Auteur :** GroupDocs

## Tutoriels associés

- [Comment indexer du texte en Java avec le guide GroupDocs.Search](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [Optimiser les performances de recherche avec les techniques d'indexation avancées dans GroupDocs.Search pour Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [Améliorer les performances des requêtes avec GroupDocs.Search Java : Optimiser l'index et la recherche](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)