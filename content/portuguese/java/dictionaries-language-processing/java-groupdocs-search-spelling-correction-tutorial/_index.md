---
date: '2025-12-20'
description: Aprenda como habilitar a correção ortográfica em Java usando o GroupDocs.Search,
  adicionar documentos ao índice e definir a contagem máxima de erros para melhorar
  a precisão da pesquisa.
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: Como habilitar a ortografia em Java com o GroupDocs.Search
type: docs
url: /pt/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Como habilitar correção ortográfica em Java usando GroupDocs.Search

Resultados de busca precisos são essenciais para qualquer aplicação moderna. Neste tutorial você aprenderá **como habilitar a correção ortográfica** em Java com o GroupDocs.Search, para que os usuários obtenham os resultados corretos mesmo quando digitam consultas com erros. Vamos percorrer a criação de um índice, **adicionar documentos ao índice**, configurar as opções de ortografia e executar uma busca que corrige automaticamente os erros.

## Respostas rápidas
- **O que significa “como habilitar a correção ortográfica”?** Ele ativa o verificador ortográfico interno que corrige erros de digitação do usuário durante uma busca.  
- **Qual biblioteca fornece esse recurso?** GroupDocs.Search para Java.  
- **Preciso de uma licença?** Uma licença de avaliação gratuita funciona para avaliação; uma licença completa é necessária para produção.  
- **Posso controlar a tolerância?** Sim – use `setMaxMistakeCount` para definir quantos erros de digitação são permitidos.  
- **É adequado para índices grandes?** Absolutamente – o mecanismo é otimizado para indexação e busca de alto desempenho.

## O que significa “como habilitar a correção ortográfica” no GroupDocs.Search?
Habilitar a correção ortográfica indica ao motor de busca que procure os termos corretos mais próximos quando uma consulta contém erros. Esse recurso melhora drasticamente a experiência do usuário ao retornar resultados relevantes mesmo com entrada digitada incorretamente.

## Por que habilitar a correção ortográfica em aplicações Java?
- **Aumenta a satisfação do usuário** – os usuários não precisam digitar perfeitamente.  
- **Reduz as taxas de rejeição** – resultados mais precisos mantêm os visitantes engajados.  
- **Funciona em diversos domínios** – de catálogos de bibliotecas a buscas de produtos em e‑commerce.

## Prerequisites
- Java Development Kit (JDK) instalado.
- Conhecimento básico de Java e Maven.
- Compreensão dos conceitos de indexação.
- Uma licença de avaliação ou chave licenciada do GroupDocs.Search.

### Configurando o GroupDocs.Search para Java
Integre a biblioteca ao seu projeto Maven.

**Maven Setup**  
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

**Direct Download**  
Alternativamente, faça o download da versão mais recente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Aquisição de Licença
Obtenha uma licença de avaliação gratuita para testes. Para uso em produção, adquira uma licença completa ou solicite uma chave temporária no site oficial.

## Como adicionar documentos ao índice
Criar um índice é a base para qualquer aplicação com busca habilitada. Abaixo está um exemplo mínimo que **adiciona documentos ao índice** a partir de uma pasta.

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

*Dica:* Verifique se os caminhos estão corretos e se a aplicação tem permissões de escrita na pasta do índice.

## Como configurar a correção ortográfica (definir contagem máxima de erros)
Você pode ajustar finamente o verificador ortográfico habilitando‑o e definindo a tolerância para erros.

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

*Por que `setMaxMistakeCount` é importante:* Ele define quantos erros de digitação o motor tolerará. Ajuste esse valor com base nos padrões típicos de erro do seu domínio.

## Como executar uma busca com correção ortográfica
Com o índice pronto e as opções de ortografia configuradas, execute uma consulta que pode conter erros.

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

A chamada `search()` retorna um `SearchResult` que contém os termos corrigidos e os documentos mais relevantes.

## Aplicações práticas
1. **Sistemas de Bibliotecas:** Corrija títulos de livros ou nomes de autores digitados incorretamente.  
2. **Plataformas de E‑commerce:** Corrija erros de digitação dos usuários nas buscas de produtos para aumentar as conversões.  
3. **Sistemas de Gerenciamento de Conteúdo:** Melhore a recuperação de artigos para a equipe editorial.

## Considerações de desempenho
- **Mantenha o índice atualizado** – reindexe arquivos novos ou alterados regularmente.  
- **Ajuste as configurações de memória da JVM** – aloque heap suficiente para índices grandes.  
- **Monitore o uso de recursos** – ajuste as flags do coletor de lixo se necessário.

## Perguntas Frequentes

**Q: O que é o GroupDocs.Search?**  
A: É uma biblioteca Java que fornece indexação rápida, recursos avançados de busca e correção ortográfica integrada.

**Q: Como obtenho uma licença para o GroupDocs.Search?**  
A: Visite o site oficial para baixar uma avaliação gratuita ou adquirir uma licença completa.

**Q: Posso integrar o GroupDocs.Search com outros frameworks Java?**  
A: Sim, funciona com Spring, Jakarta EE e qualquer aplicação Java padrão.

**Q: Quais são os problemas comuns ao configurar um índice?**  
A: Caminhos de pasta incorretos, permissões de arquivo insuficientes ou dependências ausentes no `pom.xml`.

**Q: Como a correção ortográfica melhora os resultados de busca?**  
A: Ela reescreve automaticamente consultas com erros de digitação para os termos corretos mais próximos, retornando resultados mais relevantes.

## Recursos adicionais
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Última atualização:** 2025-12-20  
**Testado com:** GroupDocs.Search 25.4  
**Autor:** GroupDocs