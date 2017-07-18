## BoostOnPremise Pipeline

BoostOnPremiseのPipelineとして機能するスタックを作成することができます。

#### 構成

Git Repository、CI Runner、Docker Registry、Nextcloud、External DNS、証明書認証局、構成管理ツールなどが含まれます。

- Gitlab
  - Postfix
- Cert Register
  - Certificate Authority
- Registry Register
- Runner Register
- Service Register
  - Consul
- Gitlab CI Runner
- SeleniumHub
  - NodePhantomjs
- Nextcloud

#### 説明

##### Gitlab

GitlabサービスではPostfixをサイドキックとして、Git・Registry・Mattermostが利用可能です。

BoostOnPremiseを初期設定で起動した場合

`https://git.service.op`がGitlab本体

`https://registry.service.op`がGitlab Registry

`https://chat.service.op`がGitlab Mattermost

で利用できます。

##### Cert Register

Rancher Loadbalancerで利用可能な証明書を発行し、Rancher Serverに登録します。ドメインを追加して証明書を更新する場合は`authority`の`SSL_DNS`に追記し、`register-cert`の`CERT_NAME`を変更してアップグレードします。

自己証明書なので、ブラウザ等で警告を出さないためには、作成したルート証明書を信頼する証明書としてPCに登録する必要があります。

##### Registry Register

Gitlab RegistryのエンドポイントをRancher Serverに登録します。ここで設定した`Registry User`と`Registry User Secret`はGitlabのユーザーとして登録する必要があります。

##### Runner Register

`runner01`コンテナをGitlab CIのrunnerとして登録します。ただし、初回起動時はリンクされていないため、Gitlab起動後に`ci token`を取得し、`registry-runner`の`REGISTRATION_TOKEN`に追記し、アップグレードすることでアクティベートされます。

##### Service Register

`consul`をExternalDNSとして利用し、各ドメインを登録します。PC等から利用する場合は、該当ホストのIPをDNSに追加してください。ドメインを追加したい場合は、`register-service`の`SERVICES`に追記してアップグレードします。

##### Gitlab CI Runner

Gitlab CIのrunnerとして動作します。runnerを追加する場合は、`runner01`から名前とボリューム名を変更したクローンを作成し、`register-runner`の設定を変更してアップグレードします。

##### SeleniumHub

Gitlab CI Runnerからe2eテストを実行する際のSelenium Grid環境です。

BoostOnPremiseを初期設定で起動した場合

`https://selenium.service.op`でWebUIにアクセスできます。

##### Nextcloud

チームメンバーとコラボレーションする際に利用するファイル共有サービスです。初回アクセス時に管理アカウントや接続DBなどの設定を行います。

BoostOnPremiseを初期設定で起動した場合

`https://share.service.op`でアクセスできます。
