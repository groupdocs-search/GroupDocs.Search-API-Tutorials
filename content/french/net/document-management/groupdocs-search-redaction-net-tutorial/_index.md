---
date: '2026-06-12'
description: Apprenez comment créer un index de recherche .NET et appliquer la rédaction
  aux PDF en utilisant GroupDocs.Search et GroupDocs.Redaction. Configuration, déploiement,
  indexation et recherche avancée expliqués.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: Créer un index de recherche .NET avec GroupDocs Search et GroupDocs.Redaction
  – Guide complet
type: docs
url: /fr/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Créer un index de recherche .NET avec GroupDocs Search et Redaction – Guide complet

Dans le paysage numérique actuel, la solution **creating a search index .NET** qui peut à la fois localiser rapidement l'information et protéger les données sensibles est une priorité majeure pour toute organisation. Ce tutoriel vous guide à travers la configuration d'un réseau GroupDocs.Search évolutif, le déploiement des nœuds, l'indexation des documents, et l'utilisation de GroupDocs.Redaction pour **apply redaction to PDF** files—le tout dans un environnement .NET.

## Réponses rapides
- **Quelle est la première étape pour créer un search index .NET ?** Définissez un chemin de base et un port, puis déployez les nœuds du réseau.  
- **Comment appliquer une redaction to PDF avec GroupDocs ?** Initialisez une instance `Redactor`, chargez le PDF, et appelez `Redact` avec les modèles souhaités.  
- **Puis-je exécuter le réseau de recherche sur plusieurs machines ?** Oui—déployez les nœuds sur des serveurs séparés et laissez le nœud maître coordonner l'indexation et les requêtes.  
- **Ai-je besoin d'une licence pour une utilisation en production ?** Une licence GroupDocs valide est requise pour la production ; une licence d'essai temporaire est disponible pour l'évaluation.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.7.2+, .NET Core 3.1+, et .NET 5/6/7 sont pleinement supportées.

## Qu'est-ce que “create search index .net” ?
*Creating a search index .NET* désigne la construction d'un référentiel consultable de métadonnées et de contenu de documents à l'aide de bibliothèques .NET, qui extrait le texte, tokenise les termes et les stocke dans une structure d'index optimisée. Cela permet des réponses instantanées aux requêtes sur des nœuds distribués, prenant en charge divers formats de fichiers et permettant une récupération de documents évolutive et haute performance dans les applications d'entreprise.

## Pourquoi utiliser GroupDocs Search et Redaction ensemble ?
GroupDocs.Search prend en charge **plus de 50 formats de fichiers**—y compris DOCX, PDF, PPTX et HTML—et peut indexer des documents de plusieurs centaines de pages sans charger le fichier complet en mémoire. Combiné avec GroupDocs.Redaction, qui peut **apply redaction to PDF** en moins de 200 ms par page, vous obtenez un pipeline de gestion de documents sécurisé et haute performance.

## Prérequis

### Bibliothèques et dépendances requises
Pour suivre ce tutoriel, installez les packages suivants :
- **GroupDocs.Search** pour .NET
- **GroupDocs.Redaction** pour .NET  

Vous pouvez utiliser l'une de ces méthodes pour installer les bibliothèques nécessaires :

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Recherchez « GroupDocs.Search » et « GroupDocs.Redaction » et installez la dernière version.

### Exigences de configuration de l'environnement
- .NET Framework 4.7.2 ou supérieur (ou .NET Core 3.1+)
- IDE Visual Studio (Community, Professional ou Enterprise)

### Prérequis de connaissances
- Programmation C# de base
- Concepts orientés objet
- Familiarité avec les configurations réseau et les systèmes de gestion de documents

## Configuration de GroupDocs.Redaction pour .NET

### Informations d'installation
Pour intégrer les fonctionnalités de redaction dans votre application, commencez par ajouter la bibliothèque GroupDocs.Redaction :

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Recherchez « GroupDocs.Redaction » et installez-le.

### Acquisition de licence
Pour commencer avec un essai gratuit ou une licence temporaire, suivez ces étapes :
- Visitez le [site Web GroupDocs](https://purchase.groupdocs.com/temporary-license/) pour demander une licence temporaire.  
- Pour les options d'achat, consultez leur [page de tarification](https://groupdocs.com/pricing).

Une fois que vous avez votre fichier de licence, appliquez-le dans la configuration de votre application :

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Initialisation de base
Pour initialiser GroupDocs.Redaction pour des opérations de base, utilisez le fragment de code suivant :

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Guide d'implémentation

### Configuration du paramétrage

#### Vue d'ensemble
Cette fonctionnalité configure votre réseau de recherche en utilisant un chemin de base et un numéro de port, formant la base de votre système de gestion de documents.

#### Ancre de définition
`SearchNetworkDeployment` est la classe qui orchestre le déploiement des nœuds de recherche à travers le réseau.

#### Étape 1 : Définir le chemin de base et le port  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### Étape 2 : Configurer le réseau
Utilisez la méthode `Configure` pour configurer le réseau de recherche avec le chemin et le port spécifiés :

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Déploiement des nœuds du réseau

#### Vue d'ensemble
Déployez des nœuds au sein de votre réseau de recherche configuré pour la recherche de documents distribuée.

#### Ancre de définition
`SearchNetworkNode` représente un nœud de recherche individuel qui communique avec le nœud maître.

#### Étape 1 : Initialiser le déploiement  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Abonnement aux événements du nœud maître

#### Vue d'ensemble
Abonnez-vous aux événements du nœud maître pour surveiller et gérer efficacement les opérations du réseau.

#### Ancre de définition
`SearchNetworkNodeEvents` fournit des rappels pour l'indexation, l'exécution de requêtes et la gestion des erreurs.

#### Étape 1 : Identifier le nœud maître
Sélectionnez le premier nœud comme votre maître :

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### Étape 2 : S'abonner aux événements
Abonnez-vous aux événements en utilisant :

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Indexation des documents

#### Vue d'ensemble
Indexez les documents pour des opérations de recherche efficaces. Cette étape est cruciale pour garantir que votre réseau puisse récupérer rapidement les données nécessaires.

#### Ancre de définition
`SearchIndex` est l'objet principal qui stocke les jetons recherchables et les métadonnées pour chaque fichier indexé.

#### Étape 1 : Ajouter des répertoires à l'index
Spécifiez les répertoires contenant vos documents :

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Fonctionnalité de recherche – Utilisation de base

#### Vue d'ensemble
Effectuez des opérations de recherche de base à travers les nœuds du réseau.

#### Réponse directe
Appelez `SearchNetwork.Query("your term")` sur le nœud maître pour récupérer instantanément les documents correspondants. La méthode renvoie une collection d'objets `SearchResult` qui incluent les chemins de fichiers et les scores de pertinence.  
`SearchNetwork.Query` est une méthode qui exécute une requête de recherche sur l'ensemble du réseau et renvoie les résultats correspondants.

#### Étape 1 : Définir les paramètres de recherche  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Fonctionnalité de recherche avancée

#### Vue d'ensemble
Utilisez des techniques de recherche avancées avec des paramètres personnalisables pour des résultats plus précis.

#### Réponse directe
Implémentez une méthode qui construit un objet `SearchOptions`, définit les propriétés `UseFuzzySearch`, `Highlight` et `PageSize`, puis le transmet à `SearchNetwork.QueryAdvanced`. Cela produit des résultats paginés et mis en évidence avec la correspondance floue activée.  
`SearchNetwork.QueryAdvanced` est une méthode qui exécute une requête avec des options avancées telles que la correspondance floue et la pagination.

#### Étape 1 : Implémenter la méthode de recherche avancée  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### Application de la redaction aux fichiers PDF

#### Vue d'ensemble
Sécurisez les informations sensibles en redactant le contenu PDF avant qu'il ne soit stocké ou partagé.

#### Réponse directe
Créez une instance `Redactor`, chargez le PDF cible, définissez un `RedactionPattern` (par ex., regex SSN), appelez `redactor.Apply(pattern)`, puis enregistrez le document redacté. Ce processus garantit que les données personnelles sont supprimées de façon permanente.

#### Ancre de définition
`Redactor` est la classe principale de GroupDocs.Redaction qui traite les documents et applique les règles de redaction.

#### Exemple de flux de travail (pas de nouveau bloc de code)  
1. Initialisez `Redactor` avec votre licence.  
2. Chargez le PDF en utilisant `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` représente une règle qui spécifie le texte ou le motif à redacter. Définissez des motifs tels que `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. Exécutez `redactor.Apply(pattern)`.  
5. Enregistrez le résultat avec `redactor.Save("sample_redacted.pdf")`.

### Applications pratiques

#### Cas d'utilisation réels
1. **Gestion de documents juridiques** – Recherchez efficacement les contrats et redactez automatiquement les identifiants des clients.  
2. **Dossiers de santé** – Localisez les notes des patients tout en assurant une redaction conforme à HIPAA du PHI.  
3. **Conformité d'entreprise** – Analysez les communications internes pour détecter les termes interdits et redactez avant l'archivage.

## Conclusion 
Ce guide fournit une voie complète pour **creating a search index .NET** qui s'adapte, indexe rapidement et protège les données grâce à la redaction. En configurant les nœuds, en indexant les documents, en exploitant les fonctionnalités de recherche avancées et en appliquant la redaction, les développeurs peuvent améliorer considérablement les flux de travail de gestion de documents tout en maintenant des normes de sécurité strictes.

## Questions fréquemment posées

**Q : Comment configurer un réseau de recherche distribué en .NET avec GroupDocs ?**  
R : Définissez un chemin de base et un port, puis appelez `SearchNetworkDeployment.Deploy()` pour lancer les nœuds maître et worker sur plusieurs machines.

**Q : Puis-je effectuer des recherches avancées avec plusieurs paramètres dans GroupDocs ?**  
R : Oui—utilisez `SearchOptions` pour combiner la correspondance floue, le support des caractères génériques et la mise en évidence des résultats dans une seule requête.

**Q : Est-il possible de surveiller l'activité du réseau sur le nœud maître ?**  
R : Absolument—abonnez‑vous à `SearchNetworkNodeEvents` tels que `IndexingCompleted` et `QueryExecuted` pour des informations en temps réel.

**Q : Comment appliquer la redaction aux fichiers PDF en utilisant GroupDocs ?**  
R : Initialisez un `Redactor`, chargez le PDF, définissez des objets `RedactionPattern` (expressions régulières ou chaînes littérales), appelez `Apply`, puis enregistrez le document désinfecté.

**Q : Quelle est la façon la plus simple d'améliorer les performances de recherche dans un environnement réseau ?**  
R : Indexez complètement votre ensemble de documents avant les requêtes, répartissez les nœuds pour exploiter le traitement parallèle, et ajustez `SearchOptions` pour le caching et la pagination.

---

**Dernière mise à jour :** 2026-06-12  
**Testé avec :** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**Auteur :** GroupDocs

## Tutoriels associés

- [Maîtriser l'indexation de documents .NET avec GroupDocs.Search : Guide complet](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Maîtriser l'indexation de documents et les requêtes de recherche avancées avec GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [Maîtriser GroupDocs Search et Redaction en .NET : Gestion avancée de documents](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)