---
layout: single
title: "[Blog] github 블로그에서 latex 사용하기"
categories: [github-blog]
tags: [github-blog, latex]
header:
  teaser: /assets/images/teasers/teaser_github.webp
---

# github 블로그에서 latex 사용하기

github 블로그에서는 기본즉올 latex을 지원하지 않는다. 따라서 latex문법을 사용하기 위해서는 몇가지 설정을 해주어야 한다.

## 1. \_config.yml 파일 수정

```yaml
# _config.yml

markdown: kramdown
highlighter: rouge
lsi: false
excerpt_separator: "\n\n"
incremental: false
```

## 2. \_include\scipts.html 파일 수정

해당 파일에 맨 아래에 다음과 같은 코드를 추가해준다.

```html
<!-- _include\scipts.html -->

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-AMS-MML_HTMLorMML"></script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    extensions: ["tex2jax.js"],
    jax: ["input/TeX", "output/HTML-CSS"],
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
      processEscapes: true
    },
    "HTML-CSS": { availableFonts: ["TeX"]}
  });
</script>
```

## 3. latex 사용하기

이제 latex문법을 사용하여 아래와 같이 수식을 작성하면 아래와 같이 정상적으로 표시가 된다.

```latex
% 이차방정식

$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$
```

<br />
$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$
<br /><br />

```latex
% 정규분포

$f(x | \mu, \sigma^2) = \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{1}{2} \left(\frac{x - \mu}{\sigma}\right)^2}$
```

<br />
$f(x | \mu, \sigma^2)$ = $\frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{1}{2} \left(\frac{x - \mu}{\sigma}\right)^2}$
