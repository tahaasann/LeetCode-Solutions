# 177. İkinci En Yüksek Maaş

## İçindekiler

- [177. İkinci En Yüksek Maaş](#177-i̇kinci-en-yüksek-maaş)
  - [İçindekiler](#i̇çindekiler)
  - [Problem Özeti](#problem-özeti)
  - [Adım 1: Problemi Anlama](#adım-1-problemi-anlama)
  - [Adım 2: Problemi Parçalara Ayırma](#adım-2-problemi-parçalara-ayırma)
  - [Adım 3: Algoritma Tasarlama](#adım-3-algoritma-tasarlama)
  - [Adım 4: Gerekli Veri Yapılarını ve Fonksiyonları Belirleme](#adım-4-gerekli-veri-yapılarını-ve-fonksiyonları-belirleme)
  - [Adım 5: Kodlama](#adım-5-kodlama)
  - [Adım 6: Optimizasyon](#adım-6-optimizasyon)

## Problem Özeti

**Tablolar:**

1. **Employee Tablosu:**

    -   `id`(int): Her çalışan için benzersiz bir kimlik numarasıdır.
    -   `salary`(int): Çalışanın maaşını temsil eder.

**Görev:** `Employee` tablosundan, ikinci en yüksek farklı maaşı bulmak. Eğer ikinci en yüksek maaş yoksa, `null` (Pandas'ta `None`) döndürmek.

## Adım 1: Problemi Anlama

-   **Girdi:** `Employee` tablosu (`id` ve `salary` sütunları).
-   **Çıktı:** İkinci en yüksek farklı maaş değeri. Eğer sadece bir benzersiz maaş varsa veya hiç veri yoksa, `null` döndür.

## Adım 2: Problemi Parçalara Ayırma

1. **Benzersiz Maaşları Bulma:** İlk olarak, tüm benzersiz maaşları elde etmeliyiz.
2. **Sıralama:** Bu benzersiz maaşları büyükten küçüğe doğru sıralamalıyız.
3. **İkinci En Yüksek Maaşı Seçme:** Sıralanmış listeden ikinci elemanı seçmeliyiz.
4. **Sonucu Dönüştürme:** İkinci en yüksek maaş varsa döndür, yoksa `null` (`None`) döndür.

## Adım 3: Algoritma Tasarlama

1. Benzersiz maaşları elde et.
2. Maaşları büyükten küçüğe sırala.
3. İkinci elemanı seç.
4. İkinci eleman yoksa `None` döndür.

## Adım 4: Gerekli Veri Yapılarını ve Fonksiyonları Belirleme

-   **Veri Yapıları:**
    -   `employee`: pandas DataFrame

-   **Fonksiyonlar:**
    -   `drop_duplicates()`: Benzersiz değerleri elde etmek için.
    -   `nlargest()`: Belirli sayıda en büyük değeri elde etmek için.
    -   `sorted()` : Sıralama yapmak için.
    -   `len()`: Listedeki eleman sayısını bulmak için.

## Adım 5: Kodlama

```python
import pandas as pd

def nth_highest_salary(employee: pd.DataFrame, N: int) -> pd.DataFrame:
    """
    N'inci en yüksek maaşı bulur.

    Args:
        employee: Çalışan bilgilerini içeren DataFrame.
        N: Bulunması gereken en yüksek maaşın sırası.

    Returns:
        N'inci en yüksek maaşı içeren DataFrame veya N'inci en yüksek maaş yoksa null.
    """

    # Maaşları azalan sırada sırala
    sorted_salaries = employee.sort_values('salary', ascending=False)
    # "employee" DataFrame'ini "salary" sütununa göre azalan sırada sıraladım
    # "ascending=False" argümanı, azalan sırada sıralama yapmamı sağladı.

    # Benzersiz maaşları bul
    unique_salaries = sorted_salaries['salary'].unique()
    # "unique()" metodu, "salary" sütununda bulunan bezersiz değerleri
    # bulmamı sağladı.

    # N'inci en yüksek maaş yoksa null döndür
    if N > len(unique_salaries) or N <= 0:
        return pd.DataFrame({'getNthHighestSalary({})'.format(N): [None]})
    # [26. satır]: Eğer N, benzersiz maaşların sayısından büyükse veya
    # N, O'dan küçük veya eşitse şartını deklare ettim.
    #[27. satır]: N'inci en yüksek maaş bulunamadığı durumda geriye None 
    # değeri içeren bir DataFrame döndürür.
    # pd.DataFrame(...): Bu kısım, yeni bir pandas DataFrame oluşturur.
    # 'getNthHighestSalary({})'.format(N): Bu kısım, sütun adını oluşturur.
    # Dinamik bir sütun adı oluşturmak için Python'un string biçimlendirme
    # Özelliği kullanıyoruz. ".format(N)" kısmı {} yerine N değerini koyar.
    # Örneğin N = 2 ise, sütun adı getNthHighestSalary(2) olur.
    # [None]: Bu kısım, sütunun içereceği değeri belirler. None değerini 
    # içeren bir liste oluşturuyoruz. Bu, DataFrame'in bu hücrede None 
    #(veya Pandas'ta NaN olarak gösterilen) değeri içereceği anlamına gelir.

    # N'inci en yüksek maaşı bul ve DataFrame olarak döndür
    nth_salary = unique_salaries[N - 1]
    return pd.DataFrame({'getNthHighestSalary({})'. format(N): [nth_salary]})
    # [42. satır]: Benzersiz maaş listesinden N'inci maaşı seçtimz. 
    # [43. satır]: Bulunan N'inci en yüksek maaşı içeren bir DataFrame 
    # oluşturup döndürdüm. Sütun adını dinamik olarak getNthHighestSalary(N) 
    # şeklinde ayarladım. Burada N fonksiyonun aldığı argümandır.

```

**Örnek**

```py
# Second Highest Salary fonksiyonunu çağıran ve N=2 için sonucu döndüren kod
def second_highest_salary(employee: pd.DataFrame) -> pd.DataFrame:
    """
    Employee tablosundan ikinci en yüksek farklı maaşı bulur.
    Eğer ikinci en yüksek maaş yoksa, null (None) döndürür.

    Args:
    - employee (pd.DataFrame): Employee tablosu

    Returns:
    - pd.DataFrame: İkinci en yüksek maaşı içeren DataFrame
    """
    return nth_highest_salary(employee, 2)

```

## Adım 6: Optimizasyon
Bu problem için nlargest() fonksiyonunu kullanmak zaten oldukça verimli. nlargest() fonksiyonu, en büyük N değeri bulmak için optimize edilmiştir ve tüm veri setini sıralamaktan daha hızlıdır. Daha da büyük veri setleri için, veriyi parçalara ayırarak (chunking) ve her parçada nlargest() uygulayarak işlem süresini daha da azaltabiliriz.