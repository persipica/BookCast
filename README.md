# 📚 BookCast

> 공공 도서 데이터를 활용한 도서 검색 및 도서관 서비스 플랫폼
> 公共図書データを活用した書籍検索・図書館サービスプラットフォーム

BookCast는 사용자가 다양한 도서 정보를 검색하고, 도서관의 소장 여부 및 대출 가능 여부를 확인하며, 희망도서 신청 등의 서비스를 이용할 수 있도록 개발한 웹 애플리케이션입니다.

프론트엔드와 백엔드뿐만 아니라 외부 공공 API 연동 및 AI 서버까지 연결하여 하나의 웹 서비스로 구현하는 것을 목표로 개발했습니다.

---

## 🇰🇷 한국어

### 📌 프로젝트 개요

기존 도서관 서비스에서는 도서 검색, 소장 여부 확인, 희망도서 신청 등의 기능이 각각 분리되어 있어 사용자가 필요한 정보를 여러 단계를 거쳐 확인해야 하는 불편함이 있습니다.

BookCast는 이러한 과정을 하나의 웹 서비스에서 처리할 수 있도록 설계한 도서관 서비스 플랫폼입니다.

사용자는 도서를 검색한 후 상세 정보를 확인하고, 해당 도서를 보유한 도서관 및 대출 가능 여부를 조회할 수 있습니다. 또한 도서관에 없는 도서는 희망도서로 신청할 수 있도록 구현했습니다.

관리자는 신청된 도서와 서비스 데이터를 확인하고 관리할 수 있도록 일반 사용자와 관리자 기능을 분리하여 개발했습니다.

---

## 🛠 Tech Stack

### Frontend

* React
* JavaScript
* Vite
* React Router
* Tailwind CSS
* Zustand
* Axios

### Backend

* Java
* Spring Boot
* Spring Data JPA
* Spring Security
* JWT
* MySQL

### AI / Data

* Python
* FastAPI

### External API

* 도서관정보나루 API 등 공공 도서 데이터 API

### Development Tools

* Git
* GitHub
* IntelliJ IDEA
* Visual Studio Code
* Postman

---

## 🏗 System Architecture

```text
                    ┌───────────────────┐
                    │       User        │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │   React + Vite    │
                    │     Frontend      │
                    └─────────┬─────────┘
                              │
                       REST API / JWT
                              │
                              ▼
                    ┌───────────────────┐
                    │   Spring Boot     │
                    │      Backend      │
                    └──────┬─────┬──────┘
                           │     │
                  ┌────────┘     └──────────┐
                  ▼                         ▼
          ┌───────────────┐         ┌───────────────┐
          │     MySQL     │         │ External APIs │
          │   Database    │         │  Public Data  │
          └───────────────┘         └───────────────┘
                  │
                  │
                  ▼
          ┌───────────────┐
          │    FastAPI    │
          │   AI Server   │
          └───────────────┘
```

---

## ✨ 주요 기능

### 🔐 1. 회원가입 및 로그인

* 일반 회원가입 및 로그인
* Spring Security 기반 인증 처리
* JWT 기반 로그인 상태 관리
* Zustand Persist를 이용한 사용자 정보 유지
* Axios Interceptor를 통한 인증 요청 처리
* 카카오 로그인 연동
* 사용자 권한(USER / ADMIN)에 따른 기능 분리

---

### 🔎 2. 통합 도서 검색

사용자가 다음 조건을 이용해 원하는 도서를 검색할 수 있습니다.

* 키워드
* 도서명
* 저자
* ISBN
* 출판사

React에서 검색 조건을 전달하고 Spring Boot에서 외부 도서 API를 호출한 후 필요한 데이터를 가공하여 프론트엔드로 전달하도록 구현했습니다.

```text
React
  ↓
Axios
  ↓
Spring Boot Controller
  ↓
Service
  ↓
External Book API
  ↓
Response DTO
  ↓
React
```

프론트엔드에서 외부 API를 직접 호출하지 않고 Spring Boot 서버를 중간 계층으로 사용함으로써 API 처리 로직을 백엔드에서 관리하도록 구성했습니다.

---

### 📖 3. 도서 상세 정보

검색 결과에서 원하는 도서를 선택하면 상세 페이지에서 다음 정보를 확인할 수 있습니다.

* 도서명
* 저자
* 출판사
* ISBN
* 도서 이미지
* 도서 관련 상세 정보
* 도서관 소장 여부
* 대출 가능 여부

일반 사용자와 관리자 페이지를 구분하여 역할에 따라 필요한 정보를 제공하도록 구성했습니다.

---

### 🏛 4. 도서관 소장 여부 및 대출 가능 여부 조회

외부 도서관 데이터를 활용하여 검색한 도서를 보유하고 있는 도서관 정보를 조회합니다.

사용자는 검색 과정에서 해당 도서의 소장 여부 및 대출 가능 여부를 함께 확인할 수 있습니다.

---

### 📩 5. 희망도서 신청

도서관에 원하는 도서가 없는 경우 사용자가 희망도서를 신청할 수 있도록 구현했습니다.

```text
사용자
 ↓
도서 검색
 ↓
희망도서 선택
 ↓
신청 정보 입력
 ↓
Spring Boot API
 ↓
MySQL 저장
 ↓
마이페이지에서 신청 상태 확인
```

사용자별 신청 내역을 저장하고 마이페이지에서 자신의 신청 정보를 확인할 수 있도록 구성했습니다.

---

### 🗳 6. 시민 투표

신청된 도서 등에 대해 사용자 의견을 반영할 수 있도록 투표 기능을 구현했습니다.

사용자가 서비스에 직접 참여할 수 있도록 함으로써 단순 도서 검색을 넘어 참여형 도서관 서비스를 목표로 했습니다.

---

### 👤 7. 마이페이지

로그인한 사용자가 자신의 정보를 관리하고 서비스 이용 기록을 확인할 수 있습니다.

* 회원 정보 확인
* 프로필 관리
* 희망도서 신청 내역 확인
* 사용자 관련 서비스 내역 확인

---

### 🛡 8. 관리자 기능

일반 사용자와 관리자의 역할을 분리하여 관리자 전용 기능을 제공합니다.

관리자는 서비스에서 발생하는 신청 및 도서 관련 데이터를 확인하고 관리할 수 있도록 구성했습니다.

---

## 👨‍💻 담당 역할

팀 프로젝트에서 주로 프론트엔드 개발과 백엔드 API 연동을 담당했습니다.

### Frontend

* React 프로젝트 구조 구성
* React Router 기반 페이지 라우팅
* 공통 Layout 및 Header 구성
* 로그인 / 회원가입 페이지 구현
* Zustand 기반 전역 사용자 상태 관리
* JWT 인증 연동
* 도서 검색 페이지 구현
* 도서 상세 페이지 구현
* 희망도서 신청 페이지 구현
* 마이페이지 구현
* 관리자 페이지와 일반 사용자 페이지 분기
* Axios를 이용한 Spring Boot REST API 연동

### Backend Integration

* Spring Boot API 구조 분석 및 프론트엔드 연동
* 외부 도서 검색 API 연동
* JWT 인증 요청 처리
* 사용자 정보 API 연동
* 희망도서 신청 API 연동
* 외부 API 응답 데이터 처리 및 오류 분석

### AI Server

* FastAPI 기반 Python 서버 연동
* React / Spring Boot와 AI 서버를 연결하는 구조 구성 및 테스트

---

# 🔧 개발 과정에서 해결한 문제

## 1. 외부 도서 API 호출 오류

### Problem

React에서 도서를 검색했을 때 Spring Boot 서버에서 다음과 같은 오류가 발생했습니다.

```text
500 Internal Server Error
```

단순히 프론트엔드 문제라고 판단하지 않고 전체 요청 흐름을 단계별로 확인했습니다.

```text
React
 ↓
ExternalBookController
 ↓
Data4LibraryService
 ↓
외부 도서 API
```

### Analysis

브라우저의 Axios 오류뿐만 아니라 Spring Boot 로그를 함께 확인하여 외부 API 요청 단계에서 `404 Not Found` 응답이 발생하고 있음을 확인했습니다.

이를 통해 화면이나 React 상태 관리 문제가 아니라 외부 API 요청 과정에서 발생하는 문제라는 것을 파악했습니다.

### What I Learned

오류가 발생한 위치만 수정하는 것이 아니라 클라이언트부터 서버, 외부 API까지 전체 데이터 흐름을 추적하여 문제의 원인을 확인하는 과정의 중요성을 배웠습니다.

---

## 2. JWT 인증 상태 관리

### Problem

로그인 이후 페이지가 변경되거나 새로고침했을 때 사용자 인증 정보를 안정적으로 유지할 필요가 있었습니다.

### Solution

Zustand의 Persist 기능을 이용하여 필요한 사용자 정보를 관리하고 Axios Interceptor를 활용해 인증이 필요한 API 요청에 JWT를 전달하도록 구성했습니다.

```text
Login
 ↓
JWT 발급
 ↓
Zustand Store
 ↓
Persist
 ↓
Axios Interceptor
 ↓
Authenticated API Request
```

이를 통해 인증 관련 코드를 각 페이지에 반복적으로 작성하는 것을 줄이고 인증 처리를 공통화했습니다.

---

## 3. 사용자 권한에 따른 UI 분리

일반 사용자와 관리자가 동일한 서비스를 사용하지만 접근해야 하는 기능이 다르기 때문에 사용자 권한에 따라 화면과 기능을 구분했습니다.

```text
USER
 ├─ 도서 검색
 ├─ 도서 상세
 ├─ 희망도서 신청
 └─ 마이페이지

ADMIN
 ├─ 도서 관리
 ├─ 신청 관리
 └─ 관리자 전용 페이지
```

이를 통해 인증(Authentication)뿐만 아니라 권한(Authorization)을 고려한 웹 서비스 구조를 경험했습니다.

---

# 📂 주요 프로젝트 구조

```text
BookCast
│
├── public/
│
├── src/
│   │
│   ├── api/
│   │   └── REST API 요청 관련 코드
│   │
│   ├── components/
│   │   └── 공통 UI Component
│   │
│   ├── layouts/
│   │   └── 공통 Layout
│   │
│   ├── pages/
│   │   ├── book/
│   │   ├── member/
│   │   ├── admin/
│   │   └── ...
│   │
│   ├── router/
│   │   └── React Router 설정
│   │
│   ├── store/
│   │   └── Zustand 상태 관리
│   │
│   └── ai-server/
│       ├── ai_server.py
│       └── requirements.txt
│
├── package.json
├── vite.config.js
└── README.md
```

---

# 🚀 실행 방법

## Frontend

```bash
npm install
npm run dev
```

기본 실행 주소:

```text
http://localhost:5173
```

---

## AI Server

가상환경 생성:

```bash
python -m venv venv
```

Windows:

```bash
venv\Scripts\activate
```

필요한 패키지 설치:

```bash
pip install -r requirements.txt
```

FastAPI 실행:

```bash
uvicorn ai_server:app --reload
```

---

## Backend

Spring Boot 서버를 실행한 후 Frontend와 연결합니다.

기본 개발 환경에서는 다음 포트를 사용했습니다.

```text
Frontend    : 5173
Spring Boot : 8080
FastAPI     : 8000
```

---

# 💡 프로젝트를 통해 배운 점

BookCast 프로젝트를 통해 단순히 하나의 화면을 구현하는 것을 넘어 실제 웹 서비스에서 프론트엔드, 백엔드, 데이터베이스 및 외부 API가 어떻게 연결되는지 경험할 수 있었습니다.

특히 다음과 같은 부분을 학습했습니다.

* React의 Component 기반 UI 설계
* REST API 기반 Frontend / Backend 통신
* Spring Security와 JWT를 이용한 인증 구조
* Zustand를 활용한 전역 상태 관리
* 외부 공공 API 연동
* 비동기 API 요청 및 예외 처리
* 사용자 권한에 따른 기능 분리
* Git을 이용한 팀 개발
* 오류 발생 시 요청 흐름을 단계별로 추적하는 디버깅 방법

프로젝트를 개발하면서 단순히 기능을 동작시키는 것뿐만 아니라 코드 구조와 데이터 흐름을 이해하고 문제의 원인을 직접 찾아 해결하는 것이 중요하다는 것을 배웠습니다.

---

# 🔮 향후 개선 사항

현재 구현된 기능을 기반으로 다음과 같은 개선을 진행할 수 있습니다.

* 외부 API 장애에 대한 예외 처리 강화
* API 응답 캐싱을 통한 검색 성능 개선
* 테스트 코드 추가
* 사용자 인증 및 권한 처리 강화
* 모바일 환경 UI 개선
* AI 기능 고도화
* 배포 환경 구축
* CI/CD 적용

---

<br>

---

# 🇯🇵 日本語

# 📚 BookCast

> 公共図書データを活用した書籍検索・図書館サービスプラットフォーム

BookCastは、ユーザーがさまざまな書籍を検索し、図書館での所蔵状況や貸出可否を確認したり、希望図書を申請したりできるWebアプリケーションです。

フロントエンドとバックエンドだけではなく、公共APIやAIサーバーを連携させ、一つのWebサービスとして構築することを目標に開発しました。

---

## 📌 プロジェクト概要

従来の図書館サービスでは、書籍検索、所蔵状況の確認、希望図書の申請などが別々に提供されることがあり、ユーザーが必要な情報を確認するまでに複数の操作が必要になるという課題があります。

BookCastでは、これらの機能を一つのWebサービス上で利用できるようにすることを目標としました。

ユーザーは書籍を検索した後、詳細情報、所蔵図書館、貸出可否などを確認できます。

また、図書館に所蔵されていない書籍については、希望図書として申請できる機能を実装しました。

一般ユーザーと管理者の機能を分け、それぞれの役割に応じた機能を利用できるよう設計しています。

---

# 🛠 使用技術

## Frontend

* React
* JavaScript
* Vite
* React Router
* Tailwind CSS
* Zustand
* Axios

## Backend

* Java
* Spring Boot
* Spring Data JPA
* Spring Security
* JWT
* MySQL

## AI / Data

* Python
* FastAPI

## External API

* 図書館情報ナール（도서관정보나루）API
* その他の公共書籍データAPI

## Development Tools

* Git
* GitHub
* IntelliJ IDEA
* Visual Studio Code
* Postman

---

# 🏗 システム構成

```text
                    ┌───────────────────┐
                    │       User        │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │   React + Vite    │
                    │     Frontend      │
                    └─────────┬─────────┘
                              │
                       REST API / JWT
                              │
                              ▼
                    ┌───────────────────┐
                    │   Spring Boot     │
                    │      Backend      │
                    └──────┬─────┬──────┘
                           │     │
                  ┌────────┘     └──────────┐
                  ▼                         ▼
          ┌───────────────┐         ┌───────────────┐
          │     MySQL     │         │ External APIs │
          │   Database    │         │  Public Data  │
          └───────────────┘         └───────────────┘
                  │
                  ▼
          ┌───────────────┐
          │    FastAPI    │
          │   AI Server   │
          └───────────────┘
```

---

# ✨ 主な機能

## 🔐 1. 会員登録・ログイン

* 一般会員登録・ログイン
* Spring Securityを利用した認証処理
* JWTを利用したログイン状態管理
* Zustand Persistによるユーザー情報管理
* Axios Interceptorによる認証リクエスト処理
* Kakao Login連携
* USER / ADMINの権限による機能分離

---

## 🔎 2. 書籍検索

以下の条件を利用して書籍を検索できます。

* キーワード
* 書籍名
* 著者
* ISBN
* 出版社

Reactから検索条件をSpring Bootへ送信し、Spring Bootから外部の書籍APIを呼び出します。

取得したデータをサービス内で利用しやすい形に処理した後、フロントエンドへ返す構成としました。

```text
React
  ↓
Axios
  ↓
Spring Boot Controller
  ↓
Service
  ↓
External Book API
  ↓
Response DTO
  ↓
React
```

フロントエンドから外部APIを直接呼び出すのではなく、Spring Bootを中間レイヤーとして利用することで、API関連の処理をバックエンド側で管理できるようにしました。

---

## 📖 3. 書籍詳細

検索結果から書籍を選択すると、詳細ページで以下の情報を確認できます。

* 書籍名
* 著者
* 出版社
* ISBN
* 書籍画像
* 書籍詳細情報
* 図書館での所蔵状況
* 貸出可否

一般ユーザーと管理者の画面を分け、それぞれに必要な情報を表示するよう構成しました。

---

## 🏛 4. 所蔵・貸出状況確認

外部の図書館データを利用し、検索した書籍を所蔵している図書館や貸出可否を確認できます。

書籍を検索してから別のサービスで図書館情報を検索する必要がないよう、一つのサービス内で確認できるようにしました。

---

## 📩 5. 希望図書申請

図書館に希望する書籍がない場合、その書籍を希望図書として申請できます。

```text
ユーザー
 ↓
書籍検索
 ↓
希望図書選択
 ↓
申請情報入力
 ↓
Spring Boot API
 ↓
MySQL
 ↓
マイページから確認
```

ユーザーごとに申請履歴を保存し、マイページから自分の申請状況を確認できるようにしました。

---

## 🗳 6. ユーザー投票

申請された書籍などに対して、ユーザーの意見を反映できる投票機能を実装しました。

単なる書籍検索サービスではなく、ユーザーが図書館サービスに参加できる仕組みを目指しました。

---

## 👤 7. マイページ

ログインユーザーが自身の情報やサービス利用状況を確認できます。

* 会員情報確認
* プロフィール管理
* 希望図書申請履歴
* ユーザー関連サービス情報

---

## 🛡 8. 管理者機能

USERとADMINの権限を分け、管理者専用機能を提供しています。

管理者はサービス上で発生した申請や書籍関連データを確認・管理できる構成としました。

---

# 👨‍💻 担当した内容

チームプロジェクトでは、主にフロントエンド開発とバックエンドAPIとの連携を担当しました。

## Frontend

* Reactプロジェクト構成
* React Routerによるルーティング
* 共通Layout / Headerの実装
* ログイン・会員登録画面
* Zustandによるグローバル状態管理
* JWT認証との連携
* 書籍検索画面
* 書籍詳細画面
* 希望図書申請画面
* マイページ
* USER / ADMINによる画面分岐
* AxiosによるREST API連携

## Backend Integration

* Spring Boot API構造の確認およびFrontendとの連携
* 外部書籍APIとの連携
* JWT認証リクエスト処理
* ユーザー情報APIとの連携
* 希望図書申請APIとの連携
* 外部APIのレスポンス処理・エラー分析

## AI Server

* Python / FastAPIサーバーとの連携
* React / Spring Boot / AI Server間の通信構成の確認・テスト

---

# 🔧 開発中に取り組んだ問題

## 1. 外部書籍APIのエラー調査

### Problem

書籍検索時にSpring Bootから以下のエラーが発生しました。

```text
500 Internal Server Error
```

フロントエンドだけを確認するのではなく、リクエスト全体の流れを確認しました。

```text
React
 ↓
ExternalBookController
 ↓
Data4LibraryService
 ↓
External Book API
```

### Analysis

ブラウザのAxiosエラーとSpring Bootのサーバーログを確認した結果、外部APIへのリクエスト段階で `404 Not Found` が発生していることを確認しました。

これによりReactの画面や状態管理ではなく、外部APIとの通信部分に問題があることを切り分けることができました。

### What I Learned

表示されているエラーだけを見るのではなく、クライアントからサーバー、さらに外部APIまで、データが流れる経路を順番に確認して原因を特定することの重要性を学びました。

---

## 2. JWT認証状態の管理

### Problem

ログイン後、画面遷移やブラウザ更新後も必要な認証情報を維持する必要がありました。

### Solution

Zustand Persistで必要なユーザー情報を管理し、Axios Interceptorを利用して認証が必要なAPIリクエストにJWTを付与する構成にしました。

```text
Login
 ↓
JWT
 ↓
Zustand Store
 ↓
Persist
 ↓
Axios Interceptor
 ↓
Authenticated API Request
```

これにより各画面で同じ認証処理を繰り返し記述することを減らし、認証処理を共通化しました。

---

## 3. ユーザー権限による機能分離

一般ユーザーと管理者では利用する機能が異なるため、ユーザー権限をもとに表示画面や利用可能な機能を分けました。

```text
USER
 ├─ 書籍検索
 ├─ 書籍詳細
 ├─ 希望図書申請
 └─ マイページ

ADMIN
 ├─ 書籍管理
 ├─ 申請管理
 └─ 管理者ページ
```

この実装を通して、AuthenticationだけでなくAuthorizationを考慮したWebサービス設計を経験しました。

---

# 📂 プロジェクト構成

```text
BookCast
│
├── public/
│
├── src/
│   │
│   ├── api/
│   │   └── REST API
│   │
│   ├── components/
│   │   └── Common Components
│   │
│   ├── layouts/
│   │   └── Common Layout
│   │
│   ├── pages/
│   │   ├── book/
│   │   ├── member/
│   │   ├── admin/
│   │   └── ...
│   │
│   ├── router/
│   │   └── React Router
│   │
│   ├── store/
│   │   └── Zustand Store
│   │
│   └── ai-server/
│       ├── ai_server.py
│       └── requirements.txt
│
├── package.json
├── vite.config.js
└── README.md
```

---

# 🚀 実行方法

## Frontend

```bash
npm install
npm run dev
```

```text
http://localhost:5173
```

---

## AI Server

仮想環境を作成します。

```bash
python -m venv venv
```

Windowsの場合：

```bash
venv\Scripts\activate
```

ライブラリをインストールします。

```bash
pip install -r requirements.txt
```

FastAPIを起動します。

```bash
uvicorn ai_server:app --reload
```

---

## Backend

Spring Bootサーバーを起動した後、FrontendからAPIへ接続します。

開発時には以下のポートを利用しました。

```text
Frontend    : 5173
Spring Boot : 8080
FastAPI     : 8000
```

---

# 💡 プロジェクトを通して学んだこと

BookCastの開発を通して、画面を実装するだけではなく、Frontend、Backend、Database、External APIがどのように連携して一つのWebサービスとして動作するのかを経験しました。

特に以下について学びました。

* ReactのComponentを利用したUI設計
* REST APIによるFrontend / Backend通信
* Spring Security / JWTによる認証
* Zustandによるグローバル状態管理
* 公共APIとの連携
* 非同期通信とエラー処理
* ユーザー権限による機能分離
* Gitを利用したチーム開発
* リクエストの流れを追跡したデバッグ

開発を通して、機能を動作させるだけではなく、コードやデータの流れを理解し、問題が発生した際に原因を切り分けて解決することが重要だと学びました。

---

# 🔮 今後の改善点

* 外部API障害時の例外処理の強化
* APIレスポンスのキャッシュによる検索性能改善
* テストコードの追加
* 認証・権限管理の強化
* モバイルUIの改善
* AI機能の改善
* 本番環境へのデプロイ
* CI/CDの導入

---

## 👤 Developer

**KANG HEE SU**

Web Developer

* Frontend: React / JavaScript / TypeScript
* Backend: Java / Spring Boot / FastAPI
* Database: MySQL / MongoDB
* GitHub: https://github.com/persipica
