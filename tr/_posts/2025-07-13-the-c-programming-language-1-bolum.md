---
layout: post
title: "Kitap: The C Programming Language: A Tutorial Introduction (1. Bölüm)"
lang: tr
lang-ref: tcpl-chapter-1
---

Yaklaşık beş yıl C++ programlama yaptıktan sonra bir süredir C ile programlamaya yapıyorum. C kullanmayı fırsat bilerek yedi yıldır kitaplığımda bulunan, çeşitli okuma girişimlerimin başarısızlıkla sonuçlandığı *[The C Programming Language (K&R, 2. Baskı)][K&R]* kitabını okumaya başladım. Bu Blogda ise ilgili bölümü okurken ve bölümdeki egzersizleri yaparken öğrendiğim, dikkatimi çeken şeyleri paylaşacağım. Bu yazının konusu ise birinci bölüm "*A Tutorial Introduction*" ile ilgili olacaktır.

* İlk ilgimi çeken durum ise şudur: `a`, `b` ve `c` bir tam sayı (`int`) olmak üzere `a = b = c = 0;` toplu atama ifadesi geçerli bir ifade olup *C*'de toplu atamaya dair özel bir sözdizimi (sentaks, *syntax*) olmamasıdır. Bu ifadenin geçerli bir ifade olmasının nedeni atama ifadesinde önce atama operatörünün sağındaki ifadenin değerlendirilmesidir. Örneği şu şekile çevirirsek daha anlaşılır olacaktır: `a = (b = (c = 0));`. Burada `(c = 0)` ifadesinin değeri `0` olup ifadenin hesaplanma adımları aşağıdaki kod bloğunda gösterilmiştir.

{% highlight c %}
int a, b, c;
a = b = c = 0;
/*
  1) a = (b = (c = 0));
  2) a = (b = 0);
  3) a = 0;
*/
{% endhighlight %}

* Diğer bir durum ise `else if` diye bir sentaksın olmamasıdır. `else if` ifadesi aslında `else`'in gövdesindeki bir `if` koşul ifadesinden başka bir şey değildir. Aşağıdaki kod bloğunu (birinci versiyon) ikinci versiyondaki gibi girintili bir şekilde yazmak/düşünmek açıklayıcı olacaktır. 

{% highlight c %}
/* Version 1 */
if (expression_1)
    statement_1
else if (expression_2)
    statement_2
else
    statement_3
{% endhighlight %}

{% highlight c %}
/* Version 2 */
if (expression_1)
    statement_1
else
    if (expression_2)
        statement_2
    else
        statement_3
{% endhighlight %}

* Koşul ifadesi içerisinde atama yapabilmek ve atama ifadesinin değeri atama yapılan değişkenin değeri olduğu (bkz. ilk madde) göz önüne alınarak şöyle temiz kodlar yazılabilir:

{% highlight c %}
int c;
while ((c = getchar()) != EOF) {
    ...
}
{% endhighlight %}

Ancak koşul ifadesi içerisinde istemeyerek yapılan atamalar bulunması zor hatalara neden olabilir[^1].

* Egzersizlerin iyi pratik yaptırdığını söyleyebilirim.
    * Egzersizleri çözerken egzersizin bulunduğu yere kadar olan kısımda verilen sentaksı kullanmaya, kitapta daha gösterilmemiş olan bir sentaksı kullanmamaya dikkat ettim. Örneğin [*modulo*][mod] operatörünü (`R = A % B;`) kullanmak yerine `R = A - (A / B) * B;` işlemi ile kalanı buldum.
    * C kodundan yorumları silme ([Ex. 1-23][ex-1-23]), detab (yazıdan tab karakterlerini boşluğa dönüştürme, [Ex. 1-20][ex-1-20]), entab (boşlukları tab karakterlerine dönüştürme, [Ex. 1-21][ex-1-21]), satır kısaltma ([Ex. 1-22][ex-1-22]) egzersizlerini özellikle faydalı buldum. Genel olarak 1. Bölüm'deki örnek kodların ve egzersizlerin yazı (*string*) işleme kabiliyetini arttırdığını söyleyebilirim. Bölümdeki egzersizlerin çözümlerini [buradan][cozumler] bulabilirsiniz.


---

[^1]: Derleyicinin seçeneklerine bağlı olarak derleme sırasında bu durumlar tespit edilebilir.

[K&R]: https://en.wikipedia.org/wiki/The_C_Programming_Language
[mod]: https://en.cppreference.com/w/c/language/operator_arithmetic.html
[ex-1-23]: https://github.com/maliozcan/the-c-programming-language/blob/master/chapter-1/ex-1-23.c
[ex-1-20]: https://github.com/maliozcan/the-c-programming-language/blob/master/chapter-1/ex-1-20.c
[ex-1-21]: https://github.com/maliozcan/the-c-programming-language/blob/master/chapter-1/ex-1-21.c
[ex-1-22]: https://github.com/maliozcan/the-c-programming-language/blob/master/chapter-1/ex-1-22.c
[cozumler]: https://github.com/maliozcan/the-c-programming-language/blob/master/chapter-1/
