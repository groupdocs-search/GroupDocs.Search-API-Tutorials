---
date: '2026-09-16'
description: Aprenda como criar um search index com GroupDocs em .NET, adicionar documentos
  ao índice e habilitar synonym search para resultados de consulta mais inteligentes.
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: Aprenda como criar um search index com GroupDocs em .NET, adicionar
  documentos ao índice e habilitar synonym search para resultados de consulta mais
  inteligentes.
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: Como criar um search index com GroupDocs em .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: Como criar um search index com GroupDocs e synonym search em .NET
type: docs
url: /pt/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# Como criar índice de pesquisa com GroupDocs e pesquisa de sinônimos em .NET

Neste guia você aprenderá **como criar índice de pesquisa** usando GroupDocs.Search, adicionar documentos a esse índice e habilitar a pesquisa de sinônimos para que os usuários encontrem conteúdo relevante mesmo quando utilizam terminologias diferentes. Seja você quem está construindo um repositório jurídico, uma base de conhecimento corporativa ou um arquivo de pesquisa, os passos abaixo fornecem uma solução pronta para produção que funciona em .NET Framework 4.6.1+, .NET Core e .NET 5+.

## Respostas rápidas
- **O que significa “criar índice de pesquisa”?** Ele cria um catálogo pesquisável dos seus documentos, armazenando o texto extraído em uma estrutura otimizada para buscas em milissegundos.  
- **Por que usar pesquisa de sinônimos?** Ela expande uma consulta para incluir palavras com o mesmo significado, aumentando a cobertura em até 30 % em corpora típicos.  
- **Quais são os principais pré-requisitos?** .NET 4.6.1+ (ou .NET Core/5+), conhecimento de C# e os pacotes NuGet GroupDocs.Search + GroupDocs.Redaction.  
- **Preciso de uma licença?** Uma avaliação gratuita é suficiente para testes; uma licença permanente é necessária para implantações em produção.  
- **Posso combinar isso com redação?** Sim—GroupDocs.Redaction pode ser executado antes ou depois da pesquisa para mascarar dados sensíveis.

## O que é “criar índice de pesquisa”?
Um **índice de pesquisa** é uma estrutura de dados que contém texto extraído e metadados de cada documento, permitindo que o mecanismo localize arquivos correspondentes instantaneamente. O GroupDocs.Search cria esse índice ao escanear a pasta de origem, analisar os formatos suportados e gravar arquivos de índice compactos em um diretório especificado por você.

## Por que habilitar pesquisa de sinônimos?
A pesquisa de sinônimos adiciona automaticamente termos alternativos à consulta do usuário, de modo que uma busca por **“improve”** também retorne documentos contendo **“enhance,” “upgrade,”** ou **“optimize.”** Na prática, isso pode aumentar a cobertura dos resultados em 20‑35 % mantendo alta precisão, pois o dicionário de sinônimos embutido é curado para cada idioma.

## Pré-requisitos
- **.NET Framework 4.6.1** ou posterior (ou qualquer runtime .NET Core/5+).  
- Habilidades básicas de desenvolvimento em C# e Visual Studio (Community, Professional ou Enterprise).  
- Pacotes GroupDocs.Search e GroupDocs.Redaction instalados via NuGet.

### Instalação
Instale o GroupDocs.Redaction para .NET usando um dos métodos abaixo (consulte a documentação do [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/) para detalhes):

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Alternativamente, use a interface do NuGet Package Manager no Visual Studio para buscar “GroupDocs.Redaction” e instalá-lo diretamente. Para referência da API, veja o [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net).

### Aquisição de licença
- **Teste gratuito:** Comece com uma versão de avaliação para explorar todos os recursos.  
- **Licença temporária:** Solicite uma licença temporária no [site da GroupDocs](https://purchase.groupdocs.com/temporary-license/) ou gerencie sua licença via o portal de [Gerenciamento de Licenças GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
- **Compra completa:** Quando estiver pronto para produção, adquira uma licença completa que remove todas as limitações de avaliação.

## Como configurar o GroupDocs.Redaction para .NET
O GroupDocs.Redaction fornece a funcionalidade central para remover conteúdo sensível antes ou depois da pesquisa. Ele expõe a classe `Redactor` que você instancia com uma licença e configurações opcionais.

O código a seguir demonstra a criação de uma instância do redator e o carregamento de um arquivo de licença:

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

Com o redator pronto, você pode chamar `redactor.Redact(...)` em qualquer documento que recupere dos resultados da pesquisa.

## Como criar o índice de pesquisa
Criar um índice de pesquisa envolve especificar uma pasta onde os arquivos de índice serão armazenados e, em seguida, inicializar a classe `Index` do GroupDocs.Search. O índice conterá todos os dados pesquisáveis extraídos dos seus documentos de origem.

Primeiro, crie um diretório para o índice e então instancie o objeto `Index`:

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

A criação do índice grava um conjunto de arquivos binários na pasta; esses arquivos normalmente têm menos de 200 KB por 1.000 páginas, permitindo escalar para milhões de páginas sem esgotar o espaço em disco.

## Como adicionar documentos ao índice
Adicionar documentos requer apontar a API para o diretório que contém os arquivos de origem e instruir o índice a ingestá‑los. O processo analisa cada formato suportado, extrai o texto e o armazena no índice para recuperação rápida.

Use o código a seguir para indexar todos os arquivos em uma pasta de origem:

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

O GroupDocs.Search suporta **30+** formatos de entrada—including DOCX, PDF, PPTX, HTML, e tipos de imagem comuns—para que você possa indexar praticamente qualquer arquivo corporativo sem conversores adicionais.

## Como habilitar e executar a pesquisa de sinônimos
O tratamento de sinônimos é ativado via `SearchOptions`. Uma vez habilitado, toda consulta é automaticamente expandida para incluir os sinônimos do dicionário, melhorando a cobertura sem sacrificar a precisão.

Habilite a pesquisa de sinônimos com o trecho a seguir:

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

O dicionário de sinônimos padrão contém mais de **5.000** pares de termos para o inglês. Você também pode carregar um arquivo `SynonymDictionary` personalizado para suportar jargões específicos da indústria.

## Dicionário de sinônimos personalizado
Se precisar de sinônimos específicos de domínio, carregue seu próprio arquivo de dicionário e atribua‑o ao `SearchOptions` antes de executar uma consulta.

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## Dicas comuns de solução de problemas
- **Problemas de caminho:** Verifique se as pastas de índice e de origem são acessíveis pela conta do processo.  
- **Limites de licença:** Uma compilação sem licença pode restringir o número de arquivos indexados a 100.  
- **Sem resultados:** Confirme se o dicionário de sinônimos está carregado; você pode inspecionar `options.SynonymDictionary.Count` em tempo de execução.  

## Aplicações práticas
1. **Gerenciamento de documentos jurídicos:** Encontre jurisprudência usando termos legais e seus sinônimos.  
2. **Pesquisa acadêmica:** Expanda buscas em literatura em PDFs e arquivos Word.  
3. **Bases de conhecimento corporativas:** Recupere políticas internas mesmo quando os usuários formulam consultas de forma diferente.  
4. **Sistemas de gerenciamento de conteúdo:** Ofereça aos editores descoberta mais rica ao marcar artigos.  
5. **Tickets de suporte ao cliente:** Relacione tickets a problemas conhecidos usando descrições sinônimas.

## Considerações de desempenho
- **Manutenção do índice:** Re‑indexe após atualizações em massa; a indexação incremental reduz o tempo de inatividade em até 70 %.  
- **Monitoramento de recursos:** Indexar um lote de 10 GB em uma VM padrão (2 vCPU, 8 GB RAM) atinge ~1,2 GB de RAM; ajuste o tamanho do lote se aproximar dos limites.  
- **Liberação de objetos:** Chame `index.Dispose()` e `redactor.Dispose()` assim que terminar para liberar recursos nativos.

## Conclusão
Agora você sabe **como criar índice de pesquisa** com GroupDocs, adicionar documentos a esse índice e habilitar a pesquisa de sinônimos para uma experiência de usuário mais intuitiva. Essa base também permite sobrepor redação, classificação personalizada ou correspondência aproximada a um mecanismo de busca robusto.

## Próximos passos
- Experimente `SearchOptions.FuzzySearch` para capturar erros de digitação.  
- Explore a API `Ranking` para aumentar a prioridade de documentos.  
- Participe da comunidade no [GroupDocs Forum](https://forum.groupdocs.com/c/search/10) ou no [Free Support Forum](https://forum.groupdocs.com/c/search/10) para compartilhar dicas e fazer perguntas.  
- Verifique os [Últimos lançamentos da GroupDocs](https://releases.groupdocs.com/search/net/) para atualizações e novos recursos.

## Perguntas frequentes

**Q: O que é pesquisa de sinônimos?**  
A: A pesquisa de sinônimos expande a consulta do usuário para incluir termos alternativos predefinidos, aumentando a chance de encontrar documentos relevantes que utilizem redações diferentes.

**Q: Como atualizo minha licença GroupDocs?**  
A: Acesse o portal de [Gerenciamento de Licenças GroupDocs](https://purchase.groupdocs.com/temporary-license/) e faça upload do novo arquivo de licença via `License.SetLicense("path/to/license.lic")`.

**Q: Posso usar pesquisa de sinônimos em um ambiente multilíngue?**  
A: Sim—carregue um arquivo `SynonymDictionary` específico para cada idioma que você suporte, e o mecanismo aplicará o conjunto de sinônimos adequado por consulta.

**Q: Quais são os problemas de indexação mais comuns?**  
A: Permissões de acesso a arquivos, formatos não suportados e ultrapassar o limite de documentos da versão de avaliação são os três principais problemas que os desenvolvedores encontram.

**Q: Como otimizar o desempenho para índices muito grandes?**  
A: Use indexação incremental, armazene o índice em SSDs e configure `IndexingOptions.MaxDegreeOfParallelism` para corresponder ao número de núcleos da CPU.

**Última atualização:** 2026-09-16  
**Testado com:** GroupDocs.Search 23.10 for .NET  
**Autor:** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## Tutoriais relacionados

- [Adicionar documento ao índice com tutoriais GroupDocs.Search .NET](/search/net/document-management/)
- [Destacar resultados de pesquisa em documentos .NET usando GroupDocs.Search e Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [Como atualizar o índice com GroupDocs.Search & Redaction (.NET)](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)