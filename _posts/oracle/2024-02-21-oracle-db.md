---
layout: single
title: "[Oracle] 오라클클라우드 Free-Tier DB 생성하기"
categories: [oracle]
tags: [oracle, cloud, Free-Tier, DB]
header:
  teaser: /assets/images/teasers/teaser_oracle.webp
---

# 오라클 클라우드 Free-Tier

`오라클` 하면 흔히 가격이 비싼 DBMS로 알려져 있습니다.

이는 사실이기도 하지만 만약 개인적으로 사용하거나, 연습용으로 사용할 목적이라면 오라클 클라우드에서 제공하는 Free-Tier를 이용하여 무료로 DB를 생성하고 사용할 수 있습니다.

특히, 맥 사용자라면 오라클 DB를 로컬환경에서 설치하고 사용하는 방법이 굉장히 번거롭기 때문에, 클라우드를 이용하는 것이 훨씬 편리합니다.

## 오라클 클라우드 Free-Tier 제공 사항

아래 사항들은 오라클 클라우드 Free-Tier에서 제공하는 사항입니다.

![oracle_free_tier](/assets/images/2024-02-27/01.png)

- AWS 클라우드와 비교했을 때, 오라클 클라우드 Free-Tier는 무료로 제공하는 사양이 매우 높고, 평생 무료라는게 가장 큰 장점인것 같습니다.

## 오라클 클라우드 Free-Tier 가입하기

오라클 클라우드 Free-Tier에 가입하려면 **[오라클 클라우드 홈페이지](https://www.oracle.com/kr/cloud/){:target="\_blank"}**에 접속하여 가입을 진행하면 됩니다.

가입을 하고 나면, 오라클 클라우드에 로그인하여 다음과 같은 화면을 볼 수 있습니다.

![oracle_free_tier](/assets/images/2024-02-27/02.png)

## 오라클 클라우드 자율운영 DB 생성하기

검색창에 `자율운영`을 입력하면 다음과 같은 화면을 볼 수 있습니다. 여기서 `자율운영 데이터베이스`를 클릭하여 DB를 생성합니다.

![oracle_free_tier](/assets/images/2024-02-27/03.png)

`자율운영 데이터베이스 생성` 버튼을 클릭하고

![oracle_free_tier](/assets/images/2024-02-27/04.png)

다음과 같이 필요한 정보들을 입력하면 됩니다.

표시 이름과 데이터베이스 이름은 임의로 정해주시면 되고, `트랜잭션 처리`를 선택합니다.

![oracle_free_tier](/assets/images/2024-02-27/05.png)

비밀번호를 입력하고, `자율운영 데이터베이스 생성` 버튼을 클릭하면 DB가 생성됩니다.

![oracle_free_tier](/assets/images/2024-02-27/06.png)

DB가 생성되고 클릭해서 들어가면 다음과 같은 화면을 볼 수 있습니다.
DB에 접속을 위한 Wallet 파일을 다운로드 하기 위해 `데이터베이스 접속` 버튼을 클릭합니다.

![oracle_free_tier](/assets/images/2024-02-27/07.png)

인스턴스 전자지갑을 다운로드 받습니다.

![oracle_free_tier](/assets/images/2024-02-27/08.png) | ![oracle_free_tier](/assets/images/2024-02-27/09.png)

## 오라클 클라우드 자율운영 DB 접속하기

### SQL Developer 다운로드 및 설치

SQL Developer는 오라클에서 제공하는 무료 DBMS 툴입니다. Mysql의 Workbench와 같은 역할을 합니다.

**[SQL Developer 다운로드](https://www.oracle.com/database/sqldeveloper/technologies/download/){:target="\_blank"}**에 접속하여 다운로드 받습니다.

SQL Developer는 Java로 작성되어 있기 때문에, 기본적으로 Java환경이 구성되어 있어야 합니다.

Java 환경이 구성되어 있지 않다면 JDK 11 included 버전을 다운로드 받아 설치하거나 별도로 설치를 해주세요.

### SQL Developer로 접속하기 (Wallet 접속 설정)

설치된 SQL Developer를 실행하면 아래와 같은 화면을 볼 수 있습니다. `+` 버튼을 클릭하여 새로운 접속을 추가합니다.

![oracle_free_tier](/assets/images/2024-02-27/10.png)

아래와 같은 화면에서 차례대로 정보를 입력합니다.

`Password`는 자율운영 데이터베이스 생성시 입력한 비밀번호를 입력합니다.

`Configureation File`에서 파일 경로는 전자지갑을 다운로드 받은 경로를 입력합니다. 압축은 따로 풀지 않아도 됩니다.

`test`를 클릭하여 접속이 잘 되는지 확인하고, `Connect`버튼을 클릭하여 접속합니다.

![oracle_free_tier](/assets/images/2024-02-27/11.png)

접속이 잘 되었다면 이제 SQL Developer를 통해 DB를 사용할 수 있습니다.

![oracle_free_tier](/assets/images/2024-02-27/12.png)
