---
date: '2026-04-04'
description: Aprenda a pesquisar documentos jurídicos e gerenciar índices usando o
  GroupDocs.Search e a integrar a redação de registros médicos com o GroupDocs.Redaction
  em .NET.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: Pesquisar documentos legais com GroupDocs Search & Redaction para .NET
type: docs
url: /pt/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Pesquisar Documentos Legais com GroupDocs Search & Redaction em .NET

No ambiente orientado a dados de hoje, **pesquisar documentos legais** rapidamente e com segurança é um requisito crítico para qualquer organização. Seja lidando com contratos, processos judiciais ou relatórios de conformidade, o GroupDocs.Search oferece um índice rápido e escalável, enquanto o GroupDocs.Redaction garante que informações sensíveis permaneçam ocultas. Este tutorial orienta você na configuração de um índice pesquisável, na adição de documentos de várias pastas e na configuração da redação para que possa pesquisar registros médicos e outros arquivos confidenciais com segurança.

## Respostas rápidas
- **O que o GroupDocs.Search faz?** Ele cria um índice pesquisável em texto completo para uma ampla variedade de formatos de documento.  
- **Posso remover informações antes de pesquisar?** Sim – use o GroupDocs.Redaction para mascarar ou remover dados sensíveis.  
- **Como adiciono documentos ao índice?** Chame `index.Add("folderPath")` para cada pasta que você deseja incluir.  
- **Quais tipos de arquivo são suportados?** PDFs, DOCX, PPTX, TXT e muitos outros.  
- **Preciso de uma licença para produção?** Um teste temporário está disponível; uma licença permanente é necessária para uso comercial.

## Pré-requisitos
Para seguir este tutorial, certifique‑se de que você tem:
- .NET Core SDK (3.1 ou superior) instalado.
- Visual Studio Code, Visual Studio ou outra IDE que suporte .NET.
- Familiaridade básica com programação C#.

### Aquisição de Licença
Você pode começar com um teste gratuito de ambas as bibliotecas. Para uso prolongado, considere adquirir uma licença temporária ou comprar uma no [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

## Instalando os Pacotes Necessários

**Instalação do GroupDocs.Search:**  
Usando **.NET CLI**, execute:
```bash
dotnet add package GroupDocs.Search
```
Alternativamente, use o Console do Gerenciador de Pacotes no Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**Instalação do GroupDocs.Redaction:**  
- Use .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- Ou, através do Gerenciador de Pacotes:
```powershell
Install-Package GroupDocs.Redaction
```

Visite a UI do NuGet Package Manager e procure por "GroupDocs.Redaction" para instalá‑lo se preferir uma interface gráfica.

## Configurar as Configurações do Redator
Antes de começar a redigir, você pode querer ajustar o comportamento do redator (por exemplo, definir a cor da redação ou definir padrões personalizados). O trecho a seguir mostra a inicialização básica:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Dica profissional:** Ajuste `redactorSettings` para corresponder às políticas de conformidade da sua organização (por exemplo, substituir texto por caixas pretas, aplicar OCR antes da redação, etc.).

## Guia de Implementação

### Como Pesquisar Documentos Legais?
Criar um índice pesquisável é a base para a recuperação rápida de documentos legais. O GroupDocs.Search permite apontar para qualquer pasta, construir um índice e, em seguida, executar consultas complexas em milhares de arquivos.

### Como Adicionar Documentos ao Índice
Adicionar documentos é simples — basta apontar a biblioteca para os diretórios que contêm seus arquivos. Você pode adicionar várias pastas, o que é útil quando seu corpus legal está distribuído em diferentes locais.

#### Criando e Gerenciando um Índice
**Visão geral:**  
Criar um índice é o primeiro passo para operações eficientes de busca de documentos. O GroupDocs.Search permite criar um índice pesquisável em qualquer diretório de sua escolha, possibilitando a recuperação rápida de documentos.

##### Passo 1: Criar o Índice
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Explicação:* `Index` inicializa um índice de busca no diretório especificado. Certifique‑se de que o caminho reflita a estrutura de pastas do seu projeto.

##### Passo 2: Adicionar Documentos ao Índice
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Explicação:* O método `Add` escaneia a pasta fornecida e inclui todos os documentos suportados no índice. Use isso para **adicionar documentos ao índice** de múltiplas fontes, como contratos, processos ou registros médicos.

### Recuperando e Exibindo Relatórios de Indexação
**Visão geral:**  
Os relatórios de indexação fornecem insights sobre quantos documentos foram processados, contagem total de termos e tamanho de armazenamento — métricas essenciais para ajuste de desempenho.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*Explicação:* `GetIndexingReports` retorna um array de relatórios que detalham o processo de indexação, ajudando você a monitorar e otimizar o desempenho.

## Aplicações Práticas
1. **Gerenciamento de Documentos Legais:** Automatize a indexação de processos para recuperação instantânea de estatutos, memorandos e sentenças.  
2. **Sistema de Registros Médicos:** Pesquise registros de pacientes enquanto preserva a privacidade usando o GroupDocs.Redaction para mascarar PHI.  
3. **Portal Corporativo de RH:** Combine arquivos de funcionários pesquisáveis com redação para proteger dados pessoais.

## Considerações de Desempenho
- **Otimização do Tamanho do Índice:** Periodicamente elimine entradas desatualizadas e reconstrua o índice para mantê‑lo enxuto.  
- **Gerenciamento de Memória:** Aproveite o coletor de lixo do .NET; descarte objetos `Index` quando não forem mais necessários.  
- **Melhores Práticas de Escalabilidade:** Armazene o índice em armazenamento SSD rápido e considere dividir grandes corpora em múltiplos índices.

## Perguntas Frequentes

**Q: Quais são os principais usos do GroupDocs.Search?**  
A: É ideal para criar índices pesquisáveis a partir de grandes coleções de documentos, permitindo recuperação rápida de arquivos legais e médicos.

**Q: Como o GroupDocs.Redaction garante a privacidade dos dados?**  
A: Ele permite definir padrões de redação que removem ou mascaram permanentemente informações sensíveis antes que o documento seja indexado ou compartilhado.

**Q: Posso usar essas bibliotecas em um ambiente de nuvem?**  
A: Sim — ambas as bibliotecas funcionam no Azure, AWS ou em qualquer implantação .NET em contêineres com licenciamento adequado.

**Q: Quais formatos de arquivo são suportados pelo GroupDocs.Search?**  
A: PDFs, Word, Excel, PowerPoint, TXT, HTML e muitos outros formatos corporativos.

**Q: Como soluciono erros de indexação?**  
A: Verifique os caminhos das pastas, verifique as permissões de arquivos e revise a saída do console de `IndexingReport` para códigos de erro específicos.

## Recursos
- **Documentação:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **Referência da API:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Download:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Suporte Gratuito:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licença Temporária:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Última atualização:** 2026-04-04  
**Testado com:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs