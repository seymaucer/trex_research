# MODERN YAZILIM GELİŞTİRME PRATİKLERİ

## Git nedir? GitHub nedir?
  Git bir projedeki kod değişikliklerini takip etmek, farklı sürümleri yönetmek ve ekip çalışmasını kolaylaştırmak için kullanılan bir dağıtılmış versiyon kontrol sistemidir. Bu da kaynak kodun ve proje geçmişinin tam kopyasının her geliştiricinin bilgisayarında bulunduğu kontrol yöntemidir.
  Github ise Git depolarını barındıran bulut tabanlı bir platformdur.Açık kaynak projeler, ekip çalışması için kullanılır.

## Temel Git Komutları
  Git init: Yeni bir Git deposu oluşturmaya yarar.
  Git clone: Uzaktaki bir depoyu yereline kopyalar.
  Git add: Dosyayı bunu kaydetmek istiyorum diyip stage(hazırlık alanına) eklenir.
  Git commit:Yapılan değişiklikleri kaydeder.
  Git push:Yaptığın commit'leri GitHub gibi bir uzak sunucuya gönderir.Böylece başkaları da senin değişikliklerini görebilir.Push işlemi,yerel değişiklikleri merkezi projeye aktarır.
  Git pull:Başka bir uzak sunucudaki en güncel değişiklikleri kendi bilgisayarına çeker.Bir ekipte başkalarının yaptığı değişiklikleri almak için kullanılır.
  Git branch:Projede farklı çalışma yolları oluşturmayı sağlar.Ana projeyi bozmadan ayrı bir kopya gibi çalışmayı sağlar.
  Git merge:Farklı bir branch'te yaptığın değişiklikleri ana projeyle birleştirmek için kullanılır.
  
  ## Merge Conflict nedir, nasıl çözülür?
  Aynı dosyada iki farklı branch'te yapılan değişiklikler Git tarafından otomatik birleştirilmezse merge conflict oluşur.
  Çözüm adımları ise şöyledir:
   . Çakışan satırlar bu işaretlerle gösterilir: "<<<<<<< (head) ======= (main) >>>>>>> (yeni-özellik)" işaretler arasındaki kısımları düzenlenmeli.
   . Daha sonra çakışmayı manuel olarak bizim düzenlememiz gerekir.
   . Git add ile çözümü staged'e eklenir.
   . Git commit ile kaydedilip çakışmayı sonlandırırız.

 ## CI/CD nedir? Azure DevOps, GitHub Actions ile pipeline örnekleri 
   Yazdığımız kodun düzgün çalışıp çalışmadığını test etmek, sonra da bu kodu kullanıcıların kullanabileceği şekilde yayına almak gerekir.CI/CD ise bunu otomatik hale getirir.
   .CI(Sürekli Entegrasyon): Gönderdiğimiz her kod GitHub tarafından otomatik test ediliyor.Böylece kodda hata varsa hemen öğrenmiş oluyoruz.
   .CD(Sürekli Dağıtım):Eğer kodlarımız testi geçtiyse CD bu kodu otomatik olarak yayına hazır hale getiriliyor veya direkt yayına alınıyor.

   GitHub actions ile .NET CI/CD 
    Kodları GitHub’a gönderdiğimde, otomatik olarak build ve test işlemleri yapılmasını istedim. Bunun için aşağıdaki pipeline dosyasını yazdım:
    Bu işlem her push sonrası otomatik çalışıyor ve projemi test edip hata varsa bana hata bildirimi geliyor.



name: .NET Otomatik Build ve Test

on:
  push:
    branches: [ main ]  # main dalına kod gönderilince çalışır

jobs:
  build-and-test:
    runs-on: ubuntu-latest  # Linux ortamında çalışır

    steps:
      - name: Kodu indir
        uses: actions/checkout@v2

      - name: .NET 8 kurulumu
        uses: actions/setup-dotnet@v2
        with:
          dotnet-version: '8.0.x'

      - name: Build işlemi
        run: dotnet build --configuration Release

      - name: Testleri çalıştır
        run: dotnet test

   Azure DevOps ile Pipeline Örneği
    Bu işlem de her commit sonrası build ve test işlemi yapıyor ve hata yapmayı engelliyor.
    # azure-pipelines.yml

trigger:
- main  # main dalına kod gönderilince çalışır

pool:
  vmImage: 'windows-latest'  # Windows ortamı kullanılıyor

steps:
- task: UseDotNet@2
  inputs:
    packageType: 'sdk'
    version: '8.0.x'

- script: dotnet build --configuration Release
  displayName: 'Projeyi Derle'

- script: dotnet test
  displayName: 'Testleri Çalıştır'


## Software Development Life Cycle(SDLC)

### Yazılım Geliştirme Sürecinin Aşamaları
   
   .Planlama (Ne Yapacağız): Yazılıma başlamadan yol haritası çıkarılır.Müşteri ne istiyor?Ne kadar zamanda,kaç kişiyle proje yapılıcak? Gibi sorular sorulur.
   .Analiz (Neye İhtiyacımız Var): İhtiyaçlar netleştirilir,iş bölümü yapılır.Hangi özellikler isteniyor?Hangi ekranlar,diller olacak?
   .Tasarım (Nasıl Yapacağız): Projenin mimarisi belirlenir. Veritabanı yapısı, sayfa tasarımları gibi oluşturulur.Koddan önce şekil yani.
   .Geliştirme (Kod Yazılır): Geliştiriciler kodu yazar, test eder. 
   .Test (Her şey Düzgün Çalışıyor mu):Hatalar aranır, düzeltilir. Kod düzgün mü, doğru çalışıyor mu bakılır.
   .Dağıtım (Proje Yayınlanır):Yazılım kullanıcıya sunulur.
   .Bakım (Proje Sonrası Destek):Kullanıcıdan geri bildirim alınır.Yeni istekler varsa düzenlenir.

### Agile/Scrum/Kanban Metodolojileri

    Agile:Esnek, hızlı ve geri bildirim odaklı çalışma yöntemidir.Büyük projeler yerine küçük işler yapılır.Bir hocam bu sisteme xanax nedeni demişti.Çalışanlar her aşamada müsteriyle iletişimde onlara göre şekil almak zorundalar diye.
    Scrum:Belirli zaman aralıklarıyla (sprint)çalışılır.Günlük toplantılar yapılır.
    Kanban:İşler kart şeklinde tahtaya yazılır. Yapılacaklar,Yapılıyor,Bitti gibi.Sürekli bir akış vardır süre kısıtlaması yoktur sprint gibi.


# .NET EKOSİSTEMİ

     -.NET nedir? Tarihçesi,amacı,neden kullanılır?
     
      .NET ekosistemiyle ilk tanıştığımda sadece "C# ile yazılım geliştirme aracı" olduğunu sanıyordum. Ancak araştırdıkça fark ettim ki .NET, sadece C# değil; web uygulamaları, API servisleri, mobil ve masaüstü uygulamalar gibi
      çok farklı yazılımlar geliştirmeye imkan sağlayan güçlü ve çok yönlü bir platformmuş..NET, Microsoft tarafından geliştirilen **açık kaynaklı ve platformlar arası** (cross-platform) bir yazılım geliştirme platformudur.  
      C#, F# ve VB.NET gibi dilleri destekler. Bu platform sayesinde;
      - Web uygulamaları (ASP.NET)
      - Masaüstü uygulamaları (Windows Forms, WPF)
      - Mobil uygulamalar (Xamarin / MAUI)
      - Oyunlar (Unity ile C#)
      - API servisleri 
       gibi birçok yazılım geliştirilebilir.
       
       Peki neden tercih ediliyor?
       -Güçlü dil desteği
       -Visual Studio ve Rider gibi gelişmiş IDE'lerle uyumlu
       -Yüksek performanslı web ve API geliştirme şansı
       -Microsoft desteği

      - .NET Framework, .NET Core ve .NET 7/8 farkları
      
| Özellik             | .NET Framework     | .NET Core         | .NET 5+ / 6 / 7 / 8    |
|---------------------|--------------------|-------------------|------------------------|
| Platform            | Sadece Windows     | Cross-platform    | Cross-platform         |
| Performans          | Orta               | Yüksek            | Daha da yüksek         |
| Açık Kaynak         | Hayır              | Evet              | Evet                   |
| Kullanım Durumu     | Eski projelerde    | Aktif             | En güncel yapı         |

    -dotnet --info çıktısı örneği ve yorumlama
    Bilgisyarımdaki .Net ortamını kontrol etmek için terminale bu kodu yazdım ve şu çıktıyı aldım:

 PS C:\Users\seyma> dotnet --info
.NET SDK:
 Version:   7.0.403
 Commit:    142776d834

Çalışma Zamanı Ortamı:
 OS Name:     Windows
 OS Version:  10.0.22631
 OS Platform: Windows
 RID:         win10-x64
 Base Path:   C:\Program Files\dotnet\sdk\7.0.403\

Host:
  Version:      7.0.13
  Architecture: x64
  Commit:       3f73a2f186

 ## SENKRON VE ASENKRON PROGRAMLAMA

  Her işlem sırayla yapılır bir iş bitmeden diğerine geçilemez.Basit uygulamalarda kullanılır.
 
 public string GetUser()
{
    Thread.Sleep(3000);  
    return "Kullanıcı bilgisi";
}
*kullanıcı bilgileri alınırken 3 saniye bekletir.Bekleme bitene kadar işlem yapılmaz.

Asenkron da ise tam tersi beklerken başka işlerde yapılabilir.Web API, veri çekme işlemleri yapılır.

public async Task<string> GetUserAsync()
{
    await Task.Delay(3000); 
    return "Kullanıcı bilgisi";
}
*bekleme olurken programın diğer işleri devam eder.Kullanıcı deneyimi çok daha yüksektir.

  -async:Bir metodun asenkron çalışacağını belirtir.
  -await:Asenkron bir işlemin sonucunu beklememizi sağlar.
  -task:Asenkron işlemi temsil eden veri türüdür.
  -configureAwait:UI veya context'e bağlı olmadan işlem yapmayı sağlar.
  
 ## C# Arrow Function
  Bu ifade lambda fonksiyonu olarak geçer. Derste hocamız kodları kısaltmak daha hızlı kısa kod olarak açıklamıştı lambda fonksiyonu.
  
  List<int> sayilar = new List<int> { 1, 2, 3, 4, 5 };
  var çiftSayilar = sayilar.Where(sayi => sayi % 2 == 0).ToList();
   *sayı çift mi? diye sorgulayan kısa bir fonksiyon var burda da.

#BACKEND GELİŞTİRME TEMELLERİ

  -Backend Nedir?Frontend ile Farkları

   *Backend:Uygulamanın kullanıcı tarafından görülmeyen tarafıdır.Veritabanı, API'ler,işin matematiği burda yer alır.
   *Frontend:Kullanıcının gördüğü kısımdır.Web sitesi tasarımı,butonlar,menüler buradadır.
   
## Web Sunucusu Nedir?API Nedir?API Türleri

   Web sunucusu: internetten gelen istekleri alıp doğru cevapları dönen bir yazılımdır.Örneğin bir kullanıcı web sitesini açtığında, web sunucusu o sayfayı kullanıcının tarayıcısına gönderir.
   API:Yani yazılımların birbiriyle konuşmasını sağlayan arayüzdür.Yani bir yazılım başka bir sistemin sunduğu bilgiyi veya işlevi kullanmak istediğinde API üzerinden veri alılverişi yapar.
    *API Türleri:
     . Rest API: HTTP üzerinden çalışır. Get,Post gibi metodlarla veri alıp gönderir.JSON kullanılır.En yaygın kullanılan API türüdür.
     . Soap API: XML tabanlıdır.Veri taşımak için daha katı kurallara sahiptir.Bankacılık sistemlerinde hala kullanılır.
     . GraphQL API: İstemci sadece ihtiyacı olan alanları ister. Çok verili sorgularda kullanılır.
     . gRPC: Google tarafından geliştirilmiştir.Binary veri taşır. Hız ve performans ön planda.

## HTTP Nedir? HTTP Metodları
   HTTP, istemci ile sunucu arasında veri alışverişini sağlayan protoldür.Bir tarayıcı veya API, sunucuya HTTP metodu ile istek gönderir ve cevap alır.

     *Metodlar
      .Get:Veri almak için kullanılır.(GET/api/urunler (tüm ürünleri getirir))
      .Post:Yeni veri eklemek için.(POST/api/urunler (yeni bir ürün ekler))
      .Put:Var olan veriyi tamamen güncellemek için kullanılır.(PUT/api/urunler/5 (ID'si 5 olan ürünü günceller))
      .Delete:Veri silmek için kullanılır.(DELETE/api/urunler/5 (ID'si 5 olan ürünü siler))
      
 POST örneği
Content-Type: application/json

{
  "ad": "Kahve Makinesi",
  "fiyat": 899.90,
  "stok": 12
} 
  

## RESTful Servislerin Çalışma Mantığı
   Basit ve URL tabanlı bir API mimarisidir.Amacı her şeyi basit, standart ve okunabilir yapmak.
   Her işlem için anlamlı bir URL olur.
   GET,POST,PUT,DELETE gibi HTTP metodları kullanılır.
   JSON formatı ile veri alışverişi yapılır.

 -REST vs SOAP vs GraphQL
 
| Özellik      | REST                     | SOAP             | GraphQL                 |
| ------------ | ------------------------ | ---------------- | ----------------------- |
| Veri Formatı | Genellikle JSON          | XML              | JSON                    |
| Hız          | Hızlı                    | Ağır             | Hızlı                   |
| Esneklik     | Orta                     | Düşük            | Çok Yüksek              |
| Öğrenme      | Kolay                    | Zor              | Orta                    |
| Kullanım     | Güncel sistemlerde sıkça | Eski sistemlerde | Yeni projelerde popüler |

## JSON Veri Formatı ve Kullanım Amacı

   Veri taşıma ve saklama şeklidir.Önceden xml kullanılıyodu şimdi json.
   Kullanım Amaçları:
    *API'ler üzerinden veri gönderip almak
    *Veritabanı ile haberleşmek
    *Hızlı ve sadec veri formatı vermek
    
   Örnek JSON:
GET /api/kullanici/1

{
  "id": 1,
  "ad": "Ayşe",
  "email": "ayse@gmail.com",
  "aktif": true
}
*API den JSON ile kullanıcı verisi çekiyoruz.

# ASP.NET

## ASP.NET ve ASP.NET core nedir?Avantajları Farkları 
  ASP.NET:Microsoft tarafından geliştirilen web uygulamaları yazmak için kullanılan bir framework’tür. Sadece Windows’ta çalışır.
  ASP.NET Core:  modern, hızlı, açık kaynak ve platformlar arası (Windows, Linux, macOS) çalışan yeni nesil versiyonudur.

  - ASP.NET Core'un Avantajları:
  .Daha hızlı ve performanslı
  .Cross-platform (Windows’a bağımlı değil)
  .Açık kaynak
  .Daha hafif ve modern yapı

## MVC Nedir? Ne için Kullanılır?
 ASP.NET projelerinde sık kullanılan bir tasarım desenidir.Açılımı Model-View-Controller'dir.
 Model:Veriyi temsil eder.
 View:Kullanıcıya gösterilen sayfa.
 Controller:Kullanıcıdan gelen istekleri alır, modeli kullanır,view'a gönderir.
  Bu yapı sayesinde kodlar düzenli olur, her şey ayrı ayrı kontrol edilir.

## Middleware Nedir?Nasıl Çalışır?
 ASP.NET Core uygulamasında gelen istek (request) ile cevabın (response) arasına giren yazılım parçalarıdır.
 Örneğin:Kimlik doğrulama,hata yönetimi,giriş yapılması.
 
   Middleware sıralaması(Program.cs içinde)
   
   var builder = WebApplication.CreateBuilder(args);
   app.UseRouting();          1. Rotalama yapılır (hangi URL'ye gidileceği)
   app.UseAuthentication();   2. Kimlik doğrulama yapılır (kullanıcı giriş yapmış mı?)
   app.UseAuthorization();    3. Yetkilendirme yapılır (bu kullanıcı bu sayfaya erişebilir mi?)
   app.UseEndpoints(endpoints =>
   {
      endpoints.MapControllers();  4. Uygun Controller çalıştırılır
    });
    Bunların sıralaması önemli 

## Dependency Injection(DI) nedir? neden önemlidir?
   Bir sınıfın ihtiyacı olan başka sınıfları kendi içinde oluşturmak yerine dışarıdan almasıdır.Diyelim ki bir kahve makinesine süt ve kahve gerekiyo makine kendi alıyosa sıkıntı ama biri gelip koyuyosa bu dependency ınjection oluyor.Çünkü makine sadece kahveyi yapar.Bu sayede;
   DI Örnek:
   
  -Interface tanımı(kim bu interface'i kullanıyorsa, mutlaka GetKullanici() fonksiyonunu yazmalı)
   
   public interface KullaniciService
{
    string GetKullanici();
}

  - Servis Sınıfı(Bu sınıf,KullanıcıService'i uyguluyor.GetKullanici() fonksiyonu da şeyme üçer yazısını döndürüyor.)
   
   public class KullaniciService : KullaniciService
{
    public string GetKullanici()
    {
        return "Şeyma Üçer";
    }
}
   
    -Program.cs'de servis kaydı(Bu DI temelidir)
    
    builder.Services.AddScoped<KullaniciService, KullaniciService>();

    -Controller'da kullanımı
    
    [ApiController]
[Route("api/[controller]")]
public class KullaniciController : ControllerBase
{
    private readonly IKullaniciService _kullaniciService;

    public KullaniciController(IKullaniciService kullaniciService)
    {
        _kullaniciService = kullaniciService;
    }

    [HttpGet]
    public IActionResult Get()
    {
        var ad = _kullaniciService.GetKullanici();
        return Ok(ad);
    }
}
 *Bunun çıktısı "Şeyma Üçer".

 ## Katmanlı Mimari
  Katmanlı mimari,bir uygulamayı görevlerine göre katmanlara ayırarak yazmamızı sağlar.Kodlar daha düzenli olur,her katman sadece kendi işiyle ilgilenir,test etmek ve bakım kolay olur böylece.
  
  ### Temel 3 Katman 
  
  **Presentation Katmanı(Sunum)
   -Kullanıcının gördüğü yer.
   -Web sayfası,butonlar.
   
  **Business Katmanı(İş kuralları)
   -Uygulamanın mantığını,hesaplamalarını,kurallarını içerir.
   -Eğer stok 0 ise ürün satılamaz gibi bir kural varsa burda kontrol edilir.

   **Data Access Katmanı(Veri erişim)
   -Veri tabanına veri ekleme, silme, güncelleme işini yapar.
   -SQL yazılmaz,entity framework gibi orm(nesne-ilişki eşleme) araçları kullanılır.
   
 ## Service & Repository Pattern
    Service: Business katmanında iş yapan sınıftır. (Kural koyar)
    Repository: Data Access katmanında veriye erişen sınıftır. (Veri alır/verir)
    Avantajı: Kodlar daha test edilebilir, katmanlar ayrılmış olur.
   
   ## Temiz Mimari
   Clean Architecture, daha profesyonel ve sürdürülebilir bir mimaridir.

   ### Katmanlar:

   **Domain Katmanı
   -Uygulamanın çekirdeği.
   -kurallar,sınıflar,arabirimler burada.

   **Application Katmanı
   -Kullanıcı ne istiyor, nasıl yapacağız?
   -Use Case’leri (iş akışları) burada yazılır.

   **Infrastructure Katmanı
   -Veritabanı, e-posta gönderimi, dosya işlemleri gibi altyapı işleri burada.

   **API Katmanı
   -Kullanıcının istek gönderdiği yerdir.
   -ASP.NET Core API Controller’lar burada yer alır.

  ## Bağımlılıkların Dışa Akması
    İçteki katmanlar, dıştaki katmanlara bağımlı olmaz.
    Domain Infrastructure'i bilmez ama
    Infrastructure Domain'i tanır.


   ## Katmanlı Mimari
   
    [Kullanıcı / Tarayıcı]
        │
        ▼
┌──────────────────────────────┐
│     Presentation Katmanı     │
│  (UI, Controller, Razor, API)│
└──────────────────────────────┘
        │ çağırır
        ▼
┌──────────────────────────────┐
│     Business Katmanı         │
│ (Kurallar, Servisler, Logic)│
└──────────────────────────────┘
        │ çağırır
        ▼
┌──────────────────────────────┐
│    Data Access Katmanı       │
│ (EF Core, SQL, Repository)   │
└──────────────────────────────┘
        │
        ▼
     [Veritabanı]

## Temiz Mimarı

         [Kullanıcı / API / Web UI]
                    │
                    ▼
    ┌──────────────────────────────┐
    │          API Katmanı         │
    │ (Controller, Request/Response)│
    └──────────────────────────────┘
                    │
                    ▼
    ┌──────────────────────────────┐
    │     Application Katmanı      │
    │ (UseCase, DTO, MediatR vs.) │
    └──────────────────────────────┘
                    │
                    ▼
    ┌──────────────────────────────┐
    │        Domain Katmanı        │
    │(Entity, Interface, Kurallar)│
    └──────────────────────────────┘
                    ▲
                    │
    ┌──────────────────────────────┐
    │     Infrastructure Katmanı   │
    │ (EF Core, Email, File Ops)   │
    └──────────────────────────────┘

# VERİTABANI VE ORM
    SQL, ilişkisel veritabanıyla iletişim kurmak için kullanılan dildir.Veri silmeye,güncellemeye,silmeye yarar.

## İlişkisel vs İlişkisel Olmayan Veritabanları
    
| Özellik             | İlişkisel (Relational)         | İlişkisel Olmayan (NoSQL)  |
| ------------------- | ------------------------------ | -------------------------- |
| Veri Yapısı         | Tablo                          | JSON, belge, anahtar-değer |
| Örnek Veritabanları | SQL Server, PostgreSQL         | MongoDB, Firebase, CouchDB |
| İlişki Desteği      | Var                            | Genelde yok                |
| Şema (Schema)       | Sabit                          | Esnek                      |
| Performans          | Karmaşık işlemlerde daha güçlü | Büyük veri için daha hızlı |


## ORM Nedir?
    SQL yazmadan c# gibi dillerle veritabanı işlemleri yapmayı sağlar.Entity Framework Core gibi.

## DbContext Nedir?
    EF Core'un kalbidir.Veritabanındaki tabloları temsil eder ve veriye erişim sağlar.
    **bu kod veritabanı ile konuşabilmek için köprü görevi görüyor.Products adında yablo oluşturuyoruz daha önce product sınıfını yazdıysak bu tablo onun özlleriklerine göre oluşturulcak.
    
    public class AppDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }
}
## LINQ Nedir?
    LINQ (Language Integrated Query), koleksiyonlar ve veritabanı üzerinde sorgu yazmayı kolaylaştırır.
    
| LINQ İfadesi (C#)                          | SQL Karşılığı                           |
| ------------------------------------------ | --------------------------------------- |
| `db.Users.ToList()`                        | `SELECT * FROM Users`                   |
| `db.Users.Where(u => u.Age > 18).ToList()` | `SELECT * FROM Users WHERE Age > 18`    |
| `db.Users.OrderBy(u => u.Name).ToList()`   | `SELECT * FROM Users ORDER BY Name ASC` |
| `db.Users.Count()`                         | `SELECT COUNT(*) FROM Users`            |

    
 ## Code-First vs Database-First
    
| Özellik       | Code-First       | Database-First                    |
| ------------- | ---------------- | --------------------------------- |
| Başlangıç     | Kod ile başlanır | Hazır veritabanı kullanılır       |
| Yapı          | Class → DB       | DB → Class                        |
| Kullanım Yeri | Yeni projelerde  | Mevcut/veritabanı olan projelerde |
| Araçlar       | Migration        | Scaffold-DbContext                |


## 4 Temel SQL Sorgusu Örneği
 *Select: select * from Products; (verileri listeler)
 *Insert: ınsert into Products (Name, Price) values ('Muz', 10);(name:muz;price:10)
 *Update: update Products SET Price = 15 where Name = 'Muz';(muzun fiyatını 15 olarak günceller)
 *Delete: delete from Products where Name = 'Muz';(ismi muz olan verileri siler)


# GÜVENLİK VE PERFORMANS

  ## Authentication vs Authorization
   Giriş yaptıysan authenticated olursun.(Kimsin sorusunun cevabı)
   Admin paneline erişebiliyorsan authorized olursun.(Neye erişebilirsin)

  ## JWT (JSON Web Token) Nedir?
    JWT, kullanıcı giriş yaptığında oluşturulan ve sunucu ile istemci arasında kimlik bilgisini taşımaya yarayan şifrelenmiş token’dır.
    3 parçadan oluşur:
    -Header:Algoritma ve token tipi 
    -Payload:Kullanıcı bilgileri,id gibi
    -Signature:Gizli Anahtarlarla imzalanmış kısım
     Token, HTTP isteklerinde Authorization: Bearer token şeklinde gönderilir.
     
  ## OAuth, OAuth2.0, OpenID, OpenIddict Nedir?
   
| Teknoloji      | Açıklama                                                                      |
| -------------- | ----------------------------------------------------------------------------- |
| **OAuth**      | Yetki verme protokolü (şifresiz erişim izni sağlar)                           |
| **OAuth2.0**   | OAuth’un gelişmiş sürümü, günümüzde yaygın                                    |
| **OpenID**     | Kimlik doğrulama sağlar ("bu kullanıcı kim?")                                 |
| **OpenIddict** | ASP.NET Core’da OpenID destekli kimlik doğrulama ve yetkilendirme kütüphanesi |
   -kısaca-
   OpenID Authentication sağlar.
   OAuth Authorization sağlar.

## Performans Artırma Teknikleri 
  
    **AsNoTracking()
    Entity Framework’te sorgularda takip kapatılır.
    Performans artar çünkü EF değişiklikleri izlemez.

    **IAsyncEnumerable
    Await foreach ile veri parça parça çekilir.
    Bellek dostu, özellikle büyük veri setlerinde işe yarar.

    **Caching (Önbellekleme)
    Sık kullanılan veriler bellekte tutulur.
    Gereksiz veritabanı sorguları engellenir.

    **Profiling
    Uygulamadaki yavaş noktalar analiz edilir.
    MiniProfiler gibi araçlarla yavaş sorgular bulunur.

## OWASP Top 10
  OWASP (Open Web Application Security Project), web uygulamalarında en yaygın güvenlik açıklarını sıralayan küresel bir projedir.


| #  | Açık Adı                               | Kısa Açıklama                                                                                           |
| -- | -------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| 1  | **Broken Access Control**              | Kullanıcının erişmemesi gereken sayfalara erişebilmesi. Örn: Normal kullanıcı admin paneline girebilir. |
| 2  | **Cryptographic Failures**             | Şifreleme eksiklikleri. Örn: Şifrelerin düz metin olarak saklanması.                                    |
| 3  | **Injection (SQL, XSS)**               | Kullanıcıdan gelen verilerle komut çalıştırma. Örn: SQL Injection ile veritabanına sızma.               |
| 4  | **Insecure Design**                    | Güvenlik düşünülmeden yapılan sistem tasarımları.                                                       |
| 5  | **Security Misconfiguration**          | Yanlış sunucu ayarları, varsayılan şifreler, açık portlar.                                              |
| 6  | **Vulnerable Components**              | Güncel olmayan paketler, açık içeren yazılımlar kullanmak.                                              |
| 7  | **Identification & Auth Failures**     | Zayıf şifre kullanımı, çoklu oturum kontrol eksikliği.                                                  |
| 8  | **Software/Data Integrity Failures**   | Kod veya veri doğrulanmadan sistemde çalıştırılır.                                                      |
| 9  | **Logging & Monitoring Failures**      | Saldırılar kaydedilmez, izleme yapılmaz.                                                                |
| 10 | **Server-Side Request Forgery (SSRF)** | Uygulama, kötü niyetli olarak başka sunuculara istek gönderir.                                          |


## ASP.NET Core ile Alınabilecek Güvenlik Önlemleri

    **SQL Injection'a karşı koruma:Entity Framework Core kullanarak parametreli sorgular yapılır.
      FromQuery, FromBody gibi binding işleminden sonra ModelState.IsValid ile doğrulama yapılır.

    **XSS(Cross-Site Scripting) saldırılarına karşı:Kullanıcının gönderdiği HTML veya script kodlarının çalıştırılmaması gerekiyor.
     Razor sayfaları HTML içerikleri otomatik olarak encode eder.
     Eğer veriyi JavaScript içinde kullanıyorsak, HtmlEncoder.Default.Encode() gibi güvenli kodlama yapılmalı.
     
    **CSRF (Cross Site Request Forgery) Önlemi:Kullanıcının haberi olmadan sistemde işlem yapılmasını engellemek için:
      Formlara otomatik gelen @Html.AntiForgeryToken() kullanılmalı.
      [ValidateAntiForgeryToken] attribute'u POST isteklerinde kontrol sağlar.

    **  Kimlik Doğrulama ve Yetkilendirme (Broken Auth)
      Kullanıcının kimliği iyi doğrulanmalı ve sadece yetkili alanlara erişebilmesi sağlanmalı.
      ASP.NET Identity ile giriş/çıkış işlemleri yapılmalı.
      Şifre politikası uygulanmalı (örneğin en az 6 karakter, büyük harf, özel karakter vs.).
      Eğer JWT token kullanıyorsak, token süresi belirlenmeli (expires) ve zamanında yenilenmeli.
      
    **Model Doğrulama (Validation):Kullanıcıdan gelen veriler önce model üzerinde kontrol edilmeli.

    **Input Sanitization (Girdi Temizleme):Kullanıcıdan gelen içerikler (özellikle HTML) sunucuda mutlaka filtrelenmeli.
      HTML içeriği gerekiyorsa, güvenli HTML parser veya HtmlSanitizer gibi kütüphaneler kullanılmalı.
      Amaç: <script> gibi zararlı kodların çalışmasını engellemek.

# LOGGING VE HATA YÖNETİM
 Yazdığımız uygulamalar bazen hata verebilir, bazen de düzgün çalışıyor gibi görünse bile arka planda bir şeyler ters gidiyor olabilir. Bu yüzden uygulamamızın neler yaptığını kaydetmemiz (loglamamız) gerekir.
       
   **Neden Loglama Yapılır?**
     Uygulamanın geçmişte ne yaptığını izlemek için
     Hata olduğunda neden olduğunu bulmak için
     Canlı sistemde sorunları hızlıca teşhis edebilmek için
     Kullanıcının yaptığı işlemleri kayıt altına almak için
         Yani loglar, uygulamanın "günlük tutması" gibi bir nevi o zaman.
         
      Her şey loglanmaz,önem derecesine göre seviyeler vardır:
        
| Seviye          | Açıklama                                                                  |
| --------------- | ------------------------------------------------------------------------- |
| **Trace**       | En detaylı log. Genelde sadece geliştirme ortamında kullanılır.           |
| **Debug**       | Hataları bulmak için kullanılan geliştirici logları.                      |
| **Information** | Uygulamanın yaptığı önemli işlemler (örneğin: kullanıcı giriş yaptı).     |
| **Warning**     | Kritik değil ama dikkat edilmesi gereken durumlar (örneğin: stok azaldı). |
| **Error**       | Hata oldu ama sistem çalışmaya devam ediyor.                              |
| **Critical**    | Ciddi hata. Sistem çalışamayabilir.                                       |

      
# ASP.NET Core'da Logging Nasıl Yapılır?
  ASP.NET Core, built-in (dahili) bir logging mekanizması sunar.dışardan özel bir şey eklemeden bile log tutmaya başlayabiliriz.
  Bu altyapı sayesinde:
  Hangi olay ne zaman olmuş öğrenebiliriz.
  Hangi metod çalışmış, hangi hatalar alınmış görebiliriz.
  Geliştiriciler olarak uygulamayı izleyebilir, hata ayıklayabilir ve sorunları tespit edebiliriz.

# Global Exception Handling
 Tüm hataları yakalamaktır.Bazen bir sayfa patladığında sunucu hatası verir ama detay yoktur.ASP.NET core bize bu hataları kontrol etme imkanı sunar.

 # UseExceptionHandler ve ILogger nasıl kullanılır?

**UseExceptionHandler:Sistemde bir hata olursa,
Kullanıcıya çirkin sistem hatası gösterilmez,
Onun yerine kullanıcı özel bir hata sayfasına yönlendirilir.
   if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Home/Error");
}
  *Error adında bir sayfa varsa tüm hatalarda o sayfa gösterilicek demektir.
 
 **ILogger:  Bu da uygulamanın log (kayıt) tutma işini yapar. Hangi controller ne zaman çalıştı, hangi işlem ne hata verdi gibi bilgileri yazdırır. 
    
    public class HomeController : Controller
{
    private readonly ILogger<HomeController> _logger;

    public HomeController(ILogger<HomeController> logger)
    {
        _logger = logger;
    }

    public IActionResult Index()
    {
        _logger.LogInformation("Anasayfa yüklendi.");
        return View();
    }

    public IActionResult Error()
    {
        _logger.LogError("Bir hata oluştu.");
        return View();
    }
}
   *ILogger<T> ile özel sınıfa alınır. 
   LogInformation() ile bilgi yazılır.(örneğin kullanıcı giriş yaptı)
   LogError() ile hata loglanır.

# Örnek Hata Yönetim kodu 
 ASP.NET Core’da bir işlem sırasında hata oluşursa, bu hatayı kullanıcıya pat diye göstermek yerine yakalamak ve loglamak isteriz. Bunun için try-catch bloğu ve ILogger kullanırız.
   
   public IActionResult Details(int id)
{
    try
    {
        var product = _db.Products.Find(id);
        return View(product);
    }
    catch (Exception ex)
    {
        _logger.LogError(ex, "Ürün detayları alınırken hata oluştu.");
        return View("Error");
    }
}
  * try bloğuna hata oluşabilcek kod yazılır.
  * catch bloğu hata olursa çalışıcak yerdir.
  * _logger.LogError kısmı ise hatayı kayıt altına alır.
  * return view("Error") burda hata sayfası gösterilir böylece sistem çökmemiş olur.

8. YAZILIM GELİŞTİRME PRENSİPLERİ

# SOLID Prensipleri

* Single Responsibility(tek sorumluluk)
  Bir sınıfın yalnızca tek işi olmalı.
  
    public class InvoicePrinter {
    public void Print(Invoice invoice) {
      
    }
}
     - Tek işi yazdırmak

* Open/Closed
  Kod genişletilmeye açık ama değiştirilmeye kapalı olmalı.
  
    public interface IDiscount {
    double Apply(double price);
}
public class StudentDiscount : IDiscount {
    public double Apply(double price) => price * 0.9;
}
     - Kod değiştirilmeden yeni sınıflar yazarak genişletilme yapılabilir.

* Liskov Substitution
  Türeyen sınıflar, ana sınıfın yerine geçebilmeli.
  -Kuş sınıfı varsa, Güvercin:Kuş sınıfı da aynı şekilde davranabilmeli.

* Interface Segregation
  Kullanılmayan metodları içeren dolu arayüzleri kullanılmamalı.
  
  public interface IPrintable {
    void Print();
}
      - Interface'ler sayesinde farklı sınıflara aynı davranışı kazandırabiliyoruz.IPrintable gibi arayüzler, kodun daha esnek ve genişletilebilir olmasını sağlıyor.
Gerçek dünyada “her yazdırılabilir nesne” bu interface’i kullanabilirmiş gibi düşünebiliriz.

* Dependency Inversion
 Sınıflar,somut değil soyut şeylere bağlı olmalı.

  public interface IMessageService {
    void Send();
}
public class EmailService : IMessageService {
    public void Send() { /* e-posta gönder */ }
}
        - Uygulama somut sınıfa (EmailService) bağımlı olmamalı.
          Soyutlama olan IMessageService'e bağımlı olmalı.
          Başta interface neden var diyordum.Ama sonra fark ettim ki, bu yapı sayesinde e-posta mı gönderiyorum, SMS mi gönderiyorum diye kodu değiştirmeme gerek kalmıyor.Sistem sadece "mesaj gönder" diyor, nasıl gönderileceği detayını bilmiyor.
          Bu da yazılımı daha sağlam ve genişletilebilir yapıyor.

# Design Patterns(Tasarım Kalıpları)
* Singleton: Uygulama çalışırken tek bir tane nesne oluşturmak istediğimizde kullanılır.Yani sınıftan sadece 1 kez oluşturulabilir, herkes onu kullanır.
  Neden Kullanılır?
  Bellek tasarrufu sağlamak için.
  Global erişim sağlamak için.
  Loglama (Logger), Ayarlar (Config), Veritabanı bağlantısı gibi yerlerde çok kullanılır.

* Repository:Veritabanı işlemlerini servis katmanından ayırmak için kullanılan bir kalıptır.Kodun "veriyi nasıl çektiğini" gizler, sadece ne yapılmak istendiğini açıklar.
  Neden Kullanılır?
  Kodun okunabilirliği ve test edilebilirliği artar.
  Veritabanı ile iş yapan sınıfları soyutlamak kolaylaşır.
  İş mantığı (business logic) ile veritabanı kodu birbirine karışmaz.

# Clean Code(Temiz kod) Nedir?
 Kolay okunan, sade, anlaşılır ve bakımı kolay koddur. Anlamlı isimler, kısa fonksiyonlar, yorum gerektirmeyen kod = Temiz koddur.
  Kötü Kod:
   if (x == 1) { Birşeyolsun(); }
  Temiz Kod:
   if (Kullanıcıgirişyaptıysa) { ShowDashboard(); }

# Yazılım Mimari Desenleri

| Mimari                           | Kısaca Açıklama                             | Ne Zaman Kullanılır?                       |
| -------------------------------- | ------------------------------------------- | ------------------------------------------ |
| **Layered (Katmanlı)**           | UI, Business, Data katmanlarına ayrılır.    | Küçük/orta ölçekli uygulamalarda.          |
| **Clean Architecture**           | Katmanlar bağımsız, merkezde domain vardır. | Uzun ömürlü büyük projelerde.              |
| **Microservices**                | Her özellik ayrı bir servistir.             | Büyük ölçekli, dağıtık sistemlerde.        |
| **Event-Driven**                 | Bileşenler mesajlar/olaylar ile haberleşir. | Gerçek zamanlı, bağımsız sistemlerde.      |
| **Hexagonal (Ports & Adapters)** | İç mantık dış sistemlerden ayrıdır.         | Test edilebilirliği yüksek sistemler için. |

   

 
 



   
   
   
   
   
   
 


      


     

   





  
