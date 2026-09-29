# アクセスパターンとデータモデル

## テーブル

|テーブル名|PK|SK|
|:-----|:-----|:-----|
|users_table|user_id|-|
|visit_table|user_id|visit_id|

## User管理機能
### アクセスパターン
- sub を指定してユーザーを取得する
- sub とアカウント名を指定してユーザーを登録する
- sub を指定してユーザーを無効化する
- sub を指定してユーザーを有効化する

### データモデル
| 属性 | 型 | 必須 | 説明 |
|:----|:----|:----|:----|
| user_id | String | True | Cognito `sub`。Partition Key |
| account_name | String | True | ユーザーの表示名 |
| created_at | String | True | ISO 8601 / UTC（例: `2026-09-29T13:39:42.601272+00:00`） |
| updated_at | String | True | ISO 8601 / UTC（例: `2026-09-29T13:39:42.601272+00:00`） |
| status | String | True | `ENABLED` / `DISABLED` |

| user_id | account_name | created_at | updated_at | status |
|:----|:----|:----|:----|:----|
| ed9affb2-b079-4be9-9cdd-2f0c77f387ca | dummy-account | 2026-09-29T13:39:42.601272+00:00 | 2026-09-29T13:39:42.601272+00:00 | ENABLED |
| ac33600a-995a-4c2e-9906-dce875cef5c7 | dummy-account2 | 2026-09-29T13:39:42.601272+00:00 | 2026-09-29T13:39:42.601272+00:00 | DISABLED |

```json
{
  "user_id": "ed9affb2-b079-4be9-9cdd-2f0c77f387ca",
  "account_name": "dummy-account",
  "created_at": "2026-09-29T13:39:42.601272+00:00",
  "updated_at": "2026-09-29T13:39:42.601272+00:00",
  "status": "ENABLED"
}
```

## 訪問管理機能

### アクセスパターン
- ユーザーIDでVisit一覧を取得する。
- ユーザーIDとVisit情報で作成できる
- user_id, visit_idで削除できる

### データモデル

| 属性 | 型 | 必須 | 説明 |
|:----|:----|:----|:----|
| user_id | String | True | Cognito `sub`。Partition Key |
| visit_id | String | True | UUIDv7。Sort Key |
| prefecture_id | Number | True | 都道府県ID（1〜47） |
| created_at | String | True | ISO 8601 / UTC（例: `2026-09-29T13:39:42.601272+00:00`） |

| user_id | visit_id | prefecture_id | created_at |
|:----|:----|:----|:----|
| ed9affb2-b079-4be9-9cdd-2f0c77f387ca | 298f7a27-d375-43ff-bfae-5d087a7421eb | 1 | 2026-09-29T13:39:42.601272+00:00 |
| ac33600a-995a-4c2e-9906-dce875cef5c7 | 9cfa3f67-7bca-45a0-ac30-45936b5c0f49 | 2 | 2026-09-29T13:39:42.601272+00:00 |

```json
{
  "user_id": "ed9affb2-b079-4be9-9cdd-2f0c77f387ca",
  "visit_id": "298f7a27-d375-43ff-bfae-5d087a7421eb",
  "prefecture_id": 1,
  "created_at": "2026-09-29T13:39:42.601272+00:00"
}
```