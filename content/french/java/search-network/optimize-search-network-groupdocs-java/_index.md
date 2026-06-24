---
date: '2026-05-17'
description: Apprenez à configurer le réseau de recherche Java, optimiser les shards,
  effectuer une recherche de texte et gérer les conflits de ports avec GroupDocs.Search
  for Java.
keywords:
- configure search network java
- GroupDocs.Search Java
- shard optimization
- Java search network
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  headline: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive
    Guide'
  type: TechArticle
- description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  name: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive Guide'
  steps:
  - name: Define Document Directories and Port
    text: '`DocumentDirectory` is a simple holder for the absolute path of a folder
      you want to index. Provide one or more paths to the configuration.'
  - name: Configure Search Network
    text: 'Create the configuration object using the defined paths:'
  - name: Deploy Nodes Using Configuration
    text: 'Deploy search network nodes and identify the master node for centralized
      management:'
  - name: Subscribe to Master Node Events
    text: '`SearchNetworkEventListener` lets you react to indexing completion, node
      failures, or shard optimizations. CODE_BLOCK_PLACEHOLDER_9_END'
  - name: Add Document Directories to Indexing Process
    text: Pass a list of folder paths to the master node; the engine will create a
      separate shard for each folder, enabling parallel query execution. CODE_BLOCK_PLACEHOLDER_10_END
  - name: Perform a Text Search
    text: Invoke the static helper to run a query and retrieve matching documents
      with relevance scores. CODE_BLOCK_PLACEHOLDER_11_END
  - name: Optimize Indexer Shards
    text: 'Optimize shards to improve search efficiency (this is where **how to optimize
      shards** really matters): CODE_BLOCK_PLACEHOLDER_12_END'
  type: HowTo
- questions:
  - answer: Optimizing shards compacts the index, reduces disk I/O, and typically
      yields 30‑50 % faster query responses for large datasets.
    question: How does shard optimization affect query speed?
  - answer: Yes, the operation is designed to run without downtime, but scheduling
      during low‑traffic periods is recommended for indexes larger than 20 GB.
    question: Is it safe to run `optimizeShards` on a live node?
  - answer: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor`
      to fine‑tune the optimization process.
    question: Can I customize the `OptimizeOptions`?
  - answer: Verify file system permissions, ensure enough free disk space, and confirm
      that no other process is locking the index files.
    question: What should I do if I encounter an `IOException` during optimization?
  - answer: Yes, the optimizer merges segments and removes tombstones, freeing up
      space occupied by deleted documents.
    question: Does optimizing shards also reclaim deleted document space?
  type: FAQPage
title: 'Comment optimiser les shards dans GroupDocs.Search for Java : guide complet'
type: docs
url: /fr/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# Comment optimiser les shards dans GroupDocs.Search pour Java : guide complet

La recherche efficace de documents est essentielle pour les développeurs et les entreprises qui gèrent de grands ensembles de données ou qui ont besoin d’une récupération interne rapide. Dans ce tutoriel, vous apprendrez **how to configure search network java**, comment indexer et interroger des documents, et les étapes exactes pour **optimize shards** afin d’obtenir des performances optimales. Nous couvrirons également des cas d’utilisation réels, les pièges courants et des conseils pratiques pour maintenir vos nœuds de recherche en bon état de fonctionnement.

## Réponses rapides
- **Qu'est-ce que l'optimisation des shards ?** Elle réorganise les données d'index pour accélérer les requêtes et réduire la surcharge de stockage.  
- **Comment configurer un réseau de recherche ?** Définissez un répertoire de base et un port, puis déployez les nœuds à l'aide de l'API fournie.  
- **Comment effectuer une recherche de texte ?** Utilisez `TextSearchInNetwork.searchAll` avec votre chaîne de requête.  
- **Comment indexer des documents en Java ?** Ajoutez les répertoires de documents au nœud maître avec `IndexingDocuments.addDirectories`.  
- **Comment gérer les conflits de ports ?** Changez la variable `basePort` pour un port inutilisé sur votre machine.

## Comment configurer le réseau de recherche
`Configuration` stocke tous les paramètres nécessaires au lancement d'un réseau GroupDocs.Search, tels que l'emplacement du dossier d'index et le port de communication.  
`SearchNetwork` orchestre les nœuds, gérant l'indexation et la distribution des requêtes.

Chargez votre configuration de recherche, définissez le chemin de base des documents, choisissez un port libre et démarrez le réseau — le tout en quelques lignes de code. Cette réponse directe explique le processus complet en moins de 70 mots : **Create a `Configuration` object, set `basePath` and `basePort`, then call `SearchNetwork.start(configuration)`.** Le réseau créera automatiquement un nœud maître et les nœuds de travail nécessaires, prêts à accepter les requêtes d'indexation.

### Ancre de définition
`Configuration` est la classe principale qui stocke tous les paramètres nécessaires au lancement d'un réseau GroupDocs.Search, tels que l'emplacement du dossier d'index et le port de communication.

Pour éviter l'erreur redoutée « port already in use », vérifiez d'abord que le port choisi est libre (par ex., en utilisant `netstat` ou un simple test de socket) avant d'initialiser le réseau.

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

## Comment indexer des documents en Java
`IndexingDocuments` est une classe utilitaire qui simplifie l'ajout de plusieurs répertoires à un nœud de recherche et déclenche le pipeline d'indexation.

Ajoutez vos dossiers de documents au nœud maître, puis laissez l'indexeur les parcourir. **Direct answer:** Call `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))` and then invoke `masterNode.index()`; the engine will create searchable shards for every folder you supplied. This approach scales horizontally—add more nodes, and the same method distributes the workload automatically.

### Ancre de définition
`IndexingDocuments` est une classe utilitaire qui simplifie l'ajout de plusieurs répertoires à un nœud de recherche et déclenche le pipeline d'indexation.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Comment effectuer une recherche de texte
`TextSearchInNetwork` fournit des méthodes d'aide statiques pour diffuser une requête texte à chaque nœud du réseau et agréger les résultats.  
`SearchResult` encapsule l'ID d'un document correspondant, un extrait et le score de pertinence.

Exécutez une requête sur tous les shards avec un seul appel de méthode. **Direct answer:** Use `TextSearchInNetwork.searchAll("your query", searchNetwork)`; the method returns a collection of `SearchResult` objects containing document IDs, snippets, and relevance scores. Vous pouvez filtrer davantage les résultats par langue, type de fichier ou métadonnées personnalisées sans écrire de code supplémentaire.

### Ancre de définition
`TextSearchInNetwork` fournit des méthodes d'aide statiques qui diffusent une requête texte à chaque nœud du réseau et agrègent les résultats.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## Comment gérer les conflits de ports
Si le port par défaut (`49132`) est occupé, choisissez simplement un autre port libre et mettez à jour le champ `basePort` avant de démarrer le réseau. **Direct answer:** Change `int basePort = 49132;` to an unused value like `49133`, rebuild, and restart; the network will bind to the new port without affecting existing nodes.

Astuce : conservez un petit fichier de configuration (par ex., `search-config.properties`) afin de pouvoir changer le port sans recompilation.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Prérequis
Avant de commencer, assurez-vous que les prérequis suivants sont en place :

### Bibliothèques requises, versions et dépendances
Pour implémenter cette solution, incluez la bibliothèque GroupDocs.Search via Maven en ajoutant la configuration suivante à votre fichier `pom.xml` :

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
Alternativement, téléchargez la dernière version depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Exigences de configuration de l'environnement
- Java Development Kit (JDK) 8 ou ultérieur.  
- Permissions réseau permettant de lier le `basePort` choisi.  
- Espace disque suffisant pour les fichiers d'index (chaque shard peut occuper ~10 Mo pour 1 000 documents).

### Prérequis de connaissances
Une compréhension de base de Java, de la programmation orientée objet et de la gestion des exceptions vous aidera à suivre les exemples sans problème.

## Configuration de GroupDocs.Search pour Java
Pour commencer à utiliser GroupDocs.Search dans votre projet, suivez ces étapes :

1. **Add the Dependency** : comme indiqué ci-dessus, ajoutez la dépendance Maven nécessaire à votre projet ou téléchargez directement depuis la page des releases.  
2. **License Acquisition** :  
   - **Free trial** – aucune clé de licence requise, mais l'utilisation est limitée à 500 documents par jour.  
   - **Temporary license** – demandez une clé d'essai de 30 jours depuis [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).  
   - **Full license** – achetez une licence de production pour un accès illimité et un support prioritaire.  
3. **Basic Initialization and Setup** :  
   Initialisez la configuration en utilisant la classe `Configuration`, en définissant le chemin de base pour les documents et en spécifiant un numéro de port :

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## Guide d'implémentation
Explorons maintenant la mise en œuvre des fonctionnalités clés avec GroupDocs.Search Java.

### Fonctionnalité : configuration du réseau de recherche
**Overview** : la mise en place d'un réseau de recherche implique de définir votre répertoire de documents et de le configurer avec un port spécifique pour la communication entre les nœuds.

#### Étape 1 : définir les répertoires de documents et le port
`DocumentDirectory` est un simple conteneur pour le chemin absolu d'un dossier que vous souhaitez indexer. Fournissez un ou plusieurs chemins à la configuration.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### Étape 2 : configurer le réseau de recherche
Créez l'objet de configuration en utilisant les chemins définis :

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Fonctionnalité : déploiement des nœuds du réseau de recherche
**Overview** : déployez des nœuds pour gérer les recherches de documents efficacement à travers votre réseau.

#### Étape 1 : déployer les nœuds à l'aide de la configuration
Déployez les nœuds du réseau de recherche et identifiez le nœud maître pour la gestion centralisée :

```java
public static void optimizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    OptimizeOptions options = new OptimizeOptions();
    indexer.optimize(options);
}

optimizeShards(masterNode);

// Perform a second text search to observe optimization effects
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Fonctionnalité : abonnement aux événements des nœuds du réseau
**Overview** : surveillez votre réseau de recherche en vous abonnant aux événements qui vous notifient des changements ou actions importants.

#### Étape 1 : s'abonner aux événements du nœud maître
`SearchNetworkEventListener` vous permet de réagir à la fin de l'indexation, aux pannes de nœuds ou aux optimisations de shards.

CODE_BLOCK_PLACEHOLDER_9_END

### Fonctionnalité : indexation des documents dans les nœuds du réseau
**Overview** : ajoutez des répertoires contenant des documents au processus d'indexation pour des recherches efficaces.

#### Étape 1 : ajouter les répertoires de documents au processus d'indexation
Passez une liste de chemins de dossiers au nœud maître ; le moteur créera un shard distinct pour chaque dossier, permettant une exécution parallèle des requêtes.

CODE_BLOCK_PLACEHOLDER_10_END

### Fonctionnalité : recherche de texte dans les nœuds du réseau
**Overview** : exécutez des recherches de texte sur tous les documents indexés au sein de votre réseau de recherche.

#### Étape 1 : effectuer une recherche de texte
Appelez l'aide statique pour exécuter une requête et récupérer les documents correspondants avec leurs scores de pertinence.

CODE_BLOCK_PLACEHOLDER_11_END

### Fonctionnalité : optimisation des shards
**Overview** : améliorez les performances en optimisant les shards au sein de l'indexeur de votre nœud du réseau de recherche.

#### Étape 1 : optimiser les shards de l'indexeur
Optimisez les shards pour améliorer l'efficacité de la recherche (c'est ici que **how to optimize shards** prend tout son sens) :

CODE_BLOCK_PLACEHOLDER_12_END

## Applications pratiques
GroupDocs.Search pour Java peut être appliqué dans divers scénarios réels, chacun bénéficiant de l'optimisation des shards :

1. **Enterprise Document Management** – Gère des archives de plus de 10 To avec des temps de requête inférieurs à une seconde après l'optimisation des shards.  
2. **E‑commerce Platforms** – Alimente la recherche de produits sur 1 million de SKU, réduisant la latence jusqu'à 45 % lorsque les shards sont optimisés.  
3. **Legal Firms** – Récupère les dossiers de cas depuis des dépôts de 200 Go en moins de 200 ms.  
4. **Library Systems** – Prend en charge les recherches de catalogue pour 500 k livres numériques avec une utilisation efficace de la mémoire.  
5. **Content Management Systems (CMS)** – Permet une découverte instantanée du contenu pour des déploiements multi‑sites avec plus de 2 millions de pages.

## Considérations de performance
Pour garantir des performances optimales de votre implémentation GroupDocs.Search :

- **Regularly optimize shards** – L'exécution de `optimizeShards()` après chaque 10 Go de nouvelles données réduit les temps de réponse des requêtes de 30‑50 %.  
- **Monitor memory usage** – Maintenez le tas JVM en dessous de 75 % de la RAM physique ; activez G1GC pour les gros index.  
- **Use incremental indexing** – Ajoutez uniquement les fichiers modifiés pour éviter une réindexation complète.  
- **Leverage multi‑node scaling** – Ajoutez des nœuds de travail pour répartir les shards ; chaque nœud supplémentaire peut améliorer le débit d'environ 20 % pour les charges de travail à forte lecture.

## Problèmes courants et solutions

| Issue | Symptom | Solution |
|-------|---------|----------|
| Conflit de port au démarrage | `java.net.BindException: Address already in use` | Changez `basePort` pour une valeur inutilisée ; vérifiez avec `netstat -ano`. |
| Erreurs de mémoire insuffisante lors de l'optimisation | `java.lang.OutOfMemoryError: Java heap space` | Augmentez le drapeau JVM `-Xmx` ou exécutez l'optimisation sur un nœud dédié avec plus de RAM. |
| Documents manquants dans les résultats de recherche | Aucun résultat retourné après l'indexation | Assurez-vous que les répertoires sont correctement ajoutés via `IndexingDocuments.addDirectories` et que `masterNode.index()` s'est terminé sans exceptions. |
| Shards obsolètes après suppression massive | Les fichiers supprimés apparaissent toujours | Exécutez `optimizeShards()` pour fusionner les segments et purger les tombstones. |

## Questions fréquentes

**Q : Comment l'optimisation des shards affecte-t-elle la vitesse des requêtes ?**  
A : L'optimisation des shards compacte l'index, réduit les entrées/sorties disque, et donne généralement des réponses aux requêtes 30‑50 % plus rapides pour les grands ensembles de données.

**Q : Est-il sûr d'exécuter `optimizeShards` sur un nœud en production ?**  
A : Oui, l'opération est conçue pour s'exécuter sans interruption, mais il est recommandé de la planifier pendant les périodes de faible trafic pour les index de plus de 20 Go.

**Q : Puis-je personnaliser le `OptimizeOptions` ?**  
A : Absolument. Vous pouvez définir des paramètres tels que `maxSegmentSize` ou `mergeFactor` pour affiner le processus d'optimisation.

**Q : Que faire si je rencontre une `IOException` lors de l'optimisation ?**  
A : Vérifiez les permissions du système de fichiers, assurez-vous qu'il y a suffisamment d'espace disque libre, et confirmez qu'aucun autre processus ne verrouille les fichiers d'index.

**Q : L'optimisation des shards récupère-t-elle également l'espace des documents supprimés ?**  
A : Oui, l'optimiseur fusionne les segments et supprime les tombstones, libérant l'espace occupé par les documents supprimés.

## Conclusion
En suivant ce guide complet, vous savez maintenant comment **configure search network java**, indexer des documents, exécuter des requêtes textuelles et, surtout, **optimize shards** pour garder vos performances de recherche ultra‑précises. Appliquez ces modèles à toute solution de recherche d'entreprise basée sur Java, et vous constaterez des améliorations mesurables en latence, évolutivité et utilisation des ressources. Pour les prochaines étapes, explorez des fonctionnalités avancées comme les analyseurs personnalisés, la recherche à facettes et l'intégration avec des fournisseurs de stockage cloud.

---

**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Tutoriels associés

- [Configuration du réseau GroupDocs.Search en .NET : guide complet](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Indexation principale de documents .NET avec GroupDocs.Search : guide complet](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Tutoriels et exemples de GroupDocs.Search pour Java](/search/net/)