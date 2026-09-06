---
date: '2026-09-06'
description: Aprenda a filtrar extensões de arquivos java usando GroupDocs.Search
  para Java, abordando os operadores lógicos AND, OR, NOT, filtros de intervalo de
  datas e filtros de caminho.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: Filtre extensões de arquivos java usando GroupDocs.Search. Aprenda
  a combinar filtros de extensão, intervalo de datas e caminho com operadores lógicos
  em Java.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: Filtrar extensões de arquivos java com GroupDocs.Search – Guia Completo
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: Como filtrar extensões de arquivos java com GroupDocs.Search
type: docs
url: /pt/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Filtrar extensões de arquivo java com GroupDocs.Search

Neste tutorial abrangente, você aprenderá como **filtrar extensões de arquivo java** ao indexar documentos com GroupDocs.Search. Ao final do guia, você poderá incluir apenas os tipos de arquivo que precisa, excluir formatos indesejados e combinar essas regras com filtros de intervalo de datas e de caminho usando operadores lógicos AND, OR e NOT. Essa abordagem mantém seu índice enxuto, acelera as buscas e ajuda a manter a conformidade com as políticas de manipulação de dados.

## Respostas rápidas
- **O que é o filtro de extensão de arquivo java?** É uma regra que indica ao GroupDocs.Search quais extensões de arquivo incluir ou excluir durante a indexação.  
- **Qual biblioteca fornece esse recurso?** GroupDocs.Search for Java.  
- **Preciso de uma licença?** Um teste gratuito funciona para avaliação; uma licença completa é necessária para produção.  
- **Posso combinar filtros?** Sim – você pode encadear filtros de extensão, data, tamanho e caminho com lógica AND, OR, NOT.  
- **É compatível com Maven?** Absolutamente – adicione a dependência GroupDocs.Search ao seu `pom.xml`.

## O que é um filtro de extensão de arquivo java?
Um **filtro de extensão de arquivo java** é um conjunto de regras que avalia a extensão de cada arquivo antes de enviá-lo ao motor de indexação. Ao especificar extensões como `.txt`, `.pdf` ou `.epub`, você pode **incluir arquivos por extensão** ou **excluir arquivos por extensão** para manter seu índice focado e seus resultados de busca relevantes.

## Por que usar filtragem de extensão de arquivo com GroupDocs.Search?
A filtragem de extensão de arquivo melhora a eficiência da indexação ao excluir formatos irrelevantes, reduz os requisitos de armazenamento e ajuda a cumprir regras de conformidade ao impedir que conteúdo indesejado entre no índice. Também permite respostas de consulta mais rápidas porque o motor de busca processa um conjunto de dados menor e mais relevante.

- **Desempenho:** Pular arquivos indesejados reduz I/O e acelera a indexação em até 40 % em grandes repositórios.  
- **Economia de armazenamento:** Apenas documentos relevantes são armazenados no índice, reduzindo o uso de disco em média em 30 %.  
- **Conformidade:** Impede a indexação acidental de tipos de arquivo confidenciais ou não suportados.  
- **Flexibilidade:** Combine com recursos de **date range filter java** para direcionar arquivos criados ou modificados dentro de períodos específicos.

## Pré-requisitos

Antes de começarmos, certifique‑se de que você tem o seguinte:

### Bibliotecas e dependências necessárias
- **GroupDocs.Search for Java** – versão 25.4 ou posterior (suporta mais de 60 formatos de entrada).  
- **Java Development Kit (JDK)** – qualquer versão compatível (8 ou superior).

### Configuração do ambiente
- Ambiente de Desenvolvimento Integrado (IDE): IntelliJ IDEA, Eclipse ou qualquer IDE compatível com Maven.

### Pré-requisitos de conhecimento
- Programação Java básica.  
- Familiaridade com I/O de arquivos em Java.  
- Compreensão de expressões regulares e manipulação de data‑hora.

## Configurando GroupDocs.Search para Java
Para começar a usar o GroupDocs.Search, você precisa incluí‑lo como dependência em seu projeto.

### Configuração Maven
Adicione a seguinte configuração de repositório e dependência ao seu arquivo `pom.xml`:

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
Alternativamente, faça o download da versão mais recente diretamente de [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Aquisição de licença
1. **Teste gratuito** – explore os recursos sem custo.  
2. **Licença temporária** – obtenha funcionalidade completa por um período limitado.  
3. **Compra** – obtenha uma licença permanente para uso em produção.

### Inicialização e configuração básicas
Depois que a biblioteca for adicionada, inicialize seu ambiente de indexação. A classe `IndexSettings` contém todas as opções de configuração, incluindo filtros.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Guia de implementação
A seguir, mergulhamos em cada tipo de filtro, explicando **por que ele é importante** e fornecendo instruções passo a passo que você pode copiar para seu projeto.

### Filtragem por extensão de arquivo
Filtre arquivos por suas extensões durante a indexação. Isso é perfeito quando você deseja processar apenas e‑books (`.fb2`, `.epub`) e arquivos de texto simples (`.txt`).

#### Visão geral
`DocumentFilter.createFileExtension` cria uma lista branca de extensões.

#### Etapas de implementação
1. **Criar filtro** – defina as extensões que você deseja manter.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Inicializar índice e adicionar documentos** – aplique o filtro ao construir o `IndexSettings`.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtro lógico NOT
Exclua extensões específicas, como páginas da web e PDFs, quando não forem necessárias para seu cenário de busca.

#### Etapas de implementação
1. **Criar filtro de exclusão** – especifique as extensões a rejeitar.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Aplicar às configurações do índice** – combine o filtro NOT com outras regras.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Adicionar documentos** – apenas arquivos que passam pelo filtro combinado são indexados.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtro lógico AND
Combine várias condições — data de criação, extensão e tamanho do arquivo — de modo que **apenas arquivos que atendam a todos os critérios** sejam indexados.

#### Visão geral
`DocumentFilter.createAnd` mescla vários filtros em uma única regra.

#### Etapas de implementação
1. **Definir filtros** – crie filtros individuais para cada condição.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combinar filtros** – use o operador AND para exigir todas as condições.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Indexar documentos** – forneça o filtro combinado ao pipeline de indexação.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtro lógico OR
Inclua arquivos que satisfaçam **qualquer** das condições especificadas — útil quando você deseja capturar tanto pequenos arquivos de texto quanto arquivos não‑texto maiores.

#### Etapas de implementação
1. **Definir filtros** – crie filtros separados para cada condição alternativa.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combinar filtros com condições lógicas** – use o operador OR.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalizar filtro OR** – anexe o filtro combinado à configuração do índice.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtros de tempo de criação
Alveje arquivos criados dentro de um período específico — um cenário clássico de **date range filter java**.

#### Etapas de implementação
1. **Definir filtro de intervalo de datas** – especifique as datas de início e fim.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Indexar documentos** – somente arquivos cujos carimbos de criação estejam dentro do intervalo são indexados.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtros de tempo de modificação
Exclua arquivos que foram modificados após uma certa data de corte.

#### Etapas de implementação
1. **Definir filtro** – defina o carimbo de tempo máximo de modificação.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Indexar documentos** – arquivos mais recentes que o corte são ignorados.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtragem por caminho de arquivo
Restrinja a indexação a arquivos localizados em pastas específicas ou que correspondam a um padrão — ideal para **include files by extension** dentro de uma hierarquia de diretórios específica.

#### Etapas de implementação
1. **Definir filtro de caminho de arquivo** – use padrões glob ou regex para combinar diretórios.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Inicializar índice e adicionar documentos** – aplique o filtro de caminho juntamente com outras regras.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Armadilhas comuns e dicas
- **Nunca misture caminhos absolutos e relativos** na mesma configuração de filtro – isso pode levar a exclusões inesperadas.  
- **Redefina o `IndexSettings`** ao trocar conjuntos de filtros; caso contrário, filtros anteriores podem persistir.  
- **Combine um limite superior de comprimento com um filtro de extensão** para grandes coleções, a fim de manter o uso de memória baixo.  
- LoggingOptions controla a configuração de registro para GroupDocs.Search.  
- **Habilite o registro** (`LoggingOptions.setEnabled(true)`) para ver por que um arquivo foi rejeitado.  

## Perguntas frequentes

**Q: Posso alterar os critérios do filtro após o índice ser criado?**  
A: Sim. Reconstrua o índice com um novo `DocumentFilter` ou use indexação incremental com configurações atualizadas.

**Q: O filtro de extensão de arquivo java funciona em arquivos compactados (por exemplo, ZIP)?**  
A: O GroupDocs.Search pode indexar formatos de arquivo suportados, mas o filtro de extensão se aplica ao próprio arquivo compactado, não aos arquivos internos. Use filtros aninhados para controle mais aprofundado.

**Q: Como faço para depurar por que um arquivo específico foi excluído?**  
A: Habilite o registro da biblioteca (`LoggingOptions.setEnabled(true)`) e inspecione o log – ele relata qual filtro rejeitou cada arquivo.

**Q: É possível combinar o filtro de extensão de arquivo java com filtros regex personalizados?**  
A: Absolutamente. Envolva um filtro regex dentro de `DocumentFilter.createAnd()` juntamente com o filtro de extensão.

**Q: Qual o impacto de desempenho ao adicionar muitos filtros?**  
A: Cada filtro adiciona uma sobrecarga modesta durante a indexação, mas a redução de dados indexados geralmente supera o custo. Teste com uma amostra representativa para encontrar o equilíbrio ideal.

---

**Última atualização:** 2026-09-06  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Tutoriais relacionados

- [Formato de Data Personalizado Java | Busca por Intervalo de Datas com GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: Domine Buscas Booleanas com GroupDocs.Search para Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Otimize o Desempenho de Busca com Técnicas Avançadas de Indexação no GroupDocs.Search para Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}