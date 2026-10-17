---
date: '2026-10-17'
description: Aprenda como usar sinônimos em Java com GroupDocs.Search, importe dicionários
  de sinônimos, gerencie grupos de sinônimos e otimize seu índice de pesquisa para
  melhor relevância.
keywords:
- how to use synonyms
- add synonym support
- manage synonym groups
- import synonym dictionary
- optimize search index
lastmod: '2026-10-17'
og_description: Aprenda como usar sinônimos em Java com GroupDocs.Search, importe
  dicionários de sinônimos, gerencie grupos de sinônimos e otimize seu índice de pesquisa
  para melhor relevância.
og_image_alt: Developer guide showing synonym dictionary integration in GroupDocs.Search
  for Java
og_title: Como usar sinônimos em Java com GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-10-17'
  description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  headline: How to use synonyms in Java with GroupDocs.Search
  type: TechArticle
- description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  name: How to use synonyms in Java with GroupDocs.Search
  steps:
  - name: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
    text: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
  - name: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
    text: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
  - name: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
    text: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
  type: HowTo
- questions:
  - answer: Any modern OS with a compatible JDK (Java 8 or newer) is sufficient.
    question: What is the minimum system requirement for using GroupDocs.Search?
  - answer: Update it whenever new terminology emerges—use `clear()` followed by `addRange()`
      for a clean refresh.
    question: How often should I refresh my synonym dictionary?
  - answer: A free trial works for evaluation, but a license is required for production
      deployments.
    question: Can I run GroupDocs.Search without purchasing a license?
  - answer: Split data into logical batches, monitor heap usage, and schedule regular
      index maintenance.
    question: What are best practices for indexing large data sets?
  - answer: Verify that the dictionary is correctly imported, that `setUseSynonymSearch(true)`
      is active, and that the terms are present in the synonym groups.
    question: I’m not seeing expected synonym matches—what should I check?
  type: FAQPage
tags:
- synonym search
- GroupDocs.Search
- Java search indexing
- document retrieval
title: Como usar sinônimos em Java com GroupDocs.Search
type: docs
url: /pt/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar sinônimos em Java com GroupDocs.Search

Se você deseja que seus usuários encontrem o conteúdo correto mesmo quando digitam palavras diferentes, **pesquisa com sinônimos** é a solução. Neste guia você aprenderá a criar um dicionário de sinônimos, importá‑lo ou exportá‑lo, gerenciar grupos de sinônimos e executar uma pesquisa que expande automaticamente as consultas usando esses sinônimos. Seja construindo um CMS, um catálogo de e‑commerce ou um repositório de documentos legais, adicionar suporte a sinônimos pode aumentar drasticamente a relevância e as taxas de conversão.

## Respostas rápidas
- **Qual é o primeiro passo para adicionar sinônimos?** Crie uma instância de `Index` e trabalhe com a API `SynonymDictionary`.  
- **Posso importar um dicionário de sinônimos pronto?** Sim – chame `importDictionary(path)` com a localização do arquivo.  
- **Como habilitar a pesquisa sensível a sinônimos?** Ative `SearchOptions.setUseSynonymSearch(true)`.  
- **É possível editar grupos de sinônimos em tempo de execução?** Absolutamente – você pode limpar, adicionar ou recuperar grupos via a API do dicionário.  
- **O que devo monitorar ao dimensionar o índice?** Faça a limpeza regular de entradas não usadas e ajuste o heap da JVM para arquivos de sinônimos grandes.

## O que é pesquisa com sinônimos?
**Pesquisa com sinônimos** significa que o mecanismo trata um conjunto de palavras ou frases como intercambiáveis. Quando um usuário digita **“better”**, o mecanismo também procura por **“improve”**, **“enhance”**, ou qualquer outro termo que você definiu no mesmo grupo de sinônimos, entregando resultados mais ricos sem alterar a consulta do usuário.

## Por que habilitar suporte a sinônimos no GroupDocs.Search?
Habilitar suporte a sinônimos permite que o mecanismo amplie automaticamente as consultas para incluir termos equivalentes, o que melhora a relevância dos resultados, aumenta a satisfação do usuário e pode elevar as taxas de conversão para sites de e‑commerce ou orientados a conteúdo. Também centraliza a gestão de terminologia, reduzindo a sobrecarga de manutenção em múltiplas aplicações.

## Pré‑requisitos
- GroupDocs.Search para Java versão **25.4** ou mais recente.  
- Uma IDE Java (IntelliJ IDEA, Eclipse, etc.) com suporte a Maven.  
- Conhecimento básico de Java e familiaridade com a estrutura de projetos Maven.

### Bibliotecas necessárias e versões
- GroupDocs.Search para Java **25.4** ou superior.

### Configuração do ambiente
- IDE de sua escolha (IntelliJ IDEA, Eclipse, etc.).  
- Maven para gerenciamento de dependências.

### Requisitos de conhecimento
- Programação orientada a objetos em Java.  
- Operações básicas de I/O de arquivos.

## Configurando o GroupDocs.Search para Java

### Informações de instalação
Adicione o repositório e a dependência ao seu `pom.xml`:

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

**Download direto** – você também pode baixar o JAR mais recente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Aquisição de licença
- **Teste gratuito:** Teste os recursos principais sem licença.  
- **Licença temporária:** Amplie as capacidades do teste durante a avaliação.  
- **Compra:** Necessária para uso em produção e o conjunto completo de recursos.

#### Inicialização e configuração básicas
Crie uma instância de `Index` e, em seguida, adicione documentos para serem pesquisáveis:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Index";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Adding documents from a specific folder to the index
index.add(documentsFolder);
```

## Como adicionar sinônimos ao seu índice de pesquisa

### Recurso 1: criar e indexar um índice
A classe `Index` representa uma coleção pesquisável de documentos armazenados em disco ou na memória.  

```java
// Create an index in the specified folder
Index index = new Index(indexFolder);

// Add documents from the given folder to the index
index.add(documentsFolder);
```

### Recurso 2: recuperar sinônimos para uma palavra
`SynonymDictionary` gerencia grupos de sinônimos e fornece métodos para consultar sinônimos de um termo.  

```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### Recurso 3: recuperar grupos de sinônimos
`SynonymDictionary.getGroups()` retorna uma lista de todos os grupos de sinônimos definidos com seus identificadores.  

```java
String[][] synonymGroups = index.getDictionaries().getSynonymDictionary().getSynonymGroups("make");
```

### Recurso 4: gerenciar entradas do dicionário de sinônimos
`add(word, synonym)` insere uma nova relação de sinônimo no dicionário. `clear()` remove todas as entradas, e `remove(word)` exclui um termo específico do dicionário.  

```java
if (index.getDictionaries().getSynonymDictionary().getCount() > 0) {
    index.getDictionaries().getSynonymDictionary().clear();
}

String[][] newSynonymGroups = new String[][]{
    new String[] { "achieve", "accomplish", "attain", "reach" },
    new String[] { "accept", "take", "have" },
    new String[] { "improve", "better" }
};

index.getDictionaries().getSynonymDictionary().addRange(newSynonymGroups);
```

### Recurso 5: exportar sinônimos para um arquivo
`exportDictionary(path)` grava o dicionário de sinônimos atual em um arquivo binário .dat no local especificado.  

```java
String exportFilePath = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.getDictionaries().getSynonymDictionary().exportDictionary(exportFilePath);
```

### Recurso 6: importar sinônimos de um arquivo
`importDictionary(path)` carrega um arquivo .dat previamente exportado para o dicionário de sinônimos.  

```java
index.getDictionaries().getSynonymDictionary().importDictionary(exportFilePath);
```

### Recurso 7: executar pesquisa com suporte a sinônimos
`SearchOptions` configura o comportamento da consulta, incluindo se a expansão por sinônimos está habilitada. `setUseSynonymSearch(true)` ativa a pesquisa sensível a sinônimos para a consulta subsequente.  

```java
String query = "better";
SearchOptions options = new SearchOptions();
options.setUseSynonymSearch(true);

SearchResult result = index.search(query, options);
```

## Como pesquisar com sinônimos
Carregue seu `Index`, habilite a pesquisa por sinônimos e execute uma consulta. O mecanismo expande automaticamente a consulta usando o dicionário de sinônimos que você criou ou importou, retornando correspondências para todos os termos relacionados.

## Como importar dicionário de sinônimos
Se você já possui um arquivo `.dat` preparado por outro ambiente, basta chamar `importDictionary(path)`. Isso é ideal para sincronizar dicionários entre servidores de desenvolvimento, teste e produção.

## Como gerenciar grupos de sinônimos
Grupos de sinônimos permitem tratar um conjunto de termos como uma única entidade lógica. Adicionar, limpar ou recuperar grupos é feito através da API `SynonymDictionary`, conforme demonstrado nos trechos de código acima.

## Como otimizar o índice de pesquisa
- **Limpar regularmente entradas não usadas:** Use `clear()` antes de atualizações em massa.  
- **Ajustar heap da JVM:** Dicionários grandes podem exigir mais memória; aumente o parâmetro `-Xmx` conforme necessário.  
- **Manter a biblioteca atualizada:** Novas versões contêm melhorias de desempenho e correções de bugs.

## Aplicações práticas
1. **Sistemas de gerenciamento de conteúdo (CMS):** Usuários encontram artigos mesmo usando terminologia alternativa.  
2. **Plataformas de e‑commerce:** Pesquisas de produtos tornam‑se tolerantes a sinônimos como “laptop” vs. “notebook”.  
3. **Repositórios de documentos:** Arquivos legais ou médicos se beneficiam de grupos de sinônimos específicos do domínio, melhorando a descoberta para profissionais.

## Considerações de desempenho
- **Otimizar armazenamento do índice:** Recompile periodicamente o índice para remover dados obsoletos.  
- **Gerenciar uso de memória:** Monitore o consumo de heap ao carregar arquivos de sinônimos grandes; um dicionário de 500 MB tipicamente requer um heap de 2 GB em uma JVM de 64 bits.  
- **Atualizações regulares:** Mantenha-se na versão mais recente do GroupDocs.Search para correções e ganhos de velocidade.

## Problemas comuns e soluções
| Problema | Causa provável | Correção |
|----------|----------------|----------|
| Nenhum resultado de sinônimo aparece | `setUseSynonymSearch(true)` não está definido ou o dicionário não foi importado | Verifique se a opção está habilitada e se o arquivo de dicionário existe. |
| Erros de falta de memória durante a importação | Arquivo `.dat` muito grande excede o heap da JVM | Aumente o tamanho do heap `-Xmx` ou importe em lotes menores. |
| Entradas duplicadas nos resultados | O mesmo termo aparece em vários grupos de sinônimos | Consolide grupos sobrepostos usando `clear()` e depois `addRange()`. |

## Perguntas frequentes

**Q: Qual é o requisito mínimo de sistema para usar o GroupDocs.Search?**  
A: Qualquer sistema operacional moderno com JDK compatível (Java 8 ou superior) é suficiente.

**Q: Com que frequência devo atualizar meu dicionário de sinônimos?**  
A: Atualize sempre que nova terminologia surgir — use `clear()` seguido de `addRange()` para uma atualização limpa.

**Q: Posso usar o GroupDocs.Search sem comprar uma licença?**  
A: Um teste gratuito funciona para avaliação, mas uma licença é necessária para implantações em produção.

**Q: Quais são as melhores práticas para indexar grandes conjuntos de dados?**  
A: Divida os dados em lotes lógicos, monitore o uso de heap e agende manutenção regular do índice.

**Q: Não estou vendo os resultados de sinônimos esperados — o que devo verificar?**  
A: Verifique se o dicionário foi importado corretamente, se `setUseSynonymSearch(true)` está ativo e se os termos estão presentes nos grupos de sinônimos.

**Recursos**  
- [Documentation](https://docs.groupdocs.com/search/java/)  
- [API Reference](https://reference.groupdocs.com/search/java)  
- [Download GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)  
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license/) 

---

**Última atualização:** 2026-10-17  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [Criar e Gerenciar Índice GroupDocs Search Java](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Biblioteca Java de Busca Full Text – Otimizar Índice com GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Busca Fuzzy em Java: Adicionar Documentos ao Índice com GroupDocs.Search](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}