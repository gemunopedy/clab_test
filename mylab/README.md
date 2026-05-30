# mylab

Cisco IOS XR 2台を接続した基本ラボです。

## トポロジー

```text
R1 Gi0-0-0-0 ---- Gi0-0-0-0 R2
```

## ノード

| Node | Kind | Management IPv4 | Management IPv6 | Loopback |
|---|---|---:|---:|---:|
| R1 | `cisco_xrd` | `172.30.0.2` | `2001:172:30::2` | `1.1.1.1/32` |
| R2 | `cisco_xrd` | `172.30.0.3` | `2001:172:30::3` | `2.2.2.2/32` |

## リンク

| Link | Endpoint A | Endpoint B | Network |
|---|---|---|---|
| R1-R2 | R1 `Gi0/0/0/0` | R2 `Gi0/0/0/0` | `192.168.12.0/24` |

## 学習目標

このラボでは以下を学習します。

- containerlab の基本的な起動方法
- Cisco IOS XR の基本操作
- startup-config の読み方
- インターフェース状態確認
- ルータ間の疎通確認

## 起動方法

```bash
sudo containerlab deploy -t mylab.clab.yml
```

## ノード確認

```bash
sudo containerlab inspect
```

## ログイン例

```bash
docker exec -it clab-mylab-R1 bash
docker exec -it clab-mylab-R2 bash
```

## 確認コマンド

IOS XR 上で以下を確認します。

```text
show ipv4 interface brief
show ipv6 interface brief
show running-config
show route
ping 192.168.12.2
```

R2 では以下を実行します。

```text
ping 192.168.12.1
```

## 演習

### 演習1: インターフェース状態を確認する

R1 と R2 の接続インターフェースが up していることを確認してください。

### 演習2: 対向ルータへ ping する

R1 から R2、R2 から R1 へ ping を実行してください。

### 演習3: 設定を読む

`configs/R1.cfg` と `configs/R2.cfg` を読み、以下を確認してください。

- hostname
- 管理インターフェース
- データプレーン用インターフェース
- Loopback0
- default route

### 演習4: description を追加する

R1 / R2 の接続インターフェースに description を追加し、running-config に反映されることを確認してください。
