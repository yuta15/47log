# Deployment

## 構成

```text
User
  |
  v
CloudFront
  |
  v
S3

User
  |
  +----> Cognito
  |        |
  |<--- JWT
  |
  v
API Gateway
  |
  v
Lambda
  |
  v
DynamoDB
```

## Components

| Service | Responsibility |
|---|---|
| CloudFront | フロントエンドの配信、キャッシュ、HTTPS通信の終端 |
| S3 | SPAのビルド成果物を保存する |
| Cognito | 外部認証を利用したユーザー認証とJWTの発行 |
| API Gateway | Backend APIの公開、ルーティング、JWTの検証 |
| Lambda | Backendのアプリケーション処理を実行する |
| DynamoDB | ユーザー情報および訪問記録を永続化する |

## Frontend

フロントエンドはSPAとしてビルドし、ビルド成果物をS3へ配置する。

ユーザーへの配信はCloudFront経由で行う。

## Backend

Backend APIはAPI Gatewayで公開し、リクエストをLambdaへルーティングする。

認証が必要なAPIについては、Cognitoが発行したJWTをAPI Gatewayで検証する。

LambdaからDynamoDBへアクセスし、ユーザー情報および訪問記録を永続化する。