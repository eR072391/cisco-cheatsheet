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



