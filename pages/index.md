# 1. Girizgah: Kabuğu Tanımak

Bash kabuğunun detaylarına değinmeden evvel, sağlam bir temel için önemli olan birkaç kavramı netleştirmemiz gerekiyor. Tüm detayları ile olmasa da kullanacağımız sistemin arkaplanda nasıl çalıştığı ve nasıl bir yapıya sahip olduğu konusunda fikir sahibi olmamız, ileride yapacağımız tüm işlemleri çok daha bilinçli şekilde gerçekleştirebilmemizi sağlar.

# 1.1 İşleyişe Genel Bakış

Bash kabuk programlamayı öğrenmek istediğinize göre Linux'un aslında çekirdek olduğunu GNU oluşumunun ise çeşitli araçlar sağladığını, neticede işletim sistemi(GNU/Linux) bütününün ortaya çıktığını biliyorsunuzdur. Hatta çekirdeğin ne işe yaradığını da mutlaka duymuşsunuzdur. Şimdi kısa bir hatırlatma olması açısından bu işleyişe biraz daha yakından bakarak olup bitenleri anlamlandırmaya çalışalım.

Bilgisayarımızı(donanım) ve içerisinde çalıştırılan işletim sistemini(yazılım) en basit haliyle aşağıdaki şekilde soyutlayabiliriz.

![1%20Girizgah%20Kabug%CC%86u%20Tan%C4%B1mak%2095ae70e200524ff59ec5719dd99f9182/OS.svg](1%20Girizgah%20Kabug%CC%86u%20Tan%C4%B1mak%2095ae70e200524ff59ec5719dd99f9182/OS.svg)

Hangi donanımın hangi işlevde olduğunu henüz ele almayacağımız için biz doğrudan "işletim sistemi" bölümüne daha yakından bakmaya başlayalım.

# 1.1.1 İşletim Sistemi

İşletim sistemi, bilgisayarımızda bulunan donanım(disk, ram, cpu, monitör, ağ kartları, vb..) ile iletişim kurabilmemize olanak sağlayan aracı bir soyutlama katmanı yani yazılımsal bir arayüzdür. İşletim sistemleri sayesinde her bir donanım ile ayrı ayrı nasıl iletişim kuracağımızı düşünmeden, mevcut donanımlara kolayca iş yaptırabiliyoruz. Eğer böyle olmasaydı binlerce çeşit marka ve model donanımı nasıl bir arada idame edebilirdik ki ? 

İşletim sisteminin bizi donanımlarla uğraşma külfetinden kurtardığını söyledik. Peki ama bunu tam olarak nasıl yapıyor ? 

İşletim sistemi temel olarak iki bölümden oluşur. Bu bölümler "kullanıcı alanı(user space)" ve "çekirdek alanı(kernel space)" olarak isimlendirilir. Bizler sistemi yöneten kullanıcılar olarak kullanıcı alanındaki araçları kullanırız. Bu araçlar da çekirdek ile iletişime geçer. Çekirdek ise kullanıcı alanından gelen emirleri donanıma ileterek ilgili işin yaptırılmasını sağlar. 

Not: Aşağıdaki diyagram kullanıcı alanındaki temsili araçları içermektedir yani tüm sistem araçları bunlardan ibaret değil elbette. 

![1%20Girizgah%20Kabug%CC%86u%20Tan%C4%B1mak%2095ae70e200524ff59ec5719dd99f9182/OS_detailed.svg](1%20Girizgah%20Kabug%CC%86u%20Tan%C4%B1mak%2095ae70e200524ff59ec5719dd99f9182/OS_detailed.svg)

## 1.1.1.1 Kullanıcı Alanı(User Space)

Standart bir kullanıcı olarak sistem üzerinde herhangi bir işi yaparken çok az şeyle ilgilenmek isteriz. Örneğin bir metin belgesine yazı yazıyorken donanıma nasıl iş yaptıracağımı falan düşünmem gerekmez, gerekmemelidir zaten. Ben sadece klavyemi kullanır yazımı yazar gerisini işletim sistemine bırakırım. İşletim sistemi bir önceki başlık altında açıkladığımız şekilde tüm gerekli işlemleri katmanlı yapısı sayesinde organize eder. 

Tüm yapı içinde bizler kullanıcı olduğumuz için "kullanıcı alanı", sistemi isteklerimiz doğrultusunda **kolayca yönetebileceğimiz** şekilde tasarlanmıştır. Yani kullanıcı alanına komuta kontrol alanı da diyebiliriz. Üstelik kullanıcı alanı, sistem yönetimi için bizlere iki alternatif ortam sunar. Bunlar "grafiksel kullanıcı arayüzü(GUI)" ve "komutu satırı arayüzü(CLI)" ortamlarıdır. 

### 1.1.1.1.1 Grafiksel Kullanıcı Arayüzü

Grafiksel arayüzden kastımız genellikle fare kullanarak, bir takım tıklama ve sürükle bırak işlemleri ile sistemi yönetebildiğimiz görselliğin ön planda olduğu çalışma ortamıdır. Bu ortamda pencereler, butonlar vardır, sürükle bırak yapılabilir, bilirsiniz işte her zaman karşımıza çıkan grafiksel kullanıcı arayüzünden bahsediyorum. Söz konusu grafiksel arayüz ortamı olduğunda, görüntü sunucumuz, masaüstü ortamımız ve pencere yöneticimiz grafiksel arayüzü kullanabilmemizi kolaylaştıran araç setleridir. Sistemimizde yüklü bulunan grafiksel arayüze sahip araçları yalnızca grafiksel arayüz ortamı üzerinde kullanabiliriz. Grafiksel arayüzlü araçlara ofis yazılımlarını örnek verebiliriz.

### 1.1.1.1.2 Komut Satırı Arayüzü

Komut satırı arayüzü ise grafiksel arayüze sahip olmayan araçların çalıştırıldığı ortamdır. Bu ortamda grafiksel arayüzle çalışan araçları kullanamazsınız çünkü bu ortam grafiksel arayüzü sunabilecek yapıda tasarlanmamıştır. Komut satırı arayüzünde çalışan araçlar, grafiksel bir etkileşime ihtiyaç duymadan klavye üzerinden yönetilebilen araçlardır. Herhangi bir grafiksel etkileşim olmadığı için araçların bulunup çalıştırılması, araçlar arasında geçiş veya ortak kullanım gibi işler için kabuk bize yardımcı olur. Nasıl ki grafiksel arayüze sahip uygulamalar masaüstü ortamı gibi çevre birimleri sayesinde kolay yönetilebilir oluyorsa, kabukta komut satırı üzerinden çalıştırılan araçları organize şekilde yönetebilmemiz için bize gereken ortamı sağlar. Yani kısacası "kabuk" dediğimiz yapı bizim komut satırı üzerindeki yaverimizdir.

Grafiksel arayüzde uygulama simgesine tıklarız, komut satırı arayüzünde kabuğa ilgili aracın ismini yazarız. Her iki ortam da bize sistem üzerindeki araçları; bulma, çalıştırma, takip etme ve gerektiğinde sonlandırma gibi konularda yani kısacası "yönetimi" konusunda yardımcı olurlar.

Şimdi çok basit bir örnek üzerinden sistem yönetiminin genel işleyişe bakalım. Örneğin ben yeni bir klasör oluşturmak istersem önümde iki temel seçenek bulunuyor. Bunlardan ilki grafiksel arayüze sahip olan dosya yöneticisini kullanmak, diğeri ise "kabuk" olarak ifade edilen sistem yönetim aracına komut vererek klasörün oluşturulmasını sağlamaktır. 

Grafiksel arayüzde sağ tıklayıp "yeni klasör oluştur" dememiz yeterli. Biz grafiksel arayüze sahip olan dosya yöneticisi aracını kullandığımızda, bu araç çekirdek ile iletişime geçip bizim gerçekleştirmek istediğimiz işlemi çekirdeğe ifade ediyor. Çekirdek, bu işlem için gereken tüm şartlar müsaitse sisteme bağlı bulunan donanıma bu işin nasıl yapılacağını izah ediyor. Ve en nihayetinde gerekli donanımlar çalıştırılarak bizim klasörümüz oluşturulmuş oluyor. Aşağıdaki diyagramda bu işlem akışının basit soyutlamasını görebilirsiniz. 

![1%20Girizgah%20Kabug%CC%86u%20Tan%C4%B1mak%2095ae70e200524ff59ec5719dd99f9182/only_gui.svg](1%20Girizgah%20Kabug%CC%86u%20Tan%C4%B1mak%2095ae70e200524ff59ec5719dd99f9182/only_gui.svg)

Grafiksel arayüze sahip olmayan komut satırı arayüzlü araçlar da aslında tamamen benzer işleyişe sahiptir. Bu durumu teyit etmek üzere komut satırı arayüzü ile dosya oluşturulma akışına göz atalım. Sisteme yapılacak işlemi emredebilmek için terminal aracımı açıp gerekli ifadeyi komut satırına giriyorum.

![1%20Girizgah%20Kabug%CC%86u%20Tan%C4%B1mak%2095ae70e200524ff59ec5719dd99f9182/only_cli.svg](1%20Girizgah%20Kabug%CC%86u%20Tan%C4%B1mak%2095ae70e200524ff59ec5719dd99f9182/only_cli.svg)

Burada grafiksel arayüze gerek kalmadan klasör oluşturmamızı sağlayan araç "mkdir" aracıdır. Bu aracı kullanmak istediğimizi sisteme belirtmek için klavyemizdeki girdileri okuyan "konsol" ya da "terminal" olarak geçen aracı kullanıyoruz. Buradaki konsol aracının tek görevi, klavyemizdeki girdileri alıp "kabuk" olarak geçen yapıya aktarmaktır. Kabuk denilen yapı bizim yazılı şekilde ifade ettiğimiz komutu anlamlandırıp, "mkdir" aracını bulup "klasor" argümanı ile çalıştırılmasını sağlıyor. Bu sayede çalıştırılan "mkdir" aracı, "klasor" isimli klasör oluşturmak istediğini çekirdeğe izah edebiliyor. Çekirdek de donanıma gereken işi yaptırabiliyor. Neticede yalnızca yazılı emirler ile istediğimiz işlemin gerçekleştirilmesini kolaylıkla sağlamış oluyoruz.

Sistemin en genel çalışma yapısı ele aldığımız şekildedir. Son olarak birkaç detaydan daha bahsedip kabuğa odaklanabiliriz. 

Devam etmeden önce "kabuk" ile çok karıştırılan, "konsol" ya da "terminal" olarak bilinen "komut satırı" araçlarından bahsederek tüm kavramları netleştirmiş olalım.

## 1.1.1.1.3 Terminal | Konsol | Komut Satırı

Kabuğun, grafiksel arayüze gerek kalmadan sistemi yönetebilmemizi sağladığından bahsettik. Kabuğun grafiksel bir arayüzü olmadığı için kabuk ile iletişim kurarken emirlerimizi "terminal" ya da "konsol" olarak ifade edilen komut satırı araçları üzerinden ulaştırmamız gerekiyor. Yani adı üstünde komut satırı araçları yalnızca bizim klavyemizdeki girdileri satır satır alarak kabuğa iletmekle ve kabuğun döndürdüğü sonuçları göstermekle mükelleftir. Verilen emirleri komut satırı araçları yorumlamaz, yorumlayan kabuktur.

Biraz daha ayrıntılı bahsetmek gerekirse sistem üzerinde TTY olarak isimlendirilen sanal konsollar vardır. Bu konsollar arasında geçiş yapmak için `Ctrl + Alt + F1` `Ctrl + Alt + F2` veya duruma göre diğer `Ctrl + Alt + F2, F3, F4, F5, F6, F7` tuşlamaları kullanılabilir. 

Eğer mevcut sistemde grafiksel arayüz ortamı kuruluysa, TTY konsollarından en az birisi bu grafiksel arayüz ortamı için ayrılmıştır. Kullanılan dağıtıma göre farklılık gösteriyor olsa da genellikle 1. ya da 7. TTY konsolu, grafiksel arayüz ortamını çalıştırmak için ayrılmıştır. Grafiksel arayüz ortamında var olan herhangi bir terminal aracını açtığınızda bu terminal aracı aslında "sözde TTY(pseudo-terminal(PTY olarak bilinir))" olarak ifade edilen, grafiksel arayüz üzerinden dahi kabuğa emirler verebilmemizi sağlayan komut satırı sunar. Tüm bu yapı sayesinde biz ister grafiksel arayüz ortamında olalım istersek de yalnızca komut satırı arayüzünde çalışalım, neticede konsol araçları sayesinde kabuk ile iletişim kurabiliriz.

Zaten klasör oluşturma örneğimizi verirken grafiksel arayüzü üzerindeki terminal aracını yani "sözde TTY(pseudo-terminal(PTY))" kullanarak kabuk ile iletişim kurmuştuk. Dilersek aynı örneği komut satırı arayüzüne geçiş yaparak da sorunsuzca tekrar edebiliriz.

Tüm bu açıkladıklarımız ışığında "konsol" aracının hangisi olduğunun bir önemi olmadığını ve bizim halimizden anlayacak esas şeyin kabuk olduğunu bizzat teyit etmiş olduk.

Kabuk dediğimiz yapı da en nihayetinde bir yazılımdır. Dolayısıyla her yazılımda olduğu gibi kabuğun da pek çok alternatifi vardır. Biz bu eğitimde dünya çağında en yaygın kullanıma sahip olan "Bash" kabuğuna odaklanıyor olacağız. 

# 1.2 Neden Bash ?

Bash kabuk dili, **Stephen Bourne**'nin UNIX için geliştirmiş olduğu "**sh"** kabuk dilini temel alarak geliştirildiği için; **B**ourne-**A**gain **SH**ell kelimelerinin kısaltması olan "**BASH"** şeklinde adlandırılmıştır. Günümüzde pek çok GNU/Linux dağıtımının varsayılan kabuğudur.

![https://raw.githubusercontent.com/taylanbildik/bash_script_dersleri/master/img/Readme/bash_shell.png](https://raw.githubusercontent.com/taylanbildik/bash_script_dersleri/master/img/Readme/bash_shell.png)

Bash kabuk dilinin yaygın şekilde kullanılma sebebi; **sh** dili haricinde **ksh**(korn shell) ve **csh**(C shell) gibi çeşitli kabuk dillerinin yararlı özelliklerini içerisinde barındırarak, hem kullanıcı etkileşimi hem de programlanabilirlik için işlevselliği arttıran geliştirmeler içermesidir. Üstelik tüm bu avantajları, çıktığı dönemde GPL lisansı altında herkese özgürce sunmuştur. Dolayısıyla sahip olduğu özellikler çok hızlı şekilde, dağıtımlar üzerinde varsayılan kabuk olarak yaygınlaşmasını sağlamıştır. Genellikle kullanıcılar geçmişten beri var olan tüm konfigürasyonlarını bash üzerinde kurguladığı için de elbette yeni bir kabuğa geçmeye pek istekli değillerdir. Bu sebeple GNU/Linux sistemlerinde **BASH** dışında çeşitli kabuk dilleri barındırılmasına rağmen, genellikle sistemin varsayılan kabuk yorumlayıcısı **BASH**'dir. İstisnalar hariç, varsayılan kabuk bash değilse bile sistemde yüklü olacağı için kolayca ulaşabilirsiniz. Hatta tüm bunlar dışında "sh" kabuğu ile yakın ilişkisi sebebiyle "bash" bilen kişiler, bash kabuğunun bulunmadığı durumlarda sh kabuğunu da rahatlıkla kullanabilirler. Bizler de kullanılabilirlik açısında sahip olduğu yaygınlığı dolayısıyla "BASH" kabuğunu öğrenme gayretindeyiz. 

## 1.2.1 Alternatif Kabuklar Hakkında

Bir dönem Bash'in yaygınlaşmasını sağlayan GPL lisansı, yeni sürümü ile MacOS gibi ticari sistemlerde yol ayrımına neden olmuştur. Nitekim GPLv3 lisanslı ile birlikte uzun süredir yeni bash sürümlerini kullanamayan MacOS, varsayılan kabuğunu "zsh" olarak değiştirmiştir. Her ne kadar bash kabuğu hala MacOS üzerinde kullanılabilir olsa da zsh kabuğuna yaşanmış olan geçiş, zsh kabuğunun bash karşısında popülarite kazanmasının önüne açabilir. Hatta interaktif yani etkileşimli kullanımda zsh kabuğu daha işlevsel bulunduğu için Kali Linux gibi bazı dağıtımlar da varsayılan olarak zsh kabuğunu kullanmaya başlandı. Yine de tüm bunların yanında, bash kabuğu üzerine kurgulanmış olan ve çok uzun süredir kararlı şekilde çalışan sistemleri ele aldığımızda bash uzunca bir süre yaygınlığını koruyacak gibi görünüyor. Kabuk dilleri bağlamında, Bash dilini öğrenmenin İngilizce öğrenmeye benzetilmesi mümkündür. İngilizce haricinde pek çok yaygın kullanımda olan dil olsa da İngilizce evrenseldir. Dünyanın neresine giderseniz gidin bu dili kullanabilirsiniz. Bu durum da ilgili dili öğrenmenin en büyük motivasyonudur zaten.

Eğer söz konusu olan "etkileşimli kullanımda kolaylık" ise, zsh yerine fish(friendly interactive shell) kabuğu da tercih konusu olabilir. Ama bizim odaklandığımız şey etkileşimli kullanım değil, evrensel olan bash kabuğunu programlayabilmektir. Özetle yaygınlığı, kararlı ve kolay programlanabilir yapısı dolayısı ile kabuk dilleri içinde "Bash" bizim "İngilizce" dilimizdir.

Biraz önce bahsettiğimiz "**etkileşimli**" ve "**programlanabilir**" ifadelerini kısaca açıklayacak olursak;

**Kabuğun etkileşimli olması demek**, anlık olarak kullanıcıdan gelen emirleri yorumlayıp yine kullanıcıya emirin sonucu sunmasıdır. Etkileşimli kabuklar sürekli kullanıcıdan emirler bekler yani kullanıcı ile sürekli etkileşim halindedirler. Daha önce de bahsettiğimiz şekilde farklı kabuk türlerinde bu etkileşim deneyimi de farklıdır. Kabuklar, renklendirme ve otomatik öneri ya da otomatik tamamlama gibi kullanımı kolaylaştırıcı çeşitli özelliklere sahiptir. Kimi kabukta etkileşim için sunulan özellikler fazlayken kimisinde bu gibi özellikler azdır veya hiç yoktur. Bu da kabuklar arasındaki "etkileşimde kolaylık" farklılığını oluşturan unsudur.

Örneğin ben sırasıyla konsola `pwd` ve `whoami` komutlarını girdiğimde ve çıktı olarak bulunduğum dizin ve oturum açtığım kullanıcı hesabını aldığımda kabuk ile etkileşime geçmiş oluyorum. Çünkü kabuk benden komut bekleyip benden aldığı komutları yorumlayıp sonuçlarını tekrar bana iletmiş oldu.

**Programlanabilir olması ise**, kabuğa verilebilecek olan emirlerin bir dosya içerisinde uygun şekilde toparlanması ve bu dosyanın çalıştırılması ile emirlerin yerine getirildiği kullanımdır. Bu kullanımda aktif kullanıcı etkileşimi şart değildir çünkü emirler önceden programlandığı şekilde otomatik olarak yerine getirilir.

Daha önce verdiğimiz örnekteki `pwd` ve `whoami` komutlarını bir dosyaya kaydedip dosyayı çalıştırdığımda ise, tek seferde iki komutta çalıştırılmış oluyor. Yani kabuk dosyayı okuyup çalıştırırken benden bir etkileşim beklemeden doğrudan işini yapıyor. İşte çok daha düzenli yapılar ile komutları bir dosyaya kaydedip tek sefer çalıştığımızda kabuğu programlamış oluyoruz. Hatta benim burada dosyayı elle çalıştırmama takılmış dahi olabilirsiniz. Dosyayı elle çalıştırmamıza da gerek yok, zamanlanmış görevler gibi yapılar sayesinde otomatik olarak çalıştırılmasını da sağlayabiliriz. 

Bizler de bu eğitim serisinde bash kabuk dilini **nasıl programlayabileceğimiz** üzerinde duruyor olacağız. Burada bahsi geçen "kabuk dilinin programlanması" bash özelinde "**bash shell scripting**" olarak geçiyor. Bu tanımı Türkçe olarak "**bash kabuk senaryolaştırması**" olarak da ifade edebiliriz. Buradaki "**senaryolaştırma**" ifadesi biraz garip bir tanım olsa da aslında yapacağımız işi gayet iyi özetliyor. Zira programlama yaparken aslında durumlara özel senaryolar yazacağımız ve kabuk da bu senaryoya uygun hareket edeceği için "**programlama**" yerine "**senaryolaştırma**" ifadesi de doğru bir çağrışım yapabilir. Tüm bu kavram açıklamalarına ek olarak "**shell script**" ifadesi Türkçe kısaca "**betik"** olarak da tabir edilebiliyor. Programlama işlemine "**betik programlama"**, oluşturacağımız "**script dosyalarına**" da kısaca "**betik**" denebiliyor yani. Aslında nasıl isimlendirildiğinin çok da bir önemi yok. Sadece ileride farklı isimler ile duyduğunuz zaman şaşırmamanız için kısaca bahsetmek istedim.

## 1.2.2 Betik Programlamanın Yapısı

Bash kabuğu aslında hem komut yorumlayıcısı hem de bir programlama dilidir. Komut yorumlayıcısı işlevi, sistem üzerindeki araçlar ile kullanıcı arasındaki arabirimi sağlar. Kabuk sayesinde bu araçları bulup, çalıştırabilir ve gerektiğinde sonlandırabiliriz. Programlama dili olması ise, gerektiğinde sistem üzerindeki araçların organize şekilde birleştirilerek kullanılmasına imkan verir. Komutlar tek bir dosya içerisinde uygun şekilde toparlandığında, pek çok aracın tek bir dosya üzerinden tek bir komutla yönetilebilmesi mümkün olur. Kısacası, kabuk programlama ile kolayca tam ihtiyacımıza uygun çözümler sunabilen çok yönlü sistem yönetimi araçlarına sahip oluruz. Zaten kabuklar, mevcut araçların etkili biçimde bir arada çalıştırılabilmesi için bize programlanabilme imkanı sunarlar.

## 1.2.3 Kullanılan Bash Sürümü ve Yeniliklerin Takibi

Elbette zaman içinde bash kabuğunda yenilikler olacaktır. Yani burada ele alınan sürüm sizin okuduğunuz dönemde eskimiş olabilir. Hatta siz kasıtlı olarak bu kitapta ele alınandan daha eski bir bash kabuğunu da kullanıyor olabilirsiniz. Peki bu durumda bu kitaptaki bilgiler, ele alındığı(bash v5.1) sürüm haricinde hükümsüz mü ? 

Kesinlikle hayır. Sürümler arasındaki farklılıklar genellikle mevcut hataların düzeltilmesi veya yeni alternatif çözümlerin(özellikler ve araçlar) sunulması şeklindedir. Güncellemeler eski sürümdeki yapıları değiştirmekten kaçınır çünkü halihazırda yazılmış olan betiklerin yeni sürümlerde çalışmaz hale gelme ihtimali vardır. Herhangi bir nedenle mevcut bir aracın ya da özelliğin temel çalışmasını etkileyecek şekilde değiştirilmesi gerekirse, mevcut olanı değiştirmek yerine değişikliği içeren yeni bir araç ya da özellik sunulur. Bu sayede eski özellikler ve araçlar yeni sürümlerde de kullanılabilir olurken, yeni ihtiyaçlara cevap verebilen yeni araçlar ve özellikler de sunulmuş olur. En nihayetinde kabuk üzerindeki değişikler var olanı bozmadan yeni çözümler sunmak için yapılır. Kabuk güncellemeleri geriye dönük uyumluluk içerisindedir. 

Bu sebeplerle kullanmakta olduğunuz bash sürümü hangisi olursa olsun, sürümler arasındaki farklılıkları görmek adına "değişim notlarına" kısaca göz atmanız yeterlidir. Değişim notlarına göz attığınızda, genellikle mevcut özelliklerin iyileştirilmesi ya da alternatif olarak aynı işi kolaylaştırıcı özelliklerin getirildiğini teyit edebilirsiniz. Ben değişim notlarına bakmanız için doğrudan bir bağlantı adresi sunmuyorum çünkü bu adresin sizin okuduğunuz dönemde geçersiz olma ihtimali var. Sadece kısa bir internet araştırması ile sürümler arasındaki tüm değişimlerin detaylı listesine kolaylıkla ulaşabilirsiniz. 

## 1.2.4 Neden Bash Programlama Öğrenmeliyiz ?

Halihazırda bu kitabı okuduğunuza göre Bash programlamayı önemli bulduğunu varsayabiliriz. Yine de kısaca Bash kabuğunu programlama becerisi ve bize sağlayacağı katkılar neden önemli diyenler için, olası senaryolara bir kaç örnek verelim.

### 1.2.4.1 Otomatikleştirilebilir işleri yerine getirir.

Hangi amaçla olursa olsun her gün sistem yönetimi için tekrar ettiğiniz rutinleri düşünün. Günlük rutinler için kısa sürede hazırlayıp kullanabileceğiniz bir betik yazsanız ve her gün zamandan tasarruf etseniz fena mı olur ?

En basit işlerden en karmaşık sorunlara kadar, kabuk üzerinde defaatle uygulamanız gereken her türlü işi kısa sürede betik hazırlayarak otomatikleştirebilirsiniz. Bu sayede siz veya siz yokken sizin yeteneklerinize ihtiyaç duyan kişiler bu betikler üzerinden spesifik sorunları kolayca çözümleyebilir. Özetle betik dosyaları bizim yardımcı sistem yöneticilerimizdir.  

### 1.2.4.2 Sistem Üzerindeki Her Araçtan Faydalanılabilir

Kabuk programlamanın esas amacı araçlar arasında yapıştırıcı görevi görmektir. Sistemde yüklü bulunan araçları bir arada organize şekilde çalıştırabilmemizi sağlar. Zaten kabuk tek başına bir anlam ifade etmez. Kabuk kullanımını güçlü kılan şey sistemde yüklü bulunan araçlardır. Kabuk yalnızca bu araçların çalıştırılması ve çıktılarının başka araçlara aktarılarak tekrar işlenebilmesi için gereken ortamı sağlar. Kabuğu orkestra şefi gibi düşünebilirsiniz. Sesler müzisyenlerin çaldığı aletlerinden gelir ancak tüm müzisyenlerin uyum içinde çalmasını sağlayan şeftir. 

Örnek bir senaryoda; betik dosyama, "öncelikle python dili oluşturulmuş olan program dosyasını çalıştır, dosyanın ürettiği çıktılar doğrultusunda perl dili ile oluşturulmuş programı çalıştırıp en son elde edilen çıktıları bir dosyaya yazdır" diyebilirim.

Yaptığımız işlem sistem yönetim komutlarını tek bir dosyada düzenli olarak toparlamak olduğu için, sistemi yönetirken yapabileceğimiz gibi farklı programlama dilleri ile geliştirilmiş olan araçların ortak paydada çalışmasını sağlayabiliyoruz. Böylelikle temel işlevleri yerine getiren pek çok farklı aracı bir arada kullanarak karmaşık sorunlara çözüm üretebiliriz. Zaten unix felsefesi gereği sistem üzerindeki araçlar genellikle tek bir işi en iyi şekilde yapmak üzere hazırlanmıştır. İşini en iyi şekilde yapan araçların kombinasyonu organize şekilde çalıştırılarak sınırsız çeşitlilikte çözüm yolu sunabilirler. Kabuk kullanımını güçlü kılan da zaten bu yaklaşımdır. 

Ayrıca farklı programlama dilleri ile kabuğun sunduğu, "araçların ortak çalıştırılması" imkanını elde etmek de mümkündür. Ancak pek çok durumda geliştirme aşamasının uzun ve zorlu olmasının yanı sıra, araçların esnekliği kabuğa oranla düşük olacaktır. 

### 1.2.4.3 Etkileşimli Kullanımda Ve Sistem Yönetiminde Verimliliğimizi Artırır

Bash kabuk programlamayı öğrenirken aslında bash kabuğunun yapısını öğreneceğimiz için programlama haricinde etkileşimli kullanımda da pek çok yetiye sahip olacağız. Yani bash kabuğuna sahip sistemleri çok daha efektif şekilde anlık olarak konsoldan yönetebiliyor olacağız. Ayrıca sistem üzerinde işlerimizi otomatikleştirmek istediğimizde yaptığımız işlemeler hakkında daha detaylı bilgi sahibi olmamız gerekir. Dolayısıyla kabuk programlarken sistemi daha yakından tanıma fırsatı bulabiliriz.

## 1.2.5 Özetle

Betik programlamanın sağladığı imkanlar üzerine pek çok örnek verebiliriz. Kısacası söz konusu sistemi yönetmek olduğunda kabuk bizim dostumuzdur. Dostumuz olan kabuğu daha yakından tanımak onu daha etkili kullanabilmemizi sağlar. Söz konusu kabuk tercihi olduğunda da alternatiflerine oranla yaygınlığı dolayısı ile "Bash" kabuğunu öğrenmek makul bir yaklaşımdır. Bu eğitimin esas amacı da bash kabuğunun programlanabilir yapısı üzerinden kabuğu daha yakından tanıyabilmemizdir. 

Betik programlamanın tüm bu özelliklerini dikkate aldığımızda; ihtiyaçlarımıza göre script yazarak bizler için çalışan ve yorulmak bilmeyen binlerce sistem yöneticisi üretebiliriz.

Eğer bash kabuğu sizin için sihirli bir kutuysa, baştan belirteyim hepsi illüzyondan ibaret. Birlikte bash kabuğunun tüm numaralarını deşifre edeceğiz. 

Hazırsanız bu üstün gücü nasıl kontrol edebileceğimizi öğrenmeye başlayalım :)
