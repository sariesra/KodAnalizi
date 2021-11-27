
# KOD ANALİZİ

## Dinamik Kod Analizi



Dinamik kod analizi, yazılımın çalıştırılarak (execute edilerek) method, kod satırı gibi seviyelerde kontrol edilmesi aktivitesidir. Dinamik analiz birincil olarak, özellikle run-time esnasında oluşabilecek hataların tespitini hedeflemektedir. Yazılım üzerinde, bulunduğu donanımın göstereceği performans veya belirli girdiler alması sonrasında oluşacak güvenlik açıkları bu konudaki iyi örneklerdendir.

Dinamik analiz aktiviteleri, kodun geliştirilmesinin hemen sonrasında statik analiz kontrollerinin yapılması ve derlenmesi ardından gerçekleştirilmelidir. Zira, statik analizler ile dinamik analizde tespit edilebilecek sorunların daha basit bir şekilde çözülmesi mümkün olabilir.



## **Statik kod analizi**

Statik kod analizi genelde test ile karıştırılır. Test’ler runtime’da bug’ları, hataları gözlemler, bu hatalara kod tarafında fix uygulanır. Statik kod analizi ise, kaynak kodu okur, pattern’lere göre üzerinde bulunan kuralları ihlal edip etmediğini ölçer.

> *Statik kod analizi, kodunuzun araçlar tarafından taranarak önceden belirlediğiniz kriterlere göre incelenmesidir. Kodunuzun belli bir kaliteyi tutturmasını sağlamak için yapılır. Eğer düzgün yapıyorsanız, üzerinde kaç kişilik takım çalışıyorsa çalışsın kodunuz tek bir elden çıkmış gibi gözükür.*

- Yapısal Kurallar: “girintileme” örneği bu başlık altına giriyor. Ama tabi ki de bu kadar değil. Exception handling, method ve sınıf isimleri, parametre ve property isimleri, method uzunlukları, sınıf uzunlukları, javadoc yazımı vs. gibi kodunuzun yapısıyla ilgili tüm kurallar bu başlığa giriyor.
- Çok bilinen, hatalı kalıplar: Bilinen, sık karşılaşılan ve genelde buglara yol açan tüm kod blokları bu başlık altına giriyor. Örnek vericek olursak, String sınıfını yanlış karşılaştırmak, karmaşıklığı yüksek kod blogları geliştirmek, bilinen güvenlik açığına yol acabilecek hatalar, vs.
- Test Kapsamınız: Unit testlerinizin kodunuzun ne kadarını kapsadığı ölçümü bu başlık altına giriyor.

### Sonarqube

- Sonarqube bir kod analiz aracı. Kodun geliştirilmesinden sonra devreye giriyor ve koddaki bugları, güvenlik açıklarını Clean Code gibi kabul görmüş kitaplardaki temiz kod kurallarına göre buluyor ve bildiriyor. Kurallar dillere göre ayrılmış durumda. 
- Server olarak kuruluyor, kurulduğunda belli başlı kuralla açık geliyor. Kuralların önem seviyesini isteğinize göre değiştirebiliyorsunuz.
- Kullanıcıları gruplandırabiliyorsunuz ve projelerin görünülürlüğünü bu grup/kullanıcılara göre değiştirebiliyorsunuz. Yani her kullanıcı her projeyi görmüyor.
- Gitlab ile entegrastonu var. Entegrasyon sağlandıktan sonra her gitlab commiti sonrası kod analiz edilebiliyor.
- Sonar anasayfasında master branchin durumu gösteriliyor. Proje içerisinde branchleri ayrı ayrı değerlendirebiliyorsunuz.
- Barındırdığı kuralların ne kadar sürede çözülebileceğini az çok biliyor. Buna göre bir “Technical Dept” çıkartıyor. 
- Diğer açık kaynaklı projelerle de entegrasyonu bulunuyor. 
- Sonarlint ile visual studio’ya entegre edilebiliyor. Commit attıktan sonra visual studio üzerinden projenizin sonar’daki durumuyla ilgili bildirim geliyor.
- En büyük eksiği build sonrasında çalışacak şekilde olması, sonar inceleyip hataları söylüyor ama buildi kırmadığı için açıp incelemek yazılımcının insiyatifine kalmış. 

### **Cucumber [ BDD ]**

#### Cucumber

- Cucumber’ı behaviour Driven Development(Davranış Güdümlü Geliştirme) ile ilişkilendirebiliriz.

- TDD’den farkı bir sistemin davranışlarını projenin tüm paydaşlarının anlayabileceği günlük konuşma dili şeklinde yazılmasıdır.

-  BDD için java tarafında Cucumber, .NET tarafında ise Specflow kütüphaneleri kullanılmaktadır.

  

*TDD : Kod öncesinde testin yazılması ve bu sadece testi geçmesi amaçlanarak bu amaç dışına çıkmadan kod yazılması yöntemine “TDD” ( test driven development)denir. Bu sayede kodun amaç dışına çıkılarak karmaşıklaşması önlenmektedir.*

1.  *Test yazılır, çalıştırılır ve hata verir.*
2. *Kod yazılır, test tekrar çalıştırılır ve test geçilir.*
3. *Yeni eklenecek kodlar ve geliştirme için test güncellenir ve döngü başa alınır.*

*BDD : Kullanıcı hikayelerinden çıkan Behavior’lar üzerinde Acceptance Test oluşturularak yazılım davranışı tasarlanmaya çalışılır. Test senaryosu proje içersindeki tüm paydaşların anlayacağı şekilde yazılır.*

#### Specflow

- Test atomasyonu için kullanılan bir tool.
- Test senaryosunun tüm proje paydaşları tarafından anlaşılabilir bir biçimde yazılmasını sağlıyor.
- Visual Studio eklentisi mevcut.
- Test senaryoları yazılırken “Gherkin” dili kullanılıyor.
- Specflow düz metin olarak yazılmış senaryolarımızı otomatize testlere dönüştüen bir test otomasyon aracıdır. 

#### *SPECFLOW ÖRNEĞİ*

- Visual Studio sürümünüze ait uzantıyı visual studio marketinden indirin.
- Test yazmak istediğiniz projeye yeni bir “Unit Test Project (.NET Framework)” ekleyin.
- Unit test projesine sağ tıklayarak  paketleri indirin ; SpecFlowSpecFlow.Tools.MsBuild.Generation, SpecRun.SpecFlow, SpecFlow
- Feature File : Belirli bir özelliği özetleyen ve bir test senaryosu içeren dosya. Pojenize sağ tık-> Yeni öğe->Specflow Feature File’I seçerek ekleyebilirsinz. Feature ve Scenario(Given,When,Then)’dan oluşur. 

![img](https://lh5.googleusercontent.com/N2c17U1I4tB1V4gbUQpVmmmB_L-De3QsWc_qx8n7r9YD2-L_O7oXdBHR7MvAz1UBTT30si888lO8sBfl4XAdRsU1FC6TtB7-AnZSnKk4Wq-y6Zgn3ZVrkDQnybyJ4w6H5AMCfEY4)

 																	*Şekil 0.1 Örnek Feature File*

- Senaryoyu test etmek için Feature dosyamızdaki senaryoya ait ifadelerin tanımlarını oluşturmamız gerekir. Specflow’u kullanarak daha sonra genişletebileceğimiz otomasyon kodumuz için iskelet oluşturabiliriz. Feature file’da koda sağ tıklayarak “Generate Step Definition” ı seçin ve Generate butonuna tıklayın.

 ![img](https://lh6.googleusercontent.com/dLiT9-xK8VRlxzV6IwacD-nKzKR2lKE0Rb8z8GyK3TOVP1Lkf1carBG3dW8lnaGE0SDAkD6HMK-HnNfepJYvjMjTgj0gk0y5r4mP6WKr1PP999Cp8M0eKYMtFkZQhM2WCDOPt1MZ)

*Şekil 0.2CalculatorSteps.cs dosyası iskeleti*

- Açılışta gelen hesap makinesi örneği üzerinden ileryecek olursak aşağıdaki kodu test edeceğimizi varsayabiliriz.

![img](https://lh4.googleusercontent.com/ChqrHD0y616YLc770IKdEHNHIxTPmQ7CoKv0S410NOmIVP6gjq76Wk9eQb3Iwy94SvuDoFD47HjyW_IJd4lTnomjPw8FbfxL4nilhbVV6LFXu1jXVNkcf0oTdNIwFDqrkYji9Vwp)

​																			*Şekil 0.3 Calculator.cs*

- Senaryo adımlarında kullandığımız girdiler o adıma ilişkin test metodunda parametre olarak kullanılmaktadır.(p0) Bu girdileri daha anlaşılır şekilde yeniden adlandırabiliriz. Ben birinci parametreye sayi1 ikincisine sayi2 diyeceğim.

- Kodun gerçekleştirmesi istenen girilen iki sayının toplanmasıdır. Bu sebeple toplanacak iki sayısı tutacak iki integer değişken ve bu iki sayının toplanması için bir metod tanımlanmıştır.

- Senaryonun oluşturulduğu Feature file ve test edilecek kodumuzun bulunduğu Calculator.cs dosyası tamamlanmıştır. Testin gerçekleştirilmesi için son adım iskeleti oluşturulan CalculatorSteps.cs dosyasının tamamlanmasıdır.

  1. ![img](https://lh3.googleusercontent.com/IXQb0JVDKwrdhZCd4rJSn5dztg8crQGftDo6EwyLpc7SzURpRcW0as5zZYAOvgx9E2LS7O9Ch_VZ3qXdTBOwIcqbNbPBn6J1vgpthIxwXkAX558mQ6dcXBlrr_LOKhLGaWCshyI_)

     ​											*Şekil 0.4. CalculatorSteps.cs Dosyasının son hali*

- Hesaplamalar için CalculatorSteps sınıfında Calculator tipinde bir değişken ve sonucu tutmak için integer tipinde bir değişken tanımlanmıştır.
- Kod iskeletindeki ScenarioContext.Current.Pending(); kısımları Şekil 0.3’de görüldüğü üzere değiştirilerek senaryo tamamlanır. Beklenen senaryoda girilen iki rakamın Calcualator sınıfındaki toplamının yine senaryoda girilen toplama eşit olmasıdır.
- Testi çalıştırmak için visual studio’da “Test Explorer penceresi” açılı ve “Run All” seçeneği tıklanır.
  1. ![img](https://lh6.googleusercontent.com/e7cDX-kcc2RAseTFcPeZUOHe44VcUZRbkiX7IBCCZimOwBA5JFfx0sZ_ZNhdLbu5nCIcEWWDj8-L5lbsno1avGM2l1OcR7er4MWXF8-1vVFoRg7gCEup6vm7lHGNt4pqLRNAj7jt)														*Şekil 0.5. Test Explorer*

- Testin tamamlanmasının ardından “Test Explorer” penceresinden çıktı incelenebilir. Teste sağ tıklayıp “Open Test” seçilerek teste ait feature file’a gidilebilir. Output’a tıklanarak test çıktısı açılabilir.
  - ![img](https://lh6.googleusercontent.com/9oeLS3ys6TwMC1XmESJo4I3j9XfhlfoK-Is2eXIRBC3uG7KNyXNfJGWxpit5eDHPGfcztxc04yyFtahYFhsoehaYSzXtvKqbH1BWDmukiK5qbeB-vFzoWJS-7MZmNeNXupl9Sx71)																			*Şekil 0.6. Test Çıktısı*
