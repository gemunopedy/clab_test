# 演習課題

このファイルでは、containerlab とネットワーク機器の基本操作を段階的に学習するための演習をまとめます。

## Level 1: containerlab の基本

### 1-1. ラボを起動する

`mylab` を起動してください。

```bash
cd mylab
sudo containerlab deploy -t mylab.clab.yml
```

確認項目:

- コンテナが作成されていること
- `containerlab inspect` でノードが表示されること

### 1-2. ラボを削除する

```bash
sudo containerlab destroy -t mylab.clab.yml
```

確認項目:

- 関連コンテナが削除されること
- 管理ネットワークが不要であれば削除されること

## Level 2: インターフェース確認

### 2-1. R1 / R2 の接続状態確認

`mylab` の R1 と R2 で、接続インターフェースが up していることを確認してください。

確認コマンド例:

```text
show ipv4 interface brief
show interfaces Gi0/0/0/0
```

### 2-2. 管理 IP を確認する

`containerlab inspect` の結果と、各ノードの設定ファイルに書かれている管理 IP が一致しているか確認してください。

## Level 3: 疎通確認

### 3-1. 隣接ルータへ ping

`mylab` で以下を確認してください。

- R1 から `192.168.12.2` へ ping
- R2 から `192.168.12.1` へ ping

### 3-2. マルチベンダー環境の隣接 ping

`vender` で以下の隣接区間の疎通を確認してください。

- R1-R2
- R2-R3
- R3-R4
- R4-R5
- R1-R5

## Level 4: 設定比較

### 4-1. Loopback 設定を比較する

`vender/configs` 配下の設定を読み、Loopback0 の設定方法を比較してください。

確認観点:

- Cisco IOS XR
- Cisco IOS XE
- Cisco IOL
- Juniper Junos
- Arista EOS

### 4-2. default route を比較する

各 NOS で default route の設定構文がどう違うか確認してください。

## Level 5: Static Route

### 5-1. R1 から R3 Loopback へ到達させる

`vender` で R1 から R3 の Loopback `3.3.3.3/32` に到達できるように static route を追加してください。

考えること:

- R1 側に必要な経路
- R3 側の戻り経路
- 中継する R2 の経路

### 5-2. R1 から R5 Loopback へ到達させる

R1-R5 の直接リンク、または R1-R2-R3-R4-R5 の経路を使って疎通できるようにしてください。

## Level 6: OSPF / BGP 発展課題

### 6-1. OSPF を設定する

マルチベンダーで OSPF を設定し、Loopback アドレスを広報してください。

確認項目:

- neighbor が確立すること
- 経路表に OSPF 経路が載ること
- Loopback 間で ping できること

### 6-2. BGP を設定する

R1-R5 間で BGP を構成し、Loopback を広報してください。

確認項目:

- BGP neighbor が Established になること
- BGP 経路が経路表に反映されること

## Level 7: 障害対応シナリオ

### 7-1. インターフェース shutdown 障害

任意のリンクを shutdown し、どのコマンドで障害を発見できるか確認してください。

### 7-2. IP アドレス誤設定

片側のインターフェース IP を別サブネットに変更し、ping が失敗する原因を調査してください。

### 7-3. 経路不足

static route を一部削除し、往路・復路のどちらに問題があるか確認してください。

## レポート作成テンプレート

演習ごとに以下の形式でメモを残すと、学習記録として役立ちます。

```markdown
## 演習名

### 実施内容

### 使ったコマンド

### 結果

### わかったこと

### 次に試したいこと
```
