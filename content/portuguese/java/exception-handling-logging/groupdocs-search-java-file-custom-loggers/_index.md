---
date: '2026-09-21'
description: Aprenda como criar logger, definir o tamanho máximo do log e usar o logger
  de console no GroupDocs.Search para Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Aprenda como criar logger, definir o tamanho máximo do log e usar
  o logger de console no GroupDocs.Search para Java. Siga instruções passo a passo
  e dicas de boas práticas.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Como criar logger e limitar o tamanho do log no GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: Como criar logger e limitar o tamanho do log no GroupDocs.Search para Java
type: docs
url: /pt/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Como criar logger e limitar o tamanho do arquivo de log no GroupDocs.Search para Java

Neste tutorial você **como criar logger** implementações para GroupDocs.Search, configurará um tamanho máximo de arquivo de log e alternará entre registro baseado em arquivo e console. O gerenciamento adequado de logs evita que os discos fiquem cheios durante grandes trabalhos de indexação, melhora a solução de problemas e fornece feedback instantâneo ao desenvolver. Começaremos com a configuração do Maven, percorreremos a configuração do logger e finalizaremos com uma consulta de pesquisa simples que demonstra o logger em ação.

## Respostas rápidas
- **O que significa “limit log file size”?** Limita o tamanho máximo de um arquivo de log, evitando crescimento descontrolado no disco.  
- **Qual logger permite limitar o tamanho do arquivo de log?** O `FileLogger` embutido aceita um parâmetro de tamanho máximo.  
- **Como usar console logger java?** Instancie `ConsoleLogger` e defina‑o em `IndexSettings`.  
- **Preciso de uma licença para o GroupDocs.Search?** Uma versão de avaliação funciona para avaliação; uma licença comercial é necessária para produção.  
- **Qual é o primeiro passo?** Adicione a dependência do GroupDocs.Search ao seu projeto Maven.  

## O que é limitar o tamanho do arquivo de log?
A configuração **limit log file size** indica ao logger que pare de gravar novas entradas quando o arquivo atingir um limite definido (por exemplo, 4 MB). Quando o limite é atingido, o logger descarta mensagens adicionais ou cria um novo arquivo, mantendo o uso de disco previsível.

## Por que usar loggers de arquivo e personalizados com GroupDocs.Search?
Loggers de arquivo e personalizados oferecem auditabilidade, insight de depuração e flexibilidade. Em ambientes de produção, logs de arquivo fornecem um registro permanente de cada operação de indexação e pesquisa, enquanto logs de console entregam feedback instantâneo durante o desenvolvimento. Esses logs ajudam as equipes a monitorar desempenho, rastrear erros e atender a requisitos de conformidade ao preservar um registro detalhado de atividades.

## Pré-requisitos
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 ou superior, com uma IDE como IntelliJ IDEA ou Eclipse.  
- Familiaridade básica com Maven e programação Java.  

## Configurando o GroupDocs.Search para Java

Adicione a biblioteca ao seu projeto usando um dos métodos abaixo.

**Configuração Maven:**  

```text
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
```

**Download direto:**  
Baixe o JAR mais recente no site oficial: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Aquisição de licença
Obtenha uma avaliação ou compre uma licença através da [página de licenciamento](https://purchase.groupdocs.com/temporary-license/).

## Como criar logger personalizado para GroupDocs.Search
Criar um logger personalizado é simples porque o GroupDocs.Search depende da interface `ILogger`. Ao implementar essa interface — ou estender o `FileLogger` ou `ConsoleLogger` fornecidos — você pode injetar comportamentos adicionais, como encaminhamento remoto ou rotação de logs. Também pode adicionar lógica de inicialização, como abrir conexões de rede, e garantir que os recursos sejam fechados no método de desligamento do logger. Essa abordagem permite integrar com plataformas de monitoramento como ELK ou Splunk.

### Âncora de definição
`ILogger` é o contrato central de logging no GroupDocs.Search; qualquer classe que implemente seu método `log(Level, String)` pode se tornar um logger.

### Exemplo de abordagem (sem bloco de código)
1. Crie uma classe que implemente `ILogger`.  
2. Substitua o método `log` para escrever mensagens no destino escolhido (arquivo, banco de dados, endpoint HTTP).  
3. Na configuração do índice, chame `settings.setLogger(new YourCustomLogger())`.  

## Como limitar o tamanho do arquivo de log com File Logger
A classe `FileLogger` grava entradas de log em um arquivo no disco e aceita um argumento de tamanho máximo. Ao especificar o limite de tamanho, o logger automaticamente para de adicionar novas entradas ou cria um novo arquivo quando o limite é atingido, evitando crescimento descontrolado do disco. Esse comportamento garante que o logging não interfira no desempenho da indexação enquanto mantém um registro conciso dos eventos.

### Âncora de definição
`FileLogger` é um logger embutido que persiste mensagens em um arquivo de texto e suporta um tamanho máximo de arquivo configurável.

### Guia passo a passo
1️⃣ **Importar pacotes necessários**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Configurar as configurações do índice com File Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **Criar ou carregar o índice**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Adicionar documentos ao índice**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Executar uma consulta de pesquisa**  
```text
```java
SearchResult result = index.search(query);
```
```

**Ponto chave:** O segundo argumento do construtor `FileLogger` (`4.0`) define o **set max log size** em megabytes, atendendo diretamente ao requisito de **limit log file size**.

## Como usar console logger java
Quando você precisa de visibilidade instantânea dos eventos de log, o `ConsoleLogger` grava cada mensagem em `System.out`. Esse logger é leve e thread‑safe, tornando‑o adequado para sessões de desenvolvimento e depuração. Ele fornece feedback imediato sobre o progresso da indexação, consultas de pesquisa e condições de erro sem exigir I/O de arquivo, o que pode acelerar testes iterativos.

### Âncora de definição
`ConsoleLogger` é um logger leve que envia entradas de log para o fluxo padrão do console, tornando‑o ideal para sessões de depuração.

### Etapas de configuração
1️⃣ **Importar o console logger**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Configurar as configurações do índice com Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Criar ou carregar o índice**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Adicionar documentos e executar uma pesquisa**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Dica:** O console logger é ideal durante o desenvolvimento porque imprime cada entrada de log instantaneamente, ajudando a verificar se a indexação e a pesquisa se comportam como esperado.

## Aplicações práticas
1. **Sistemas de gerenciamento de documentos:** Manter trilhas de auditoria de cada documento indexado, atendendo aos requisitos de conformidade.  
2. **Motores de busca corporativos:** Monitorar o desempenho de consultas e taxas de erro em tempo real, permitindo verificações rápidas de conformidade com SLA.  
3. **Software jurídico e de conformidade:** Registrar termos de pesquisa e timestamps para relatórios regulatórios, com logs mantidos pelo período de retenção exigido.

## Considerações de desempenho
- **Tamanho do log:** Ao **set max log size**, você evita uso excessivo de disco que poderia desacelerar o coletor de lixo da JVM.  
- **Logging assíncrono:** Para cenários de alto volume, envolva seu logger em uma fila assíncrona para desacoplar I/O da thread de indexação (implementação fora do escopo deste guia).  
- **Gerenciamento de memória:** Libere objetos `Index` grandes com `index.close()` quando não forem mais necessários para manter a pegada da JVM baixa.

## Problemas comuns e soluções
- **Caminho do log inacessível:** Verifique se o diretório existe e se a aplicação tem permissões de gravação para a conta de usuário que executa a JVM.  
- **Logger não disparando:** Certifique‑se de chamar `settings.setLogger(...)` *antes* de criar o objeto `Index`; caso contrário, o logger padrão será usado.  
- **Saída do console ausente:** Confirme que está executando a aplicação em um terminal que exibe `System.out`, e que nenhum framework de logging (por exemplo, SLF4J) está interceptando a saída.

## Perguntas frequentes

**Q: O que controla o segundo parâmetro do `FileLogger`?**  
A: Ele define o tamanho máximo do arquivo de log em megabytes, permitindo que você **set max log size** e evite crescimento descontrolado.

**Q: Posso combinar loggers de arquivo e console?**  
A: Sim. Crie um logger personalizado que encaminhe cada chamada `log` tanto para um `FileLogger` quanto para um `ConsoleLogger`, e registre esse logger composto em `IndexSettings`.

**Q: Como adiciono documentos ao índice após a criação inicial?**  
A: Chame `index.add(pathToNewDocs)` a qualquer momento; o logger configurado registrará automaticamente a adição.

**Q: O `ConsoleLogger` é thread‑safe?**  
A: Ele grava diretamente em `System.out`, que a JVM sincroniza internamente, tornando‑o seguro para casos de uso multi‑thread típicos.

**Q: Limitar o tamanho do arquivo de log afetará a quantidade de informações armazenadas?**  
A: Quando o limite de tamanho é atingido, novas entradas são descartadas ou o logger cria um novo arquivo, dependendo da implementação escolhida.

## Recursos
- [Documentação](https://docs.groupdocs.com/search/java/)
- [Referência da API](https://reference.groupdocs.com/search/java/)

---

**Última atualização:** 2026-09-21  
**Testado com:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs  

---

## Tutoriais Relacionados

- [Como implementar logging - Tutoriais de tratamento de exceções e logging para GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Implementar logging assíncrono em Java com GroupDocs.Search – Guia de Logger Personalizado](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Criar índice de pesquisa Java – Tutoriais GroupDocs.Search](/search/java/indexing/)