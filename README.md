# docker-learn
Dockerについて勉強するためのリポジトリ

## Dockerってなんやねん。
- コンテナ型の仮想環境を作成、配布、実行するためのプラットフォーム。
- Linuxのコンテナ技術を使用したもぼ
- ホストマシンのカーネルを利用して、プロセスやユーザを隔離することによって、同時並行的に多くのマシンを動かしているように振舞わせることができる。
- ミドルウェアのインストールや各種環境設定をコード化して管理

### 運用による利点
- コード化されたファイルの共有による環境構築の円滑化
- 開発環境の配布が可能に
- スクラップ＆ビルドが容易にできる

### [環境構築](https://qiita.com/fsdg-adachi_h/items/2c6608a5ffc65ad0e5a7#%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8%E3%82%92%E3%83%93%E3%83%AB%E3%83%89)
1. [Rustのインストール](https://static.rust-lang.org/rustup/dist/x86_64-pc-windows-msvc/rustup-init.exe)
2. プロジェクトフォルダを作る：`mkdir <project-name> && cd ./<project-name>`
3. `Cargo.toml`を作成する

```toml
[package]
name = "ar"
version = "0.1.0"
edition = "2023"

[dependencies]
```

4. アプリケーションファイルを作成：`mkdir -p src && touch main.rs`
5. Option:アプリのビルド：`cargo clean && cargo build`
6. Dockerfileを作成する
```Dockerfile
# build the app.
FROM rust:1.71 AS build-env

# set the working dir.
WORKDIR /app

# copy the source and dependencies of the app.
COPY src ./src
COPY Cargo.toml Cargo.lock ./

# build the app.
RUN cargo build --release

# set up the container.
FROM debian:12-slim

# set the working dir.
WORKDIR /app

# copy the built app binary from the build-env.
COPY --from=build-env /app/target/release/app ./app

# set the environment variable.
ENV ROCKET_ADDRESS=0.0.0.0

# expose the port.
EXPOSE 8000

# command to run the app.
CMD ["./app"]
```
7. Option:Dockerデーモンの起動：`service docker start`
8. コンテナイメージのビルド
```bash
docker build \
    --no-cache \
    --tag app-hello-rocket:latest .

```
9. コンテナの起動
```bash
docker run --rm \
    --publish 8000:8000 \
    --name app-local \
    app-hello-rocket:latest

```
