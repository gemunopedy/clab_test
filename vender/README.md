# vender

Cisco / Juniper / Arista を接続したマルチベンダー検証ラボです。

## トポロジー

```text
R1 Cisco XR ---- R2 Cisco C8000V ---- R3 Cisco IOL ---- R4 Juniper ---- R5 Arista
 |                                                                    |
 +--------------------------------------------------------------------+
```

## ノード

| Node | Vendor / NOS | Kind | Management IPv4 | Loopback |
|---|---|---|---:|---:|
| R1 | Cisco IOS XR | `cisco_xrd` | `172.30.0.2` | `1.1.1.1/32` |
| R2 | Cisco IOS XE | `cisco_c8000v` | `172.30.0.3` | `2.2.2.2/32` |
| R3 | Cisco IOL | `cisco_iol` | `172.30.0.4` | `3.3.3.3/32` |
| R4 | Juniper Junos Evolved | `juniper_cjunosevolved` | `172.30.0.5` | `4.4.4.4/32` |
| R5 | Arista EOS | `arista_ceos` | `172.30.0.6` | `5.5.5.5/32` |

## リンク

| Link | Endpoint A | Endpoint B | Network |
|---|---|---|---|
| R1-R2 | R1 `Gi0/0/0/0` | R2 `GigabitEthernet2` | `192.168.12.0/24` |
| R2-R3 | R2 `GigabitEthernet3` | R3 `Ethernet0/1` | `192.168.23.0/24` |
| R3-R4 | R3 `Ethernet0/2` | R4 `et-0/0/0` | `192.168.34.0/24` |
| R4-R5 | R4 `et-0/0/1` | R5 `eth0` | `192.168.45.0/24` |
| R1-R5 | R1 `Gi0/0/0/1` | R5 `eth1` | `192.168.15.0/24` |

## 学習目標

- マルチベンダー環境の基本操作
- Cisco / Juniper / Arista の設定差分理解
- インターフェース状態確認
- 疎通確認
- 経路確認
- ベンダーごとの show コマンド比較

## 起動方法

```bash
sudo containerlab deploy -t vender.clab.yml
```

## 確認コマンド例

### Cisco IOS XR

```text
show ipv4 interface brief
show running-config
show route
```

### Cisco IOS XE / IOL

```text
show ip interface brief
show running-config
show ip route
```

### Juniper Junos

```text
show interfaces terse
show configuration
show route
```

### Arista EOS

```text
show ip interface brief
show running-config
show ip route
```

## 演習

### 演習1: 全ノードの管理IPを確認する

`containerlab inspect` を使って、各ノードの管理IPを確認してください。

### 演習2: 各リンクの状態を確認する

各ルータでインターフェース状態を確認し、リンクが up していることを確認してください。

### 演習3: ベンダーごとの設定差分を比較する

同じ目的の設定が Cisco / Juniper / Arista でどのように異なるか比較してください。

確認観点:

- hostname の設定方法
- Loopback の設定方法
- インターフェース IP アドレスの設定方法
- default route の設定方法

### 演習4: end-to-end 疎通確認

R1 から R5 まで疎通できるか確認してください。

### 演習5: 経路制御を追加する

Static route または OSPF / BGP を追加して、複数経路で通信できるようにしてください。
