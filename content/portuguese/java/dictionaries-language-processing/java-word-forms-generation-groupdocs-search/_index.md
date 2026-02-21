---
date: '2026-02-21'
description: Aprenda como gerar formas singulares e plurais em Java usando a API GroupDocs.Search.
  Crie um provedor de formas de palavras personalizado para busca precisa e análise
  de texto.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Gerar Formas Singulares e Plurais em Java com GroupDocs.Search
type: docs
url: /pt/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

.# Gerar Formas Singular e Plural em Java com GroupDocs.Search

Se você precisa **gerar formas singular e plural em Java**, um provedor de formas de palavra personalizado é a chave para fazer seu motor de busca ou de análise de texto entender todas as variações de um termo. Neste tutorial, vamos guiá‑lo na construção de um provedor assim com a API Java do GroupDocs.Search, para que sua aplicação possa corresponder automaticamente “cat”, “cats”, “city” e “citis” sem esforço adicional.

## Respostas Rápidas
- **O que faz um provedor de formas de palavra?** Ele gera formas alternativas (singular, plural, etc.) de uma palavra fornecida para que as buscas possam corresponder a todas as variantes.  
- **Qual biblioteca é necessária?** GroupDocs.Search para Java (versão 25.4 ou mais recente).  
- **Preciso de licença?** Um teste gratuito funciona para avaliação; uma licença permanente é necessária para produção.  
- **Qual versão do Java é suportada?** JDK 8 ou superior.  
- **Quantas linhas de código são necessárias?** Cerca de 30 linhas para uma implementação simples do provedor.

## O que é o recurso “Create Word Forms Provider”?
Um componente **create word forms provider** é uma classe personalizada que implementa `IWordFormsProvider`. Ela recebe uma palavra e devolve um array de formas possíveis — singular, plural ou outras variações linguísticas — com base nas regras que você definir. Isso permite que o índice de busca trate “cat” e “cats” como equivalentes, melhorando a abrangência sem sacrificar a precisão.

## Por que usar o GroupDocs.Search para geração de formas de palavra?
- **Extensibilidade incorporada:** Conecte seu próprio provedor diretamente ao pipeline de indexação.  
- **Desempenho otimizado:** Lida com índices grandes de forma eficiente, e você pode armazenar em cache os resultados para maior velocidade.  
- **Suporte multilíngue:** Os conceitos se aplicam ao .NET e a outras plataformas também.

## Pré‑requisitos
Antes de implementar o **create word forms provider**, certifique‑se de que você tem:

- **Maven** instalado e um JDK 8 ou mais recente configurado na sua máquina.  
- Familiaridade básica com desenvolvimento Java e a configuração `pom.xml` do Maven.  
- Acesso à biblioteca GroupDocs.Search Java (versão 25.4 ou posterior).  

## Configurando o GroupDocs.Search para Java

### Configuração do Maven

Adicione o repositório e a dependência ao seu arquivo `pom.xml` exatamente como mostrado abaixo:

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

### Download Direto

Alternativamente, faça o download do JAR mais recente na página oficial de lançamentos: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Etapas para Aquisição de Licença

1. **Teste gratuito:** Inscreva‑se para um teste e explore os recursos principais.  
2. **Licença temporária:** Solicite uma chave temporária para testes prolongados.  
3. **Compra:** Obtenha uma licença comercial para uso em produção sem restrições.  

### Inicialização e Configuração Básicas

 O snippet a seguir demonstra como criar um índice—seu ponto de partida para adicionar documentos e lógica de formas de palavra:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Guia de Implementação

A seguir, percorremos as etapas para **create word forms provider** que lida com transformações simples de singular‑para‑plural e plural‑para‑singular.

### Implementando o SimpleWordFormsProvider

#### Visão geral
Nosso provedor personalizado irá:

- Remover o sufixo “es” ou “s” ao final para adivinhar a forma singular.  
- Alterar um “y” final para “is” para produzir a forma plural (ex.: “city” → “citis”).  
- Anexar “s” e “es” para gerar candidatos plurais básicos.

#### Etapa 1 – Criar o Esqueleto da Classe

Comece definindo uma classe que implementa `IWordFormsProvider`. Mantenha as declarações de importação inalteradas:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Etapa 2 – Implementar `getWordForms`

Adicione o método que constrói a lista de formas possíveis. Este bloco contém a lógica central; você pode estendê‑lo posteriormente para cobrir regras mais complexas.

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### Explicação da Lógica
- **Singularização:** Detecta sufixos plurais comuns (`es`, `s`) e os remove para aproximar a palavra base.  
- **Pluralização:** Lida com substantivos que terminam em `y` trocando‑os por `is`, uma regra simples que funciona para muitas palavras em inglês.  
- **Anexar sufixos:** Adiciona `s` e `es` para cobrir formas plurais regulares que podem não ser capturadas pelas verificações anteriores.

#### Dicas de Solução de Problemas
- **Sensibilidade a maiúsculas/minúsculas:** O método usa `toLowerCase()` para comparação, garantindo que “Cats” e “cats” se comportem da mesma forma.  
- **Casos limites:** Palavras mais curtas que o comprimento do sufixo são ignoradas para evitar retornar strings vazias.  
- **Desempenho:** Para vocabulários grandes, considere armazenar em cache os resultados em um `ConcurrentHashMap`.

## Aplicações Práticas

Implementar um **create word forms provider** pode impulsionar vários cenários reais:

1. **Motores de Busca:** Usuários que digitam “mouse” também devem encontrar documentos contendo “mice”. Um provedor pode gerar essas formas irregulares.  
2. **Ferramentas de Análise de Texto:** A extração de sentimento ou entidades torna‑se mais confiável quando todas as variantes de palavras são reconhecidas.  
3. **Sistemas de Gerenciamento de Conteúdo:** A geração automática de tags pode incluir sinônimos plurais, melhorando SEO e links internos.

## Considerações de Desempenho

Ao incorporar o provedor em um sistema de produção, tenha em mente estas dicas:

- **Cache de formas usadas frequentemente:** Armazene resultados na memória para evitar recomputar a mesma palavra repetidamente.  
- **Monitore o heap da JVM:** Índices grandes podem aumentar a pressão de memória; ajuste `-Xmx` conforme necessário.  
- **Use coleções eficientes:** `ArrayList` funciona para pequenos conjuntos, mas para milhares de formas considere `HashSet` para eliminar duplicatas rapidamente.

**Melhores Práticas**

- Mantenha a biblioteca atualizada para aproveitar correções de desempenho.  
- Perfilar o provedor com cargas de consulta realistas para identificar gargalos cedo.  

## Conclusão

Você aprendeu agora como **gerar formas singular e plural em Java** usando um `SimpleWordFormsProvider` personalizado com o GroupDocs.Search. Este componente leve pode melhorar drasticamente a relevância dos resultados de busca e a precisão da análise linguística em diversas aplicações.

**Próximos passos:**  
- Experimente regras linguísticas mais sofisticadas (plurais irregulares, stemming).  
- Integre o provedor em um pipeline de indexação e meça melhorias de recall.  
- Explore outros recursos do GroupDocs.Search, como dicionários de sinônimos e analisadores personalizados.

**Chamada à Ação:** Experimente adicionar o `SimpleWordFormsProvider` ao seu próprio projeto hoje e veja como ele enriquece sua experiência de busca!

## Seção de Perguntas Frequentes

**1. O que é o GroupDocs.Search para Java?**  
É uma biblioteca poderosa que oferece busca full‑text, indexação e recursos linguísticos—including a capacidade de conectar provedores de formas de palavra personalizados.

**2. Como funciona o SimpleWordFormsProvider?**  
Ele gera formas alternativas aplicando regras simples baseadas em sufixos (removendo “s/es”, convertendo “y” para “is” e anexando “s/es”).

**3. Posso personalizar as regras de geração de formas de palavra?**  
Absolutamente. Modifique o método `getWordForms` para incluir formas irregulares, regras específicas de localidade ou integração com dicionários externos.

**4. Quais são algumas aplicações comuns para este recurso?**  
Motores de busca, pipelines de análise de texto e plataformas CMS se beneficiam ao reconhecer variantes singular/plural.

**5. Preciso de uma licença comercial para uso em produção?**  
Sim—enquanto um teste permite explorar a API, uma licença comprada remove limites de uso e garante suporte.

---

**Última atualização:** 2026-02-21  
**Testado com:** GroupDocs.Search 25.4 (Java)  
**Autor:** GroupDocs  

---