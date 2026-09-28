# Architecture Overview

## 1. Overview

Log47は、ユーザーが訪問した都道府県を記録し、
訪問済み・未訪問の都道府県を確認できるWebサービス。

## 2. System Context

User
  |
  v
Frontend
  |
  v
API
  |
  +----> Database
  |
  +----> External Identity Provider

## 3. Components

### Frontend
- ユーザーインターフェースを提供する
- 訪問済み・未訪問都道府県を表示する
- 外部認証を開始する
- APIを呼び出す

### API
- ユーザー情報を管理する
- 訪問記録を管理する
- 認証済みユーザーを識別する

### Database
以下のデータを永続化する。

- ユーザー
- 都道府県
- 訪問記録

### External Identity Provider
- ユーザー認証を提供する
- Log47では認証情報そのものを管理しない

## 4. Repository Structure

| Repository | Responsibility |
|---|---|
| `log47` | プロジェクト管理・ドキュメント |
| `log47-frontend` | Frontend |
| `log47-backend` | Backend API |
| `log47-infra` | Infrastructure |

## 5. Deployment Overview

Frontend / API / Database を本番環境に配置する。

詳細なインフラ構成は deployment.md を参照する。


## 6. Version管理

バージョンは全体バージョン、フロントエンドバージョン、バックエンドバージョン、インフラバージョンをそれぞれ管理する。
各コンポーネントのバージョンはリポジトリで管理し、全体バージョンは`log47`リポジトリで管理する。