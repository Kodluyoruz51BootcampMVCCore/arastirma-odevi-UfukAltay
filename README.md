# Araştırma Ödevi

1. Solid Prensiplerini Öğren.

S.O.L.I.D PRENSİPLERİ

SOLID yazılım prensipleri; geliştirilen yazılımın esnek, yeniden kullanılabilir, sürdürülebilir ve anlaşılır olmasını sağlayan, kod tekrarını önleyen ve Robert C. Martin tarafından Nesneye Yönelik Programlamanın (Object Oriented Programming) ilk 5 maddesi olarak öne sürülen prensipler bütünüdür. Kısaltması Michael Feathers tarafından tanımlanan bu prensiplerin amacı;
Geliştirdiğimiz yazılımın gelecekte gerek duyulacak gereksinimlere kolayca adapte olması, yeni bir özellik istendiğinde kodda bir değişikliğe gerek kalmadan kolayca ekleyebileceğimiz, projede minimum değişiklik yapılarak gerçekleştirilsin düşüncesidir ve kod üzerinde sürekli düzeltme, hatta yeniden yazma gibi sorunların yol açtığı zaman kaybını da minimuma indirerek geliştirilmesidir.

S — Single-Responsibility Principle(Tek Sorumluluk Prensibi)
O — Open-Closed Principle(Açık Kapalı Prensibi)
L — Liskov Substitution Principle ( Liskov’un Yerine geçme Prensibi)
I — Interface Segregation Principle ( Arayüz Ayrımı Prensibi)
D — Dependency Inversion Principle ( Bağımlılıkların Terslenmesi Prensibi)

S — Single-Responsibility Principle (Tek Sorumluluk Prensibi)
“Yapabildiğin yapman gerektiği anlamına gelmiyor.”
Single Responsibility; Tek işi, tek sorumlulukta yapma sanatı olarak özetlenebilir. Bir sınıfın (class), fonksiyonun ya da metodun tek bir görevi, sorumluluğu olmalıdır. Başka sınıfların görevlerini gerçekleştirmemelidir.
Örneğin: Aşçı sınıfında YemekYap metodu olur ama malzemeAl metodu olmaz. Ancak Aşçı isterse gidip malzemeyi alabilir. Lakin bu aşçının ana görevi değildir dolayısıyla gerek yoktur.

public class User {
private Long id;
private String name;
private String street;
private String city;
private String username;

//Getters, setters

public void changeAddress(String street,String city) {
//logic
}

public void login(String username) {
//logic
}

public void logout(String username) {
//logic
}
}
Buradaki kötü örnekte Adres ile ilgili street ve city gibi veriler direkt olarak User sınıfı içerisinde bulunmamalıdır. Herhangi bir ek adres bilgisi istendiğinde(country yada zipCode gibi) burada tamamen User sınıfını etkileyecektir. User sınıfı direkt olarak sorumlu olmadığı bir işlemden etkilenmiş olacak. “street”, “city” gibi veriler sadece adres için gereklidir, bu durumda Address adında yeni bir class oluşturmak daha mantıklı olur.

O — Open-Closed Principle(Açık Kapalı Prensibi)
“Ceket giyerken göğüs operasyonuna gerek yoktur.”
Open-Closed prensibi kısacası bir programın, application ın veya objelerin ya da entitylerin geliştirilmeye açık ancak değiştirmeye kapalı olduğunu belirtir. İnterface ve abstract sınıflar kullanılarak istenen eklemeler yapılabilir. Sınıflarımız / fonksiyonlarımız değişikliğe kapalı ancak yeni davranışların eklenmesine açık olmalıdır. Bu prensip; sürdürülebilir ve tekrar kullanılabilir yapıda kod yazmanın temelini oluşturur.
Open Sınıf için yeni davranışlar eklenebilmesini sağlar. Gereksinimler değiştiğinde, yeni gereksinimlerin karşılanabilmesi için bir sınıfa yeni veya farklı davranışlar eklenebilir olmasıdır.
Closed Bir sınıf temel özelliklerinin değişimi ise mümkün olmamalıdır.
Örnek : Bir şirkette çalışanların emeklilik günleri hesaplanacak. Her sınıf ayrı ayrı tanımlı işçi, memur vs. ve her birinin bilgileri, işe giriş tarihleri sınıflarında tanımlı. Ne zaman emekli olduklarını hesaplamak için sgkHesap isimli sınıfımızda hesap metodu var. Patronumuz dedi ki buraya yöneticileri de ekle ve yöneticilerin de emeklilik günleri hesaplansın. Bunun için sadece sgkHesap kısmına if-else koşullarıyla kontrol edilip hesaplatılmak istenen gün sayısının sahibi olan kişinin ne olduğu tespit edilerek yaptırılabilir. Hesap aynı hesap, değişen şey sadece obje.

L — Liskov Substitution Principle ( Liskov’un Yerine geçme Prensibi)
“Eğer bir ördek, ördek gibi quacklerse (ördek gibi ses çıkartırsa) ama bataryaya ihtiyaç duyuyorsa muhtemelen yanlış abstract edilmiştir.”
Bir ana sınıftan ya da sınıflardan türetilen sınıfların bir üst hiyerarşideki sınıfların yerine geçmesini esas alan bir prensiptir. Türeyen sınıf yani alt sınıflar ana(üst) sınıfın tüm özelliklerini ve metotlarını aynı işlevi gösterecek şekilde kullanabilmeli ve kendine ait yeni özellikler barındırabilmelidir. Alt seviye sınıflardan oluşan nesnelerin/sınıfların, ana(üst) sınıfın nesneleri ile yer değiştirdikleri zaman, aynı davranışı sergilemesi gerekmektedir. Türetilen sınıflar, türeyen sınıfların tüm özelliklerini kullanabilmelidir.
Başka bir örnek: Dörtgenler Üst sınıf ve kare alt sınıf olsun. Dörtgen sınıfında tanımlı boyut değiştir metodu uzun kenarı 300 ve kısa kenarı 100 yapsın. Kare sınıfını bunun yerine geçirdiğiniz zaman (Kare de bir dörtgendir) karenin tüm kenarları eşit olduğu için bu metodu karşılayamaz ve bu yüzünden LSP’ ye uymaz.

public class Square extends Rectangle { @override
public void setWidth(int width) {
super.setWidth(width);
super.setHeight(width);
} @override
public void setHeight(int height) {
super.setHeight(height);
super.setWidth(height);
}
}
Matematiksel olarak bir kareyi de bir dikdörtgen olarak kabul edebiliriz. Ama yazılım dünyasında da böyle kabul etmeli miydik?

@test
public void testRectangleArea() throws Exception {
Rectangle rectangle = new Square();
rectangle.setWidth(20);
rectangle.setHeight(4);
assertEquals(80, rectangle.area());
}
Kareyi de beklendiği yerde dikdörtgen olarak kullanılabilir hale getirmiş olduk. Ancak böyle yaparak dikdörtgen davranışındaki beklentiyi bozuyoruz. Çünkü karenin sadece tek bir kenar bilgisi yeterlidir yada uzunluk ve en bilgisi aynı olmak durumundadır.
Matematiksel olarak karenin dikdörtgenden türediğini varsayabiliriz. Ama davranışsal olarak Kare Dikdörtgenin yerine geçmez, bu hiyerarşi Liskov prensibini (LSP) ihlal eder.
I — Interface Segregation Principle ( Arayüz Ayrımı Prensibi)
“Benden bunu bir yere takmamı istiyorsun, Nereye?”
Bir arayüze gerekli olmayan eklentilerin eklenmemesini belirten bir prensiptir. Arayüzde o an sadece kullanılacak olan eklentilerin ekli olması gerektiğini savunur. Bir müşteri asla kullanmadığı bir arabirimi uygulamaya zorlanmamalı veya istemciler kullanmadıkları yöntemlere bağlı olmaya zorlanmamalıdır. Tek bir interface yerine kullanımlarına göre parçalanmış birden fazla interface ile işlemleri yürütmeliyiz. Yani her farklı sorumluluğun kendine özgü bir arayüzü olması gerekmektedir. Böylece interface’i kullanan kişide sadece ihtiyacı olanlarla ilgilenmiş olur. Birden fazla amaç için yalnızca bir arayüzümüz var ise buna gerektiğinden fazla method ya da özellik ekliyoruz demektir, bu da IS prensibine aykırı davrandığınız anlamına gelir. Görüldüğü gibi single responsibility ve interface segregation prensipleri birbirine oldukça yakın ve aynı amaca hizmet eden prensiplerdir. Tek fark ise Interface segregation arayüz(interface)ler ile ilgilenirken, Single responsibility sınıflarla ilgilenmektedir.
Örnek: İki boyutlu şekiller sınıfında hacim isimli bir metot tanımlamak. İki boyutlu şekillerin hacmi olmadığı için bu metot gereksizdir.

namespace InterfacesDemo // Bu örnekte interfacelerin doğru planlanmasını yaptık. SOLID prensibinin I (Interface Segregation) prensibini yaptık.
{
class Program
{
static void Main(string[] args)
{
IWorker[] workers = new IWorker[3]
{
new Manager(),
new Worker(),
new Robot()
};

        foreach (var worker in workers)
        {
            worker.Work();
        }

        IEat[] eats = new IEat[2]
        {
            new Manager(), 
            new Worker()
        };

        foreach (var eat in eats)
        {
            eat.Eat();
        }

        Console.ReadLine();
    }
}

interface IWorker
{
    void Work();
}

interface IEat
{
    void Eat();
}

interface ISalary
{
    void GetSalary();
}

class Manager : IWorker, IEat, ISalary
{
    public void Work()
    {
        Console.WriteLine("Yönetici Çalıştı");
    }

    public void Eat()
    {
        Console.WriteLine("Yönetici Yemek Yedi");
    }

    public void GetSalary()
    {
        Console.WriteLine("Yönetici Maaş Aldı");
    }
}

class Worker : IWorker, IEat, ISalary
{
    public void Work()
    {
        Console.WriteLine("İşçi Çalıştı");
    }

    public void Eat()
    {
        Console.WriteLine("İşçi Yemek Yedi");
    }

    public void GetSalary()
    {
        Console.WriteLine("İşçi Maaş Aldı");
    }
}

class Robot : IWorker
{
    public void Work()
    {
        Console.WriteLine("Robot Çalıştı");
    }
}
}

D — Dependency Inversion Principle ( Bağımlılıkların Terslenmesi Prensibi)
“ Bir lambayı doğrudan duvardaki elektrik kablolarına lehimleyebilir misiniz? ”
Sınıflar arası bağımlılıklar olabildiğince az olmalıdır özellikle üst seviye sınıflar alt seviye sınıflara bağımlı olmamalıdır.
Bir sınıfın, metodun ya da özelliğin, onu kullanan diğer sınıflara karşı olan bağımlılığı en aza indirgenmelidir. Bir alt sınıfta yapılan değişiklikler üst sınıfları etkilememelidir. Yüksek seviye sınıflarda bir davranış değiştiğinde, alt seviye davranışların bu değişime uyum sağlaması gerekir. Ancak, düşük seviye sınıflarda bir davranış değiştiğinde, üst seviye sınıfların davranışında bir bozulma meydana gelmemelidir. Peki, bütün bu sorunlardan kurtulmanın yolu nedir ?
Cevap: Dependency Inversion, yani üst sınıflar, alt seviyeli sınıflara bağlı olmamalı, çözüm ise her ikisi de soyut kavramlar üzerinden yönetilebilmelidir. Yüksek seviye ve düşük seviye sınıflar arasında bir soyutlama katmanı oluşturabiliriz.
Üst Seviye Sınıflar -> Soyutlama Katmanı -> Düşük Seviye Sınıfları
Örnek: Yönetici ve işçi diye bir sınıfımız olsun. Yönetici sınıfımızın yeterince karmaşık olduğunu ve hem yöneticiye ait bilgilerin hem de işçiler üzerinde etki edebilecek metotları olduğunu düşünelim. Süper işçi diye yeni bir sınıf tanımladık. Ancak şu an yönetici sınıfındaki metotlar sadece işçilere hizmet veriyor ve bu durumda yönetici sınıfında çok büyük değişikliğe gitmemiz gerekecek çünkü oradaki metotların hepsi sadece işçiler için tasarlandı. Eğer dependency inversion prensibine uyulsaydı karmaşıklık minimum düzeye indirilebilirdi ve üst sınıf (yönetici) alt sınıf olan süper işçilere bağlı olmazdı.

2. Microsoft Build 'den 2 etkinlik araştır.

1- Ask the Team: Visual Studio Code - https://mybuild.microsoft.com/sessions/be31cf74-1b32-4ac5-9673-333bc6018b18?source=sessions
2- The Journey to One .NET - https://mybuild.microsoft.com/sessions/b7e27509-c56c-42ad-9ce2-34270ecb0a38?source=sessions

3. Microsoft Build 2020 yeniliklerini Araştır.

Microsoft’un her sene düzenlediği en büyük etkinliklerden biri olan Microsoft Build, 2020 ayağı için geri döndü. COVID-19 pandemisinin dünyada yarattığı değişikliklere ayak uyduran etkinlik, bu sene ücretsiz katılım hakkıyla tamamiyle dijital gerçekleşecek.

Her sektörden geliştiricilere odaklanan Build, geçtiğimiz senelerde 2395 dolar katılım ücreti gerektiriyordu. Diğer tüm konferans ve etkinliklerin aksine iptal edilmek yerine tamamiyle dijitale taşınan Microsoft Build, içerik anlamında da değişikliklere gidecek.

Microsoft’a ek olarak bu sene farklı şirketlerin de programa dahil edileceğini duyuran Microsoft CEO’su Satya Nadella, açılış konuşmasını da üstleneceğini belirtti. Pandemi sırasında şirketlerin izlemesi gereken yol haritalarının da inceleneceği etkinlik, aynı zamanda Twitch üzerinde 48 saatlik bir workshop’a sahip olacak.

Microsoft Build, Nadella’ya ek olarak Julia White, Scott Guthrie, Panos Panay, Kevin Scott, Rajesh Jha, Mark Russinovich ve daha birçok geliştiriciye söz hakkı tanıyacak. Pasifik zaman dilimi dahilinde 19 Mayıs sabah 8’te başlayacak olan etkinlik, kesintisiz olarak 48 saat dijital yayın gerçekleştirecek. Zaman dilimi dolayısıyla yaşanacak olan farklılıkları ortadan kaldırmak istediğini belirten Microsoft, farklı zamanlarda farklı bölgelere özel söyleşilerin gerçekleşeceğini açıkladı.

Etkinlik düzeni ve içeriğiyle ilgili yorumda bulunan Microsoft Program Müdürü Scott Hanselman, Build’ı beklemekte sabırsızlandığının altını çizdi.

“Herkesin beklediği Build’dan farklı ancak özel bir etkinlik gerçekleştireceğiz. Topluluğumuz içinde bulunan yazılımcıları ve geliştiricileri bir araya getirmek için sabırsızlanıyoruz. Geliştiricilerimizi özellikle böyle zor zamanlarda insan hayatını kolaylaştıran bütçe dostu, inovatif ve geleceğe dönük projelerle desteklemeye tamamiyle bağlıyız.”

Asp.Net Blazor WebAssembly’nin resmi olarak yayınlanması

2021 yılında Xamarin’İn evrim geçirecek hali olan .Net MAUI(Multi-platform App UI) preview olarak kullanılabiliyor.

Entity Framework Core 5 ve .Net 5 preview olarak yayınlandı. C# 9.0’ın gelişi duyuruldu. Kubernetes temelli microservisleri hedefleyen deneysel bir araç olan Project Type duyuruldu.

Azure tarafındaki gelişmeler: Özellikle makine öğrenmesi ve yapay zekaya yönelik gelişmeler, Azure Quantum ile kuantum işlem gelişmeleri, Azure Static Web Apps ile Github repositoryleri üzerinden Azure’da yayına alınabilecek full-stack web uygulamalarının mümkün olması

4. Takip Ettiğin 2 yazılımcıyı araştır.

1-Engin POLAT - https://enginpolat.com/
2-Engin DEMİROĞ - https://www.linkedin.com/in/engindemirog/
5. Devler Azure'da araştır [Eğitim-Workshop]

    Kuburnetes Atolyeleri
    DevOps Atolyeleri
    Topluluk Liderleri ile Atolyeler
6. Yazılım ile ilgili Yarışmaları araştır (Örneğin: GGJ)

Travel Hackathon - https://www.teknofest.org/yarisma-detaylar-27.html
