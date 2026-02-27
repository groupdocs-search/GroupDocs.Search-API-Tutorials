---
date: '2026-01-08'
description: Aprenda a configurar a pesquisa e habilitar atualizações de pesquisa
  em tempo real usando o GroupDocs.Search para Java. Guia passo a passo sobre configuração
  de rede, implantação de nós e indexação.
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 'Como Configurar a Busca com GroupDocs.Search em Java - Guia de Configuração
  e Implantação'
type: docs
url: /pt/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# Como Configurar a Busca com GroupDocs.Search em Java

No mundo digital de hoje, que se move rapidamente, **como configurar a busca** de forma eficiente pode fazer ou quebrar o sucesso de um projeto. Seja lidando com milhares de contratos, artigos de pesquisa ou relatórios internos, uma rede de busca bem projetada permite localizar o documento correto em segundos. Este tutorial orienta você na configuração de uma rede de busca, na implantação de nós e na habilitação de **atualizações de busca em tempo real** com GroupDocs.Search para Java.

## Respostas Rápidas
- **Qual é o objetivo principal de uma rede de busca?** Distribuir indexação e processamento de consultas entre vários nós para escalabilidade e velocidade.  
- **Qual versão da biblioteca é necessária?** GroupDocs.Search para Java v25.4 ou mais recente.  
- **Preciso de uma licença?** Um teste gratuito funciona para avaliação; uma licença comercial é necessária para produção.  
- **Como as atualizações em tempo real são tratadas?** Assinando eventos de nó que são disparados nas alterações de indexação.  
- **Posso adicionar novas pastas de documentos dinamicamente?** Sim—use o método `addDirectories` do indexador.

## O que é “como configurar a busca” no contexto do GroupDocs?
Configurar a busca significa criar uma **rede de busca** que sabe onde seus documentos estão, como os nós se comunicam e como a indexação é coordenada. Uma vez que a rede está configurada, você pode adicionar ou remover nós sem tempo de inatividade, garantindo acesso contínuo a resultados de busca atualizados.

## Por que usar GroupDocs.Search para Java?
- **Escalabilidade:** Distribuir cargas de trabalho entre várias máquinas.  
- **Atualizações em tempo real:** Refletir instantaneamente arquivos recém-indexados em toda a rede.  
- **Facilidade de integração:** Configuração simples com Maven e APIs Java claras.  
- **Pronto para empresas:** Lida com grandes corpora e cenários de consulta complexos.

## Pré‑requisitos
- **Java Development Kit (JDK) 8+** instalado.  
- **Maven** para gerenciamento de dependências.  
- Familiaridade básica com Java, Maven e conceitos de busca.  

## Configurando GroupDocs.Search para Java

### Dependência Maven
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

**Download direto:** Você também pode obter a biblioteca em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Aquisição de Licença
- **Teste gratuito:** Obtenha uma licença de avaliação para explorar todos os recursos.  
- **Licença temporária:** Solicite para períodos de avaliação estendidos.  
- **Licença comercial:** Necessária para implantações em produção.

### Inicialização Básica
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Como configurar a rede de busca em Java

### Etapa 1: Importar Pacotes Necessários
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### Etapa 2: Configurar a Rede
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Parâmetros:** `basePath` aponta para sua pasta de documentos; `basePort` é a porta TCP usada para comunicação entre nós.

## Implantando Nós da Rede de Busca

### Etapa 1: Importar Pacote de Implantação
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### Etapa 2: Implantar Nós
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Nó mestre:** Coordena buscas e indexação em todos os nós.

## Inscrevendo-se em Eventos de Nó para Atualizações de Busca em Tempo Real

### Etapa 1: Importar Pacote de Eventos
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### Etapa 2: Inscrever‑se em Eventos do Nó Mestre
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Manipulação de eventos:** Habilita **atualizações de busca em tempo real** sempre que documentos são adicionados, atualizados ou removidos.

## Adicionando Diretórios para Indexação

### Etapa 1: Importar Pacote do Indexador
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### Etapa 2: Adicionar Diretórios de Documentos
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Indexação dinâmica:** Adicione quantas pastas precisar; a rede as indexará automaticamente.

## Recuperando Documentos Indexados

### Etapa 1: Importar Pacote do Searcher
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### Etapa 2: Recuperar Informações do Documento
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **Gerenciamento de shards:** Lida eficientemente com grandes conjuntos de dados distribuindo documentos entre shards.

## Aplicações Práticas
1. **Gerenciamento de Documentos Corporativos:** Centralize a busca em milhões de arquivos.  
2. **Escritórios de Advocacia:** Localize rapidamente arquivos de casos, contratos e evidências.  
3. **Pesquisa Acadêmica:** Indexe periódicos e artigos para recuperação instantânea.

## Considerações de Desempenho
- **Otimizar a indexação:** Agende atualizações regulares do índice e elimine dados obsoletos.  
- **Gerenciamento de memória:** Monitore o heap da JVM, especialmente ao lidar com shards grandes.  
- **Planejamento de escalabilidade:** Adicione nós conforme seu corpus cresce; a rede balanceia a carga automaticamente.

## Problemas Comuns & Soluções

| Problema | Causa | Solução |
|----------|-------|---------|
| Nós não conseguem conectar | Conflito de porta ou firewall | Certifique-se de que `basePort` está aberto e não é usado por outros serviços |
| Índice não está atualizando | Assinatura de evento ausente | Chame `SearchNetworkNodeEvents.subscribe(masterNode)` após a implantação |
| Erros de falta de memória | Muitos shards grandes carregados | Reduza o tamanho do shard ou aumente o heap da JVM (`-Xmx` flag) |

## Perguntas Frequentes

**Q: Posso adicionar novos diretórios após a rede estar em execução?**  
A: Sim—use o método `indexer.addDirectories()`; os eventos inscritos propagarão atualizações em tempo real.

**Q: Como monitorar a saúde dos nós?**  
A: Cada `SearchNetworkNode` fornece APIs de status; integre com a ferramenta de monitoramento de sua escolha.

**Q: É possível executar o nó mestre em uma máquina separada?**  
A: Absolutamente. Apenas certifique-se de que todos os nós compartilhem o mesmo `basePort` e possam se comunicar pela rede.

**Q: Quais formatos de arquivo são suportados?**  
A: O GroupDocs.Search suporta PDFs, Word, Excel, PowerPoint, texto simples e muitos outros nativamente.

**Q: Preciso reiniciar a rede após adicionar um novo nó?**  
A: Não—os nós podem ser adicionados ou removidos dinamicamente; o nó mestre reequilibrará os shards automaticamente.

## Conclusão
Agora você tem uma compreensão completa, passo a passo, de **como configurar a busca** usando GroupDocs.Search para Java, desde a configuração inicial até atualizações em tempo real e indexação distribuída. Aplique esses padrões para construir soluções de busca de documentos rápidas, escaláveis e confiáveis para qualquer setor.

---

**Última atualização:** 2026-01-08  
**Testado com:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs