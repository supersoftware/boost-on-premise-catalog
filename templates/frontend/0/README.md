## BoostOnPremise Frontend

BoostOnPremiseのFrontendとして機能するスタックを作成することができます。

#### 構成

静的ファイルの配信とオブジェクトストレージ

- Minio Server (管理用WebUI含む)
- Minio Client
- (SPAをNginx, Caddyなどで追加)

#### 説明

MinioはAWS S3の代替としてコンテナイメージには含めたくない、画像や動画の配置場所として利用できます。

BoostOnPremiseを初期設定で起動した場合、`https://assets.service.op`でMinioのWebUIにアクセス可能です。

MinioのWebUIではバケットに対するポリシーが設定できないため、付属している`mc`サービスのシェルからCLIで設定することができます。

##### CLI実行例

```
# mc mb minio/mybucket #=> バケットの作成
# touch test.txt #=> テストファイル
# mc cp test.txt minio/mybucket #=> テストファイルのアップロード
# mc policy public minio/awesome #=> バケットポリシーの変更

```

上記の場合、`https://assets.service.op/mybucket/test.txt`で直接アクセスすることができます。

また、自前のSPAへのアクセスは`gateway`スタックを経由することで認証・認可・スロットルなどのコントロールが可能です。

##### スタック間の関連

- (WebClient) -> routing -> gateway -> **frontend**
