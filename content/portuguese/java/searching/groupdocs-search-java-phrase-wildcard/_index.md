---
date: '2026-01-26'
description: Aprenda como pesquisar frases usando padrões curinga no GroupDocs.Search
  para Java. Este guia aborda a criação de um índice de pesquisa, a adição de documentos
  ao índice e a execução de pesquisa com curinga em Java.
keywords:
- GroupDocs.Search for Java
- phrase searches
- wildcard patterns
title: Como pesquisar frase com curingas no GroupDocs.Search Java
type: docs
url: /pt/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Como Pesquisar Frases com Curingas no GroupDocs.Search para Java

No mundo acelerado de gerenciamento de documentos de hoje, **how to search phrase** de forma eficiente pode fazer ou quebrar a usabilidade de uma aplicação. Seja você construindo um sistema de gerenciamento de conteúdo, um catálogo de e‑commerce ou um repositório de documentos legais, ser capaz de localizar frases exatas — ou variações flexíveis delas — é importante. Neste tutorial vamos percorrer a configuração do **GroupDocs.Search for Java**, a criação de um índice de pesquisa, a adição de documentos ao índice e o domínio tanto de buscas simples de frases quanto de poderosas técnicas de busca com curingas em Java.

## Respostas Rápidas
- **Qual é o principal benefício das buscas por frase?** Correspondência precisa da ordem das palavras e proximidade.  
- **É possível usar curingas dentro de uma frase?** Sim, você pode combinar curingas com palavras exatas para correspondência flexível.  
- **Preciso de uma licença para desenvolvimento?** Um teste gratuito funciona para testes; uma licença completa é necessária para produção.  
- **Qual versão do Maven devo usar?** A versão mais recente do GroupDocs.Search for Java (por exemplo, 25.4 no momento da escrita).  
- **Esta abordagem é adequada para grandes conjuntos de documentos?** Absolutamente — basta manter o índice otimizado e usar padrões de curinga direcionados.

## O que é “how to search phrase”?
Pesquisar uma frase significa procurar uma sequência específica de palavras em um documento. Quando você adiciona curingas, permite que o motor de busca pule ou substitua palavras, oferecendo flexibilidade para corresponder a variações sem sacrificar a relevância.

## Por que Usar o GroupDocs.Search para Consultas de Frases e Curingas?
- **Alto desempenho** em grandes coleções graças a um índice invertido otimizado.  
- **Linguagem de consulta rica** que suporta frase exata, curingas simples e padrões avançados.  
- **Integração fácil** com qualquer aplicação baseada em Java via Maven ou download direto.  

## Pré-requisitos
- Java 8 ou superior instalado.  
- Maven 3 ou posterior (se preferir gerenciamento de dependências via Maven).  
- Familiaridade básica com a sintaxe Java e estrutura de projetos.  

## Configurando o GroupDocs.Search para Java

### Using Maven
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

### Direct Download
Alternativamente, faça o download do JAR mais recente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
- **Teste Gratuito:** Ideal para experimentos rápidos.  
- **Licença Temporária:** Solicite via portal do GroupDocs para testes estendidos.  
- **Compra Completa:** Recomendada para implantações em produção.

### Basic Initialization and Setup
Crie uma pasta para o índice e inicialize-a:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

Adicione os documentos que você deseja tornar pesquisáveis:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

## Como Pesquisar Frases com Curingas no GroupDocs.Search
A seguir, detalhamos três cenários progressivos: busca de frase exata, uso simples de curingas e padrões avançados de curinga.

### Busca de Frase Simples

#### Overview
Use isto quando precisar de uma correspondência exata de uma sequência de palavras.

##### Step 1: Create an Index
```java
Index index = new Index(indexFolder);
```

##### Step 2: Add Documents to Index
```java
index.add(documentsFolder);
```

##### Step 3: Search for a Specific Phrase (Text Form)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Step 4: Object‑Based Queries (Search Exact Phrase)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Busca de Frase com Curingas

#### Overview
Os marcadores de curinga permitem pular um número variável de palavras entre termos exatos.

##### Step 1: Create an Index
* (Mesmo que os passos da Busca de Frase Simples.)*

##### Step 2: Add Documents to Index
* (Mesmo que acima.)*

##### Step 3: Text Form Search with Wildcards
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Step 4: Object‑Based Queries with Wildcards (Wildcard Search Java)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Busca Avançada com Curingas

#### Overview
Combine intervalos numéricos, caracteres opcionais e padrões personalizados para correspondência sofisticada.

##### Step 1: Create an Index
* (Repetido para clareza.)*

##### Step 2: Add Documents to Index
* (Repetido.)*

##### Step 3: Text Form Search with Complex Wildcard Patterns
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

##### Step 4: Object‑Based Queries with Advanced Wildcards
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

## Aplicações Práticas
- **Sistemas de Gerenciamento de Conteúdo:** Permitem que editores localizem cláusulas exatas ou trechos flexíveis.  
- **Catálogos de E‑commerce:** Permitem que compradores encontrem produtos mesmo que faltem palavras ou usem sinônimos.  
- **Legal & Compliance:** Isola rapidamente linguagem contratual que pode aparecer com pequenas variações.  

## Considerações de Desempenho
- **Create Search Index** apenas uma vez por conjunto de documentos, depois reutilize-o.  
- **Add Documents to Index** incrementalmente quando novos arquivos chegarem — não reconstrua todo o índice a cada vez.  
- Use **precise wildcard patterns** para evitar varreduras desnecessárias; padrões mais amplos aumentam a carga da CPU.  
- Periodicamente chame `index.optimize()` (se disponível) para manter o uso de memória baixo.

## Problemas Comuns & Soluções

| Problema | Solução |
|----------|---------|
| Nenhum resultado retornado para uma consulta com curinga | Verifique a sintaxe do curinga (`*min~~max`) e assegure que as palavras existam dentro da distância especificada. |
| O índice fica desatualizado após atualizações de arquivos | Execute novamente `index.add(updatedFolder)` ou use a API de atualização incremental. |
| Alto consumo de memória em grandes conjuntos de dados | Aumente o tamanho do heap da JVM e considere dividir o índice em múltiplas partições. |

## Perguntas Frequentes

**Q: Qual é a diferença entre um curinga e uma busca por frase?**  
A: Uma busca por frase procura uma ordem exata de palavras, enquanto um curinga permite substituir ou pular palavras dentro dessa ordem.

**Q: Posso usar curingas com dados numéricos nas buscas?**  
A: Sim, os parâmetros de intervalo de curinga funcionam com números assim como com palavras.

**Q: Como devo lidar com coleções de documentos muito grandes?**  
A: Mantenha o índice otimizado, use atualizações incrementais e projete seus padrões de curinga para serem o mais específicos possível.

**Q: O GroupDocs.Search é adequado para cenários de busca em tempo real?**  
A: Absolutamente — uma vez que o índice está construído, as consultas são executadas em milissegundos, tornando-o adequado para aplicações interativas.

**Q: Posso integrar esta biblioteca a um projeto Java existente?**  
A: Sim. Adicione a dependência Maven ou o JAR, inicialize o índice conforme mostrado, e você está pronto para usar.

**Última Atualização:** 2026-01-26  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs