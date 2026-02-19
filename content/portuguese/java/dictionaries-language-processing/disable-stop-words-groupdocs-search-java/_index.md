---
date: '2026-02-19'
description: Aprenda como desativar palavras‑stop na pesquisa e adicionar documentos
  ao índice com o GroupDocs.Search para Java, aumentando a precisão da consulta.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 'Palavras de parada na pesquisa: adicionar documentos ao índice com GroupDocs.Search
  Java'
type: docs
url: /pt/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Stop Words in Search: Add Documents to Index with GroupDocs.Search Java

Se você precisa **adicionar documentos ao índice** garantindo que nenhum termo importante—especialmente os mais comuns—seja ignorado, está no lugar certo. Neste guia mostraremos como **desativar stop words na pesquisa** usando o GroupDocs.Search para Java, de modo que cada token (mesmo “on”, “by” ou “the”) se torne pesquisável e seus resultados sejam muito mais precisos.

## Quick Answers
- **O que significa “add documents to index”?** Significa carregar seus arquivos de origem em um índice pesquisável para que possam ser consultados de forma eficiente.  
- **Por que eu desativaria stop words?** Para incluir palavras comuns (ex.: “on”, “the”) nas pesquisas quando esses termos são relevantes para o seu domínio.  
- **Qual versão da biblioteca é necessária?** GroupDocs.Search for Java 25.4 ou posterior.  
- **Preciso de licença?** Um teste gratuito funciona para avaliação; uma licença permanente é necessária para produção.  
- **Posso usar isso em um projeto Maven?** Sim – basta adicionar o repositório e a dependência mostrados abaixo.

## What are stop words in search and why might you want to disable them?
Stop words são termos frequentes que muitos mecanismos de busca filtram automaticamente para acelerar as consultas. Embora isso melhore o desempenho em buscas genéricas na web, pode prejudicar a precisão em domínios especializados—contratos legais, catálogos de e‑commerce ou manuais técnicos—onde palavras como “on”, “by” ou “as” carregam significado real. Desativar stop words permite tratar cada palavra como significativa, garantindo que nenhum documento relevante seja perdido.

## How does adding documents to index work in GroupDocs.Search?
Ao adicionar documentos, a biblioteca lê cada arquivo, tokeniza seu conteúdo e armazena os tokens em uma estrutura de dados otimizada (o índice). Uma vez indexado, o motor pode recuperar documentos correspondentes em milissegundos, mesmo para coleções grandes.

## Prerequisites

- **Bibliotecas Necessárias**: GroupDocs.Search for Java 25.4 (ou mais recente).  
- **Ambiente de Desenvolvimento**: IntelliJ IDEA, Eclipse ou qualquer IDE Java de sua preferência.  
- **Conhecimento Básico**: Familiaridade com a sintaxe Java e o conceito de indexação.

## Setting Up GroupDocs.Search for Java

### Maven Installation

Se você usa Maven, inclua o seguinte no seu `pom.xml`:

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

### Direct Download

Alternativamente, faça o download da versão mais recente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### License Acquisition Steps
- **Free Trial** – comece a testar imediatamente.  
- **Temporary License** – obtenha uma chave temporária para funcionalidade completa.  
- **Purchase** – adquira uma licença permanente para uso em produção.

## Basic Initialization and Setup

Crie uma instância de `IndexSettings` para controlar o comportamento do índice:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## How to disable stop words in search (Java)

A linha a seguir desativa o filtro interno de stop‑words:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Parâmetros*: `setUseStopWords` aceita um boolean.  
*Objetivo*: Garante que cada palavra—incluindo stop words comuns—seja indexada e pesquisável.

## How to add documents to index

### Defining the Output Directory

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Specifying the Document Directory

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Agora cada arquivo em `YOUR_DOCUMENT_DIRECTORY` é **added documents to index** e está pronto para consultas.

## Performing a Search Query

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Como as stop words estão desativadas, o termo `"on"` será considerado durante a pesquisa, retornando correspondências que de outra forma seriam ignoradas.

## Practical Applications

1. **Enterprise Document Search** – Garanta que terminologia crítica não seja filtrada.  
2. **E‑commerce Platforms** – Melhore a descoberta de produtos indexando cada palavra nas descrições.  
3. **Legal Research Tools** – Capture todos os termos jurídicos, mesmo aqueles normalmente tratados como stop words.

## Performance Considerations

- **Optimization Tips**: Atualize e faça a limpeza do índice regularmente para manter alta velocidade de busca.  
- **Resource Usage**: Monitore o tamanho do heap da JVM; índices grandes podem exigir ajustes nas configurações de coleta de lixo.  
- **Java Memory Management**: Use estruturas de dados eficientes e considere armazenamento off‑heap para corpora muito grandes.

## Common Issues and Solutions

| Symptom | Likely Cause | Fix |
|---|---|---|
| No results for common words | `setUseStopWords(true)` (default) | Call `setUseStopWords(false)` as shown above. |
| Out‑of‑memory errors during indexing | Indexing too many large files at once | Index files in batches; increase `-Xmx` JVM option. |
| Search returns stale data | Index not refreshed after adding new files | Call `index.update()` or re‑add the changed documents. |

## Frequently Asked Questions

**Q: What are stop words?**  
A: Stop words are common terms (e.g., “the”, “is”, “on”) that many search engines ignore to speed up queries. Disabling them lets you treat every token as searchable.

**Q: Why disable stop words in search indexes?**  
A: When exact phrase matching is required—such as in legal or technical documents—every word carries meaning, so you need to include stop words.

**Q: How does GroupDocs.Search handle large datasets?**  
A: The library uses optimized data structures and incremental indexing to keep memory usage low, even with millions of documents.

**Q: Can I integrate GroupDocs.Search with other Java applications?**  
A: Yes, the API is designed for easy embedding into any Java‑based system, from web services to desktop apps.

**Q: What should I do if my search results are not accurate?**  
A: Verify that the index includes all required documents (`add documents to index`), ensure stop‑word filtering is disabled if needed, and consider re‑building the index after major changes.

## Additional Resources

- **Documentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **GitHub Repository**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free Support**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Seguindo este guia, você agora sabe como **add documents to index** e **disable stop words in search** para oferecer resultados mais precisos em suas aplicações Java.

---

**Last Updated:** 2026-02-19  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs