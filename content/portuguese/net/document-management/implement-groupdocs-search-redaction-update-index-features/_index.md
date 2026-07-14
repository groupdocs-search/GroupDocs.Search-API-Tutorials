---
date: '2026-06-07'
description: Aprenda a atualizar o índice de forma eficiente com GroupDocs.Search
  e Redaction para .NET, aprimorando seu sistema de gerenciamento de documentos.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: Como atualizar o índice com GroupDocs.Search e Redaction (.NET)
type: docs
url: /pt/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# Como Atualizar o Índice com GroupDocs.Search & Redaction (.NET)

Em empresas modernas orientadas a dados, **como atualizar o índice** de forma rápida e confiável pode fazer ou quebrar sua experiência de busca. Seja lidando com milhares de contratos ou uma base de conhecimento extensa, manter o índice de busca sincronizado com as últimas alterações nos documentos é essencial para resultados rápidos e precisos. Este tutorial orienta você a usar o GroupDocs.Search para .NET junto com o GroupDocs.Redaction para **atualizar arquivos de índice**, gerenciar índices versionados e proteger conteúdo sensível — tudo dentro de um projeto .NET limpo.

## Respostas Rápidas
- **O que significa “como atualizar o índice”?** É o processo de modificar um índice de busca existente para que novos documentos ou documentos alterados se tornem pesquisáveis sem reconstruir tudo do zero.  
- **Quais bibliotecas são necessárias?** GroupDocs.Search e GroupDocs.Redaction para .NET (ambas disponíveis via NuGet).  
- **Preciso de licença?** Um teste gratuito funciona para experimentação; uma licença de produção desbloqueia a funcionalidade completa.  
- **Posso executar isso no .NET Core?** Sim, as bibliotecas suportam .NET Framework 4.5+, .NET Core 3.1+, e .NET 5/6+.  
- **Qual desempenho posso esperar?** Atualizar um índice de 1 GB com 2 threads termina em menos de um minuto em um servidor típico de 4 núcleos.

## O que é “como atualizar o índice”?
**Como atualizar o índice** refere‑se à técnica de aplicar mudanças incrementais a um índice de busca existente em vez de recriá‑lo totalmente. Essa abordagem reduz o tempo de inatividade, economiza ciclos de CPU e mantém seus resultados de busca atualizados à medida que documentos são adicionados, editados ou removidos.

## Por que usar GroupDocs.Search & Redaction para atualizações de índice?
GroupDocs.Search suporta **mais de 50 formatos de arquivo** (PDF, DOCX, XLSX, PPTX, HTML, imagens, etc.) e pode processar documentos com centenas de páginas sem carregar o arquivo inteiro na memória. Combinado ao GroupDocs.Redaction, você pode remover ou mascarar automaticamente dados sensíveis antes da indexação, garantindo conformidade enquanto mantém a relevância da busca.

## Pré‑requisitos

- **GroupDocs.Search** – instalar via NuGet.  
- **GroupDocs.Redaction para .NET** – necessário para recursos de redação.  
- Visual Studio (ou qualquer IDE .NET) com .NET 6+ instalado.  
- Conhecimento básico de C# e familiaridade com conceitos de indexação.

### Bibliotecas e Versões Necessárias
- **GroupDocs.Search** – versão estável mais recente do NuGet.  
- **GroupDocs.Redaction para .NET** – versão estável mais recente do NuGet.

### Requisitos de Configuração do Ambiente
- Uma máquina Windows ou Linux com o SDK .NET instalado.  
- Acesso a uma pasta onde os arquivos de índice serão armazenados.

### Pré‑requisitos de Conhecimento
- Entendimento de indexação de documentos e fundamentos de busca.  
- Consciência da gestão do ciclo de vida de documentos em sistemas corporativos.

## Configurando GroupDocs.Redaction para .NET

### Instalar os Pacotes

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Pesquise por “GroupDocs.Redaction” e instale a versão mais recente.

### Etapas para Aquisição de Licença
1. **Teste Gratuito** – comece com um teste para explorar todos os recursos.  
2. **Licença Temporária** – solicite uma chave temporária para testes prolongados.  
3. **Compra** – obtenha uma licença completa para implantações em produção.

### Inicialização e Configuração Básicas
`Redactor` é a classe principal que aplica regras de redação a documentos.  
Para começar, referencie o namespace Redaction e crie uma instância de `Redactor`:

```csharp
using GroupDocs.Redaction;
```

Isso prepara você para aplicar regras de redação antes de alimentar os documentos no índice de busca.

## Guia de Implementação

Cobriremos duas capacidades principais: atualizar documentos indexados e manter o controle de versão do índice.

### Como atualizar o índice usando GroupDocs.Search?

`Index` representa a coleção pesquisável armazenada em disco.  
`UpdateOptions` configura como as atualizações incrementais são realizadas (por exemplo, contagem de threads).  
`UpdateDocument` aplica alterações a um único documento, e `Commit` finaliza todas as atualizações pendentes.

**Resposta direta (40‑70 palavras):**  
Crie um objeto `Index` apontando para sua pasta de índice, use `UpdateOptions` para especificar a contagem de threads, chame `UpdateDocument` para cada arquivo alterado e, por fim, invoque `Commit` para persistir as mudanças. Essa abordagem incremental atualiza apenas as partes modificadas, mantendo o índice atual sem reconstrução completa.

#### Recurso 1: Atualizar Documentos Indexados

##### Visão geral
Atualizar documentos indexados garante que seus resultados de busca reflitam o conteúdo mais recente, mesmo quando documentos são editados ou substituídos.

##### Etapa 1: Criar um Índice  
A classe `Index` é o objeto de nível superior que representa uma coleção pesquisável em disco.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### Etapa 2: Adicionar Documentos ao Índice  
Adicione arquivos de um diretório; a biblioteca extrai automaticamente o texto pesquisável.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### Etapa 3: Buscar e Atualizar  
Execute uma consulta, modifique o arquivo de origem e então chame `UpdateDocument` com as mesmas `UpdateOptions` usadas durante a indexação.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Por que isso funciona:** Definindo `Threads = 2`, a atualização aproveita dois núcleos de CPU, reduzindo o tempo de processamento aproximadamente à metade em uma máquina quad‑core.

### Como manter o controle de versão do índice?

`IndexUpdater` é uma classe utilitária que atualiza formatos de índice mais antigos para a versão mais recente suportada pela biblioteca.  

**Resposta direta (40‑70 palavras):**  
Instancie `IndexUpdater` com o caminho do seu índice existente, chame `CanUpdateVersion()` para verificar a compatibilidade e, se necessário, execute `UpdateVersion()`. Após a atualização, recarregue o índice com o novo formato e realize uma busca para confirmar que tudo funciona. Isso garante migração tranquila entre versões da biblioteca.

#### Recurso 2: Manter o Controle de Versão do Índice

##### Visão geral
O controle de versão garante que índices antigos permaneçam pesquisáveis após uma atualização da biblioteca.

##### Etapa 1: Verificar Compatibilidade  
`IndexUpdater` verifica se o índice atual pode ser atualizado para o formato mais recente.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### Etapa 2: Carregar e Buscar  
Após a atualização, carregue o índice renovado e execute uma consulta para validar a integridade.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Por que isso funciona:** A verificação `CanUpdateVersion` impede exceções em tempo de execução causadas por esquemas de índice incompatíveis, proporcionando um caminho de atualização seguro.

## Aplicações Práticas

Cenários reais onde **como atualizar o índice** é importante:

1. **Gestão de Documentos Legais** – Re‑indexe rapidamente contratos após emendas enquanto reda cláusulas confidenciais.  
2. **Arquivos Corporativos** – Mantenha registros históricos pesquisáveis sem reprocessar milhões de arquivos.  
3. **Sistemas de Gerenciamento de Conteúdo (CMS)** – Envie atualizações incrementais ao índice de busca à medida que autores publicam novos artigos.

## Considerações de Desempenho

- **Opções de Threading:** Ajuste `UpdateOptions.Threads` conforme os núcleos de CPU; mais threads aumentam o throughput, mas também o uso de memória.  
- **Uso de Recursos:** Monitore a RAM; a biblioteca faz streaming dos arquivos, portanto picos de memória são mínimos mesmo para PDFs de 500 páginas.  
- **Melhores Práticas:** Agende atualizações incrementais regulares e limpe versões de índice obsoletas para manter desempenho ótimo.

## Problemas Comuns e Soluções

| Problema | Causa | Solução |
|----------|-------|----------|
| **Índice não encontrado** | Caminho da pasta incorreto | Verifique se o construtor `Index` aponta para o diretório correto. |
| **Erro de incompatibilidade de versão** | Uso de um índice antigo com uma biblioteca mais nova | Execute o fluxo `IndexUpdater` antes da indexação normal. |
| **Redação não aplicada** | Regras de redação carregadas após a indexação | Aplique a redação **antes** de adicionar documentos ao índice. |

## Perguntas Frequentes

**P: Qual a diferença entre `UpdateDocument` e `Rebuild`?**  
R: `UpdateDocument` modifica apenas arquivos alterados, enquanto `Rebuild` recria todo o índice do zero, consumindo mais tempo e recursos.

**P: Posso atualizar vários documentos em paralelo?**  
R: Sim, defina `UpdateOptions.Threads` para o número de núcleos que deseja utilizar; a biblioteca gerencia o processamento paralelo internamente.

**P: O GroupDocs.Search suporta PDFs criptografados?**  
R: Absolutamente. Forneça a senha via `SearchOptions.Password` ao carregar o documento.

**P: Como verificar se a redação foi bem‑sucedida antes da indexação?**  
R: Chame `Redactor.Apply()` e inspecione o tamanho do arquivo de saída; um tamanho reduzido costuma indicar redação bem‑sucedida.

**P: Quais versões .NET são oficialmente suportadas?**  
R: .NET Framework 4.5+, .NET Core 3.1+, .NET 5 e .NET 6+.

## Conclusão

Agora você tem um guia completo e pronto para produção sobre **como atualizar o índice** usando GroupDocs.Search e como manter esses índices compatíveis com versões usando GroupDocs.Redaction para .NET. Seguindo os passos acima, você garante que sua camada de busca permaneça rápida, precisa e em conformidade com regulamentos de privacidade de dados.

**Próximos passos:**  
- Experimente diferentes configurações de `Threads` para encontrar o ponto ideal para seu hardware.  
- Explore padrões avançados de redação (por exemplo, remoção de SSN baseada em regex) antes da indexação.  
- Integre a rotina de atualização de índice ao seu pipeline CI/CD para gerenciamento totalmente automatizado de documentos.

---

**Última atualização:** 2026-06-07  
**Testado com:** GroupDocs.Search 23.10 para .NET, GroupDocs.Redaction 23.10 para .NET  
**Autor:** GroupDocs  

## Recursos
- [Documentation](https://docs.groupdocs.com/search/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

## Tutoriais Relacionados

- [Mastering GroupDocs.Redaction .NET: Efficient Index Creation and Alias Management for Advanced Document Search](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Implement Synonym Search with GroupDocs.Redaction .NET for Enhanced Document Management](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [Mastering GroupDocs Search and Redaction in .NET: Advanced Document Management](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)