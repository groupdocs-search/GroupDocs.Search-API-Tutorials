---
date: '2026-07-02'
description: Apprenez comment obtenir une licence temporaire pour GroupDocs.Search,
  ajouter des répertoires à l'index et ajouter des attributs de document personnalisés
  tout en gérant les nœuds du réseau de recherche Java.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Obtenir une licence temporaire GroupDocs – Nœuds maîtres de recherche (Java)
type: docs
url: /fr/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Obtenir une licence temporaire GroupDocs – Nœuds de recherche maîtres (Java)

Dans ce guide complet, vous **obtiendrez une licence temporaire pour GroupDocs.Search**, configurerez un réseau de recherche multi‑nœuds et apprendrez à **ajouter des répertoires à indexer** et à **ajouter des attributs de document personnalisés** en Java. Que vous construisiez un système de gestion de documents d’entreprise ou un catalogue de produits consultable, maîtriser ces étapes vous permet d’évaluer la plateforme sans restrictions et de faire évoluer rapidement vos capacités de recherche.

## Réponses rapides
- **Quelle est la première étape pour commencer à utiliser GroupDocs.Search ?** Obtenez une licence temporaire depuis le portail GroupDocs.  
- **Quel dépôt Maven héberge la bibliothèque ?** `https://releases.groupdocs.com/search/java/`.  
- **Comment ajouter des répertoires à indexer ?** Appelez l’assistant `addDirectoriesToIndex` sur le nœud maître.  
- **Puis-je ajouter des attributs de document personnalisés ?** Oui — invoquez `addAttribute` avec la clé du document et le nom de l’attribut.  
- **Comment fermer proprement les nœuds ?** Invoquez `closeNodes` pour libérer les ressources.

## Qu’est‑ce qu’une licence temporaire et pourquoi en ai‑je besoin ?
Une licence temporaire vous permet d’évaluer GroupDocs.Search sans aucune limitation d’évaluation. Elle est idéale pour le développement, les tests ou les projets de preuve de concept avant de s’engager dans un achat complet. La licence offre un accès complet aux fonctionnalités pendant une période limitée, vous permettant de mesurer les performances, de tester les points d’intégration et de vous assurer que la solution répond à vos exigences sans engagement financier.

## Prérequis

Avant de commencer, assurez‑vous d’avoir les prérequis suivants en place :

### Bibliothèques et dépendances requises
Pour travailler avec GroupDocs.Search pour Java, incluez les dépendances Maven nécessaires :
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
Vous pouvez également télécharger la dernière version directement depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Configuration de l’environnement
- Assurez‑vous d’avoir un JDK compatible installé (Java 8 ou supérieur).  
- Configurez votre IDE pour prendre en charge les projets Maven.

### Prérequis de connaissances
Une compréhension de base de la programmation Java et une familiarité avec la gestion de projets Maven seront utiles. Si vous êtes novice à ces concepts, envisagez d’explorer des ressources d’introduction pour commencer.

## Comment obtenir une licence temporaire
Une licence temporaire s’obtient en visitant le portail GroupDocs, en remplissant un court formulaire de demande, puis en plaçant le fichier `.lic` reçu dans le dossier `resources` de votre projet. Ensuite, initialisez la licence avec quelques lignes de code (voir l’extrait ci‑dessous). Pour le formulaire de demande, utilisez la page officielle : [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## Configuration de GroupDocs.Search pour Java

### Informations d’installation
Pour commencer à utiliser GroupDocs.Search pour Java dans votre projet, suivez les étapes Maven ci‑dessus ou téléchargez la dernière version directement depuis la page officielle des releases.

#### Étapes d’acquisition de licence
1. **Essai gratuit** – Explorez les fonctionnalités sans aucun engagement.  
2. **Licence temporaire** – Obtenez une clé à court terme pour les tests (voir la section ci‑dessus).  
3. **Achat** – Pour une utilisation en production, achetez une licence complète depuis la **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)**.

### Initialisation et configuration de base
Initialisez votre projet avec GroupDocs.Search comme suit :
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Cette étape d’initialisation est cruciale pour garantir que tous les composants fonctionnent de manière fluide au sein de votre réseau de recherche.

## Guide d’implémentation
Décomposons maintenant le processus en sections gérables, chacune se concentrant sur une fonctionnalité spécifique du déploiement et de la gestion des nœuds du réseau de recherche.

### Fonctionnalité 1 : Configuration du paramétrage
**Aperçu :** Configurer les paramètres de votre réseau de recherche est la première étape du déploiement des nœuds. Cette configuration implique de spécifier les chemins et les ports critiques pour le déploiement des nœuds.

#### Étapes d’implémentation :
##### Étape 1 : Définir le chemin de base et le port
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Étape 2 : Configurer le réseau de recherche
La fonction `configureSearchNetwork` prépare l’objet de configuration nécessaire au déploiement des nœuds.  
`Configuration` est une classe qui contient tous les paramètres tels que le dossier d’index, les ports réseau et les rôles des nœuds.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Paramètres :** Le chemin de base et le port sont utilisés pour localiser les ressources et établir les canaux de communication.  
- **Valeur de retour :** Un objet `Configuration` configuré adapté à vos besoins de déploiement.

### Fonctionnalité 2 : Déploiement du réseau de recherche
**Aperçu :** Le déploiement des nœuds est essentiel pour faire évoluer vos capacités de recherche à travers différents environnements ou segments de données.

#### Étapes d’implémentation :
##### Étape 1 : Déployer les nœuds
La fonction `deploySearchNetwork` initialise et renvoie un tableau de nœuds du réseau de recherche.  
`SearchNetworkNodes` représente chaque instance de nœud qui participe au cluster de recherche distribué.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Paramètres :** Le chemin de base, le port et la configuration sont utilisés pour déterminer l’environnement de déploiement.  
- **Valeur de retour :** Un tableau contenant des `SearchNetworkNodes` initialisés.

### Fonctionnalité 3 : Souscription aux événements du réseau
**Aperçu :** Surveiller les activités de votre réseau de recherche est crucial pour maintenir des performances et une fiabilité optimales.

#### Étapes d’implémentation :
##### Étape 1 : S’abonner aux événements du nœud maître
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Objectif :** Cette étape garantit que vous êtes informé des événements ou changements significatifs au sein de votre réseau de recherche.

### Fonctionnalité 4 : Indexation des documents
**Aperçu :** Ajouter des répertoires contenant des documents à indexer permet une récupération efficace des données à travers votre réseau.

#### Comment ajouter des répertoires à indexer
`addDirectoriesToIndex` est une méthode d’assistance qui enregistre les chemins de dossiers pour l’indexation sur le nœud maître.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Objectif :** Facilite l’accès rapide et la recherchabilité de tous les documents dans les répertoires spécifiés.

### Fonctionnalité 5 : Ajout d’attributs aux documents
**Aperçu :** Les attributs personnalisés enrichissent les métadonnées des documents, rendant les recherches plus flexibles et informatives.

#### Comment ajouter des attributs de document personnalisés
`addAttribute` ajoute un attribut de métadonnées personnalisé à un document spécifié dans l’index.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Paramètres :** Spécifiez le nœud, la clé du document et l’attribut à ajouter.  
- **Objectif :** Étend la fonctionnalité de recherche en enrichissant les documents avec des métadonnées supplémentaires.

### Fonctionnalité 6 : Récupération des documents indexés
**Aperçu :** Récupérez et listez efficacement les documents indexés afin d’assurer la précision et l’intégrité des données.

#### Étapes d’implémentation :
##### Étape 1 : Obtenir les documents indexés
```java
getIndexedDocuments(nodes[0]);
```  
- **Objectif :** Vérifie l’indexation réussie de tous les documents nécessaires au sein de votre réseau de recherche.

### Fonctionnalité 7 : Fermeture des nœuds du réseau
**Aperçu :** Fermer correctement les nœuds est crucial pour la gestion des ressources et la prévention des fuites de mémoire.

#### Étapes d’implémentation :
##### Étape 1 : Fermer tous les nœuds
`closeNodes` ferme tous les nœuds de recherche actifs et libère les ressources allouées.  
```java
closeNodes(nodes);
```  
- **Objectif :** Libère les ressources occupées par chaque nœud, assurant un processus d’arrêt propre.

## Pourquoi utiliser une licence temporaire pour GroupDocs.Search ?
Une licence temporaire offre **un accès complet aux fonctionnalités pendant 30 jours** et prend en charge jusqu’à **50 000 documents indexés** sans limitation de performance. Cela vous permet de mesurer la vitesse d’indexation, la latence des requêtes et la scalabilité sur des données réelles avant d’acheter une licence de production. Elle supprime également les filigranes d’évaluation, vous offrant une représentation fidèle des capacités du produit final.

## Cas d’utilisation courants
1. **Gestion de documents d’entreprise** – Indexez des millions de fichiers internes à travers les départements, permettant une recherche en texte intégral instantanée.  
2. **Plateformes e‑commerce** – Créez un catalogue de produits consultable qui couvre plusieurs entrepôts et flux de tiers.  
3. **Cabinets juridiques** – Organisez les dossiers de cas, les contrats et les preuves avec des métadonnées personnalisées pour une récupération rapide.

Les possibilités d’intégration avec d’autres systèmes incluent les plateformes CRM, les systèmes de gestion de contenu (CMS) et les outils d’analyse de données, tirant parti des fonctionnalités d’indexation et de recherche robustes fournies par GroupDocs.Search pour Java.

## Considérations de performance
Pour optimiser les performances lors de l’utilisation de GroupDocs.Search pour Java :
- **Optimiser la configuration** – Adaptez vos paramètres de configuration à votre environnement de déploiement spécifique.  
- **Surveiller l’utilisation des ressources** – Vérifiez régulièrement le CPU, la mémoire et les E/S pour éviter les goulets d’étranglement ou les fuites de mémoire.  
- **Suivre les meilleures pratiques** – Respectez les directives de gestion de la mémoire Java, assurant une utilisation efficace des ressources système.

## Questions fréquemment posées

**Q : Combien de temps une licence temporaire reste‑t‑elle valide ?**  
R : Les licences temporaires sont généralement valides pendant 30 jours, vous offrant amplement de temps pour évaluer le produit.

**Q : Puis‑je passer d’une licence temporaire à une licence complète sans réinstaller ?**  
R : Oui — remplacez le fichier de licence temporaire par le fichier de licence complet et redémarrez votre application.

**Q : Dois‑je ré‑indexer les documents après avoir appliqué une nouvelle licence ?**  
R : Non, l’index reste intact ; la licence ne régit que les droits d’utilisation.

**Q : Que se passe‑t‑il si j’oublie de fermer les nœuds ?**  
R : Des ressources non libérées peuvent entraîner des fuites de mémoire ; invoquez toujours `closeNodes` lors de l’arrêt.

**Q : Est‑il possible d’ajouter plus d’un attribut personnalisé par document ?**  
R : Absolument — appelez `addAttribute` plusieurs fois avec des noms d’attribut différents.

---

**Dernière mise à jour :** 2026-07-02  
**Testé avec :** GroupDocs.Search for Java 25.4  
**Auteur :** GroupDocs

## Tutoriels associés

- [Déployer un nœud de réseau de recherche en .NET avec GroupDocs pour l’indexation et la récupération efficaces de documents](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Comment implémenter un réseau de recherche avec GroupDocs.Search en .NET pour les systèmes de gestion de documents](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Configurer le réseau Aspose.Search et ajouter des attributs de document avec GroupDocs.Redaction pour .NET : Guide complet](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)