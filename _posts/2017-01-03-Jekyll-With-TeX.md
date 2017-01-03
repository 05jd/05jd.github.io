---
layout: post
title: Rendering LaTeX in Javascript with KaTeX and Jekyll
permalink: latex-equation-rendering-in-javascript-with-jekyll-and-katex
---
{% include katex_import.html %}

[Ref] https://xuc.me/blog/KaTeX-and-Jekyll/

[Ref] http://willdrevo.com/latex-equation-rendering-in-javascript-with-jekyll-and-katex/

웹 포스팅을 시작하면서 항상 걸리던 부분은 수식이다. 정리하고픈 자료는 언제나 수식이 필요했지만 TeX과의 연동은 걸림돌이 많다. (그 핑계로 여태 포스팅을 제대로 한 적이 없다....) 이번에 Jekyll로 페이지 구성을 하면서 어차피 환경설정을 하고 있으니 TeX 연동에 대한 포스팅을 하나 작성해본다.

# Math Engine 설정

Markdown parser로 MathJax를 사용하도록 _config.yml에 설정을 추가하자.
```
markdown: kramdown
kramdown:
  math_engine: mathjax
```

이제 Jekyll build를 해보면 결과 html 파일에서 "math/tex" 태그로 수식이 감싸 있는 것을 볼 수 있다.

# KaTeX 연동
아래와 같이 만들어 KaTeX render를 연동하자.
_include/katex_import.html
```
<!-- Load jQuery -->
<script src="//code.jquery.com/jquery-1.11.1.min.js"></script>
<!-- Load KaTeX -->
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/KaTeX/0.1.1/katex.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/KaTeX/0.1.1/katex.min.js"></script>
```

_include/katex_render.html
```
<script type="text/javascript">
    var tex = document.getElementsByClassName("equation");
    Array.prototype.forEach.call(tex, function(el) {
        katex.render(el.getAttribute("data-expr"), el);
    });
</script>
```

# 사용방법

포스팅을 위한 Markdown file은 아래와 같은 구조로 작성하면 된다.
아래 내용에서 {와 %는 붙여야 한다.
```
---
layout: post
tile: blahblah
---
{ % include katex_import.html % }

본문 내용

{ % include katex_render.html % }
```


# 3. 테스트

{% raw %}
<!-- The Normal Distribution -->
<div class="equation" data-expr="\displaystyle P(x)=\frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x-\mu)^2}{2\sigma ^2}}"></div>
{% endraw %}

    
{% include katex_render.html %} 