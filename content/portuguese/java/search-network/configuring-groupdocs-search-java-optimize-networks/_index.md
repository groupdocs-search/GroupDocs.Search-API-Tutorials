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

# Configure a rede GroupDocs.Search em Java – Impulsione a pesquisa

Nas aplicações voltadas para os dados de hoje, **configure groupdocs search network** é uma etapa chave para oferecer resultados rápidos e precisos em coleções massivas de documentos. Seja construindo um portal de busca corporativa ou ampliando uma solução existente, uma rede GroupDocs.Search bem definida permite escalar horizontalmente, adicionar suporte a sinônimos e manter a latência baixa. Neste tutorial você aprenderá como configurar, implantar e ajustar finamente uma rede GroupDocs.Search using Java, além de dicas práticas para adicionar símbolos simultâneos ao índice e gerenciar o ciclo de vida dos nós.

## Respostas rápidas
- **Qual é o principal benefício de configurar uma rede GroupDocs.Search?**Ela permite indexação e consulta distribuída, melhorando desempenho e escalabilidade.
- **Preciso de licença para executar os exemplos?**Um teste gratuito funciona para desenvolvimento; uma licença comercial é necessária para produção.
- **É possível adicionar sinônimos sem reconstruir o índice?**Sim—use o dicionário de sinônimos em tempo de execução para **adicionar sinônimos ao índice**.
- **Quantos nós podemos implantar?**Você pode implantar quantos nós sua infraestrutura permitir; cada nó roda em sua própria porta.

## O que é configurar uma rede GroupDocs.Search?
Configurar uma rede GroupDocs.Search significa definir uma estrutura de pastas, portas e configurações de nós que permitem que múltiplas instâncias JVM colaborem na indexação e busca. Essa configuração cria um nó‑mestre que coordena os trabalhadores (shards) e garante que as consultas sejam realizadas em todo o conjunto de dados.

## Por que configurar uma rede GroupDocs.Search?
- **Escalabilidade** – Distribuir carga de indexação entre várias máquinas.
- **Confiabilidade** – Nós podemos ser aumentados ou removidos sem tempo de inatividade.
- **Relevância da pesquisa** – Adicionar variáveis ​​ao índice para resultados mais ricos.
- **Desempenho** – A execução paralela de consultas reduz o tempo de resposta.

## Pré-requisitos
- Java Development Kit (JDK)8 ou mais recente
- Maven para compilar o projeto
- Familiaridade básica com a sintaxe Java
- Acesso à biblioteca GroupDocs.Search for Java (baixada via Maven ou página oficial de releases)

## Configurando GroupDocs.Search para Java

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

### Aquisição de licença
- **Teste Gratuito** – Explore os recursos principais sem custo.
- **Licença Temporária** – Desbloqueie todas as funcionalidades para testes de curto prazo.
- **Licença Comercial** – Necessária para implantações em produção.

### Inicialização e configuração básicas
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

## Guia passo a passo para configurar a rede GroupDocs.Search

### 1. Configurando a rede de pesquisa
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

### 2. Implantação de Nós de Rede de Busca
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

### 3. Inscrição em Eventos de Nós
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

### 4. Adição de Sinônimos ao Indexador de um Nó 
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

### 5. Adição de Diretórios para Indexação
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

### 6. Realização de Busca de Texto na Rede
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

### 7. Encerramento de Nós de Rede
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

## Aplicações Práticas
| Cenário | Como a rede ajuda |
|----------|------------|
| **Pesquisa empresarial** | Distribui indexação entre servidores de data center para corpora em escala de petabytes. |
| **Gerenciamento de documentos** | Adicionados aleatoriamente ao índice para que os usuários encontrem documentos mesmo com terminologia variada. |
| **Catálogo de comércio eletrônico** | Implante nós regionais para servir buscas de produtos localizadas rapidamente. |
| **Gerenciamento de conteúdo** | Os editores mantêm o conteúdo pesquisável enquanto adicionam novos arquivos a diretórios específicos. |

## Problemas e soluções comuns
- **Port Conflicts** – Garanta que a porta de cada nó (basePort+índice) esteja livre; ajuste `basePort` se necessário.
- **Sinônimo não aplicado** – Verifique se você chamou `indexer.setDictionary(dictionary)` após adicionar os termos.
- **Node Not Responding** – Inscreva‑se nos eventos; obtenha retornos de chamada `NodeFailed` para diagnosticar problemas de rede.
- **Memory Leak on Close** – Sempre invoca `node.close()` para cada nó implantado.

## Perguntas frequentes

**P: Como a implantação de vários nós melhora o desempenho da pesquisa?**
R: Cada nó indexa um fragmento de dados, permitindo o processamento paralelo e reduzindo a latência das consultas na medida em que a carga é compartilhada.

**P: Posso adicionar sinônimos sem reindexar documentos existentes?**
R: Sim, você pode **adicionar sinônimos ao índice** em tempo de execução via dicionário de sinônimos; as alterações entram em vigor imediatamente para novas consultas.

**P: A assinatura de eventos de nó é obrigatória?**
R: Embora não seja obrigatório para a operação básica, a assinatura de eventos fornece visibilidade sobre a saúde de nós e ajuda a reagir rapidamente a falhas.

**P: Quais são as práticas recomendadas para gerenciar recursos de nós?**
R: Feche-nos ociosos regularmente, monitore o uso de memória da JVM e recicle-nos durante períodos de baixa demanda para manter o consumo de recursos otimizado.

**P: O GroupDocs.Search é compatível com formatos não textuais, como PDFs ou imagens?**
R: Absolutamente. A biblioteca extrai texto de PDFs, arquivos Office e ainda realiza OCR em imagens, tornando‑os pesquisáveis ​​out‑of‑the‑box.

---

**Última atualização:** 16/01/2026
**Testado com:** GroupDocs.Search 25.4 para Java
**Autor:** GroupDocs