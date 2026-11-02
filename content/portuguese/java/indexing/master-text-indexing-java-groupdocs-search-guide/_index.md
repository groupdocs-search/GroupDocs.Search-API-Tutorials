---
date: '2026-11-02'
description: Aprenda como adicionar pasta ao índice com GroupDocs.Search em Java,
  configurar compressão alta e executar fast full‑text queries.
keywords:
- add folder to index
- java full text search
- groupdocs search compression
lastmod: '2026-11-02'
og_description: Aprenda como adicionar pasta ao índice com GroupDocs.Search em Java,
  configurar compressão e executar fast full‑text searches. Ideal para grandes conjuntos
  de documentos.
og_image_alt: Guide showing Java code for adding a folder to a GroupDocs.Search index
og_title: Como adicionar pasta ao índice com GroupDocs.Search em Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  headline: How to add folder to index with GroupDocs.Search in Java
  type: TechArticle
- description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  name: How to add folder to index with GroupDocs.Search in Java
  steps:
  - name: define the index folder
    text: 'Choose a directory where the index files will reside:'
  - name: configure index settings
    text: '`TextStorageSettings` configures how text is stored in the index, including
      compression level. `Compression` is an enum that specifies the desired compression
      algorithm.'
  - name: create the index with custom settings
    text: 'Instantiate the index using the configuration defined above:'
  type: HowTo
- questions:
  - answer: It is a robust Java library that provides advanced full‑text search capabilities,
      including indexing, compression, and complex query support.
    question: What is GroupDocs.Search?
  - answer: Enable high compression (`Compression.High`) and periodically commit changes
      to keep the index lean. Also, allocate sufficient heap memory (e.g., 4 GB for
      indexes over 20 GB).
    question: How do I handle large datasets with GroupDocs.Search?
  - answer: Yes, the library can be embedded in any Java‑based backend, REST services,
      or micro‑services architecture.
    question: Can I integrate GroupDocs.Search with existing enterprise systems?
  - answer: Use the `index.add()` method to append new files and `index.delete()`
      to remove obsolete ones, then re‑run `index.optimize()` if needed.
    question: What if my index becomes outdated?
  - answer: Visit the community forum at [GroupDocs forums](https://forum.groupdocs.com/c/search/10)
      for troubleshooting and best‑practice tips.
    question: Where can I get help or support?
  type: FAQPage
tags:
- add folder to index
- groupdocs search
- java search indexing
title: Como adicionar pasta ao índice com GroupDocs.Search em Java
type: docs
url: /pt/java/indexing/master-text-indexing-java-groupdocs-search-guide/
weight: 1
---

# Como adicionar pasta ao índice com GroupDocs.Search em Java

## Respostas rápidas
- **Qual é a biblioteca principal?** GroupDocs.Search for Java  
- **Como adicionar uma pasta ao índice?** Use `index.add(folderPath)`  
- **Posso configurar compressão de texto?** Sim, via `TextStorageSettings(Compression.High)`  
- **Qual versão do Java é necessária?** JDK 8 ou superior  
- **Onde obter uma licença de avaliação?** No site da GroupDocs ou na página do repositório  

## O que é pesquisa de texto completo em Java e por que isso importa?

A pesquisa de texto completo em Java converte documentos brutos em um índice invertido, permitindo a recuperação em subsegundos de qualquer termo em milhares de arquivos. Essa capacidade é essencial para repositórios jurídicos, bibliotecas de pesquisa e bases de conhecimento corporativas onde os usuários esperam resultados instantâneos. Também melhora a produtividade em aplicações modernas.

## Por que usar groupdocs.search para pesquisa de texto completo em Java?

GroupDocs.Search oferece indexação de alta taxa de transferência e execução de consultas, além de compressão avançada integrada. Suporta **mais de 50 formatos de entrada e saída**—incluindo PDF, DOCX, EML e HTML—e pode processar documentos com centenas de páginas sem carregar o arquivo inteiro na memória, mantendo a pegada de memória abaixo de 200 MB para cargas de trabalho típicas.

## Pré-requisitos

- **GroupDocs.Search for Java** (versão 25.4 ou posterior) – a biblioteca central que alimenta a indexação e a pesquisa.  
- **JDK 8+** instalado e configurado – o runtime mínimo exigido para o SDK.  
- **Maven** para gerenciamento de dependências – simplifica a adição da biblioteca ao seu projeto.  
- Uma IDE como **IntelliJ IDEA** ou **Eclipse** – para escrever e depurar código Java.

## Configurando o GroupDocs.Search para Java

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
Alternativamente, faça o download da versão mais recente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Aquisição de licença
- **Free trial** – explore todos os recursos sem compromisso.  
- **Temporary license** – período de teste estendido.  
- **Purchase** – desbloqueie todas as capacidades de produção.

### Inicialização e configuração básicas
`Index` é a classe central usada para criar, abrir e gerenciar um índice de pesquisa.

```java
import com.groupdocs.search.Index;

public class InitializeSearch {
    public static void main(String[] args) {
        // Path to store index data
        String indexPath = "path/to/index";
        
        // Creating an index at specified location
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## Indexar texto com compressão personalizada

### Etapa 1: definir a pasta do índice
Escolha um diretório onde os arquivos de índice serão armazenados:

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\StoringTextOfIndexedDocuments";
```

### Etapa 2: configurar as definições do índice
`TextStorageSettings` configura como o texto é armazenado no índice, incluindo o nível de compressão. `Compression` é um enum que especifica o algoritmo de compressão desejado.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.options.TextStorageSettings;
import com.groupdocs.search.compression.Compression;

IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Etapa 3: criar o índice com configurações personalizadas
Instancie o índice usando a configuração definida acima:

```java
Index index = new Index(indexFolder, settings);
System.out.println("Index created with high compression.");
```

## Como adicionar uma pasta ao índice

`Index` é a classe principal que representa o índice pesquisável.

Carregue o índice existente (ou crie um novo) e então chame o método `add` no objeto `Index`. A operação `add` varre o diretório fornecido, extrai texto de cada arquivo suportado e o armazena no índice comprimido, pronto para busca instantânea.

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual document path.
Index index = new Index(indexFolder);
```

## Como pesquisar documentos indexados

`SearchResult` representa uma correspondência única com caminho do documento e relevância.

Defina uma string de consulta que represente o termo ou frase que você deseja localizar, então invoque o método `search` na instância `Index`. O método retorna uma coleção de objetos `SearchResult`, cada um contendo o caminho do documento, pontuação de relevância e um trecho destacando a correspondência.

```java
index.add(documentsFolder);
System.out.println("Documents added successfully.");
```

## Aplicações práticas

Cenários reais onde **java full text search** se destaca:

1. **Legal document management** – recuperação instantânea de arquivos de casos.  
2. **Academic research libraries** – busca rápida de artigos e teses.  
3. **Enterprise knowledge bases** – acesso rápido a manuais e FAQs.  
4. **Content management systems** – descoberta eficiente de conteúdo para sites grandes.  
5. **Customer service archives** – busca rápida de tickets e chats anteriores.  

## Considerações de desempenho

- **Compressão vs. velocidade**: compressão alta economiza até 70 % de espaço em disco, mas adiciona uma leve sobrecarga de indexação; execute testes de benchmark para seu volume de dados.  
- **Gerenciamento de memória**: aloque pelo menos 2 GB de heap para índices maiores que 10 GB para evitar `OutOfMemoryError`.  
- **Atualizações de índice**: adicione documentos incrementalmente com `index.add()` e chame periodicamente `index.optimize()` para manter o índice compacto.  
- **Otimização de consultas**: use a sintaxe avançada de consultas (coringas, proximidade, busca difusa) para refinar resultados e reduzir o tempo de resposta.

## Armadilhas comuns e dicas profissionais

- **Armadiça:** Esquecer de chamar `index.optimize()` após adições em massa.  
  **Dica profissional:** Execute `index.optimize()` todas as noites para manter o índice compacto.  

- **Armadiça:** Usar a compressão padrão (baixa) em conjuntos de dados massivos.  
  **Dica profissional:** Troque para `Compression.High` em ambientes de produção para reduzir custos de armazenamento.  

- **Armadiça:** Não tratar `IOException` ao adicionar arquivos de um compartilhamento de rede.  
  **Dica profissional:** Envolva `index.add()` em um bloco try‑catch e registre quaisquer falhas para revisão posterior.  

## Perguntas frequentes

**Q: O que é GroupDocs.Search?**  
A: É uma biblioteca Java robusta que fornece recursos avançados de pesquisa de texto completo, incluindo indexação, compressão e suporte a consultas complexas.

**Q: Como lidar com grandes volumes de dados usando GroupDocs.Search?**  
A: Ative compressão alta (`Compression.High`) e faça commit das alterações periodicamente para manter o índice enxuto. Também aloque memória heap suficiente (por exemplo, 4 GB para índices acima de 20 GB).

**Q: Posso integrar GroupDocs.Search a sistemas corporativos existentes?**  
A: Sim, a biblioteca pode ser incorporada a qualquer backend Java, serviços REST ou arquitetura de microsserviços.

**Q: E se meu índice ficar desatualizado?**  
A: Use o método `index.add()` para acrescentar novos arquivos e `index.delete()` para remover os obsoletos, então execute `index.optimize()` novamente, se necessário.

**Q: Onde posso obter ajuda ou suporte?**  
A: Visite o fórum da comunidade em [GroupDocs forums](https://forum.groupdocs.com/c/search/10) para solução de problemas e dicas de boas práticas.

## Recursos adicionais

- Guia de uso detalhado: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- Referência completa da API: [API Reference Guide](https://reference.groupdocs.com/search/java)  
- Mantenha-se atualizado com novos recursos: [Latest Releases](https://releases.groupdocs.com/search/java/)  

---

**Last Updated:** 2026-11-02  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs  

---

```java
String query = "sample";  
```

```java
import com.groupdocs.search.results.SearchResult;

SearchResult result = index.search(query);
System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## Tutoriais Relacionados

- [Groupdocs Search Java Create Index Guide](/search/java/indexing/groupdocs-search-java-create-index-guide/)
- [Mastering Groupdocs Search Java Index Management Guide](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Java Full Text Search Library – Optimize Index with GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)