---
layout: single
title: "[Python] 다른 폴더에 module import(호출)하기"
categories: [python]
tags: [python]
header:
  teaser: assets/images/2023-12-18/get_path.png
---

# 다른폴더에 있는 module 호출

바로 본론으로 들어가자면...

파이썬을 배우면서 어떻게 보면 가장 기본적이지만, 헷갈리는 부분이 있었는데

그 중에 하나가 바로 내가 만든 class나 함수를 만들어 놓은 파일을 다른 폴더에서 import 하는 방법이다

여러 경우의 수가 있는데, 한번 살펴 보기로 해보자

## 1.같은 폴더에 있는 파일인 경우

- 가장 간단한 케이스이다

```python
from 다른파일.py import 내모듈
```

## 2.하위 폴더일 경우

```python
from 하위폴더.다른파일.py import 내모듈
```

## 3.상위 폴더일 경우

만약 상위폴더에 접근을 해야할 경우라면, 작업경로에 파일의 새로운 경로를 추가해줘야 한다.

하지만 폴더 구조가 복잡할 경우를 대비해서 제일 상위 폴더를 잡아놓는게 일반적이다.

![copy-path](/assets/images/2023-12-18/get_path.png)

vscode 기준으로 절대 경로를 얻는 방법은 폴더를 오른쪽 클릭 후 copy path를 선택하면 복사가 된다.

```python
import sys
sys.path.append("해당 폴더의 절대 경로")
```

## 4.같은 부모 폴더 안에 있지만 다른 폴더에 있는 파일인 경우

상위 폴더의 경우와 마찬가지로 절대 경로로 불러와야 한다.
