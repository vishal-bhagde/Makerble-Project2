Step - 1 (Required)
DOCKER
Build a Dockerfile for deploying a simple Ruby on Rails application with PostgreSQL DB  enabled. Application and DB should run on different containers.
Examples: Example – I (or) Example - II (or) Example - III (or) Example - IV
Note: You can use any ruby on rails examples or create a new simple rails app to satisfy the requirements


Step - 2 (Required)
KUBERNETES
Build a YAML file for the same application you’ve used in your first step to deploy it on Kubernetes. You can use any local cluster provider such as Minikube or K3d. The deployment of the standalone PostgreSQL pod must use Kubernetes StatefulSet. Additionally, the candidate may use any ingress controller they are comfortable with or a service mesh.
Useful Documentation - https://kubernetes.github.io/ingress-nginx/deploy/

book-manager
============

ISBNを元に蔵書の管理を行うWEBアプリです。

## Requirements

 - Apacheなど適当なhttpd(Proxy機能が必要)
 - Ruby
 - PostgreSQL with PGroonga

## Usage

### APサーバの準備

1. `ap`ディレクトリに`secret.rb`を作成して、以下の定数を定義します。

|定数|型|内容|要・不要|
|----|--|----|:-:|
|CACHE_DIR|string|書影画像([ISBN].jpg)を保存するディレクトリへの絶対パス|必須|
|RACK_SESSION_SECRET|string|Rackのession secret|必須|
|DB_HOST|string|database address|必須(不要な場合はnilを指定)|
|DB_NAME|string|database名|必須|
|DB_USER|string|DB用ユーザー名|必須|
|DB_PWD|string|DB用パスワード|必須(不要な場合はnilを指定)|
|RAKUTEN_APP_ID|integer|楽天APIのApplication ID|オプション|
|RAKUTEN_AFFILIATE_ID|string|楽天APIのAffiliate ID|オプション|

2. `ap`ディレクトリで以下のコマンドを実行します。

```
> bundle install
> bundle exec pumactl start
```

### WEBサーバの準備

1. Document rootとして`dist`ディレクトリを指定します。
2. Reverse proxy設定等で、`/api`以下へのアクセスを上記APサーバ(`http://localhost:9292`)へ転送するように設定します。
