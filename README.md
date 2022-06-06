- 👋 Hi, I’m @onur54yetim
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
onur54yetim/onur54yetim is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
# EESEC 448
Merhaba arkadaşlar. Bu sayfada **OpenCV**'nin **OpenCV for Beginners** isimli resmi kursunu referans olacağız. Bu kursa 

https://opencv.org/course-opencv-for-beginners/

bağlantısından ulaşabilirsiniz. Kursa kayıt ücreti $117. Ben bu kursa  

https://www.kickstarter.com/projects/opencv/opencv-for-beginners

bağlantısından çok önce kayıt olup $57 ödemiştim. Ayrıca **Adrian Rosebrock** tarafından kurulan **PyImageSearch University** diğer büyük bir referansımız.

https://www.pyimagesearch.com/pyimagesearch-university/

Bu plana yaklaşık olarak $300 gibi bir ücretle kaydolabiliyorsunuz. Adrian'ın **PyImageSearch university** planında **OpenCV 101 — OpenCV Basics** kursunda öğretilen konuların hepsini EEM 448'de işleyeceğiz. Sizlerin bu kurs ve planlara kaydolmanız zorunlu değil. DBS ve bu sayfayı takip ederseniz yeterli olacaktır.

Bu sayfadaki projelerde **Python 3.9.6** ve **OpenCV 4.5.5** kullanacağız. Aşağıda açıklamalarını/sonuçlarını gördüğünüz projelerin **py** uzantılı **Python** kodlarını yukarıda **project** isimli dosyada bulabilirsiniz. Bilgisayarınıza **Python** yüklemek için aşağıdaki resime tıkladığınızda açılan videoyu takip edebilirsiniz. Bu videoda ayrıca **OpenCV** yüklemeye de başlıyoruz ama bir hata ile karşılaşınca yarıda kalıyor.

[![IMAGE ALT TEXT HERE](figure/install-python.jpg)](https://www.youtube.com/watch?v=HwQ46b3KmUw)

Karşılaşılan hatayı çözüp **OpenCV** yüklemeyi tamamladığımız video için aşağıdaki resme tıklayabilirsiniz.

[![IMAGE ALT TEXT HERE](figure/opencv-python-resized.jpg)](https://www.youtube.com/watch?v=9DwK0K8UcAw)
#### Kullandığımız Komutlar
Masaüstünde **EESEC 448** isimli klasörü oluşturduktan sonra **Windows PowerShell**'de gerekli **cd** komutlarıyla bu klasörün içine girin. Sonra **sanal ortam** (İng. **virtual environment**) oluşturmak için 

```
python -m venv opencv-env
```

yazın. Ardından bulunduğunuz dizinde 

```
.\opencv-env\Scripts\activate
```

komutunu girerek sanal ortamı **aktif** hale getirin. Bunu müteakiben sırasıyla 

```
pip install opencv-contrib-python streamlit jupyter moviepy ipykernel matplotlib
```

ve

```
pip install pyautogui mediapipe mime
```

komutlarını koşturarak bilgisayarımızda **OpenCV** koşturabilmek için gerekli olan bütün **paket** ve **kütüphane**leri yükleyin.

#### Visual Studio Code'a Sanal Ortamın Kaydedilmesi/Tanıtılması
Yukarıdaki videolarda bilgisayarımıza **Python** yükledikten sonra **opencv-env** isimli bir sanal ortam oluşturup içerisine **OpenCV**'yi ve bağımlı olduğu kütüphaneleri yükledik. Derste kullanacağımız **Visual Studio Code** (VSC) editöründe kod yazarken kullanacağımız **OpenCV** fonksiyonları hakkında yardım alabilmek için VSC'ye sanal ortamımızı kaydetmemiz/tanıtmamız lazım. Bu işlem için aşağıdaki resme tıklayınca açılan videoyu izleyin.

[![IMAGE ALT TEXT HERE](figure/opencv_env_VSC.jpg)](https://youtu.be/6Z5lM1WqBXU)

Ara sınavda **OpenCV**'yi bilgisayarımıza direk değil de **sanal ortam**a yüklememizle ilgili bir soru soracağım.

## Proje 1: Resim Yükleme ve Görüntüleme (load-display-image)
### Yüklenen Resmin Üzerine Yazı Yazma, Resmi Yeniden Boyutlandırma, Ekranda Görüntüleme ve Dosyaya Kaydetme
Bu egzersizde **OpenCV** kütüphanesinden **imread()**, **putText()**, **resize()**, **imshow()** ve **imwrite()** fonksiyonlarını kullanacağız. Resim yüklemek için kullandığımız fonksiyon olan **imread()**, argüman (yani giriş) olarak uzantısıyla beraber resim/fotoğraf ismi kabul ediyor. Yani fonksiyona *string* veri tipinde resmin uzantılı ismini giriş olarak veriyoruz. Mesela burada fotoğrafımızın ismi **IMG_20210616_202539.jpg** olduğundan **imread('IMG_20210616_202539.jpg')** şeklinde fonksiyonu çağırdığımızda resmi bizim ismini verdiğimiz değişkene atıyor. Bu arada gözden kaçırmayın, bütün fonksiyonları her zaman **cv2** anahtar kelimemizin sonuna **nokta** koyup çağırıyoruz, çünkü **cv2** yazdığımız kodda **OpenCV** kütüphanesini temsil ediyor. Zaten bu yüzden her kodumuzun başında **import cv2** diye bir komutla **OpenCV**'yi aktif hale getirmiş oluyoruz. Sonuç olarak, eğer **IMG_20210616_202539.jpg** isimli bir fotoğrafı **OpenCV**'de **resim** isminde bir değişkene atamak istiyorsak, o zaman aşağıdaki kodu koşturmalıyız.

```
import cv2
resim = cv2.imread('IMG_20210616_202539.jpg')
```

Aşağıdaki kod resmin **yüksekliğini** (height), **genişliğini** (width) ve BGR (Blue-Green-Red yani Mavi-Yeşil-Kırmızı) kanal sayısını (channels) **print** komutuyla ekrana basıyor. Burada yükseklik **satır sayısı**na, genişlik **sütun sayısı**na eşit. Aşağıdaki kod satırında **resim.shape[0]** ve **resim.shape[1]** komutları sırasıyla resmin yükseklik ve genişliğini piksel cinsinden bir sayı olarak ekrana basıyor. Kanal sayısı olan **resim.shape[2]** hakkında ara sınavdan önceki haftalarda konuşacağız.

```
print('yükseklik = %i   genişlik = %i   kanal sayısı = %i' %(resim.shape[0], resim.shape[1], resim.shape[2]))
```

Aşağıdaki videoyu izleyerek yukarıda bir kısmı açıklanan ve tamamı aşağıda verilen kodu gerçekleyebilirsiniz.

[![IMAGE ALT TEXT HERE](figure/imread_puttext_resize_imwrite.jpg)](https://youtu.be/622veo4_lDw)

```
import cv2 # OpenCV kütüphanesine erişim
resim = cv2.imread('IMG_20210616_202539.jpg') # resim yükle
print('yükseklik = %i   genişlik = %i   kanal sayısı = %i' %(resim.shape[0],resim.shape[1],resim.shape[2]))
# resmin üzerine yazı yazalım
font = cv2.FONT_HERSHEY_SIMPLEX # font tipi
org = (300, 300) # yazının içinde bulunduğu dikdörtgenin sol alt köşesi
fontScale = 7 # font büyüklüğü
color = (0, 0, 0) # BGR sırasında yazının renk kodu
thickness = 12 # yazının kalınlığı
yaziliResim = cv2.putText(resim, 'Gumushane', org, font, fontScale, color, thickness, cv2.LINE_AA)
# resmi yeniden boyutlandır, dosyaya kaydet ve ekranda görüntüle
s = 0.2 # scale - ölçek
dim = (int(s*resim.shape[1]), int(s*resim.shape[0])) # boyut
kucukResim = cv2.resize(yaziliResim, dim, interpolation = cv2.INTER_AREA)
cv2.imwrite('Gumushane.jpg', kucukResim, [cv2.IMWRITE_JPEG_QUALITY, 100])
cv2.imshow("Uzerine yazi yazilmis ve yeniden boyutlandirilmis resim", kucukResim)
cv2.waitKey(0) # klavyede herhangi bir tuşa basana kadar ekranda görüntüle
```

## Proje 2: Web Kamerası (web-cam-stream)
Video dediğimiz şey ard arda yakalanan (İng. **capture**) resimlerin ekranda seri halde görüntülenmesinden başka birşey değil. Burada **FPS** kavramı karşımıza çıkıyor. Yani **Frame per Second**, Türkçesi **saniyedeki kare sayısı**. Aşağıdaki animasyonda [2] aynı hareketin değişik FPS değerlerinde yakalanmış halini izleyebilirsiniz. Animasyonda da görüldüğü gibi yüksek FPS değerleri ayrıntıları gözlemleyebilmeyi artırsa da daha fazla işlem yapıldığından dolayı bilgisayarı yoracaktır. Karşımıza çıkan FPS kavramını Sinyaller-Sistemler ve Haberleşme derslerinde gördüğünüz **örnekleme frekansı** (İng. sampling frequency) olarak düşünebilirsiniz.

<img src="https://www.productioncrate.com/news/wp-content/uploads/2019/08/ezgif-1-e18c2f9c89ad.gif" alt="FPS simulation" height="200"/>

Genelde FPS değeri standart web kameraları için 30. Bilgisayarımızın web kamerasını OpenCV kullanarak aşağıdaki gibi açabiliriz.

```
cap = cv2.VideoCapture(0)
```

Burada **VideoCapture** web kamerasına erişmek için bizim kullanımımıza sunulmuş OpenCV'nin **videoio** ana modülünde yer alan bir sınıf (class). Bu komuta 0 girişini verdik çünkü bilgisayarımızda eğer bir web kamerası varsa OpenCV o kameraya 0 kodunu atamış. Eğer birden fazla kamera varsa, o zaman argüman olarak 0 değil de 1, 2, ... girebiliriz. Bu arada **VideoCapture()** komutunun bize döndürdüğü değişkene **capture** kelimesinin kısaltması olan **cap** ismini uygun bulduk zira **capture** yakalamak demek ki web kamerası da saniyede otuz kez görüntüyü yakalayarak bize video sağlamış oluyor. OpenCV'de **VideoCapture** sınıfı web kamerası başarıyla açıldı mı açılmadı mı kontrol etmemiz için Türkçesi **acildi mi?** olarak tercüme edilebileek bir fonksiyon kullanımımıza sunuyor: **isOpened()**. Yukarıda **VideoCapture()** komutunun bize döndürdüğü **cap** değişkenini kullanarak kamera açıldı mı açılmadı mı aşağıdaki gibi kontrol edelim.

```
if (cap.isOpened() == False): ## eğer açılmadıysa
    print('Web kamerasına erişimde sorun yaşandı!')
else: ## eğer açıldıysa
    print('Kameranın FPS değeri %i.' %cap.get(cv2.CAP_PROP_FPS))
```

Eğer kamera yoksa veya erişimde (veya bağlantıda) bir sıkıntı yaşandıysa o zaman ekrana **Web kamerasına erişimde sorun yaşandı!** yazılacak. Aksi durumda kameradan kareler (İng. frame) sürekli geliyor olacak ve web kamerasının FPS değerini ekrana basacağız. Kameraya başarıyla eriştiğimizi kabul ederek devam ediyoruz. Şimdi görüntü sürekli gelmeye devam edeceğinden, web kamerası kare yakaladığı müddetçe aktif olacak bir döngü oluşturalım. Bu döngü içine her girişte web kamerasından resmi alıp **frame** isimli bir değişkene atayalım. Döngüden çıkmadan yakalanan renkli resmi ekranda **imshow()** komutu ile görüntüleyelim ve eğer kullanıcı **'q'** tuşuna bir an bile basarsa (imlecin görüntülediğimiz video ekranı üzerine tıklı olması lazım) o zaman o anda **frame** değişkeninde RAM hafızadaki resmi hard diskte dosyaya yazıp hem döngüden çıkalım hem de programı sonlandıralım.

```
import cv2
cap = cv2.VideoCapture(0)
if cap.isOpened() == False:
    print('Web kamerasına erişimde sorun!')
else:
    print('Kameranın FPS değeri %i.' %cap.get(cv2.CAP_PROP_FPS))
while cap.isOpened() == True:
    ret, frame = cap.read() # web kamerası ile kare yakala
    if ret == True: # eğer kareyi yakaladıysak
        cv2.imshow('web kamerasi renkli resim', frame) # yakalanan kareyi ekranda görüntüle
        if cv2.waitKey(1) & 0xFF == ord('q'): # eğer bir an bile q'ya basarsa
            cv2.imwrite('web kamerasi resim.jpg', frame, [cv2.IMWRITE_JPEG_QUALITY, 100]) # dosyaya yaz 
            break # ve döngüden çık
    else: # eğer kareyi yakalayamadıysak
        print('Kare yakalanamadı!') # ekrana uyarı mesajı yaz
        break # ve döngüden çık
cap.release() # release serbest bırak demek
cv2.destroyAllWindows() # bütün pencereleri kapat ve programı sonlandır
```

Video için aşağıdaki resme tıklayınız.
[![IMAGE ALT TEXT HERE](https://www.manmade2.com/wp-content/uploads/2016/10/webCm1.png)](https://youtu.be/0LjEFyVVs0g)

## Proje 3: Filtreleme (filtering)
Görüntü işleme denince belki de akla gelen ilk şey olan **filtreleme** ile devam ediyoruz. Burada OpenCV kütüphanesinin Görüntü İşleme ana modülünde (**imgproc**) hazır olan filtrelerden normalize edilmiş kutu filtresi (İng. normalized box filter) **blur()**, istatistikteki en popüler dağılım olan Gaussian (öbür ismiyle Normal) fonksiyonu kullanan Gaussian filtresi **GaussianFilter()**, yine istatistikte bir algoritma olarak karşımıza çıkan medyan filtresi **medianBlur()** ve de Gaussian filtresinin piksel şiddet değişimlerinin çok olduğu yerleri bulandırmayan ve resmi aynen Snapshot uygulamasında olduğu gibi oldukça artistik hale getiren versiyonu olan **BilateralFilter()** komutlarını kullanarak ilk önce web kamerasından gelen video akışını filtreleyeceğiz. Ardından da aynı komutları tek bir resim üzerine uygulayıp sonuçları inceleyeceğiz (**ÖDEV 1**). Yukarıda isimleri verilen filtrelerle ilgili bir tutorial'a ihtiyacı olanlar derste baktığımız [3]'den faydalanabilirler. Yazdığımız kod aşağıda.

```
import cv2
cap = cv2.VideoCapture(0) # web kamerasını aç
while True:
    ret, frame = cap.read() # frame yakaladığımız görüntü yani kare
    k = 15 # kernel size - pencere boyutu
    # aşağıda değişik filtrelerle resmi filtreleyelim
    # filtered = cv2.blur(frame, (k,k))
    # filtered = cv2.GaussianBlur(frame, (k,k), 0)
    # filtered = cv2.medianFilter(frame, k)
    # filtered = cv2.bilateralFilter(frame, k, 90, 90)
    windowText = '(%i x %i) pencere boyutu ile filtrelenmis video' %(k,k)
    cv2.imshow('web kamerasi', frame)
    cv2.imshow(windowText, filtered)
    if cv2.waitKey(1) & 0xFF == ord('q'): # eğer bir an bile q'ya basılırsa -->
        cv2.imwrite('web kamerasi.jpg', frame, [cv2.IMWRITE_JPEG_QUALITY, 100])
        cv2.imwrite('web kamerasi filtrelenmis.jpg', filtered, [cv2.IMWRITE_JPEG_QUALITY, 100])
        break # --> döngüyü sonlandır
cap.release()
cv2.destroyAllWindows()
```

Bu kodun değişik filtre ve parametreler için koşturulmasını görmek için aşağıdaki resme tıklayın. Açılan videoda ayrıca **EESEC 448**'de verilecek ekstra puan ve ödevlerle ilgili bilgi de mevcut. Herşeye ek olarak yaptığımız ilk iki projedeki bazı fonksiyonları kullanarak web kamerası kodu çalıştırılınca gelen video üzerine **dinamik** bir şekilde (1) yakalanan kare numarasını yazdırma, (2) farklı isimlerle resim kaydetme ve (3) kaydedilen bu resimler hakkındaki bilgiyi yine dinamik bir biçimde konsol ekranına yazdırma işlemlerini de videoda bulabilirsiniz. Videonun sonunda ilk ödev sözlü olarak açıklanıyor. Ara sınav notuna +3 puan eklemek isteyenler yazdıkları kodu bana email atsınlar. Ödevin son teslim tarihi ve vakti 31 Mart 2022 saat sabah 9:15.

[![IMAGE ALT TEXT HERE](https://docs.opencv.org/3.4/filter.jpg)](https://youtu.be/gbO0RVemXB0)

## Proje 4: Görüntü İşleme Hızını Hesaplama
Filtreleme dersinde kullandığımız **BilateralFilter()** komutu üç girişe sahipti. İlk girişi olan pencere boyutunu parametresinin filtrelemeye olan etkisini yukarıdaki videoda ve derste görmüştük. Bilateral filtre gördüğümüz öbür üç filtreden farklı olarak k değerinin artmasıyla artan işlem yükünden dolayı işlem hızına tekabül eden FPS'yi azaltıyor. Biz de derste bu hızı Pyhthon'ın **time** paketini [4] kullanarak hesaplayıp resim üzerine **putText()** komutu ile yazdırarak görselleştireceğiz. Aşağıdaki kodun yazılmasını ve koşturulmasını kodun altındaki resme tıklayarak izleyebilirsiniz.

```
import cv2
import time
cap = cv2.VideoCapture(1)
timePrevious = time.time()
while True:
    ret, frame = cap.read()
    filtered = cv2.bilateralFilter(frame, 27, 75, 85)
    timeCurrent = time.time() # şu anki zaman
    elapsedTime = timeCurrent - timePrevious # geçen zaman
    FPS = 1 / elapsedTime
    text = 'FPS = %.2f' %FPS
    filtered = cv2.putText(filtered, text, (30, 50), 0, 1, (0, 0, 0), 1, 1)
    cv2.imshow('bilateral filtre', filtered)
    print('Bilateral filtre %.5fs\'de koştu.' %elapsedTime)
    timePrevious = timeCurrent
    if cv2.waitKey(1) & 0xFF == ord('q'): # eğer bir an bile q'ya basarsa -->
        break # --> programı sonlandır
cap.release()
cv2.destroyAllWindows()
```

[![görüntü işleme hızını hesaplama](figure/bilateral_filter_processing_speed.jpg)](https://youtu.be/07E6AFL08DA)

Dersi hatırlayacak olursak, ilk önce hızını ölçmek istediğimiz **BilateralFilter()** komutundan hemen önce bilgisayarın içindeki kronometreden faydalanarak **timeStart** ismiyle zamanı yakalamıştık. Görüntü işlemeyi yaptıktan hemen sonra **timeStop** ismiyle yine zamanı yakalayıp **timeElapsed = timeStop - timeStart** şeklinde geçen zamanı hesaplamıştık. Daha sonra kodun üzerinde düşündüğümüzde sonsuz döngüde olduğumuzu göz önünde bulundurarak iki ayrı zaman yakalama yerine bir kez zamanı da yakalayarak görüntü işleme hızımızı ölçebileceğimizi anlamıştık. Yukarıdaki kod bu ikinci metoda ait. Bu metodda döngünün sonundan başa dönmeden hemen önce **timePrevious = timeCurrent** şeklinde yukarıda hesapta kullanılan şu andaki zamanı bir sonraki adım için geçmiş zaman haline getirme işlemi mutlaka yapılmak zorunda. Döngüye her başlandığında zaten yeri geldiğinde o andaki zaman **timeCurrent = time.time()** komutuyla yakalanıyor. Bu işin mantığını kendiniz biraz düşünerek anlamanız lazım.

## Proje 5: Piksel Şiddet Değerleri, Renk Uzayları (RGB - Gri Ton - Siyah Beyaz)
İkinci hafta yaptığımız ilk projede öğrendiğimiz bazı bilgileri burada kullanacağız. Şimdi **albert_einstein.jpg** isminde bir fotoğrafı (yukarıda **project/color-space** dizininde bulabilirsiniz) OpenCV kullanarak bilgisayarımıza okuyalım ve bu renkli resmi analiz edelim. Aşağıdaki kod resmi okur ve ekrana sırasıyla resmin **yüksekliğini** ve **genişliğini** piksel cinsinden basar. Ayrıca fotoğrafın **kanal** sayısı denilen bilgiyi ekrana yazar.

```
img = cv2.imread('albert_einstein.jpg')
print('Yükseklik = %i piksel   Genişlik = %i piksel' %(img.shape[0], img.shape[1]))
print('Kanal sayısı = %i' %img.shape[2])
```

Burada kanal sayısının renkli bir resim için üç olduğunu görüyoruz. Bu şekilde üç kanalın oluşturmuş olduğu renkli bir resme **RGB** resim deniyor. Baş harfleri **Red**-**Green**-**Blue** yani **Kırmızı**-**Yeşil**-**Mavi**. İnsan gözünün yaklaşık olarak kırmızıya %30, yeşile %60 ve maviye %10 duyarlı olduğu kabul ediliyor.
#### Piksel Şiddet Değerleri
Python konsolunda yüklenen fotoğrafın ilk pikselinin (i.e., sol en üst piksel) şiddet değerine ulaşmak için

```
img[0][0]
```

yazarız. Alternatif olarak 

```
img[0,0]
```

de yazılabilir. Bize bir dizi halinde üç değer döndürdüğü gibi veri tipini de **uint8** olarak gösteriyor. Bir pikselin şiddet değeri **8 bit unsigned integer** yani 8 bitlik (1 byte) işaretsiz tam sayı aralığında olabiliyor. Tek kanal için 0 kodu siyahı, 255 ise beyazı temsil ediyor. Ara değerler gri tonları oluşturuyor. Sonuç olarak üç kanalın farklı kombinasyonları aşağıdaki gibi renkleri oluşturuyor. Aşağıda RGB kübünü görebilirsiniz ([5]'in izni ile).

<p align="center"><img src="https://929687.smushcdn.com/2633864/wp-content/uploads/2021/04/opencv_color_spaces_rgb_cube.png?lossy=1&strip=1&webp=1" alt="RGB kübü" height="360"></p>

Renkli resmi yukarıda bahsettiğimiz RGB ağırlıkları olan (0.3, 0.6, 0.1) ile gri tonlu bir resme dönüştürmek ve yeni oluşan gri tonlu resimde yukarıda incelediğimiz sol üst pikselin yeni oluşan şiddet değerini görüntülemek için aşağıdaki satırları koşturalım. Burada kullandığımız **cvtColor()** fonksiyonu **convert color** kısaltması, Türkçe olarak renk uzayları arasında dönüşüm manasına geliyor.

```
imgGray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
imgGray[0][0]
```

Görüldüğü gibi artık üç değer yerine tek bir piksel şiddet değeri var. Bütün piksel şiddet değerleri [0-255] aralığında bir tam sayı değeri alıyor.

<p align="center"><img src="figure/RGB and gray scale resized.jpg" alt="RGB ve gri tonlu resim" width=%100 height=auto></p>

#### Gri Tonlu Resimden Siyah Beyaz Resime
Artık her bir piksele gittiğimizde üç değil bir tane şiddet değeri var. Her bir piksel şiddet değeri bilgisayar hafısaında **uint8** veri tipine uygun olan bir byte'da tutuluyor. İkilik sistemi (binary) hatırlayacak olursak: 1 byte = 8 bit. Toplam alabileceği piksel şiddet değeri 2<sup>8</sup>=256. Burada 0'dan başlandığından dolayı maksimum piksel şiddet değeri 2<sup>8</sup>-1=255 olur.

<p align="center"><img src="figure/gray scale.jpg" alt="gri tonlar ve piksel değerleri" width=%100 height=auto></p>

Resmin üzerindeki her pikselin şiddet değerini eşik değer (İng. threshold) olan T ile kıyaslayalım. Eğer piksel değeri T'den küçükse o zaman o pikselin değerini 0 yapalım, küçük değil de büyük eşitse o zaman da pikselin değerini maksimum değer olan 255 yapalım. Bunun için OpenCV'de **threshold()** fonksiyonunu kullanacağız.

```
(T, imgBW) = cv2.threshold(imgGray, T, 255, cv2.THRESH_BINARY)
```

<p align="center"><img src="figure/gray scale and BW resized.jpg" alt="gri tonlu ve siyah beyaz resim" width=%100 height=auto></p>

Burada OpenCV kullanarak hem video hem gif animasyonu yapan kodları **project/color-space** dizininde bulabilirsiniz diye ekleyelim.

<p align="center"><img src="figure/black and white.gif" alt="resim eşikleme animasyon" width=%100 height=auto></p>

## Proje 6: NumPy Kullanarak Sentetik Resim Oluşturma, Resimleri Birleştirme, Kendi Eşik Fonksiyonumuzu Yazma ve OpenCV ile Hız Bakımından Kıyaslama
Ara sınavdan önceki bu son projemizde döngüleri kullanmayı iyice öğreneceğiz.

## ARA SINAV

### Referanslar
[1] OpenCV 4.5.5 Dökümantasyonu - https://docs.opencv.org/4.5.5/</br>
[2] FPS animasyonu - https://news.productioncrate.com/tag/fps/</br>
[3] OpenCV'de Görüntü Filtreleme (Bulandırma) [A. Rosebrock, pyimagesearch.com] - https://www.pyimagesearch.com/2021/04/28/opencv-smoothing-and-blurring/</br>
[4] OpenCV'de **time** paketi kullanılarak FPS hesaplanması - https://www.geeksforgeeks.org/python-displaying-real-time-fps-at-which-webcam-video-file-is-processed-using-opencv/</br>
[5] OpenCV'de Renk Uzayları Arasında Dönüşüm - https://www.pyimagesearch.com/2021/04/28/opencv-color-spaces-cv2-cvtcolor/</br>
[6] OpenCV'de VideoWrite() komutuyla video oluşturma - https://docs.opencv.org/4.x/dd/d43/tutorial_py_video_display.html</br>
[7] OpenCV'de imageio paketinden faydalanarak gif animasyon yapma - https://pysource.com/2021/03/25/create-an-animated-gif-in-real-time-with-opencv-and-python/</br>
[8] Standard Kütüphane ve **numpy** ile Rasgele Sayı, Dizi ve Matris Üretme - https://machinelearningmastery.com/how-to-generate-random-numbers-in-python/</br>
[9] OpenCV'de Eşikleme (Thresholding) [A. Rosebrock, pyimagesearch.com] - https://www.pyimagesearch.com/2021/04/28/opencv-thresholding-cv2-threshold/</br>
[10] OpenCV'de **Haar Cascade** Metodu ile Yüz Tespiti [A. Rosebrock, pyimagesearch.com] - https://www.pyimagesearch.com/2021/04/05/opencv-face-detection-with-haar-cascades/</br>
[11] Raspberry Pi ve OpenCV kullanarak Pan-Tilt Kamera ile Yüz Takibi [A. Rosebrock, pyimagesearch.com] - https://www.pyimagesearch.com/2019/04/01/pan-tilt-face-tracking-with-a-raspberry-pi-and-opencv/</br>
[12] Haar Cascade ile Yüz ve Göz Tespiti (OpenCV tutorial) - https://docs.opencv.org/4.x/db/d28/tutorial_cascade_classifier.html</br>
[13] OpenCV ile Yeşil Top Tespiti (Takibi) - https://www.pyimagesearch.com/2015/09/14/ball-tracking-with-opencv/</br>
