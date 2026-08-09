---
date: '2026-07-02'
description: Aprenda como obter uma licença temporária para GroupDocs.Search, adicionar
  diretórios ao índice e adicionar atributos personalizados de documentos enquanto
  gerencia Java search network nodes.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Obter Licença Temporária GroupDocs – Master Search Nodes (Java)
type: docs
url: /pt/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Obter Licença Temporária GroupDocs – Nós Mestres de Busca (Java)

Neste guia abrangente você **obterá uma licença temporária para o GroupDocs.Search**, configurará uma rede de busca multi‑nó e aprenderá como **adicionar diretórios ao índice** e **adicionar atributos personalizados de documento** usando Java. Seja construindo um sistema de gerenciamento de documentos corporativo ou um catálogo de produtos pesquisável, dominar estas etapas permite avaliar a plataforma sem restrições e escalar rapidamente suas capacidades de busca.

## Respostas Rápidas
- **Qual é o primeiro passo para começar a usar o GroupDocs.Search?** Obtenha uma licença temporária no portal do GroupDocs.  
- **Qual repositório Maven hospeda a biblioteca?** `https://releases.groupdocs.com/search/java/`.  
- **Como adiciono diretórios ao índice?** Chame o helper `addDirectoriesToIndex` no nó mestre.  
- **Posso adicionar atributos personalizados de documento?** Sim—chame `addAttribute` com a chave do documento e o nome do atributo.  
- **Como encerro os nós corretamente?** Invocar `closeNodes` para liberar recursos.

## O que é uma licença temporária e por que preciso dela?
Uma licença temporária permite que você avalie o GroupDocs.Search sem quaisquer limitações de avaliação. É ideal para desenvolvimento, testes ou projetos de prova de conceito antes de comprometer-se com uma compra completa. A licença concede acesso a todos os recursos por um período limitado, permitindo que você faça benchmark de desempenho, teste pontos de integração e garanta que a solução atenda aos seus requisitos sem compromisso financeiro.

## Pré‑requisitos

Antes de começarmos, certifique‑se de que você tem os seguintes pré‑requisitos em vigor:

### Bibliotecas e Dependências Necessárias
Para trabalhar com o GroupDocs.Search para Java, inclua as dependências Maven necessárias:
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
Você também pode baixar a versão mais recente diretamente de [versões do GroupDocs.Search para Java](https://releases.groupdocs.com/search/java/).

### Configuração do Ambiente
- Certifique‑se de que tem um JDK compatível instalado (Java 8 ou posterior).  
- Configure sua IDE para suportar projetos Maven.

### Pré‑requisitos de Conhecimento
Um entendimento básico de programação Java e familiaridade com o gerenciamento de projetos Maven serão úteis. Se você for novo nesses conceitos, considere explorar recursos introdutórios para começar.

## Como obter uma licença temporária
Uma licença temporária é obtida visitando o portal do GroupDocs, preenchendo um breve formulário de solicitação e colocando o arquivo `.lic` recebido na pasta `resources` do seu projeto. Em seguida, inicialize a licença com algumas linhas de código (veja o trecho abaixo). Para o formulário de solicitação, use a página oficial: [Licença Temporária do GroupDocs](https://purchase.groupdocs.com/temporary-license/).

## Configurando o GroupDocs.Search para Java

### Informações de Instalação
Para começar a usar o GroupDocs.Search para Java em seu projeto, siga os passos Maven acima ou baixe a versão mais recente diretamente da página oficial de lançamentos.

#### Etapas de Aquisição de Licença
1. **Teste Gratuito** – Explore os recursos sem nenhum compromisso.  
2. **Licença Temporária** – Obtenha uma chave de curto prazo para testes (veja a seção acima).  
3. **Compra** – Para uso em produção, compre uma licença completa na **[Página de Compra do GroupDocs](https://purchase.groupdocs.com/)**.

### Inicialização e Configuração Básicas
Inicialize seu projeto com o GroupDocs.Search da seguinte forma:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Esta etapa de inicialização é crucial para garantir que todos os componentes funcionem perfeitamente dentro da sua rede de busca.

## Guia de Implementação
Agora, vamos dividir o processo em seções manejáveis, cada uma focando em um recurso específico de implantação e gerenciamento de nós da rede de busca.

### Recurso 1: Configuração
**Visão geral:** Configurar a configuração da sua rede de busca é o primeiro passo na implantação de nós. Esta configuração envolve especificar caminhos e portas críticos para a implantação dos nós.

#### Etapas de Implementação:
##### Etapa 1: Definir Caminho Base e Porta
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Etapa 2: Configurar a Rede de Busca
A função `configureSearchNetwork` prepara o objeto de configuração necessário para implantar nós.  
`Configuration` é uma classe que contém todas as configurações, como pasta de índice, portas de rede e papéis dos nós.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parâmetros:** O caminho base e a porta são usados para localizar recursos e estabelecer canais de comunicação.  
- **Valor de Retorno:** Um objeto `Configuration` configurado, adaptado às necessidades da sua implantação.

### Recurso 2: Implantação da Rede de Busca
**Visão geral:** Implantar nós é essencial para escalar suas capacidades de busca em diferentes ambientes ou segmentos de dados.

#### Etapas de Implementação:
##### Etapa 1: Implantar Nós
A função `deploySearchNetwork` inicializa e retorna um array de nós da rede de busca.  
`SearchNetworkNodes` representa cada instância de nó que participa do cluster de busca distribuído.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parâmetros:** Caminho base, porta e configuração são usados para determinar o ambiente de implantação.  
- **Valor de Retorno:** Um array contendo `SearchNetworkNodes` inicializados.

### Recurso 3: Inscrição em Eventos da Rede
**Visão geral:** Monitorar as atividades da sua rede de busca é crucial para manter desempenho e confiabilidade ótimos.

#### Etapas de Implementação:
##### Etapa 1: Inscrever-se em Eventos do Nó Mestre
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Objetivo:** Esta etapa garante que você seja notificado sobre eventos ou alterações significativas dentro da sua rede de busca.

### Recurso 4: Indexação de Documentos
**Visão geral:** Adicionar diretórios contendo documentos a serem indexados permite recuperação de dados eficiente em toda a sua rede.

#### Como adicionar diretórios ao índice
`addDirectoriesToIndex` é um método auxiliar que registra caminhos de pastas para indexação no nó mestre.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Objetivo:** Facilita o acesso rápido e a pesquisabilidade de todos os documentos dentro dos diretórios especificados.

### Recurso 5: Adição de Atributos a Documentos
**Visão geral:** Atributos personalizados aprimoram os metadados dos documentos, tornando as buscas mais flexíveis e informativas.

#### Como adicionar atributos personalizados a documentos
`addAttribute` adiciona um atributo de metadados personalizado a um documento especificado no índice.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parâmetros:** Especifique o nó, a chave do documento e o atributo a ser adicionado.  
- **Objetivo:** Expande a funcionalidade de busca ao enriquecer documentos com metadados adicionais.

### Recurso 6: Recuperação de Documentos Indexados
**Visão geral:** Recuperar e listar documentos indexados de forma eficiente para garantir a precisão e completude dos dados.

#### Etapas de Implementação:
##### Etapa 1: Obter Documentos Indexados
```java
getIndexedDocuments(nodes[0]);
```  
- **Objetivo:** Verifica a indexação bem‑sucedida de todos os documentos necessários dentro da sua rede de busca.

### Recurso 7: Encerramento de Nós da Rede
**Visão geral:** Encerrar corretamente os nós é crucial para o gerenciamento de recursos e prevenção de vazamentos de memória.

#### Etapas de Implementação:
##### Etapa 1: Fechar Todos os Nós
`closeNodes` encerra todos os nós de busca ativos e libera os recursos alocados.  
```java
closeNodes(nodes);
```  
- **Objetivo:** Libera os recursos ocupados por cada nó, garantindo um processo de encerramento limpo.

## Por que usar uma licença temporária para o GroupDocs.Search?
Uma licença temporária fornece **acesso total aos recursos por 30 dias** e suporta até **50.000 documentos indexados** sem limitação de desempenho. Isso permite que você faça benchmark da velocidade de indexação, latência de consultas e escalabilidade em dados reais antes de adquirir uma licença de produção. Também remove marcas d'água de avaliação, oferecendo uma representação fiel das capacidades do produto final.

## Casos de Uso Comuns
1. **Gerenciamento Corporativo de Documentos** – Indexe milhões de arquivos internos entre departamentos, permitindo busca instantânea em texto completo.  
2. **Plataformas de E‑commerce** – Crie um catálogo de produtos pesquisável que abrange múltiplos armazéns e feeds de terceiros.  
3. **Escritórios de Advocacia** – Organize arquivos de casos, contratos e evidências com metadados personalizados para recuperação rápida.

As possibilidades de integração com outros sistemas incluem plataformas CRM, sistemas de gerenciamento de conteúdo (CMS) e ferramentas de análise de dados, aproveitando os recursos robustos de indexação e busca fornecidos pelo GroupDocs.Search para Java.

## Considerações de Desempenho
Para otimizar o desempenho ao usar o GroupDocs.Search para Java:
- **Otimizar Configuração** – Ajuste as configurações para corresponder ao seu ambiente de implantação específico.  
- **Monitorar Uso de Recursos** – Verifique regularmente CPU, memória e I/O para prevenir gargalos ou vazamentos de memória.  
- **Seguir as Melhores Práticas** – Siga as diretrizes de gerenciamento de memória do Java, garantindo utilização eficiente dos recursos do sistema.

## Perguntas Frequentes

**Q: Quanto tempo uma licença temporária permanece válida?**  
A: Licenças temporárias geralmente são válidas por 30 dias, oferecendo tempo suficiente para avaliar o produto.

**Q: Posso mudar de uma licença temporária para uma licença completa sem reinstalar?**  
A: Sim—substitua o arquivo de licença temporária pelo arquivo de licença completa e reinicie sua aplicação.

**Q: Preciso re‑indexar documentos após aplicar uma nova licença?**  
A: Não, o índice permanece intacto; a licença apenas regula os direitos de uso.

**Q: O que acontece se eu esquecer de fechar os nós?**  
A: Recursos não liberados podem causar vazamentos de memória; sempre invoque `closeNodes` durante o encerramento.

**Q: É possível adicionar mais de um atributo personalizado por documento?**  
A: Absolutamente—chame `addAttribute` várias vezes com nomes de atributos diferentes.

---

**Última Atualização:** 2026-07-02  
**Testado com:** GroupDocs.Search para Java 25.4  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [Implantar um Nó de Rede de Busca em .NET usando GroupDocs para Indexação e Recuperação Eficientes de Documentos](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Como Implementar uma Rede de Busca com GroupDocs.Search em .NET para Sistemas de Gerenciamento de Documentos](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Configurando a Rede Aspose.Search & Adicionando Atributos de Documento com GroupDocs.Redaction para .NET: Um Guia Abrangente](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)