---
date: '2026-08-26'
description: Aprenda como os operadores booleanos Java permitem que você crie um search
  index rápido, execute content search Java e execute faceted queries com GroupDocs.Search.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: Aprenda como os operadores booleanos Java permitem que você construa
  um search index rápido, execute content search Java e execute faceted queries com
  GroupDocs.Search.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Operadores booleanos Java – construir search index e faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Operadores booleanos Java – criar search index & faceted search
type: docs
url: /pt/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Operadores booleanos Java – criar índice de busca & busca facetada

Implementar uma **experiência de busca** poderosa em Java pode parecer assustador, especialmente quando você precisa **criar um search index Java** que suporte **boolean operators Java** para consultas facetadas e complexas. Neste tutorial, percorreremos a configuração do **GroupDocs.Search for Java**, a construção de um índice, a adição de documentos e a criação de buscas facetadas simples e consultas sofisticadas de múltiplos critérios que utilizam lógica Booleana. Ao final, você entenderá como aproveitar as operações de **content search Java**, **filename search Java** e até mesmo **update index Java** para manter seus dados atualizados.

## Respostas rápidas
- **O que é uma busca facetada?** Uma forma de filtrar resultados por categorias predefinidas, como tipo de arquivo ou data.  
- **Como criar um search index Java?** Inicialize um objeto `Index` apontando para uma pasta e adicione documentos.  
- **Posso combinar múltiplos critérios com operadores booleanos?** Sim—use consultas baseadas em objetos ou operadores Booleanos em uma consulta de texto.  
- **Preciso de uma licença?** Um teste gratuito funciona para desenvolvimento; uma licença comercial remove limites.  
- **Qual IDE funciona melhor?** Qualquer IDE Java (IntelliJ IDEA, Eclipse, NetBeans) funciona bem.

## O que é “create search index java”?

Criar um search index Java significa construir uma estrutura baseada em disco que armazena o texto e os metadados dos documentos, permitindo a recuperação instantânea de documentos correspondentes por meio de consultas. O índice mapeia termos para identificadores de documentos, suporta buscas rápidas e pode ser atualizado incrementalmente à medida que os arquivos mudam, fornecendo a base para recursos de busca poderosos.

## Por que usar GroupDocs.Search para consultas facetadas e complexas?

O GroupDocs.Search for Java oferece facetas integradas, suporte a consultas Booleanas e indexação de alto desempenho que pode lidar com até 10 milhões de documentos, mantendo a latência de consultas abaixo de 200 ms em hardware de servidor típico. Ele fornece filtros de campo prontos para uso, uma linguagem de consulta rica e compatibilidade pura em Java, tornando‑o ideal para cenários de busca em escala empresarial.

## Pré-requisitos

Antes de começarmos, certifique‑se de que você tem o seguinte:

- **JDK 8 ou superior** instalado e configurado em sua IDE.  
- **Maven** (ou Gradle) para gerenciamento de dependências.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Familiaridade básica com conceitos OOP de Java e estrutura de projetos Maven.

## Configurando GroupDocs.Search para Java

### Configuração do Maven
Adicione o repositório e a dependência ao seu arquivo `pom.xml`:

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

### Download direto
Alternativamente, faça o download do JAR mais recente na página oficial de lançamentos:  
[GroupDocs.Search para Java releases](https://releases.groupdocs.com/search/java/)

### Aquisição de licença
Para desbloquear a funcionalidade completa:

1. **Teste gratuito** – perfeito para desenvolvimento e teste.  
2. **Licença de avaliação temporária** – estende os limites do teste.  
3. **Licença comercial** – remove todas as restrições para uso em produção.

### Inicialização e configuração básica
A classe `Index` é o componente central que representa um índice pesquisável armazenado em disco. O trecho a seguir mostra como **criar um search index Java** instanciando a classe `Index`:

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

Com o índice pronto, podemos avançar para consultas facetadas e complexas do mundo real.

## Como usar boolean operators java – Busca facetada simples

Carregue seu índice, adicione documentos e emita uma consulta de campo; o padrão de duas etapas permite recuperar contagens de facetas e resultados filtrados em uma única chamada. Essa abordagem oferece aos usuários uma maneira intuitiva de restringir resultados por categorias como tipo de arquivo, autor ou metadados personalizados.

### Etapa 1: Criar um índice
Primeiro, aponte o `Index` para uma pasta onde os arquivos de índice serão armazenados.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Etapa 2: Adicionar documentos ao índice
Informe ao GroupDocs.Search onde seus documentos de origem estão. Todos os tipos de arquivo suportados (PDF, DOCX, TXT, etc.) serão indexados automaticamente.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Etapa 3: Executar uma busca no campo de conteúdo com uma consulta de texto
Uma consulta de texto rápida filtra pelo campo `content`. A sintaxe `content: Pellentesque` limita os resultados a documentos que contêm a palavra *Pellentesque* em seu texto principal.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Etapa 4: Executar uma busca usando uma consulta de objeto
Consultas baseadas em objetos dão controle granular. Aqui construímos uma consulta de palavra, a encapsulamos em uma consulta de campo e a executamos.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Como usar boolean operators java – Busca de consulta complexa

Para executar uma consulta complexa, combine múltiplas condições de campo com operadores AND/OR/NOT e, opcionalmente, inclua buscas por frases. Você pode especificar cada condição usando consultas de campo, aninhá‑las com operadores Booleanos e controlar a relevância com boosting, permitindo recuperar apenas os documentos mais relevantes que satisfaçam todos os critérios necessários.

### Etapa 1: Criar um índice para consultas complexas
Reutilize a mesma estrutura de pastas; você pode compartilhar o índice entre cenários simples e complexos.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Etapa 2: Executar uma busca com uma consulta de texto
A consulta a seguir procura arquivos nomeados *lorem* **e** *ipsum* **ou** conteúdo contendo qualquer uma das duas frases exatas.

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

### Etapa 3: Executar uma busca com uma consulta de objeto
A construção baseada em objetos espelha a consulta textual, mas oferece segurança de tipo e assistência da IDE.

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

## Aplicações práticas de buscas facetadas e complexas

| Cenário | Como a faceta ajuda | Consulta de exemplo |
|----------|-------------------|---------------|
| **Catálogo de comércio eletrônico** | Filtrar por categoria, preço, marca | `category: Electronics AND price:[100 TO 500]` |
| **Repositório de documentos legais** | Restringir por número do caso, jurisdição | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Arquivos de pesquisa** | Combinar autor, ano de publicação, palavras‑chave | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Intranet corporativa** | Buscar por tipo de arquivo e departamento | `filetype: pdf AND department: HR` |

Esses exemplos ilustram por que dominar as técnicas de **boolean operators java** e **filename search java** é um divisor de águas para qualquer aplicação intensiva em dados.

## Armadilhas comuns & solução de problemas

O objeto `SearchResult` contém os documentos que correspondem a uma consulta e fornece acesso às suas pontuações de relevância e fragmentos destacados.  
A classe `CommonFieldNames` define nomes de campo padrão, como `Content` e `FileName`, usados em toda a API.

- **Resultados vazios** – Verifique se os documentos foram adicionados com sucesso (`index.getDocumentCount()` pode ajudar).  
- **Índice obsoleto** – Após adicionar ou remover arquivos, chame `index.update()` para **update index java** e manter o índice sincronizado.  
- **Nomes de campo incorretos** – Use as constantes `CommonFieldNames` (`Content`, `FileName`, etc.) para evitar erros de digitação.  
- **Gargalos de desempenho** – Para coleções enormes, considere habilitar `index.setCacheSize()` ou usar um SSD dedicado para a pasta de índice.  
- **Destaques ausentes** – Para **highlight search results java**, recupere os fragmentos correspondentes via `SearchResult.getFragments()` (não mostrado aqui, mas disponível na API).  

## Perguntas frequentes

**Q: Posso usar o GroupDocs.Search com Spring Boot?**  
A: Absolutamente. Adicione a dependência Maven, configure o índice como um bean Spring e injete‑o onde precisar de recursos de busca.

**Q: A biblioteca suporta campos de metadados personalizados?**  
A: Sim – você pode adicionar campos definidos pelo usuário durante a indexação e então facetá‑los.

**Q: Quão grande o índice pode crescer?**  
A: O índice baseado em disco pode lidar com até 10 milhões de documentos; basta garantir armazenamento suficiente e monitorar as configurações de cache.

**Q: Existe uma forma de classificar resultados por relevância?**  
A: O GroupDocs.Search pontua automaticamente as correspondências; você pode recuperar a pontuação via `SearchResult.getDocument(i).getScore()`.

**Q: O que acontece se eu indexar PDFs criptografados?**  
A: Forneça a senha ao adicionar o documento: `index.add(filePath, password)`.

## Conclusão

Até agora você deve se sentir confortável **criando um search index Java** com o GroupDocs.Search, adicionando documentos e criando tanto consultas facetadas simples quanto buscas Booleanas sofisticadas usando **boolean operators java**. Essas capacidades permitem que você ofereça experiências de busca rápidas, precisas e amigáveis ao usuário em uma ampla gama de aplicações — desde plataformas de comércio eletrônico até bases de conhecimento corporativas.

Pronto para o próximo passo? Explore os recursos avançados do **GroupDocs.Search**, como **highlighting**, **suggestions** e **real‑time indexing**, para aumentar ainda mais o poder de busca da sua aplicação.

---

**Última atualização:** 2026-08-26  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Tutoriais relacionados

- [Busca curinga Java com GroupDocs.Search – Recursos avançados](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Como atualizar o Index Java com GroupDocs.Search – Um guia abrangente](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Como implementar busca de texto completo em java: criar diretório de índice com GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)