# tellus-market-sdk-gateway

Market SDK Gateway

## 処理内容

JWTのバリデーションを行い、認証に通れば、別のサーバにリバースプロキシする。

## 設定

config.ymlにて以下の項目を設定します

|                             | 意味                     | 例                                                   |
| --------------------------- | ----------------------- | --------------------------------------------------- |
| http.listen_address         | Listenするアドレス             | 127.0.0.1:8000                                      |
| http.tls.autocert.enabled   | 自動証明書発行を有効にするか      | true                               |
| http.tls.autocert.cache_dir | 証明書発行のキャッシュディレクトリ | /tmp/autocert                    |
| http.tls.certificate        | 証明書 | /opt/cert.pem    |
| http.tls.key                | 秘密鍵 | /opt/privkey.pem |
| upsteram.url                | 認証後に接続するサーバ             | https://www.example.com/         |
| upstream.headers            | プロキシ先に付与するリクエストヘッダ | {"Authorization": "Bearer token"} |
| private_key_url | JWTを検証する公開鍵をダウンロードするURL | https://sdk.tellusxdp.com/api/manager/v1/auth/public_keys |
| upstream          | 認証後に接続するサーバ             | https://www.example.com/                            |
| provider_id     | プロバイダ名                    | provider-a                                           |
| tool_id           | 商品ID                    | 1_9ffc0bb13148c605795b5bc22143b7b00c30ad            |
| api_key           | 集計用APIキー              | fa3a3293-d1be-41cf-9b6a-70d4d75c41ba             |
| tool_label        | 商品ラベル                 | product01                                           |
| allowed_auth_types | 許可認証方式                | ["password", "apikey"] |


### Example

```yaml
http:
  listen_address: 0.0.0.0:443
  tls:
    autocert:
      enabled: true
      cache_dir: /opt/market/autocert

upstream:
  url: http://www.example.com
  headers:
    Authorization: "Basic Zm9vOmJhcg=="

private_key_url: https://sdk.tellusxdp.com/api/manager/v1/auth/public_keys
counter_url: https://sdk.tellusxdp.com/api/manager/v1/items/counts
api_key: b424a335-ea26-4ff1-bdf8-168469778499

provider_id: acmeinc
tool_label: owesome-api
tool_id: 1_e849acf73765b19fd700af9374ab0fa2
allowed_auth_types:
  - apikey
  - password
```



## Getting started

```bash
mkdir -p ~/go/src/github.com/tellusxdp
cd ~/go/src/github.com/tellusxdp
git clone https://github.com/tellusxdp/tellus-market-sdk-gateway
cd tellus-market-sdk-gateway
vi config.yml
go run main.go
```

