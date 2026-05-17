---
date: '2026-01-16'
description: Aprenda como configurar a rede de pesquisa do GroupDocs em Java e adicionar
  sinônimos ao índice para melhorar a eficiência da pesquisa.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Configurar o GroupDocs.Search Network em Java – Impulsionar a Busca
type: docs
url: /pt/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Configure GroupDocs.Search Network in Java – Boost Search

Nas aplicações orientadas a dados de hoje, **configure groupdocs search network** é a etapa chave para oferecer resultados rápidos e precisos em coleções massivas de documentos. Seja construindo um portal de busca corporativo ou ampliando uma solução existente, uma rede GroupDocs.Search bem configurada permite escalar horizontalmente, adicionar suporte a sinônimos e manter a latência baixa. Neste tutorial você aprenderá como configurar, implantar e ajustar finamente uma rede GroupDocs.Search usando Java, além de dicas práticas para adicionar sinônimos ao índice e gerenciar o ciclo de vida dos nós.

## Quick Answers
- **Qual é o principal benefício de configurar uma rede GroupDocs.Search?** Ela permite indexação e consulta distribuídas, melhorando desempenho e escalabilidade.  
- **Preciso de licença para executar os exemplos?** Um teste gratuito funciona para desenvolvimento; uma licença comercial é necessária para produção.  
- **É possível adicionar sinônimos sem reconstruir o índice?** Sim—use o dicionário de sinônimos em tempo de execução para **add synonyms to index**.  
- **Quantos nós posso implantar?** Você pode implantar quantos nós sua infraestrutura permitir; cada nó roda em sua própria porta.  

## What is configuring a GroupDocs.Search network?
Configurar uma rede GroupDocs.Search significa definir a estrutura de pastas, portas e configurações de nós que permitem que múltiplas instâncias JVM colaborem na indexação e busca. Essa configuração cria um nó‑mestre que coordena os workers (shards) e garante que as consultas sejam executadas em todo o conjunto de dados.

## Why configure a GroupDocs.Search network?
- **Scalability** – Distribuir a carga de indexação entre várias máquinas.  
- **Reliability** – Nós podem ser adicionados ou removidos sem tempo de inatividade.  
- **Search relevance** – Adicionar sinônimos ao índice para resultados mais ricos.  
- **Performance** – Execução paralela de consultas reduz o tempo de resposta.

## Prerequisites
- Java Development Kit (JDK) 8 ou mais recente  
- Maven para compilar o projeto  
- Familiaridade básica com a sintaxe Java  
- Acesso à biblioteca GroupDocs.Search for Java (baixada via Maven ou página oficial de releases)

## Setting Up GroupDocs.Search for Java

Adicione o repositório e a dependência ao seu **pom.xml** Maven:

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

Alternativamente, baixe a versão mais recente diretamente de [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
- **Free Trial** – Explore os recursos principais sem custo.  
- **Temporary License** – Desbloqueie todas as funcionalidades para testes de curto prazo.  
- **Commercial License** – Necessária para implantações em produção.

### Basic Initialization and Setup
Crie uma classe Java simples para verificar se a biblioteca carrega corretamente:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Step‑by‑Step Guide to Configure GroupDocs.Search Network

### 1. Configuring the Search Network
Defina a pasta base de documentos e a porta inicial para a comunicação entre nós.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Onde residem os dicionários (por exemplo, arquivos de sinônimos).  
- **basePort** – A primeira porta; nós subsequentes incrementam a partir desse valor.

### 2. Deploying Search Network Nodes
Inicie múltiplos nós worker que compartilham a mesma configuração.

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Cada nó roda em sua própria porta (basePort + índice) e mantém um shard do índice geral.

### 3. Subscribing to Node Events
Monitore a saúde, o progresso da indexação e condições de erro ao anexar um listener de eventos ao nó mestre.

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Os callbacks de evento permitem reagir ao início/parada de nós, conclusão da indexação e falhas inesperadas.

### 4. Adding Synonyms to a Node’s Indexer  
Aumente a relevância ao **add synonyms to index** em tempo de execução.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Array de termos que devem ser tratados como equivalentes.  
- **clearBeforeAdding** – Defina como `true` se quiser substituir entradas existentes.

### 5. Adding Directories for Indexing
Informe ao nó mestre quais pastas contêm os documentos que devem ser pesquisáveis.

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

O método varre o diretório recursivamente e distribui os arquivos entre os shards.

### 6. Performing Text Search in the Network
Execute uma consulta em todos os nós, opcionalmente forçando comportamento de correspondência exata.

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Altere `exactMatchOnly` para `true` quando precisar de correspondência estrita de termos sem stemming.

### 7. Closing Network Nodes
Libere recursos de forma graciosa ao concluir o processamento.

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Um desligamento adequado evita vazamentos de memória e mantém a JVM saudável.

## Practical Applications
| Cenário | Como a rede ajuda |
|----------|-----------------------|
| **Enterprise Search** | Distribui a indexação entre servidores de data‑center para corpora em escala de petabytes. |
| **Document Management** | Adiciona sinônimos ao índice para que usuários encontrem documentos mesmo com terminologia variada. |
| **E‑commerce Catalog** | Implanta nós regionais para servir buscas de produtos localizadas rapidamente. |
| **Content Management** | Mantém o conteúdo pesquisável enquanto editores adicionam novos arquivos a diretórios específicos. |

## Common Issues & Solutions
- **Port Conflicts** – Garanta que a porta de cada nó (basePort + índice) esteja livre; ajuste `basePort` se necessário.  
- **Synonym Not Applied** – Verifique se você chamou `indexer.setDictionary(dictionary)` após adicionar os termos.  
- **Node Not Responding** – Inscreva‑se nos eventos; procure callbacks `NodeFailed` para diagnosticar problemas de rede.  
- **Memory Leak on Close** – Sempre invoque `node.close()` para cada nó implantado.

## Frequently Asked Questions

**Q: How does deploying multiple nodes improve search performance?**  
A: Cada nó indexa um shard dos dados, permitindo processamento paralelo e reduzindo a latência das consultas à medida que a carga é compartilhada.

**Q: Can I add synonyms without re‑indexing existing documents?**  
A: Sim, você pode **add synonyms to index** em tempo de execução via dicionário de sinônimos; as alterações entram em vigor imediatamente para novas consultas.

**Q: Is subscribing to node events mandatory?**  
A: Embora não seja obrigatório para operação básica, a assinatura de eventos fornece visibilidade sobre a saúde dos nós e ajuda a reagir rapidamente a falhas.

**Q: What are best practices for managing node resources?**  
A: Feche nós ociosos regularmente, monitore o uso de memória da JVM e recicle nós durante períodos de baixa demanda para manter o consumo de recursos otimizado.

**Q: Does GroupDocs.Search support non‑text formats like PDFs or images?**  
A: Absolutamente. A biblioteca extrai texto de PDFs, arquivos Office e ainda realiza OCR em imagens, tornando‑os pesquisáveis out‑of‑the‑box.

---

**Last Updated:** 2026-01-16  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs