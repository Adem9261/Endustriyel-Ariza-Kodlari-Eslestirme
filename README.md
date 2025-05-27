# 🛠️ Endüstriyel Arıza Kodları Eşleştirme Projesi

Bu projede, endüstriyel sistemlerde ortaya çıkan arıza açıklamalarını doğal dil işleme (NLP) yöntemleri kullanarak teknik hata kodları ile eşleştirmektir. Bu sayede teknik personelin sistemde oluşan arızaları daha hızlı ve doğru bir şekilde sınıflandırması sağlanır.

---

## 1. Hafta — Veri Hazırlama ve Önişleme
1.1. Veri Toplama

ilk olarak endüstriyel otomotiv ve makineleri çekilmiştir daha sonra bu verilerin hata kodu açıklamasının olduğu sütunlarına ayrılmıştır.
Ayırılan açıklama sütunlarını birleştirerek yeni bir csv (birlesik_aciklamalar.csv) dosyasına kaydedilmiştir.
yeni csv dosyası üzerinde aşağıdaki işlemleri uyguladım.
-Bu çalışmam ise `Endustriyel_Ariza_Kodlari_Eslestirme.ipynb` adlı kaynak dosyasında bulunmaktadır

1.2. Veri Ön İşleme
Açıklama verileri üzerinde gerçekleştirilen temel işlemler:

-  Küçük harfe çevirme  
-  Noktalama işaretlerinin kaldırılması  
-  İngilizce stopword (gereksiz kelimeler) temizliği  
-  Tokenizasyon (metni kelimelere ayırma)  
-  Lemmatizasyon ( Kelimeler köklerine indirgenerek farklı çekimler aynı forma getirilmiştir.) 
-  Stemming: Kelimenin kökünü bulmak için yapılmıştır

---

## 🔍 Proje Özeti

CSV dosyasından alınan açıklamalar şu adımlardan geçirilmiştir:

- Verinin `pandas` ile yüklenmesi ve genel incelemesi
- Eksik verilerin kontrolü
- Cümle ve kelime seviyesinde ayrıştırma (`tokenization`)
- İngilizce stopwords (nltk) ile filtreleme
- Lemmatizasyon ve stemleme işlemleriyle kelimelerin kök formlarının çıkarılması
- Cümle listesi oluşturularak yapısal analiz yapılması
- Veri ön işleme adımları, nltk python, pandas ve re kütüphaneleri kullanılarak Python'da uygulanmıştır.

---

## 📊 Zipf Yasası Analizi

Veri setindeki kelimelerin frekans dağılımı analiz edilerek log-log grafiği çizilmiştir. Sonuçlar Zipf yasasına uygunluk göstermektedir. 
> 🔎 `Endustriyel_Ariza_Kodlari_Eslestirme.ipynb` dosyasında ilgili analizler ve grafikler yer almaktadır.

---

## 🛠️ Kullanılan Teknolojiler ve Kütüphaneler

- Python 3.x
- Jupyter Notebook
- NLTK, pandas, numpy, gensim, scikit-learn

---

## 2. Hafta: TF-IDF Vektörleştirme ve Word2Vec Modelleri 

### 2.1. TF-IDF Vektörleştirme
TF-IDF yöntemiyle metinler vektörleştirilmiş ve giriş metniyle cosine similarity skorları hesaplanmıştır. 
Her veri türü için ilk 5 benzer metin ve skorları listelenmiştir.

### 2.2. Cosine Similarity (Kosinüs Benzerliği) Karşılaştırması
Tüm modellerin giriş metniyle olan ortalama ve en yüksek cosine similarity skorları hesaplanmış ve tablo halinde karşılaştırılmıştır.

> 📌 Detaylı analizler: `Endustriyel_Ariza_Kodlari_Eslestirme.ipynb` içinde

### 2.3. Jaccard Benzerlik Matrisi
TF-IDF ve Word2Vec modellerinin her birinin ilk 5 benzer metin seçimi alınıp, bu seçimler arasında Jaccard benzerlik skoru hesaplanarak 18x18'lik bir skor matrisi oluşturulmuştur.

> 📌 Detaylı analizler: `Endustriyel_Ariza_Kodlari_Eslestirme.ipynb` içinde

### 2.4. Word2Vec Model Eğitimi ve İnceleme
16 farklı parametre kombinasyonuyla Word2Vec modeli eğitilmiştir (CBOW / SkipGram, window=2/4, dim=100/300). Giriş metnine benzerlikler cosine similarity ile değerlendirilmiştir.

---

## 📌 Sonuçlar ve Değerlendirme

- En yüksek ortalama skor: `word2vec_lemmatized_skipgram_win4_dim300`
- En anlamlı sonuçları sunanlar: `tfidf_lemmatized` ve `skipgram_win4_dim300`
- SkipGram modelleri CBOW’a göre, dim=300 modelleri dim=100’e göre daha başarılı olmuştur.
- TF-IDF yüzeysel benzerlik sunarken, Word2Vec anlamsal yakınlık sağlamıştır.
- Jaccard skorları TF-IDF modelleri arasında yüksek, Word2Vec modelleri arasında ise çeşitlilik göstermektedir.

---

## 📥 Nasıl Çalıştırılır?
1. Çalışmayı bilgisayarınıza indirip, arşivden klasöre çıkarıp 'notebooks/Endustriyel_Ariza_Kodlari_Eslestirme.ipynb` dosyasını jupyter notebok da açınız ve tüm hücreleri sırasıyla çalıştırın, sonuçları listelenecektir.
2. Kendi veri setlerinizin analizini yapmak isterseniz sonraki adımları takip edin.
3. `notebooks/`, `models/` klasörü ve `data/` klasörü hazır olmalıdır.
4. Veri setlerinizi 'data' klasörü içerisine atın, `Endustriyel_Ariza_Kodlari_Eslestirme.ipynb` dosyasında veri seti yükleme kısmında, veri setlerinizin isimlerini doğru şekilde yazın ve birleştirilecek sütun isimlerini doğru şekilde belirtin.
5. Hücreleri sırayla çalıştırın.
6. Çıktılar ve karşılaştırmalar otomatik olarak üretilir.