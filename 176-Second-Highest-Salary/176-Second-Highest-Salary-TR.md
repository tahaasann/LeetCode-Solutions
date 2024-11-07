# 176. Second Highest Salary

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
1. **Employee Tablosu:**
    - ```id```(int): Her çalışan için benzersiz bir kimlik numarasıdır.
    - ```salary```(int): Çalışanın maaşını temsil eder
    

**Görev:** Employee tablosundan, ikinci en yüksek farklı maaşı bulmak. Eğer ikinci en yüksek maaş yoksa, ```null``` (Pandas'ta ```None```) döndürmek.

### Adım 1: Problemi Anlama
- Girdi: Employee tablosu (id ve salary sütunları).
- Çıktı: İkinci en yüksek farklı maaş değeri. Eğer sadece bir benzersiz maaş varsa, ```null``` döndür.

### Adım 2: Problemi Parçalara Ayırma
1. Benzersiz Maaşları Bulma: İlk olarak, tüm benzersiz maaşları elde etmeliyiz.
2. Sıralama: Bu benzersiz maaşları büyükten küçüğe doğru sıralamalıyız.
3. İkinci En Yüksek Maaşı Seçme: Sıralanmış listeden ikinci elemanı seçmeliyiz.
4. Sonucu Dönüştürme: İkinci en yüksek maaş varsa döndür, yoksa ```null``` (None) döndür.

### Adım 3: Algoritma Tasarlama
1. Benzersiz maaşları elde et.
2. Maaşları büyükten küçüğe sırala.
3. İkinci elemanı seç.
4. İkinci eleman yoksa ```None``` döndür.

### Adım 4: Gerekli Veri Yapılarını ve Fonksiyonları Belirleme
- **Veri Yapıları:**
    - ```employee```: pandas DataFrame

- **Fonksiyonlar:**
    - ```unique()```: Benzersiz değerleri elde etmek için.
    - ```sort_values()```: Sıralama yapmak için.
    - ```iloc[]```: Belirli bir indeksteki değeri almak için.
    - ```shape```: DataFrame boyutlarını kontrol etmek için.

### Adım 5: Kodlama
```py
import pandas as pd

def second_highest_salary(employee: pd.DataFrame) -> pd.DataFrame:
    """
    Employee tablosundan ikinci en yüksek farklı maaşı bulur.
    Eğer ikinci en yüksek maaş yoksa, null (None) döndürür.
    
    Args:
    - employee (pd.DataFrame): Employee tablosu
    
    Returns:
    - pd.DataFrame: İkinci en yüksek maaşı içeren DataFrame
    """
    
    # Adım 1: Benzersiz maaşları elde et
    unique_salaries = employee['salary'].unique()
    # 'unique()' fonksiyonu ile 'salary' sütunundaki benzersiz değerleri alıyoruz
    
    # Adım 2: Benzersiz maaşları büyükten küçüğe sırala
    sorted_salaries = sorted(unique_salaries, reverse=True)
    # 'sorted()' fonksiyonu ile maaşları sıralıyoruz
    # 'reverse=True' ile sıralamayı büyükten küçüğe yapıyoruz
    
    # Adım 3: İkinci en yüksek maaşı seç
    if len(sorted_salaries) >= 2:
        second_highest = sorted_salaries[1]
        # Eğer en az iki farklı maaş varsa, ikinci elemanı alıyoruz
    else:
        second_highest = None
        # Eğer sadece bir benzersiz maaş varsa, 'None' atıyoruz
    
    # Adım 4: Sonucu DataFrame olarak döndür
    # Sonucu istenen formatta döndürmek için bir DataFrame oluşturuyoruz
    result = pd.DataFrame({
        'SecondHighestSalary': [second_highest]
    })
    
    return result
```


### Adım 6: Optimizasyon
Bu basit problem için algoritma zaten oldukça verimli. Ancak, daha büyük veri setlerinde performansı artırmak için farklı yöntemler de kullanılabilir. Örneğin, ```nlargest()``` fonksiyonunu kullanarak sadece en büyük iki benzersiz maaşı elde edebiliriz.

**Kullanımı**:
```py
    # Adım 1: Benzersiz maaşları elde et ve büyükten küçüğe sırala
    sorted_salaries = employee['salary'].drop_duplicates().nlargest(2)
    # 'drop_duplicates()' ile benzersiz maaşları alıyoruz
    # 'nlargest(2)' ile en büyük iki maaşı elde ediyoruz
```