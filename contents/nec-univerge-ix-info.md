# NEC IX 関連の情報集 兼 チートシート

編集中のページです。ご注意ください  
また、予告なしに削除、あるいは編集される場合があります

## コマンドリファレンスリンク

[コマンドリファレンスマニュアル🔗](https://www.support.nec.co.jp/View.aspx?id=3170102594)

## 絶対覚えておくべき操作

### コンフィグに入る

- `enable-config` 省略形：`en`
- `configure terminal` 省略形：`con t` (Cisco IOS風の記述)

```
Router# enable-config
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)# 
```

### コンフィグから抜ける

- `exit`
- ショートカット：[Ctrl] + [Z] (むやみに使うのは推奨しない)

```
Router(config)# exit
Router#
```

### ルータの名前の変更

- 付けたい名前：`IX2215`

```
Router(config)# hostname IX2215
IX2215(config)#
```

この名前は SSH 等でコンソールに入ったときや、Web コンソールにアクセスした際に表示されます

### admin ユーザーとパスワードの追加

- ユーザー名：`myname`
- パスワード：`mypassword`

```
Router(config)# username myname password plain 1 mypassword administrator
```

### コンフィグの保存

- `write memory` 省略形： `wr m`

```
Router(config)# write memory
Building configuration...
% Warning: do NOT enter CNTL/Z while saving to avoid config corruption.
Router(config)#
```

### 各種ログインを有効化する

#### SSH
```
Router(config)# ssh-server ip enable
```

#### Telnet

```
Router(config)# telnet-server ip enable
```

#### Web UI

```
Router(config)# http-server ip enable
```

## IX をこれから買おうとしている人向けの情報

誤家庭を志し、自宅に IX シリーズをお迎えしようとしている人に向けて、弊サーバのメンバ有志が集めた情報を集約します。どなたかの参考になれば幸いです  
特記ない場合、例として、広く出回っている IX2215 を指すものとします

### IX シリーズの購入

一時期、一台あたり 2千円程度と言わば価格崩壊のような状態になっていました。本稿執筆時点でのオークション相場はおよそ ¥5,000/台 程度で、これでも十分安いため、購入しようと思っている人もいらっしゃると思います。その際、どのようなものを買うべきか、ここに残しておきます

オススメはファームウェアバージョンが 10.x 以降と明記されている IX2215 です。IX2105 も少々出回っていますが、筐体サイズが小さい分スペックも控えめなため、ガッツリネットワークを構築したい人にはあまり向かないと思われます

### コンソールケーブル

機器のスーパーリセットや初期設定等を行うために必要となります。USB Type-A to RJ45 のものがオススメです。使えそうなものの Amazon リンクを以下に貼っておきます

<https://www.amazon.co.jp/dp/B0769J9QXP>  
<https://www.amazon.co.jp/dp/B01F05XLDM>  
<https://www.amazon.co.jp/dp/B00JPFOTOY>

※少なくとも最後のものに関しては、FTDI チップ採用を謳っていますが私（はるさめ）が購入したものは WCH チップ（CH340）採用のモノでした。ロットによって差はあるとは思いますが、値段を考えても FTDI チップを採用しているとは思えないため、そのことを予め念頭に置いた上で、購入を検討してください。ドライバをインストールする必要はありますが、使えはします

参考：<https://twitter.com/HarusameTech/status/1614607100231155712>

### ファームウェア

Ver.10.x 以降であれば、NetMeister 経由でアップデートが可能なため、なるべく 10.x 以降と明記されているものを選びましょう。8.x のようなものを買ってしまうと、何かしらの方法でファームウェアを入手する必要があります。（法人格を持っている場合は気にしなくて良いかもしれません）

### コマンド操作

本稿前章を参考に、まずはぶっ壊してもいい環境で練習するといいと思います。困ったときは、自分で調べたり、弊サーバ内の質問フォーラムを活用するなりしましょう  
運のいいことに、弊サーバには若干名、コマンド操作や IX の扱いに慣れている方が存在するため、色々教えてくれるかもしれません  
熟知こそしていなくても、カバー範囲の人は結構いるため、自力で解決できなかったらためらわず質問しましょう！

### 最後に

おそらく、コレより優れている備忘録はもっとたくさんあると思いますが、我こそはという方は、サーバ内フォーラムの活用や、自分のブログで書いてみるのも良いかも知れません

___

※随時加筆・修正します

## 執筆者一覧
- はるさめ [@HarusameTech](https://twitter.com/HarusameTech)
- mkaraki