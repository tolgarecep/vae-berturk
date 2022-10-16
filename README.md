- VAE was trained (with different training strategies and three different dim_z settings) on various Turkish datasets that were tokenized with BERTurk tokenizer.
- Quality of representations VAEs, BERTurk and TF-IDF provided were tested by using them in classification tasks.
- Results show that the best training strategy is to balance training set size and number of epochs and not increase one while keeping the other low (relative to sizes and numbers that are being played with).
- Best latent space dimensionality setting for VAE while dealing with Turkish sentences is 128, although the conclusion here might change with the completion of incomplete experiments. 

## experiments
- `vae.ipynb`: Train VAE models with [shentianxiao/text-autoencoders](https://github.com/shentianxiao/text-autoencoders) for different training strategies and dim_z values.
- `berturk.ipynb`: Get BERTurk representations for sentences from evaluation datasets. Notebook pops each split list once to get rid of empty strings, and computes for 500 samples at each run to properly work on Google Colab.
- `tf-idf.ipynb`: Numericalize and represent sentences (in usually high-dimensional vectors) with statistical measure TF-IDF.
- `berturk_svm.ipynb`: Model BERTurk representations with SVM and tune hyperparameter C.
- `vae_svm.ipynb`: Get VAE representations and model with SVM.

## VAE training dataset
Dataset was imported from [turkish-corpus](https://www.kaggle.com/datasets/redrussianarmy/turkish-corpus) and arranged with `tr_corpus.ipynb`. 

## representation evaluation datasets
**text categorization (dünya, ekonomi, sağlık, spor, kültür, siyaset, teknoloji)**: 3430, 1470; 700x7  
**sentiment analysis (neg, pos)**: 6000, 2489; 4252+4237  
**sentiment analysis (neu, neg, pos)**: 5000, 1500 
**text categorization (6 categories)**: 5000, 1000; 6x1000

## training comparison
| vae training | text categorization (7) | sentiment analysis (binary) | sentiment analysis (neu, neg, pos) | text categorization (6)
| ------------- | ------------- | ------------- | ------------- | ------------- |
| 180K, 6 epochs | 0.4496598639455782 | 0.6753716351948573 | 0.858 | 0.573 |
| 360K, 3 epochs | 0.563265306122449 | 0.6894335074327039 | 0.866 | 0.637 |
| 1080K, 1 epoch | 0.42585034013605444 | 0.6801928485335476 | 0.856 | 0.454 |
| 2000K, 1 epoch, `dim_z=128` | 0.6891156462585034 | 0.706709521896344 | 0.8646666666666667 | 0.676 |
| 2000K, 1 epoch, `dim_z=256` | 0.689795918367347 | 0.7183607874648453 | 0.8653333333333333 | 0.693 |
| 2000K, 1 epoch, `dim_z=512` | 0.7006802721088435 | 0.7063077541181197 | 0.8693333333333333 | 0.706 |


## dim_z comparison
vae training: 360/3
| model/method | text categorization (7) | sentiment analysis (binary) | sentiment analysis (neu, neg, pos) | text categorization (6)
| ------------- | ------------- | ------------- | ------------- | ------------- |
| vae `dim_z=64` | 0.5571428571428572 | 0.685415829650462 | 0.8646666666666667 | 0.657 |
| vae `dim_z=128` | 0.563265306122449 | 0.6894335074327039 | 0.866 | 0.637 | 
| vae `dim_z=256` | 0.4530612244897959 | 0.6838087585375653 | 0.8586666666666666 | 0.59 | 
| berturk | 0.8625850340136054 | 0.8782643631980716 | 0.9333333333333333 | 0.9130000000000001 |
| tf-idf | 0.9108843537414966 `dim_z=46389` | 0.9023704298915227 `dim_z=8792` | 0.882 `dim_z=8119`| 0.954 `dim_z=14190` |

## reconstruction
### 360/3, `dim_z=128`, sentiment analysis (neu, neg, pos); 0.866  
#### training examples
*Bu sırada bir atlı tarafından öldürüldü.*  
Bu sırada , bir süre sonra da öldü  

*Albüm "En İyi Reggae Albümü" dalında Grammy ödülünü aldı.*  
Albümde "The " " adlı şarkıyla " The " " adlı şarkıyla seslendirmiştir

#### test examples
*Profesyonel kariyerine Torino kulübünde başladı.*  
Profesyonel kariyerine 2009 yılında ise 2 gol attı  

*Ama daha fazla para lazım olunca kumar oynar.*  
Ama bu yüzden de de kendi içindeki insanlar vardı  

*Kendiliğinden ışık yayan gök cismi.*  
İnsanlar arasındaki bir su vardır  

*ürünü yeni sipariş ettim. elime ne zaman ulaşır bilmiyorum, iyi sonuçlar elde edeceğimi umuyorum. fiyatı işlevine göre oldukça uygun. umarım bu üründen memnun kalırım...*  
) ki bu nedenle de de de , bu nedenle de de de de de de de de de de de de de de de de de de de de de de de de  

*Anadolu Üniversitesi ve Marmara Üniversitesi mezunudur.*  
İstanbul Üniversitesi , İstanbul Üniversitesi Hukuk Fakültesi ' nde doğdu  


### 360/3, `dim_z=128`, text categorization (7); 0.563265306122449  
#### test examples
*7 mart tarihine dikkat sosyal medya devi facebook 7 mart tarihinde gerçekleştir ##eceği etkinlik için basın mensuplarına davetiye gönderme ##ye başladı peki bu tarihte ne olacak t ##si 20 00 da yeni _ z ##ela ##nda da gerçekleştirilecek etkinlikte facebook un haber kaynağı nın yeni görünümü paylaş ##ılacak yeni gelecek tek  sütun ##lu tasarım ile yeni türde reklamlar için bir hazırlık olduğuna kesin gözüyle bak ##abiliriz özellikle reklam konusunda son dönemde sıkıntı yaşayan facebook un yeni arama motoru gr ##ap ##h _ se ##arch ün de vereceği ivme ve yeni tasarım ##da olması beklenen büyük fotoğraf kutu ##cuk ##lu tasarım*  
" C " ) , " C " - 1 ) , " C " - 1 ) , " n " ) , bu nedenle , bu nedenle , bu nedenle , bu  

*salon ve do ##t işbirliğiyle karşınızda iki _ kişilik _ bir _ oyun salon do ##t işbirliğiyle gerçekleştirilen ve salon _ ik ##s ##v de 12 kez sahne ##lenecek olan yeni iki _ kişilik _ bir _ oyun 12 kasım _ pazartesi 21 00 de pr ##öm ##iyer yapıyor karşılaşan tanış ##an bakış ##an şaka ##laşan dokun ##an seviş ##en seven sahip ##lenen öz ##leyen kıskan ##an aldat ##an kandır ##an terk ##eden terk ##ede ##meyen tutun ##an tutun ##amayan unuta ##n ve hatırla ##yan yeniden ve yeniden deney ##en iki kişinin yaşam boyu sürdürdü ##k ##leri bir ilişki oyunu*  
Örneğin , bu nedenle , bu nedenle , bu nedenle , bu nedenle , bu nedenle , bu nedenle , bu nedenle , bu nedenle , bu nedenle , bu nedenle , bu nedenle  

## interpolation
### 360/3, `dim_z=128`, sentiment analysis (neu, neg, pos); 0.866  
#### training examples  
**Albüm " En İyi Reg ##ga ##e Albüm ##ü " dalında Gram ##my ödülünü aldı .**  
Albüm ##de " The " " adlı şarkı ##yla " The " " adlı şarkı ##yla seslendir ##miştir  
Albüm ##ün ilk albümün ##de " The " " adlı şarkı ##yla birlikte seslendir ##miştir  
Bu albüm ##de ilk kez ilk kez " The " adlı şarkı ##yla birlikte yazdı  
Bu arada bir süre sonra da ilk kez tekrar çıktı  
Bu sırada , bir süre sonra da öldü  
**Bu sırada bir at ##lı tarafından öldürüldü .**
