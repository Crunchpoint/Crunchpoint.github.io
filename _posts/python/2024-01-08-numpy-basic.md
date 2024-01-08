---
layout: single
title: "[Python] numpy 기본 사용법"
categories: [python]
tags: [Python, numpy]
header:
  teaser: /assets/images/teasers/teaser_python.webp
---

# numpy 기본 사용법

1. 데이터 분석에서 pandas와 함께 자주 사용되는 라이브러리로, 다차원 배열을 효과적으로 처리할 수 있도록 도와주는 라이브러리이다.
2. numpy는 기본적으로 array타입을 사용하고 큰 특징으로는 python의 list와 다르게 같은 타입의 데이터만 저장할 수 있다.
   - 만약 다른 타입의 데이터를 저장하려고 하면 numpy는 자동으로 가장 포괄적인 형태로 형변환을 시도한다.

## 1. numpy 배열 생성

```python
import numpy as np

arry = np.array([1, 2, 3, 4, 5])
print(type(arry), arry)

# <class 'numpy.ndarray'> [1 2 3 4 5]
```

## 2. numpy 배열의 형변환

```python
arry = np.array([1, 2, 3, 4, 5], dtype="string")
```
