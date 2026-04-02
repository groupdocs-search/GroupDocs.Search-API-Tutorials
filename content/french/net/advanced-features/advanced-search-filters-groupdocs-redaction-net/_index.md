---
date: '2026-04-02'
description: Apprenez à filtrer par extension de fichier et à rechercher uniquement
  les fichiers txt avec GroupDocs.Redaction pour .NET — améliorez l’efficacité de
  la gestion des documents.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Filtrer par extension de fichier dans .NET à l'aide de GroupDocs.Redaction
type: docs
url: /fr/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Filtrer par extension de fichier dans .NET avec GroupDocs.Redaction

Parcourir une vaste collection de fichiers peut sembler écrasant, surtout lorsque vous ne avez besoin que de résultats provenant de types de fichiers spécifiques. Dans ce tutoriel, vous découvrirez **comment filtrer par extension de fichier** avec GroupDocs.Redaction pour .NET, vous permettant de rechercher uniquement les fichiers txt ou toute autre extension de votre choix. Nous parcourrons la configuration des filtres basés sur le type de fichier et sur le chemin, afin que vous puissiez rapidement localiser exactement les documents dont vous avez besoin.

## Réponses rapides
- **What does “filter by file extension” do?** Il limite la recherche aux documents dont l'extension correspond à celle spécifiée (par ex., *.txt).  
- **Why use GroupDocs.Redaction for this?** Il fournit des API de filtrage intégrées qui sont rapides et faciles à intégrer.  
- **Do I need a license?** Une version d'essai gratuite suffit pour les tests ; une licence payante est requise pour la production.  
- **Which .NET versions are supported?** Les versions .NET prises en charge sont .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Can I combine file‑type and path filters?** Oui—appliquez plusieurs filtres pour des recherches très précises.

## Ce que vous apprendrez
- Comment **filter by file extension** afin que seuls les fichiers texte soient recherchés.  
- Comment configurer les **file path filters** pour restreindre les résultats à des dossiers spécifiques ou à des modèles de nommage.  
- Conseils pour garder votre index rapide et efficace en mémoire.

## Prérequis

Avant de commencer, assurez-vous d'avoir :

- **GroupDocs.Redaction Library** installée et compatible avec votre projet .NET.  
- Un environnement de développement tel que Visual Studio ou VS Code.  
- Connaissances de base en C# et familiarité avec la structure d'un projet .NET.

## Configuration de GroupDocs.Redaction pour .NET

Tout d'abord, ajoutez la bibliothèque à votre projet.

**Using .NET CLI :**  
```bash
dotnet add package GroupDocs.Redaction
```

**Using Package Manager :**  
```bash
Install-Package GroupDocs.Redaction
```

Ou localisez « GroupDocs.Redaction » dans l'interface du gestionnaire de packages NuGet et installez la dernière version.

### Acquisition de licence

Vous pouvez commencer avec une version d'essai gratuite ou demander une licence temporaire. Pour les projets à long terme, achetez une licence sur le site officiel.

### Initialisation de base

Après l'installation du package, créez un index qui contiendra les références à vos documents :

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Guide d'implémentation

### Fonctionnalité 1 : Définir un filtre pour les documents texte (.txt)

#### Comment filtrer par extension de fichier pour les documents texte

1. **Définir l'index et les dossiers de documents**  
   Définissez les chemins où se trouvent vos fichiers source :

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Créer un index**  
   Chargez tous les fichiers du dossier source dans l'index :

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Configurer les options de recherche avec un filtre d'extension de fichier**  
   Indiquez au moteur de ne prendre en compte que les fichiers *.txt :

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Exécuter la recherche**  
   Exécutez une requête ; le filtre garantit que les fichiers non‑texte sont ignorés :

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Explanation*: La méthode `Search` renvoie les correspondances qui satisfont le filtre, réduisant considérablement le bruit et améliorant les performances.

### Fonctionnalité 2 : Filtres de chemin de fichier

#### Pourquoi utiliser les filtres de chemin de fichier ?

Parfois, vous devez limiter les recherches à un dossier de service particulier ou à un ensemble de fichiers partageant une convention de nommage. Les filtres de chemin vous permettent de faire exactement cela.

1. **Définir l'index et les dossiers de documents**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Créer un index**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Configurer les options de recherche avec une expression régulière basée sur le chemin**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Cette expression régulière correspond à tout fichier dont le chemin complet contient le mot « Lorem », vous permettant de cibler des sous‑dossiers spécifiques.

4. **Exécuter la recherche basée sur le chemin**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Applications pratiques
- **Legal Document Management** – Localisez rapidement les contrats pertinents stockés sous forme de fichiers texte brut.  
- **Academic Research** – Récupérez uniquement les notes de recherche *.txt qui appartiennent à un dossier de projet particulier.  
- **Corporate Reporting** – Filtrez les rapports internes par chemin de département (par ex., `/Finance/2025/`).  

## Considérations de performance
- Indexez uniquement les types de documents dont vous avez réellement besoin ; les fichiers inutiles augmentent la taille de l'index et le temps de recherche.  
- Maintenez votre index à jour avec une tâche planifiée qui appelle `index.Add()` pour les fichiers nouveaux ou modifiés.  
- Utilisez des expressions régulières simples ; des motifs trop complexes peuvent ralentir le moteur de recherche.  
- Libérez les objets `Index` lorsqu'ils ne sont plus nécessaires pour libérer la mémoire.

## Conclusion
Vous savez maintenant comment **filter by file extension** et appliquer des **file path filters** avec GroupDocs.Redaction pour .NET. Ces techniques vous offrent un contrôle granulaire sur de grandes collections de documents, rendant les recherches plus rapides et plus pertinentes. Ensuite, expérimentez la combinaison de plusieurs filtres ou l'intégration de la recherche dans un flux de travail d'application plus large.

## Section FAQ

**Q1 : Puis‑je filtrer des documents autres que les fichiers texte ?**  
A1 : Oui, GroupDocs.Redaction prend en charge de nombreux formats. Changez l'argument dans `CreateFileExtension` pour l'extension souhaitée (par ex., « .pdf »).

**Q2 : Comment mettre à jour régulièrement mon index de recherche ?**  
A2 : Planifiez un service en arrière‑plan ou une tâche cron qui exécute `index.Add()` sur les répertoires que vous souhaitez garder à jour.

**Q3 : Y a‑t‑il un impact sur les performances lors du filtrage par chemin de fichier ?**  
A3 : Des expressions régulières correctement optimisées ont un impact minimal, mais effectuez toujours des tests de performance avec votre propre jeu de données.

**Q4 : Puis‑je combiner plusieurs filtres pour des recherches plus précises ?**  
A4 : Absolument. Vous pouvez enchaîner les filtres ou créer des filtres composites pour cibler à la fois le type de fichier et le chemin simultanément.

**Q5 : Où puis‑je trouver plus de ressources sur GroupDocs.Redaction ?**  
A5 : Consultez la documentation officielle sur [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) pour des guides détaillés et des références API.

## Questions fréquemment posées

**Q : Le `SearchDocumentFilter` fonctionne‑t‑il avec des fichiers chiffrés ?**  
A : Le filtre lui‑même agit sur les métadonnées du fichier, ainsi les fichiers chiffrés sont toujours indexés si vous fournissez les informations d’identification de déchiffrement nécessaires lors de l'indexation.

**Q : Puis‑je utiliser des caractères génériques au lieu d’une expression régulière pour le filtrage de chemin ?**  
A : L'API nécessite actuellement une expression régulière, mais vous pouvez simuler des caractères génériques simples (par ex., `.*` pour n’importe quels caractères).

**Q : Quelle taille maximale peut atteindre l'index avant de devoir envisager le sharding ?**  
A : Les index de plusieurs centaines de gigaoctets peuvent bénéficier d’une division en plusieurs index logiques ; testez les performances à mesure que votre collection grandit.

**Q : Existe‑t‑il des méthodes intégrées pour supprimer des documents de l'index ?**  
A : Oui—appelez `index.Delete(documentId)` ou `index.DeleteAll()` pour gérer les entrées obsolètes.

**Q : Existe‑t‑il un moyen de prévisualiser les résultats de recherche avant de charger le document complet ?**  
A : L'objet `SearchResult` inclut des informations d'extrait que vous pouvez afficher dans l'interface sans ouvrir le fichier complet.

## Ressources
- **Documentation** : [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)  
- **Référence API** : [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)  
- **Téléchargement** : [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)  
- **Support gratuit** : [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licence temporaire** : [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Dernière mise à jour :** 2026-04-02  
**Testé avec :** GroupDocs.Redaction 23.12 for .NET  
**Auteur :** GroupDocs