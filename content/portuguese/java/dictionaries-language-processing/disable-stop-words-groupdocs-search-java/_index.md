---
date: '2026-07-07'
description: Aprenda como desativar stop words Java e add documents to index usando
  GroupDocs.Search para Java, boosting search accuracy and performance.
keywords:
- disable stop words java
- add documents to index
- groupdocs search java
og_description: Desativar stop words Java e add documents to index com GroupDocs.Search
  para Java. Siga este guia passo a passo para melhorar query accuracy e performance.
og_title: Desativar stop words Java – Add Docs to Index com GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  headline: Disable Stop Words Java – Add Docs to Index with GroupDocs
  type: TechArticle
- description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  name: Disable Stop Words Java – Add Docs to Index with GroupDocs
  steps:
  - name: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
    text: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
  - name: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
    text: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
  - name: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
    text: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
  type: HowTo
- questions:
  - answer: Stop words are common terms (e.g., “the”, “is”, “on”) that many search
      engines ignore to speed up queries. Disabling them lets you treat every token
      as searchable.
    question: What are stop words?
  - answer: When exact phrase matching is required—such as in legal or technical documents—every
      word carries meaning, so you need to include stop words.
    question: Why disable stop words in search indexes?
  - answer: The library uses optimized data structures and incremental indexing to
      keep memory usage low, even with **millions of documents**.
    question: How does GroupDocs.Search handle large datasets?
  - answer: Yes, the API is designed for easy embedding into any Java‑based system,
      from web services to desktop apps.
    question: Can I integrate GroupDocs.Search with other Java applications?
  - answer: Verify that the index includes all required files (`add documents to index`),
      ensure stop‑word filtering is disabled when needed, and consider rebuilding
      the index after major changes.
    question: What should I do if my search results are not accurate?
  type: FAQPage
title: Desativar stop words Java – Add Docs to Index com GroupDocs
type: docs
url: /pt/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Desativar Palavras‑vazias Java – Adicionar Documentos ao Índice com GroupDocs

Neste tutorial, você descobrirá como **disable stop words java** ao adicionar seus arquivos a um índice pesquisável com GroupDocs.Search for Java. Ao desativar o filtro interno de palavras‑vazias, cada token — incluindo palavras comuns como “on”, “by” ou “the” — torna‑se pesquisável, o que melhora drasticamente a relevância dos resultados para domínios especializados, como contratos legais, catálogos de comércio eletrônico ou manuais técnicos.

## Respostas Rápidas
- **O que significa “add documents to index”?** Significa carregar seus arquivos de origem em um índice pesquisável para que possam ser consultados de forma eficiente.  
- **Por que eu desativaria palavras‑vazias?** Para incluir palavras comuns (por exemplo, “on”, “the”) nas buscas quando esses termos são significativos para o seu domínio.  
- **Qual versão da biblioteca é necessária?** GroupDocs.Search for Java 25.4 ou posterior.  
- **Preciso de uma licença?** Um teste gratuito funciona para avaliação; uma licença permanente é necessária para produção.  
- **Posso usar isso em um projeto Maven?** Sim – basta adicionar o repositório e a dependência mostrados abaixo.

## O que são palavras‑vazias na pesquisa e por que você pode querer desativá‑las?

Palavras‑vazias são termos de alta frequência que muitos mecanismos de busca filtram automaticamente para acelerar o processamento de consultas. Desativá‑las garante que **every word** — incluindo aquelas tradicionalmente ignoradas — contribua para o índice de pesquisa, o que é essencial quando essas palavras carregam significado específico do domínio. Por exemplo, em um contrato legal a palavra “by” pode distinguir as partes, e em um catálogo de produtos “on” pode fazer parte do nome de um modelo.

## Como funciona a adição de documentos ao índice no GroupDocs.Search?

Quando você adiciona documentos, o GroupDocs.Search lê cada arquivo, tokeniza o conteúdo e armazena os tokens em um índice invertido otimizado. Essa estrutura permite recuperação em subsegundos mesmo para coleções contendo **hundreds of thousands of files**. A biblioteca também suporta atualizações incrementais, de modo que você pode manter o índice atualizado sem reconstruí‑lo do zero.

## Pré‑requisitos

- **Bibliotecas Necessárias**: GroupDocs.Search for Java 25.4 (ou mais recente).  
- **Ambiente de Desenvolvimento**: IntelliJ IDEA, Eclipse ou qualquer IDE Java de sua preferência.  
- **Conhecimento Básico**: Familiaridade com a sintaxe Java e o conceito de indexação.

## Configurando o GroupDocs.Search para Java

### Instalação via Maven

Se você estiver usando Maven, inclua o seguinte no seu `pom.xml`:

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

### Download Direto

Alternativamente, baixe a versão mais recente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Etapas de Aquisição de Licença
- **Teste Gratuito** – comece a testar imediatamente.  
- **Licença Temporária** – obtenha uma chave de tempo limitado para funcionalidade completa.  
- **Compra** – adquira uma licença permanente para uso em produção.

## Inicialização e Configuração Básicas

IndexSettings é uma classe de configuração que define como o índice é construído, pesquisado e quais recursos são habilitados.

Crie uma instância de `IndexSettings` para controlar o comportamento do índice:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Como desativar palavras‑vazias na pesquisa (Java)?

IndexSettings é o objeto de configuração que controla o comportamento do índice de pesquisa. Por padrão, ele habilita um filtro interno de palavras‑vazias. Para desativar esse filtro, chame o método `setUseStopWords(false)` na instância de `IndexSettings`. Essa única chamada desativa a remoção de palavras‑vazias, garantindo que cada token — incluindo palavras comuns como “on” ou “the” — seja indexado e possa ser consultado.

## Como adicionar documentos ao índice

Adicionar documentos ao índice é realizado criando um objeto `Index` com o `IndexSettings` desejado e, em seguida, invocando seu método `add` para cada arquivo ou pasta. A biblioteca lê cada documento, tokeniza seu conteúdo e armazena os termos resultantes no índice invertido, tornando‑os pesquisáveis instantaneamente. Você pode apontar o índice para um diretório de saída específico e especificar a pasta de origem contendo os arquivos a serem indexados.

### Definindo o Diretório de Saída

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

### Especificando o Diretório de Documentos

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

## Executando uma Consulta de Pesquisa

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Como `disable stop words java` está ativo, uma consulta contendo o termo "on" será avaliada, retornando correspondências que de outra forma seriam ignoradas pelo filtro padrão.

## Aplicações Práticas

1. **Pesquisa de Documentos Corporativos** – Preserve a terminologia crítica que seria removida pelas listas padrão de palavras‑vazias.  
2. **Plataformas de E‑commerce** – Aumente a descoberta de produtos indexando cada palavra em descrições, números de modelo e especificações.  
3. **Ferramentas de Pesquisa Jurídica** – Capture cada termo legal, mesmo aqueles comumente tratados como palavras‑vazias, para evitar perder cláusulas cruciais.

## Considerações de Desempenho

- **Dicas de Otimização**: Atualize e faça a limpeza do seu índice regularmente para manter alta velocidade de pesquisa. O GroupDocs.Search pode lidar **com até 1 million documents** enquanto mantém tempos de consulta em subsegundos.  
- **Uso de Recursos**: Monitore o tamanho do heap da JVM; índices grandes podem exigir um heap máximo (`-Xmx`) de 4 GB ou mais.  
- **Gerenciamento de Memória Java**: Use opções de armazenamento off‑heap para corpora muito grandes a fim de manter a pegada on‑heap abaixo de 2 GB.

## Problemas Comuns e Soluções

| Sintoma | Causa Provável | Solução |
|---|---|---|
| Nenhum resultado para palavras comuns | `setUseStopWords(true)` (padrão) | Chame `setUseStopWords(false)` como mostrado acima. |
| Erros de falta de memória durante a indexação | Indexar muitos arquivos grandes de uma vez | Indexe arquivos em lotes; aumente a opção JVM `-Xmx`. |
| A pesquisa retorna dados desatualizados | Índice não atualizado após adicionar novos arquivos | Chame `index.update()` ou re‑adicione os documentos alterados. |

## Perguntas Frequentes

**Q: O que são palavras‑vazias?**  
A: Palavras‑vazias são termos comuns (por exemplo, “the”, “is”, “on”) que muitos mecanismos de busca ignoram para acelerar as consultas. Desativá‑las permite tratar cada token como pesquisável.

**Q: Por que desativar palavras‑vazias em índices de pesquisa?**  
A: Quando a correspondência exata de frases é necessária — como em documentos legais ou técnicos — cada palavra tem significado, portanto você precisa incluir palavras‑vazias.

**Q: Como o GroupDocs.Search lida com grandes conjuntos de dados?**  
A: A biblioteca usa estruturas de dados otimizadas e indexação incremental para manter o uso de memória baixo, mesmo com **millions of documents**.

**Q: Posso integrar o GroupDocs.Search com outras aplicações Java?**  
A: Sim, a API foi projetada para fácil incorporação em qualquer sistema baseado em Java, desde serviços web até aplicativos desktop.

**Q: O que devo fazer se meus resultados de pesquisa não forem precisos?**  
A: Verifique se o índice inclui todos os arquivos necessários (`add documents to index`), assegure que o filtro de palavras‑vazias está desativado quando necessário e considere reconstruir o índice após mudanças significativas.

## Recursos Adicionais

- **Documentação**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Referência da API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **Repositório GitHub**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Suporte Gratuito**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Licença Temporária**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Seguindo este guia, você agora sabe como **add documents to index** e **disable stop words java** para fornecer resultados de pesquisa mais precisos em suas aplicações Java.

---

**Última Atualização:** 2026-07-07  
**Testado com:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs  

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

## Tutoriais Relacionados

- [Processamento de Linguagem Java – Criar Dicionário de Sinônimos com GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Como adicionar documentos ao índice com Indexação de Metadados em Java usando GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Como Adicionar Documentos ao Índice com GroupDocs.Search para Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)