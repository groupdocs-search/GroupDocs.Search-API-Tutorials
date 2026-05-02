---
date: '2026-01-21'
description: Aprenda como adicionar a dependência GroupDocs Maven, configurar e sincronizar
  uma rede de busca Java e adicionar diretórios ao índice com o GroupDocs.Search.
keywords:
- Java Search Network Configuration
- GroupDocs.Search for Java
- Document Indexing and Retrieval
title: Dependência Maven do GroupDocs – Sincronização de Rede de Busca Java
type: docs
url: /pt/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# Dependência Maven do GroupDocs: Configurando e Sincronizando Redes de Busca Java

Neste guia abrangente, você descobrirá **como adicionar a dependência Maven do GroupDocs** ao seu projeto e, em seguida, configurar uma rede de busca Java robusta usando o GroupDocs.Search. Seja lidando com documentos jurídicos, relatórios financeiros ou artigos acadêmicos, as etapas abaixo ajudarão você a indexar, buscar e manter seus shards sincronizados de forma eficiente.

## Introdução

Gerenciar e buscar em coleções massivas de documentos é um desafio diário para muitas organizações. Ao integrar a **dependência Maven do GroupDocs**, você obtém acesso a um motor de indexação poderoso que escala em múltiplos nós. Este tutorial orienta você na configuração da dependência, implantação de nós de rede, adição de diretórios ao índice e sincronização de shards para desempenho ideal.

### Respostas Rápidas
- **O que é a dependência Maven do GroupDocs?** Um artefato Maven que traz a biblioteca GroupDocs.Search para o seu projeto Java.  
- **Por que usar uma rede de busca?** Ela distribui a carga de indexação e consultas entre vários nós, melhorando velocidade e confiabilidade.  
- **Como adiciono diretórios ao índice?** Use `IndexingDocuments.addDirectories` no nó mestre.  
- **Como sincronizar shards?** Chame `SynchronizeOptions` no `Indexer` de cada nó.  
- **Preciso de licença?** Sim, uma licença de teste ou comercial é necessária para uso em produção.

## O que é a Dependência Maven do GroupDocs?

A dependência Maven do GroupDocs (`com.groupdocs:groupdocs-search`) empacota todas as classes necessárias para criar índices pesquisáveis, gerenciar nós de rede e executar consultas rápidas. Adicioná‑la ao seu `pom.xml` garante que o Maven baixe os binários corretos e as dependências transitivas.

## Como Adicionar a Dependência Maven do GroupDocs

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

Você também pode baixar o JAR diretamente do site oficial: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## Pré-requisitos

- **JDK** (11 ou superior) instalado.  
- Uma IDE como IntelliJ IDEA ou Eclipse.  
- Conhecimento básico de Java, familiaridade com Maven e compreensão dos conceitos de nós de rede.  
- Uma licença válida do GroupDocs.Search (teste gratuito ou comercial).

## Inicialização e Configuração Básicas

Comece criando um diretório de índice:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Esta etapa simples prepara o ambiente para a configuração subsequente da rede.

## Guia de Implementação

### Recurso 1: Configuração da Rede de Busca

#### Visão Geral

Configurar a rede de busca define os caminhos de arquivos e portas que os nós usarão para se comunicar.

##### Configurar Caminhos e Portas
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
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Recurso 3: Inscrição em Eventos de Nós da Rede de Busca

#### Visão Geral

Escutar eventos permite o tratamento dinâmico de alterações ou atualizações em sua rede.

##### Implementação da Inscrição
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Recurso 4: Adicionando Diretórios ao Índice

#### Visão Geral

Adicionar diretórios é a etapa central que torna seus documentos pesquisáveis.

##### Adição de Documentos
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Recurso 5: Sincronizando Shards no Nó da Rede de Busca

#### Visão Geral

A sincronização garante a consistência dos dados em todos os shards.

##### Código de Sincronização
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

Fechar os nós corretamente libera recursos e evita vazamentos de memória.

##### Fechamento do Nó
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Aplicações Práticas

1. **Gestão de Documentos Jurídicos** – Recupere rapidamente processos e precedentes.  
2. **Manutenção de Registros Financeiros** – Acesse extratos e auditorias em segundos.  
3. **Pesquisa Acadêmica** – Busque entre milhares de artigos para encontrar citações relevantes.

## Considerações de Desempenho

- **Otimizar Consultas** – Escreva consultas concisas para reduzir o tempo de resposta.  
- **Gerenciamento de Memória** – Monitore o uso de heap da JVM; considere ajustes de GC para índices grandes.  
- **Estratégia de Escala** – Adicione nós proporcionalmente ao volume de dados e à carga de consultas.

## Problemas Comuns e Soluções

| Problema | Causa | Solução |
|----------|-------|----------|
| Nós falham ao conectar | Conflito de porta | Alterar `basePort` para um valor não usado |
| Índice não está sendo atualizado | Falta de inscrição em eventos | Garantir que `SearchNetworkNodeEvents.subscribe(masterNode)` seja chamado |
| Alta latência | Shards insuficientes | Aumentar o número de nós e balancear a distribuição de documentos |

## Perguntas Frequentes

**Q: Qual é o principal benefício de usar o GroupDocs.Search?**  
A: Ele oferece capacidades de busca rápidas e escaláveis em grandes conjuntos de documentos com configuração mínima.

**Q: Posso personalizar as configurações dos nós em uma rede de busca?**  
A: Sim, você pode definir caminhos, portas e outras opções personalizadas via o objeto `Configuration`.

**Q: Como adiciono diretórios ao índice após a rede estar em execução?**  
A: Chame `IndexingDocuments.addDirectories(masterNode, "caminho")` sempre que precisar indexar novas pastas.

**Q: Como sincronizar shards quando um novo nó entra na rede?**  
A: Use o método `synchronizeShards` mostrado acima no nó recém‑adicionado.

**Q: Preciso de licença para desenvolvimento?**  
A: Uma licença de teste gratuita é suficiente para testes; uma licença comercial é necessária para produção.

## Conclusão

Seguindo este guia, você agora sabe **como adicionar a dependência Maven do GroupDocs**, configurar uma rede de busca multi‑nó, indexar diretórios e manter os shards sincronizados. Essas etapas estabelecem a base para uma solução de busca de documentos de alto desempenho que pode crescer conforme as necessidades da sua organização.

---

**Última atualização:** 2026-01-21  
**Testado com:** GroupDocs.Search 25.4  
**Autor:** GroupDocs