# kod-olarak-matematik-cpp

[Asıl proje: [math-as-code](https://github.com/Jam3/math-as-code)]

Bu, geliştiricilere C++ kod karşılıklarını göstererek matematiksel notasyonu anlamalarını kolaylaştırmayı amaçlayan bir referanstır.

Motivasyon: Akademik makaleler, kendi kendini eğiten oyun ve grafik programcıları için korkutucu olabilir :)

Bu kılavuz henüz tamamlanmadı. Hata görürseniz veya katkıda bulunmak isterseniz, lütfen bir kayıt açın veya bir değişiklik isteği gönderin.


# önsöz
Matematiksel semboller; yazara, bağlama ve çalışma alanına (lineer cebir, küme teorisi, vb.) bağlı olarak farklı şeyler ifade edebilir. Bu kılavuz, bir sembolün tüm kullanımlarını kapsamayabilir. Bazı durumlarda, gerçek dünyada referansları (blog yazıları, yayınlar, vb.) verilerek bir sembolün vahşi ortamda nasıl görünebileceğini gösterilmeye çalışılacaktır.

Daha eksiksiz bir liste için Wikipedia'da [Matematiksel Sembollerin Listesi](https://en.wikipedia.org/wiki/List_of_mathematical_symbols)'ne bakınız.

Basitlik için, buradaki kod örneklerinin çoğu kayan nokta değerleri üzerinde çalışır ve sayısal olarak sağlam değildir. Bunun neden bir sorun olabileceğine dair daha çok ayrıntı için Mikola Lysenko'nun [Sağlam Aritmetik Notlarına](https://github.com/mikolalysenko/robust-arithmetic-notes) bakınız.


# içindekiler


## değişken isim kuralları
Çalışmanın bağlamına ve alanına bağlı olarak çeşitli isimlendirme kuralları vardır ve bunlar her zaman tutarlı değildir. Bununla birlikte, literatürde, aşağıdaki gibi bir deseni takip eden değişken isimleri bulabilirsiniz:

- *s* - skaler için italik küçük harfler (ör. bir sayı)
- **x** - vektörler için kalın küçük harfler (ör. bir 2B nokta)
- **A** - matrisler için büyük harfli harfler (ör. bir 3B dönüşüm)
- *θ* - sabitler ve özel değişkenler için italik küçük harfli Yunan harfleri (ör. [kutup açısı *θ*, *teta*](https://en.wikipedia.org/wiki/Spherical_coordinate_system))

Bu ayrıca bu kılavuzun da biçimi olacaktır.


## eşitlik sembolleri

Eşittir işareti ='e benzeyen bir dizi sembol vardır. Aşağıda birkaç genel örnek görülebilir:

- `=` eşitlik için kullanılır (değerler aynıdır)
- `≠` eşitsizlik için kullanılır (değer aynı değildir)
- `≈` yaklaşık olarak eşittir ifadesi için kullanılır (`π ≈ 3.14159`)
- `:=` tanımlama içindir (A, B olarak tanımlanmıştır)

C++'taysa:

```cpp
#include <iostream>
#include <cmath>

bool yaklasikEsitMi(double a, double b, double epsilon) {
  return fabs(a - b) <= epsilon;
}

int main()
{
    // eşitlik
    if (2==3)
        std::cout << "İki, üçe eşittir.\n";
    // eşitsizlik
    if (2!=3)
        std::cout << "İki, üçe eşit değildir.\n";
    // yaklaşık eşitlik
    if (yaklasikEsitMi(M_PI, 3.14159265359, 1e-5))
        std::cout << M_PI << ", yaklaşık olarak 3.14159265359 değerine eşittir.\n";

    return 0;
}
```

Tanımlama için `:=`, `=:` ve `=` sembollerinin kullanıldığını görebilirsiniz.<sup>[1]</sup>

Örneğin aşağıdaki tanımlama, x'i 2kj'nin farklı bir ismi olarak tanımlar:

![x := 2kj](http://latex.codecogs.com/svg.latex?x%20%3A%3D%202kj)

<!-- x := 2kj -->

C++'ta değişkenlerimizi tanımlamak ve takma adlar sağlamak için tür isimlerini kullanabiliriz:

```cpp
auto x = 2 * k * j;
```

Ancak, bu değişebilir ve sadece o anki değerlerin bir anlık görüntüsünü alır. Bazı diller, matematiksel bir tanımlamaya daha yakın olan ön işlemci #define ifadesine sahiptir.

C++'ta daha doğru bir tanımlama şöyle olabilir:

```cpp
const auto x = 2 * k * j;
```

Öte yandan, aşağıdaki ifade eşitliği temsil eder:

![x = 2kj](http://latex.codecogs.com/svg.latex?x%20%3D%202kj)

<!-- x = 2kj -->

Bu denklem de C++'ta öncekiler gibi yorumlanabilir:

```cpp
const auto x = 2 * k * j;
```


## karekök ve karmaşık sayılar

Bir karekök işlemi şu şekildedir:

![squareroot](http://latex.codecogs.com/svg.latex?%5Cleft%28%5Csqrt%7Bx%7D%5Cright%29%5E2%20%3D%20x)

Programlamada, aşağıdaki gibi bir sqrt fonksiyonu kullanırız:

```cpp
    int x = 9;
    std::cout << sqrt(x);
    // 3
```

Kompleks sayılar, ![complex](http://latex.codecogs.com/svg.latex?a&space;&plus;&space;ib) biçimindeki ifadelerdir, ![a](http://latex.codecogs.com/svg.latex?a) gerçek kısım ve ![b](http://latex.codecogs.com/svg.latex?b) de sanal kısımdır. Sanal sayı ![i](http://latex.codecogs.com/svg.latex?i) şöyle tanımlanır:

![imaginary](http://latex.codecogs.com/svg.latex?i%3D%5Csqrt%7B-1%7D).
<!-- i=\sqrt{-1} -->

C++'ta, karmaşık sayılar için yerleşik fonksiyonlar vardır ve bunlarla karmaşık sayı aritmetiği işlemleri yapılabilir. Örneğin:

```cpp
#include <iostream>
#include <complex>

int main()
{
    //{ re: 3, im: -1 }
    std::complex<double> a(3.0, -1.0);
    //{ re: 0, im: 1 }
    std::complex<double> b(0.0, 1.0);
    std::complex<double> c = a * b;

    //'1 + 3i'
    std::cout << c << '\n';

    std::cout << "Gerçek kısım: " << real(c) << '\n';
    std::cout << "Sanal kısım: " << imag(c) << '\n';

    return 0;
}

```

C++'ta karmaşık sayılarla ilgili birçok işlem daha kolayca yapılabilir, bunlar hakkında daha çok bilgi için GeeksforGeeks'teki [Complex numbers in C++](https://www.geeksforgeeks.org/complex-numbers-c-set-1/) yazısına bakabilirsiniz.


## nokta ve çarpı

Nokta `·` ve çarpım `×` sembolleri, içeriğe bağlı olarak farklı kullanımlara sahiptir.

Ne oldukları belli görünebilir, ancak diğer bölümlere devam etmeden önce ince farkları anlamak önemlidir.

#### skaler çarpım

Her iki sembol de skalerlerin basit çarpımını temsil edebilir. Aşağıdakiler eşdeğerdir:

![dotcross1](http://latex.codecogs.com/svg.latex?5%20%5Ccdot%204%20%3D%205%20%5Ctimes%204)

<!-- 5 \cdot 4 = 5 \times 4 -->

Programlama dillerinde çarpma için yıldız işareti kullanma eğilimindeyizdir:

```cpp
int sonuc = 5 * 4
```

Çoğunlukla, çarpım işareti sadece belirsizliği önlemek için kullanılır (ör. iki sayı arasında). Şurada tamamen atlayabiliriz örneğin:

![dotcross2](http://latex.codecogs.com/svg.latex?3kj)

<!-- 3kj -->

Eğer bu değişkenler skalerleri temsil ediyorsa kod şöyle olur:

```cpp
int sonuc = 3 * k * j
```

#### vektör çarpımı

Bir vektörün bir skaler ile çarpımını veya bir vektörün başka bir vektörle öğe öğe çarpımını göstermek için, genellikle nokta `·` veya çarpı `×` sembolleri kullanmayız. Bunlar, lineer cebirde farklı anlamlara sahiptir.

Daha önceki örneğimizi alıp vektörlere uygulayalım. Öğe öğe vektör çarpımını temsil etmek için, Hadamard çarpımında bir açık nokta `∘` kullanıldığını görebilirsiniz.<sup>[2]</sup>

![dotcross3](http://latex.codecogs.com/svg.latex?3%5Cmathbf%7Bk%7D%5Ccirc%5Cmathbf%7Bj%7D)

<!-- 3\mathbf{k}\circ\mathbf{j} -->

Diğer durumlarda yazar, daire içine alınmış bir nokta `⊙` veya dolu bir daire `●` gibi farklı bir gösterimi açıkça tanımlayabilir.<sup>[3]</sup>

2B vektörleri temsil etmek için kodda dizilerin [x, y] nasıl kullanılacağını aşağıda görebilirsiniz:

```cpp
#include <iostream>
#include <array>

std::array<int, 2> carp(std::array<int, 2> a, std::array<int, 2> b)
{
    std::array<int, 2> tmp;
    for(int i = 0; i < a.size(); i++)
        tmp[i] = a[i] * b[i];
    return tmp;
}

std::array<int, 2> skalerCarp(std::array<int, 2> a, int b)
{
    std::array<int, 2> tmp;
    for(int i = 0; i < a.size(); i++)
        tmp[i] = a[i] * b;
    return tmp;
}


int main()
{
    int s = 3;
    std::array<int, 2> k = {1, 2};
    std::array<int, 2> j = {2, 3};

    std::array<int, 2> tmp = carp(k, j);
    std::array<int, 2> sonuc = skalerCarp(tmp, s);

    for(const auto& s: sonuc)
        std::cout << s << ' ';
        // [ 6, 18 ]

    return 0;
}
```

Benzer şekilde, matris çarpımı da genellikle nokta `·` veya çarpı sembolü `×` kullanmaz. Matris çarpımı daha sonraki bölümlerde ele alınacaktır.


#### nokta çarpım

Nokta sembolü `·` iki vektörün [nokta çarpımını](https://www.wikiwand.com/tr/Nokta_%C3%A7arp%C4%B1m) göstermek için kullanılabilir. Skaler olarak değerlendirildiğinden bazen bu skaler çarpım olarak adlandırılır.

![dotcross4](http://latex.codecogs.com/svg.latex?%5Cmathbf%7Bk%7D%5Ccdot%20%5Cmathbf%7Bj%7D)

<!-- \mathbf{k}\cdot \mathbf{j} -->

Lineer cebirin çok yaygın bir özelliğidir ve üç boyutlu bir vektör için aşağıdaki gibi görünebilir:

```cpp
#include <iostream>
#include <array>
#include <numeric>

int main()
{

    std::array<int, 3> k = { 3, -2, 5 };
    std::array<int, 3> j = { -1, -4, 2 };

    std::cout << std::inner_product(std::begin(k), std::end(k), std::begin(j), 0.0);
    //=> 15

    return 0;
}
```

#### çapraz çarpım

Çarpma sembolü `×`, iki vektörün [çapraz çarpımını](https://www.wikiwand.com/tr/%C3%87apraz_%C3%A7arp%C4%B1m) belirtmek için kullanılabilir.

![dotcross5](http://latex.codecogs.com/svg.latex?%5Cmathbf%7Bk%7D%5Ctimes%20%5Cmathbf%7Bj%7D)

<!-- \mathbf{k}\times \mathbf{j} -->

Bu, kodda şöyle görünecektir:

```cpp
#include <iostream>
#include <vector>

template <typename T, typename U>
std::vector<T> crossProduct(std::vector<T> const &a, std::vector<U> const &b)
{
  std::vector<T> r (a.size());
  r[0] = a[1] * b[2] - a[2] * b[1];
  r[1] = a[2] * b[0] - a[0] * b[2];
  r[2] = a[0] * b[1] - a[1] * b[0];
  return r;
}

int main()
{

    std::vector<int> k = { 0, 1, 0 };
    std::vector<int> j = { 1, 0, 0 };

    std::vector<int> sonuc = crossProduct(k, j);

    for(const auto& s: sonuc)
        std::cout << s << ' ';
        //=> [ 0, 0, -1 ]

    return 0;
}
```

Burada, [0, 0, -1] elde ederiz, bu da hem k'nin hem de j'nin dik olduğu anlamına gelir.


## toplam sembolü

Büyük Yunanca `Σ` ([Sigma](https://www.wikiwand.com/tr/Toplam_sembol%C3%BC)), toplama içindir. Başka bir deyişle, bazı sayıları toplar.

![sigma](http://latex.codecogs.com/svg.latex?%5Csum_%7Bi%3D1%7D%5E%7B100%7Di)

<!-- \sum_{i=1}^{100}i -->

Burada `i=1`, 1'den başlanıp toplama sembolünün üstündeki sayı olan 100'de sonlanacağı söylenmektedir. Bunlar sırasıyla alt ve üst sınırlardır. `Σ`'nın sağındaki *i*, bize ne topladığımızı gösterir. Kodda:

```cpp
    int toplam = 0;
    for (int i = 1; i <= 100; i++) {
        toplam += i;
    }
    std::cout << toplam << '\n';
```

Toplamın sonucunu tutan `toplam`'ın değeri 5050 olur.

**İpucu:** Tam sayılarla, bu model aşağıdaki şekilde optimize edilebilir:

```cpp
    int n = 100; // üst sınır
    int toplam = (n * (n + 1)) / 2;

    std::cout << toplam << '\n';
```

İşte, *i*'nin veya "toplanacak şeyin" farklı olduğu başka bir örnek:

![sum2](http://latex.codecogs.com/svg.latex?%5Csum_%7Bi%3D1%7D%5E%7B100%7D%282i&plus;1%29)

<!-- \sum_{i=1}^{100}(2i+1) -->

Kodda:

```cpp
    int toplam = 0;
    for (int i = 1; i <= 100; i++) {
        toplam += (2 * i + 1);
    }
    std::cout << toplam << '\n';
```

Toplamın sonucu 10200'dür.

Notasyon, bir for döngüsünün iç içe olduğuna benzer şekilde iç içe olabilir. Yazar, sırayı değiştirmek için parantez içine almadığı sürece, en sağdaki toplama sembolünü ilk önce değerlendirmelisiniz. Ancak, aşağıdaki durumda, sınırlı miktarlarla uğraştığımız için, sıranın önemi yoktur:

![sigma3](http://latex.codecogs.com/svg.latex?%5Csum_%7Bi%3D1%7D%5E%7B2%7D%5Csum_%7Bj%3D4%7D%5E%7B6%7D%283ij%29)

<!-- \sum_{i=1}^{2}\sum_{j=4}^{6}(3ij) -->

Kodda:

```cpp
    int toplam = 0;
    for (int i = 1; i <= 2; i++) {
        for (int j = 4; j <= 6; j++) {
            toplam += (3 * i * j);
        }
    }

    std::cout << toplam << '\n';
```

veya

```cpp
    int toplam = 0;
    for (int j = 4; j <= 6; j++) {
        for (int i = 1; i <= 2; i++) {
            toplam += (3 * i * j);
        }
    }

    std::cout << toplam << '\n';
```

Burada her iki kod parçası için de `toplam` 135 olacaktır.


## büyük Pi

[Büyük Pi](https://www.wikiwand.com/en/Multiplication#/Capital_Pi_notation), toplama sembolüne çok benzer, tek farkı bir dizi değerin toplamını değil çarpımını bulmak için kullanılır.

Şuna bakalım:

![capitalPi](http://latex.codecogs.com/svg.latex?%5Cprod_%7Bi%3D1%7D%5E%7B6%7Di)

<!-- \prod_{i=1}^{6}i -->

Bu, kodda şöyle görünebilir:

```cpp
    int sonuc = 1;
    for (int i = 1; i <= 6; i++) {
      sonuc *= i;
    }

    std::cout << sonuc << '\n';
```

`sonuc`, 720 olarak hesaplanacaktır.


## borular

Çubuk olarak da bilinen boru sembolleri, içeriğe bağlı olarak farklı şeyler ifade edebilir. Aşağıda üç yaygın kullanım bulunmaktadır: [mutlak değer](https://www.wikiwand.com/tr/Mutlak_de%C4%9Fer), [Öklid normu](https://www.wikiwand.com/en/Norm_(mathematics)#/Euclidean_norm) ve [determinant](https://www.wikiwand.com/tr/Determinant).

Bu üç özelliğin tümü, bir nesnenin uzunluğunu tanımlar.


#### mutlak değer

![pipes1](http://latex.codecogs.com/svg.latex?%5Cleft%20%7C%20x%20%5Cright%20%7C)

<!-- \left | x \right | -->

*x* sayısı için `|x|`, x'in mutlak değerini belirtir. Kodda:

```cpp
#include <iostream>
#include <cmath>

int main()
{
    int x = -5;
    int sonuc = abs(x);
    std::cout << sonuc << '\n';
    // => 5

    return 0;
}
```


#### Öklid normu

![pipes4](http://latex.codecogs.com/svg.latex?%5Cleft%20%5C%7C%20%5Cmathbf%7Bv%7D%20%5Cright%20%5C%7C)

<!-- \left \| \mathbf{v} \right \| -->

**v** vektörü için `‖v‖`, v'nin Öklid normudır. Bu, ayrıca bir vektörün "büyüklüğü" veya "uzunluğu" olarak da adlandırılır.

Çoğunlukla *mutlak değer* gösterimiyle karıştırılmasını önlemek için çift çubukla gösterilir, ancak bazen tek çubukla da gösteriliyor olabilir:

![pipes2](http://latex.codecogs.com/svg.latex?%5Cleft%20%7C%20%5Cmathbf%7Bv%7D%20%5Cright%20%7C)

<!-- \left | \mathbf{v} \right | -->

İşte bir 3B vektörü temsil etmek için [x, y, z] şeklindeki bir dizinin kullanılışına örnek:

```cpp
#include <iostream>
#include <cmath>
#include <vector>

int uzunluk (std::vector<int> vektor) {
  int x = vektor[0];
  int y = vektor[1];
  int z = vektor[2];
  return sqrt(x * x + y * y + z * z);
}

int main()
{
    std::vector<int> v = { 0, 4, -3 };
    std::cout << uzunluk(v) << '\n';
    //=> 5

    return 0;
}
```

Bu işlemi yapmak için C++'ta birden çok yol vardır, bazılarını This Thread'deki [Euclidean norm](http://thisthread.blogspot.com/2012/03/euclidean-norm.html) yazısında görebilirsiniz, buradan alınan bir gerçekleştirim aşağıdadır:

```cpp
#include <iostream>

#include <boost/numeric/ublas/vector.hpp>
#include <boost/numeric/ublas/io.hpp>

int main()
{
    boost::numeric::ublas::vector<int> uv(3);
    uv[0] = 0;
    uv[1] = 4;
    uv[2] = -3;

    std::cout << "Öklid normu: " << boost::numeric::ublas::norm_2(uv) << std::endl;

    return 0;
}
```


#### determinant

![pipes3](http://latex.codecogs.com/svg.latex?%5Cleft%20%7C%5Cmathbf%7BA%7D%20%5Cright%20%7C)

<!-- \left |\mathbf{A}  \right | -->

Bir **A** matrisi için `|A|`, **A** matrisinin determinantı demektir.

Aşağıda, bir 2x2 matrisin determinantını hesaplayan örnek verilmiştir:

```cpp
#include <iostream>
#include <armadillo>

int main()
{
    arma::mat A = "1 0; 0 1;";
    std::cout << arma::det(A) << '\n';

    return 0;
}
```

Yukarıdaki gerçekleştirimde lineer cebir ve bilimsel bilgi işlem kütüphanesi olan [Armadillo](http://arma.sourceforge.net) kullanılmıştır, derleyebilmeniz için başlık dosyasını programınıza dahil etmeli ve örneğin CMake kullanıyorsanız kütüphaneyi `target_link_libraries(${PROJECT_NAME} -larmadillo)` ile programınıza bağlamalısınız.

Eğer bir kütüphane kullanmak yerine determinant alan fonksiyonu kendiniz yazmak isterseniz GeeksforGeeks'teki [Determinant of a Matrix](https://www.geeksforgeeks.org/determinant-of-a-matrix/), Stack Overflow'daki [Fastest way to calculate determinant?](https://stackoverflow.com/questions/36254193/fastest-way-to-calculate-determinant) ve Code Review'daki [Determinant of a matrix](https://codereview.stackexchange.com/questions/79330/determinant-of-a-matrix) yazılarına bakabilirsiniz. Bunlardan sonuncusundan alınmış gerçekleştirim aşağıdadır:

```cpp
#include <iostream>
#include <vector>

static int CalcDeterminant(std::vector<std::vector<int>> Matrix)
   {
        // Bu fonksiyon matrisin determinantını hesaplar
        // herhangi bir boyuttaki matrisin determinantını özyinelemeli olarak hesaplayabilir
        int det = 0; // determinant değeri burada saklanır
        if (Matrix.size() == 1)
        {
            return Matrix[0][0]; // hesaplama gerekmez
        }
        else if (Matrix.size() == 2)
        {
            // Bu durumda, 2 boyutlu matrisin determinantını bir öntanımlı prosedürde hesaplıyoruz
            det = (Matrix[0][0] * Matrix[1][1] - Matrix[0][1] * Matrix[1][0]);
            return det;
        }
        else
        {
            // Bu durumda, 2'den büyük, örneğin 3x3 boyutlarına sahip bir kare matrisin
            // determinantını hesaplıyoruz
            for (int p = 0; p < Matrix[0].size(); p++)
            {
                //this loop iterate on each elements of the first row in the matrix.
                //at each element we cancel the row and column it exist in
                //and form a matrix from the rest of the elements in the matrix
                std::vector<std::vector<int>> TempMatrix; // to hold the shaped matrix;
                for (int i = 1; i < Matrix.size(); i++)
                {
                    // iteration will start from row one cancelling the first row values
                    std::vector<int> TempRow;
                    for (int j = 0; j < Matrix[i].size(); j++)
                    {
                        // iteration will pass all cells of the i row excluding the j
                        //value that match p column
                        if (j != p)
                        {
                           TempRow.push_back(Matrix[i][j]);//add current cell to TempRow
                        }
                    }
                    if (TempRow.size() > 0)
                        TempMatrix.push_back(TempRow);
                    //after adding each row of the new matrix to the vector tempx
                    //we add it to the vector temp which is the vector where the new
                    //matrix will be formed
                }
                det = det + Matrix[0][p] * pow(-1, p) * CalcDeterminant(TempMatrix);
                //then we calculate the value of determinant by using a recursive way
                //where we re-call the function by passing to it the new formed matrix
                //we keep doing this until we get our determinant
            }
            return det;
        }
    };

int main()
{
    std::cout << CalcDeterminant({{1, 0}, {0, 1}}) << '\n';

    return 0;
}
```


## more...

Like this guide? Suggest some [more features](https://github.com/Jam3/math-as-code/issues/1) or send us a Pull Request!

## Contributing

For details on how to contribute, see [CONTRIBUTING.md](./CONTRIBUTING.md).

## License

MIT, see [LICENSE.md](http://github.com/Jam3/math-as-code/blob/master/LICENSE.md) for details.

[1]: http://mimosa-pudica.net/improved-oren-nayar.html#images
[2]: http://buzzard.ups.edu/courses/2007spring/projects/million-paper.pdf
[3]: https://www.math.washington.edu/~morrow/464_12/fft.pdf
