---
date: '2026-02-06'
description: Aprenda como adicionar documentos ao índice e habilitar a pesquisa sensível
  a maiúsculas e minúsculas em Java com o GroupDocs.Search, aumentando a precisão
  da sua aplicação.
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 'Adicionar documentos ao índice: pesquisa Java sensível a maiúsculas e minúsculas
  com GroupDocs'
type: docs
url: /pt/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Adicionar documentos ao índice: Dominando buscas sensíveis a maiúsculas e minúsculas em Java com GroupDocs

Recuperar a informação correta de uma enorme coleção de documentos é um requisito essencial para aplicações modernas. Neste guia, você aprenderá **como adicionar documentos ao índice** e executar **buscas sensíveis a maiúsculas e minúsculas** usando GroupDocs.Search para Java. Seja construindo um repositório de documentos legais, um catálogo de e‑commerce ou um sistema de gerenciamento de conteúdo, resultados de busca precisos mantêm os usuários satisfeitos e seus dados confiáveis.

## Respostas rápidas
- **Qual é a etapa principal para começar a buscar?** Adicionar documentos a um índice com `index.add(...)`.
- **Como habilitar a busca sensível a maiúsculas e minúsculas?** Definir `options.setUseCaseSensitiveSearch(true)`.
- **Posso buscar em vários diretórios?** Sim – chame `index.add()` para cada pasta que desejar incluir.
- **Qual método permite buscar com objetos?** Use `SearchQuery.createWordQuery(...)`.
- **Preciso de licença para testes?** Uma licença temporária está disponível para fins de avaliação.

## O que significa “adicionar documentos ao índice”?
Adicionar documentos ao índice significa alimentar seus arquivos de origem (PDFs, documentos Word, texto simples etc.) ao GroupDocs.Search para que ele possa construir uma estrutura de dados pesquisável. Uma vez indexado, o mecanismo pode executar consultas rápidas, inclusive sensíveis a maiúsculas e minúsculas.

## Por que habilitar busca sensível a maiúsculas e minúsculas em Java?
- **Correspondência exata de termos** – diferenciar “Apple” (a empresa) de “apple” (a fruta).  
- **Conformidade regulatória** – alguns setores exigem correspondência exata de frases.  
- **Relevância aprimorada** – usuários frequentemente esperam resultados específicos de caixa em contextos técnicos ou jurídicos.

## Pré‑requisitos
- JDK (Java 17 ou superior recomendado)  
- Maven para gerenciamento de dependências  
- Uma IDE como IntelliJ IDEA ou Eclipse  
- Familiaridade básica com programação Java  

## Configurando GroupDocs.Search para Java
Primeiro, adicione o repositório GroupDocs e a dependência ao seu `pom.xml`:

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

Alternativamente, você pode baixar a versão mais recente diretamente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenciamento
Para começar com uma avaliação, visite o GroupDocs para adquirir uma licença temporária. Isso permitirá que você teste todos os recursos sem limitações.

## Como adicionar documentos ao índice – Busca por Consulta de Texto

### Etapa 1: Criar um índice e adicionar seus documentos
Crie uma pasta onde os arquivos de índice serão armazenados e, em seguida, adicione o diretório de origem que contém os documentos que você deseja buscar.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Dica profissional:** Você pode chamar `index.add()` várias vezes para **buscar em vários diretórios** em um único índice.

### Etapa 2: Habilitar busca sensível a maiúsculas e minúsculas
Configure as opções de busca para respeitar a capitalização das letras.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Etapa 3: Executar uma consulta de texto sensível a maiúsculas e minúsculas
Execute uma consulta que diferencia “Advantages” de “advantages”.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

O loop imprime o caminho completo de cada documento que contém o termo exatamente com a caixa correspondente.

## Como adicionar documentos ao índice – Busca por Consulta de Objeto

Consultas de objeto oferecem mais flexibilidade, especialmente quando você precisa combinar múltiplos critérios.

### Etapa 1: Inicializar um segundo índice (opcional)
Se preferir manter as buscas baseadas em objeto separadas, crie outra pasta de índice.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Etapa 2: Reutilizar a opção sensível a maiúsculas e minúsculas
A mesma instância de `SearchOptions` funciona para consultas de objeto.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Etapa 3: Construir e executar uma consulta de objeto
Crie um objeto de consulta de palavra e passe‑o ao mecanismo de busca.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Usar `createWordQuery` permite que você combine posteriormente com consultas de frase, curinga ou Booleanas para cenários mais complexos.

## Aplicações práticas
- **Gerenciamento de documentos jurídicos:** Recuperar estatutos específicos onde a capitalização importa.  
- **Plataformas de e‑commerce:** Diferenciar SKUs de produtos como “PRO‑X” vs. “pro‑x”.  
- **Sistemas de gerenciamento de conteúdo (CMS):** Garantir que autores encontrem exatamente títulos ou tags.

## Considerações de desempenho
- **Mantenha o índice atualizado** – reindexe quando novos arquivos forem adicionados ou os existentes forem alterados.  
- **Monitore o uso de memória** – corpora grandes se beneficiam de indexação incremental e dimensionamento adequado do heap da JVM.  
- **Aproveite o coletor de lixo do Java** – libere objetos `Index` quando não forem mais necessários.

## Problemas comuns e soluções
| Problema | Solução |
|----------|---------|
| `useCaseSensitiveSearch` parece ignorado | Verifique se está usando a versão mais recente do GroupDocs.Search e se o índice foi reconstruído após alterar a opção. |
| Nenhum resultado retornado para um termo conhecido | Certifique‑se de que o caso do termo corresponde exatamente e de que o documento foi adicionado ao índice com sucesso. |
| Busca em muitas pastas deixa o processo lento | Adicione cada pasta individualmente com `index.add()` e considere dividir o índice em shards para conjuntos de dados muito grandes. |

## Perguntas frequentes

**P:** Como lidar com grandes volumes de dados usando GroupDocs.Search?  
**R:** Utilize particionamento de índice, ajuste as configurações de memória da JVM e compacte periodicamente o índice para manter o desempenho ideal.

**P:** Posso buscar em vários diretórios simultaneamente?  
**R:** Sim – chame `index.add()` para cada diretório que desejar incluir, depois execute uma única consulta contra o índice combinado.

**P:** Quais são as armadilhas comuns ao configurar buscas sensíveis a maiúsculas e minúsculas?  
**R:** Esquecer de reconstruir o índice após habilitar `useCaseSensitiveSearch` ou usar o caso errado na string de consulta.

**P:** Como posso diagnosticar erros de busca?  
**R:** Verifique os arquivos de log gerados pelo GroupDocs.Search para rastreamentos de pilha e confirme que todas as dependências Maven foram resolvidas corretamente.

**P:** O GroupDocs.Search é adequado para aplicações em tempo real?  
**R:** Com estratégias adequadas de indexação (atualizações incrementais e cache em memória), ele pode fornecer resultados de busca quase em tempo real.

## Recursos
- **Documentação:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **Referência de API:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **Repositório GitHub:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Fórum de suporte:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Licença temporária:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Última atualização:** 2026-02-06  
**Testado com:** GroupDocs.Search 25.4  
**Autor:** GroupDocs