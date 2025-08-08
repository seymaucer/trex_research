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
 
    yaml

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
 
public string KullaniciGetir()

   {
    Thread.Sleep(3000);  
    return "Kullanıcı bilgisi"; 
   }

  *kullanıcı bilgileri alınırken 3 saniye bekletir.Bekleme bitene kadar işlem yapılmaz.

**Asenkron** da ise tam tersi beklerken başka işlerde yapılabilir.Web API, veri çekme işlemleri yapılır.

public async Task<string> KullaniciGetirAsync()

  {
    await Task.Delay(3000); 
    return "Kullanıcı bilgisi";  
  }
  
    *bekleme olurken programın diğer işleri devam eder.Kullanıcı deneyimi çok daha yüksektir.

**anahtar kavramlar**
  - Async: Bir metodun asenkron çalışacağını söylüyoruz. Yani işlemi başlatıyoruz ama beklemiyoruz.
  - Await: Asenkron işin sonucunu beklememizi sağlıyor. Yani "bu bitsin, sonra devam et" gibi düşünebilirsin.
  - Task: Asenkron işlemin temsilcisi gibi. Bir tür veri tipi yani.
  - ConfigureAwait: UI’ya ya da bulunduğun ortama bağlı olmadan çalışması için kullanılıyor. Özellikle mobil veya arka plan işleri için önemli oluyormuş.
  
 ## C# Arrow Function
  Bu ifade lambda fonksiyonu olarak geçer. Derste hocamız kodları kısaltmak daha hızlı kısa kod olarak açıklamıştı lambda fonksiyonu.
  
  List<int> sayilar = new List<int> { 1, 2, 3, 4, 5 };
  var çiftSayilar = sayilar.Where(sayi => sayi % 2 == 0).ToList();
  
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
  
[HttpGet]
public List<Ogrenci> TumOgrencileriGetir()
{
    return ogrenciServisi.HepsiniGetir();
}

  .Post:Yeni veri eklemek için.

  [HttpPost]
public IActionResult YeniOgrenciEkle([FromBody] Ogrenci yeniOgrenci)
{
    ogrenciServisi.Ekle(yeniOgrenci);
    return Ok();
}


  .Put:Var olan veriyi tamamen güncellemek için kullanılır.

[HttpPut("{id}")]
public IActionResult Guncelle(int id, [FromBody] Ogrenci guncelOgrenci)
{
    ogrenciServisi.Guncelle(id, guncelOgrenci);
    return Ok();
}


  .Delete:Veri silmek için kullanılır.
      
[HttpDelete("{id}")]
public IActionResult Sil(int id)
{
    ogrenciServisi.Sil(id);
    return Ok();
}

 

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

   {
  "email": "aylin@gmail.com",
  "sifre": "Aylin1234!"
}

 Sunucu json'u alır ve düşünür böyle bir kullanıcı var mı şifresi doğru mu diye.Eğer doğruysa şu şeklde bir JSON ile cevap gönderilir:

{
  "mesaj": "Giriş başarılı",
  "kullaniciAdi": "Aylin",
  "token": "ab123abc456xyz789",  
  "sonGiris": "2025-08-08"
}

  **Ayrıca sunucu giriş başarılı olduğunda kullanıcıya özel bir token verir.Dijital anahtar,id gibi düşünebiliriz aslında.Yani token saklanır ve tekrar giriş yapmana gerek kalmaz çünkü o id ile seni tanır.
  

# ASP.NET

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

   
## Dependency Injection(DI) nedir? neden önemlidir?
   Bir sınıfın ihtiyacı olan başka sınıfları kendi içinde oluşturmak yerine dışarıdan almasıdır.Diyelim ki bir kahve makinesine süt ve kahve gerekiyo makine kendi alıyosa sıkıntı ama biri gelip koyuyosa bu dependency ınjection oluyor.Çünkü makine sadece kahveyi yapar.
   
  **DI Örnek**:

- Burada sadece bir iş yapılıyor o da mesajı hazırlamak.
  
public class SelamServisi
{
    public string MesajHazirla()
    {
        return "Merhaba, iyi günler!";
    }
}

  -Selamci sınıfı mesajı hazırlamıyor sadece dışardan aldığı Selamservisi sınıfını kullanıyor.Yani selamci sadece mesajı nasıl göndericeğini biliyor mesajın içeriği hakkında bilgisi yok.Yani kendi işine odaklanıyor,bağımlı değil DI'da burda devreye giriyor.
  
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

-Burada ilk olarak bir SelamServisi nesnesi oluşturuyoruz.Sonra bunu Selamci sınıfına constructer ile veriyoruz(new metodu ile).En son SelamVer() metodunu çağırıp mesajı basmış oluyoruz.

class Program
{
    static void Main(string[] args)
    {
        SelamServisi servis = new SelamServisi(); 
        Selamci selamci = new Selamci(servis);   

        selamci.SelamVer(); 
    }
}

   
 
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

 
 # YAZILIM GELİŞTİRME PRENSİPLERİ

## SOLID Prensipleri

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

## Design Patterns(Tasarım Kalıpları)
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

## Clean Code(Temiz kod) Nedir?
 Kolay okunan, sade, anlaşılır ve bakımı kolay koddur. Anlamlı isimler, kısa fonksiyonlar, yorum gerektirmeyen kod = Temiz koddur.
  Kötü Kod:
   if (x == 1) { Birşeyolsun(); }
  Temiz Kod:
   if (Kullanıcıgirişyaptıysa) { ShowDashboard(); }

## Yazılım Mimari Desenleri

| Mimari                           | Kısaca Açıklama                             | Ne Zaman Kullanılır?                       |
| -------------------------------- | ------------------------------------------- | ------------------------------------------ |
| **Layered (Katmanlı)**           | UI, Business, Data katmanlarına ayrılır.    | Küçük/orta ölçekli uygulamalarda.          |
| **Clean Architecture**           | Katmanlar bağımsız, merkezde domain vardır. | Uzun ömürlü büyük projelerde.              |
| **Microservices**                | Her özellik ayrı bir servistir.             | Büyük ölçekli, dağıtık sistemlerde.        |
| **Event-Driven**                 | Bileşenler mesajlar/olaylar ile haberleşir. | Gerçek zamanlı, bağımsız sistemlerde.      |
| **Hexagonal (Ports & Adapters)** | İç mantık dış sistemlerden ayrıdır.         | Test edilebilirliği yüksek sistemler için. |

   

 
 



   
   
   
   
   
   
 


      


     

   





  
