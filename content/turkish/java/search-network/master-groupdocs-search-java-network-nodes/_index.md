---
date: '2026-07-02'
description: GroupDocs.Search için geçici bir lisans almayı, dizinlere klasör eklemeyi
  ve Java search network nodes yönetirken özel belge öznitelikleri eklemeyi öğrenin.
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
title: Geçici Lisans Alın GroupDocs – Master Search Nodes (Java)
type: docs
url: /tr/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Geçici Lisans Alın GroupDocs – Ana Arama Düğümleri (Java)

Bu kapsamlı rehberde **GroupDocs.Search için geçici bir lisans alacak**, çok düğümlü bir arama ağı yapılandıracak ve Java kullanarak **dizinlemek için dizinleri eklemeyi** ve **özel belge nitelikleri eklemeyi** öğreneceksiniz. İster kurumsal bir belge yönetim sistemi ister aranabilir bir ürün kataloğu oluşturuyor olun, bu adımları öğrenmek platformu kısıtlamalar olmadan değerlendirmenizi ve arama yeteneklerinizi hızlıca ölçeklendirmenizi sağlar.

## Hızlı Cevaplar
- **GroupDocs.Search'i kullanmaya başlamak için ilk adım nedir?** GroupDocs portalından geçici bir lisans alın.  
- **Hangi Maven deposu kütüphaneyi barındırıyor?** `https://releases.groupdocs.com/search/java/`.  
- **Dizinlere nasıl ekleme yaparım?** Ana düğümde `addDirectoriesToIndex` yardımcı metodunu çağırın.  
- **Özel belge nitelikleri ekleyebilir miyim?** Evet—belge anahtarı ve nitelik adıyla `addAttribute` metodunu çağırın.  
- **Düğümleri düzgün bir şekilde nasıl kapatırım?** Kaynakları serbest bırakmak için `closeNodes` metodunu çağırın.

## Geçici lisans nedir ve neden ihtiyacım var?
Geçici bir lisans, GroupDocs.Search'ı herhangi bir değerlendirme sınırlaması olmadan değerlendirmenizi sağlar. Geliştirme, test veya kanıt‑konsepti projeleri için mükemmeldir; tam bir satın alma yapmadan önce.

Lisans, sınırlı bir süre için tam özellik erişimi verir, böylece performansı ölçebilir, entegrasyon noktalarını test edebilir ve çözümün gereksinimlerinizi karşılayıp karşılamadığını finansal bir taahhüt olmadan doğrulayabilirsiniz.

## Önkoşullar

Başlamadan önce, aşağıdaki önkoşulların yerine getirildiğinden emin olun:

### Gerekli Kütüphaneler ve Bağımlılıklar
Java için GroupDocs.Search ile çalışmak üzere gerekli Maven bağımlılıklarını ekleyin:
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
En son sürümü doğrudan [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden de indirebilirsiniz.

### Ortam Kurulumu
- Uyumlu bir JDK'nin (Java 8 veya daha yeni) kurulu olduğundan emin olun.  
- IDE'nizi Maven projelerini destekleyecek şekilde ayarlayın.

### Bilgi Önkoşulları
Java programlaması hakkında temel bir anlayış ve Maven proje yönetimi konusunda aşinalık faydalı olacaktır. Bu kavramlara yeniyseniz, başlangıç kaynaklarını incelemeyi düşünün.

## Geçici lisans nasıl alınır
Geçici bir lisans, GroupDocs portalını ziyaret ederek, kısa bir istek formunu doldurarak ve alınan `.lic` dosyasını projenizin `resources` klasörüne yerleştirerek elde edilir. Ardından lisansı birkaç satır kodla başlatın (aşağıdaki kod parçacığına bakın). İstek formu için resmi sayfayı kullanın: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## GroupDocs.Search for Java Kurulumu

### Kurulum Bilgileri
Projenizde GroupDocs.Search for Java'ı kullanmaya başlamak için yukarıdaki Maven adımlarını izleyin veya resmi sürüm sayfasından en son sürümü doğrudan indirin.

#### Lisans Edinme Adımları
1. **Ücretsiz Deneme** – Herhangi bir taahhüt olmadan özellikleri keşfedin.  
2. **Geçici Lisans** – Test için kısa vadeli bir anahtar edinin (yukarıdaki bölüme bakın).  
3. **Satın Alma** – Üretim kullanımı için **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)** adresinden tam lisans satın alın.

### Temel Başlatma ve Kurulum
Projenizi GroupDocs.Search ile aşağıdaki gibi başlatın:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Bu başlatma adımı, tüm bileşenlerin arama ağınız içinde sorunsuz çalışmasını sağlamak için kritiktir.

## Uygulama Kılavuzu
Şimdi, süreci yönetilebilir bölümlere ayıralım, her biri dağıtılmış arama ağı düğümlerinin dağıtımı ve yönetimiyle ilgili belirli bir özelliğe odaklanacak.

### Özellik 1: Yapılandırma Kurulumu
**Genel Bakış:** Arama ağınız için yapılandırmayı ayarlamak, düğümleri dağıtmanın ilk adımıdır. Bu kurulum, düğüm dağıtımı için kritik olan yolları ve portları belirtmeyi içerir.

#### Uygulama Adımları:
##### Adım 1: Temel Yol ve Portu Tanımla
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Adım 2: Arama Ağını Yapılandır
`configureSearchNetwork` fonksiyonu, düğümleri dağıtmak için gerekli yapılandırma nesnesini hazırlar.  
`Configuration` sınıfı, indeks klasörü, ağ portları ve düğüm rolleri gibi tüm ayarları tutar.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parametreler:** Temel yol ve port, kaynakları bulmak ve iletişim kanallarını kurmak için kullanılır.  
- **Dönüş Değeri:** Dağıtım ihtiyaçlarınıza göre özelleştirilmiş bir `Configuration` nesnesi.

### Özellik 2: Arama Ağı Dağıtımı
**Genel Bakış:** Düğümleri dağıtmak, arama yeteneklerinizi farklı ortamlar veya veri segmentleri arasında ölçeklendirmek için gereklidir.

#### Uygulama Adımları:
##### Adım 1: Düğümleri Dağıt
`deploySearchNetwork` fonksiyonu, arama ağı düğümlerinin bir dizisini başlatır ve döndürür.  
`SearchNetworkNodes`, dağıtılmış arama kümesine katılan her düğüm örneğini temsil eder.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parametreler:** Temel yol, port ve yapılandırma, dağıtım ortamını belirlemek için kullanılır.  
- **Dönüş Değeri:** Başlatılmış `SearchNetworkNodes` içeren bir dizi.

### Özellik 3: Ağ Olaylarına Abone Olma
**Genel Bakış:** Arama ağınızın etkinliklerini izlemek, optimal performans ve güvenilirliği sürdürmek için kritiktir.

#### Uygulama Adımları:
##### Adım 1: Ana Düğüm Olaylarına Abone Ol
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Amaç:** Bu adım, arama ağınızdaki önemli olaylar veya değişikliklerden haberdar olmanızı sağlar.

### Özellik 4: Belgeleri Dizinleme
**Genel Bakış:** Dizinlenecek belgeleri içeren dizinlerin eklenmesi, ağınızda verimli veri geri getirmeyi sağlar.

#### Dizinlemek için dizinleri nasıl eklenir
`addDirectoriesToIndex` ana düğümde dizinleme için klasör yollarını kaydeden bir yardımcı metottur.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Amaç:** Belirtilen dizinlerdeki tüm belgelerin hızlı erişimini ve aranabilirliğini kolaylaştırır.

### Özellik 5: Belgeler İçin Nitelikler Ekleme
**Genel Bakış:** Özel nitelikler belge meta verilerini geliştirir, aramaları daha esnek ve bilgilendirici hâle getirir.

#### Özel belge nitelikleri nasıl eklenir
`addAttribute` indeks içindeki belirli bir belgeye özel bir meta veri niteliği ekler.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parametreler:** Eklenmek istenen düğümü, belge anahtarını ve niteliği belirtin.  
- **Amaç:** Belgeleri ek meta verilerle zenginleştirerek arama işlevselliğini genişletir.

### Özellik 6: Dizinlenmiş Belgeleri Getirme
**Genel Bakış:** Veri doğruluğu ve bütünlüğünü sağlamak için dizinlenmiş belgeleri verimli bir şekilde alıp listeleyin.

#### Uygulama Adımları:
##### Adım 1: Dizinlenmiş Belgeleri Al
```java
getIndexedDocuments(nodes[0]);
```  
- **Amaç:** Arama ağınızdaki tüm gerekli belgelerin başarılı bir şekilde dizinlendiğini doğrular.

### Özellik 7: Ağ Düğümlerini Kapatma
**Genel Bakış:** Düğümleri doğru bir şekilde kapatmak, kaynak yönetimi ve bellek sızıntılarını önlemek için kritiktir.

#### Uygulama Adımları:
##### Adım 1: Tüm Düğümleri Kapat
`closeNodes` tüm aktif arama düğümlerini kapatır ve tahsis edilen kaynakları serbest bırakır.  
```java
closeNodes(nodes);
```  
- **Amaç:** Her düğmenin işgal ettiği kaynakları serbest bırakarak temiz bir kapatma süreci sağlar.

## GroupDocs.Search için geçici lisans neden kullanılmalı?
Geçici bir lisans, **30 gün boyunca tam özellik erişimi** sağlar ve **50.000'e kadar dizinlenmiş belge**yi performans kısıtlaması olmadan destekler. Bu, üretim lisansı satın almadan önce gerçek veri üzerinde indeksleme hızı, sorgu gecikmesi ve ölçeklenebilirliği ölçmenizi sağlar. Ayrıca değerlendirme filigranlarını kaldırarak ürünün nihai yeteneklerinin gerçek bir temsilini sunar.

## Yaygın Kullanım Senaryoları
1. **Kurumsal Belge Yönetimi** – Bölümler arasında milyonlarca iç dosyayı indeksleyerek anlık tam metin arama sağlar.  
2. **E‑ticaret Platformları** – Birden fazla depo ve üçüncü taraf beslemelerini kapsayan aranabilir bir ürün kataloğu oluşturur.  
3. **Hukuk Firmaları** – Hızlı erişim için özel meta verilerle dava dosyalarını, sözleşmeleri ve delilleri düzenler.

Diğer sistemlerle entegrasyon olanakları arasında CRM platformları, içerik yönetim sistemleri (CMS) ve veri analitiği araçları bulunur; bu, Java için GroupDocs.Search tarafından sağlanan güçlü indeksleme ve arama özelliklerinden yararlanır.

## Performans Düşünceleri
Java için GroupDocs.Search kullanırken performansı optimize etmek için:
- **Yapılandırmayı Optimize Et** – Yapılandırma ayarlarınızı belirli dağıtım ortamınıza göre özelleştirin.  
- **Kaynak Kullanımını İzle** – CPU, bellek ve I/O'yu düzenli olarak kontrol ederek darboğazları veya bellek sızıntılarını önleyin.  
- **En İyi Uygulamaları Takip Et** – Java bellek yönetimi yönergelerine uyun, sistem kaynaklarının verimli kullanılmasını sağlayın.

## Sıkça Sorulan Sorular

**S: Geçici bir lisans ne kadar süreyle geçerlidir?**  
C: Geçici lisanslar genellikle 30 gün geçerlidir, bu da ürünü değerlendirmek için yeterli zaman tanır.

**S: Geçici bir lisansı tam lisansa yeniden kurulum yapmadan geçiş yapabilir miyim?**  
C: Evet—geçici lisans dosyasını tam lisans dosyasıyla değiştirin ve uygulamanızı yeniden başlatın.

**S: Yeni bir lisans uyguladıktan sonra belgeleri yeniden indekslemem gerekir mi?**  
C: Hayır, indeks aynı kalır; lisans sadece kullanım haklarını yönetir.

**S: Düğümleri kapatmayı unutursam ne olur?**  
C: Serbest bırakılmayan kaynaklar bellek sızıntılarına yol açabilir; kapanış sırasında her zaman `closeNodes` metodunu çağırın.

**S: Bir belgeye birden fazla özel nitelik eklemek mümkün mü?**  
C: Kesinlikle—farklı nitelik adlarıyla `addAttribute` metodunu birden çok kez çağırın.

---  
**Son Güncelleme:** 2026-07-02  
**Test Edilen Versiyon:** GroupDocs.Search for Java 25.4  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [GroupDocs kullanarak .NET'te Verimli Belge Dizinleme ve Getirme için Bir Arama Ağı Düğümü Dağıtın](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [.NET'te Belge Yönetim Sistemleri için GroupDocs.Search ile Bir Arama Ağı Nasıl Uygulanır](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [.NET için Aspose.Search Ağını Yapılandırma ve GroupDocs.Redaction ile Belge Nitelikleri Ekleme: Kapsamlı Bir Rehber](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)