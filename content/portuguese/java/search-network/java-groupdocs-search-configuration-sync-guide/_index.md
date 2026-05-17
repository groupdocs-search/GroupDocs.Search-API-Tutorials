---
date: '2026-05-17'
description: Aprenda como adicionar a dependência Maven do groupdocs, configurar uma
  rede de pesquisa Java e adicionar diretórios ao índice para recuperação de documentos
  rápida e escalável.
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: Como adicionar a dependência Maven do GroupDocs para rede de pesquisa
type: docs
url: /pt/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# Como Adicionar a Dependência Maven do GroupDocs para Rede de Busca

Neste guia abrangente, você descobrirá **como adicionar a dependência Maven do groupdocs**, configurar uma rede de busca Java robusta usando GroupDocs.Search e manter seus shards sincronizados. Seja indexando pareceres jurídicos, demonstrações financeiras ou artigos acadêmicos, os passos abaixo ajudarão você a criar índices pesquisáveis, distribuir a carga de consultas entre nós e manter a consistência dos dados com esforço mínimo.

## Respostas Rápidas
- **O que é a dependência Maven do GroupDocs?** Um artefato Maven que inclui a biblioteca GroupDocs.Search para projetos Java.  
- **Por que usar uma rede de busca?** Ela distribui a carga de indexação e consultas entre múltiplos nós, melhorando a velocidade e a confiabilidade.  
- **Como adiciono diretórios ao índice?** Use `IndexingDocuments.addDirectories` no nó mestre.  
- **Como sincronizar shards?** Chame `SynchronizeOptions` no `Indexer` de cada nó.  
- **Preciso de uma licença?** Sim, uma licença de avaliação ou comercial é necessária para uso em produção.

## O que é a Dependência Maven do GroupDocs?

A `dependência Maven do GroupDocs` é um artefato Maven que inclui a biblioteca GroupDocs.Search para projetos Java.  
Ela fornece todas as classes necessárias para criar índices pesquisáveis, gerenciar nós da rede e executar consultas rápidas, e o Maven resolve dependências transitivas automaticamente, proporcionando um motor de busca pronto‑para‑usar com apenas algumas linhas no seu `pom.xml`.

## Como Adicionar a Dependência Maven do GroupDocs

Adicione as entradas de repositório e dependência ao seu `pom.xml`, então execute `mvn clean install`; o Maven baixa o JAR `groupdocs-search` e suas bibliotecas necessárias, tornando a API disponível em seu projeto. Após a construção ser concluída com sucesso, você pode começar a usar as classes `com.groupdocs.search` imediatamente.

### Configuração Maven

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

> **Dica:** Mantenha o número da versão atualizado verificando a página oficial de lançamentos.

Você também pode baixar o JAR diretamente do site oficial: [Lançamentos do GroupDocs.Search para Java](https://releases.groupdocs.com/search/java/).

## Por que Usar uma Rede de Busca?

Uma rede de busca permite escalabilidade horizontal ao particionar o índice em shards que residem em nós separados. O GroupDocs.Search pode lidar com **mais de 50 formatos de entrada** e processar **documentos com centenas de páginas** sem carregar o arquivo inteiro na memória, oferecendo respostas a consultas em menos de um segundo mesmo com o crescimento do volume de dados.

## Pré‑requisitos

- **JDK** (11 ou superior) instalado.  
- Uma IDE como IntelliJ IDEA ou Eclipse.  
- Conhecimento básico de Java, familiaridade com Maven e compreensão dos conceitos de nós de rede.  
- Uma licença válida do GroupDocs.Search (avaliação gratuita ou comercial).

## Inicialização e Configuração Básicas

Comece criando um diretório de índice:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Esta etapa simples prepara o ambiente para a configuração de rede subsequente.

## Guia de Implementação

### Recurso 1: Configuração da Rede de Busca

#### Visão Geral

Configurar a rede de busca define os caminhos de arquivos e portas que os nós usarão para se comunicar.

##### Configurar Caminhos e Portas

Configuration é uma classe que contém caminhos de rede, portas e outras configurações para o cluster de busca.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
O objeto `configuration` agora contém todas as configurações necessárias para sua rede de busca.

### Recurso 2: Implantação de Nós da Rede de Busca

#### Visão Geral

Implante nós para distribuir a carga de trabalho em sua rede. O nó mestre gerencia operações e eventos.

##### Código de Implantação

SearchNetworkNode representa um nó na rede de busca que pode atuar como mestre ou trabalhador.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Recurso 3: Inscrição em Eventos de Nó da Rede de Busca

#### Visão Geral

Escutar eventos permite o tratamento dinâmico de alterações ou atualizações em sua rede.

##### Implementação da Inscrição

SearchNetworkNodeEvents fornece ganchos de eventos para o ciclo de vida do nó e ações de indexação.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Recurso 4: Adicionando Diretórios ao Índice

#### Visão Geral

Adicionar diretórios é a etapa central que torna seus documentos pesquisáveis.

##### Adição de Documentos

`IndexingDocuments.addDirectories` adiciona caminhos de pastas ao índice para processamento.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Recurso 5: Sincronizando Shards no Nó da Rede de Busca

#### Visão Geral

A sincronização garante a consistência dos dados em todos os shards.

##### Código de Sincronização

`SynchronizeOptions` configura como os shards são sincronizados entre nós.  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### Recurso 6: Fechando Nós da Rede de Busca

#### Visão Geral

Fechar nós corretamente libera recursos e previne vazamentos de memória.

##### Fechamento do Nó

`close()` libera recursos e desliga o nó da rede de busca.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Aplicações Práticas

1. **Gerenciamento de Documentos Jurídicos** – Recupere rapidamente arquivos de casos e precedentes.  
2. **Manutenção de Registros Financeiros** – Acesse demonstrações e trilhas de auditoria em segundos.  
3. **Pesquisa Acadêmica** – Pesquise entre milhares de artigos para encontrar citações relevantes.

## Considerações de Desempenho

- **Otimizar Consultas** – Escreva consultas concisas para reduzir o tempo de resposta.  
- **Gerenciamento de Memória** – Monitore o uso do heap da JVM; considere ajuste de GC para índices grandes.  
- **Estratégia de Escala** – Adicione nós proporcionalmente ao volume de dados e carga de consultas.

## Problemas Comuns e Soluções

| Problema | Causa | Solução |
|----------|-------|----------|
| Nós falham ao conectar | Conflito de porta | Altere `basePort` para um valor não usado |
| Índice não está atualizando | Inscrição de evento ausente | Garanta que `SearchNetworkNodeEvents.subscribe(masterNode)` seja chamado |
| Alta latência | Shards insuficientes | Aumente o número de nós e balanceie a distribuição de documentos |

## Perguntas Frequentes

**Q: Qual é o principal benefício de usar o GroupDocs.Search?**  
A: Ele fornece recursos de busca rápidos e escaláveis em grandes conjuntos de documentos com configuração mínima.

**Q: Posso personalizar as configurações de nós em uma rede de busca?**  
A: Sim, você pode definir caminhos personalizados, portas e outras opções através do objeto `Configuration`.

**Q: Como adiciono diretórios ao índice após a rede estar em execução?**  
A: Chame `IndexingDocuments.addDirectories(masterNode, "path")` sempre que precisar indexar novas pastas.

**Q: Como sincronizar shards quando um novo nó entra na rede?**  
A: Use o método `synchronizeShards` mostrado acima no nó recém‑adicionado.

**Q: Preciso de uma licença para desenvolvimento?**  
A: Uma licença de avaliação gratuita é suficiente para testes; uma licença comercial é necessária para produção.

## Conclusão

Seguindo este guia, você agora sabe como **adicionar a dependência Maven do groupdocs**, configurar uma rede de busca multi‑nó, indexar diretórios e manter os shards sincronizados. Essas etapas estabelecem a base para uma solução de busca de documentos de alto desempenho que pode crescer com as necessidades da sua organização.

---

**Última Atualização:** 2026-05-17  
**Testado com:** GroupDocs.Search 25.4  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [Tutoriais e Exemplos do GroupDocs.Search para Java](/search/net/)
- [Configurando a Rede GroupDocs.Search em .NET: Um Guia Abrangente](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Como Implementar uma Rede de Busca com GroupDocs.Search em .NET para Sistemas de Gerenciamento de Documentos](/search/net/search-network/implement-search-network-groupdocs-dotnet/)