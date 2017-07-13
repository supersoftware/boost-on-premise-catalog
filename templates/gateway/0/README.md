## BoostOnPremise Gateway

BoostOnPremiseのGatewayとして機能するスタックを作成することができます。

#### 構成

APIゲートウェイと管理用WebUI

- Kong
- Kong Dashboard (管理用WebUI)
- Postgres

#### 説明

KongはAPIGatewayとしてFrontendとBackendへのリクエストコントロールを行います。

BoostOnPremiseを初期設定で起動した場合、`https://apigw.service.op`でKongのWebUIにアクセス可能です。

KongはOpenID Connectの`OP`としては利用できないため、必要な場合は`coreos/dex`などを組み合わせる必要があります。

`oauth2 provider`としては利用可能です。

Kongのデータストアは`postgres`の他に`cassandra`も利用可能ですが、このテンプレートでは`postgres`を利用しています。

##### スタック間の関連

- (WebClient) -> routing -> **gateway** -> frontend
- (WebClient) -> routing -> **gateway** -> backend
