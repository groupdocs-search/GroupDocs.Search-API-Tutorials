---
date: '2026-04-21'
description: Apprenez à filtrer les fichiers avec GroupDocs.Redaction pour .NET, y
  compris le filtrage par date de création, taille du fichier, date de modification,
  et comment appliquer des filtres NOT.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Comment filtrer les fichiers avec GroupDocs.Redaction pour .NET
type: docs
url: /fr/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Comment filtrer les fichiers avec GroupDocs.Redaction pour .NET

Dans l’environnement numérique actuel en évolution rapide, **comment filtrer les fichiers** efficacement peut faire ou défaire votre productivité. Que vous ayez besoin d’isoler des documents par extension, date de création, taille ou date de modification, une stratégie de filtrage solide fait gagner du temps, réduit les coûts de stockage et maintient votre index de recherche propre. Dans ce tutoriel, nous parcourrons des exemples concrets utilisant GroupDocs.Redaction pour .NET, vous montrant exactement comment filtrer les fichiers pour répondre aux besoins courants des entreprises.

## Réponses rapides
- **Quelle bibliothèque faut‑il ?** GroupDocs.Redaction pour .NET (install via NuGet).  
- **Puis‑je filtrer par date de création ?** Oui – utilisez `CreateCreationTimeRange`.  
- **Comment exclure certains types ?** Appliquer un filtre NOT avec `DocumentFilter.CreateNot`.  
- **Le filtrage par taille de fichier est‑il pris en charge ?** Absolument, via `CreateFileLengthRange` ou des limites supérieures/inférieures.  
- **Ai‑je besoin d’une licence ?** Une version d'essai ou une licence complète est requise pour une utilisation en production.

## Qu’est‑ce que le filtrage de fichiers avec GroupDocs.Redaction ?
Le filtrage de fichiers vous permet d’indiquer au moteur d’indexation quels documents inclure ou ignorer en fonction de métadonnées telles que l’extension, les dates, les motifs de chemin ou la taille. En définissant des règles précises de `DocumentFilter`, vous gardez votre index léger et vos recherches rapides.

## Pourquoi utiliser GroupDocs.Redaction pour .NET ?
- **Assistants de filtre intégrés** – pas besoin d'écrire du code système personnalisé.  
- **Opérateurs logiques** – combinez plusieurs critères avec AND, OR et NOT.  
- **Optimisé pour les performances** – les filtres sont appliqués pendant l'indexation, pas après.  
- **Cross‑platform** – fonctionne avec .NET Framework, .NET Core et .NET 5/6+.

## Prérequis
- .NET Framework 4.6+ ou .NET Core 3.1+ installé.  
- Visual Studio ou votre IDE C# préféré.  
- Connaissances de base en C#.

### Bibliothèques requises et configuration
Installez le package NuGet en utilisant votre méthode préférée :

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Conseil pro :** Après l'installation, ajoutez votre fichier de licence à la racine du projet et appelez `License.SetLicense("license-file-path")` avant de créer tout objet Redactor ou Index.

## Configuration de GroupDocs.Redaction pour .NET

Tout d'abord, créez une instance `Redactor` qui pointe vers le document que vous souhaitez traiter :

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Pourquoi c’est important :** Initialiser le Redactor garantit que la bibliothèque est prête à appliquer des filtres et des règles de rédaction plus tard dans le flux de travail.

## Comment filtrer les fichiers par extension

Filtrer par extension de fichier est la méthode la plus courante pour réduire un ensemble de documents. Ci‑dessous, nous ne conservons que les fichiers FB2, EPUB et TXT.

### Filtrer par extension de fichier

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Comment appliquer un filtre NOT pour exclure les types indésirables

Si vous devez **appliquer un filtre NOT** — par exemple, exclure les fichiers HTML et PDF — utilisez `CreateNot`.

### Exclure les fichiers HTM, HTML et PDF

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Comment filtrer les fichiers par date de création

Lorsque vous devez **filtrer par date de création**, spécifiez un `DateTime` de début et de fin.

### Filtrer par plage de dates de création

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Comment filtrer les fichiers par date de modification

De même que pour les dates de création, vous pouvez limiter les résultats aux fichiers modifiés avant un certain moment.

### Filtrer par date de modification

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Comment filtrer les fichiers par chemin à l’aide d’expressions régulières

Si votre structure de dossiers suit des conventions de nommage, une expression régulière peut cibler des chemins spécifiques.

### Filtrer par motif de chemin de fichier

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Comment filtrer les fichiers par taille

Contrôler la taille des documents est essentiel lorsqu’on gère la bande passante ou les limites de stockage.

### Filtrer par taille de fichier (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Comment combiner plusieurs conditions avec AND

Lorsque vous devez **filtrer les fichiers** en utilisant plusieurs critères à la fois, combinez‑les avec `CreateAnd`.

### Exemple d’AND logique

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Comment combiner plusieurs conditions avec OR

Utilisez `CreateOr` lorsque l’une quelconque des plusieurs règles doit être satisfaite.

### Exemple d’OR logique

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Problèmes courants et solutions
- **Filtre non appliqué :** Assurez‑vous d'assigner `settings.DocumentFilter` **avant** de créer l'instance `Index`.  
- **Des fichiers inattendus apparaissent :** Vérifiez que les extensions de fichier incluent le point initial (`.txt`).  
- **Ralentissement des performances :** Combinez les filtres avec AND pour réduire le nombre de fichiers scannés tôt dans le pipeline d'indexation.  
- **Erreurs d’expression régulière :** Échappez les caractères spéciaux dans votre motif de chemin ou utilisez `RegexOptions.IgnoreCase` pour des correspondances insensibles à la casse.

## Questions fréquemment posées

**Q : Puis‑je combiner un filtre NOT avec un filtre AND ?**  
R : Oui. Créez d’abord le filtre NOT (`DocumentFilter.CreateNot`) puis incluez‑le comme l’un des arguments de `DocumentFilter.CreateAnd`.

**Q : Comment filtrer les fichiers de plus de 10 MB ?**  
R : Utilisez `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` pour ne retenir que les fichiers dépassant cette taille.

**Q : Est‑il possible de filtrer à la fois par dates de création et de modification ?**  
R : Absolument. Créez chaque filtre séparément et combinez‑les avec `CreateAnd`.

**Q : Ces filtres fonctionnent‑ils avec des chemins de stockage cloud ?**  
R : Les filtres opèrent sur le système de fichiers local. Pour des sources cloud, téléchargez les fichiers dans un dossier temporaire d’abord, puis appliquez les mêmes filtres.

**Q : Le changement de filtre nécessite‑t‑il une nouvelle indexation ?**  
R : Oui. Les filtres sont évalués lors de l’appel à `index.Add`. Modifier un filtre implique de reconstruire l’index pour refléter les nouveaux critères.

## Conclusion

En maîtrisant **comment filtrer les fichiers** avec GroupDocs.Redaction pour .NET — que ce soit par extension, date de création, date de modification, taille de fichier ou en utilisant la logique NOT — vous pouvez rationaliser la gestion documentaire, garder vos index performants et vous concentrer sur le contenu réellement important. Expérimentez avec les opérateurs logiques pour adapter le filtrage à vos règles métier précises, et vous constaterez immédiatement des gains en vitesse et en efficacité de stockage.

---

**Dernière mise à jour :** 2026-04-21  
**Testé avec :** GroupDocs.Redaction 24.11 pour .NET  
**Auteur :** GroupDocs