---
date: '2026-01-11'
description: Aprenda a criar um índice de pesquisa personalizado usando o GroupDocs.Search
  para Java, configurando caracteres regulares e mesclados para OCR avançado e pesquisa
  de imagens.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Criar índice de pesquisa personalizado com reconhecimento de caracteres – GroupDocs.Search
  Java
type: docs
url: /pt/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Criar Índice de Busca Personalizado com Reconhecimento de Caracteres usando GroupDocs.Search para Java

Em aplicações modernas que lidam com muitos documentos, **criar um índice de busca personalizado** que compreenda as nuances do seu texto — como hífens, sublinhados ou símbolos específicos de idioma — é essencial para uma recuperação rápida e precisa. Este tutorial orienta você na configuração do reconhecimento de caracteres no **GroupDocs.Search para Java**, abordando tanto caracteres regulares (letras, dígitos, sublinhados) quanto caracteres combinados (por exemplo, hífens). Ao final, você poderá adaptar um índice atenda exatamente às necessidades do seu cenário de OCR ou busca de imagens.

## Respostas Rápidas
- **O que significa “criar índice de busca personalizado”?** Significa configurar um índice para tratar símbolos específicos como letras ou caracteres combinados, em vez de ignorá‑los.  
- **Qual biblioteca é usada?** GroupDocs.Search para Java (v25.4 no momento da escrita).  
- **Preciso de uma licença?** Uma versão de avaliação gratuita funciona para desenvolvimento; uma licença paga é necessária para produção.  
- **Posso indexar PDFs e imagens?** Sim — o GroupDocs.Search suporta OCR em imagens e PDFs quando configurado corretamente.  
- **O Maven é obrigatório?** O Maven é a forma recomendada de gerenciar dependências, mas você também pode usar Gradle ou JARs manuais.  

## O que é um Índice de Busca Personalizado?
Um índice de busca personalizado permite definir como o motor de busca interpreta os caracteres. Por padrão, muitos símbolos são ignorados, o que pode levar a correspondências perdidas para itens como números de processo (`ABC-123`) ou trechos de código (`my_variable`). Ajustar o dicionário de alfabeto lhe dá controle total sobre o que o motor trata como texto pesquisável.

## Por que Configurar Caracteres Regulares e Combinados?
- **Caracteres regulares** (letras, dígitos, sublinhados) são tratados como tokens independentes, melhorando buscas de correspondência exata.  
- **Caracteres combinados** (hífens, barras) conectam palavras; configurá‑los evita a divisão indesejada de tokens, o que é crucial para referências legais, códigos de produto ou indexação de código‑fonte.  

## Pré‑requisitos
- **JDK 8** ou superior instalado.  
- **Maven** para gerenciamento de dependências.  
- Acesso à biblioteca **GroupDocs.Search para Java** (baixada via Maven ou site oficial).  

### Bibliotecas e Dependências Necessárias
Adicione o repositório e as entradas de dependência ao seu `pom.xml` (conforme mostrado abaixo). O bloco XML deve permanecer inalterado.

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

Você também pode baixar os JARs mais recentes em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Aquisição de Licença
- **Teste Gratuito** – perfeito para experimentação inicial.  
- **Licença Temporária** – útil para ciclos de desenvolvimento mais longos.  
- **Licença de Produção** – necessária para implantação comercial.  

Obtenha uma licença no portal oficial: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Inicialização Básica
O trecho abaixo mostra o código mínimo necessário para criar um índice vazio. Mantenha‑o como está; construiremos sobre ele mais tarde.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Configurando GroupDocs.Search para Java

### Instalação via Maven
A configuração Maven da seção *Pré‑requisitos* é tudo o que você precisa. Após adicioná‑la, execute `mvn clean install` para baixar os binários.

### Requisitos de Configuração do Ambiente
- Certifique‑se de que a **pasta de índice** e a **pasta de documentos** existam no disco.  
- Use caminhos absolutos ou configure sua IDE para resolver caminhos relativos corretamente.  

## Guia de Implementação

A seguir, percorremos duas funcionalidades distintas: **caracteres regulares** e **caracteres combinados**. Cada funcionalidade segue o mesmo padrão — definir caminhos, criar o índice, definir o dicionário de caracteres e, finalmente, indexar seus documentos.

### Recurso 1 – Caracteres Regulares

#### Visão geral
Caracteres regulares são tratados como tokens independentes. Isso é ideal quando você deseja que dígitos, letras e sublinhados sejam pesquisáveis exatamente como aparecem.

#### Implementação Passo a Passo

**1️⃣ Definir Caminhos**  
Defina onde o índice será armazenado e onde seus documentos de origem estão.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Criar e Configurar o Índice**  
Instancie o índice e limpe qualquer configuração de alfabeto pré‑existente.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Definir Caracteres Regulares**  
Construa um array de caracteres que inclua dígitos, letras latinas e o sublinhado.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Indexar Documentos**  
Adicione todos os arquivos da pasta de origem ao índice recém‑configurado.

```java
index.add(documentFolder);
```

### Recurso 2 – Caracteres Combinados

#### Visão geral
Caracteres combinados (como hífens) frequentemente conectam duas palavras. Marcá‑los como *combinados* indica ao motor que mantenha os tokens ao redor juntos durante a indexação.

#### Implementação Passo a Passo

**1️⃣ Definir Caminhos**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Criar e Configurar o Índice**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Definir Caracteres Combinados**  
Aqui informamos ao dicionário que o hífen deve ser tratado como um caractere combinado.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Indexar Documentos**  

```java
index.add(documentFolder);
```

## Aplicações Práticas

### Caso de Uso 1 – Gerenciamento de Documentos Legais
Arquivos legais frequentemente contêm números de processo como `2023-AB-456`. Ao configurar sublinhados e hífens, as buscas retornam correspondências exatas sem dividir o identificador.

### Caso de Uso 2 – Repositórios de Código‑Fonte
Desenvolvedores precisam buscar trechos de código onde sublinhados (`my_variable`) e hífens (`my-function`) são significativos. O reconhecimento de caracteres personalizado garante que o motor de busca respeite esses símbolos.

### Caso de Uso 3 – Conjuntos de Dados Multilíngues
Ao trabalhar com idiomas que utilizam alfabetos adicionais, você pode ampliar o conjunto de caracteres regulares para incluir esses intervalos Unicode, garantindo resultados de busca precisos entre idiomas.

## Considerações de Desempenho

- **Gerenciamento de Recursos** – Fique atento ao uso de heap; índices grandes se beneficiam de commits incrementais.  
- **Coleta de Lixo** – Libere objetos `Index` quando terminar para que a JVM recupere a memória.  
- **Otimização do Índice** – Chame periodicamente `index.optimize()` (se disponível) para compactar o índice e melhorar a velocidade das consultas.  

## Conclusão

Agora você sabe como **criar um índice de busca personalizado** que distingue entre caracteres regulares e combinados usando o GroupDocs.Search para Java. Esse controle detalhado permite que você construa soluções de busca de alto desempenho e compatíveis com OCR, adaptadas a ambientes legais, de desenvolvimento ou multilíngues.

**Próximos Passos**  
- Experimente intervalos Unicode adicionais para alfabetos não latinos.  
- Combine a configuração de caracteres com outros recursos do GroupDocs.Search, como stemming ou sinônimos.  
- Integre o índice a uma API REST para expor as funcionalidades de busca a aplicações front‑end.

## Perguntas Frequentes

**Q:** *Qual é o propósito de `CharacterType.Letter`?*  
**A:** Indica ao índice que trate os caracteres fornecidos como letras regulares, de modo que sejam tokenizados separadamente durante a indexação.

**Q:** *Posso misturar caracteres regulares e combinados no mesmo índice?*  
**A:** Sim — basta chamar `setRange` para cada tipo; o dicionário lidará com ambas as configurações simultaneamente.

**Q:** *Preciso reconstruir o índice após alterar o alfabeto?*  
**A:** Absolutamente. Alterações no dicionário de caracteres afetam a tokenização, portanto você deve re‑indexar os documentos para aplicar as novas regras.

**Q:** *Existe um limite para o número de caracteres personalizados que posso definir?*  
**A:** A biblioteca suporta todo o intervalo Unicode; o desempenho pode degradar se você adicionar um conjunto extremamente grande, portanto limite aos caracteres que realmente necessita.

**Q:** *Como isso afeta a precisão do OCR?*  
**A:** Ao alinhar o conjunto de caracteres do índice com a saída do motor OCR, você reduz falsos negativos e melhora a relevância geral da busca.

**Última Atualização:** 2026-01-11  
**Testado com:** GroupDocs.Search 25.4 para Java  
**Autor:** GroupDocs