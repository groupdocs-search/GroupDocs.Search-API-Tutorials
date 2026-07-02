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

# Pare palavras na pesquisa: adicione documentos ao índice com GroupDocs.Search Java

Se você precisa **adicionar documentos ao índice** garantindo que nenhum termo importante—especialmente os mais comuns—seja ignorado, não está no lugar certo. Neste guia mostraremos como **desativar palavras de parada na pesquisa** usando o GroupDocs.Search para Java, de modo que cada token (mesmo “on”, “by” ou “the”) se torna pesquisável e seus resultados são muito mais precisos.

## Respostas rápidas
- **O que significa “adicionar documentos ao índice”?** Significa carregar seus arquivos de origem em um índice pesquisável para que possam ser consultados de forma eficiente.
- **Por que eu desativaria stopwords?** Para incluir palavras comuns (ex.: “on”, “the”) nas pesquisas quando esses termos são relevantes para o seu domínio.
- **Qual versão da biblioteca é necessária?** GroupDocs.Search for Java25.4 ou posterior.
- **Preciso de licença?** Um teste gratuito funciona para avaliação; uma licença permanente é necessária para produção.
- **Posso usar isso em um projeto Maven?** Sim – basta adicionar o repositório e a dependência mostrada abaixo.

## O que são palavras irrelevantes na pesquisa e por que você pode querer desativá-las?
Palavras de parada são termos frequentes que muitos mecanismos de busca filtram automaticamente para acelerar as consultas. Embora isso seja melhor o desempenho em buscas genéricas na web, pode prejudicar a precisão em domínios especializados—contratos legais, catálogos de e-commerce ou manuais técnicos—onde palavras como “on”, “by” ou “as” carregam significado real. Desativar palavras irrelevantes permite tratar cada palavra como significativa, garantindo que nenhum documento relevante seja perdido.

## Como funciona a adição de documentos ao índice no GroupDocs.Search?
Ao adicionar documentos, a biblioteca lê cada arquivo, tokeniza seu conteúdo e armazena os tokens em uma estrutura de dados otimizada (o índice). Uma vez indexado, o motor pode recuperar documentos correspondentes em milissegundos, mesmo para grandes coleções.

## Pré-requisitos

- **Bibliotecas Necessárias**: GroupDocs.Search for Java25.4 (ou mais recente).
- **Ambiente de Desenvolvimento**: IntelliJ IDEA, Eclipse ou qualquer IDE Java de sua preferência.
- **Conhecimento Básico**: Familiaridade com a sintaxe Java e o conceito de indexação.

## Configurando GroupDocs.Search para Java

### Instalação do Maven

Se você usa Maven, incluindo o seguinte em seu `pom.xml`:

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

Alternativamente, faça o download da versão mais recente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Etapas de aquisição de licença
- **Teste Gratuito** – comece a testar imediatamente.
- **Licença Temporária** – Obtenha uma chave temporária para funcionalidade completa.
- **Compra** – adquire uma licença permanente para uso em produção.

## Inicialização e configuração básicas

Crie uma instância de `IndexSettings` para controlar o comportamento do índice:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Como desativar palavras irrelevantes na pesquisa (Java)

A linha a seguir desativa o filtro interno de palavras irrelevantes:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Parâmetros*: `setUseStopWords` aceita um boolean.
*Objetivo*: Garantir que cada palavra—incluindo stopwords comuns—seja indexada e pesquisável.

## Como adicionar documentos ao índice

### Definindo o diretório de saída

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Especificando o diretório do documento

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Agora cada arquivo em `YOUR_DOCUMENT_DIRECTORY` é **added documents to index** e está pronto para consultas.

## Executando uma consulta de pesquisa

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Como as stop words estão desativadas, o termo `"on"` será considerado durante a pesquisa, retornando correspondências que de outra forma seriam ignoradas.

## Aplicações Práticas

1. **Enterprise Document Search** – Garanta que a terminologia crítica não seja filtrada.
2. **Plataformas de comércio eletrônico** – Melhore a descoberta de produtos indexando cada palavra nas seguranças.
3. **Ferramentas de pesquisa jurídica** – Capture todos os termos jurídicos, mesmo aqueles normalmente tratados como palavras irrelevantes.

## Considerações de desempenho

- **Dicas de otimização**: Atualize e faça a limpeza do índice regularmente para manter alta velocidade de busca.
- **Uso de Recursos**: Monitora o tamanho do heap da JVM; índices grandes podem exigir ajustes nas configurações de coleta de lixo.
- **Gerenciamento de memória Java**: use estruturas de dados eficientes e considere o armazenamento fora do heap para corpos muito grandes.

## Problemas e soluções comuns

| Sintoma | Causa provável | Correção |
|---|---|---|
| Nenhum resultado para palavras comuns | `setUseStopWords(true)` (padrão) | Chame `setUseStopWords(false)` como mostrado acima. |
| Erros de falta de memória durante a indexação | Indexação de muitos arquivos grandes simultaneamente | Indexe os arquivos em lotes; aumente a opção `-Xmx` da JVM. |
| A pesquisa retorna dados desatualizados | Índice não atualizado após a adição de novos arquivos | Chame `index.update()` ou adicione novamente os documentos alterados. |

## Perguntas Frequentes

**P: O que são stopwords?**
R: Stopwords são termos comuns (por exemplo, “o”, “é”, “em”) que muitos mecanismos de busca ignoram para acelerar as consultas. Desativá-las permite que você trate cada token como pesquisável.

**P: Por que desativar stopwords nos índices de pesquisa?**
R: Quando a correspondência exata de frases é necessária — como em documentos jurídicos ou técnicos — cada palavra tem significado, portanto, você precisa incluir stopwords. **P: Como o GroupDocs.Search lida com grandes conjuntos de dados?**

R: A biblioteca utiliza estruturas de dados otimizadas e indexação incremental para manter o uso de memória baixo, mesmo com milhões de documentos.

**P: Posso integrar o GroupDocs.Search com outros aplicativos Java?**
R: Sim, a API foi projetada para fácil incorporação em qualquer sistema baseado em Java, desde serviços web até aplicativos desktop.

**P: O que devo fazer se meus resultados de pesquisa não forem precisos?**
R: Verifique se o índice inclui todos os documentos necessários (`adicione documentos ao índice`), certifique-se de que a filtragem de palavras irrelevantes esteja desativada, se necessário, e considere reconstruir o índice após alterações significativas.

**P: O que devo fazer se meus resultados de pesquisa não forem precisos?**
R: Verifique se o índice inclui todos os documentos necessários (`adicione documentos ao índice`), certifique-se de que a filtragem de palavras irrelevantes esteja desativada, se necessário, e considere reconstruir o índice após alterações importantes. ## Recursos Adicionais

- **Documentação**: [Documentação da Pesquisa do GroupDocs](https://docs.groupdocs.com/search/java/)
- **Referência da API**: [Referência da API do GroupDocs](https://reference.groupdocs.com/search/java)
- **Download**: [Obtenha a versão mais recente do GroupDocs.Search para Java](https://releases.groupdocs.com/search/java/)
- **Repositório do GitHub**: [Explore no GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Suporte Gratuito**: [Participe do Fórum do GroupDocs](https://forum.groupdocs.com/c/search/10)
- **Licença Temporária**: [Solicite uma Licença Temporária](https://purchase.groupdocs.com/temporary-license/)

Seguindo este guia, você agora sabe como **adicionar documentos ao índice** e **desativar palavras de parada na pesquisa** para oferecer resultados mais precisos em suas aplicações Java.

---

**Última atualização:** 19/02/2026
**Testado com:** GroupDocs.Search for Java25.4
**Autor:** GroupDocs