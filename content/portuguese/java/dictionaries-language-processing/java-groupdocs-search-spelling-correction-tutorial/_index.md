---
date: '2026-09-02'
description: Aprenda a criar índice de pesquisa java e ativar correção ortográfica
  usando GroupDocs.Search. Siga instruções passo a passo para adicionar documentos,
  configurar a contagem máxima de erros e melhorar a precisão da pesquisa.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: Aprenda a criar índice de pesquisa java e ativar correção ortográfica
  usando GroupDocs.Search. Siga instruções passo a passo para adicionar documentos,
  configurar a contagem máxima de erros e melhorar a precisão da pesquisa.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: Como criar índice de pesquisa java e ativar correção ortográfica
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: Como criar índice de pesquisa java e ativar correção ortográfica
type: docs
url: /pt/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Como criar índice de pesquisa Java e habilitar correção ortográfica

Em aplicações Java modernas, fornecer resultados de pesquisa precisos é um recurso indispensável. Este tutorial mostra **como criar índice de pesquisa Java** e ativar a correção ortográfica com o GroupDocs.Search, para que os usuários recebam resultados relevantes mesmo quando digitam consultas com erros. Você verá como configurar a biblioteca, adicionar documentos, definir a contagem máxima de erros e executar uma pesquisa tolerante a erros de digitação — tudo sem escrever uma única linha de código de configuração adicional.

## Respostas rápidas
- **O que faz “habilitar correção ortográfica”?** Ele ativa o verificador ortográfico embutido que reescreve termos digitados incorretamente para suas formas corretas mais próximas durante uma pesquisa.  
- **Qual biblioteca fornece esse recurso?** GroupDocs.Search para Java.  
- **Preciso de uma licença?** Uma avaliação gratuita funciona para testes; uma licença completa é necessária para uso em produção.  
- **Posso controlar a tolerância?** Sim – use `setMaxMistakeCount` para definir quantos erros de digitação são permitidos por consulta.  
- **É adequado para índices grandes?** Absolutamente – o mecanismo lida com índices contendo milhões de registros, mantendo a latência de consulta abaixo de 100 ms em hardware de servidor típico.

## O que é o GroupDocs.Search?
GroupDocs.Search é uma biblioteca Java que oferece indexação rápida de texto completo e recursos avançados de pesquisa, incluindo correção ortográfica embutida. Ela suporta mais de 50 formatos de entrada e pode processar documentos com centenas de páginas sem carregar o arquivo inteiro na memória.

## Por que habilitar a correção ortográfica em aplicações Java?
- **Aumenta a satisfação do usuário** – os visitantes obtêm resultados corretos mesmo com digitação imperfeita.  
- **Reduz as taxas de rejeição** – resultados precisos mantêm os usuários engajados por mais tempo.  
- **Funciona em diversos domínios** – de catálogos de bibliotecas a buscas de produtos em e‑commerce, a correção ortográfica melhora a relevância em todos os lugares.

## Pré-requisitos
- Java Development Kit (JDK) instalado.  
- Conhecimento básico de Java e Maven.  
- Compreensão dos conceitos de indexação.  
- Uma avaliação ou chave licenciada do GroupDocs.Search.

### Configurando o GroupDocs.Search para Java
Integre a biblioteca ao seu projeto Maven.

**Configuração Maven**  
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

**Download direto**  
Alternativamente, faça o download da versão mais recente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Aquisição de licença
Obtenha uma licença de avaliação gratuita para testes. Para uso em produção, adquira uma licença completa ou solicite uma chave temporária no site oficial.

## Como criar um índice de pesquisa em Java?
`SearchIndex` é a classe principal que representa um índice pesquisável armazenado em disco.  
Crie uma instância de `SearchIndex` apontando para uma pasta no disco, então adicione documentos de um diretório de origem. O mecanismo constrói um índice invertido que possibilita buscas rápidas. Você pode chamar `index.add()` para cada arquivo; a biblioteca extrai o texto automaticamente com base no tipo de arquivo.

## Como habilitar a correção ortográfica?
`getSpellingOptions()` retorna o objeto de configuração de ortografia para o índice, permitindo habilitar ou ajustar os recursos de verificação ortográfica.  
Habilite a correção chamando `index.getSpellingOptions().setEnabled(true)`. Isso indica ao mecanismo que ele deve analisar os termos da consulta e sugerir alternativas corrigidas quando forem detectadas divergências. O recurso funciona imediatamente para todos os idiomas indexados suportados pela biblioteca.

## O que é a configuração de contagem máxima de erros?
`setMaxMistakeCount` configura o número máximo de edições de caracteres que o verificador ortográfico tolerará por termo.  
`setMaxMistakeCount(int)` define o número máximo de edições de caracteres (inserções, exclusões, substituições) que o verificador ortográfico tolerará por termo. Definir como **2** permite que o mecanismo corrija erros comuns de dois caracteres, evitando correções excessivamente agressivas que poderiam retornar resultados não relacionados.

## Como executar uma pesquisa com correção ortográfica
`search()` executa uma consulta contra o índice e retorna um objeto `SearchResult` contendo correspondências e quaisquer termos corrigidos.  
Execute uma consulta de pesquisa usando o método `search()`. Se a consulta contiver palavras digitadas incorretamente, o mecanismo retornará um `SearchResult` que inclui os termos corrigidos e uma lista dos documentos mais relevantes. Você pode exibir tanto a consulta original quanto a versão corrigida ao usuário para transparência.  
`SearchResult` contém a lista de documentos correspondentes e informações sobre as correções da consulta.

## Aplicações práticas
1. **Sistemas de bibliotecas** – corrige automaticamente títulos de livros ou nomes de autores digitados incorretamente.  
2. **Plataformas de e‑commerce** – corrige erros de digitação em nomes de produtos para aumentar as taxas de conversão.  
3. **Gestão de conteúdo** – ajuda a equipe editorial a localizar artigos mesmo com palavras‑chave imperfeitas.

## Considerações de desempenho
- **Mantenha o índice atualizado** – re‑indexe arquivos novos ou modificados regularmente.  
- **Ajuste as configurações de memória da JVM** – aloque heap suficiente para índices grandes (por exemplo, `-Xmx4g`).  
- **Monitore o uso de recursos** – ajuste as flags do coletor de lixo se notar pausas durante a indexação em massa.

## Problemas comuns e solução de problemas
| Sintoma | Causa provável | Correção |
|---------|----------------|----------|
| Nenhum resultado após habilitar a correção ortográfica | O caminho da pasta do índice está errado ou vazio | Verifique se `indexFolder` aponta para um índice válido e se `index.add()` foi bem‑sucedido |
| O verificador ortográfico não corrige erros óbvios | `setMaxMistakeCount` está definido muito baixo | Aumente a contagem para 2 ou 3 para uma correção mais tolerante |
| Aplicação falha em conjuntos de documentos grandes | Heap da JVM insuficiente | Aumente a opção `-Xmx` (por exemplo, `-Xmx4g`) |

## Perguntas frequentes

**Q: O que é o GroupDocs.Search?**  
A: GroupDocs.Search é uma biblioteca Java que fornece indexação rápida, recursos avançados de consulta e correção ortográfica embutida para qualquer aplicação Java.

**Q: Como obtenho uma licença para o GroupDocs.Search?**  
A: Visite o site oficial para baixar uma avaliação gratuita ou adquirir uma licença completa; uma chave temporária também está disponível para testes de curto prazo.

**Q: Posso integrar o GroupDocs.Search com outros frameworks Java?**  
A: Sim, ele funciona perfeitamente com Spring, Jakarta EE e qualquer aplicação Java padrão.

**Q: Quais são os problemas comuns ao configurar um índice?**  
A: Caminhos de pastas incorretos, permissões de arquivo ausentes ou dependências Maven faltantes são os culpados típicos.

**Q: Como a correção ortográfica melhora os resultados de pesquisa?**  
A: Ela reescreve automaticamente consultas digitadas incorretamente para seus termos corretos mais próximos, retornando resultados mais relevantes e reduzindo a frustração do usuário.

## Recursos adicionais
- [Documentação](https://docs.groupdocs.com/search/java/)
- [Referência da API](https://reference.groupdocs.com/search/java)
- [Download](https://releases.groupdocs.com/search/java/)
- [Repositório no GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Fórum de Suporte Gratuito](https://forum.groupdocs.com/c/search/10)
- [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)

---

**Última atualização:** 2026-09-02  
**Testado com:** GroupDocs.Search 25.4  
**Autor:** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## Tutoriais Relacionados

- [Como criar índice de documento e adicionar documentos usando a API GroupDocs.Search para Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Processamento de linguagem Java – Criar dicionário de sinônimos com GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Palavras‑stop na pesquisa: adicionar documentos ao índice com GroupDocs.Search Java](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)