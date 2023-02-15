# ControlNet

ControlNet, ek koşullar ekleyerek difüzyon modellerini kontrol etmek için kullanılan bir Neural Network yapısıdır.

![img](github_page/he.png)

Bu, Neural Network bloklarının ağırlıklarını "kilitli" bir kopyaya ve "eğitilebilir" bir kopyaya kopyalar.

"Eğitilebilir" olan koşullarınızı öğrenir. "Kilitli" olan modelinizi korur.

Böylece, küçük resim çiftleri veri kümesiyle eğitim, üretim için hazır difüzyon modellerinizi yok etmeyecektir.

"Sıfır konvolüsyon", hem ağırlığı hem de önyargısı sıfırlanan 1×1 konvolüsyondur.

Eğitimden önce, tüm sıfır konvolüsyonları sıfır değeri üretir ve ControlNet herhangi bir bozulmaya neden olmaz.

Hiçbir katmandaki öğeler sıfırdan eğitilmez. Hala ince ayar yapılır. Orijinal modeliniz güvendedir.

Bu, küçük ölçekli veya hatta kişisel cihazlarda eğitim yapmayı mümkün kılar.

Ayrıca, modellerin/ağırlıkların/blokların/katmanların birleştirilmesine/değiştirilmesine/ofsayt ayarlanmasına da olanak sağlar.

### SORU CEVAP

S: Bi dakika ya, bir conv katmanının ağırlığı sıfırsa, gradyan da sıfır olacaktır ve ağ hiçbir şey öğrenmeyecektir. Neden "sıfır konvolüsyon" işe yarıyor?

C: Bu doğru değil. Burada bir açıklama bulabilirsiniz --> docs/faq.md. 

# Stable Diffusion + ControlNet

Yukarıdaki basit yapıyı 14 kez tekrarlayarak, istikrarlı bir difüzyon kontrolü sağlayabiliriz:

![img](github_page/sd.png)

Katmanları birleştirme şeklimizin hesaplama açısından verimli olduğuna dikkat edin. Orijinal SD kodlayıcısının gradyanları depolamasına gerek yoktur (kilitli orijinal SD Kodlayıcı Blok 1234 ve Orta). Eklenen birçok katman olmasına rağmen, gereken GPU belleği orijinal SD'den çok daha büyük değildir. GREAT!!!!

# Üretim için Hazır, Önceden Eğitilmiş Modeller

Öncelikle yeni bir conva environment'i oluşturun.

    conda env create -f environment.yaml
    conda activate control

Tüm modeller ve tespit ediciler Hugging Face sayfasından indirilebilir (https://huggingface.co/lllyasviel/ControlNet). SD modellerinin "ControlNet/models" klasörüne, tespit edicilerin ise "ControlNet/annotator/ckpts" klasörüne yerleştirildiğinden emin olun. HED kenar tespiti modeli, Midas derinlik tahmini modeli, Openpose vb. dahil olmak üzere, gerekli tüm önceden eğitilmiş ağırlıkları ve tespit modellerini Hugging Face sayfasından indirdiğinizden emin olun.

Bahsi geçen link bu modellerle birlikte 9 Gradio uygulaması sağlıyor.

Bütün test görselleri bu klasörde bulunabilir --> "test_imgs".

[Arxiv Link](https://arxiv.org/abs/2302.05543)
