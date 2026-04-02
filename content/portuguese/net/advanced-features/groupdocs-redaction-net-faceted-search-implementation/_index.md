---
date: '2026-04-02'
description: Aprenda como criar um índice de pesquisa GroupDocs e adicionar documentos
  ao índice enquanto implementa busca facetada usando GroupDocs.Search e GroupDocs.Redaction
  em .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Criar Índice de Pesquisa GroupDocs com Redação .NET Busca Facetada
type: docs
url: /pt/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Criar Índice de Busca GroupDocs com Redação .NET Busca Facetada

Em aplicações modernas, **criar um índice de busca com GroupDocs** é essencial para recuperação rápida e precisa de documentos. Seja lidando com contratos legais, catálogos de produtos ou grandes bases de conhecimento, um índice bem‑construído permite que você **adicione documentos ao índice** e execute buscas facetadas poderosas em segundos. Este tutorial orienta todo o processo — desde a configuração do GroupDocs.Redaction até a criação de consultas facetadas simples e complexas — para que você ofereça uma experiência de busca responsiva em seus projetos .NET.

## Respostas Rápidas
- **Qual é o objetivo principal?** Criar um índice de busca com GroupDocs e habilitar busca facetada.  
- **Quais bibliotecas são necessárias?** GroupDocs.Redaction e GroupDocs.Search para .NET.  
- **Como adiciono documentos ao índice?** Use `index.Add(documentsFolder)` após inicializar o índice.  
- **Posso executar consultas complexas?** Sim, combine consultas de objeto com operadores lógicos para filtragem avançada.  
- **É necessária uma licença?** Uma avaliação gratuita funciona para desenvolvimento; uma licença comercial é exigida para produção.

## O que é busca facetada e por que usá‑la com GroupDocs?
A busca facetada permite que os usuários refinem resultados aplicando múltiplos filtros — como categoria, data ou autor — simultaneamente. Quando combinada com **GroupDocs.Redaction**, você obtém conteúdo seguro e pesquisável que respeita as regras de redação, tornando‑a ideal para ambientes com alta exigência de conformidade.

## Pré‑requisitos

### Bibliotecas Necessárias, Versões e Dependências
- **GroupDocs.Redaction .NET** – última versão estável.  
- **GroupDocs.Search .NET** – funciona em conjunto com Redaction para indexação.

### Requisitos de Configuração do Ambiente
- **IDE**: Visual Studio 2019 ou posterior.  
- **Framework**: .NET Core 3.1, .NET 5 ou .NET 6.  
- **Compatibilidade de SO**: Windows, Linux, macOS.

### Pré‑requisitos de Conhecimento
Habilidades básicas em C# e compreensão de alto nível dos conceitos de busca facetada ajudarão, mas o guia passo a passo também é amigável para iniciantes.

## Configurando GroupDocs.Redaction para .NET

### Informações de Instalação
Você pode adicionar o pacote GroupDocs.Redaction usando qualquer um dos métodos a seguir:

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Procure por "GroupDocs.Redaction" e instale a versão mais recente.

### Etapas para Aquisição de Licença
Para desbloquear todos os recursos, comece com uma avaliação gratuita ou obtenha uma licença permanente:

1. Visite [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) para explorar as opções de licenciamento.  
2. Siga as instruções na tela para receber seu arquivo de licença de avaliação ou comprado.

### Inicialização e Configuração Básicas
Depois que o pacote for instalado, inicialize o Redactor em sua aplicação:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Como criar índice de busca groupdocs

A seguir dividimos a implementação em duas partes: **Busca Facetada Simples** e **Consulta Complexa**. Cada parte mostra como **criar um índice de busca groupdocs**, adicionar documentos e executar consultas.

### Recurso 1: Busca Facetada Simples

**Visão geral**  
A busca facetada permite que os usuários restrinjam resultados selecionando múltiplos critérios. Esta seção demonstra uma abordagem direta usando GroupDocs.Search.

#### Etapa 1: Definir Pastas de Índice e Documentos
Configure os caminhos das pastas onde o índice será armazenado e onde seus documentos de origem residem.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Etapa 2: Criar um Índice
Inicialize o índice de busca na pasta que você definiu.

```csharp
Index index = new Index(indexFolder);
```

#### Etapa 3: Adicionar Documentos ao Índice
Carregue seus documentos para que se tornem pesquisáveis.

```csharp
index.Add(documentsFolder);
```

#### Etapa 4: Executar uma Busca por Consulta de Texto
Execute uma consulta de texto básica contra o campo **content**.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Etapa 5: Executar uma Busca por Consulta de Objeto
Use consultas orientadas a objeto para controle mais fino.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Recurso 2: Consulta Complexa

**Visão geral**  
Quando precisar combinar múltiplos filtros — como padrões de nome de arquivo e correspondência de frases — você pode construir uma consulta complexa usando operadores lógicos.

#### Etapa 1: Definir Pastas de Índice e Documentos
Reutilize a mesma estrutura de pastas para um cenário mais avançado.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Etapa 2: Criar um Índice e Adicionar Documentos
(Consulte as etapas 2‑3 do exemplo simples; permanecem iguais.)

#### Etapa 3: Executar Busca por Consulta de Texto
Execute uma consulta de texto composta que mistura critérios de nome de arquivo e conteúdo.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Etapa 4: Construir e Executar Consultas de Objeto
Construa a mesma lógica programaticamente.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Continue combinando frases, intervalos e operadores booleanos para atender exatamente às regras de negócio desejadas.

## Aplicações Práticas

1. **Plataformas de E‑Commerce** – Filtre produtos por categoria, preço e avaliação.  
2. **Sistemas de Gerenciamento de Documentos** – Localize contratos por autor, data ou nível de confidencialidade.  
3. **Portais de Conteúdo** – Permita que leitores aprofundem a busca por tags, tópicos e datas de publicação.

## Considerações de Desempenho

- **Atualização do Índice**: Re‑indexe regularmente arquivos novos ou atualizados para manter a busca rápida.  
- **Gerenciamento de Memória**: Libere objetos `Index` quando terminar, especialmente em conjuntos de dados grandes.  
- **Indexação Assíncrona**: Use `Task.Run` ou serviços em segundo plano para evitar travamentos da UI durante indexação pesada.

## Problemas Comuns e Soluções

| Problema | Solução |
|----------|---------|
| **Índice não encontrado** | Verifique o caminho `indexFolder` e assegure que a pasta tenha permissões de gravação. |
| **Nenhum resultado retornado** | Confirme que os campos que você consulta (ex.: `Content`, `Filename`) estão indexados. |
| **Erros de falta de memória** | Processe documentos em lotes e considere aumentar o tamanho do heap do .NET GC. |

## Perguntas Frequentes

**P: O que é busca facetada?**  
R: A busca facetada permite que os usuários refinem resultados usando múltiplos filtros independentes, como categoria, data ou autor.

**P: Como lidar com grandes volumes de dados usando GroupDocs.Search?**  
R: Use indexação incremental, processamento em lotes e operações assíncronas para manter o uso de memória baixo e o desempenho alto.

**P: Posso integrar funcionalidades do GroupDocs em aplicações .NET existentes?**  
R: Sim, as bibliotecas foram projetadas para integração perfeita com qualquer projeto .NET.

**P: Quais são alguns problemas comuns com busca facetada?**  
R: Sintaxe de consulta complexa e garantir que todos os campos relevantes estejam indexados são desafios típicos; testes adequados e manutenção do índice ajudam a mitigá‑los.

**P: Como obtenho uma licença temporária para o GroupDocs?**  
R: Visite a [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) para solicitar uma licença de avaliação que desbloqueia todas as funcionalidades durante a avaliação.

## Recursos
- **Documentação**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **Referência de API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Última atualização:** 2026-04-02  
**Testado com:** GroupDocs.Redaction 23.12 para .NET, GroupDocs.Search 23.12 para .NET  
**Autor:** GroupDocs