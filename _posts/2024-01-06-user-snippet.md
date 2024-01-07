---
layout: single
title: "[vscode] user snippet 사용법"
categories: [vscode]
tags: [vscode, user snippet]
header:
  teaser: /assets/images/teaser_default.jpg
---

## user snippet 이란?

vscode에서 제공하는 기능으로, 자주 사용하는 코드를 미리 저장해두고 사용할 수 있게 해주는 기능이다

## user snippet 사용법

### 1. vscode에서 `ctrl + shift + p`를 눌러서 명령어 창을 띄운다

### 2. 명령어 창에 `snippet`을 입력하고 `Configure User Snippets`를 선택

![user-snippet](/assets/images/2024-01-06/01.png)

### 3. `snippet`을 사용할 영역을 선택 (3가지 옵션)

1. 글로벌 영역에서 사용할 경우 `New Global Snippets file...`
2. 특정 프로젝트에서만 사용할 경우 `New Snippets file for 'project name'`
3. 특정 언어에서만 사용할 경우 `New Snippets file for 'language name'`

### 4. `snippet`의 이름을 입력

본인이 알아보기 쉽게 이름을 지어주면 된다. (ex. `print hello python`)

### 5. 사용할 코드를 입력

처음 스니펫을 생성하면 아래와 같이 비어있는 `snippet`이 생성된다

![user-snippet](/assets/images/2024-01-06/02.png)

이를 쉽게 작성하기 위해 [https://snippet-generator.app](https://snippet-generator.app){: target="\_blank"} 에서 `snippet`을 생성할 수 있다

사이트에 접속을 하면 아래와 같은 화면이 나오는데 각각 입력할 내용은 아래와 같다

![user-snippet](/assets/images/2024-01-06/03.png){: width="80%"}

1. description : `snippet`의 설명
2. Tab trigger : `snippet`을 호출할 때 사용할 문구
3. Your snippet : `snippet`으로 사용할 코드를 입력
4. 오른쪽 에 생성된 코드를 확인하고 오른쪽 하단의 `Copy snippet`을 눌러서 복사
5. vscode에서 `snippet`을 생성한 파일에 복사한 코드를 붙여넣기

```json
{
  "test snippet": {
    "prefix": "my_snippet",
    "body": ["print(\"hello python\")"],
    "description": "test snippet"
  }
}
```

### 6. `snippet` 사용

`snippet`을 사용할 때는 `Tab trigger`에 입력한 문구를 입력하고 `Tab`키를 누르면 된다

![user-snippet](/assets/images/2024-01-06/05.gif){: width="70%"}
