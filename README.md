## boost-on-premise-catalog
Rancher用プライベートカタログです。

<p align="center">
<img align=center src="https://cdn.rawgit.com/supersoftware/boost-on-premise-catalog/preview/logo.svg" width=50% />
</p>

フルスタックなWebアプリケーション開発&動作環境をプライベートネットワーク内で完結できるように調整しています。

以下５つのスタックで構成でされています。

- [backend](templates/backend/0/README.md)
- [frontend](templates/frontend/0/README.md)
- [gateway](templates/gateway/0/README.md)
- [pipeline](templates/pipeline/0/README.md)
- [routing](templates/routing/0/README.md)

#### ホストの事前設定

プライベートネットワーク内で完結できるようにするために、ホストの事前設定いくつか必要です。RancherOSをホストとして利用する場合の`cloud-config.yml`は以下になります。各自の環境に合わせて適宜変更してください。

[cloud-config.ymlのサンプル](https://gist.github.com/kyamazawa/435acdb0445fade900681d0ab68dc095#file-cloud-config-yml)

#### 設定内容について

##### Insecure Registry

Gitlab RegistryをHTTPSで利用しますが、証明書もカタログ起動後に内部で生成するため、あらかじめRegistryサービスのドメイン(`registry.service.op`)をInsecureRegistryとして登録しています。ドメインをデフォルトから変更する場合は、こちらも合わせて変更してください。

##### Network

DNSの役割を持つホストは、他のホストからnameserverとして参照するため、IPアドレスを固定しています。

##### DNS

ConsulをExternalDNSとして利用しています。
ホスト自身もそのDNSを利用するため、あらかじめ自IPをnameserverに登録しておきます。

##### SearchDomain

Gitlab CI Runnerがホストdocker経由で名前解決できるように、明示的に`git.service.op`と`registry.service.op`をサーチドメインに指定しています。

## boost-on-premise-docker

カタログで使用しているカスタムイメージのDockerfileは[コチラ](https://github.com/supersoftware/boost-on-premise-docker)です。
