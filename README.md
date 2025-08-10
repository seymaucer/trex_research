# 1.MODERN YAZILIM GELİŞTİRME PRATİKLERİ

## Git nedir? GitHub nedir?
  Git bir projedeki kod değişikliklerini takip etmek, farklı sürümleri yönetmek ve ekip çalışmasını kolaylaştırmak için kullanılan bir dağıtılmış versiyon kontrol sistemidir. Bu da kaynak kodun ve proje geçmişinin tam kopyasının her geliştiricinin bilgisayarında bulunduğu kontrol yöntemidir.
  Github ise Git depolarını barındıran bulut tabanlı bir platformdur.Açık kaynak projeler, ekip çalışması için kullanılır.

## Temel Git Komutları
- **Git init**: Bilgisayarımda yeni bir Git projesi başlatmak için kullanılıyor.
- **Git clone**: İnternette bir yerde bulunan bir projeyi kendi bilgisayarıma indirip üzerinde çalışabilmemi sağlıyor.
- **Git add**: Yaptığım değişiklikleri Git’e bildiriyorum. Bu komutla, dosyayı kaydedeceğim değişiklikler listesine eklemiş oluyorum.
- **Git commit**: add komutuyla hazırladığım değişiklikleri gerçekten kaydediyorum. Sanki “bunu not al” der gibi.
- **Git push**: Yaptığım bu kayıtları GitHub gibi bir uzak sunucuya yüklüyorum. Böylece başkaları da ne yaptığımı görebiliyor.
- **Git pull**: Takımda başka biri projeyi değiştirdiyse, bu komutla onların yaptığı değişiklikleri kendi bilgisayarıma alabiliyorum.
- **Git branch**: Aynı proje içinde farklı versiyonlar oluşturmamı sağlıyor. Ana projeyi bozmadan farklı şeyler deneyebiliyorum.
- **Git merge**: Farklı yollarda (branch’lerde) yapılan işleri birleştiriyor. Mesela önce ayrı çalışıp sonra her şeyi bir araya getirmek gibi düşünebiliriz.
  
  ## Merge Conflict nedir, nasıl çözülür?
  Projede aynı dosya üzerinde iki kişi farklı branch’lerde değişiklik yaparsa ve bu değişiklikler birleştirilmek istendiğinde arada çakışma olursa buna merge conflict deniyor. Git bunu otomatik olarak birleştiremiyor ve bize diyor ki: "Sen karar ver hangisi kalacak?"
  
  Çözüm adımları ise şöyledir:
   . Çakışan satırlar bu işaretlerle gösterilir: "<<<<<<< (head) ======= (main) >>>>>>> (yeni-özellik)" Hangisi kalacak, hangisi silinecek ona ben karar veriyorum.
   . Daha sonra çakışmayı manuel olarak bizim düzenlememiz gerekir.
   . Git add ile çözümü staged'e eklenir.
   . Git commit ile kaydedilip çakışmayı sonlandırıyoruz.

 ## CI/CD nedir? Azure DevOps, GitHub Actions ile pipeline örnekleri 
   Projeyi yazarken sadece kodu yazmak yetmiyor, çalışıyor mu çalışmıyor mu bunu test etmemiz gerekiyor. Sonra da her şey düzgünse, bu kodu yayına almak lazım. İşte CI/CD dediğimiz sistem bunu bizim yerimize otomatik yapıyor.
   .CI(Sürekli Entegrasyon): Ben her kod gönderdiğimde (örneğin GitHub'a push yapınca), GitHub bunu otomatik test ediyor. Kodda hata varsa anında görüyorum. Böylece daha erken fark edip düzeltebiliyorum.
   .CD(Sürekli Dağıtım): Eğer testler sorunsuz geçtiyse, bu sefer sistem kodu yayına hazır hale getiriyor, hatta bazen otomatik olarak yayına bile alıyor. Yani elle bir şey yapmamıza gerek kalmıyor.
   
 ###  GitHub actions ile .NET CI/CD 
 
name:.NET Pipeline Örneği

on:[push]
jobs:
derleme-ve-test:
runs-on:windows-latest
steps:
name: Kodları İndir
- uses: actions/checkout@v2
- uses: actions/setup-dotnet@v2
        with:
          dotnet-version: '8.0.x'
  - run: dotnet build
  - run: dotnet test


. Burada her push işlemi yapıldığında koda derleme ve test işlemi yapan pipeline örneğini yazdım.
. Windows'ta çalışması için runs-on kısmını yazdım, steps kısmında adımları tek tek gösterdim ve .NET'in son sürümünde çalışması için de kod yazdım.



## Software Development Life Cycle(SDLC)

### Yazılım Geliştirme Sürecinin Aşamaları
   
-**Planlama (Ne Yapacağız)**: İşe başlamadan önce bir yol haritası çiziyoruz. Müşteri ne istiyor, ne kadar sürede bitmeli, kaç kişiyle yapacağız gibi soruları cevaplıyoruz. Yani kafamızda her şey netleşiyor.

-**Analiz (Neye İhtiyacımız Var)**: Projede neye ihtiyacımız var, hangi özellikler olacak, hangi ekranlar kullanılacak, hangi dil/dillerle yazılacak gibi detayları konuşup netleştiriyoruz.

-**Tasarım (Nasıl Yapacağız)**: Burada projenin mimarisini kuruyoruz. Veritabanı nasıl olacak, sayfalar nasıl görünecek gibi şeyleri belirliyoruz. Önce şekli çiziyoruz, sonra koda geçiyoruz gibi düşünebilirsiniz.

-**Geliştirme (Kod Yazılır)**: Artık kod yazma kısmına geliyoruz. Geliştiriciler burada kodu yazıyor ve test ediyor.

-**Test (Her şey Düzgün Çalışıyor mu)**: Kod düzgün çalışıyor mu, hata var mı diye kontrol ediyoruz. Hataları düzeltip sistemin sorunsuz çalıştığından emin oluyoruz.

-**Dağıtım (Proje Yayınlanır)**: Her şey hazırsa, yazılım kullanıcıya sunuluyor.

-**Bakım (Proje Sonrası Destek)**: Kullanıcıdan geri bildirim alıyoruz. Yeni istekler varsa onları da ekliyoruz, varsa hataları düzeltiyoruz.

### Agile/Scrum/Kanban Metodolojileri

    Agile: Agile dediğimiz şey aslında daha esnek ve hızlı bir çalışma yöntemi. Büyük projeler yerine küçük küçük işler yapılıyor. Bir hocamız şöyle demişti: "Bu sistemde her adımda müşteriye gösterip onay almak zorundasınız." Yani sürekli iletişim hâlindeyiz.
    Scrum: Scrum'da işler belirli zaman dilimlerine (sprint) bölünüyor. Günlük mini toplantılarla herkes ne yaptığını anlatıyor. Çok düzenli bir sistem.
    Kanban: Burada işler kart şeklinde yazılıyor. Yapılacaklar, Yapılıyor, Bitti gibi bölümler oluyor. Sürekli bir akış var. Sprint gibi zaman baskısı yok.


# 2. .NET EKOSİSTEMİ

   ## .NET nedir? Tarihçesi,amacı,neden kullanılır?
     
      .NET’i ilk duyduğumda sadece "C# ile yazılım geliştirme aracı" sanmıştım. Ama araştırınca fark ettim ki .NET aslında çok daha fazlasıymış. Sadece C# değil; web siteleri, API servisleri, mobil ve masaüstü uygulamalar gibi bir sürü farklı yazılımı yapmaya imkân tanıyan, güçlü ve esnek bir platformmuş..NET, Microsoft’un geliştirdiği açık kaynaklı ve farklı platformlarda çalışabilen (yani cross-platform) bir yazılım geliştirme ortamıymış. C#, F# ve VB.NET gibi dilleri destekliyor.
      
      Bu platform sayesinde;
      - Web uygulamaları (ASP.NET)
      - Masaüstü uygulamaları (Windows Forms, WPF)
      - Mobil uygulamalar (Xamarin / MAUI)
      - Oyunlar (Unity ile C#)
      - API servisleri 
       gibi birçok yazılım geliştirilebilir.
       
       Peki neden tercih ediliyor?
       - Dil desteği gerçekten çok güçlü.
       - Visual Studio veya Rider gibi güçlü editörlerle uyumlu çalışıyor.
       - Web ve API projelerinde performansı baya iyi.
       - Bir de arkasında Microsoft olunca güven veriyor açıkçası.

## .NET Framework, .NET Core ve .NET 7/8 farkları
      
| Özellik             | .NET Framework     | .NET Core         | .NET 5+ / 6 / 7 / 8    |
|---------------------|--------------------|-------------------|------------------------|
| Platform            | Sadece Windows     | Cross-platform    | Cross-platform         |
| Performans          | Orta               | Yüksek            | Daha da yüksek         |
| Açık Kaynak         | Hayır              | Evet              | Evet                   |
| Kullanım Durumu     | Eski projelerde    | Aktif             | En güncel yapı         |


 ## dotnet --info çıktısı örneği ve yorumlama
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

  **Senkronda** Her işlem sırayla yapılır bir iş bitmeden diğerine geçilemez.Basit uygulamalarda kullanılır.

```csharp
public string KullaniciyiGetir()
{
Thread.Sleep(3000);
return "Kullanıcı bilgisi";
}
```

  *kullanıcı bilgileri alınırken 3 saniye bekletir.Bekleme bitene kadar işlem yapılmaz.

**Asenkron** da ise tam tersi beklerken başka işlerde yapılabilir.Web API, veri çekme işlemleri yapılır.

```csharp
public async Task<string> KullaniciGetirAsync()
{
    await Task.Delay(3000);
    return "Kullanıcı bilgisi";
}
```

  
    *bekleme olurken programın diğer işleri devam eder.Kullanıcı deneyimi çok daha yüksektir.

**anahtar kavramlar**
  - Async: Bir metodun asenkron çalışacağını söylüyoruz. Yani işlemi başlatıyoruz ama beklemiyoruz.
  - Await: Asenkron işin sonucunu beklememizi sağlıyor. Yani "bu bitsin, sonra devam et" gibi düşünebilirsin.
  - Task: Asenkron işlemin temsilcisi gibi. Bir tür veri tipi yani.
  - ConfigureAwait: UI’ya ya da bulunduğun ortama bağlı olmadan çalışması için kullanılıyor. Özellikle mobil veya arka plan işleri için önemli oluyormuş.
  
 ## C# Arrow Function
  Bu ifade lambda fonksiyonu olarak geçer. Derste hocamız kodları kısaltmak daha hızlı kısa kod olarak açıklamıştı lambda fonksiyonu.

```csharp
List<int> sayilar = new List<int> { 1, 2, 3, 4, 5 };
var ciftSayilar = sayilar.Where(sayi => sayi % 2 == 0).ToList();
```
  
    *sayı çift mi? diye sorgulayan kısa bir fonksiyon var burda da.

# 3. BACKEND GELİŞTİRME TEMELLERİ

 ## -Backend Nedir?Frontend ile Farkları

   *Backend: Uygulamanın kullanıcı tarafından görünmeyen kısmı. Veritabanı, API'ler, hesaplamalar yani arka planda dönen bütün olaylar burada dönüyor.
   *Frontend: Kullanıcının ekranda gördüğü kısım. Web sitesinin tasarımı, butonlar, menüler falan hep burada.
   
## Web Sunucusu Nedir?API Nedir?API Türleri

 -**Web sunucusu**: Web sunucusu dediğimiz şey, internette kullanıcıdan gelen isteklere cevap veren yazılım. Mesela bir kullanıcı web sitesini açınca, aslında web sunucusu o sayfayı alıp tarayıcıya gönderiyor.
-**API**: API'yi de şöyle düşünebiliriz: iki farklı yazılımın birbiriyle konuşmasını sağlayan aracı. Yani bir program başka bir sistemden veri çekmek veya işlem yaptırmak istiyorsa, bunu API üzerinden yapıyor.

  -API Türleri:
  
     . Rest API: En çok kullanılan API türü. HTTP üzerinden çalışıyor. Get, Post gibi metotlarla veri gönderip alıyoruz. JSON formatında çalışıyor genelde.
     . Soap API: XML tabanlı. Veri taşımak için ama biraz daha kurallı ve katı. Özellikle bankacılık sistemlerinde hâlâ kullanılıyormuş.
     . GraphQL API: Sadece ihtiyaç olan veriyi çekmeye yarıyor. Çok fazla veriyle uğraşırken işe yarıyor çünkü fazlalık çekmiyorsun.
     . gRPC: Google geliştirmiş. Binary veri taşıyor. Yani performans ve hız açısından çok iyi.


## HTTP Nedir? HTTP Metodları
  HTTP, tarayıcıyla sunucu arasında veri alışverişini sağlayan bir iletişim dili gibi düşünebiliriz. API’lerle çalışırken sık sık HTTP metotlarını kullanıyoruz.

- **Metodlar**
  
  .Get:Veri almak için kullanılır.

```csharp
[HttpGet]
public List<Ogrenci> TumOgrencileriGetir()
{
    return ogrenciServisi.HepsiniGetir();
}
```

  .Post:Yeni veri eklemek için.

```csharp
[HttpPost]
public IActionResult YeniOgrenciEkle([FromBody] Ogrenci yeniOgrenci)
{
    ogrenciServisi.Ekle(yeniOgrenci);
    return Ok();
}
```


  .Put:Var olan veriyi tamamen güncellemek için kullanılır.

```csharp
[HttpPut("{id}")]
public IActionResult Guncelle(int id, [FromBody] Ogrenci guncelOgrenci)
{
    ogrenciServisi.Guncelle(id, guncelOgrenci);
    return Ok();
}
```

  .Delete:Veri silmek için kullanılır.

 ```csharp
[HttpDelete("{id}")]
public ActionResult Sil(int id)
{
    ogrenciServisi.Sil(id);
    return Ok();
}
```
 

## RESTful Servislerin Çalışma Mantığı
   Basit ve URL tabanlı bir API mimarisidir.Amacı her şeyi basit, standart ve okunabilir yapmak.
   Her işlem için anlamlı bir URL olur.
   GET,POST,PUT,DELETE gibi HTTP metodları kullanılır.
   JSON formatı ile veri alışverişi yapılır.

 ## -REST vs SOAP vs GraphQL
 
| Özellik      | REST                     | SOAP             | GraphQL                 |
| ------------ | ------------------------ | ---------------- | ----------------------- |
| Veri Formatı | Genellikle JSON          | XML              | JSON                    |
| Hız          | Hızlı                    | Ağır             | Hızlı                   |
| Esneklik     | Orta                     | Düşük            | Çok Yüksek              |
| Öğrenme      | Kolay                    | Zor              | Orta                    |
| Kullanım     | Güncel sistemlerde sıkça | Eski sistemlerde | Yeni projelerde popüler |


## JSON Veri Formatı ve Kullanım Amacı
JSON, veriyi taşımak ve saklamak için kullanılan bir formattır. Eskiden XML kullanılıyormuş ama artık çoğu sistem JSON kullanıyor.

 -  Kullanım Amaçları:
   
    * API’lerle veri gönderip almak çok kolay oluyor.
    * Veritabanıyla iletişim kurmak için kullanılıyor.
    * Hızlı ve sade bir format, fazla detayla uğraştırmıyor.
    
**Örnek JSON**:
 Kullanıcı giriş yaparken bu bilgileri girer ve bu bilgiler API'ye gönderilir.Gönderilen JSON ise budur:

```json
{
  "email": "aylin@gmail.com",
  "sifre": "Aylin1234!"
}
```

 Sunucu json'u alır ve düşünür böyle bir kullanıcı var mı şifresi doğru mu diye.Eğer doğruysa şu şeklde bir JSON ile cevap gönderilir:

```json
{
  "mesaj": "Giriş başarılı",
  "kullaniciAdi": "Aylin",
  "token": "ab123abc456xyz789",  
  "sonGiris": "2025-08-08"
}
```

  **Ayrıca sunucu giriş başarılı olduğunda kullanıcıya özel bir token verir.Dijital anahtar,id gibi düşünebiliriz aslında.Yani token saklanır ve tekrar giriş yapmana gerek kalmaz çünkü o id ile seni tanır.
  

# 4.ASP.NET

## ASP.NET ve ASP.NET core nedir?Avantajları Farkları 

  ASP.NET: Microsoft’un geliştirdiği bir framework yani yazılım iskeleti gibi düşünebiliriz. Web uygulamaları yapmamızı sağlıyor ama klasik ASP.NET sadece Windows ortamında çalışıyor.
  ASP.NET Core: Sonra Microsoft, Hadi biz bunu daha hızlı, açık kaynak ve her platformda çalışabilir hale getirelim demiş ve böylece ortaya ASP.NET Core üretilmiş.

- **ASP.NET Core'un Avantajları**:
  .Daha hızlı ve performanslı
  .Cross-platform (Windows’a bağımlı değil)
  .Açık kaynak
  .Daha hafif ve modern yapı

## MVC Nedir? Ne için Kullanılır?
 ASP.NET projelerinde sık kullanılan bir tasarım desenidir.Açılımı Model-View-Controller'dir.
 
 Model: Verileri temsil eden kısım. (Yani "bu ürün nedir", "kullanıcının adı ne" gibi bilgiler burada tutuluyor.)
 
 View: Kullanıcının gördüğü sayfa.Yani tasarım kısmı
 
 Controller: Kullanıcıdan gelen istekleri alır, işin mantığını yönetir, View’a gönderir.

 Bu üçlü yapı sayesinde her şey düzenli duruyor. Kodlar karışmıyor çünkü herkes kendi işini yapıyor. Hem yazmak hem bakım yapmak çok daha kolay oluyor.

## Middleware Nedir?Nasıl Çalışır?
 Middleware dediğimiz şey, bir istek (request) geldiğinde ve cevabı (response) dönmeden araya giren küçük yazılım parçacıkları.

Yani kullanıcı bir sayfaya gitmek istediğinde bu istek, sunucuya ulaşmadan önce bu middleware’lerden geçiyor. Sanki kapılardan geçer gibi. Her kapıda bir görevli var, bakıyor:
“Giriş yaptı mı?”, “Yetkisi var mı?”, “Log tutayım mı?”, “Bir sorun var mı?” gibi.

 
### Middleware sıralaması(Program.cs içinde)
   
  **İlk önce anlamak için yapay zekaya gerçek hayat örneği vermesini istedim. Ve bana bir kafeye gitmek gibi olduğunu söyledi ve çok açıklayıcı oldu bana.Örneğin;
  
 - Girişte güvenlik var → Hata var mı?
 - Maskeni taktın mı, ateşin ölçüldü mü? → HTTPS + güvenlik kontrolü
 - Menüye göz atıyorsun → Statik dosyalar
 - Garson geldi "Ne alırsınız?" dedi → Routing
 - "Rezervasyonun var mı?" → Authentication
 - "VIP bölüm mü? Normal mi?" → Authorization
 - Sipariş geldi → Controller çalıştı

**Program.cs içinde middleware örneği**

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();
   app.UseExceptionHandler("/Home/Error");  (Mesela sistem patladı diyelim. Kodu yazan geliştirici bir yerde hata yaptı. İşte kullanıcıya siyah ekran vermeyelim diye onu şık bir Bir sorun oluştu sayfasına yönlendiriyoruz.)
   
   app.UseHttpsRedirection();   (HTTP güvensiz olabilir o yüzden HTTPS 'ye çeviriyoruz.)
   
   app.UseStaticFiles();     (Web sitesinde logo, stil dosyaları (CSS) veya animasyonlar varsa, bu satır sayesinde kullanıcı bunları görebiliyor.)
   
   app.UseRouting();         (Bu satır kullanıcı URL’de ne yazdıysa onu anlayayım kısmı. Mesela /hakkimizda direkt hakkımızda kısmına yönlendiriyor demek oluyor.)
   
   app.UseAuthentication();   (Bu satır kullanıcı sisteme giriş yapmış mı onu kontrol ediyor. Yani kullanıcı giriş yaptı mı?Yaptıysa gerçekten o mu?)
   
   app.UseAuthorization();     (Kullanıcı giriş yapmış olabilir ama her yere giremez Mesela admin sayfası sadece admin'lere açık olur. Bu satır da Bu kişinin yetkisi var mı? diye bakıyor.)
   
   app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");  (En sonunda artık her şey hazır. Kullanıcının istediği sayfa çalıştırılıyor. Mesela anasayfa mı istiyor O zaman HomeController içindeki Index çalışıyor.)

app.Run();   (Uygulama çalışıyor.)
```
   
## Dependency Injection(DI) nedir? neden önemlidir?
   Bir sınıfın ihtiyacı olan başka sınıfları kendi içinde oluşturmak yerine dışarıdan almasıdır.Diyelim ki bir kahve makinesine süt ve kahve gerekiyo makine kendi alıyosa sıkıntı ama biri gelip koyuyosa bu dependency ınjection oluyor.Çünkü makine sadece kahveyi yapar.
   
  **DI Örnek**:

- Burada sadece bir iş yapılıyor o da mesajı hazırlamak.

```csharp
public class SelamServisi
{
    public string MesajHazirla()
    {
        return "Merhaba, iyi günler!";
    }
}
```

  -Selamci sınıfı mesajı hazırlamıyor sadece dışardan aldığı Selamservisi sınıfını kullanıyor.Yani selamci sadece mesajı nasıl göndericeğini biliyor mesajın içeriği hakkında bilgisi yok.Yani kendi işine odaklanıyor,bağımlı değil DI'da burda devreye giriyor.

```csharp
public class Selamci
{
    private SelamServisi _servis; 

    public Selamci(SelamServisi servis)
    {
        _servis = servis;
    }

    public void SelamVer()
    {
        string mesaj = _servis.MesajHazirla(); 
        Console.WriteLine(mesaj);
    }
}
```


-Burada ilk olarak bir SelamServisi nesnesi oluşturuyoruz.Sonra bunu Selamci sınıfına constructer ile veriyoruz(new metodu ile).En son SelamVer() metodunu çağırıp mesajı basmış oluyoruz.

```csharp
class Program
{
    static void Main(string[] args)
    {
        SelamServisi servis = new SelamServisi(); 
        Selamci selamci = new Selamci(servis);   

        selamci.SelamVer(); 
    }
}
```

   
 
 ## Katmanlı Mimari
  Katmanlı mimari,bir uygulamayı görevlerine göre katmanlara ayırarak yazmamızı sağlar.Kodlar daha düzenli olur,her katman sadece kendi işiyle ilgilenir,test etmek ve bakım kolay olur böylece.
  
  ### Temel 3 Katman 
  
  **Presentation Katmanı**(Sunum)
   - Kullanıcının gördüğü yer.
   - Web sayfası,butonlar.
   
  **Business Katmanı**(İş kuralları)
   -Uygulamanın mantığını,hesaplamalarını,kurallarını içerir.
   -Eğer stok 0 ise ürün satılamaz gibi bir kural varsa burda kontrol edilir.

   **Data Access Katmanı**(Veri erişim)
   -Veri tabanına veri ekleme, silme, güncelleme işini yapar.
   -SQL yazılmaz,entity framework gibi orm(nesne-ilişki eşleme) araçları kullanılır.
   
   
 **Service & Repository Pattern**
   - Service: Business katmanında iş yapan sınıftır. (Kural koyar)
   - Repository: Data Access katmanında veriye erişen sınıftır. (Veri alır/verir)
   - Avantajı: Kodlar daha test edilebilir, katmanlar ayrılmış olur.
   
   ## Temiz Mimari
    Bu mimari, yazılım dünyasında biraz daha profesyonel bir yapı. Katmanlar daha detaylı ve iç içe geçmez.

   ### Katmanlar:

   **Domain Katmanı**
   -Uygulamanın çekirdeği.
   -kurallar,sınıflar,arabirimler burada.
   -Bu katman hiçbir şeye bağımlı değil. En saf, en sade hali

   **Application Katmanı**
   -Kullanıcı ne istiyor, nasıl yapacağız?
   -Use Case’leri (iş akışları) burada yazılır.

   **Infrastructure Katmanı**
   -Veritabanı, e-posta gönderimi, dosya işlemleri gibi altyapı işleri burada.

   **API Katmanı**
   -Kullanıcının istek gönderdiği yerdir.
   -ASP.NET Core API Controller’lar burada yer alır.

  ## Bağımlılıkların Dışa Akması
    İçteki katmanlar, dıştaki katmanlara bağımlı olmaz.
    Domain Infrastructure'i bilmez ama Infrastructure Domain'i tanır.
    Çünkü iş mantığı her şeyden önemlidir. Veritabanı değişebilir, e-mail servisi değişebilir ama kural değişmez.


   ## Katmanlı Mimari


         [Kullanıcı / Tarayıcı]
                   │
                   ▼
    ┌────────────────────────────────────┐
    │        Presentation Katmanı        │
    │   (Kullanıcının gördüğü yer)       │
    │   → UI, Controller, Razor, API     │
    └────────────────────────────────────┘
                   │ çağırır
                   ▼
    ┌────────────────────────────────────┐
    │          Business Katmanı          │
    │  (İş mantığı, servisler, kurallar) │
    │  → Validasyonlar, hesaplamalar     │
    └────────────────────────────────────┘
                   │ çağırır
                   ▼
    ┌────────────────────────────────────┐
    │        Data Access Katmanı         │
    │ (Veritabanına erişim kısmı)        │
    │ → EF Core, SQL, Repository         │
    └────────────────────────────────────┘
                   │ erişir
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
    

# 5. VERİTABANI VE ORM
  SQL dediğimiz şey, ilişkisel veritabanıyla konuşmamızı sağlayan bir dil. Yani veri eklemek, silmek, güncellemek, aramak gibi işlerimizi bu dil sayesinde yapıyoruz. Normalde veritabanına tek tek komut yazarak ulaşabiliriz ama işin içine ORM girince işler kolaylaşıyor.

## İlişkisel vs İlişkisel Olmayan Veritabanları
    
| Özellik             | İlişkisel (Relational)         | İlişkisel Olmayan (NoSQL)  |
| ------------------- | ------------------------------ | -------------------------- |
| Veri Yapısı         | Tablo                          | JSON, belge, anahtar-değer |
| Örnek Veritabanları | SQL Server, PostgreSQL         | MongoDB, Firebase, CouchDB |
| İlişki Desteği      | Var                            | Genelde yok                |
| Şema (Schema)       | Sabit                          | Esnek                      |
| Performans          | Karmaşık işlemlerde daha güçlü | Büyük veri için daha hızlı |


## ORM Nedir?
  ORM (Object Relational Mapping), veritabanına SQL yazmadan, C#, Java, Python gibi dillerle işlem yapmamızı sağlıyor.
Ben mesela Entity Framework Core kullanarak, SQL sorgusu yazmadan db.Products.Add() diyerek veri ekleyebiliyorum. Bu sayede hem kod okunaklı oluyor hem de SQL hatası yapma ihtimalim azalıyor.


## DbContext Nedir?
  Entity Framework Core’un kalbi diyebilirim. Veritabanındaki tabloları temsil ediyor ve onlarla konuşmamızı sağlıyor.
Bunu bir köprü gibi düşünebilirz: Kod tarafındaki sınıflarımız ile veritabanındaki tabloları birbirine bağlıyor.


```csharp
public class OkulDbContext : DbContext
{
    public DbSet<Ogrenci> Ogrenciler { get; set; }
    public DbSet<Ders> Dersler { get; set; }
}

public class Ogrenci
{
    public int Id { get; set; }
    public string Ad { get; set; }
    public string Soyad { get; set; }
    public int Yas { get; set; }
}

public class Ders
{
    public int Id { get; set; }
    public string DersAdi { get; set; }
    public int Kredi { get; set; }
}
```


    *OkulDbContext bizim veritabanıyla konuştuğumuz yer.
    *Ögrenciler tablosu ve Dersler tablosu otomatik oluşuyor.
    *Ögrenci sınıfındaki her özellik (Ad, Soyad, Yas) veritabanında sütun olarak yer alıyor.
    *Ders sınıfı da derslerin bilgilerini tutuyor.



   
## LINQ Nedir?
 LINQ (Language Integrated Query) dediğimiz şey, hem koleksiyonlarda (listeler, diziler vs.) hem de veritabanında sorgu yazmayı kolaylaştıran bir özellik.
SQL komutları yazmak yerine C# içinde direkt nokta (.) ile sorgu yazabiliyoruz. Kod daha okunaklı oluyor, hem de tek bir dil üzerinden gidiyoruz.

    
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


 .Code-First’te önce kodu yazıyorsun, sonra veritabanı o koda göre oluşuyor.
 .Database-First’te ise zaten hazır bir veritabanın var, kodu ona göre üretiyorsun.
 .Ben yeni projelerde genelde Code-First kullanırım, çünkü esnek.


## 4 Temel SQL Sorgusu Örneği
 **Select**: SELECT * FROM Ogrenciler; (Öğrenciler tablosunu listeler.Yani verileri göstermeye yarar.)
 
 **Insert**: INSERT INTO Ogrenciler (Ad, Soyad, Yas) VALUES ('Ayşe', 'Yılmaz', 21); (Ayşe yılmaz adında 21 yaşında bir öğrenciyi öğrenciler tablosuna eklemeye yarar.)
 
 **Update**: UPDATE Ogrenciler SET Yas = 22 WHERE Ad = 'Ayşe' AND Soyad = 'Yılmaz'; (Ayşe yılmaz'ın yaşını 22 olarak günceller.)
 
 **Delete**: DELETE FROM Ogrenciler WHERE Ad = 'Ayşe' AND Soyad = 'Yılmaz'; (Ayşe Yılmaz adındaki öğrenciyi tablodan kaldırır.)


# 6.GÜVENLİK VE PERFORMANS

  ## Authentication vs Authorization
**Authentication (Kimlik Doğrulama)**: “Sen kimsin?” sorusunun cevabı.
Giriş yaptıysan authenticated oluyorsun. Yani sistem seni tanıyor.
  Örnek: Kullanıcı adı ve şifreyle giriş yaptığında “Evet, bu kişi Hakan” diye onaylanmak.

**Authorization (Yetkilendirme)**: “Nereye girebilirsin, ne yapabilirsin?” sorusunun cevabı.
Sisteme giriş yaptıktan sonra, admin paneline erişebiliyorsan authorized oluyorsun.
  Örnek: Normal kullanıcı sisteme girer ama admin panelini göremez; admin görebilir.

  ## JWT (JSON Web Token) Nedir?
  JWT’yi ilk öğrendiğimde kafamda direkt “dijital giriş bileti” gibi canlandı. Kullanıcı sisteme giriş yaptığında sunucu sana bir token veriyor. Bu token şifrelenmiş ve güvenli bir şekilde kimliğini taşıyor.
  
    3 parçadan oluşur:
    -Header: Hangi algoritma ve token tipi kullanılacak, bu kısımda yazıyor.
    -Payload: Kullanıcıya ait bilgiler, mesela ID ya da kullanıcı adı.
    -Signature: Gizli anahtarla imzalanmış bölüm, bu sayede token’ın sahte olup olmadığı anlaşılabiliyor.

     Bana göre JWT’nin olayı şu: Parola her istekte tekrar gönderilmiyor, onun yerine bu “giriş bileti” kullanılıyor. Böylece hem güvenlik hem de hız açısından avantaj sağlanıyor.
     
  ## OAuth, OAuth2.0, OpenID, OpenIddict Nedir?
   
| Teknoloji      | Açıklama                                                                      |
| -------------- | ----------------------------------------------------------------------------- |
| **OAuth**      | Yetki verme protokolü (şifresiz erişim izni sağlar)                           |
| **OAuth2.0**   | OAuth’un gelişmiş sürümü, günümüzde yaygın                                    |
| **OpenID**     | Kimlik doğrulama sağlar ("bu kullanıcı kim?")                                 |
| **OpenIddict** | ASP.NET Core’da OpenID destekli kimlik doğrulama ve yetkilendirme kütüphanesi |


   -kısaca-
   -OpenID Authentication sağlar.
   -OAuth Authorization sağlar.

## Performans Artırma Teknikleri 
  Performans konusu bence hem kullanıcı deneyimi hem de sistemin sağlığı için kritik. Ben araştırırken özellikle Entity Framework’te yapılabilecek birkaç yöntemi not aldım:
  
**AsNoTracking()**:
 Normalde EF, sorgudan gelen verileri takip ediyor ki ileride değiştirirsen kaydedebiliriz. Ama sadece veri görüntüleyeceksek bu gereksiz.
AsNoTracking() kullanınca bu takip kapanıyor, performans artıyor.

**IAsyncEnumerable**:
 Bu özellik sayesinde veriler “parça parça” çekiliyor. Yani hepsini bir anda belleğe yüklemiyoruz.
Büyük veri setlerinde özellikle bellek tasarrufu sağlıyor.
Await foreach ile kullanılıyor, veri geldikçe işlem yapabiliyorsun.

**Caching (Önbellekleme)**:
 Sık kullanılan verileri bellekte saklıyoruz. Böylece her seferinde veritabanına gitmeye gerek kalmıyor.
Bu, hem sorgu sayısını hem de yükü ciddi anlamda azaltıyor.
Mesela anasayfadaki kategori listesi sürekli değişmiyorsa cache’e almak mantıklı.

**Profiling**:
 Uygulamanın nerede yavaşladığını bulmak için kullanılıyor.
MiniProfiler gibi araçlar, hangi sorguların uzun sürdüğünü ve hangi sayfanın ağır çalıştığını gösteriyor.
Geliştirme sırasında çok işe yarıyor çünkü sorunları anında tespit edebiliyoruz.

## OWASP Top 10
OWASP (Open Web Application Security Project) aslında dünya çapında bir topluluk.
Bunlar web uygulamalarında en sık görülen güvenlik açıklarını listeleyip geliştiricilerin dikkat etmesi gereken konuları belirtiyorlar.
En popüler listesi “OWASP Top 10” olarak geçiyor.


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

**SQL Injection'a karşı koruma:** SQL Injection, veritabanına zararlı kod enjekte etme olayı.
Bunu önlemenin en kolay yolu, Entity Framework Core ile parametreli sorgular kullanmak.
Yani kullanıcıdan gelen veriyi doğrudan SQL’e yapıştırmak büyük risk oluşturur.

**XSS(Cross-Site Scripting) saldırılarına karşı:** XSS dediğimiz olay, kullanıcıya zararlı JavaScript kodu çalıştırmak.
Razor sayfaları bu konuda güzel, çünkü gelen veriyi otomatik encode ediyor, yani HTML olarak çalıştırmıyor.
Ama JavaScript içinde kullanıcıdan gelen bir veri kullanacaksam, ekstra olarak HtmlEncoder.Default.Encode() ile güvenli hale getirmem gerektiğini öğrendim.
Bunu da “Kullanıcıdan gelen veri, dokunmadan tarayıcıya dönmez” diye aklıma yazdım.
     
**CSRF (Cross Site Request Forgery) Önlemi:** Bu saldırı türünde kullanıcı farkında olmadan sistemde işlem yapıyor.
ASP.NET Core burada da kolaylık sağlıyor:
Formlarda otomatik gelen @Html.AntiForgeryToken() koruma sağlıyor.
POST isteklerinde [ValidateAntiForgeryToken] attribute’u eklemek gerekiyor.
Kendi kendime “Token’sız POST olmaz” diye not aldım.

**Kimlik Doğrulama ve Yetkilendirme (Broken Auth)**: Kullanıcı kimliği doğru doğrulanmalı ve sadece yetkili olduğu alanlara erişebilmeli.
   ASP.NET Identity kullanmak güvenli bir yöntem.
   Şifre politikası oluşturulmalı (mesela en az 6 karakter, büyük harf, özel karakter).
   JWT token kullanılıyorsa süresi (expires) belirlenmeli ve zamanında yenilenmeli.
Bunu da “Doğrula, yetkilendir, ama fazla kapı açma” diye kafama yazdım.
      
**Model Doğrulama (Validation):** Kullanıcıdan gelen veriler önce model üzerinde kontrol edilmeli.Böylece hem saçma veriler hem de güvenlik açıkları sisteme girmez.

**Input Sanitization (Girdi Temizleme):** Eğer kullanıcıdan HTML alacaksam, direkt kaydetmek yok.
Bunun için güvenli HTML parser ya da HtmlSanitizer gibi kütüphaneler kullanılmalı.
Bunu da “<script> gördün mü, temizle!” diye kendime yazdım.


# 7.LOGGING VE HATA YÖNETİM
 Ben bu konuyu araştırırken fark ettim ki loglama, yazdığımız uygulamanın geçmişini tutmak gibi bir şey. Yani uygulama aslında kendi günlüğünü yazıyor.
İlk başta her şeyi mi kaydediyoruz diye düşündüm ama öğrendim ki hayır, her şey loglanmaz; önem derecesine göre seviyeler var.
       
**Neden Loglama Yapılır?**
  -Uygulamanın geçmişte ne yaptığını izlemek için
  -Hata olduğunda neden olduğunu bulmak için
  -Canlı sistemde sorunları hızlıca teşhis edebilmek için
  -Kullanıcının yaptığı işlemleri kayıt altına almak için
         
        
| Seviye          | Açıklama                                                                  |
| --------------- | ------------------------------------------------------------------------- |
| **Trace**       | En detaylı log. Genelde sadece geliştirme ortamında kullanılır.           |
| **Debug**       | Hataları bulmak için kullanılan geliştirici logları.                      |
| **Information** | Uygulamanın yaptığı önemli işlemler (örneğin: kullanıcı giriş yaptı).     |
| **Warning**     | Kritik değil ama dikkat edilmesi gereken durumlar (örneğin: stok azaldı). |
| **Error**       | Hata oldu ama sistem çalışmaya devam ediyor.                              |
| **Critical**    | Ciddi hata. Sistem çalışamayabilir.                                       |

      
## ASP.NET Core'da Logging Nasıl Yapılır?
  Ben bu konuyu araştırırken şunu fark ettim: ASP.NET Core zaten içinde hazır bir logging (log tutma) sistemiyle geliyor. Yani dışarıdan ekstra bir kütüphane eklemeden bile log tutmaya başlayabiliyoruz.
  
Bu altyapı sayesinde:
-Hangi olay ne zaman olmuş öğrenebiliriz.
-Hangi metod çalışmış, hangi hatalar alınmış görebiliriz.
-Geliştiriciler olarak uygulamayı izleyebilir, hata ayıklayabilir ve sorunları tespit edebiliriz.

## Global Exception Handling
 Bazı durumlarda uygulama patlayabiliyor ve kullanıcıya sadece “500 Server Error” gibi çirkin bir mesaj çıkıyor. Burada Global Exception Handling devreye giriyor.
Amacı: Tüm hataları yakalamak ve kullanıcıya daha düzgün, özel bir hata sayfası göstermek.

 ## UseExceptionHandler ve ILogger nasıl kullanılır?

**UseExceptionHandler:** Sistemde bir hata olursa,
Kullanıcıya çirkin sistem hatası gösterilmez,
Onun yerine kullanıcı özel bir hata sayfasına yönlendirilir.

```csharp
if (!uygulama.Ortam.GelistirmeModu())
{
    uygulama.HataYakalayici("/AnaSayfa/Hata");
}
```


    *Error adında bir sayfa varsa tüm hatalarda o sayfa gösterilicek demektir.
 
 **ILogger:**  Bu da uygulamanın log (kayıt) tutma işini yapar. Hangi controller ne zaman çalıştı, hangi işlem ne hata verdi gibi bilgileri yazdırır. 
 
  '''csharp
    public class AnaSayfaDenetleyici : Controller
{
    private readonly IGunlukKayitlayici<AnaSayfaDenetleyici> _gunluk;

    public AnaSayfaDenetleyici(IGunlukKayitlayici<AnaSayfaDenetleyici> gunluk)
    {
        _gunluk = gunluk;
    }

    public IActionResult AnaSayfa()
    {
        _gunluk.BilgiKaydet("Ana sayfa yüklendi.");
        return View();
    }

    public IActionResult Hata()
    {
        _gunluk.HataKaydet("Bir hata oluştu.");
        return View();
    }
}
'''

-IGunlukKayitlayici<T>: Belirli bir sınıf için log kaydı tutar.
-BilgiKaydet(): Bilgi mesajı yazar (Ana sayfa yüklendi.)
-HataKaydet(): Hata mesajı yazar (Bir hata oluştu.)


### Örnek Hata Yönetim kodu 
 ASP.NET Core’da bir işlem sırasında hata olursa, bunu kullanıcıya çirkin bir hata mesajı olarak göstermek yerine yakalayıp loglamak isteriz. Bunun için try-catch bloğu ve ILogger kullanılır.
 
```csharp
public IActionResult Detay(int id)
{
    try
    {
        var urun = _db.Products.Find(id);
        return View(urun);
    }
    catch (Exception ex)
    {
        _logger.LogError(ex, "Ürün detayları alınırken hata oluştu.");
        return View("Hata");
    }
}
```


  * try bloğuna hata oluşabilcek kod yazılır.
  * catch bloğu hata olursa çalışıcak yerdir.
  * _logger.LogError kısmı ise hatayı kayıt altına alır.
  * return view("Hata") burda hata sayfası gösterilir böylece sistem çökmemiş olur.

 
# 8.YAZILIM GELİŞTİRME PRENSİPLERİ

## SOLID Prensipleri
 Bu konuyu araştırırken fark ettim ki SOLID prensipleri aslında yazılımın sağlam, esnek ve kolay değiştirilebilir olması için oluşturulmuş kurallar.
 
**Single Responsibility(tek sorumluluk)**
 Bir sınıf sadece tek bir iş yapmalı.
Eğer sınıfın içinde hem veri tabanı işlemi hem yazdırma hem de hesaplama varsa bu prensip bozulmuş oluyor.

```csharp
public class FaturaYazdirici
{
    public void Yazdir(Fatura fatura)
    {
    }
}
```  

   -Sadece yazdırma işi yapar.
  
**Open/Closed**
 Kod genişletmeye açık, değiştirmeye kapalı olmalı.
Yani yeni özellik eklemek için eski kodu bozmak zorunda kalmamalıyız.

```csharp
public interface Indirim
{
    double Uygula(double fiyat);
}

public class OgrenciIndirimi : Indirim
{
    public double Uygula(double fiyat) => fiyat * 0.9;
}
```  
    
    - Burada yeni bir indirim eklemek istersem sadece yeni bir sınıf yazarım, mevcut kodu değiştirmem.

**Liskov Substitution**
  Türeyen sınıflar, ana sınıfın yerine geçebilmeli.
  -Kuş sınıfı varsa, Güvercin:Kuş sınıfı da aynı şekilde davranabilmeli.

**Interface Segregation**
  Kullanmayacağımız metodlarla dolu büyük arayüzler yerine, küçük ve amaca yönelik arayüzler kullanılmalı.
  
```csharp
public interface Yazdirilabilir
{
    void Yazdir();
}
```  

    - Interface'ler sayesinde farklı sınıflara aynı davranışı kazandırabiliyoruz.Yazdirilabilir gibi arayüzler, kodun daha esnek ve genişletilebilir olmasını sağlıyor.
Gerçek dünyada “her yazdırılabilir nesne” bu interface’i kullanabilirmiş gibi düşünebiliriz.

**Dependency Inversion**
 Sınıflar,somut değil soyut şeylere bağlı olmalı.
 
```csharp
public interface MesajServisi
{
    void Gonder();
}

public class EpostaServisi : MesajServisi
{
    public void Gonder()
    {
       E-posta gönderme islemi
    }
}
```  

      - Uygulama somut sınıfa (EmailService) bağımlı olmamalı.
      -  Soyutlama olan IMessageService'e bağımlı olmalı.
      -  Başta interface neden var diyordum.Ama sonra fark ettim ki, bu yapı sayesinde e-posta mı gönderiyorum, SMS mi gönderiyorum diye kodu değiştirmeme gerek kalmıyor.Sistem sadece "mesaj gönder" diyor, nasıl gönderileceği detayını bilmiyor.
       Bu da yazılımı daha sağlam ve genişletilebilir yapıyor.

## Design Patterns(Tasarım Kalıpları)

**Singleton:** program çalışırken aynı sınıftan sadece tek bir tane nesne oluyor. Mesela log tutmak için her seferinde yeni nesne oluşturmak yerine bir tane yapıyorsun, herkes onu kullanıyor. Hem hafızayı boşuna doldurmuyorsun hem de işler daha düzenli oluyor.

  -Neden Kullanılır?
  .Bellek tasarrufu sağlamak için.
  .Global erişim sağlamak için.
  .Loglama (Logger), Ayarlar (Config), Veritabanı bağlantısı gibi yerlerde çok kullanılır.

**Repository:** Aslında veritabanıyla uğraşırken iş mantığını ve veri çekme işlemlerini birbirinden ayırıyor. Yani “hangi veriyi nasıl çekeceğim” kısmını gizleyip sadece “ne yapacağım” kısmını yazıyorsun. Kod daha düzenli oluyor, test etmek de kolaylaşıyor.

  -Neden Kullanılır?
  .Kodun okunabilirliği ve test edilebilirliği artar.
  .Veritabanı ile iş yapan sınıfları soyutlamak kolaylaşır.
  .İş mantığı (business logic) ile veritabanı kodu birbirine karışmaz.

## Clean Code(Temiz kod) Nedir?
 Kısaca kodun karışık olmaması, okununca hemen anlaşılması lazım. Mesela değişken isimleri saçma sapan olursa kimse anlamaz, ama anlamlı isim verince hem sen hem başkası rahat ediyor.

```csharp
const int GecmeNotu = 50;

if (puan > GecmeNotu)
{
Console.WriteLine("Geçti");
}
```


  
## Yazılım Mimari Desenleri

| Mimari                           | Kısaca Açıklama                             | Ne Zaman Kullanılır?                       |
| -------------------------------- | ------------------------------------------- | ------------------------------------------ |
| **Layered (Katmanlı)**           | UI, Business, Data katmanlarına ayrılır.    | Küçük/orta ölçekli uygulamalarda.          |
| **Clean Architecture**           | Katmanlar bağımsız, merkezde domain vardır. | Uzun ömürlü büyük projelerde.              |
| **Microservices**                | Her özellik ayrı bir servistir.             | Büyük ölçekli, dağıtık sistemlerde.        |
| **Event-Driven**                 | Bileşenler mesajlar/olaylar ile haberleşir. | Gerçek zamanlı, bağımsız sistemlerde.      |
| **Hexagonal (Ports & Adapters)** | İç mantık dış sistemlerden ayrıdır.         | Test edilebilirliği yüksek sistemler için. |

   

 
 



   
   
   
   
   
   
 


      


     

   





  
