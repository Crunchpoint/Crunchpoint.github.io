---
layout: single
title: "[Oracle] 오라클클라우드 인스턴스 생성"
categories: [oracle]
tags: [oracle, cloud, Free-Tier, instance]
header:
  teaser: /assets/images/teasers/teaser_oracle.webp
---

# 오라클 클라우드 인스턴스 생성

오라클 클라이드에 인스턴스를 생성하고 개인서버로 사용할 수 있는 방법에 대해서 알아보겠습니다.

평생 무료로 사용할 수 있기 때문에 클라우드 서버를 직접 구축해서 공부하거나 개인 프로젝트에 사용하기에 좋다고 생각합니다.

인스턴스 생성에 대해서 알아보기 전에 기본적으로 구획은 생성되어 있다고 가정하겠습니다.

혹시 구획 구성이 되어있지 않다면 **[오라클 클라우드 구획 생성](https://crunchpoint.github.io/oracle/oracle-compartments-copy/){:target="\_blank"}**을 참고하여 생성할 수 있습니다.

## 인스턴스 생성

### _인스턴스_ 검색

오라클클라우드 웹사이트에 접속하고 검색창에 `인스턴스`를 검색하고 검색결과의 `인스턴스`를 클릭합니다.

![oracle-cloud-instance-01](/assets/images/2024/2024-03-07/01.png)

### _인스턴스 생성_ 버튼을 클릭합니다.

![oracle-cloud-instance-02](/assets/images/2024/2024-03-07/02.png)

### _인스턴스_ 생성에 필요한 정보를 입력합니다.

- 이름: 인스턴스 이름을 입력합니다.
- 컴파트먼트에 생성: 생성해 놓은 구획이 있다면 해당 구획을 선택합니다. (구획이 없다면 기본 구획을 선택합니다)

![oracle-cloud-instance-03](/assets/images/2024/2024-03-07/03.png)

- 이미지 및 구성 : oracle linux, ubuntu, centos 등 다양한 이미지를 선택할 수 있습니다.
- shape : 인스턴스의 크기를 선택합니다. (무료티어는 VM.Standard.E2.1.Micro를 선택합니다)

![oracle-cloud-instance-04](/assets/images/2024/2024-03-07/04.png)

- 기본 VNIC정보 : 새 가상 클라우드 네트워크와 서브넷을 생성합니다.

![oracle-cloud-instance-05](/assets/images/2024/2024-03-07/05.png)

- SSH 키 추가 : 자동으로 키 쌍 생성을 선택하고 전용키와 공용키를 모두 저장해서 잘 보관합니다. (SSH 접속을 위해 필요합니다)

![oracle-cloud-instance-06](/assets/images/2024/2024-03-07/06.png)

- 부트 볼륨 : 사용자정의 부트 볼륨 크기 지정을 선택하면 부트 볼륨 크기를 지정할 수 있습니다. (프리티어는 50GB x 2나 100GB x 1 로 구성 가능합니다)

![oracle-cloud-instance-07](/assets/images/2024/2024-03-07/07.png)

## 인스턴스 접속

### 맥OS에서 SSH 접속

맥 환경이라면 다운로드 받은 key와 pub 파일을 .ssh 폴더에 이동후 사용을 권장합니다.

예) /Users/사용자명/.ssh

생성된 인스턴스 화면에서 `인스턴스 액세스`를 확인 해 보면 퍼블릭 IP 주소와 사용자 이름을 확인할 수 있습니다.

- 접속 예시

```zsh
ssh -i ~/.ssh/your_private_key user_name@your_public_ip
```

권한 에러가 발생한다면 아래 명령어로 권한을 변경합니다.

```zsh
chmod 400 ~/.ssh/your_private_key
```

또는 sudo 명령어를 사용하여 접속합니다.

### 윈도우에서 SSH 접속

윈도우 환경에서 테스트를 해보지 않아서 프로그램 정보만 남겨놓습니다.

**[putty](https://www.putty.org/){:target="\_blank"}**라는 프로그램을 사용하여 편하게 접속할 수 있다고 합니다.

## 문제점

최초 임시 퍼블릭 IP를 할당 받은 후에 고정 IP로 변경하고 새로운 SSH키를 생성하여 접속을 시도 했는데 실패가 계속 되었습니다.

인스턴스의 설정과는 관계없이 최초 인스턴스 생성시에 다운로드 받은 SSH키를 사용하여 접속을 시도하니 정상적으로 접속이 되었습니다.
