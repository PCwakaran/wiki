# ACLを書く

　Access List (ACL)は主にネットワークにおけるパケットの通行ルールを指すことが多い（ように感じる）

### Juniper EXシリーズでACLを書く

今回記述するACLは下記の要素を持ちます

1. Webサーバ (17.0.80.1) の TCP 443アクセス
1. ADサーバ (192.168.53.1) への無制限アクセス
1. 17.0.0.0/8と一般的なローカルIPへのアクセス拒否
1. それ以外は許可

　ルールはVlan.100から入ってくるパケットに対して策定され、
Vlan.100のユーザが上記のルール内でしか行動できないように制限します。
また、このルールは`deny-intra-except-ad-and-www`と命名されます

　詳しく知りたい場合は、[Juniper公式ドキュメント](https://www.juniper.net/documentation/jp/ja/software/junos/routing-policy/topics/task/firewall-filter-ex-series-cli.html)を参照してください。

#### Webサーバへのアクセス許可

　ルールはtermという単位に分けられ、termの投入順に処理されていきます。
1つのterm内の条件はANDで計算され、`then`で一致するパケットの行方を設定します。

```junos
set firewall family inet filter deny-intra-except-ad-and-www term allow-to-www from destination-address 17.0.80.1/32
set firewall family inet filter deny-intra-except-ad-and-www term allow-to-www from protocol tcp
set firewall family inet filter deny-intra-except-ad-and-www term allow-to-www from destination-port 443
set firewall family inet filter deny-intra-except-ad-and-www term allow-to-www then accept
```

今回は、

- 宛先が`17.0.80.1`
- TCP
- 宛先ポート443

が明示的に許可されます。

#### ADへのアクセス許可

　ADのルール仕様ではポートなどが指定されていません。
そのため、ホストアドレスのみがルール条件となり、下記のコードが出来上がります。

```junos
set firewall family inet filter deny-intra-except-ad-and-www term allow-to-nw-ad from destination-address 192.168.53.1/32
set firewall family inet filter deny-intra-except-ad-and-www term allow-to-nw-ad then accept
```

#### ローカルへのアクセス拒否

　`destination-address`は複数指定でき、これらはOR演算されます。

```junos
set firewall family inet filter deny-intra-except-ad-and-www term deny-to-local-addr from destination-address 17.0.0.0/8
set firewall family inet filter deny-intra-except-ad-and-www term deny-to-local-addr from destination-address 172.16.0.0/12
set firewall family inet filter deny-intra-except-ad-and-www term deny-to-local-addr from destination-address 192.168.0.0/16
set firewall family inet filter deny-intra-except-ad-and-www term deny-to-local-addr from destination-address 100.64.0.0/10
set firewall family inet filter deny-intra-except-ad-and-www term deny-to-local-addr from destination-address 10.0.0.0/8
set firewall family inet filter deny-intra-except-ad-and-www term deny-to-local-addr then discard
```

#### インターネットへのアクセス許可

　ローカルアドレスへのアクセスを拒否しているため、
これは事実上インターネットレンジへのアクセス許可設定となります。
今回は対象ポートなどを設定せず、すべての通信を許可します。

```junos
set firewall family inet filter deny-intra-except-ad-and-www term allow-to-others then accept
```

#### インターネットにルールを設定する

　Vlan Unit 100の入力方向にファイアウォールルールを設定します。
入力方向とはスイッチのインタフェース（多くの場合はポートとみてよい）へ入ってくることを指し、
ユーザ視点ではなくスイッチ視点であることを注意してください。

```junos
set interfaces vlan unit 100 family inet filter input deny-intra-except-ad-and-www
```

## 執筆者一覧

- mkaraki
