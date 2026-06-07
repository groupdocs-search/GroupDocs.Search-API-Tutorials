---
date: '2026-06-07'
description: Apprenez comment implémenter une compression élevée .NET pour le stockage
  de texte et masquer les données confidentielles en utilisant GroupDocs.Search et
  GroupDocs.Redaction dans les applications .NET.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'Implémenter une compression élevée .NET avec GroupDocs : Guide du texte et
  de la rédaction'
type: docs
url: /fr/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Implémenter la compression élevée .NET avec GroupDocs : Guide du texte et de la rédaction

Dans les solutions .NET modernes, **implement high compression .net** est essentiel lorsque vous devez stocker d'énormes collections de texte sans exploser l'utilisation du disque. En même temps, protéger les informations sensibles—telles que les identifiants personnels ou les données financières—requiert une rédaction fiable. Ce tutoriel vous montre, étape par étape, comment configurer le stockage de texte à haute compression avec **GroupDocs.Search** et comment rédiger en toute sécurité les données confidentielles à l'aide de **GroupDocs.Redaction**. À la fin, vous pourrez compresser le texte indexé jusqu'à 90 % et supprimer le contenu privé des PDF, des fichiers Word et de nombreux autres formats.

## Réponses rapides
- **Quelle bibliothèque fournit l'indexation à haute compression ?** GroupDocs.Search for .NET.  
- **Quel outil rédige les données sensibles ?** GroupDocs.Redaction for .NET.  
- **Puis-je ajouter des documents à l'index automatiquement ?** Oui—utilisez l'API `AddDocument` dans une boucle de scan de dossiers.  
- **La compression est‑elle sans perte pour la recherche ?** Oui, le texte reste entièrement recherchable après compression.  
- **Ai‑je besoin d'une licence pour la production ?** Une licence permanente GroupDocs est requise pour une utilisation commerciale.

## Qu’est‑ce que “implement high compression .net” ?
Implémenter la compression élevée .net signifie configurer le moteur d'indexation GroupDocs.Search pour stocker le contenu textuel extrait sous forme compressée. Cela réduit la taille de l'index sur disque de façon spectaculaire tout en conservant le texte entièrement recherchable. La compression est sans perte, de sorte que la pertinence des requêtes et l'extraction des extraits fonctionnent exactement comme avec un index non compressé.

## Pourquoi utiliser GroupDocs pour la compression et la rédaction ?
GroupDocs.Search prend en charge plus de cinquante formats d'entrée et peut compresser le texte indexé jusqu'à quatre‑vingt‑dix pour cent, permettant aux grandes collections de documents de n'occuper qu'une fraction de leur taille originale. GroupDocs.Redaction complète cela en effaçant ou masquant de façon permanente les informations sensibles dans plus de trente types de fichiers, vous aidant à respecter des réglementations strictes telles que le RGPD et la HIPAA sans outils supplémentaires.

## Prérequis
- **Environnement de développement :** Visual Studio 2022 ou ultérieur, .NET 6+ (ou .NET Framework 4.7.2).  
- **Bibliothèques :** packages NuGet `GroupDocs.Search` et `GroupDocs.Redaction`.  
- **Permissions :** accès en lecture/écriture aux dossiers contenant les documents source et l'emplacement de sortie de l'index.  
- **Connaissances de base :** syntaxe C#, I/O de fichiers, et familiarité avec la structure de projet .NET.

## Comment implémenter la compression élevée .NET avec GroupDocs ?
Pour implémenter la compression élevée .NET avec GroupDocs, créez d'abord une instance `TextStorageSettings` et définissez son `CompressionLevel` sur `High`. Ensuite, instanciez un objet `Index`, en passant les paramètres et le dossier où l'index sera stocké. Une fois l'index prêt, ajoutez des documents avec `AddDocument`, puis exécutez des recherches avec la méthode `Search`, le tout pendant que le moteur gère de façon transparente la compression et la décompression.

### Étape 1 : Installer les packages NuGet requis
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Recherchez “GroupDocs.Search” et cliquez sur **Install**.  

### Étape 2 : Installer GroupDocs.Redaction (pour la rédaction de données)
- Ouvrez le **NuGet Package Manager**.  
- Recherchez **GroupDocs.Redaction** et installez la dernière version stable.  

### Étape 3 : Obtenir et appliquer une licence
- **Essai gratuit :** Inscrivez‑vous sur le portail GroupDocs pour obtenir une clé d'essai de 30 jours.  
- **Licence temporaire :** Demandez une clé temporaire pour les environnements de développement.  
- **Licence permanente :** Achetez une licence de production pour supprimer les limitations d'évaluation.

### Étape 4 : Initialisation de base des deux bibliothèques
Le `Search` et le `Redaction` engines partagent un modèle de licence commun. Initialise‑les au démarrage de l'application :

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Fonctionnalité 1 : Paramètres de stockage de texte à haute compression

### Configurer la configuration d'indexation
`TextStorageSettings` est la classe qui indique à GroupDocs.Search comment conserver le texte extrait. Activer la haute compression réduit la taille de l'index jusqu'à **10×** sans affecter la vitesse de recherche.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Explication :**  
- `CompressionLevel.High` active un algorithme basé sur ZSTD qui compresse efficacement les blocs de texte.  
- `UseMemoryCache = false` force le moteur à diffuser les données depuis le disque, ce qui est idéal pour les déploiements à grande échelle.

### Créer et gérer l'index
L'objet `Index` représente le référentiel searchable sur le disque. Vous spécifiez le dossier où les fichiers d'index seront stockés et transmettez les paramètres de compression définis ci‑dessus.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Explication :**  
- `indexFolder` détermine où les fichiers d'index compressés sont stockés.  
- `settings` injecte la configuration de haute compression, garantissant que chaque document ajouté en bénéficie.

## Fonctionnalité 2 : Ajouter des documents à l'index

### Ajouter des documents à votre index
`AddDocument` ajoute un fichier unique à l'index, en extrayant son texte, en le compressant selon les paramètres configurés, et en stockant le résultat. GroupDocs.Search peut ingérer des fichiers depuis un arbre de répertoires. La boucle suivante parcourt `documentsFolder`, ajoute chaque fichier et consigne la progression.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Explication :**  
- `AddDocument` analyse le fichier, extrait le texte searchable, le compresse selon `TextStorageSettings` et le stocke dans l'index.  
- Cette approche fonctionne pour **PDF, DOCX, TXT, HTML**, et plus de **30** autres formats.

## Fonctionnalité 3 : Exécuter une requête de recherche

### Effectuer une recherche
`Search` exécute une requête contre l'index compressé et renvoie une collection d'objets `DocumentResult` correspondants avec des scores de pertinence et des extraits mis en évidence. Une fois l'index rempli, vous pouvez exécuter des requêtes rapides. La méthode `Search` renvoie une collection d'objets `DocumentResult` qui incluent les chemins de fichiers et les extraits mis en évidence.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Explication :**  
- Le moteur de recherche analyse le texte compressé directement, de sorte que la latence des requêtes reste faible même pour les index contenant **des millions de pages**.  
- `Score` indique la pertinence ; des valeurs plus élevées signifient une meilleure correspondance.

## Comment rédiger les données confidentielles avec GroupDocs.Redaction ?
Rédiger les données confidentielles avec GroupDocs.Redaction commence par créer une instance `Redactor` pour le fichier cible. Définissez un ou plusieurs objets `SearchPattern` qui décrivent le texte à supprimer, comme des expressions régulières pour les numéros de sécurité sociale. Appliquez chaque motif avec `Redact`, en spécifiant un `RedactionType` tel que `BlackOut`, et enregistrez le résultat sous forme d'un nouveau document, en veillant à ce que l'original reste intact.

`Redactor` est la classe principale de GroupDocs.Redaction utilisée pour charger un document et effectuer des opérations de rédaction.  
`SearchPattern` définit une expression régulière qui identifie le texte à rédiger.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Explication :**  
- `SearchPattern` utilise une expression régulière pour localiser les numéros de sécurité sociale.  
- `RedactionType.BlackOut` remplace le texte correspondant par un rectangle noir plein, garantissant que les données ne peuvent pas être récupérées.

## Applications pratiques
1. **Gestion de documents juridiques :** Compressez automatiquement d'énormes dossiers de cas et rédigez les identifiants des clients avant l'archivage.  
2. **Dossiers de santé :** Stockez des années de notes de patients dans un index compressé et supprimez les PHI (Informations de santé protégées) avant de les partager avec des partenaires de recherche.  
3. **Rapports financiers :** Sécurisez les rapports trimestriels en rédigeant les numéros de compte tout en conservant le texte searchable pour les requêtes d'audit.

## Considérations de performance
- **Impact de la compression :** La haute compression réduit la taille de l'index jusqu'à **90 %**, ce qui diminue l'usure du SSD et accélère les opérations de sauvegarde.  
- **Utilisation de la mémoire :** Désactivez le cache en mémoire pour les index très volumineux afin de garder l'empreinte du processus sous **500 Mo**.  
- **Optimisation I/O :** Ajoutez les documents par lots de 100 pour minimiser les accès disque excessifs.  
- **Traitement asynchrone :** Enveloppez les appels `AddDocument` dans `Task.Run` pour garder les threads UI réactifs dans les applications de bureau.

## Pièges courants & dépannage
- **Chemins de fichiers incorrects :** Vérifiez que `documentsFolder` et `indexFolder` sont des chemins absolus et que l'application dispose des permissions de lecture/écriture.  
- **Erreurs de licence :** Assurez‑vous que les fichiers `.lic` sont déployés avec l'exécutable ou incorporés comme ressources.  
- **La recherche ne renvoie aucun résultat :** Vérifiez que le niveau de compression `TextStorageSettings` correspond à celui utilisé lors de l'indexation ; des paramètres incompatibles peuvent entraîner des échecs de désérialisation.  

## Questions fréquemment posées

**Q : Puis‑je ajouter des documents à l'index après la construction initiale ?**  
R : Oui—appelez simplement `index.AddDocument` pour les nouveaux fichiers ; le moteur met à jour l'index compressé de façon incrémentielle.

**Q : La rédaction modifie‑t‑elle le fichier original ?**  
R : Non—le fichier original reste intact ; la version rédigée est enregistrée comme un nouveau fichier, préservant l'intégrité du document.

**Q : Quels formats GroupDocs.Redaction prend‑il en charge ?**  
R : Plus de **30** formats, incluant PDF, DOCX, PPTX, XLSX, images (PNG, JPEG) et texte brut.

**Q : Comment la haute compression affecte‑t‑elle la pertinence de la recherche ?**  
R : Cela n'affecte pas. La compression est sans perte pour le texte, donc les scores de pertinence sont identiques à ceux d'un index non compressé.

**Q : Existe‑t‑il une limite à la taille des documents que je peux indexer ?**  
R : GroupDocs.Search peut gérer des fichiers multi‑gigaoctets en diffusant le contenu ; toutefois, assurez‑vous d'avoir suffisamment d'espace disque pour l'index compressé (environ 10 % de la taille originale).

## Ressources
- [Documentation](https://docs.groupdocs.com/search/net/)
- [Référence API](https://reference.groupdocs.com/redaction/net)
- [Télécharger GroupDocs.Redaction pour .NET](https://releases.groupdocs.com/search/net/)
- [Forum d'assistance gratuit](https://forum.groupdocs.com/c/search/10)
- [Obtention d'une licence temporaire](https://purchase.groupdocs.com/temporary-license/)

---

**Dernière mise à jour :** 2026-06-07  
**Testé avec :** GroupDocs.Search 23.12 et GroupDocs.Redaction 23.12 pour .NET  
**Auteur :** GroupDocs

## Tutoriels associés

- [Implémentation de GroupDocs.Search et Redaction en .NET pour la gestion de documents](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Comment optimiser GroupDocs.Redaction pour .NET : Guide de gestion efficace de l'index et de l'orthographe](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Maîtriser GroupDocs Redaction et Search en .NET : Gestion efficace des documents et recherche sécurisée](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)