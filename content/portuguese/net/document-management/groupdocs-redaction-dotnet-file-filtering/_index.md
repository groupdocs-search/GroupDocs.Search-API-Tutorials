---
date: '2026-04-21'
description: Aprenda a filtrar arquivos usando o GroupDocs.Redaction para .NET, incluindo
  filtragem por data de criação, tamanho do arquivo, data de modificação e como aplicar
  filtros NOT.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Como filtrar arquivos com o GroupDocs.Redaction para .NET
type: docs
url: /pt/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Como Filtrar Arquivos com GroupDocs.Redaction para .NET

No ambiente digital de hoje, que se move rapidamente, **como filtrar arquivos** de forma eficiente pode fazer ou quebrar sua produtividade. Seja isolando documentos por extensão, data de criação, tamanho ou data de modificação, uma estratégia de filtragem sólida economiza tempo, reduz custos de armazenamento e mantém seu índice de pesquisa organizado. Neste tutorial, percorreremos exemplos do mundo real usando GroupDocs.Redaction para .NET, mostrando exatamente como filtrar arquivos para atender às necessidades comerciais comuns.

## Respostas Rápidas
- **Qual biblioteca eu preciso?** GroupDocs.Redaction para .NET (instale via NuGet).  
- **Posso filtrar por data de criação?** Sim – use `CreateCreationTimeRange`.  
- **Como excluo certos tipos?** Aplique um filtro NOT com `DocumentFilter.CreateNot`.  
- **O filtro por tamanho de arquivo é suportado?** Absolutamente, via `CreateFileLengthRange` ou limites superior/inferior.  
- **Preciso de licença?** Uma licença de teste ou completa é necessária para uso em produção.

## O que é filtragem de arquivos com GroupDocs.Redaction?
A filtragem de arquivos permite que você indique ao mecanismo de indexação quais documentos incluir ou ignorar com base em metadados como extensão, datas, padrões de caminho ou tamanho. Definindo regras precisas de `DocumentFilter`, você mantém seu índice enxuto e suas buscas rápidas.

## Por que usar GroupDocs.Redaction para .NET?
- **Auxiliares de filtro integrados** – não é necessário escrever código personalizado de sistema de arquivos.  
- **Operadores lógicos** – combine múltiplos critérios com AND, OR e NOT.  
- **Otimizado para desempenho** – os filtros são aplicados durante a indexação, não depois.  
- **Multiplataforma** – funciona com .NET Framework, .NET Core e .NET 5/6+.

## Pré-requisitos
- .NET Framework 4.6+ ou .NET Core 3.1+ instalado.  
- Visual Studio ou sua IDE C# preferida.  
- Conhecimento básico de C#.

### Bibliotecas Necessárias e Configuração
Install the NuGet package using your preferred method:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Dica profissional:** Após a instalação, adicione seu arquivo de licença à raiz do projeto e chame `License.SetLicense("license-file-path")` antes de criar quaisquer objetos Redactor ou Index.

## Configurando GroupDocs.Redaction para .NET

First, create a `Redactor` instance that points to the document you want to work with:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Por que isso importa:** Inicializar o Redactor garante que a biblioteca esteja pronta para aplicar filtros e regras de redação mais adiante no fluxo de trabalho.

## Como filtrar arquivos por extensão

Filtrar por extensão de arquivo é a forma mais comum de reduzir um conjunto de documentos. Abaixo, mantemos apenas arquivos FB2, EPUB e TXT.

### Filtrar por extensão de arquivo

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Como aplicar filtro NOT para excluir tipos indesejados

Se você precisar **aplicar lógica de filtro NOT** — por exemplo, excluir arquivos HTML e PDF — use `CreateNot`.

### Excluir arquivos HTM, HTML e PDF

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Como filtrar arquivos por data de criação

Quando precisar **filtrar por data de criação**, especifique um `DateTime` de início e fim.

### Filtrar por intervalo de data de criação

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Como filtrar arquivos por data de modificação

Semelhante às datas de criação, você pode limitar os resultados a arquivos modificados antes de um determinado ponto.

### Filtrar por data de modificação

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Como filtrar arquivos por caminho usando expressões regulares

Se a estrutura de pastas segue convenções de nomenclatura, uma regex pode direcionar caminhos específicos.

### Filtrar por padrão de caminho de arquivo

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Como filtrar arquivos por tamanho

Controlar o tamanho do documento é essencial ao lidar com limites de largura de banda ou armazenamento.

### Filtrar por tamanho de arquivo (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Como combinar múltiplas condições com AND

Quando precisar **filtrar arquivos** usando vários critérios ao mesmo tempo, combine-os com `CreateAnd`.

### Exemplo de AND lógico

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Como combinar múltiplas condições com OR

Use `CreateOr` quando qualquer uma de várias regras deve ser atendida.

### Exemplo de OR lógico

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Problemas Comuns e Soluções
- **Filtro não aplicado:** Certifique-se de atribuir `settings.DocumentFilter` **antes** de criar a instância `Index`.  
- **Arquivos inesperados aparecem:** Verifique se as extensões de arquivo incluem o ponto inicial (`.txt`).  
- **Desempenho reduzido:** Combine filtros com AND para reduzir o número de arquivos escaneados no início do pipeline de indexação.  
- **Erros de regex:** Escape caracteres especiais em seu padrão de caminho ou use `RegexOptions.IgnoreCase` para correspondências sem distinção de maiúsculas/minúsculas.

## Perguntas Frequentes

**Q: Posso combinar um filtro NOT com um filtro AND?**  
A: Sim. Construa primeiro o filtro NOT (`DocumentFilter.CreateNot`) e então inclua‑o como um dos argumentos para `DocumentFilter.CreateAnd`.

**Q: Como filtro arquivos maiores que 10 MB?**  
A: Use `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` para incluir apenas arquivos que excedam esse tamanho.

**Q: É possível filtrar por datas de criação e modificação simultaneamente?**  
A: Absolutamente. Crie cada filtro separadamente e combine‑os com `CreateAnd`.

**Q: Esses filtros funcionam com caminhos de armazenamento em nuvem?**  
A: Os filtros operam no sistema de arquivos local. Para fontes na nuvem, baixe os arquivos para uma pasta temporária primeiro, então aplique os mesmos filtros.

**Q: Alterar o filtro exigirá reindexação?**  
A: Sim. Os filtros são avaliados quando você chama `index.Add`. Alterar um filtro significa que você precisa reconstruir o índice para refletir os novos critérios.

## Conclusão

Dominando **como filtrar arquivos** com GroupDocs.Redaction para .NET — seja por extensão, data de criação, data de modificação, tamanho de arquivo ou usando lógica NOT — você pode simplificar a gestão de documentos, manter os índices eficientes e focar no conteúdo que realmente importa. Experimente os operadores lógicos para adaptar a filtragem às suas regras de negócio específicas, e você verá ganhos imediatos em velocidade e eficiência de armazenamento.

---

**Última Atualização:** 2026-04-21  
**Testado com:** GroupDocs.Redaction 24.11 for .NET  
**Autor:** GroupDocs  

---