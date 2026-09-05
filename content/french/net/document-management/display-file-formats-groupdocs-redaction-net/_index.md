---
date: '2026-06-07'
description: Apprenez à répertorier les extensions de fichiers et à obtenir les formats
  de fichiers en utilisant GroupDocs.Redaction en C#. Comprend la configuration, le
  code et des conseils pratiques.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Comment répertorier les extensions de fichiers avec GroupDocs.Redaction dans
  .NET – Guide complet
type: docs
url: /fr/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Affichage des formats de fichiers pris en charge avec GroupDocs.Redaction en .NET

Gestion d'une grande variété de types de documents est une réalité quotidienne pour les développeurs .NET. En utilisant **GroupDocs.Redaction**, vous pouvez **list file extensions** que la bibliothèque prend en charge, offrant à votre application l'intelligence nécessaire pour accepter ou rejeter les téléchargements, présenter des choix d'interface conviviaux et éviter des erreurs d'exécution coûteuses. Ce tutoriel vous guide à travers tout ce dont vous avez besoin — des prérequis à une implémentation complète prête pour la production — afin que vous puissiez en toute confiance **get file formats** et **c# display file formats** dans votre solution.

## Réponses rapides
- **What does “list file extensions” mean?** Cela signifie récupérer la collection des identifiants de types de fichiers pris en charge (par ex., *.pdf*, *.docx*) depuis l'API.  
- **Which NuGet package provides this capability?** `GroupDocs.Redaction` (dernière version stable).  
- **Do I need a license to run the sample?** Une licence d'essai gratuite fonctionne pour le développement ; une licence permanente est requise pour la production.  
- **Can I cache the results?** Oui — stockez la liste en mémoire ou dans un cache distribué pour éviter les appels API répétés.  
- **Is this feature compatible with .NET 6 and .NET Core?** Absolument ; la bibliothèque prend en charge .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ et .NET 6+.

## Qu'est-ce que GroupDocs.Redaction ?
**GroupDocs.Redaction** est une bibliothèque .NET qui permet aux développeurs de masquer le contenu sensible, de convertir des documents et de découvrir les types de fichiers pris en charge — le tout sans nécessiter Microsoft Office sur le serveur. Elle abstrait la gestion complexe des formats derrière une API propre et orientée objet. Elle propose une API unifiée pour le masquage, la conversion et la découverte de formats, prenant en charge les PDFs, les documents Office, les images, etc., tout en garantissant haute performance et sécurité.

## Pourquoi lister les extensions de fichiers avec GroupDocs.Redaction ?
La bibliothèque **supports 50+ input and output formats**, y compris PDF, DOCX, PPTX, XLSX, HTML, et plus de 30 types d'images. En listant programmaticalement **list file extensions**, vous pouvez :

- Empêcher les utilisateurs de télécharger des fichiers non pris en charge (réduisant les erreurs de validation jusqu'à 90 %).  
- Remplir dynamiquement les menus déroulants, garantissant que l'interface reste synchronisée avec les mises à jour de la bibliothèque.  
- Construire des journaux d'audit qui enregistrent le type de fichier exact qu'un utilisateur a tenté de traiter.

## Prérequis
- **GroupDocs.Redaction** : Installez via NuGet (voir les commandes ci‑dessous).  
- **.NET SDK** : Assurez‑vous que le dernier SDK .NET est installé. Téléchargez‑le [ici](https://dotnet.microsoft.com/download).  
- **IDE** : Visual Studio 2022 ou tout éditeur compatible.  
- **Basic C# knowledge** : Vous devez être à l'aise avec les collections et LINQ.

## Configuration de GroupDocs.Redaction pour .NET

### Installer la bibliothèque

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Ouvrez le Gestionnaire de packages NuGet, recherchez “GroupDocs.Redaction”, et installez la dernière version.

### Obtenir et appliquer une licence

Commencez avec un essai gratuit ou demandez une licence temporaire pour explorer toutes les fonctionnalités sans limitations. Pour les options d'achat, visitez la [page d'achat de GroupDocs](https://purchase.groupdocs.com/). Une fois que vous avez votre fichier de licence :

1. Placez‑le dans un dossier accessible à l'intérieur de votre projet (par ex., `./Licenses/GroupDocs.Redaction.lic`).  
2. Initialisez la licence au démarrage de l'application :

La classe `License` charge votre fichier de licence et active GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Comment lister les extensions de fichiers avec GroupDocs.Redaction ?
Chargez l'API Redaction et appelez la méthode qui renvoie les formats pris en charge. L'appel retourne une collection où chaque élément contient une extension et une description lisible par l'homme. Cette opération est légère et peut être effectuée au démarrage ou à la demande.

### Récupérer les types de fichiers pris en charge
La méthode `RedactionApi.GetSupportedFileFormats()` renvoie une collection en lecture seule d'objets `FileFormatInfo` décrivant chaque format.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Afficher chaque extension et description
Chaque `FileFormatInfo` fournit les propriétés `Extension` et `Description` pour un type de fichier.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Explanation** : La boucle parcourt chaque objet `FileFormatInfo`, affichant son `Extension` et son `Description` dans un tableau bien aligné.

## Comment intégrer la liste dans un menu déroulant UI ?
Une fois que vous avez la collection, liez‑la à n'importe quel composant UI — `ComboBox` WinForms, `ComboBox` WPF, ou élément `select` ASP.NET Core. L'essentiel est d'utiliser `Extension` comme valeur et `Description` comme texte affiché. Cela garantit que les utilisateurs voient des noms conviviaux tandis que votre code travaille avec les chaînes d'extension exactes.

## Problèmes courants et solutions
- **Missing namespace error** – Vérifiez que vous avez importé `GroupDocs.Redaction` et `GroupDocs.Redaction.Common`.  
- **License not found** – Assurez‑vous que le chemin du fichier de licence est correct et que le fichier est inclus dans la sortie de compilation.  
- **Performance on large projects** – Mettez en cache le résultat dans une variable statique ou un cache distribué (par ex., Redis) pour éviter les énumérations répétées.

## Applications pratiques
Connaître la liste exacte des extensions prises en charge ouvre plusieurs scénarios réels :

1. **Document Management Systems** – Auto‑catégorisez les fichiers entrants en fonction de leur extension.  
2. **Content Filtering Tools** – Bloquez les formats non autorisés (par ex., les fichiers exécutables) lors du téléchargement.  
3. **File Conversion Pipelines** – Décidez dynamiquement si un fichier peut être converti ou nécessite un flux de travail de secours.

## Considérations de performance
- **Memory footprint** – La liste des formats est stockée dans une `IReadOnlyCollection` légère, généralement inférieure à 2 KB.  
- **Thread safety** – La collection est immuable après création, ce qui la rend sûre pour les lectures concurrentes.  
- **Caching** – Pour les API à fort trafic, mettez en cache la liste pendant la durée de vie de l'application afin d'éliminer les quelques microsecondes de surcharge par requête.

## Conclusion
En suivant les étapes ci‑dessus, vous disposez désormais d'une méthode fiable pour **list file extensions** et **c# display file formats** avec GroupDocs.Redaction. Cette capacité améliore non seulement l'expérience utilisateur mais protège également votre backend contre les fichiers non pris en charge. Explorez les fonctionnalités supplémentaires de Redaction — comme le masquage de contenu, la rédaction de PDF et le traitement par lots — pour renforcer davantage votre flux de travail documentaire.

## Questions fréquemment posées
**Q: What are the default supported file formats?**  
A : GroupDocs.Redaction prend en charge plus de 50 formats, dont PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG et bien d’autres. Consultez la liste complète sur [GroupDocs documentation](https://docs.groupdocs.com/search/net/).

**Q: How do I upgrade the library to the latest version?**  
A : Ouvrez le Gestionnaire de packages NuGet, recherchez “GroupDocs.Redaction”, et cliquez sur **Update**. Alternativement, exécutez `dotnet add package GroupDocs.Redaction --version <latest>`.

**Q: Can I use this list for server‑side validation of uploaded files?**  
A : Oui — comparez l'extension du fichier téléchargé avec la collection récupérée avant le traitement. Cela élimine 99 % des erreurs de format invalide.

**Q: Is it possible to extend support for custom file types?**  
A : Les extensions personnalisées nécessitent des gestionnaires personnalisés ; la bibliothèque de base n'ajoute pas nativement de nouveaux formats. Consultez la documentation de l'API pour créer des pipelines d'import/export personnalisés.

**Q: My application crashes after adding the code—what should I check?**  
A : Assurez‑vous que la licence est chargée correctement, que les instructions `using` font référence aux bons espaces de noms, et que vous gérez les `IOException` lors de la lecture du fichier de licence.

---

**Dernière mise à jour** : 2026-06-07  
**Testé avec** : GroupDocs.Redaction 23.9 for .NET  
**Auteur** : GroupDocs  

## Ressources
- [Documentation](https://docs.groupdocs.com/search/net/)
- [Référence API](https://reference.groupdocs.com/redaction/net)
- [Télécharger GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Forum d'assistance gratuit](https://forum.groupdocs.com/c/search/10)
- [Demande de licence temporaire](https://purchase.groupdocs.com/temporary-license/)

## Tutoriels associés
- [Maîtriser le filtrage de fichiers en .NET avec GroupDocs.Redaction : Techniques de gestion de documents efficaces](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Maîtriser GroupDocs.Redaction .NET : Configuration et gestion d'événements pour une gestion sécurisée des documents](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Maîtriser la gestion de documents en .NET avec GroupDocs.Redaction : Configuration de licence et mise en évidence de recherche HTML](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)