# ベンダー別コマンド比較

マルチベンダー環境では、同じ目的の操作でも NOS ごとにコマンドが異なります。  
このファイルでは、学習時によく使う確認コマンドを比較します。

## containerlab コマンド

| 目的 | コマンド |
|---|---|
| ラボ起動 | `sudo containerlab deploy -t <file>` |
| ラボ確認 | `sudo containerlab inspect` |
| ラボ削除 | `sudo containerlab destroy -t <file>` |
| 全ラボ削除 | `sudo containerlab destroy --all` |
| ノード一覧確認 | `docker ps --format "table {{.Names}}\t{{.Status}}"` |
| ノードへ入る | `docker exec -it <container-name> bash` |

## インターフェース確認

| 目的 | Cisco IOS XR | Cisco IOS XE / IOL | Juniper Junos | Arista EOS |
|---|---|---|---|---|
| IF 一覧 | `show ipv4 interface brief` | `show ip interface brief` | `show interfaces terse` | `show ip interface brief` |
| IPv6 IF 一覧 | `show ipv6 interface brief` | `show ipv6 interface brief` | `show interfaces terse` | `show ipv6 interface brief` |
| IF 詳細 | `show interfaces` | `show interfaces` | `show interfaces` | `show interfaces` |
| 設定確認 | `show running-config` | `show running-config` | `show configuration` | `show running-config` |
| 経路確認 | `show route` | `show ip route` | `show route` | `show ip route` |
| IPv6 経路確認 | `show route ipv6` | `show ipv6 route` | `show route table inet6.0` | `show ipv6 route` |
| 疎通確認 | `ping <ip>` | `ping <ip>` | `ping <ip>` | `ping <ip>` |
| 経路追跡 | `traceroute <ip>` | `traceroute <ip>` | `traceroute <ip>` | `traceroute <ip>` |

## 設定モードへの入り方

| NOS | コマンド |
|---|---|
| Cisco IOS XR | `configure` |
| Cisco IOS XE / IOL | `configure terminal` |
| Juniper Junos | `configure` |
| Arista EOS | `configure terminal` |

## 設定保存

| NOS | コマンド |
|---|---|
| Cisco IOS XR | `commit` |
| Cisco IOS XE / IOL | `write memory` または `copy running-config startup-config` |
| Juniper Junos | `commit` |
| Arista EOS | `write memory` または `copy running-config startup-config` |

## 学習ポイント

- Cisco IOS XR と Juniper は `commit` が必要です。
- IOS XE / IOL / EOS は `configure terminal` で設定モードに入る操作が似ています。
- Juniper は階層型設定、Cisco / Arista はコマンド列挙型の設定です。
- 同じ IP アドレス設定でも、NOS によってインターフェース名と構文が異なります。
