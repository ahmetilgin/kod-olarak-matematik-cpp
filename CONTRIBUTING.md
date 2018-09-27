## Katkı

### Sorunlar

Matematiksel ifadelerde hatalar, anlatım veya dilde problemler ya da bir sembol veya denklemin koda çevrilmesiyle ilgili halledilmesi gereken durumlar görürseniz lütfen [bir hata kaydı](https://github.com/maidis/kod-olarak-matematik-cpp/issues/new) oluşturun.

Lütfen yeni bir tane oluşturmadan önce [mevcut kayıtları](https://github.com/maidis/kod-olarak-matematik-cpp/issues) arayın.

### Değişiklik İstekleri

Değişiklik istekleri göndermeniz harika olur! :tada: Yeni bir özellik ekleyecekseniz veya büyük değişiklikler yapacaksanız ilerlemeden ve değişiklik üzerinde çalışmadan önce tartışmak için bir hata kaydı açmak en iyisidir.

Diğer bazı yönergeler:

- Değişiklik isteklerinizi temiz tutun ve yalnızca eklemek istediğiniz özellikle ilgili olan parçaları değiştirin. Farklı özellikler veya düzeltmeler için en iyisi bağımsız değişiklik istekleri olarak sunulmasıdır.
- Bazı unicode semboller satır içi olarak kullanılabilir, ancak genel olarak bunun amacı, literatürde yaygın olarak bulunan denklemleri açığa çıkarmaktır. Lütfen LaTeX SVG'leri kullanın.
- Şu anda denklemler [bu LaTeX düzenleyicisi](http://www.codecogs.com/latex/eqneditor.php) kullanılarak oluşturuluyor, dosya biçimi olarak SVG seçiliyor ve ortaya çıkan bağlantılar doğrudan görüntülere bağlanıyor.
- Ayrıca, resmin hemen altına bir Markdown yorumu olarak ham LaTeX'i de ekleyin. Yorum biçimi olarak şunu kullanın: `<!-- comment -->`
- Kod `cpp` ile vurgulanan sözdiziminde olmalı ve [bu biçim kılavuzunu](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md) takip etmelidir.
- Lütfen yeni değişikliklerde genel yazı biçimini korumaya çalışın.

#### LaTeX Örneği

LaTeX'te yeni bir denklemin nasıl görüneceğine dair bir örnek:

```md
![piecewise1](http://latex.codecogs.com/svg.latex?f%28x%29%3D%20%5Cbegin%7Bcases%7D%20%5Cfrac%7Bx%5E2-x%7D%7Bx%7D%2C%26%20%5Ctext%7Bif%20%7D%20x%5Cgeq%201%5C%5C%200%2C%20%26%20%5Ctext%7Botherwise%7D%20%5Cend%7Bcases%7D)

<!--    
f(x)= 
\begin{cases}
    \frac{x^2-x}{x},& \text{if } x\geq 1\\
    0, & \text{aksi takdirde}
\end{cases} 
-->
```

İşlenen sonuç:

![piecewise1](http://latex.codecogs.com/svg.latex?f%28x%29%3D%20%5Cbegin%7Bcases%7D%20%5Cfrac%7Bx%5E2-x%7D%7Bx%7D%2C%26%20%5Ctext%7Bif%20%7D%20x%5Cgeq%201%5C%5C%200%2C%20%26%20%5Ctext%7Baksi%20takdirde%7D%20%5Cend%7Bcases%7D)
