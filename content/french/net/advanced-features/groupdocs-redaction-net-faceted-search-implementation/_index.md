---
date: '2026-04-02'
description: Apprenez à créer un index de recherche GroupDocs et à ajouter des documents
  à l’index tout en implémentant la recherche à facettes à l’aide de GroupDocs.Search
  et GroupDocs.Redaction en .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Créer un index de recherche GroupDocs avec la rédaction .NET et la recherche
  à facettes
type: docs
url: /fr/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Créer un index de recherche GroupDocs avec Redaction .NET Recherche à facettes

Dans les applications modernes, **créer un index de recherche avec GroupDocs** est essentiel pour une récupération de documents rapide et précise. Que vous manipuliez des contrats juridiques, des catalogues de produits ou de vastes bases de connaissances, un index bien construit vous permet **d'ajouter des documents à l'index** et d'exécuter des recherches à facettes puissantes en quelques secondes. Ce tutoriel vous guide à travers l'ensemble du processus — de la configuration de GroupDocs.Redaction à la création de requêtes facettées simples et complexes — afin que vous puissiez offrir une expérience de recherche réactive dans vos projets .NET.

## Réponses rapides
- **Quel est le but principal ?** Créer un index de recherche avec GroupDocs et activer la recherche à facettes.  
- **Quelles bibliothèques sont requises ?** GroupDocs.Redaction et GroupDocs.Search pour .NET.  
- **Comment ajouter des documents à l'index ?** Utilisez `index.Add(documentsFolder)` après avoir initialisé l'index.  
- **Puis-je exécuter des requêtes complexes ?** Oui, combinez des requêtes d'objets avec des opérateurs logiques pour un filtrage avancé.  
- **Une licence est‑elle nécessaire ?** Un essai gratuit suffit pour le développement ; une licence commerciale est requise pour la production.

## Qu'est-ce que la recherche à facettes et pourquoi l'utiliser avec GroupDocs ?
La recherche à facettes permet aux utilisateurs d'affiner les résultats en appliquant plusieurs filtres—comme la catégorie, la date ou l'auteur—simultanément. Lorsqu'elle est combinée avec **GroupDocs.Redaction**, vous obtenez un contenu sécurisé et interrogeable qui respecte les règles de rédaction, ce qui la rend idéale pour les environnements fortement soumis à la conformité.

## Prérequis

### Bibliothèques requises, versions et dépendances
- **GroupDocs.Redaction .NET** – dernière version stable.  
- **GroupDocs.Search .NET** – fonctionne main dans la main avec Redaction pour l'indexation.

### Exigences de configuration de l'environnement
- **IDE** : Visual Studio 2019 ou version ultérieure.  
- **Framework** : .NET Core 3.1, .NET 5 ou .NET 6.  
- **Compatibilité OS** : Windows, Linux, macOS.

### Prérequis de connaissances
Des compétences de base en C# et une compréhension générale des concepts de recherche à facettes seront utiles, mais le guide pas à pas est également accessible aux débutants.

## Configuration de GroupDocs.Redaction pour .NET

### Informations d'installation
Vous pouvez ajouter le package GroupDocs.Redaction en utilisant l'une des méthodes suivantes :

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Recherchez « GroupDocs.Redaction » et installez la dernière version.

### Étapes d'obtention de licence
Pour débloquer toutes les fonctionnalités, commencez par un essai gratuit ou obtenez une licence permanente :

1. Visitez [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) pour explorer les options de licence.  
2. Suivez les instructions à l'écran pour recevoir votre fichier de licence d'essai ou acheté.

### Initialisation et configuration de base
Une fois le package installé, initialisez le Redactor dans votre application :

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Comment créer un index de recherche groupdocs

Ci-dessous, nous divisons l'implémentation en deux parties : **Simple Faceted Search** et **Complex Query**. Chaque partie montre comment **créer un index de recherche groupdocs**, ajouter des documents et exécuter des requêtes.

### Fonctionnalité 1 : Simple Faceted Search

**Aperçu**  
La recherche à facettes permet aux utilisateurs de restreindre les résultats en sélectionnant plusieurs critères. Cette section montre une approche simple en utilisant GroupDocs.Search.

#### Étape 1 : Définir les dossiers d'index et de documents
Configurez les chemins des dossiers où l'index sera stocké et où résident vos documents sources.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Étape 2 : Créer un index
Initialisez l'index de recherche dans le dossier que vous avez défini.

```csharp
Index index = new Index(indexFolder);
```

#### Étape 3 : Ajouter des documents à l'index
Chargez vos documents afin qu'ils deviennent interrogeables.

```csharp
index.Add(documentsFolder);
```

#### Étape 4 : Effectuer une recherche de requête texte
Exécutez une requête texte de base sur le champ **content**.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Étape 5 : Exécuter une recherche de requête d'objet
Utilisez des requêtes orientées objet pour un contrôle plus fin.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Fonctionnalité 2 : Complex Query

**Aperçu**  
Lorsque vous devez combiner plusieurs filtres—comme des motifs de nom de fichier et des correspondances de phrases—vous pouvez créer une requête complexe en utilisant des opérateurs logiques.

#### Étape 1 : Définir les dossiers d'index et de documents
Réutilisez la même structure de dossiers pour un scénario plus avancé.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Étape 2 : Créer un index et ajouter des documents
(Voir les étapes 2‑3 de l'exemple simple ; elles restent les mêmes.)

#### Étape 3 : Exécuter une recherche de requête texte
Exécutez une requête texte composée qui mélange les critères de nom de fichier et de contenu.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Étape 4 : Construire et exécuter des requêtes d'objet
Construisez la même logique de manière programmatique.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Continuez à combiner des phrases, des plages et des opérateurs booléens pour correspondre à vos règles métier exactes.

## Applications pratiques

1. **Plateformes E‑Commerce** – Filtrer les produits par catégorie, prix et note.  
2. **Systèmes de gestion de documents** – Localiser les contrats par auteur, date ou niveau de confidentialité.  
3. **Portails de contenu** – Permettre aux lecteurs d'affiner par tags, sujets et dates de publication.

## Considérations de performance

- **Actualisation de l'index** : Ré‑indexez régulièrement les fichiers nouveaux ou mis à jour pour maintenir une recherche rapide.  
- **Gestion de la mémoire** : Libérez les objets `Index` une fois terminés, surtout pour les grands ensembles de données.  
- **Indexation asynchrone** : Utilisez `Task.Run` ou des services en arrière‑plan pour éviter le gel de l'interface lors d'une indexation lourde.

## Problèmes courants et solutions

| Problème | Solution |
|----------|----------|
| **Index non trouvé** | Vérifiez le chemin `indexFolder` et assurez‑vous que le dossier possède les permissions d'écriture. |
| **Aucun résultat retourné** | Vérifiez que les champs que vous interrogez (par ex., `Content`, `Filename`) sont indexés. |
| **Erreurs de dépassement de mémoire** | Traitez les documents par lots et envisagez d'augmenter la taille du tas du GC .NET. |

## Questions fréquentes

**Q : Qu'est‑ce que la recherche à facettes ?**  
R : La recherche à facettes permet aux utilisateurs d'affiner les résultats en utilisant plusieurs filtres indépendants tels que la catégorie, la date ou l'auteur.

**Q : Comment gérer de grands ensembles de données avec GroupDocs.Search ?**  
R : Utilisez l'indexation incrémentielle, le traitement par lots et les opérations asynchrones pour maintenir une faible consommation de mémoire et de hautes performances.

**Q : Puis‑je intégrer les fonctionnalités GroupDocs dans des applications .NET existantes ?**  
R : Oui, les bibliothèques sont conçues pour une intégration transparente avec tout projet .NET.

**Q : Quels sont les problèmes courants avec la recherche à facettes ?**  
R : La syntaxe des requêtes complexes et la garantie que tous les champs pertinents sont indexés sont des défis typiques ; des tests appropriés et la maintenance de l'index les atténuent.

**Q : Comment obtenir une licence temporaire pour GroupDocs ?**  
R : Visitez la [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) pour demander une licence d'essai qui débloque toutes les fonctionnalités pendant l'évaluation.

## Ressources
- **Documentation** : [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **Référence API** : [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Dernière mise à jour** : 2026-04-02  
**Testé avec** : GroupDocs.Redaction 23.12 pour .NET, GroupDocs.Search 23.12 pour .NET  
**Auteur** : GroupDocs