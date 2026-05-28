---
date: '2026-05-28'
description: Aprenda como pesquisar frase com padrões de wildcard usando o GroupDocs.Search
  for Java. Inclui a criação de um search index, a adição de documents e a execução
  de consultas de exact phrase e wildcard queries.
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: Como pesquisar frase com wildcards no GroupDocs.Search for Java
type: docs
url: /pt/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Como pesquisar frase com curingas no GroupDocs.Search para Java

Em aplicações modernas centradas em documentos, **how to search phrase** rapidamente e com precisão é um fator decisivo para a experiência do usuário. Seja construindo uma base de conhecimento, um catálogo de e‑commerce ou um repositório orientado por conformidade, a capacidade de localizar uma frase exata — ou uma variação flexível dela — mantém os usuários produtivos e reduz a sobrecarga de suporte. Este tutorial orienta você na instalação do **GroupDocs.Search para Java**, na criação de um índice de pesquisa, no carregamento de documentos e na execução de consultas de frase exata e aprimoradas com curingas, tudo com trechos de código claros e prontos para produção.

## Respostas rápidas
- **What is the primary benefit of phrase searches?** Correspondência precisa da ordem e proximidade das palavras, garantindo que apenas documentos contendo a sequência exata sejam retornados.  
- **Can wildcards be used inside a phrase?** Sim — curingas permitem pular ou substituir palavras mantendo a ordem geral.  
- **Do I need a license for development?** Um teste gratuito funciona para testes; uma licença completa é necessária para implantações em produção.  
- **Which Maven version should I use?** A versão mais recente do GroupDocs.Search para Java (por exemplo, 25.4 no momento da escrita).  
- **Is this approach suitable for large document sets?** Absolutamente — o GroupDocs.Search pode lidar com coleções de centenas de milhares de documentos com latência de consulta subsegundo quando o índice está otimizado.

## O que é “how to search phrase”?
**Pesquisar uma frase significa procurar uma sequência específica de palavras em um documento.**  
Ao executar uma consulta de frase, o mecanismo verifica se as palavras aparecem na ordem exata e dentro da proximidade definida, eliminando resultados irrelevantes que contenham as mesmas palavras em um contexto diferente. Isso torna as buscas por frase ideais para localizar cláusulas legais, códigos de produto ou qualquer texto onde a ordem importa.

## Por que usar o GroupDocs.Search para consultas de frase e curinga?
O GroupDocs.Search oferece **indexação de alta taxa de transferência de até 1 milhão de documentos, mantendo tempos de resposta de consulta subsegundo** em hardware de servidor típico. Sua linguagem de consulta suporta frases exatas, curingas simples `*` e `?`, e padrões avançados como intervalos numéricos (`*2~5`). A biblioteca integra-se a qualquer aplicação Java via Maven ou download direto de JAR, e funciona em Java 8+ sem serviços externos.

## Pré-requisitos
- Java 8 ou mais recente (Java 11 LTS recomendado).  
- Maven 3 ou posterior (se preferir gerenciamento de dependências).  
- Familiaridade básica com a estrutura de projetos Java e conceitos orientados a objetos.  

## Configurando o GroupDocs.Search para Java

### Usando Maven
Adicione o repositório oficial e a dependência do GroupDocs.Search ao seu `pom.xml`:

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### Download direto
Alternativamente, faça o download do JAR mais recente na página oficial de lançamentos: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Aquisição de licença
- **Free Trial:** Ideal para experimentos rápidos; limitado a 100 MB de dados indexados.  
- **Temporary License:** Solicite uma chave de avaliação de 30 dias no portal GroupDocs.  
- **Full License:** Necessária para uso em produção e capacidade de indexação ilimitada.

## Inicialização e configuração básicas
Crie uma pasta que armazenará os arquivos de índice e instancie o objeto `Index`. A classe `Index` representa o índice pesquisável armazenado em disco e fornece métodos para adicionar, atualizar e consultar documentos.

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

Adicione os documentos que você deseja tornar pesquisáveis:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## Como pesquisar frase com curingas no GroupDocs.Search
Esta seção demonstra três níveis de busca por frase — correspondência exata, curinga simples e padrões avançados de curinga — mostrando como criar um índice, adicionar documentos e executar cada tipo de consulta com código Java conciso. Os exemplos ilustram consultas baseadas em texto e construção de consultas baseadas em objetos, permitindo que desenvolvedores integrem recursos de busca flexíveis em suas aplicações.

### Busca de frase simples

#### Visão geral
Use esta abordagem quando precisar de uma **correspondência exata** de uma sequência de palavras, como uma cláusula legal ou um número de modelo de produto.

#### Resposta direta
Carregue o índice, chame `search` com uma frase entre aspas (por exemplo, `"quick brown fox"`), e o mecanismo retorna apenas documentos contendo essa sequência exata, preservando a ordem e o espaçamento das palavras. A consulta é executada em milissegundos, mesmo em índices contendo centenas de milhares de arquivos.

#### Etapa 1: Criar um índice
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### Etapa 2: Adicionar documentos ao índice
```java
Index index = new Index(indexFolder);
```

#### Etapa 3: Pesquisar uma frase específica (forma de texto)
```java
index.add(documentsFolder);
```

#### Etapa 4: Consultas baseadas em objeto (pesquisar frase exata)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### Busca de frase com curingas

#### Visão geral
Marcadores curinga (`*` para qualquer número de caracteres, `?` para um único caractere) permitem que você **pule palavras variáveis** enquanto ainda impõe a ordem ao redor.

#### Resposta direta
Insira um token curinga (`*`) dentro de uma frase entre aspas — por exemplo, `"quick * fox"` — para corresponder a qualquer palavra(s) entre *quick* e *fox*. O mecanismo expande o curinga no momento da consulta, analisando apenas os termos indexados que satisfazem o padrão, o que mantém o desempenho comparável a uma consulta de frase simples.

#### Etapa 1: Criar um índice
*(Mesmo que a Busca de frase simples.)*

#### Etapa 2: Adicionar documentos ao índice
*(Mesmo que acima.)*

#### Etapa 3: Busca em forma de texto com curingas
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Etapa 4: Consultas baseadas em objeto com curingas (Wildcard Search Java)
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### Busca avançada com curingas

#### Visão geral
Combine intervalos numéricos, caracteres opcionais e padrões personalizados semelhantes a regex para **correspondência sofisticada**, como números de versão ou códigos de produto.

#### Resposta direta
Use a sintaxe de curinga estendida `*min~max` para definir um intervalo de distâncias de palavras permitidas, ou `?` para corresponder a um único caractere. Por exemplo, `"error *2~5 code"` encontra a palavra *error* seguida por duas a cinco palavras e então *code*. Essa precisão reduz falsos positivos enquanto ainda oferece flexibilidade.

#### Etapa 1: Criar um índice
*(Repetido para clareza.)*

#### Etapa 2: Adicionar documentos ao índice
*(Repetido.)*

#### Etapa 3: Busca em forma de texto com padrões complexos de curinga
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Etapa 4: Consultas baseadas em objeto com curingas avançados
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## Aplicações práticas
- **Content Management Systems:** Editores podem localizar cláusulas exatas ou trechos flexíveis sem precisar escanear manualmente centenas de páginas.  
- **E‑commerce Catalogs:** Compradores encontram produtos mesmo quando omitem um descritor ou usam sinônimos, graças à tolerância de curingas.  
- **Legal & Compliance:** Isole rapidamente a linguagem contratual que pode aparecer com pequenas variações em diferentes acordos.  

## Considerações de desempenho
- **Create Search Index** apenas uma vez por conjunto de documentos estável; reutilize a mesma instância `Index` para todas as consultas.  
- **Add Documents Incrementally** quando novos arquivos chegarem — evite reconstruir todo o índice para manter o uso de CPU baixo.  
- **Design Precise Wildcard Patterns**; padrões mais amplos (`*`) aumentam o número de expansões de termos e podem elevar a carga de CPU.  
- **Call `index.optimize()`** periodicamente (se suportado) para compactar o índice e manter o consumo de memória sob controle.  

## Problemas comuns e soluções

| Problema | Solução |
|----------|----------|
| Nenhum resultado retornado para uma consulta com curinga | Verifique a sintaxe do curinga (`*min~max`) e assegure que as palavras-alvo existam dentro da distância definida. |
| O índice fica desatualizado após atualizações de arquivos | Use `index.add(updatedFolder)` ou a API de atualização incremental para atualizar apenas os arquivos alterados. |
| Alto consumo de memória em grandes conjuntos de dados | Aumente o heap da JVM (`-Xmx4g` ou superior) e considere dividir o índice em múltiplos shards para processamento paralelo. |

## Perguntas frequentes

**Q: Qual é a diferença entre um curinga e uma busca por frase?**  
A: Uma busca por frase requer a ordem exata das palavras e o espaçamento, enquanto um curinga permite substituir ou pular palavras dentro dessa ordem, oferecendo correspondência flexível.

**Q: Posso usar curingas com dados numéricos nas buscas?**  
A: Sim — os parâmetros de intervalo de curinga (`*min~max`) funcionam com números assim como com palavras, permitindo consultas como `"version *1~3"`.

**Q: Como devo lidar com coleções de documentos muito grandes?**  
A: Mantenha o índice otimizado, execute atualizações incrementais e crie padrões de curinga específicos para limitar a expansão de termos. O GroupDocs.Search pode indexar 1 milhão de documentos mantendo a latência de consulta abaixo de 200 ms em hardware padrão.

**Q: O GroupDocs.Search é adequado para cenários de busca em tempo real?**  
A: Absolutamente — uma vez que o índice está construído, as consultas são executadas em milissegundos, tornando-o ideal para caixas de busca interativas e recursos de auto‑complete.

**Q: Posso integrar esta biblioteca em um projeto Java existente?**  
A: Sim. Adicione a dependência Maven ou o JAR, instancie o `Index` conforme mostrado, e você estará pronto para consultar sem alterar o código existente.

---

**Última atualização:** 2026-05-28  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## Tutoriais relacionados

- [Criar índice de pesquisa Java – Tutoriais GroupDocs.Search](/search/java/)
- [Adicionar documentos ao índice – Tutoriais GroupDocs.Search Java](/search/java/document-management/)
- [Criar índice de pesquisa - Tutoriais GroupDocs.Search Java](/search/java/advanced-features/)