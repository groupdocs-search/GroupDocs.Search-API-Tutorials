---
date: '2026-01-19'
description: Geçici lisans almayı, GroupDocs.Search for Java ile arama ağı düğümlerini
  dağıtıp yönetmeyi öğrenerek belge getirmeyi geliştirin.
keywords:
- GroupDocs.Search for Java
- search network nodes
- document management system
title: GroupDocs.Search Java Düğümleri için Geçici Lisans Alın
type: docs
url: /tr/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# GroupDocs.Search for Java ile Arama Ağ Düğümlerini Ustalıkla Yönetme

Günümüz veri odaklı dünyasında, GroupDocs.Search için **geçici bir lisans edinmek**, arama ağ düğümlerini verimli bir şekilde yönetmek ve kuruluşunuzun bilgiyi hızlı ve doğru bir şekilde geri getirme yeteneğini artırmak için ilk adımdır. Bu öğretici, bir yapılandırma ayarlamaktan birden çok düğüm dağıtmaya ve dizinleme klasörlerinden özel belge öznitelikleri eklemeye kadar her şeyi nasıl yöneteceğinizi adım adım gösterir—ve çözümü test etmeye hazır olduğunuzda geçici lisansı nasıl alacağınızı tam olarak gösterir.

## Hızlı Yanıtlar
- **GroupDocs.Search'i kullanmaya başlamak için ilk adım nedir?** GroupDocs portalından geçici bir lisans edinin.  
- **Hangi Maven deposu kütüphaneyi barındırıyor?** `https://releases.groupdocs.com/search/java/`.  
- **Dizinlere eklemek için nasıl klasör eklerim?** Ana düğümde `addDirectoriesToIndex` yardımcı metodunu kullanın.  
- **Özel belge öznitelikleri ekleyebilir miyim?** Evet—belge anahtarı ve öznitelik adıyla `addAttribute` metodunu çağırın.  
- **Düğümleri düzgün bir şekilde nasıl kapatırım?** Kaynakları serbest bırakmak için `closeNodes` metodunu çağırın.

## Geçici lisans nedir ve neden ihtiyacım var?
Geçici bir lisans, GroupDocs.Search'i herhangi bir değerlendirme sınırlaması olmadan denemenizi sağlar. Tam bir satın alma yapmadan önce geliştirme, test veya kanıt‑konsepti projeleri için mükemmeldir.

## Önkoşullar

Başlamadan önce, aşağıdaki önkoşulların yerine getirildiğinden emin olun:

### Gerekli Kütüphaneler ve Bağımlılıklar
GroupDocs.Search for Java ile çalışmak için gerekli Maven bağımlılıklarını ekleyin:
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
Ayrıca en son sürümü doğrudan [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

### Ortam Kurulumu
- Uyumlu bir JDK'nin (Java 8 veya üzeri) kurulu olduğundan emin olun.  
- IDE'nizi Maven projelerini destekleyecek şekilde yapılandırın.

### Bilgi Önkoşulları
Java programlamaya temel bir anlay konusunda bir aşinalık fayeyi düşünün.

## Geçici lisans nasıl alınır
1. **[GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)** sayfasını ziyaret edin.  
2. E-posta adresinizi ve proje detaylarunu doldurun.  
3. Kurulum izleyin veya resmi sürüm sayfasından en son sürümü doğrudan indirin.

#### Lisans Edinme Adımları
1. **Ücretsiz Deneme** – Özellikleri herhangi bir taahhüt olm. **Geçici Lisans** – Test için kısa vadeli bir anahtar edinin (yukarıdaki bölüme bakın).  
3. **Satın Alma** – Üretim kullanımı için tam lisansı **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)** adresinden satın alın.

### Temel Başlatma ve Kurulum
Projenizi GroupDocs.Search ile aşağıdaki gibi başlatın:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```
Bu başlatma adımı, tüm bileşenlerin arama ağınız içinde sorunsuz çalışmasını sağlamak için kritiktir.

## Uygulama Kılavuzu
Şimdi, süreci yönetilebilir bölümlere ayıralım; her biri arama ağ düğümlerini dağıtma ve yönetme ile ilgili belirli bir özelliğe odaklanacak.

### Özellik 1: Yapılandırma Ayarı
**Genel Bakış:** Arama ağınız için yapılandırmayı ayarlamak, düğümleri dağıtmanın ilk adımıdır. Bu ayar, düğüm dağıtımı için kritik olan yol ve portları belirtmeyi içerir.

#### Uygulama Adımları:
##### Adım 1: Temel Yol ve Portu Tanımla
```java
String basePath = "/path/to/config";
int basePort = 8080;
```
##### Adım 2: Arama Ağını Yapılandır
`configureSearchNetwork` fonksiyonu, düğümleri dağıtmak için gerekli yapılandırma nesnesini hazırlar.
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
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```
- **Parametreler:** Temel yol, port ve yapılandırma, dağıtım ortamını belirlemek için kullanılır.  
- **Dönüş Değeri:** Başlatılmış `SearchNetworkNodes` içeren bir dizi.

### Özellik 3: Ağ Olaylarına Abone Olma
**Genel Bakış:** Arama ağınızın aktivitelerini izlemek, optimum performans ve güvenilirliği sürdürmek için kritiktir.

#### Uygulama Adımları:
##### Adım 1: Ana Düğüm Olaylarına Abone Ol
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```
- **Amaç:** Bu adım, arama ağınızdaki önemli olaylar veya değişikliklerden haberdar olmanızı sağlar.

### Özellik 4: Belgeleri Dizinleme
**Genel Bakış:** Dizinlenecek belgeleri içeren klasörlerin eklenmesi, ağınızda verimli veri geri getirmeyi sağlar.

#### Dizinlemek için klasörleri nasıl eklenir
Motoru indekslemek istediğiniz klasörlere yönlendirmek için ana düğümdeki yardımcı metodu kullanın.
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```
- **Amaç:** Belirtilen klasörlerdeki tüm belgelerin hızlı erişimini ve aranabilirliğini sağlar.

### Özellik 5: Belgeler İçin Öznitelik Ekleme
**Genel Bakış:** Özel öznitelikler belge meta verilerini geliştirir, aramaları daha esnek ve bilgilendirici hâle getirir.

#### Özel belge öznitelikleri nasıl eklenir
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```
- **Parametreler:** Eklenmek istenen düğüm, belge anahtarı ve özniteliği belirtin.  
- **Amaç:** Belgeleri ek meta veri ile zenginleştirerek arama işlevselliğini genişletir.

### Özellik 6: Dizinlenmiş Belgeleri Getirme
**Genel Bakış:** Veri doğruluğu ve bütünlüğünü sağlamak için dizinlenmiş belgeleri verimli bir şekilde alıp listeleyin.

#### Uygulama Adımları:
##### Adım 1: Dizinlenmiş Belgeleri Al
```java
getIndexedDocuments(nodes[0]);
```
- **Amaç:** Arama ağınız içinde gerekli tüm belgelerin başarılı bir şekilde dizinlendiğini doğrular.

### Özellik 7: Ağ Düğümlerini Kapatma
**Genel Bakış:** Düğümleri düzgün bir şekilde kapatmak, kaynak yönetimi ve bellek sızıntılarını önlemek için kritiktir.

#### Uygulama Adımları:
##### Adım 1: Tüm Düğümleri Kapat
```java
closeNodes(nodes);
```
- **Amalardır:
1. ****ileştirir.  
2. **E‑ticaret Platformları** – Farklı sunucularda depolanan geniş kataloglara hızlı erişim sağlayarak ürün arama yeteneklerini artırır.  
3. **Hukuk Firmaları** – Büyük miktarda hukuki belgeyi kolay aranabilir bir formata organize ederek dava araştırmalarını kolaylaştırır.

Diğer sistemlerle entegrasyon olanakları arasında CRM platformları, içerik yönetim sistemleri (CMS) ve veri analitiği araçları bulunur; bu entegrasyonlar GroupDocs.Search for Java tarafından sağlanan güçlü indeksleme ve arama özellik etmek için:
- **Yapılandırmayı Optimize Et** – Yapılandırma ayarlarınızı belirli dağıtım ortamınıza- **Kaynak Kullanımını İzle** – Dar boğazları veya bellek sızıntılarını önlemek için kaynak tahsislerini düzenli olarak kontrol edin.  
- **En İyi Uygulamaları Takip Et** – Java bellek yönetimi yönergelerine uyun, sistem kaynaklarının verimli kullanılmasını sağlayın.

## Sıkça Sorulan Sorular

** ne kadar süreyle geçerlidir?**  
C: Geçici lisanslar genellikle 30 gün geçerlidir ve ürünü değerlendirmek için yeterli zaman?**mayı: Serbest bırakılmamış kaynaklar bellek sızıntılarına yol açabilir; kapanış sırasında her zaman `closeNodes` metodunu çağırın.

**S: Bir belgeye birden fazla özel öznitelik eklemek mümkün mü?**  
C: Kesinlikle—farklı öznitelik adlarıyla `addAttribute` metodunu birden çok kez çağırın.

## Sonuç
Bu öğreticide, **geçici bir lisans edinmeyi**, arama ağ düğüarak özel belge öznitelikleri eklemeyi öğrendiniz. Bu adımları izleyerek, kuruluşunuzun bilgiyi hızlı ve doğru bir şekilde geri getirme yeteneğini artırabilirsiniz. Bu teknikleri bugün projelerinizde uygulamaya başlayın ve performans artışını ilk elden deneyimleyin.

---

**Son Güncelleme:** 2026-01-19  
**Test Edilen Versiyon:** GroupDocs.Search for Java 25.4  
**Yazar:** GroupDocs