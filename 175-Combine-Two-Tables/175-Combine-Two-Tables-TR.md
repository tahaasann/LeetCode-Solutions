# 175. Combine Two Tables

## İçindekiler
[Problem Özeti](#problem-özeti)
[Adım 1: Problemi Anlama](#adım-1-problemi-anlama)
[Adım 2: Problemi Parçalara Ayırma](#adım-2-problemi-parçalara-ayırma)
[Adım 3: Algoritma Tasarlama](#adım-3-algoritma-tasarlama)
[Adım 4: Gerekli Veri Yapılarını ve Fonksiyonları Belirleme](#adım-4-gerekli-veri-yapılarını-ve-fonksiyonları-belirleme)
[Adım 5: Kodlama](#adım-5-kodlama)
[Adım 6: Optimizasyon](#adım-6-optimizasyon)

## Problem Özeti

**Tablolar:**
1. **Person Tablosu:**
    - ```personId```(int): Birincil anahtar, her kişi için benzersiz.
    - ```lastName```(varchar): Kişinin soyadı
    - ```firstName```(varchar): Kişinin adı.

2. **Address Tablosu:**
    - ```addressId```(int): Birincil anahtar, her adres için benzersiz.
    - ```personId```(int): İlgili kişinin ```personId```si.
    - ```city```(varchar): Şehir.
    - ```state```(varchar): Eyalet.

**Görev:** Person tablosundaki her kişi için, ilk adı, soyadı, şehir ve eyalet bilgilerini raporlamak. Eğer bir kişinin adresi Address tablosunda yoksa, şehir ve eyalet bilgileri ```null``` olarak raporlanmalı.

### Adım 1: Problemi Anlama
İki tabloyu birleştirerek (join) her kişinin bilgilerini almak istiyoruz. Eğer Address tablosunda bir kişinin adresi yoksa, şehir ve eyalet bilgileri ```Null``` olmalı. Bu, SQL'de sol dış birleştirme (```LEFT JOIN```) olarak bilinir ve pandas'ta ```merge``` fonksiyonu ile gerçekleştirilebilir.

### Adım 2: Problemi Parçalara Ayırma
1. **Birleştirme (Join):** Person tablosunu Address tablosuyla ```personId``` sütunu üzerinden birleştireceğiz.
2. **Seçilecek Sütunlar:** Birleştirme sonucunda ```firstName```, ```lastName```, ```city```, ```state``` sütunlarını alacağız.
3. **Eksik verilerin Yönetimi:** Adres bilgisi olmayan kişiler için ```null``` değerler olacak.

### Adım 3: Algoritma Tasarlama
1. **Birleştirme Türünü Belirleme:** Sol dış birleştirme (```left join```) kullanacağız çünkü tüm Person kayıtlarını almak istiyoruz.
2. **Birleştirilecek Sütunları Belirleme:** ```personId``` üzerinden birleştirme yapacağız.
3. **Sonuç Tablosunu Oluşturma:** İstenen sütunları seçip, gereksiz sütunları atacağız.

### Adım 4: Gerekli Veri Yapılarını ve Fonksiyonları Belirleme
- **Veri Yapıları:**
    - ```person```: pandas DataFrame
    - ```address```: pandas DataFrame

- **Fonksiyonlar:**
    - ```pd.merge()```: DataFrame'leri birleştirmek için.
    - ```fillna()```: Eksik değerleri doldurmak için (opsiyonel - zaten test ettiğimizde boş değerleri kendisi ```null``` değeriyle dolduruyor. ```fillna()``` kullandığımızda hata alıyoruz.)

- **Veri Tipleri:**
    - ```personId```: int
    - ```lastName```, ```firstName```, ```city```, ```state```: varchar (string)

### Adım 5: Kodlama
```py
import pandas as pd

def combine_two_tables(person: pd.DataFrame, address: pd.DataFrame) -> pd.DataFrame:
    """
    Person ve Address tablolarını birleştirerek her kişi için 
    firstName, lastName, city ve state bilgilerini döndürür.
    Adres bilgisi olmayan kişiler için city ve state null olur.
    
    Args:
    - person (pd.DataFrame): Person tablosu
    - address (pd.DataFrame): Address tablosu
    
    Returns:
    - pd.DataFrame: Birleştirilmiş tablo
    """

    # Birleştirme işlemi: Sol dış birleştirme (left join) kullanıyoruz
    merged_df = pd.merge(person, address, on="personId", how='left')

    # İstenen sütunları seçiyoruz
    result_df = merged_df[['firstName', 'lastName', 'city', 'state']]

    # Eksik değerleri 'null' olarak göstermek istersek(fakat hata alırız çünkü çıktı "null" şeklinde çıkar fakat biz direkt null olarak çıktı almak istiyoruz):
    # result_df = result_df.fillna('null')

    return result_df
```


### Adım 6: Optimizasyon
Bu basit birleştirme işlemi olduğu için, daha fazla optimizasyona gerek yoktur. Ancak, büyük veri setleriyle çalışırken performansı artırmak için indeksleme veya belirli sütunları önceden seçmek gibi yöntemler kullanılabilir.