---
layout: single
title: "[Python] 파이썬 모든 패키지 일괄 업데이트"
categories: [python]
tags: [Python, pip, update, upgrade, 패키지, 업데이트]
header:
  teaser: /assets/images/teasers/teaser_python.webp
---

# 파이썬 패키지 일괄 업데이트

파이썬 패키지를 일괄 업데이트 하는 방법은 다음과 같습니다.

## 1. 설치된 패키지 리스트 txt 파일로 저장

파일은 현재 `terminal` 또는 `cmd` 창이 열려 있는 디렉토리에 저장됩니다.

```zsh
$ pip freeze > package.txt
```

## 2. 저장된 txt 파일 수정

`package.txt` 파일을 열어서 `==`부분을 `>=`로 수정합니다.

예를들어, `pandas==1.5.3` 이렇게 되어 있다면 `pandas>=1.5.3`으로 바꿔줍니다.

> 전체 선택을 해서 한번에 바꿔주면 됩니다

## 3. 패키지 일괄 업데이트

```zsh
$ pip install -r package.txt --upgrade
```
