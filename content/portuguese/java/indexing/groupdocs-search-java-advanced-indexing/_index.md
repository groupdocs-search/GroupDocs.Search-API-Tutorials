---
date: '2026-08-15'
description: Saiba como melhorar a latência de busca usando recursos avançados de
  indexação do GroupDocs.Search para Java, incluindo cancelamento, operações async,
  multithreading e personalização de metadados.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: Melhore a latência de busca com o GroupDocs.Search para Java usando
  cancelamento, asynchronous indexing, multithreading e personalização de metadados.
  Aumente o desempenho e reduza o uso de recursos.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: Melhore a latência de busca com indexação avançada no GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: Melhore a latência de busca com indexação avançada no GroupDocs
type: docs
url: /pt/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Melhorar a latência de pesquisa com indexação avançada no GroupDocs

No ambiente digital acelerado de hoje, **melhorar a latência de pesquisa** é essencial para entregar resultados instantâneos aos usuários. Seja construindo um mecanismo de busca personalizado ou aprimorando um sistema de gerenciamento de documentos existente, a estratégia de indexação correta pode reduzir drasticamente a latência, diminuir o consumo de recursos e **melhorar a latência de pesquisa** de forma geral. Neste tutorial, percorreremos os recursos mais poderosos do GroupDocs.Search para Java—cancelamento, indexação assíncrona, multithreading e personalização de metadados—para que você possa **adicionar documentos ao índice** de forma mais rápida e eficiente.

**O que você aprenderá**

- Como cancelar uma operação de indexação após um tempo especificado  
- Executar operações de indexação assíncronas e lidar com mudanças de status  
- Configurar multithreading para indexação mais rápida  
- Personalizar opções de indexação de metadados para **personalizar metadados de pesquisa**  

Vamos garantir que você tenha tudo o que precisa antes de mergulharmos no código.

## Respostas rápidas
- **O que o cancelamento faz?** Ele interrompe a indexação após um tempo limite definido, liberando CPU e memória para outras tarefas.  
- **Posso indexar documentos de forma assíncrona?** Sim – habilite com `options.setAsync(true)`.  
- **Quantas threads posso usar?** Qualquer inteiro positivo; 2‑4 threads são típicas para a maioria dos servidores.  
- **A indexação de metadados é opcional?** Absolutamente – você pode habilitar ou ajustar finamente por campo.  
- **Preciso de licença para esses recursos?** Um trial funciona para testes; uma licença completa é necessária para produção.

## Pré-requisitos

- **Biblioteca GroupDocs.Search** – versão 25.4 ou posterior.  
- **Ambiente de Desenvolvimento Java** – JDK 8 ou superior é recomendado.  
- Familiaridade básica com Java e o conceito de indexação.

### Configurando o GroupDocs.Search para Java

#### Instalação via Maven

Adicione o repositório e a dependência ao seu arquivo `pom.xml`:

`pom.xml` configuration tells Maven which GroupDocs.Search artifacts to download and include in your project.

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

#### Download direto

Alternativamente, faça o download do JAR mais recente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**Aquisição de licença** – Comece com um trial gratuito ou solicite uma licença temporária para desbloquear o conjunto completo de recursos.

### Inicialização e configuração básicas

A classe `SearchIndex` é o ponto de entrada que representa um índice pesquisável armazenado em disco ou na memória.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## O que significa “otimizar o desempenho da pesquisa” neste contexto?

Otimizar o desempenho da pesquisa significa configurar o processo de indexação de modo que ele consuma a quantidade correta de CPU, memória e tempo, ao mesmo tempo em que entrega os resultados mais relevantes instantaneamente. Ao controlar cancelamento, execução assíncrona, threading e tratamento de metadados, você influencia diretamente a rapidez com que o motor pode **adicionar documentos ao índice** e responder às consultas.

## Por que usar recursos avançados de indexação?

A indexação assíncrona e multithread mantém sua aplicação responsiva, enquanto o cancelamento impede processos descontrolados. Opções de metadados finamente ajustadas permitem expor as informações mais importantes, o que **melhora a latência de pesquisa** para os usuários finais. Além disso, esses recursos reduzem picos de CPU, diminuem a pressão de memória e permitem escalabilidade mais suave ao lidar com grandes volumes de documentos.

## Como melhorar a latência de pesquisa com indexação avançada?

Carregue sua instância `SearchIndex`, configure `IndexingOptions` com cancelamento, async e parâmetros de thread, então chame `index.add(document)` — essa combinação reduz o tempo total de indexação em até 60 % em cargas de trabalho típicas e garante que trabalhos de longa duração não bloqueiem outras operações. Você também pode ajustar limites de indexação de metadados e monitorar o progresso através dos eventos de mudança de status para garantir que o pipeline permaneça dentro dos orçamentos de desempenho.

## Guia de implementação

### Propriedade de cancelamento

**Visão geral** – Cancelar a indexação após uma duração especificada para evitar consumo excessivo de recursos.

#### Etapa 1: configurar o ambiente

Crie uma instância `SearchIndex` apontando para a pasta do seu índice.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Etapa 2: criar opções de indexação com cancelamento

`IndexingOptions` permite especificar como o motor de indexação se comporta.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Pontos principais**

- `setCancellation()` ativa o recurso.  
- `cancelAfter(int milliseconds)` define o tempo limite (3 segundos neste exemplo).

### Propriedade assíncrona

**Visão geral** – Executar a indexação em uma thread em segundo plano e ouvir mudanças de status.

#### Etapa 1: configurar o ambiente

Instancie o índice e prepare a coleção de documentos.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Etapa 2: inscrever-se no evento de mudança de status

O evento `StatusChanged` notifica quando o trabalho de indexação muda de estado.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Etapa 3: configurar opções assíncronas

Habilite o modo async para que a chamada retorne imediatamente e o processamento continue em segundo plano.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Propriedade de threads

**Visão geral** – Acelerar a indexação aproveitando múltiplos núcleos de CPU.

#### Etapa 1: configurar o ambiente

Prepare o índice e assegure que a JVM tenha memória heap suficiente.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Etapa 2: configurar multithreading

Defina o número de threads de trabalho; cada thread processa um subconjunto de documentos.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Propriedade de opções de indexação de metadados

**Visão geral** – Ajustar finamente quais metadados de documento são indexados e como são armazenados.

#### Etapa 1: configurar o ambiente

Carregue um documento que contenha campos de metadados como autor, título e tags personalizadas.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Etapa 2: configurar opções de metadados

`MetadataIndexingOptions` permite habilitar ou desabilitar campos individuais de metadados e definir limites de tamanho.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Aplicações práticas

1. **Sistemas de gerenciamento de documentos** – Use indexação assíncrona para manter a UI responsiva enquanto grandes lotes são processados em segundo plano.  
2. **Mecanismos de busca de conteúdo** – Aplique cancelamento para impedir que trabalhos longos consumam recursos do servidor durante picos de tráfego.  
3. **Pipelines de ingestão em larga escala** – Aproveite o multithreading para **adicionar documentos ao índice** em escala, reduzindo drasticamente o tempo de processamento.  

## Considerações de desempenho

- **Gerenciamento de threads** – Monitore o uso de CPU; muitas threads podem causar sobrecarga de troca de contexto.  
- **Pegada de memória** – Limites de metadados (ex.: `setMaxBytesToIndexField`) mantêm o uso de memória previsível.  
- **Coleta de lixo** – Use flags adequadas da JVM (`-Xmx`, `-XX:+UseG1GC`) ao indexar corpora massivos.  

## Problemas comuns e soluções

| Sintoma | Causa provável | Solução |
|---------|----------------|---------|
| Indexação nunca termina | Cancelamento definido muito baixo | Aumente o valor de `cancelAfter` ou remova o cancelamento para trabalhos longos |
| Nenhuma atualização de status no modo async | Manipulador de evento não anexado corretamente | Garanta que `index.getEvents().StatusChanged.add(...)` seja chamado antes de `index.add` |
| Erros de falta de memória | Muitas threads ou limites altos de metadados | Reduza `options.setThreads` e diminua os limites de campos de metadados |
| Metadados ausentes nos resultados | Indexação de metadados desabilitada | Verifique se `options.getMetadataIndexingOptions()` está configurado e não definido para ignorar campos |

## Perguntas frequentes

**P: Como obtenho uma licença temporária para o GroupDocs.Search?**  
R: Visite a [página de licença temporária da GroupDocs](https://purchase.groupdocs.com/temporary-license/) e siga as instruções na tela.

**P: Posso cancelar uma operação de indexação no meio do processo?**  
R: Sim – use a propriedade de cancelamento com `cancelAfter()` ou invoque `Cancellation.cancel()` programaticamente.

**P: Quais são alguns casos de uso para indexação assíncrona?**  
R: Recuperação de documentos em tempo real, processamento de lotes em segundo plano e aplicações com UI responsiva se beneficiam da indexação assíncrona.

**P: É seguro aumentar a contagem de threads em um servidor compartilhado?**  
R: Aumente gradualmente e monitore a carga de CPU; em ambientes altamente compartilhados, mantenha a contagem de threads modesta (2‑4).

**P: Como a indexação de metadados afeta a relevância da pesquisa?**  
R: Metadados indexados corretamente (autor, data de criação, tags) podem receber peso maior nas consultas, melhorando a precisão dos resultados.

## Conclusão

Ao adotar esses recursos avançados do GroupDocs.Search para Java, você **melhorará a latência de pesquisa** em diversos cenários—from ingestão rápida de documentos até controle granular de metadados. Experimente diferentes configurações, monitore o uso de recursos e ajuste as definições ao seu workload específico para obter os melhores resultados.

---

**Última atualização:** 2026-08-15  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Tutoriais relacionados

- [Melhorar o desempenho de consultas com GroupDocs.Search Java: Otimizar Índice & Busca](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Como adicionar documentos ao índice com Indexação de Metadados em Java usando GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Como adicionar múltiplos aliases e adicionar documentos ao índice no GroupDocs.Search para Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)