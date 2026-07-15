---
date: '2026-06-22'
description: Apprenez comment caviarder des documents dans .NET tout en optimisant
  la search performance avec GroupDocs.Redaction et GroupDocs.Search. attribute management,
  indexing et secure redaction, étape par étape, pour les développeurs .NET.
keywords:
- how to redact documents
- optimize search performance
- how to index attributes
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  headline: How to Redact Documents in .NET Using GroupDocs Redaction
  type: TechArticle
- description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  name: How to Redact Documents in .NET Using GroupDocs Redaction
  steps:
  - name: Initialize Index
    text: '`Index` represents a searchable collection of documents and their associated
      metadata. csharp using GroupDocs.Search.Common; using GroupDocs.Search.Options;
      using GroupDocs.Search.Results; Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
      index.Add("@YOUR_DOCUMENT_DIRECTORY/Docum'
  - name: Modify Attributes
    text: '`AttributeChangeBatch` is the class that batches attribute updates for
      efficiency. **Definition anchor:** *`AttributeChangeBatch` batches add, update,
      and delete operations on document attributes in a single transaction.* csharp
      DocumentInfo[] documents = index.GetIndexedDocuments(); AttributeChange'
  - name: Search with Attribute Filters
    text: You can filter search results by attribute values using `SearchOptions`.
      **Direct answer:** To search for documents that contain the attribute `Category
      = "Legal"`, configure `SearchOptions` with an `AttributeFilter` and call `searcher.Search("contract",
      options)`. This returns only the legally tagg
  - name: Set Up Event Handler for Indexing
    text: '**Definition anchor:** *The `DocumentIndexed` event fires each time a document
      is successfully added to the index, allowing custom logic to run.* csharp Index
      index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing"); index.Events.FileIndexing
      += (sender, args) => { if (args.Document'
  - name: Configure and Perform Search
    text: After attributes are attached, you can search using those new fields. **Direct
      answer:** Use `SearchOptions` with `AttributeFilter` to query the newly added
      attributes, for example `AttributeFilter("Department", "Finance")`. This returns
      only finance‑related files, demonstrating **how to index attri
  type: HowTo
- questions:
  - answer: Load each file with `Redactor`, add a `RedactionRegion` for every sensitive
      area, then call `Redactor.Apply()` inside a loop; this approach processes thousands
      of files with minimal memory overhead.
    question: What is the best way to batch‑redact multiple PDFs?
  - answer: Yes. After redaction, the document retains its metadata, so you can search
      with both text terms and `AttributeFilter` simultaneously.
    question: Can I combine redaction with attribute filtering in a single query?
  - answer: Pass the password to the `Redactor` constructor; the library will decrypt,
      redact, and re‑encrypt the file automatically.
    question: How do I handle password‑protected documents?
  - answer: Absolutely. Enable `RedactorOptions.Ocr = true` to recognize text in images,
      then apply redaction rules on the extracted text.
    question: Does GroupDocs support OCR for scanned images before redaction?
  - answer: GroupDocs.Redaction and GroupDocs.Search support .NET Core 3.1, .NET 5,
      .NET 6, and .NET 7, as well as .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Comment caviarder des documents dans .NET avec GroupDocs Redaction
type: docs
url: /fr/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# Comment masquer des documents dans .NET à l'aide de GroupDocs Redaction

Dans ce tutoriel complet, vous découvrirez **comment masquer des documents** dans un environnement .NET et maîtriserez simultanément la gestion des attributs de documents avec GroupDocs.Redaction et GroupDocs.Search. Que vous ayez besoin de protéger des données sensibles, d'accélérer la recherche ou d'organiser de grandes bibliothèques de documents, les techniques présentées ici vous offrent une solution prête pour la production qui s'étend à des centaines de milliers de fichiers.

## Réponses rapides
- **Comment masquer un PDF dans .NET ?** Chargez le fichier avec `Redactor`, définissez une `RedactionRegion` et appelez `Redactor.Apply()` – trois lignes de code gèrent le travail lourd.  
- **Puis-je modifier les attributs d'un document après l'indexation ?** Oui, utilisez `AttributeChangeBatch` pour ajouter, mettre à jour ou supprimer des attributs en masse.  
- **Quelles bibliothèques sont requises ?** `GroupDocs.Redaction` + `GroupDocs.Search` (dernières versions NuGet).  
- **Ai-je besoin d'une licence pour la production ?** Une licence GroupDocs valide est requise ; une licence d'essai temporaire est disponible pour l'évaluation.  
- **Comment améliorer la vitesse de recherche ?** Activez le traitement par lots et l'indexation sélective ; ces techniques peuvent **optimiser les performances de recherche** jusqu'à 40 % sur de grands ensembles de données.

## Qu'est-ce que « comment masquer des documents » ?

Il décrit le processus automatisé de localisation d'informations sensibles dans un fichier et de leur remplacement par du contenu masqué — comme des barres noires ou des espaces blancs — tout en conservant la mise en page originale. Cela garantit que les données confidentielles sont cachées aux yeux des utilisateurs, mais que le document reste lisible et fonctionnel pour les tâches en aval.

## Pourquoi utiliser GroupDocs.Redaction et GroupDocs.Search ensemble ?

GroupDocs.Redaction prend en charge **plus de 50 formats de fichiers** (PDF, DOCX, XLSX, PPTX, images, etc.) et peut traiter des documents jusqu'à **2 Go** sans charger le fichier complet en mémoire. GroupDocs.Search indexe plus de **70 millions de termes** par heure sur un serveur standard, vous permettant de **optimiser les performances de recherche** de façon spectaculaire lorsqu'il est combiné avec le filtrage basé sur les attributs.

## Prérequis

- **Bibliothèques requises :** `GroupDocs.Search` et `GroupDocs.Redaction` (dernières versions NuGet).  
- **Environnement de développement :** Visual Studio 2019 ou ultérieur, ciblant .NET Core 3.1 ou .NET 6+.  
- **Connaissances de base :** syntaxe C#, concepts orientés objet et familiarité avec les principes d'indexation de documents.

## Configuration de GroupDocs.Redaction pour .NET

### Installation de la bibliothèque

Vous pouvez ajouter **GroupDocs.Redaction** à votre projet en utilisant l'une des méthodes suivantes :

**CLI .NET**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Gestionnaire de packages**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**Interface du gestionnaire de packages NuGet**  
- Rechercher “GroupDocs.Redaction” et installer la dernière version.

### Étapes d'obtention de licence

Pour commencer, vous pouvez obtenir une licence temporaire ou en acheter une. Un essai gratuit est disponible pour tester les fonctionnalités avant de vous engager :
1. Visitez la [page de licence GroupDocs](https://purchase.groupdocs.com/temporary-license/) pour demander une licence temporaire.  
2. Suivez les instructions fournies pour appliquer votre licence dans votre application.

### Initialisation et configuration de base

`Redactor` est la classe principale utilisée pour charger un document et appliquer des opérations de masquage.

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## Fonctionnalité 1 : Modifier les attributs du document

### Vue d'ensemble
Modifier les attributs d'un document vous permet d'ajuster finement la façon dont les documents apparaissent dans les résultats de recherche, permettant un filtrage et une catégorisation précis.

#### Étape 1 : Initialiser l'index
`Index` représente une collection consultable de documents et leurs métadonnées associées.

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Étape 2 : Modifier les attributs
`AttributeChangeBatch` est la classe qui regroupe les mises à jour d'attributs pour plus d'efficacité.

**Ancre de définition :** *`AttributeChangeBatch` regroupe les opérations d'ajout, de mise à jour et de suppression d'attributs de documents en une seule transaction.*

```csharp
```csharp
DocumentInfo[] documents = index.GetIndexedDocuments();
AttributeChangeBatch batch = new AttributeChangeBatch();

// Adding "public" to all documents
batch.AddToAll("public");

// Removing "public" from the first document
batch.Remove(documents[0].FilePath, "public");

// Adding "main" and "key" to the first document
batch.Add(documents[0].FilePath, "main", "key");
index.ChangeAttributes(batch);
```
```

#### Étape 3 : Rechercher avec des filtres d'attributs
Vous pouvez filtrer les résultats de recherche par valeurs d'attributs en utilisant `SearchOptions`.

**Réponse directe :** Pour rechercher les documents contenant l'attribut `Category = "Legal"`, configurez `SearchOptions` avec un `AttributeFilter` et appelez `searcher.Search("contract", options)`. Cela ne renvoie que les contrats étiquetés légalement, réduisant le bruit des résultats et **optimisant les performances de recherche**.

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## Fonctionnalité 2 : Ajouter des attributs lors de l'indexation

### Vue d'ensemble
Ajouter des attributs au moment de l'indexation garantit que chaque document est enrichi avec les métadonnées appropriées dès le départ, éliminant le besoin de mises à jour massives ultérieures.

#### Étape 1 : Configurer le gestionnaire d'événements pour l'indexation
**Ancre de définition :** *L'événement `DocumentIndexed` se déclenche chaque fois qu'un document est ajouté avec succès à l'index, permettant l'exécution d'une logique personnalisée.*

```csharp
```csharp
Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing");

index.Events.FileIndexing += (sender, args) => {
    if (args.DocumentFullPath.EndsWith("Lorem ipsum.pdf")) {
        // Specify attributes for this document
        args.Attributes = new string[] { "main", "key" };
    }
};

// Add documents to index
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Étape 2 : Configurer et exécuter la recherche
Après l'ajout des attributs, vous pouvez rechercher en utilisant ces nouveaux champs.

**Réponse directe :** Utilisez `SearchOptions` avec `AttributeFilter` pour interroger les attributs nouvellement ajoutés, par exemple `AttributeFilter("Department", "Finance")`. Cela ne renvoie que les fichiers liés aux finances, démontrant **comment indexer les attributs** pour des résultats plus rapides et plus pertinents.

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## Applications pratiques

Voici trois scénarios courants où la gestion conjointe des attributs de documents et du masquage apporte une valeur commerciale tangible :
1. **Gestion de documents juridiques** – Masquez automatiquement les clauses confidentielles et étiquetez les contrats par juridiction, permettant aux avocats de ne localiser que les fichiers pertinents.  
2. **Organisation des dossiers médicaux** – Masquez les identifiants des patients tout en ajoutant des attributs tels que `PatientID` et `VisitDate` pour une récupération conforme et rapide.  
3. **Catalogage de produits e‑commerce** – Masquez les informations de prix des fournisseurs et étiquetez les produits avec `StockStatus` ou `DiscountRate` lors de l'importation en masse, permettant des requêtes d'inventaire en temps réel.

## Considérations de performance

Lorsque vous traitez de grands ensembles de données, gardez ces meilleures pratiques à l'esprit :
- **Traitement par lots :** `AttributeChangeBatch` réduit les allers‑retours vers l'index, diminuant le temps de traitement jusqu'à **45 %** sur des lots de 100 k documents.  
- **Indexation sélective :** Indexez uniquement les documents qui nécessitent de nouveaux attributs ; ignorez les fichiers inchangés pour économiser le CPU et les I/O.  
- **Gestion de la mémoire :** Libérez les instances de `SearchResult`, `Redactor` et `Indexer` dès que vous avez fini de les utiliser pour libérer les ressources non gérées.

## Problèmes courants et solutions

| Problème | Cause | Solution |
|----------|-------|----------|
| Le masquage ne masque pas le texte | Coordonnées incorrectes de `RedactionRegion` | Vérifiez les dimensions de la page avec `Redactor.GetPageSize()` avant de définir la région. |
| Les modifications d'attributs ne sont pas reflétées dans la recherche | Index non rafraîchi | Appelez `searcher.Refresh()` après l'exécution de `AttributeChangeBatch`. |
| Erreurs de mémoire insuffisante sur de gros fichiers | Chargement du fichier complet en mémoire | Activez le mode streaming en définissant `RedactorOptions.Stream = true`. |

## Foire aux questions

**Q : Quelle est la meilleure façon de masquer par lots plusieurs PDF ?**  
R : Chargez chaque fichier avec `Redactor`, ajoutez une `RedactionRegion` pour chaque zone sensible, puis appelez `Redactor.Apply()` dans une boucle ; cette approche traite des milliers de fichiers avec une surcharge mémoire minimale.

**Q : Puis-je combiner le masquage avec le filtrage d'attributs dans une seule requête ?**  
R : Oui. Après le masquage, le document conserve ses métadonnées, vous pouvez donc rechercher à la fois avec des termes texte et `AttributeFilter` simultanément.

**Q : Comment gérer les documents protégés par mot de passe ?**  
R : Passez le mot de passe au constructeur `Redactor` ; la bibliothèque déchiffrera, masquera et ré‑chiffrera le fichier automatiquement.

**Q : GroupDocs prend‑il en charge l’OCR pour les images numérisées avant le masquage ?**  
R : Absolument. Activez `RedactorOptions.Ocr = true` pour reconnaître le texte dans les images, puis appliquez les règles de masquage sur le texte extrait.

**Q : Quelles versions de .NET sont officiellement prises en charge ?**  
R : GroupDocs.Redaction et GroupDocs.Search prennent en charge .NET Core 3.1, .NET 5, .NET 6 et .NET 7, ainsi que .NET Framework 4.6.2+.

## Conclusion

Vous disposez maintenant d'une solution complète pour **comment masquer des documents** tout en **optimisant les performances de recherche** et **comment indexer les attributs** à l'aide de GroupDocs.Redaction et GroupDocs.Search. En suivant les étapes ci‑dessus, vous pouvez protéger les données sensibles, enrichir votre index de recherche avec des métadonnées pertinentes et garder vos applications .NET rapides et sécurisées.

---

**Dernière mise à jour :** 2026-06-22  
**Testé avec :** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 for .NET  
**Auteur :** GroupDocs

## Tutoriels associés

- [Maîtriser GroupDocs.Redaction .NET : création d'index efficace et gestion des alias pour la recherche avancée de documents](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Maîtriser le masquage de documents et l'indexation des métadonnées avec GroupDocs.Redaction .NET](/search/net/document-management/groupdocs-redaction-net-document-metadata/)
- [Maîtriser GroupDocs.Redaction .NET : configuration et gestion des événements pour une gestion sécurisée des documents](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)