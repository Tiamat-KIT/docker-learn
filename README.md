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

### 今回運用する構成(Windows)
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
5. Option:アプリのビルド:`cargo clean && cargo build`
