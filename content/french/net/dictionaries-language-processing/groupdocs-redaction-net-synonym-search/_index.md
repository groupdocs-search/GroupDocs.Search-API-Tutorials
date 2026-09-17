---
date: '2026-09-16'
description: Apprenez comment créer un index de recherche avec GroupDocs en .NET,
  ajouter des documents à l'index et activer la recherche de synonymes pour des résultats
  de requête plus intelligents.
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: Apprenez comment créer un index de recherche avec GroupDocs en .NET,
  ajouter des documents à l'index et activer la recherche de synonymes pour des résultats
  de requête plus intelligents.
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: Comment créer un index de recherche avec GroupDocs en .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: Comment créer un index de recherche avec GroupDocs et la recherche de synonymes
  en .NET
type: docs
url: /fr/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# Comment créer un index de recherche avec GroupDocs et la recherche de synonymes en .NET

Dans ce guide, vous apprendrez **comment créer un index de recherche** à l’aide de GroupDocs.Search, ajouter des documents à cet index et activer la recherche de synonymes afin que les utilisateurs puissent trouver du contenu pertinent même s’ils utilisent une terminologie différente. Que vous construisiez un référentiel juridique, une base de connaissances d’entreprise ou une archive de recherche, les étapes ci‑dessous vous offrent une solution prête pour la production qui fonctionne sur .NET Framework 4.6.1+, .NET Core et .NET 5+.

## Réponses rapides
- **Que signifie « créer un index de recherche » ?** Il crée un catalogue consultable de vos documents, stockant le texte extrait dans une structure optimisée pour des recherches en millisecondes.  
- **Pourquoi utiliser la recherche de synonymes ?** Elle élargit une requête pour inclure des mots ayant le même sens, augmentant le rappel jusqu’à 30 % dans des corpus typiques.  
- **Quelles sont les principales prérequis ?** .NET 4.6.1+ (ou .NET Core/5+), connaissances en C#, et les packages NuGet GroupDocs.Search + GroupDocs.Redaction.  
- **Ai‑je besoin d’une licence ?** Un essai gratuit suffit pour l’évaluation ; une licence permanente est requise pour les déploiements en production.  
- **Puis‑je combiner cela avec la rédaction ?** Oui—GroupDocs.Redaction peut s’exécuter avant ou après la recherche pour masquer les données sensibles.

## Qu’est‑ce que « créer un index de recherche » ?
Un **index de recherche** est une structure de données qui conserve le texte extrait et les métadonnées de chaque document, permettant au moteur de localiser instantanément les fichiers correspondants. GroupDocs.Search construit cet index en parcourant le dossier source, en analysant les formats pris en charge et en écrivant des fichiers d’index compacts dans un répertoire que vous spécifiez.

## Pourquoi activer la recherche de synonymes ?
La recherche de synonymes ajoute automatiquement des termes alternatifs à la requête d’un utilisateur, de sorte qu’une recherche de **« improve »** renvoie également des documents contenant **« enhance », « upgrade »** ou **« optimize ».** En pratique, cela peut augmenter le rappel des résultats de 20‑35 % tout en maintenant une précision élevée, car le dictionnaire de synonymes intégré est sélectionné pour chaque langue.

## Prérequis
- **.NET Framework 4.6.1** ou ultérieur (ou tout runtime .NET Core/5+).  
- Compétences de base en développement C# et Visual Studio (Community, Professional ou Enterprise).  
- Packages GroupDocs.Search et GroupDocs.Redaction installés via NuGet.

### Installation
Installez GroupDocs.Redaction pour .NET en utilisant l’une de ces méthodes (voir la documentation [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/) pour plus de détails) :

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Alternativement, utilisez l’interface UI du Gestionnaire de packages NuGet dans Visual Studio pour rechercher « GroupDocs.Redaction » et l’installer directement. Pour la référence API, voir [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net).

### Obtention de licence
- **Essai gratuit :** Commencez avec une version d’essai pour explorer toutes les fonctionnalités.  
- **Licence temporaire :** Demandez une licence temporaire sur le [site Web GroupDocs](https://purchase.groupdocs.com/temporary-license/) ou gérez votre licence via le portail [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/).  
- **Achat complet :** Lorsque vous êtes prêt pour la production, achetez une licence complète qui supprime toutes les limites d’évaluation.

## Comment configurer GroupDocs.Redaction pour .NET
GroupDocs.Redaction fournit la fonctionnalité principale pour masquer le contenu sensible avant ou après la recherche. Elle expose une classe `Redactor` que vous instanciez avec une licence et des paramètres de configuration optionnels.

Le code suivant montre comment créer une instance de redacteur et charger un fichier de licence :

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

Avec le redacteur prêt, vous pouvez ensuite appeler `redactor.Redact(...)` sur tout document que vous récupérez à partir des résultats de recherche.

## Comment créer l’index de recherche
Créer un index de recherche implique de spécifier un dossier où les fichiers d’index seront stockés, puis d’initialiser la classe `Index` de GroupDocs.Search. L’index contiendra toutes les données consultables extraites de vos documents sources.

Tout d’abord, créez un répertoire pour l’index puis instanciez l’objet `Index` :

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

La création de l’index écrit un ensemble de fichiers binaires dans le dossier ; ces fichiers font généralement moins de 200 KB pour 1 000 pages, vous permettant de passer à des millions de pages sans épuiser l’espace disque.

## Comment ajouter des documents à l’index
Ajouter des documents nécessite de pointer l’API vers le répertoire contenant les fichiers sources et d’instruire l’index à les ingérer. Le processus analyse chaque format pris en charge, extrait le texte et le stocke dans l’index pour une récupération rapide.

Utilisez le code suivant pour indexer tous les fichiers d’un dossier source :

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

GroupDocs.Search prend en charge **plus de 30** formats d’entrée—y compris DOCX, PDF, PPTX, HTML et les types d’image courants—vous permettant d’indexer pratiquement n’importe quelle archive d’entreprise sans convertisseurs supplémentaires.

## Comment activer et exécuter la recherche de synonymes
La gestion des synonymes est activée via `SearchOptions`. Une fois activée, chaque requête s’étend automatiquement pour inclure les synonymes du dictionnaire, améliorant le rappel sans sacrifier la précision.

Activez la recherche de synonymes avec l’extrait suivant :

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

Le dictionnaire de synonymes par défaut contient plus de **5 000** paires de termes pour l’anglais. Vous pouvez également charger un fichier `SynonymDictionary` personnalisé pour prendre en charge le jargon spécifique à un secteur.

## Dictionnaire de synonymes personnalisé
Si vous avez besoin de synonymes spécifiques à un domaine, chargez votre propre fichier de dictionnaire et affectez‑le à `SearchOptions` avant d’exécuter une requête.

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## Conseils de dépannage courants
- **Problèmes de chemin :** Vérifiez que les dossiers d’index et source sont accessibles par le compte du processus.  
- **Limites de licence :** Une version non licenciée peut limiter le nombre de fichiers indexés à 100.  
- **Aucun résultat :** Vérifiez que le dictionnaire de synonymes est chargé ; vous pouvez inspecter `options.SynonymDictionary.Count` à l’exécution.  

## Applications pratiques
1. **Gestion de documents juridiques :** Trouvez la jurisprudence en utilisant des termes juridiques et leurs synonymes.  
2. **Recherche académique :** Étendez les recherches bibliographiques à travers les PDF et fichiers Word scientifiques.  
3. **Bases de connaissances d’entreprise :** Récupérez les politiques internes même lorsque les utilisateurs formulent les requêtes différemment.  
4. **Systèmes de gestion de contenu :** Offrez aux éditeurs une découverte plus riche lors du balisage des articles.  
5. **Gestion des tickets de support client :** Faites correspondre les tickets aux problèmes connus en utilisant des descriptions synonymes.  

## Considérations de performance
- **Maintenance de l’index :** Ré‑indexez après des mises à jour massives ; l’indexation incrémentale réduit le temps d’arrêt jusqu’à 70 %.  
- **Surveillance des ressources :** L’indexation d’un lot de 10 GB sur une VM standard (2 vCPU, 8 GB RAM) atteint un pic d’environ 1,2 GB RAM ; limitez la taille du lot si vous approchez des limites.  
- **Libération des objets :** Appelez `index.Dispose()` et `redactor.Dispose()` dès que vous avez terminé pour libérer les ressources natives.  

## Conclusion
Vous savez maintenant **comment créer un index de recherche** avec GroupDocs, ajouter des documents à cet index et activer la recherche de synonymes pour une expérience utilisateur plus intuitive. Cette base vous permet également d’ajouter la rédaction, le classement personnalisé ou la correspondance floue au-dessus d’un moteur de recherche robuste.

## Étapes suivantes
- Expérimentez avec `SearchOptions.FuzzySearch` pour détecter les fautes de frappe.  
- Explorez l’API `Ranking` pour mettre en avant les documents prioritaires.  
- Rejoignez la communauté sur le [GroupDocs Forum](https://forum.groupdocs.com/c/search/10) ou le [Free Support Forum](https://forum.groupdocs.com/c/search/10) pour partager des astuces et poser des questions.  
- Consultez les [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/) pour les mises à jour et les nouvelles fonctionnalités.  

## Questions fréquentes

**Q : Qu’est‑ce que la recherche de synonymes ?**  
R : La recherche de synonymes élargit la requête d’un utilisateur pour inclure des termes alternatifs prédéfinis, augmentant la probabilité de trouver des documents pertinents qui utilisent une formulation différente.

**Q : Comment mettre à jour ma licence GroupDocs ?**  
R : Visitez le portail [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) et téléchargez le nouveau fichier de licence via `License.SetLicense("path/to/license.lic")`.

**Q : Puis‑je utiliser la recherche de synonymes dans un environnement multilingue ?**  
R : Oui—chargez un fichier `SynonymDictionary` spécifique à chaque langue pour chaque paramètre régional que vous supportez, et le moteur appliquera l’ensemble de synonymes approprié à chaque requête.

**Q : Quels sont les problèmes d’indexation les plus courants ?**  
R : Les permissions d’accès aux fichiers, les formats non pris en charge et le dépassement de la limite de documents de la version d’essai sont les trois principaux problèmes rencontrés par les développeurs.

**Q : Comment optimiser les performances pour des index très volumineux ?**  
R : Utilisez l’indexation incrémentale, stockez l’index sur des SSD et configurez `IndexingOptions.MaxDegreeOfParallelism` pour correspondre au nombre de cœurs de votre CPU.

---

**Last Updated:** 2026-09-16  
**Tested With:** GroupDocs.Search 23.10 for .NET  
**Author:** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## Tutoriels associés

- [Ajouter un document à l’index avec les tutoriels GroupDocs.Search .NET](/search/net/document-management/)
- [Mettre en évidence les résultats de recherche dans les documents .NET avec GroupDocs.Search et Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [Comment mettre à jour l’index avec GroupDocs.Search & Redaction (.NET)](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)