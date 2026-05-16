---
date: '2026-02-16'
description: Tanulja meg, hogyan használhatja a logikai operátorokat Java-ban a GroupDocs.Search
  segítségével keresőindex létrehozásához, tartalomkereséshez és facettált lekérdezésekhez,
  ezáltal növelve a teljesítményt és a felhasználói élményt.
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: Boolean operátorok Java – Keresési index létrehozása és fácett keresés
type: docs
url: /hu/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean Operators Java – Keresési Index Létrehozása és Facettált Keresés

Implementing a powerful **search experience** in Java can feel overwhelming, especially when you need to **create a search index Java** that supports **boolean operators Java** for faceted and complex queries. In this tutorial we’ll walk through setting up **GroupDocs.Search for Java**, building an index, adding documents, and crafting both simple faceted searches and sophisticated multi‑criteria queries that use Boolean logic. By the end you’ll understand how to leverage **content search Java**, **filename search Java**, and even **update index java** operations to keep your data fresh.

## Gyors válaszok
- **Mi az a facettált keresés?** A way to filter results by predefined categories such as file type or date.  
- **Hogyan hozhatok létre keresési indexet Java-ban?** Initialize an `Index` object pointing to a folder and add documents.  
- **Kombinálhatok több kritériumot Boolean operátorokkal?** Yes—use object‑based queries or Boolean operators in a text query.  
- **Szükségem van licencre?** A free trial works for development; a commercial license removes limits.  
- **Melyik IDE a legjobb?** Any Java IDE (IntelliJ IDEA, Eclipse, NetBeans) works fine.

## Mi az a “create search index java”?
Creating a search index in Java means building a searchable data structure that stores document metadata and content, enabling fast retrieval based on user queries. With GroupDocs.Search, the index lives on disk, can be updated incrementally, and supports advanced features like faceting, **boolean operators Java**, and complex Boolean logic.

## Miért használjuk a GroupDocs.Search-t facettált és összetett lekérdezésekhez?
- **Out‑of‑the‑box faceting** – filter by fields such as file name, size, or custom metadata.  
- **Rich query language** – mix text, phrase, and field queries using AND/OR/NOT operators (the core of **boolean operators java**).  
- **Scalable performance** – indexes millions of documents while keeping latency low.  
- **Pure Java** – no native dependencies, works on any platform that runs JDK 8+.  
- **Easy index maintenance** – call `index.update()` to **update index java** after adding or removing files.

## Előkövetelmények

- **JDK 8 vagy újabb** installed and configured in your IDE.  
- **Maven** (or Gradle) for dependency management.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Basic familiarity with Java OOP concepts and Maven project structure.

## A GroupDocs.Search for Java beállítása

### Maven beállítás
Add the repository and dependency to your `pom.xml` file:

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

### Közvetlen letöltés
Alternatively, download the latest JAR from the official release page:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Licenc beszerzése
To unlock full functionality:

1. **Free trial** – perfect for development and testing.  
2. **Temporary evaluation license** – extends trial limits.  
3. **Commercial license** – removes all restrictions for production use.

### Alapvető inicializálás és beállítás
The following snippet shows how to **create a search index Java** by instantiating the `Index` class:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

With the index ready, we can move on to real‑world faceted and complex queries.

## Hogyan használjuk a boolean operators java – Egyszerű facettált keresés

Faceted search lets end‑users narrow results by selecting values from predefined categories (facets). Below is a step‑by‑step walk‑through.

### 1. lépés: Index létrehozása
First, point the `Index` to a folder where the index files will be stored.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### 2. lépés: Dokumentumok hozzáadása az indexhez
Tell GroupDocs.Search where your source documents live. All supported file types (PDF, DOCX, TXT, etc.) will be indexed automatically.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### 3. lépés: Keresés a Content mezőben szöveges lekérdezéssel
A quick text query filters by the `content` field. The syntax `content: Pellentesque` limits results to documents containing the word *Pellentesque* in their body text.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### 4. lépés: Keresés objektum lekérdezéssel
Object‑based queries give you fine‑grained control. Here we build a word query, wrap it in a field query, and execute it.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Hogyan használjuk a boolean operators java – Összetett lekérdezés keresés

Complex queries combine multiple fields, Boolean operators, and phrase searches. This is ideal for scenarios like e‑commerce filters or legal document research.

### 1. lépés: Index létrehozása összetett lekérdezésekhez
Reuse the same folder structure; you can share the index across both simple and complex scenarios.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### 2. lépés: Keresés szöveges lekérdezéssel
The following query looks for files named *lorem* **and** *ipsum* **or** content containing either of two exact phrases.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### 3. lépés: Keresés objektum lekérdezéssel
Object‑based construction mirrors the textual query but offers type safety and IDE assistance.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Gyakorlati alkalmazások a facettált és összetett keresésekhez

| Forgatókönyv | Hogyan segít a faceting | Példa lekérdezés |
|--------------|------------------------|-----------------|
| **E‑commerce catalog** | Szűrés kategória, ár, márka szerint | `category: Electronics AND price:[100 TO 500]` |
| **Legal document repository** | Szűrés ügyiratszám, joghatóság szerint | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Research archives** | Szerző, publikáció éve, kulcsszavak kombinálása | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Enterprise intranet** | Keresés fájltípus és részleg szerint | `filetype: pdf AND department: HR` |

These examples illustrate why mastering **boolean operators java** and **filename search java** techniques is a game‑changer for any data‑intensive application.

## Gyakori hibák és hibaelhárítás

- **Empty results** – Verify that the documents were successfully added (`index.getDocumentCount()` can help).  
- **Stale index** – After adding or removing files, call `index.update()` to **update index java** and keep the index in sync.  
- **Incorrect field names** – Use `CommonFieldNames` constants (`Content`, `FileName`, etc.) to avoid typos.  
- **Performance bottlenecks** – For huge collections, consider enabling `index.setCacheSize()` or using a dedicated SSD for the index folder.  
- **Missing highlights** – To **highlight search results java**, retrieve the matched fragments via `SearchResult.getFragments()` (not shown here but available in the API).  

## Gyakran ismételt kérdések

**Q: Can I use GroupDocs.Search with Spring Boot?**  
A: Absolutely. Add the Maven dependency, configure the index as a Spring bean, and inject it wherever you need search capabilities.

**Q: Does the library support custom metadata fields?**  
A: Yes – you can add user‑defined fields during indexing and then facet on them.

**Q: How large can the index grow?**  
A: The index is disk‑based and can handle millions of documents; just ensure sufficient storage and monitor cache settings.

**Q: Is there a way to rank results by relevance?**  
A: GroupDocs.Search automatically scores matches; you can retrieve the score via `SearchResult.getDocument(i).getScore()`.

**Q: What happens if I index encrypted PDFs?**  
A: Provide the password when adding the document: `index.add(filePath, password)`.

## Következtetés

By now you should feel comfortable **creating a search index Java** with GroupDocs.Search, adding documents, and crafting both simple faceted queries and sophisticated Boolean searches using **boolean operators java**. These capabilities empower you to deliver fast, accurate, and user‑friendly search experiences across a wide range of applications—from e‑commerce platforms to enterprise knowledge bases.

Ready for the next step? Explore **GroupDocs.Search’s** advanced features such as **highlighting**, **suggestions**, and **real‑time indexing** to further boost your application’s search power.

---

**Legutóbb frissítve:** 2026-02-16  
**Tesztelve a következővel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs