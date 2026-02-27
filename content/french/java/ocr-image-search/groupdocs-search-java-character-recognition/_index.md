---
date: '2026-01-11'
description: Apprenez à créer un index de recherche personnalisé avec GroupDocs.Search
  pour Java, en configurant les caractères réguliers et mélangés pour une recherche
  OCR avancée et la recherche d’images.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Créer un index de recherche personnalisé avec reconnaissance de caractères
  – GroupDocs.Search Java
type: docs
url: /fr/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Créer un index de recherche personnalisé avec reconnaissance de caractères à l'aide de GroupDocs.Search pour Java

Dans les applications modernes très axées sur les documents, **créer un index de recherche personnalisé** qui comprend les subtilités de votre texte — telles que les traits d’union, les underscores ou les symboles spécifiques à une langue — est essentiel pour une récupération rapide et précise. Ce tutoriel vous guide à travers la configuration de la reconnaissance de caractères dans **GroupDocs.Search pour Java**, en couvrant à la fois les caractères réguliers (lettres, chiffres, underscores) et les caractères fusionnés (par exemple, les traits d’union). À la fin, vous serez capable d’adapter un index qui répond exactement aux besoins de votre scénario OCR ou de recherche d’images.

## Réponses rapides
- **Que signifie « créer un index de recherche personnalisé » ?** Cela consiste à configurer un index pour traiter des symboles spécifiques comme des lettres ou des caractères fusionnés, plutôt que de les ignorer.  
- **Quelle bibliothèque est utilisée ?** GroupDocs.Search pour Java (v25.4 au moment de la rédaction).  
- **Ai‑je besoin d’une licence ?** Un essai gratuit suffit pour le développement ; une licence payante est requise pour la production.  
- **Puis‑je indexer à la fois des PDF et des images ?** Oui — GroupDocs.Search prend en charge l’OCR sur les images et les PDF lorsqu’il est correctement configuré.  
- **Maven est‑il obligatoire ?** Maven est la méthode recommandée pour gérer les dépendances, mais vous pouvez également utiliser Gradle ou des JARs manuels.

## Qu’est‑ce qu’un index de recherche personnalisé ?
Un index de recherche personnalisé vous permet de définir comment le moteur de recherche interprète les caractères. Par défaut, de nombreux symboles sont ignorés, ce qui peut entraîner des correspondances manquées pour des éléments tels que les numéros de dossier (`ABC-123`) ou les extraits de code (`my_variable`). Ajuster le dictionnaire d’alphabet vous donne un contrôle total sur ce que le moteur considère comme texte indexable.

## Pourquoi configurer les caractères réguliers et fusionnés ?
- **Caractères réguliers** (lettres, chiffres, underscores) sont traités comme des jetons autonomes, améliorant les recherches en correspondance exacte.  
- **Caractères fusionnés** (traits d’union, barres obliques) relient des mots ; les configurer empêche une division indésirable des jetons, ce qui est crucial pour les références juridiques, les codes produit ou l’indexation de code source.

## Prérequis
- **JDK 8** ou version ultérieure installé.  
- **Maven** pour la gestion des dépendances.  
- Accès à la bibliothèque **GroupDocs.Search pour Java** (téléchargée via Maven ou le site officiel).  

### Bibliothèques et dépendances requises
Ajoutez les entrées de dépôt et de dépendance à votre `pom.xml` (comme indiqué ci‑dessous). Le bloc XML doit rester inchangé.

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

Vous pouvez également télécharger les derniers JARs depuis [versions de GroupDocs.Search pour Java](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
- **Essai gratuit** – idéal pour les premières expérimentations.  
- **Licence temporaire** – utile pour des cycles de développement plus longs.  
- **Licence de production** – requise pour le déploiement commercial.  

Obtenez une licence via le portail officiel : [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Initialisation de base
L’extrait ci‑dessous montre le code minimal nécessaire pour créer un index vide. Conservez‑le tel quel ; nous le développerons plus tard.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Configuration de GroupDocs.Search pour Java

### Installation via Maven
La configuration Maven de la section *Prérequis* est tout ce dont vous avez besoin. Après l’avoir ajoutée, exécutez `mvn clean install` pour récupérer les binaires.

### Exigences de configuration de l’environnement
- Assurez‑vous que le **dossier d’index** et le **dossier de documents** existent sur le disque.  
- Utilisez des chemins absolus ou configurez votre IDE pour résoudre correctement les chemins relatifs.  

## Guide d’implémentation

Ci‑dessous, nous parcourons deux fonctionnalités distinctes : **caractères réguliers** et **caractères fusionnés**. Chaque fonctionnalité suit le même schéma — définir les chemins, créer l’index, définir le dictionnaire de caractères, puis indexer vos documents.

### Fonctionnalité 1 – Caractères réguliers

#### Vue d’ensemble
Les caractères réguliers sont traités comme des jetons indépendants. C’est idéal lorsque vous voulez que les chiffres, lettres et underscores soient recherchables exactement tels quels.

#### Implémentation pas à pas

**1️⃣ Définir les chemins**  
Spécifiez où l’index sera stocké et où se trouvent vos documents source.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Créer et configurer l’index**  
Instanciez l’index et effacez toute configuration d’alphabet pré‑existante.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Définir les caractères réguliers**  
Construisez un tableau de caractères incluant les chiffres, les lettres latines et l’underscore.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Indexer les documents**  
Ajoutez tous les fichiers du dossier source à l’index nouvellement configuré.

```java
index.add(documentFolder);
```

### Fonctionnalité 2 – Caractères fusionnés

#### Vue d’ensemble
Les caractères fusionnés (comme les traits d’union) relient souvent deux mots. Les marquer comme *fusionnés* indique au moteur de garder les jetons environnants ensemble lors de l’indexation.

#### Implémentation pas à pas

**1️⃣ Définir les chemins**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Créer et configurer l’index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Définir les caractères fusionnés**  
Ici, nous indiquons au dictionnaire que le trait d’union doit être traité comme un caractère fusionné.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Indexer les documents**  

```java
index.add(documentFolder);
```

## Applications pratiques

### Cas d’utilisation 1 – Gestion de documents juridiques
Les dossiers juridiques contiennent souvent des numéros de dossier comme `2023-AB-456`. En configurant les underscores et les traits d’union, les recherches renvoient des correspondances exactes sans scinder l’identifiant.

### Cas d’utilisation 2 – Référentiels de code source
Les développeurs doivent rechercher des extraits de code où les underscores (`my_variable`) et les traits d’union (`my-function`) sont significatifs. La reconnaissance de caractères personnalisée garantit que le moteur de recherche respecte ces symboles.

### Cas d’utilisation 3 – Jeux de données multilingues
Lorsque vous travaillez avec des langues qui utilisent des alphabets supplémentaires, vous pouvez étendre l’ensemble des caractères réguliers pour inclure ces plages Unicode, assurant ainsi des résultats de recherche précis entre plusieurs langues.

## Considérations de performance

- **Gestion des ressources** – Surveillez l’utilisation du tas ; les gros index bénéficient de validations incrémentielles.  
- **Garbage Collection** – Libérez les objets `Index` une fois terminés afin que la JVM récupère la mémoire.  
- **Optimisation de l’index** – Appelez périodiquement `index.optimize()` (si disponible) pour compacter l’index et améliorer la vitesse des requêtes.  

## Conclusion

Vous savez maintenant comment **créer un index de recherche personnalisé** qui distingue les caractères réguliers des caractères fusionnés à l’aide de GroupDocs.Search pour Java. Ce contrôle fin vous permet de construire des solutions de recherche OCR‑aware, haute performance, adaptées aux environnements juridiques, de développement ou multilingues.

**Prochaines étapes**  
- Expérimentez avec des plages Unicode supplémentaires pour les alphabets non latins.  
- Combinez la configuration des caractères avec d’autres fonctionnalités de GroupDocs.Search comme le stemming ou les synonymes.  
- Intégrez l’index dans une API REST pour exposer les capacités de recherche aux applications front‑end.

## Foire aux questions

**Q :** *Quel est le rôle de `CharacterType.Letter` ?*  
**R :** Il indique à l’index de traiter les caractères fournis comme des lettres régulières, de sorte qu’ils soient tokenisés séparément lors de l’indexation.

**Q :** *Puis‑je mélanger des caractères réguliers et fusionnés dans le même index ?*  
**R :** Oui — appelez simplement `setRange` pour chaque type ; le dictionnaire gérera les deux configurations simultanément.

**Q :** *Dois‑je reconstruire l’index après avoir modifié l’alphabet ?*  
**R :** Absolument. Les changements du dictionnaire de caractères affectent la tokenisation, il faut donc ré‑indexer les documents pour appliquer les nouvelles règles.

**Q :** *Existe‑t‑il une limite au nombre de caractères personnalisés que je peux définir ?*  
**R :** La bibliothèque prend en charge l’ensemble complet de l’Unicode ; les performances peuvent se dégrader si vous ajoutez un ensemble extrêmement vaste, il est donc recommandé de ne retenir que les caractères réellement nécessaires.

**Q :** *Comment cela influence‑t‑il la précision de l’OCR ?*  
**R :** En alignant l’ensemble de caractères de l’index avec la sortie du moteur OCR, vous réduisez les faux négatifs et améliorez la pertinence globale des recherches.

---

**Dernière mise à jour :** 2026-01-11  
**Testé avec :** GroupDocs.Search 25.4 pour Java  
**Auteur :** GroupDocs  

---