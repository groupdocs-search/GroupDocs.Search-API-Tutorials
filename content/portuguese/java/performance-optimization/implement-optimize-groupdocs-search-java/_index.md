---
date: '2026-07-07'
description: Aprenda como excluir o índice, executar pesquisa de texto completo em
  Java e otimizar o desempenho da pesquisa usando GroupDocs.Search for Java. Guia
  passo a passo com configuração de rede e indexação.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: Como excluir o índice e executar pesquisa de texto completo em Java
  usando GroupDocs.Search. Siga este guia para configurar uma rede de pesquisa, criar
  um índice pesquisável e otimizar o desempenho da pesquisa.
og_title: Como excluir o índice e executar pesquisa de texto com GroupDocs.Search
  for Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: Como excluir o índice e executar pesquisa de texto com GroupDocs.Search for
  Java
type: docs
url: /pt/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Como Excluir o Índice e Realizar Busca de Texto com GroupDocs.Search para Java

No mundo orientado a dados de hoje, **como excluir o índice** rapidamente enquanto ainda oferece recursos de busca de texto completo em Java ultrarrápidos é uma vantagem competitiva. Seja construindo uma base de conhecimento interna, um repositório de casos jurídicos ou um catálogo de produtos de e‑commerce, uma rede de busca bem ajustada pode melhorar drasticamente a satisfação do usuário. Neste guia, você aprenderá a **configurar uma rede de busca**, **criar um índice pesquisável**, **otimizar o desempenho da busca** e **excluir documentos do índice** quando necessário — tudo usando o GroupDocs.Search para Java.

## Respostas Rápidas
- **Qual é o objetivo principal do GroupDocs.Search para Java?** Ele fornece busca de texto completo em mais de 50 formatos de documentos, permitindo recuperação rápida de palavras‑chave.  
- **Como realizo busca de texto em um ambiente distribuído?** Implante uma rede de busca, indexe documentos em um nó mestre e, em seguida, consulte qualquer nó.  
- **Posso excluir documentos do índice sem reconstruí‑lo?** Sim, use a API Delete para remover arquivos selecionados, efetivamente *como excluir o índice* sem reindexação completa.  
- **Qual versão do Java é necessária?** JDK 8 ou superior.  
- **É necessária uma licença para produção?** É necessária uma licença válida do GroupDocs.Search; uma avaliação gratuita está disponível.

## O que é “perform text search”?
Realizar busca de texto significa consultar um índice de texto completo para recuperar documentos que contenham as palavras‑chave ou frases especificadas. O GroupDocs.Search cria um índice invertido que torna essas consultas extremamente rápidas, mesmo em milhares de arquivos.

## Por que configurar uma rede de busca?
Uma rede de busca distribui as cargas de indexação e consulta entre vários nós, permitindo que você **otimize o desempenho da busca**, escale horizontalmente e mantenha alta disponibilidade. Essa arquitetura é ideal para repositórios de documentos em nível empresarial, onde latência e taxa de transferência são importantes.

## Como Implementar e Otimizar uma Rede de Busca com GroupDocs.Search para Java
Carregue sua configuração, inicie um nó mestre e, em seguida, adicione nós de trabalho que compartilham o mesmo caminho base e porta. Implantar a rede dessa forma permite que qualquer nó trate solicitações de indexação ou consulta, oferecendo tempos de resposta consistentes mesmo à medida que a quantidade de documentos cresce para centenas de milhares.

### Visão geral passo a passo
1. **Defina uma configuração base** que inclua um diretório compartilhado e uma porta TCP.  
2. **Inicie o nó mestre** para gerenciar o índice e coordenar os nós de trabalho.  
3. **Adicione nós de trabalho** que se conectam ao mestre, permitindo indexação e busca paralelas.  
4. **Monitore o uso de recursos** e ajuste as configurações de heap da JVM para manter a latência baixa.

## Como Excluir o Índice no GroupDocs.Search para Java
`SearchNode` representa um nó na rede GroupDocs.Search que gerencia operações de indexação e consulta. O método `delete` remove documentos especificados do índice.

### Etapas de exclusão direta
- Chame o método `delete` na instância `SearchNode`.  
- Forneça um array de caminhos de arquivos relativos.  
- Confirme as alterações; o índice é atualizado instantaneamente e buscas subsequentes não retornam mais os arquivos removidos.

## O que é uma Rede de Busca?
Uma **rede de busca** é um cluster de nós interconectados que compartilham um repositório de índice comum, permitindo indexação distribuída e execução de consultas. Ela possibilita escalabilidade horizontal e tolerância a falhas para coleções de documentos em grande escala.

## Como Criar um Índice Pesquisável (index documents java)
O método `add` indexa um documento no índice de busca. Adicione documentos ao nó mestre usando o método `add`; a rede propaga as alterações para todos os nós de trabalho. Essa abordagem garante que cada nó possa atender consultas contra o índice mais recente sem etapas adicionais de sincronização.

### Ações principais
- Aponte o nó mestre para a pasta que contém os arquivos de origem.  
- Invoque a rotina de indexação; a rede processa cada arquivo e atualiza o índice invertido.  
- Verifique se os arquivos de índice aparecem no diretório de armazenamento designado.

## Como Remover Arquivos Indexados (remove indexed files)
Quando um documento se torna obsoleto, chame a API `delete` com seu caminho. O sistema remove as entradas do arquivo do índice invertido, liberando armazenamento e evitando resultados desatualizados.

## Configurando o GroupDocs.Search para Java
Para começar, integre o GroupDocs.Search ao seu projeto Java usando a configuração a seguir:

### Configuração Maven
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

### Download Direto
Alternativamente, você pode [baixar a versão mais recente diretamente da GroupDocs](https://releases.groupdocs.com/search/java/).

### Aquisição de Licença
A GroupDocs oferece uma avaliação gratuita, que permite avaliar seus recursos antes da compra. Você pode obter uma licença temporária seguindo os passos na página de [compra](https://purchase.groupdocs.com/temporary-license/). Isso habilitará a funcionalidade completa durante sua fase de testes.

### Inicialização e Configuração Básicas
Inicialize o GroupDocs.Search em sua aplicação Java com:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## Guia de Implementação

### Configurando a Rede de Busca
**Visão geral:** Defina um caminho base e uma porta para sua rede de busca, permitindo que os nós se comuniquem efetivamente.

#### Etapa 1: Definir Configuração Base
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parâmetros:**  
  - `basePath`: Caminho do diretório para operações da rede.  
  - `basePort`: Número da porta usada pela rede de busca.

#### Etapa 2: Solução de Problemas
Certifique-se de que a porta especificada não esteja bloqueada por configurações de firewall ou sendo usada por outra aplicação. Ajuste conforme necessário para evitar conflitos.

### Implantando Nós da Rede de Busca
**Visão geral:** Usando sua configuração, implante nós em sua rede para indexação e busca distribuídas.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Opções de Configuração Principais:**  
  - **Base Path & Port:** Esses valores devem corresponder aos usados na sua configuração inicial para garantir consistência.

### Indexando Documentos (`create searchable index`)
**Visão geral:** Adicione documentos ao índice de busca de forma eficiente usando um nó mestre.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Objetivo:**  
  - `masterNode`: O nó principal que gerencia a indexação de documentos.  
  - `documentsPath`: Caminho para o diretório que contém os documentos.

#### Dicas de Solução de Problemas
Verifique se os caminhos dos documentos estão corretos e acessíveis. Certifique‑se de que as permissões permitem leitura desses diretórios.

### Buscando Texto na Rede (`perform text search`)
**Visão geral:** Realize buscas de texto abrangentes em sua rede indexada.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- `query`: O texto que você está buscando.  
- `masterNode`: Nó que realiza a busca.

### Excluindo Documentos do Índice (`delete documents index`)
**Visão geral:** Remova documentos específicos do seu índice usando seus caminhos de arquivo.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- `node`: O nó alvo para operações de exclusão.  
- `filePaths`: Caminhos dos documentos a serem removidos do índice.

#### Solução de Problemas
Certifique‑se de que os caminhos dos arquivos são precisos e que os arquivos existam no seu diretório. Se os problemas persistirem, verifique as permissões da rede e a conectividade.

## Aplicações Práticas
1. **Gerenciamento de Documentos Corporativos:** Otimize a recuperação de conhecimento interno.  
2. **Análise de Casos Jurídicos:** Localize rapidamente arquivos de casos relevantes em múltiplos repositórios.  
3. **Plataformas de E‑commerce:** Aumente a velocidade de busca de produtos indexando descrições e avaliações.  
4. **Pesquisa Acadêmica:** Pesquise eficientemente grandes bibliotecas digitais de artigos e teses.  
5. **Sistemas de Suporte ao Cliente:** Reduza o tempo de resposta permitindo que agentes busquem tickets anteriores instantaneamente.

## Considerações de Desempenho
- **Otimizar a Velocidade de Indexação:** Adicione documentos novos incrementalmente durante períodos de baixa demanda para manter a latência baixa.  
- **Diretrizes de Uso de Recursos:** Monitore CPU e memória, especialmente ao escalar o número de nós.  
- **Gerenciamento de Memória Java:** Ajuste as configurações de heap da JVM com base na sua carga de trabalho (por exemplo, `-Xmx2g` para índices de tamanho médio).

## Conclusão
Seguindo este guia, você aprendeu a **configurar uma rede de busca**, **criar um índice pesquisável**, **realizar busca de texto** e **excluir documentos do índice** usando o GroupDocs.Search para Java. Essas capacidades permitem recuperação de documentos rápida e confiável em ambientes distribuídos.

**Próximos Passos**
- Experimente diferentes configurações de nós para encontrar o equilíbrio ideal para sua carga de trabalho.  
- Aprofunde-se em opções avançadas de indexação, como analisadores personalizados e ajuste de relevância.  
- Explore a integração com outros produtos GroupDocs para processamento de documentos de ponta a ponta.

## Perguntas Frequentes

**Q: Qual é o caso de uso principal do GroupDocs.Search para Java?**  
A: Ele fornece busca de texto completo em diversos formatos de documentos, permitindo que você **perform text search** em grandes repositórios.

**Q: Como posso melhorar a velocidade de busca em uma grande rede?**  
A: Implante nós adicionais, ajuste o heap da JVM e agende a indexação durante períodos de baixo tráfego para **optimize search performance**.

**Q: É possível excluir um único documento sem reindexar toda a coleção?**  
A: Sim, use a API **delete documents index** conforme mostrado no exemplo de código para remover arquivos específicos.

**Q: Preciso de uma licença para desenvolvimento?**  
A: Uma licença de avaliação gratuita é suficiente para testes; uma licença comercial é necessária para implantações em produção.

**Q: Posso indexar PDFs, arquivos Word e e‑mails juntos?**  
A: Absolutamente — o GroupDocs.Search suporta uma ampla variedade de formatos nativamente.

---

**Last Updated:** 2026-07-07  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs

## Tutoriais Relacionados

- [Como Indexar Texto em Java com o Guia GroupDocs.Search](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [Otimizar Desempenho de Busca com Técnicas Avançadas de Indexação no GroupDocs.Search para Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [Melhorar Desempenho de Consulta com GroupDocs.Search Java: Otimizar Índice & Busca](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)