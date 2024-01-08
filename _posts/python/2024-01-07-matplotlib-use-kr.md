---
layout: single
title: "[Python] matplotlib 에서 한글 사용하기"
categories: [python]
tags: [python, matplotlib]
header:
  teaser: /assets/images/teasers/teaser_python.webp
---

matplotlib에서는 기본적으로 한글을 지원하지 않는다. 따라서 한글을 사용하기 위해서는 한글 폰트를 설정 해줘야 한다.

## 1. 사용중인 os에 설치된 폰트 확인

**설치된** 폰트만 사용할 수 있으므로, 사용중인 os에 설치된 폰트를 확인한다.

1. 윈도우 : `C:\Windows\Fonts` 폴더에 설치된 폰트 확인
2. 맥 : `~/Library/Fonts` 폴더에 설치된 폰트 확인

## 2. matplotlib 폰트 설정

설치된 폰트를 확인 했다면, 한글을 사용할 수 있는 폰트를 찾아 설정한다.

예제에서는 os가 맥인 경우, `AppleGothic` 폰트를 사용하고, 윈도우인 경우 `Malgun Gothic` 폰트를 사용해 보았다.

```python
import sys
from matplotlib import pyplot as plt

plt.rcParams.update(
    {
        "font.family": "AppleGothic" if sys.platform == "darwin" else "Malgun Gothic",
    }
)
```

### update() 메서드에 설정할 수 있는 파라미터

| 파라미터           | 설명                |                 값 (예제)                  |
| ------------------ | ------------------- | :----------------------------------------: |
| font.family        | 폰트 (글꼴 설정)    |              "Malgun Gothic"               |
| font.size          | 폰트 크기           |                     14                     |
| figure.figsize     | 그래프 크기         |                   (14,7)                   |
| figure.dpi         | 해상도 (dpi)        |                    200                     |
| axes.unicode_minus | 음수 기호 깨짐 설정 | True / False (False = 음수 기호 깨짐 방지) |
| axes.grid          | 그래프 격자         |      True / False (True = 격자 생성)       |

등등 그래프에 적용되는 다양한 설정을 할 수 있고, 추가 입력은 딕셔너리 형태로 입력하면 된다.

## 3. 설정한 폰트가 제대로 적용되었는지 확인

```python
import sys
from matplotlib import pyplot as plt


plt.rcParams.update(
    {
        "font.family": "AppleGothic" if sys.platform == "darwin" else "Malgun Gothic",
        "font.size": 12,
        "axes.unicode_minus": False,
        "figure.figsize": (12, 8),
        "figure.dpi": 100,
        "axes.grid": True,
    }
)

plt.plot([-2, -1, 3, 4])
plt.xlabel("x축 한글 표시")
plt.ylabel("y축 한글 표시")
plt.show()
plt.close()
```

### 출력결과

![matplotlib_use_kr](/assets/images/2024-01-07/01.png)

한글과 음수 기호가 제대로 표시되는 것을 확인할 수 있다.
