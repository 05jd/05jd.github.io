---
layout: post
title: Jekyll에서 TeX 사용하기 
permalink: using-tex-with-jekyll
---
{% include mathjax.html %}
{% include katex.html %}

## MathJax
---

TeX 렌더링을 할 때 많이 사용하는 것이 MathJax다. 사용법은 단순히 header에 추가하면 된다. Jekyll에서는 아래와 같이 사용하면 된다.

1. _inlcude/mathjax.html 파일 생성
2. mathjax.html에 아래 문구 추가  
```    
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
```
3. post 파일 시작 부분에 {\% include mathjax.html \%} 추가 (\는 빼고)

테스트를 해보자.

```
수식은 $$a^2 + b^2 = \sum_{i=0}^n c_i^2$$ 이렇게 표현 됩니다. 
```

> 수식은 $$a^2 + b^2 = \sum_{i=0}^n c_i^2$$ 이렇게 표현 됩니다.

또는

```
\begin{equation}
    R = \mathbb{E}\left[ \sum_{i \geq 0} S_i \right]
\end{equation}
```

\begin{equation}
    R = \mathbb{E}\left[ \sum_{i \geq 0} S_i \right]
\end{equation}


잘 나온다! 
다만 주의할 것은 include에 만들 때 head.html로 만들면 default head.html의 다른 설정을 덮어버리므로 다른 이름을 사용해야 한다.
매번 include를 하기 귀찮아서 head.html에 추가하고 싶었지만 방법은 아직...

## KaTeX
---

MathJax가 사용하기 편하지만 렌더링이 느리다는 단점이 있다. (...라고 어느 블로그에서 말하지만 잘 모르겠다. 보통 포스팅 할때 수식으로 도배하는 경우는 잘 없으니...)
그래서 빠른 렌더링을 위해 KaTeX를 사용하는 분들도 있다. 
이번에 Jekyll로 페이지 구성을 하면서 어차피 환경설정을 하고 있으니 KaTeX 연동에 대해서도 함께 작성해본다.

슬픈 사실은 Github가 Jekyll을 지원하지만 custom plugin은 지원하지 않는다고 한다[2][2].
직접 compile 후 포스팅을 하는 방법을 [2][2]에서 자세히 설명해주고 있으나 여기서는 plugin 없이 KaTeX을 활용하는 방법도 알아보자.

Markdown parser로 MathJax를 사용하도록 _config.yml에 설정을 추가하자.
```
markdown: kramdown
kramdown:
  math_engine: mathjax
```

이제 Jekyll build를 해보면 결과 html 파일에서 "math/tex" 태그로 수식이 감싸 있는 것을 볼 수 있다.

마지막으로 KaTeX을 사용하도록 header에 관련 설정을 추가해야 한다. 
include 폴더에 아래와 같이 두 개의 설정 파일을 만들자. (katex.html, katex_render.html)

```
<!-- Load jQuery -->
<script src="//code.jquery.com/jquery-1.11.1.min.js"></script>
<!-- Load KaTeX -->
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/KaTeX/0.1.1/katex.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/KaTeX/0.1.1/katex.min.js"></script>
```

```
<script type="text/javascript">
    var tex = document.getElementsByClassName("equation");
    Array.prototype.forEach.call(tex, function(el) {
        katex.render(el.getAttribute("data-expr"), el);
    });
</script>
```

이제 다 끝났다. 포스팅 하면서 Markdown 파일을 아래와 같은 구조로 작성하면 된다.
(include 부분에서 역시 \는 제거하면 된다.)

```
---
layout: post
tile: blahblah
---
{\% include katex.html \%}

본문 내용

{\% include katex_render.html \%}
```

수식을 사용해보자. 조금 귀찮다.

```
{\% raw \%}
<!-- The Normal Distribution -->
<div class="equation" data-expr="\displaystyle P(x)=\frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x-\mu)^2}{2\sigma ^2}}"></div>
{\% endraw \%}
```

{% raw %}
<!-- The Normal Distribution -->
<div class="equation" data-expr="\displaystyle P(x)=\frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x-\mu)^2}{2\sigma ^2}}"></div>
{% endraw %}
  
  
{% include katex_render.html %} 
  
   
## Reference
---

\[1\] [https://xuc.me/blog/KaTeX-and-Jekyll/][1]  
\[2\] [https://www.drewsilcock.co.uk/custom-jekyll-plugins][2]  
\[3\] [http://willdrevo.com/latex-equation-rendering-in-javascript-with-jekyll-and-katex/][3]

[1]: https://xuc.me/blog/KaTeX-and-Jekyll/
[2]: https://www.drewsilcock.co.uk/custom-jekyll-plugins
[3]: http://willdrevo.com/latex-equation-rendering-in-javascript-with-jekyll-and-katex/
