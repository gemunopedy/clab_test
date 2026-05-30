# clab_test

containerlab を使ってネットワーク検証・学習を行うためのラボ集です。

このリポジトリは `gemunopedy/containerlab_study` をベースに、学習しやすいように README、演習、コマンド比較表を追加した構成です。

## 目的

このリポジトリでは、仮想ネットワーク機器を使って以下を学習します。

- containerlab の基本操作
- Cisco IOS XR / C8000V / IOL の基本設定
- Juniper Junos Evolved の基本設定
- Arista cEOS の基本設定
- マルチベンダー環境での疎通確認
- インターフェース設定、ルーティング、到達性確認

## ラボ一覧

| ラボ | 内容 |
|---|---|
| `mylab` | Cisco IOS XR 2台構成の基本ラボ |
| `vender` | Cisco / Juniper / Arista を接続したマルチベンダーラボ |

> Note: ディレクトリ名は元リポジトリに合わせて `vender` のままにしています。

## 必要環境

- Linux 環境
- Docker
- containerlab
- 各 NOS のコンテナイメージ

利用するイメージ例:

- `ios-xr/xrd-control-plane:latest`
- `xrd-control-plane:latest`
- `c8000v:latest`
- `cisco_iol:latest`
- `cjunosevolved:latest`
- `ceos:latest`

商用 NOS イメージは利用条件やライセンスを確認したうえで準備してください。

## 基本操作

### ラボ起動

```bash
cd mylab
sudo containerlab deploy -t mylab.clab.yml
```

または

```bash
cd vender
sudo containerlab deploy -t vender.clab.yml
```

### ラボ状態確認

```bash
sudo containerlab inspect
```

### ラボ削除

```bash
sudo containerlab destroy -t mylab.clab.yml
```

または

```bash
sudo containerlab destroy -t vender.clab.yml
```

## 学習の進め方

1. トポロジーファイルを読む
2. 各ルータの startup-config を確認する
3. ラボを起動する
4. 各ノードにログインする
5. インターフェース状態を確認する
6. ping / traceroute で疎通確認する
7. 設定を変更して挙動の違いを確認する

## ドキュメント

| ファイル | 内容 |
|---|---|
| [`mylab/README.md`](mylab/README.md) | Cisco IOS XR 2台ラボの学習ガイド |
| [`vender/README.md`](vender/README.md) | マルチベンダーラボの学習ガイド |
| [`docs/commands.md`](docs/commands.md) | ベンダー別コマンド比較 |
| [`docs/exercises.md`](docs/exercises.md) | 段階別の演習課題 |
