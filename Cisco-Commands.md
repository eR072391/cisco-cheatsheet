[引用](https://www.rental-network.jp/tips/cisco_command/)  

# Ciscoルータコマンド  

| コマンド | 説明 |
| --- | --- |
| enable | 特権モードへ移動する |
| enable password | イネーブルパスワードを設定する |
| enable secret | イネーブルパスワードを暗号化する |
| show running-config | コンフィグを表示 |
| copy running-config startup-config | 現在の設定を保存する |
| show ip route | ルーティングテーブルを表示 |
| show clock | 時刻を表示 |
| show version | ルータのいろいろな情報を表示 |
| show logging | ルータが認識したイベントを表示 |
| show arp | ARP cache（アープキャッシュ）の表示 |
| dir flash | flashメモリ情報を表示 |
| show environment | ルータの置かれた環境を表示 |
| show processes cpu | 各プロセスのcpu使用率を表示 |
| show processes memory | 各プロセスのメモリを表示 |
| show tech support | ルータのシステム情報を表示 |
| show diagnostic status | モジュール情報を表示 |
| show cdp neighbors | CDPを利用して隣接ルータの情報を表示 |
| show interface | インターフェイスの状態を表示 |
| show ip interface brief | インターフェイスの状態をシンプルに表示 |
| show history | 過去に使ったコマンドを表示 |
| no shutdown | インターフェイスを立ち上げる |
| configure terminal | グローバルコンフィグレーションモードへ移動する |
| terminal length 0 | 表示する行の長さを決定する |
| do ~ | 下位モードのコマンドを使える |
| line vty 0 4 + password ~ | line vtyにパスワードを設定する |
| transport input ssh | ssh接続設定 |
| logging x.x.x.x | ログサーバを指定 |
| logging buffered 512000 debugging | ログをバッファに入れるようにする |
| ping x.x.x.x | x.x.x.x宛ての疎通確認をする |
| ping | 拡張ping。疎通確認をする |
| traceroute x.x.x.x | 通信経路の確認 |
| reload | ルータを再起動する |
| clock timezone JST 9 | タイムゾーンを日本時間にする |
| ip nat inside source static | 静的NATの設定 |
| ip nat inside source list 1 pook ~ | 動的NATの設定 |
| access-list ~ deny x.x.x.x | アクセスリストを定義する |
| ip access-group ~ in | アクセスリストをインターフェイスに適用する |
| ip route 0.0.0.0 0.0.0.0 x.x.x.x(interface) | デフォルトルーティングを指定する |
| router rip | リップを設定する |
| version 2 | リップバージョン2を設定する |
| router eigrp [1~65535] | EIGRPを設定する |
| no auto-summary | 自動集約を無効にする |
| passive-interface ~ | インターフェイスをパッシブにする |
| router ospf [1~65535] | OSPFを設定する |
| log-adjacency-changes | OSPFルータの隣接関係のログが出るようにする |
| redistribute ~ | 再配信の設定 |
| encapsulation frame-relay | インターフェイスをフレームリレーでカプセルする |
| clear ip route * | ルーティングテーブルをクリア |
| no cdp run | CDPを無効にする |
| encapsulation ppp | インターフェイスをpppでカプセル化する |
| ppp authentication chap | pppで暗号化の認証をさせる |
| banner motd | バナーの設定 |
| speed [10/100/1000/auto] | インターフェイスの速度を変更する |
| duplex [full/half/auto] | インターフェイスのduplexを変更する |
| aaa new-model | 認証機能を設定する |
| no ip domain-lookup | ドメイン名から名前解決サービスを止める |
| isdn switch-type ntt | スイッチタイプをnttに設定する |
| ntp server x.x.x.x | NTPサーバのアドレスを指定する |
| service compress-config | コンフィグを圧縮する |
| ip tcp header-compression | TCPヘッダー圧縮をする |
| clock set ~ | 日時を設定する |
| copy flash tftp | flashメモリからtftpサーバへコピーする |
| copy tftp flash | tftpサーバからflashメモリへコピーする |



[引用2](https://qiita.com/k-yasuhiro/items/aede8bf0ce31665cc18e)


# 基本設定コマンド

## 特権EXECモードに移行  
特権EXECモードは、機器のステータスを制限なしに確認出来るモード。  
ユーザEXECモードで enableコマンドを実行する。  
```
Router> enable
Router#
```
プロンプトが「>」となっているのはユーザEXECモード  
「#」となっているのは特権EXECモード  


## グローバルコンフィグレーションモードに移行  
グローバルコンフィグレーションモードは、機器全般に関わる設定を行うモード。  
グローバルコンフィグレーションモードに移行するには configure terminal コマンド。  
```
Router# configure terminal
Router(config)#
```
プロンプトが「(config)」となっていたら、グローバルコンフィグレーションモード。  

## ホスト名の設定
グローバルコンフィグレーションモードで hostnameコマンド
```
Router(config)# hostname <ホスト名>
```

## イネーブルパスワードの設定
ユーザEXECモードから特権EXECモードに移行する際に設定するパスワード。  
コンフィグレーションモードで enable passwordコマンド。  
```
(config)# enable password <パスワード>
```

## コンソールパスワードの設定
グローバルコンフィグレーションモードで line console 0コマンド。  
```
(config)# line console 0
(config-line)#
```
プロンプトが「（config-line)#」となっていたら、ラインコンフィグレーションモード。  
次に、パスワードを設定する passwordコマンド。  
```
(config-line)# password <パスワード>
```
認証を有効化。  
```
(config-line)# login
```

## VTYパスワードの設定
ラインコンフィグレーションモードで行う。  
```
(config)# line vty <開始ライン番号> [<終了ライン番号>]
```
<終了ライン番号>を省略すると、開始ライン番号で指定したVTYポートのみに設定を行う。  
次にパスワードを設定する。  
```
(config-line)# password <パスワード>
```
認証を有効化
```
(config-line)# login
```

## ローカル認証の設定
パスワードだけでなく、ユーザー名も必要な設定方法。  
ユーザーアカウントの作成。  
グローバルコンフィグレーションモードで usernameコマンドを実行。  
```
(config)# username <ユーザー名> [privilege <特権レベル>] password <パスワード>
```
<特権レベル>には、ユーザーの特権レベルを指定。  
0 ~ 15が指定でき、設定されたレベル以下のコマンドしか実行出来ない。  

ラインコンフィグレーションモードに移行する。  
```
// コンソール接続の場合
(config)# line console 0
// VTY接続の場合
(config)# line vty <開始ライン番号> [<終了ライン番号>]
```
認証を有効化。  
ラインコンフィグレーションモードで login localコマンド  
```
(config-line)# login local
```

## 設定ファイルの保存
設定を保存したい場合には、特権EXECモードで copyコマンド  
```
# copy <コピー元> <コピー先>
```
running-configを startup-configにコピーする場合によく使用される。  

## ルータの初期化
NVRAM上の startup-configを消去する startup-configを消去するには、  
特権モードで erase startup-configコマンド。  
```
# erase startup-config
```
再起動する。  
```
# reload
```

# ルータの設定

## IPアドレスの設定
インターフェイスコンフィグレーションモードに移行。  
そして、グローバルコンフィグレーションモードで interfaceコマンド。  
```
(config)# interface <タイプ> <ポート番号>
```
```
(config)# interface fastEthernet 0/0
(config-if)#
```
プロンプトが「(config-if)#」となっていたら、インターフェイスコンフィグレーションモード。  
<タイプ>には、機器のインターフェイスによって下記のいずれかを指定。  
[ Ethernet、fastEthernet、Gigabit Ethernet、Loopback ]  
<ポート番号>には、インターフェイスの番号を指定。  
番号は、0や1といった数字を指定するものや、「0/0」といった「スロット番号/インターフェイス番号」  
という形で指定するものがある。  

IPアドレスを設定。  
インターフェイスコンフィグレーションモードで ip addressコマンドを実行  
```
(config-if)# ip address <IPアドレス> <サブネットマスク>
```
インターフェイスを有効にする。  
インターフェイスコンフィグレーションモードで no shutdownコマンドを実行。  
```
(config-if)# no shutdown
```

## シリアルインターフェイスの設定
2台のルータをシリアルケーブルで直接つないだ場合、DCEコネクトが接続された方にクロックレートの設定を行う必要がある。  

DCEコネクトを確認する。直接ケーブルから確認出来ない場合は、特権EXECモードで次の show controllers serialコマンド。  
```
# show controllers serial <番号>
```
<番号>は、インターフェイス番号を指定  

クロックレートの設定。  
クロックレートの設定をするには、インターフェイスコンフィグレーションモードで次の clock rate <クロックレート値>  
```
(config-if)# clock rate <クロックレート値>
```
<クロックレート値>の単位は、bpsとなります。  


## インターフェイスの通信モードと通信速度の設定
通信モードのオートネゴシエーション機能の有効・無効を設定するには、  
インターフェイスコンフィグレーションモードで次の duplexコマンド。  
```
(config-if)# duplex <auto|full|half>
```
\<auto\>は、オートネゴシエーション機能が有効になる。  
\<full\>は、オートネゴシエーション機能が無効になり、全二重の通信モードになる。  
\<half\>は、オートネゴシエーション機能が無効になり、半二重の通信モードになる。  

通信速度のオートネゴシエーション機能の有効・無効を設定するには、  
インターフェイスコンフィグレーションモードで次の speedコマンド  
```
(config-if)# speed <10|100|1000|auto>
```

# パスワードの暗号化設定

## イネーブルパスワードの暗号化
イネーブルパスワードの暗号化するには、  
グローバルコンフィグレーションモードで enable secretコマンド  
```
(config)# enable secret <パスワード>
```
enable secretコマンドと enable passwordコマンド両方でパスワード設定した場合、  
enable secretコマンドで設定したパスワードが優先される。  

## 異なるアルゴリズムを用いたイネーブルパスワードの暗号化
異なるアルゴリズムを用いたイネーブルパスワードの暗号化をするには、  
グローバルコンフィグレーションモードで enable algorithm-typeコマンド。  
```
(config)# enable algorithm-type <md5|scrypt|sha256> secret <パスワード>
```

## ローカル認証を使用するユーザアカウントパスワードの暗号化
ローカル認証を使用するユーザアカウントパスワードの暗号化をするには、  
グローバルコンフィグレーションモードで usernameコマンド  
```
(config)# username <ユーザ名> [<privilege <特権レベル>] algorithm-type <md5|scrypt|sha256> secret <パスワード>
```

## パスワード全般の暗号化
パスワード全般の暗号化は、グローバルコンフィグレーションモードで、  
service password-encryptionコマンド  
```
(config)# service password-encryption
```
コマンドで設定済みのパスワードだけでなく、今後設定するパスワードも暗号化されて保存されます。  
ただし、イネーブルパスワードは、enable secretコマンドを実行した方が暗号化の強度が強い。  
また、次のコマンドを実行すると暗号化が無効になり、  
以降設定されるパスワードは暗号化されない。  
```
(config)#no service password-encryption
```
既に暗号化されて保存されたパスワードは元には戻らない。  


## SSHの設定
①ホスト名を設定する。  
ホスト名の設定は、グローバルコンフィグレーションモードで hostnameコマンド  
```
Router(config)# hostname <ホスト名>
```
デフォルトのホスト名であるRouterは、この後で行うRSA暗号鍵を生成することが出来ない。  
なのであらかじめ変更しておく必要がある。  

②ドメイン名を設定する  
ドメイン名を設定するには、グローバルコンフィグレーションモードで、  
次の ip domain-nameコマンドを実行する。  
```
(config)# ip domain-name <ドメイン名>
```

③RSA暗号鍵を生成する  
SSHで使用するRSA暗号鍵を設定するには、グローバルコンフィグレーションモードで、  
次の crypto key generate rsa コマンド  
```
(config)# crypto key generate rsa
```
ホスト名がデフォルトのままだと、実行できない。  

④ユーザーアカウントを作成する  
ユーザーアカウントを作成するには、グローバルコンフィグレーションモードで、  
次の usernameコマンド  
```
(config)# username <ユーザー名> [privilege <特権レベル>] password <パスワード>
```

⑤ローカル認証を設定する  
作成したユーザーアカウントを使用してログインの認証をするには、login localコマンド  
```
//コンソール接続の場合
(config)# line console 0
//VTY接続の場合
(config)# line vty <開始ライン番号> [<終了ライン番号>]

(config-line)# login local
```
SSH接続では、VTYパスワードを用いた方法ではログイン出来ない為、ローカル認証を用いる必要がある。  

⑥SSHの接続許可を設定する  
SSHの接続許可を設定するには、ラインコンフィグレーションモードで、  
次の transport inputコマンド  
```
(config-line)# transport input < ssh|telnet|all|none >
```

⑦SSHのバージョンを設定する  
SSHのバージョンを設定するには、グローバルコンフィグレーションモードで、  
次の ip ssh versionコマンド  
```
(config)# ip ssh version < 1|2 >
```

## スタティックルーティング設定

スタティックルーティングの設定をするには、
グローバルコンフィグレーションモードで、次の ip routeコマンド
```
(config)# ip route <宛先ネットワーク> <サブネットマスク> <ネクストホップ|出力インターフェイス> [<アドミニストレーティブでぃいスタンス値>]
```

## デフォルトルートの設定  
デフォルトルートの設定をするには、  
グローバルコンフィグレーションモードで、次の ip routeコマンド  
```
(config)# ip route 0.0.0.0 0.0.0.0 <ネクストホップ|出力インターフェイス> [<アドミニストレーティブディスタンス値>]
```
デフォルトルートの設定は、スタティックルート追加の際に宛先ネットワークとサブネットマスクを、  
全て0にする。  


## OSPF設定コマンド  
ダイナミックルーティングを行うには、ルータでOSPFを有効化する必要がある  

①OSPFの有効化  
OSPFを有効化するには、グローバルコンフィグレーションモードで router ospf コマンドを実行  
```
(config)# router ospf <プロセスID>
(config-router)#
```
<プロセスID>は、1~65535の値を指定可能  
このコマンドを実行するとプロンプトが、ルータコンフィグレーションモードに移行して、  
プロンプトが(config-router)#に変更される。  

②インターフェイスの指定  
次にOSPFを有効にするインターフェイスを指定  
インターフェイスでOSPFを有効にするには、ルータコンフィグレーションモードで  
networkコマンドを実行。  
```
(config-router)# network <IPアドレス> <ワイルドカードマスク> area <エリアID>
```
<エリアID>には、有効にするインターフェイスが所属するエリア番号を指定  
または、インターフェイスコンフィグレーションモードで ip ospf areaコマンドを実行  
```
(config-if)# ip ospf <プロセスID> area <エリアID>
```
<プロセスID>は、どのプロセスを動作させるかを指定  
<エリアID>には、有効にするインターフェイスが所属するエリア番号を指定  


## パッシブインターフェイスの指定
パッシブインターフェイスの設定をするには、ルータコンフィグレーションモードで、  
passive-interfaceコマンドを実行  
```
(config-router)# passive-interface <インターフェイス>
```
指定されたインターフェイスから、Helloパケットが送信されなくなる。  


## ルータIDの指定
IPアドレスが設定されていれば、ルータIDを設定しなくても問題ないが、  
手動で設定がしたい場合は、ルータコンフィグレーションモードで、router-idコマンドを実行  
```
(config-router)# router-id <ルータID> 
```
ルータIDには、32ビットの値をIPアドレスと同じ形式で指定。  
手動で設定していない場合は、ループバックインターフェイス、物理インターフェイスの順で、  
最も大きい値のIPアドレスからルータIDが設定される。  
ループバックインターフェイスとは、管理者が任意で作成する事が出来る仮想的な  
インターフェイスの事で、ループバックインターフェイスを作成するには、  
グローバルコンフィグレーションモードで、interface Loopbackコマンドを実行。  
```
(config)# interface Loopback <番号>
```
番号には、0 ~ 2,147,483,647の値を指定  


## ルータIDの再設定
ルータIDを設定した後に、再度設定変更するには、  
router-idコマンドで再設定した後、再起動する必要があります。  
再起動のコマンドは、特権EXECモードで clear ip ocpf processコマンド  
```
clear ip ospf process
```

# OSPF関連のパラーメタ調整

## ルータプライオリティの変更
ルータプライオリティの設定をするには、インターフェイスコンフィグレーションモードで、  
ip ospf priority コマンドを実行  
```
(config-if)# ip ospf priority <ルータプライオリティ値>
```

ルータプライオリティを変更することで、意図するルータにDRの役割を持たせることが出来る。  
ルータプライオリティ値には、0 ~ 255の値を指定  
0を設定すると、DR及びBDRに選出されなくなる。  

## コストの変更  
インターフェイスのコスト値を変更するには、インターフェイスコンフィグレーションモードで、  
ip ospf costコマンドを実行  
```
(config-if)# ip ospf cost <コスト値>
```
インターフェイスのコスト値を変更することで、最適ルートを任意に変更することが出来る。  
コスト値は、1 ~ 65535の範囲で指定  

## 帯域幅
インターフェイスの帯域幅を変更するには、インターフェイスコンフィグレーションモードで、  
bandwidthコマンドを実行  
```
(config-if)# bandwidth <帯域幅>
```

帯域幅は、bps単位で指定  
※コスト値と帯域幅の変更を同時に行った場合、コスト値の変更で設定した値が優先される  

また、基準帯域幅を変更するにはルータコンフィグレーションモードで  
auto-cost reference-bandwidth コマンドを実行  
```
(config-router)# auto-cost reference-bandwidth
```

基準帯域幅は、100Mbps  


## Helloインターバルの変更
Helloインターバルを変更するには、インターフェイスコンフィグレーションモードで、  
ip ospf hello-intervalコマンドを実行  
```
(config-if)# ip ospf hello-interval <秒数>
```
Helloインターバルを変更すると、Deadインターバルは自動でその4倍の時間に設定される  

また、Deadインターバルのみを変更するには、インターフェイスコンフィグレーションモードで、  
次の ip ospf dead-intervalコマンドを実行  
```
(config-if)# ip ospf dead-interval <秒数>
```
※隣接するルータと、Helloインターバル、Deadインターバルが一致していないとネイバーとして認識されない為、  
実行する際には注意が必要  

## MTUのミスマッチ検出機能の無効化
MTUの不一致を検出する機能を無効にするには、インターフェイスコンフィグレーションモードで、  
ip ospf mtu-ignoreコマンドを実行  
```
(config-if)# ip ospf mtu-ignore
```
MTUのサイズが異なると、完全な隣接環境を築くことができない為、  
MTUを合わせるか、またはMTUの不一致を検出する機能を無効にする必要がある。  

## OSPFのネットワークタイプの変更 
OSPFのネットワークタイプを変更するには、インターフェイスコンフィグレーションモードで、  
ip ospf network コマンドを実行  
```
(config-if)# ip ospf network < broadcast | point-to-point>
```
"broadcast"を指定すると、ネットワークタイプがブロードキャストマルチアクセスに変更される。  
Ethernetインターフェイスで接続した際にはコマンド無しで自動で選択される。  

"point-to-point"を指定すると、ネットワークタイプがポイントツーポイントに変更される。  
Searialインターフェイスで接続した際にはコマンド無しで自動で選択される。  

## デフォルトルートの配布
デフォルトルートを他のルータに配布するには、ルータコンフィグレーションモードで、  
default-information originateコマンドを実行  
```
(config-router)# default-information originate [always]
```
alwaysのオプションを付けると、ルータにデフォルトルートの設定がされていなくても  
デフォルトルートを他のルータに配布することが出来る。  


# ACL設定コマンド  
## 標準ACLの設定（番号付き標準ACL）
①標準ACLを作成する  
番号付き標準ACLの作成をするには、グローバルコンフィグレーションモードで、  
access-list コマンドを実行  
```
(config)# access-list <ACL番号> <permit/deny> <送信元アドレス> <ワイルドカードマスク>
```
ACL番号には、1~99、1300~1999の範囲で指定する。  
送信元アドレス、ワイルドカードマスクには、許可/拒否する送信元アドレスとワイルドカードマスクを指定する。  
permit/denyには、指定条件に一致したパケットを許可する場合はpermit、拒否する場合はdenyを指定する。  

②インターフェイスの適用  
作成したACLをインターフェイスに、インバウンドまたはアウトバウンドで適用する。  
この設定によりACLが有効となり、そのインターフェイスでパケットフィルタリングが、行われる。  

作成した標準ACLをインターフェイスに適用するには、インターフェイスコンフィグレーションモードで  
ip access-gourpコマンドを実行する。  

```
(config-if)# ip access-group <ACL番号> <in|out>
```

ACL番号には、適用する標準ACLの番号を指定する。  
in|outは、インバウンドに指定する場合はin、アウトバウンドに指定する場合はoutを指定する。  
また、頭にnoを付けるとインターフェイスの適用を解除します。  
標準ACLでは、目安として宛先に近いインターフェイスに適用します。  


## 標準ACLの設定（名前付き標準ACL）
①標準ACLを作成する  
番号付き標準ACLの作成するには、グローバルコンフィグレーションモードで  
ip access-list standardコマンドを実行  
```
(config)# ip access-list standard <ACL名>
```

このコマンドを実行すると、標準ACLグローバルコンフィグレーションモードに移行し、  
プロンプト（config-std-nacl）# に変わります。  
その後、条件を指定していきます。  
```
(config-std-nacl)# <permit/deny> <送信元アドレス> <ワイルドカードマスク>
```
条件の指定は番号付き標準ACLの場合と同じです。  

②インターフェイスの適用  
作成した標準ACLをインターフェイスに適用するには、インターフェイスコンフィグレーションモードで、  
ip access-groupコマンドを実行する。  
```
(config-if)# ip access-group <ACL名> <in|out>
```

<ACL名>には、適用する標準ACLの名前か番号を指定します。  
<in|out>は、インバウンドに指定する場合in、アウトバウンドに指定する場合outを指定する。  
また、頭にnoを付けるとインターフェイスの適用を解除する。  
標準ACLでは、目安として宛先に近いインターフェイスに適用します。  

## 拡張ACLの設定(番号付き拡張ACL)
① 拡張ACLを作成する  

番号付き拡張ACLを作成するには、グローバルコンフィグレーションで  
access-listコマンド  
```
(config)# access-list <ACL番号> <permit|deny> <プロトコル> <送信元アドレス> <ワイルドカードマスク> [<送信元ポート番号>] <宛先IPアドレス> <ワイルドカードマスク> [<オプション>]
```
＜ACL番号＞には、拡張ACL識別する為に、100 ～ 199、2000 ～ 2699 の範囲で指定する。  
通常は100 ～ 199を使用します。こちらの全てを使用した場合に 2000 ～ 2699 を使用して行きます。  

＜permit / deny＞は、条件文のパケット許可する場合は permit、拒否する場合は denyを使用します。  
＜プロトコル＞には、プロトコル名を指定します。（ 例 ： ip / icmp / tcp / udp )  
＜送信元アドレス＞と＜宛先IPアドレス＞、それぞれの＜ワイルドカードマスク＞を指定します。  

＜送信元ポート番号＞は、省略可能です。  
プロトコルでTCP、UDPを指定した際に指定する事が出来ます。  
指定方法は、パラメータ＋ポート番号となります。パラメータには以下の種類があります。  
eq （ equal = 等しい） / neq （ not equal = 等しくない） / gt （ greater than = より大きい ）
lt （ less than = より小さい ） / range （ ポート番号の範囲 ）

＜オプション＞は、プロトコルで指定したプロトコルによって指定出来る値が異なります。  


② インターフェイスに適用する  

作成した拡張ACLをインターフェイスに適用するには、  
インターフェイスコンフィギューレションモードで ip access-groupコマンド  
```
(config)# ip access-group < ACL番号 > < in | out >
```

＜ACL番号＞には、適用する標準ACLの名前か番号を指定します。  
＜ in | out ＞は、インバウンドに指定する場合 in、アウトバウンドに指定する場合 outを指定します。  
拡張ACLでは、送信元に近いインターフェイスに適用に適用します。  

## 拡張ACLの設定(名前付き拡張ACL)


① 拡張ACLを作成する  

名前付き拡張ACLの作成には、グローバルコンフィギューレションモードで  
ip access-list extendedコマンド  
```
(config)# ip access-list extended < ACL名 >
```
このコマンドを実行すると、拡張ACLグローバルコンフィギューレションモードに移行し、  
プロンプト（config-ext-nacl）#に変わります。  

その後、条件を指定していきます。  

```
（config-ext-nacl）# < permit / deny > < プロトコル > < 送信元アドレス > < ワイルドカードマスク >
　　　　　　　　　　　[< 送信元ポート番号 >] < 宛先IPアドレス > < ワイルドカードマスク > [< オプション >]
```
条件の指定は番号付き拡張ACLの場合と同じです。  

② インターフェイスに適用する  

作成した拡張ACLをインターフェイスに適用するには、  
インターフェイスコンフィギューレションモードで ip access-groupコマンド  

```
(config)# ip access-group < ACL名 > < in | out >
```
＜ACL名＞には、適用する標準ACLの名前か番号を指定します。  
＜ in | out ＞は、インバウンドに指定する場合 in、アウトバウンドに指定する場合 outを指定します。  
拡張ACLでは、送信元に近いインターフェイスに適用に適用します。  


## ACLの削除
ACLの作成を間違い削除したい場合、グローバルコンフィギューレションモードモードで  
no access-listコマンド  
```
(config)# no access-list < ACL番号 | ACL名 >
```

この場合、対象のACLの全てのエントリが消えます。  

特定の行だけを削除するには、標準/拡張ACLコンフィギューレションモードモードで noコマンドを実行  
```
(config)# ip access-list < standard | extended > < ACL番号 | ACL名 >
（config-std-nacl）# no < シーケンス番号 >
```
＜ACL番号 | ACL名 ＞で対象の標準ACLを指定します。  
番号付きACLであっても番号自体を名前で扱う事によって、名前付きACL同様  
ACLコンフィギューレションモードモードで操作する事が出来ます。  
＜シーケンス番号＞には対象のシーケンス番号は入ります。  

## VTYアクセス制御
VTYアクセス制御を行うには、標準ACLを作成してから、  
VTYのラインコンフィギューレションモードで access-classコマンドを実行  
```
(config-line)# access-class < ACL番号 | ACL名 > <in | out>
```
＜in＞を指定すると、標準ACLで指定された送信元からアクセスを制御します。  
＜out＞は少し挙動が異なり、outの場合は、標準ACLが設定されているルータに  
VTY回線で接続し、そこからさらに別のルータへVTYアクセスする際に制御します。  
その場合、標準ACLで指定した送信元は宛先として使用されます。  
VTYアクセス制御については、[ACL](https://qiita.com/k-yasuhiro/items/4f0e59fdcdf0ec908bbf#1-3vty%E3%82%A2%E3%82%AF%E3%82%BB%E3%82%B9%E5%88%B6%E5%BE%A1)を参照









