---
date: '2026-10-07'
description: Aprenda como implementar pesquisas custom date format java com GroupDocs,
  cobrindo date range queries, custom patterns e performance tips.
keywords:
- custom date format java
- search documents by date
- date range query example
- optimize search performance
- configure custom date pattern
lastmod: '2026-10-07'
og_description: Tutorial Custom date format java mostra como configurar GroupDocs.Search
  para Java, executar date range queries e melhorar performance. Siga exemplos passo
  a passo.
og_image_alt: Guide illustrating custom date format java usage in GroupDocs Search
og_title: Custom date format java – guia para date range search com GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-07'
  description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  headline: Custom date format java | date range search with GroupDocs
  type: TechArticle
- description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  name: Custom date format java | date range search with GroupDocs
  steps:
  - name: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
    text: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
  - name: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
    text: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
  - name: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
    text: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
  type: HowTo
- questions:
  - answer: Text form is quick and easy but limited to the default ISO format; object‑based
      queries let you supply `Date` objects and custom formats for greater flexibility.
    question: What is the difference between text form and object‑based date queries?
  - answer: Yes, combine `daterange` clauses with logical operators like `AND` or
      `OR` to build complex queries.
    question: Can I search for multiple date ranges in a single query?
  - answer: There is a minor overhead for additional parsing, but the impact is negligible
      for typical workloads and is outweighed by the accuracy gains.
    question: Will custom date formats slow down the search?
  - answer: Absolutely. With proper indexing strategies and JVM tuning, it scales
      to millions of documents while maintaining sub‑second query response times.
    question: Is GroupDocs.Search suitable for large‑scale deployments?
  - answer: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
      for additional samples and use‑case implementations.
    question: Where can I find more Java examples?
  type: FAQPage
tags:
- custom date format
- GroupDocs.Search
- Java date handling
- document indexing
- search optimization
title: Custom date format java | date range search com GroupDocs
type: docs
url: /pt/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Formato de data personalizado java | pesquisa de intervalo de datas com GroupDocs

Buscar documentos por data é uma necessidade frequente — seja você construindo um sistema de arquivamento, uma ferramenta de relatórios financeiros ou um portal de gerenciamento de conteúdo. Neste tutorial você aprenderá **custom date format java** usando o GroupDocs.Search, cobrindo consultas de intervalo de datas, definições de padrões personalizados e dicas para **optimize search performance**. Ao final, você poderá permitir que os usuários recuperem registros que estejam dentro de qualquer intervalo de datas, independentemente do formato que utilizem.

## Respostas rápidas
- **Qual é a classe principal para indexação?** `Index` from the `com.groupdocs.search` package.  
- **Como definir um padrão de data personalizado?** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **Posso pesquisar com uma consulta de texto?** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **Quais coordenadas Maven são necessárias?** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **Preciso de uma licença para desenvolvimento?** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## O que é custom date format java?
Custom date format java informa ao GroupDocs.Search como interpretar strings de data que não seguem o padrão ISO padrão (YYYY‑MM‑DD). Ao definir seu próprio padrão — como `MM/dd/yyyy` ou `dd‑MM‑yyyy` — você permite que o mecanismo reconheça datas incorporadas em documentos que utilizam formatos regionais ou legados. Essa capacidade permite indexar e consultar datas de forma consistente em fontes heterogêneas, melhorando tanto a recall quanto a precisão para buscas centradas em datas.

## Por que usar o GroupDocs.Search para consultas de intervalo de datas?
GroupDocs.Search combina indexação de alta velocidade com construção flexível de consultas, tornando‑o ideal para cenários de intervalo de datas. O mecanismo pode localizar rapidamente documentos que contenham datas dentro de um intervalo especificado, mesmo quando essas datas aparecem em texto livre ou campos de metadados. Seu suporte nativo a múltiplos formatos de arquivo e analisadores de data personalizáveis significa que você pode lidar com coleções de documentos diversificadas sem escrever código específico para cada formato, enquanto ainda alcança tempos de resposta subsegundos em índices grandes.

## Como pesquisar documentos por data com o GroupDocs.Search
Você configurará a biblioteca, indexará uma pasta de exemplo e, em seguida, executará tanto consultas simples em forma de texto quanto consultas mais ricas baseadas em objetos. O processo começa com a criação de uma instância `Index`, configurando quaisquer formatos de data personalizados que precisar, e então invocando a API de pesquisa com uma string simples ou um `SearchQuery` estruturado. Essa abordagem permite escolher o nível de controle que corresponde aos requisitos da sua aplicação.

### Pré-requisitos
- Java 8 ou mais recente instalado.  
- Maven para gerenciamento de dependências.  
- Acesso a uma licença do GroupDocs.Search (versão de avaliação ou temporária funciona para desenvolvimento).  

### Configurando o GroupDocs.Search para Java

#### Instalação usando Maven
Add the repository and dependency to your `pom.xml`:

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
Alternativamente, você pode baixar a versão mais recente diretamente de [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Inicialização e configuração básicas
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

**Definition anchor:** A classe `Index` é o contêiner principal que armazena metadados pesquisáveis para cada arquivo que você adiciona, permitindo buscas rápidas em grandes coleções.

## Recurso 1: criando consultas de pesquisa de intervalo de datas

### Usando consulta em forma de texto
The simplest way is to embed the date range directly in the query string:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Direct answer:** Carregue seu índice, então chame `search("daterange(2022-01-01 ~~ 2022-12-31)")` para recuperar todos os documentos cuja data indexada esteja entre 1 de janeiro de 2022 e 31 de dezembro de 2022. Esta consulta de uma linha funciona imediatamente e retorna resultados ordenados por relevância.

**Explanation:** A sintaxe `daterange` espera datas no formato `YYYY‑MM‑DD`. Ela retorna todos os documentos cujas datas indexadas estejam dentro do intervalo.

### Usando objeto de consulta
Para controle programático e análise personalizada, construa um objeto `SearchQuery`. A classe `SearchQuery` representa uma consulta estruturada que pode combinar múltiplos critérios, como palavras‑chave, filtros e intervalos de datas.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Direct answer:** Construa um `SearchQuery` com `createDateRangeQuery(startDate, endDate)` onde `startDate` e `endDate` são instâncias `java.util.Date`; então passe a consulta para `index.search(query)` para obter resultados precisos que respeitam deslocamentos de fuso horário e calendários específicos de localidade.

**Definition anchor:** A classe `SearchQuery` encapsula todos os critérios de pesquisa, permitindo combinar intervalos de datas com filtros de palavras‑chave, operadores booleanos e regras de elevação.

**Explanation:** `createDateRangeQuery` permite fornecer objetos `java.util.Date`, oferecendo total flexibilidade sobre fusos horários e tratamento específico de localidade.

## Recurso 2: especificando padrões de custom date format java

### Definindo formatos de data personalizados
The `DateFormat` class tells the engine how to split and interpret a date string based on element order and separator characters. Define a `DateFormat` that matches your document’s date representation:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Direct answer:** Limpe os formatos padrão com `dateFormat.clear()`, então adicione um novo `DateFormat` construído a partir de objetos `DateFormatElement` (mês, dia, ano) e defina o separador como `/`. Depois disso, o mecanismo analisará corretamente datas escritas como `MM/dd/yyyy` durante a indexação e a consulta.

**Definition anchor:** `DateFormat` é um objeto de configuração que informa ao GroupDocs.Search como dividir e interpretar uma string de data com base na ordem dos elementos e nos caracteres separadores.

**Explanation:** Ao limpar os formatos padrão e adicionar um `DateFormat` que usa `/` como separador, o mecanismo agora entende datas escritas como `MM/dd/yyyy`. Isso é essencial para **search documents by date** em regiões que preferem a notação mês‑primeiro.

## Dicas para otimizar o desempenho da pesquisa
- **Index incrementally:** Adicione novos arquivos ao índice existente em vez de reconstruí‑lo do zero; isso reduz o uso de CPU em até 70 % para atualizações diárias.  
- **Prune stale data:** Remova periodicamente documentos que não são mais necessários; um índice enxuto melhora as taxas de acerto de cache e reduz a latência das consultas.  
- **Adjust memory settings:** Aumente o heap da JVM (`-Xmx4g` ou superior) ao trabalhar com índices maiores que 5 GB para evitar erros de falta de memória.  
- **Enable multi‑threaded indexing:** Use `IndexingOptions.setThreadCount(Runtime.getRuntime().availableProcessors())` para paralelizar o processamento de documentos e reduzir o tempo de indexação em aproximadamente o número de núcleos da CPU.

## Problemas comuns e soluções
- **Date parsing errors:** Verifique se as strings de data do documento correspondem exatamente ao padrão personalizado que você definiu; separadores incompatíveis ou zeros à esquerda ausentes causam falhas.  
- **Missing results:** Certifique‑se de que os campos indexados contenham metadados de data; se um documento possui datas apenas em parágrafos de texto livre, habilite a opção `ExtractDateMetadata` durante a indexação.  
- **Index access exceptions:** Confirme que o caminho `indexFolder` é gravável e não está bloqueado por outro processo; use uma pasta dedicada por ambiente (dev, test, prod) para evitar conflitos.

## Aplicações práticas
1. **Archival systems** – Recupere registros de um período histórico específico sem normalizar datas manualmente.  
2. **Content management** – Suporte a formatos de data regionais como `dd/MM/yyyy` para públicos europeus, melhorando a satisfação do usuário.  
3. **Financial software** – Filtre transações por trimestre fiscal ou ano rapidamente, permitindo painéis de relatórios em tempo real.

## Por que isso importa
Implementar o tratamento de **custom date format java** elimina a fricção de lidar com representações de data inconsistentes em documentos. Ele permite que você **handle multiple date formats** em um único índice, garantindo que os usuários finais obtenham resultados precisos independentemente de como as datas foram originalmente registradas. Essa flexibilidade melhora a relevância da pesquisa, reduz o esforço de pré‑processamento e encurta o tempo‑para‑valor em aplicações centradas em datas.

## Próximos passos
- Explore combinações de consultas mais avançadas usando os operadores `AND`, `OR` e `NOT`.  
- Experimente analisadores personalizados se precisar indexar metadados temporais adicionais, como timestamps incorporados em tags XML.  
- Revise o guia de ajuste de desempenho na documentação oficial para escalar sua solução para milhões de documentos e ambientes multi‑tenant.

## Perguntas frequentes

**Q: Qual é a diferença entre consultas em forma de texto e consultas baseadas em objeto?**  
A: A forma de texto é rápida e fácil, mas limitada ao formato ISO padrão; consultas baseadas em objeto permitem fornecer objetos `Date` e formatos personalizados para maior flexibilidade.

**Q: Posso pesquisar múltiplos intervalos de datas em uma única consulta?**  
A: Sim, combine cláusulas `daterange` com operadores lógicos como `AND` ou `OR` para construir consultas complexas.

**Q: Os formatos de data personalizados vão desacelerar a pesquisa?**  
A: Há uma pequena sobrecarga de análise adicional, mas o impacto é insignificante para cargas de trabalho típicas e é compensado pelos ganhos de precisão.

**Q: O GroupDocs.Search é adequado para implantações em grande escala?**  
A: Absolutamente. Com estratégias adequadas de indexação e ajuste da JVM, ele escala para milhões de documentos mantendo tempos de resposta de consulta subsegundos.

**Q: Onde posso encontrar mais exemplos em Java?**  
A: Explore o [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) para amostras adicionais e implementações de casos de uso.

**Resources**

- **Documentação:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Referência da API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **Repositório GitHub:** [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Ver no GitHub:** [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Fórum de suporte gratuito:** [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Licença temporária:** [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

**Última atualização:** 2026-10-07  
**Testado com:** GroupDocs.Search Java 25.4  
**Autor:** GroupDocs  

## Tutoriais relacionados

- [Recursos avançados de pesquisa Java do Groupdocs Search](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Biblioteca Java de Busca de Texto Completo – Otimizar Índice com GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Como adicionar documentos ao índice com Indexação de Metadados em Java usando GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)