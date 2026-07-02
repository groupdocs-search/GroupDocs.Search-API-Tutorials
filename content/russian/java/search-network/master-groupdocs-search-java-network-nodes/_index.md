---
date: '2026-07-02'
description: Узнайте, как получить временную лицензию для GroupDocs.Search, добавить
  каталоги в индекс и добавить пользовательские атрибуты документов, управляя узлами
  поисковой сети Java.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Получить временную лицензию GroupDocs – Master Search Nodes (Java)
type: docs
url: /ru/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Получение временной лицензии GroupDocs – Главные узлы поиска (Java)

В этом всестороннем руководстве вы **получите временную лицензию для GroupDocs.Search**, настроите многопользовательскую поисковую сеть и узнаете, как **добавлять каталоги в индекс** и **добавлять пользовательские атрибуты документов** с помощью Java. Независимо от того, создаёте ли вы корпоративную систему управления документами или поисковый каталог товаров, освоив эти шаги, вы сможете оценить платформу без ограничений и быстро масштабировать возможности поиска.

## Быстрые ответы
- **Какой первый шаг для начала использования GroupDocs.Search?** Получите временную лицензию на портале GroupDocs.  
- **В каком Maven‑репозитории находится библиотека?** `https://releases.groupdocs.com/search/java/`.  
- **Как добавить каталоги в индекс?** Вызовите вспомогательный метод `addDirectoriesToIndex` на главном узле.  
- **Можно ли добавить пользовательские атрибуты документа?** Да — вызовите `addAttribute`, передав ключ документа и имя атрибута.  
- **Как корректно завершить работу узлов?** Вызовите `closeNodes` для освобождения ресурсов.

## Что такое временная лицензия и зачем она нужна?
Временная лицензия позволяет оценить GroupDocs.Search без каких‑либо ограничений оценки. Она идеальна для разработки, тестирования или проектов‑прототипов до принятия решения о полной покупке. Лицензия предоставляет доступ ко всем функциям на ограниченный период, позволяя измерять производительность, тестировать точки интеграции и убедиться, что решение отвечает вашим требованиям без финансовых обязательств.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть следующие условия:

### Требуемые библиотеки и зависимости
Для работы с GroupDocs.Search для Java включите необходимые зависимости Maven:
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
Вы также можете загрузить последнюю версию напрямую с [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Настройка окружения
- Убедитесь, что установлен совместимый JDK (Java 8 или новее).  
- Настройте вашу IDE для поддержки Maven‑проектов.

### Требования к знаниям
Базовое понимание программирования на Java и знакомство с управлением проектами Maven будет полезным. Если вы новичок в этих концепциях, рассмотрите возможность изучения вводных ресурсов для начала работы.

## Как получить временную лицензию
Временная лицензия получается путем посещения портала GroupDocs, заполнения короткой формы запроса и размещения полученного файла `.lic` в папке `resources` вашего проекта. Затем инициализируйте лицензию несколькими строками кода (см. фрагмент ниже). Для формы запроса используйте официальную страницу: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## Настройка GroupDocs.Search для Java

### Информация об установке
Чтобы начать использовать GroupDocs.Search для Java в вашем проекте, следуйте шагам Maven выше или загрузите последнюю версию напрямую со страницы официальных релизов.

#### Шаги получения лицензии
1. **Бесплатная пробная версия** – Исследуйте возможности без обязательств.  
2. **Временная лицензия** – Получите краткосрочный ключ для тестирования (см. раздел выше).  
3. **Покупка** – Для использования в продакшене приобретите полную лицензию на **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)**.

### Базовая инициализация и настройка
Инициализируйте ваш проект с GroupDocs.Search следующим образом:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Этот шаг инициализации критически важен для обеспечения бесшовной работы всех компонентов в вашей поисковой сети.

## Руководство по реализации
Теперь разберём процесс на управляемые разделы, каждый из которых фокусируется на конкретной функции развертывания и управления узлами поисковой сети.

### Функция 1: Настройка конфигурации
**Обзор:** Настройка конфигурации вашей поисковой сети — первый шаг в развертывании узлов. Эта настройка включает указание путей и портов, критически важных для развертывания узлов.

#### Шаги реализации:
##### Шаг 1: Определить базовый путь и порт
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Шаг 2: Настроить поисковую сеть
Функция `configureSearchNetwork` подготавливает объект конфигурации, необходимый для развертывания узлов.  
`Configuration` — класс, содержащий все настройки, такие как папка индекса, сетевые порты и роли узлов.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Параметры:** Базовый путь и порт используются для поиска ресурсов и установления каналов связи.  
- **Возвращаемое значение:** Настроенный объект `Configuration`, адаптированный под ваши потребности развертывания.

### Функция 2: Развертывание поисковой сети
**Обзор:** Развёртывание узлов необходимо для масштабирования возможностей поиска в разных средах или сегментах данных.

#### Шаги реализации:
##### Шаг 1: Развернуть узлы
Функция `deploySearchNetwork` инициализирует и возвращает массив узлов поисковой сети.  
`SearchNetworkNodes` представляет каждый экземпляр узла, участвующий в распределённом поисковом кластере.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Параметры:** Базовый путь, порт и конфигурация определяют среду развертывания.  
- **Возвращаемое значение:** Массив, содержащий инициализированные `SearchNetworkNodes`.

### Функция 3: Подписка на события сети
**Обзор:** Мониторинг активности вашей поисковой сети критически важен для поддержания оптимальной производительности и надёжности.

#### Шаги реализации:
##### Шаг 1: Подписка на события главного узла
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Назначение:** Этот шаг гарантирует, что вы будете уведомлены о значимых событиях или изменениях в вашей поисковой сети.

### Функция 4: Индексация документов
**Обзор:** Добавление каталогов, содержащих документы для индексации, обеспечивает эффективный поиск данных по всей сети.

#### Как добавить каталоги в индекс
`addDirectoriesToIndex` — вспомогательный метод, регистрирующий пути папок для индексации на главном узле.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Назначение:** Обеспечивает быстрый доступ и возможность поиска всех документов в указанных каталогах.

### Функция 5: Добавление атрибутов к документам
**Обзор:** Пользовательские атрибуты обогащают метаданные документов, делая поиск более гибким и информативным.

#### Как добавить пользовательские атрибуты к документу
`addAttribute` добавляет пользовательский метаданные‑атрибут к указанному документу в индексе.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Параметры:** Укажите узел, ключ документа и атрибут, который необходимо добавить.  
- **Назначение:** Расширяет функциональность поиска, обогащая документы дополнительными метаданными.

### Функция 6: Получение проиндексированных документов
**Обзор:** Эффективное получение и перечисление проиндексированных документов гарантирует точность и полноту данных.

#### Шаги реализации:
##### Шаг 1: Получить проиндексированные документы
```java
getIndexedDocuments(nodes[0]);
```  
- **Назначение:** Проверяет успешную индексацию всех необходимых документов в вашей поисковой сети.

### Функция 7: Закрытие узлов сети
**Обзор:** Корректное закрытие узлов важно для управления ресурсами и предотвращения утечек памяти.

#### Шаги реализации:
##### Шаг 1: Закрыть все узлы
`closeNodes` завершает работу всех активных поисковых узлов и освобождает выделенные ресурсы.  
```java
closeNodes(nodes);
```  
- **Назначение:** Освобождает ресурсы, занятые каждым узлом, обеспечивая чистый процесс завершения работы.

## Зачем использовать временную лицензию для GroupDocs.Search?
Временная лицензия предоставляет **полный доступ ко всем функциям на 30 дней** и поддерживает до **50 000 проиндексированных документов** без ограничения производительности. Это позволяет измерять скорость индексации, задержку запросов и масштабируемость на реальных данных до покупки производственной лицензии. Кроме того, она удаляет водяные знаки оценки, давая истинное представление о возможностях конечного продукта.

## Общие сценарии использования
1. **Enterprise Document Management** – Индексировать миллионы внутренних файлов по отделам, обеспечивая мгновенный полнотекстовый поиск.  
2. **E‑commerce Platforms** – Создать поисковый каталог товаров, охватывающий несколько складов и сторонних поставок.  
3. **Legal Firms** – Организовать судебные дела, контракты и доказательства с пользовательскими метаданными для быстрого извлечения.

Возможные интеграции с другими системами включают CRM‑платформы, системы управления контентом (CMS) и инструменты аналитики данных, используя мощные функции индексации и поиска, предоставляемые GroupDocs.Search для Java.

## Соображения по производительности
Для оптимизации производительности при использовании GroupDocs.Search для Java:
- **Оптимизировать конфигурацию** – Настройте параметры конфигурации в соответствии с вашей конкретной средой развертывания.  
- **Мониторить использование ресурсов** – Регулярно проверяйте CPU, память и I/O, чтобы избежать узких мест или утечек памяти.  
- **Следовать лучшим практикам** – Соблюдайте рекомендации по управлению памятью в Java, обеспечивая эффективное использование системных ресурсов.

## Часто задаваемые вопросы

**Q: Как долго действует временная лицензия?**  
A: Временные лицензии обычно действуют 30 дней, что дает достаточно времени для оценки продукта.

**Q: Можно ли перейти от временной к полной лицензии без переустановки?**  
A: Да — замените файл временной лицензии на файл полной лицензии и перезапустите приложение.

**Q: Нужно ли переиндексировать документы после применения новой лицензии?**  
A: Нет, индекс остаётся неизменным; лицензия лишь регулирует права использования.

**Q: Что происходит, если я забуду закрыть узлы?**  
A: Неосвобождённые ресурсы могут привести к утечкам памяти; всегда вызывайте `closeNodes` при завершении работы.

**Q: Можно ли добавить более одного пользовательского атрибута к документу?**  
A: Абсолютно — вызывайте `addAttribute` несколько раз с разными именами атрибутов.

**Последнее обновление:** 2026-07-02  
**Тестировано с:** GroupDocs.Search for Java 25.4  
**Автор:** GroupDocs

## Связанные руководства

- [Развернуть узел поисковой сети в .NET с использованием GroupDocs для эффективной индексации и извлечения документов](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Как реализовать поисковую сеть с GroupDocs.Search в .NET для систем управления документами](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Настройка сети Aspose.Search и добавление атрибутов документов с GroupDocs.Redaction для .NET: Полное руководство](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)