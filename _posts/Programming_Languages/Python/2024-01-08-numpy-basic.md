---
layout: single
title: "[Python] numpy 기본 사용법 - 배열 생성, 형변환, 연산, 조건식"
categories: [python]
tags: [Python, numpy]
header:
  teaser: /assets/images/teasers/teaser_python.webp
---

# numpy 기본 사용법 (1) - 배열 생성, 형변환, 차원 확인, 함수를 사용한 연산

## 0. 기본 개요

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

dtype에 원하는 타입 속성을 지정해주면 된다.

`int`, `float`, `str` 등을 사용할 수 있다.

```python
arry = np.array([1, 2, 3, 4, 5], dtype="str")
print(type(arry), arry)

# <class 'numpy.ndarray'> ['1' '2' '3' '4' '5']
```

## 3. numpy 배열의 차원 확인

```python
arry = np.array([1, 2, 3, 4, 5])
print(f"{arry.ndim}차원 배열")

# 1차원 배열
```

## 4. numpy의 함수를 사용한 사칙연산

```python
arr1 = np.array([10, 20, 30, 40, 50])
arr2 = np.array([1, 2, 3, 4, 5])

# 더하기, 빼기, 곱하기, 나누기
plus = np.add(arr1, arr2)
minus = np.subtract(arr1, arr2)
multiply = np.multiply(arr1, arr2)
divide = np.divide(arr1, arr2)

print(plus, minus, multiply, divide, sep="\n")

# [11 22 33 44 55]
# [ 9 18 27 36 45]
# [ 10  40  90 160 250]
# [10. 10. 10. 10. 10.]
```

## 5. numpy의 함수를 사용한 조건식

각각 and, or, not에 포함된 두 조건식은 같은 결과를 리턴한다.

```python
arr1 = np.array([10, 20, 30, 40, 50])

# and 조건
print(arr1[np.logical_and(arr1 > 20, arr1 < 40)])
print(arr1[(arr1 > 20) & (arr1 < 40)])

# or 조건
print(arr1[np.logical_or(arr1 < 20, arr1 > 40)])
print(arr1[(arr1 < 20) | (arr1 > 40)])

# not 조건
print(arr1[np.logical_not(arr1 == 30)])
print(arr1[~(arr1 == 30)])

# [30]
# [10 50]
# [10 20 40 50]
```
