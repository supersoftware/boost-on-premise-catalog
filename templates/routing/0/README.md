## BoostOnPremise Routing

BoostOnPremiseのRoutingとして機能するスタックを作成することができます。

#### 構成

ドメインベースのリクエスト振り分けとSSL終端

- internal (内部ロードバランサとして)
- external (外部ロードバランサとして)

#### 説明

このスタックでは`external`でドメインでのリクエスト振りわけとSSL終端を行い、`internal`でセレクタールールでのリクエスト振り分けを行います。

BoostOnPremiseを初期設定で起動した場合、以下のサービスが利用可能です。

- `http://git.service.op` #=> Pipeline(Gitlab HTTP)
- `https://git.service.op` #=> Pipeline(Gitlab HTTPS)
- `https://registry.service.op` #=> Pipeline(Gitlab Registry)
- `https://chat.service.op` #=> Pipeline(Gitlab Mattermost)
- `https://apigw.service.op` #=> Gateway(Kong Dashboard)
- `https://db.service.op` #=> Backend(ArangoDB WebUI)
- `https://assets.service.op` #=> Frontend(Minio)

##### スタック間の関連

- (WebClient) -> **routing** -> pipeline
- (WebClient) -> **routing** -> gateway
- (WebClient) -> **routing** -> backend
- (WebClient) -> **routing** -> frontend
