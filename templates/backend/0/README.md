## BoostOnPremise Backend

BoostOnPremiseのBackendとして機能するスタックを作成することができます。

#### 構成

Foxxアプリケーション(WebAPI)とデータベース

- ArangoDB agency x 3
- ArangoDB coordinator x 3 (管理用WebUI含む & Foxxアプリケーションをインストール)
- ArangoDB primary db x 3

#### 説明

別で起動する`routing`スタックの`internal`サービスが３台の`coordinator`にセレクタールールでロードバランスします。

BoostOnPremiseを初期設定で起動した場合、`https://db.service.op`でArangoDBのWebUIにアクセスできます。

ArangoDBはFoxxフレームワークで作成したAPIを、zipファイルやgitリポジトリなどから、サービスとして取り込むことができます。取り込んだAPIサービスは`coordinator`上で動作します。

APIへのアクセスは`gateway`スタックを経由することで認証・認可・スロットルなどのコントロールが可能です。

##### スタック間の関連

- (WebClient) -> routing -> gateway -> **backend**
