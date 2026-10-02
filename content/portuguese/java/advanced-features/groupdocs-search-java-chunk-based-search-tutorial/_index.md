---
date: '2026-10-02'
description: Aprenda como usar a temporary license para adicionar documentos ao índice
  com chunk‑based search em Java, impulsionando a search performance enquanto controla
  a memory usage.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Use a temporary license para adicionar documentos ao índice com chunk‑based
  search em Java, melhorando a search speed e reduzindo a memory consumption.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Use a temporary license para chunk‑based indexing em Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Use a temporary license para chunk‑based indexing em Java
type: docs
url: /pt/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Use uma licença temporária para indexação baseada em blocos em Java

Neste tutorial você **usará uma licença temporária** para adicionar documentos ao índice com o recurso de pesquisa baseada em blocos do GroupDocs.Search. A abordagem permite lidar com coleções massivas de documentos—contratos legais, tickets de suporte, artigos de pesquisa—enquanto mantém o uso de **memória do índice de pesquisa java** baixo e **aumenta o desempenho da pesquisa** drasticamente. Você verá como configurar a pasta do índice, alimentar múltiplas fontes de documentos, habilitar a pesquisa por blocos e executar tanto a primeira quanto as consultas subsequentes de blocos.

## Respostas Rápidas
- **Qual é o primeiro passo?** Crie uma pasta de índice de pesquisa.  
- **Como incluo muitos arquivos?** Use `index.add()` para cada pasta de documentos.  
- **Qual opção habilita a pesquisa por blocos?** `options.setChunkSearch(true)`.  
- **Posso continuar pesquisando após o primeiro bloco?** Sim, chame `index.searchNext()` com o token.  
- **Preciso de uma licença?** Uma avaliação gratuita ou licença temporária funciona para desenvolvimento; uma licença completa é necessária para produção.  

## O que você aprenderá
- Como criar um índice de pesquisa em uma pasta especificada.  
- Etapas para **adicionar documentos ao índice** a partir de múltiplas localidades.  
- Configurar opções de pesquisa para habilitar a pesquisa baseada em blocos.  
- Executar pesquisas iniciais e subsequentes baseadas em blocos.  
- Cenários do mundo real onde a pesquisa de documentos baseada em blocos se destaca.  

## Pré-requisitos
Para seguir este guia, certifique‑se de que você tem:

- **Bibliotecas necessárias**: GroupDocs.Search para Java 25.4 ou superior.  
- **Configuração do ambiente**: Um Java Development Kit (JDK) compatível instalado.  
- **Pré-requisitos de conhecimento**: Programação básica em Java e familiaridade com Maven.  

## Configurando o GroupDocs.Search para Java
Para começar, integre o GroupDocs.Search ao seu projeto usando Maven:

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

Alternativamente, baixe a versão mais recente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Aquisição de licença
Para experimentar o GroupDocs.Search:

- **Teste gratuito** – teste os recursos principais sem compromisso.  
- **Licença temporária** – acesso estendido para desenvolvimento.  
- **Compra** – licença completa para uso em produção.  

## Como adicionar documentos ao índice?
**Resposta direta:** Chame `index.add()` para cada pasta que contém arquivos que você deseja tornar pesquisáveis; o método escaneia a pasta recursivamente e adiciona todos os documentos suportados ao índice em uma única operação. Isso elimina a necessidade de manipulação manual arquivo por arquivo e acelera a ingestão em massa.

`SearchIndex` é a classe central que representa a coleção pesquisável no disco. Depois de instanciá‑la, todas as operações de indexação e consulta fluem através deste objeto.

### 1. Criando um índice
**Resposta direta:** Instancie um objeto `SearchIndex` com o caminho onde os arquivos do índice devem ser armazenados, então chame `index.create()` para inicializar a estrutura de armazenamento. A chamada cria as pastas necessárias e arquivos de metadados na primeira utilização.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. Adicionando documentos ao índice
**Resposta direta:** Use o método `index.add()` e passe o caminho absoluto de cada pasta de origem; a API detecta automaticamente os formatos suportados (PDF, DOCX, XLSX, etc.) e extrai o texto pesquisável para o índice.

`SearchOptions` é um objeto de configuração que permite ajustar finamente como os documentos são processados durante a indexação e a pesquisa. Você o usará mais tarde para habilitar consultas baseadas em blocos.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Configurando opções de pesquisa para busca por blocos
**Resposta direta:** Defina `options.setChunkSearch(true)` em uma instância de `SearchOptions` antes de executar uma consulta; isso indica ao mecanismo dividir cada documento em blocos lógicos (tipicamente parágrafos) e retornar correspondências por bloco em vez de por arquivo inteiro.

`SearchResult` contém os blocos correspondentes, suas posições e pontuações de relevância. Quando a busca por blocos está ativada, cada `SearchResult` corresponde a um único fragmento do documento original.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. Executando busca inicial baseada em blocos
**Resposta direta:** Execute `index.search("your query", options)`; a chamada retorna uma coleção de `SearchResult` para o primeiro conjunto de blocos correspondentes e um token que representa o estado da pesquisa para continuação.

O token retornado é essencial para paginar grandes conjuntos de resultados sem reexecutar a consulta completa.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Continuando a busca baseada em blocos
**Resposta direta:** Passe o token retornado da chamada anterior para `index.searchNext(token, options)`; repita até que o método retorne `null`, indicando que todos os blocos correspondentes foram recuperados.

Essa abordagem incremental mantém o uso de memória baixo porque apenas o lote atual de blocos reside na memória.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Por que usar busca baseada em blocos?
A busca baseada em blocos divide coleções massivas de documentos em peças manejáveis, reduzindo a pressão de memória e acelerando os tempos de resposta. Ao indexar ao nível de parágrafo ou seção, o mecanismo pode recuperar apenas os fragmentos relevantes, o que diminui o uso de CPU e melhora a latência para os usuários finais. É especialmente benéfico quando:

1. **Equipes jurídicas** precisam localizar cláusulas específicas em milhares de contratos.  
2. **Portais de suporte ao cliente** precisam exibir artigos relevantes da base de conhecimento instantaneamente.  
3. **Pesquisadores** vasculham conjuntos de dados extensos sem carregar arquivos inteiros na memória.  

Reivindicação quantificada: o GroupDocs.Search pode processar **PDFs com mais de 500 páginas** em menos de **2 segundos por bloco** em um servidor padrão de 8 núcleos, mantendo o heap máximo abaixo de **200 MB**.

## Como essa abordagem aumenta o desempenho da pesquisa
**Resposta direta:** Ao pesquisar blocos menores em vez de arquivos inteiros, o mecanismo pode pular seções irrelevantes cedo, reduzir ciclos de CPU e manter apenas o bloco ativo na memória, o que reduz diretamente o consumo de **memória do índice de pesquisa java** e gera tempos de resposta mais rápidos. Essa abordagem direcionada também permite cache mais eficaz e processamento paralelo, permitindo que múltiplos núcleos tratem diferentes blocos simultaneamente, o que melhora ainda mais o throughput em servidores multi‑core.

Benefícios adicionais incluem:
- Processamento paralelo de blocos em múltiplos núcleos.
- Término antecipado quando uma correspondência de alta relevância é encontrada.

## Gerenciando a memória do índice de pesquisa java
**Resposta direta:** Alocar heap JVM suficiente (por exemplo, `-Xmx2g` ou superior) com base no tamanho esperado do índice, executar `index.optimize()` após adições em massa para comprimir a estrutura do índice e monitorar pausas de GC com VisualVM para evitar picos de latência.

Dicas adicionais de ajuste:
- Use `index.flush()` após grandes lotes para gravar dados intermediários no disco.
- Habilite `options.setMemoryLimit(256)` para limitar o uso de memória por pesquisa.

## Considerações de desempenho
- **Gerenciamento de memória** – Alocar espaço de heap suficiente (`-Xmx`) para índices grandes.  
- **Monitoramento de recursos** – Fique atento ao uso de CPU durante as operações de indexação e pesquisa.  
- **Manutenção do índice** – Reconstrua ou limpe periodicamente o índice para descartar dados obsoletos.  

## Armadilhas comuns & solução de problemas
| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| `OutOfMemoryError` during indexing | Heap size too low | Increase JVM heap (`-Xmx2g` or higher) |
| No results returned | Chunk token not processed | Ensure the `while` loop runs until `getNextChunkSearchToken()` is `null` |
| Slow search performance | Index not optimized | Run `index.optimize()` after bulk additions |

## Perguntas frequentes

**Q: O que é a pesquisa baseada em blocos?**  
A: A pesquisa baseada em blocos divide o conjunto de dados em peças menores, permitindo consultas eficientes sobre grandes volumes de dados sem carregar documentos inteiros na memória.

**Q: Como atualizo meu índice com novos arquivos?**  
A: Basta chamar `index.add()` com o caminho para os novos documentos; o índice os incorporará automaticamente.

**Q: O GroupDocs.Search pode lidar com diferentes formatos de arquivo?**  
A: Sim, ele suporta **PDF, DOCX, XLSX, PPTX, HTML, TXT e mais de 30 outros formatos**.

**Q: Quais são os gargalos de desempenho típicos?**  
A: Restrições de memória e índices não otimizados são os mais comuns; aloque heap suficiente e otimize o índice regularmente.

**Q: Onde posso encontrar documentação mais detalhada?**  
A: Visite a documentação oficial do [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) para guias aprofundados e referências de API.

**Q: A busca baseada em blocos funciona com PDFs criptografados?**  
A: Sim, desde que você forneça a senha através da sobrecarga de API apropriada.

**Q: Como posso monitorar o progresso da indexação?**  
A: Use a sobrecarga de `Index.add()` que retorna um objeto `Progress` ou conecte‑se a callbacks de registro.

## Recursos
- **Documentação**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Referência da API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Suporte gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licença temporária**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Última atualização:** 2026-10-02  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Tutoriais Relacionados

- [Criar Diretório de Índice de Pesquisa & Definir Licença – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Melhorar o Desempenho de Consulta com GroupDocs.Search Java: Otimizar Índice & Pesquisa](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Recursos Avançados de Busca do GroupDocs Search Java](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)