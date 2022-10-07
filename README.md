# system-design

## Client-Server Model(Architecture)

クライアントサーバーモデルとは、**何かしらの機能や情報を提供するサーバー**と、**それを利用するクライアント**を分け、**クライアントとサーバー間をネットワーク通信によって接続**する、ソフトウェアモデル。

例えば、一人の利用者が[google](google.co.jp)を見たいとなったとき、ブラウザのURLにgoogle.co.jpと入力し、Enterを押下する。その時、ブラウザはgoogle.co.jpからIPアドレスへの変換をDNS(Domain Name System)サーバーを通じて行い、IPアドレスを使ってgoogleにアクセスされ、googleは利用者に対してgoogleの検索ページ(HTML)を利用者のブラウザに返却し、ブラウザはgoogleの検索ページを表示できる。

上記の例だと、一人の利用者のブラウザがクライアントで、[google](google.co.jp)がサーバーとなる。

DNSサーバーとは、ドメイン名(google.co.jp)を、IPアドレスに変換する仕組みを提供するサーバーのことで、`dig`コマンドでDNSサーバーの動きを確認できる。 Windows では`nslookup`コマンドで確認できる。

ブラウザの例に戻るが、IPアドレスだけだとサーバーは返答できない。  
サーバーはクライアントからのアクセスを待っているが、サーバーで動いているプログラムがポート番号も追加で指定しているため、クライアントからアクセスするには追加でポート番号が必要になる。  
そのため、ブラウザはIPアドレスとポート番号を指定してアクセスするようにしている。サイトを閲覧する際は通常**HTTP**または**HTTPS**通信が行われており、HTTPはポート番号が80番、HTTPSはポート番号が443番と定められているため、ブラウザは自動でポート番号を指定してアクセスしている。

## Network protocols

ネットワークプロトコルとは、コンピュータ間で通信を行うために取り決められた約束事。

### IP(Internet Protocol)

IPとは、インターネットでIPアドレスを使い、相手までデータをパケットにして送信するためのプロトコル。  
パケットとは、バイトで構成されたデータで、ヘッダ(IPのバージョンなどメタデータ)とペイロード(データ)に分けられる。パケットの容量には制限があるため、大きな容量のデータを送る際にはパケットが複数に分けて送信されるため、ロスが発生する可能性がある。

### TCP(Transmission Control Protocol)

TCPとは、IPの上位プロトコルで、IPと一緒に用いられる。  
TCPは信頼性の高い通信を行うために使用するプロトコルであり、パケットの再送やエラー訂正などを行う機能がある。

- TCP通信は以下のように実現される
  - AがBに対してSYNを送信する(AからBへ通信を行いたいという要求)
  - BがAに対してACK/SYNを送信する(BからAへ通信可能という返答)
  - AがBに対してACKを送信する(AからBへ今から通信するという返答)
  - 上記手順の後はAとB間で通信が開始されているため、データを送受信することができる(また、上記手順のことをスリーウェイハンドシェイクと呼ばれる)

### HTTP

HTTPとは、WebクライアントとWebサーバー間で通信を行うために用いられる。  
TCPとともに使われている。
