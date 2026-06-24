---
date: '2026-05-02'
description: Apprenez à configurer la recherche et à activer les mises à jour en temps
  réel de la recherche avec GroupDocs.Search pour Java. Guide étape par étape sur
  la configuration du réseau, le déploiement des nœuds et l’indexation.
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: Comment configurer la recherche avec GroupDocs.Search en Java – Guide de configuration
  et de déploiement
type: docs
url: /fr/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# Comment configurer la recherche avec GroupDocs.Search en Java

Dans le monde numérique d'aujourd'hui, **comment configurer la recherche** efficacement peut faire ou défaire le succès d'un projet. Que vous manipuliez des milliers de contrats, d'articles de recherche ou de rapports internes, un réseau de recherche bien conçu vous permet de localiser le bon document en quelques secondes. Ce tutoriel vous guide à travers la configuration d'un réseau de recherche, le déploiement des nœuds et l'activation des **mises à jour de recherche en temps réel** avec GroupDocs.Search pour Java.

## Réponses rapides
- **Quel est le but principal d'un réseau de recherche ?** Pour distribuer l'indexation et le traitement des requêtes sur plusieurs nœuds afin d'assurer évolutivité et rapidité.  
- **Quelle version de la bibliothèque est requise ?** GroupDocs.Search for Java v25.4 ou plus récente.  
- **Ai‑je besoin d'une licence ?** Un essai gratuit suffit pour l'évaluation ; une licence commerciale est requise pour la production.  
- **Comment les mises à jour en temps réel sont‑elles gérées ?** En s'abonnant aux événements des nœuds qui se déclenchent lors des changements d'indexation.  
- **Puis‑je ajouter de nouveaux dossiers de documents à la volée ?** Oui—utilisez la méthode `addDirectories` de l'indexeur.

## Qu’est‑ce que « comment configurer la recherche » dans le contexte GroupDocs ?
Configurer la recherche signifie mettre en place un **réseau de recherche** qui sait où se trouvent vos documents, comment les nœuds communiquent et comment l'indexation est coordonnée. Une fois le réseau configuré, vous pouvez ajouter ou supprimer des nœuds sans interruption, garantissant un accès continu aux résultats de recherche à jour.

## Pourquoi utiliser GroupDocs.Search pour Java ?
- **Scalabilité :** Distribuer la charge de travail sur plusieurs machines.  
- **Mises à jour en temps réel :** Réfléter instantanément les fichiers nouvellement indexés sur le réseau.  
- **Facilité d'intégration :** Configuration Maven simple et API Java claires.  
- **Prêt pour l'entreprise :** Gère de grands corpus et des scénarios de requêtes complexes.

## Prérequis
- **Java Development Kit (JDK) 8+** installé.  
- **Maven** pour la gestion des dépendances.  
- Familiarité de base avec Java, Maven et les concepts de recherche.  

## Configuration de GroupDocs.Search pour Java

### Dépendance Maven
Ajoutez le dépôt et la dépendance à votre `pom.xml` :

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

**Téléchargement direct :** Vous pouvez également obtenir la bibliothèque depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
- **Essai gratuit :** Obtenez une licence d'essai pour explorer toutes les fonctionnalités.  
- **Licence temporaire :** Demandez une période d'évaluation prolongée.  
- **Licence commerciale :** Requise pour les déploiements en production.

### Initialisation de base
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Comment configurer le réseau de recherche en Java

### Étape 1 : Importer les packages requis
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### Étape 2 : Configurer le réseau
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Paramètres :** `basePath` pointe vers votre dossier de documents ; `basePort` est le port TCP utilisé pour la communication des nœuds.

## Déploiement des nœuds du réseau de recherche

### Étape 1 : Importer le package de déploiement
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### Étape 2 : Déployer les nœuds
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Nœud maître :** Coordonne les recherches et l'indexation sur tous les nœuds. Vous pouvez **configurer le nœud maître** avec des paramètres tels que l'allocation des shards et les vérifications de santé.

## S'abonner aux événements des nœuds pour les mises à jour de recherche en temps réel

### Étape 1 : Importer le package d'événements
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### Étape 2 : S'abonner aux événements du nœud maître
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Gestion des événements :** Active les **mises à jour de recherche en temps réel** chaque fois que des documents sont ajoutés, mis à jour ou supprimés.

## Ajout de répertoires pour l'indexation

### Étape 1 : Importer le package d'indexation
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### Étape 2 : Ajouter des répertoires de documents
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Indexation dynamique :** Utilisez la méthode `addDirectories` pour **ajouter des répertoires à l'index** à la volée sans redémarrer le réseau.

## Récupération des documents indexés

### Étape 1 : Importer le package de recherche
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### Étape 2 : Récupérer les informations du document
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **Gestion des shards :** Gère efficacement les grands ensembles de données en répartissant les documents sur plusieurs shards. Pour **optimiser la taille des shards**, surveillez les statistiques des shards et ajustez la configuration `shardSize` dans les futures versions.

## Pourquoi cela importe pour votre projet
Un réseau de recherche correctement configuré élimine les goulets d'étranglement, réduit la latence et garantit que les utilisateurs voient toujours la version la plus récente d'un document. Les mises à jour en temps réel et la capacité d'**ajouter des répertoires à l'index** sans interruption sont particulièrement précieuses pour les cabinets juridiques, les institutions de recherche et toute organisation qui gère des collections de documents en constante évolution.

## Applications pratiques
1. **Gestion documentaire d'entreprise :** Centraliser la recherche sur des millions de fichiers.  
2. **Cabinets juridiques :** Localiser rapidement les dossiers de cas, les contrats et les preuves.  
3. **Recherche académique :** Indexer les revues et les articles pour une récupération instantanée.

## Considérations de performance
- **Optimiser l'indexation :** Planifier des rafraîchissements d'index réguliers et purger les données obsolètes.  
- **Gestion de la mémoire :** Surveiller le tas JVM, surtout lors du traitement de gros shards.  
- **Planification de l'évolutivité :** Ajouter des nœuds à mesure que votre corpus grandit ; le réseau équilibre automatiquement la charge.  
- **Optimiser la taille des shards :** Des shards plus petits améliorent la latence des requêtes, tandis que des shards plus grands réduisent la surcharge. Ajustez en fonction de votre matériel et des modèles de requêtes.

## Problèmes courants et solutions
| Problème | Cause | Solution |
|----------|-------|----------|
| Les nœuds ne peuvent pas se connecter | Conflit de port ou pare-feu | Assurez-vous que `basePort` est ouvert et n'est pas utilisé par d'autres services |
| L'index ne se met pas à jour | Abonnement aux événements manquant | Appelez `SearchNetworkNodeEvents.subscribe(masterNode)` après le déploiement |
| Erreurs de dépassement de mémoire | Trop de gros shards chargés | Réduisez la taille des shards ou augmentez le tas JVM (`-Xmx` flag) |

## Questions fréquentes

**Q : Puis‑je ajouter de nouveaux répertoires après le démarrage du réseau ?**  
A : Oui—utilisez la méthode `indexer.addDirectories()` ; les événements abonnés propageront les mises à jour en temps réel.

**Q : Comment surveiller la santé des nœuds ?**  
A : Chaque `SearchNetworkNode` fournit des API de statut ; intégrez‑les à votre outil de surveillance préféré.

**Q : Est‑il possible d'exécuter le nœud maître sur une machine séparée ?**  
A : Absolument. Assurez‑vous simplement que tous les nœuds partagent le même `basePort` et peuvent se joindre via le réseau.

**Q : Quels formats de fichiers sont pris en charge ?**  
A : GroupDocs.Search prend en charge les PDF, Word, Excel, PowerPoint, le texte brut et de nombreux autres formats dès l'installation.

**Q : Dois‑je redémarrer le réseau après avoir ajouté un nouveau nœud ?**  
A : Non—les nœuds peuvent être ajoutés ou supprimés dynamiquement ; le nœud maître rééquilibrera les shards automatiquement.

## Conclusion
Maintenant que vous savez **comment configurer la recherche** avec GroupDocs.Search pour Java, vous pouvez créer des solutions de recherche documentaire rapides, évolutives et fiables qui suivent le rythme de la croissance de votre organisation. Appliquez ces modèles pour créer des expériences de recherche distribuées et en temps réel pour tout secteur.

**Dernière mise à jour :** 2026-05-02  
**Testé avec :** GroupDocs.Search for Java 25.4  
**Auteur :** GroupDocs