# ページロードの速度を左右するネットワーク処理

Web ページを構成する各種サブリソースに対するネットワーク処理と、それに関連するブラウザの挙動についてのはなしです。

## ページロード時間の理想は 1 秒以内

ページロード時間の理想は 1 秒以内と言われますが、 それは十分な時間ではなく、ネットワークやレンダリングには大量の処理が発生します。HTML を取得するための最初のリクエストだけでもそれ以上が消費されることもあるので、すべての処理を 1 秒以内に収めることは難しいです。

## ネットワーク処理の速度に影響を与える要素

ページロードスピードにおいて、HTTP プロトコルでやりとりされるネットワーク上の処理がもっとも大きなウェイトを占めています。

### リソースの大きさ

ファイル（ペイロード）サイズが大きければ、そのデータを転送するために多くの時間がかかります。テキストデータや画像データを圧縮することでリソースの大きさを最小限に抑えます。

### HTTP リクエストの数

ブラウザはページロードを完了するまで、HTML ドキュメントをロードするだけでなく、それに紐付くアセットをロードするために連続的に HTTP リクエストします。リクエストの数が多くなれば、通信距離のオーバーヘッドや転送量は増加しやすくなります。ブラウザがキャッシュを利用することでムダな HTTP リクエストを抑えます。

### ネットワークの通信距離

データがサーバとクライアントの間を往復するために有線または無線による通信網を通過する時間や、ルータでリレー処理が行われる時間は、ネットワーク処理上のオーバーヘッドになります。

## ネットワーク処理の流れ

HTTP リクエストの流れは

1. DNS でホスト名の名前解決
2. TCP 接続の確立
3. サーバへのリクエスト
4. サーバからのレスポンス

ここにかかる時間もネットワーク処理の遅延につながります。

### ホスト名の名前解決

ブラウザでは HTTP リクエストの前に、URL のドメインに対応する IP アドレスを DNS を通じて探します。これを **DNS ルックアップ**といいます。

### TCP 接続の確立

HTTP は TCP の上位レイヤのプロトコルなので、その前提として TCP 接続を確立します。

1. クライアントからサーバへの接続要求（SYN）
2. サーバによる接続要求に対する応答（SYN-ACK）
3. クライアントによる接続開始応答（ACK）

という 3 段階のパケットのやりとりを必要とします。これを **TCP 3 ウェイハンドシェイク**と言います。

HTTPS では、SSL/TLS のハンドシェイクが行われます。通信の暗号化に必要な鍵、セッション ID、乱数などをクライアントとサーバ間でやりとりします。

### HTTP リクエストとレスポンス

TCP 接続が確立すると、クライアントは HTTP リクエストが可能になり、サーバはリクエストに応じてレスポンスを送信します。

サーバがクライアントにデータを送信するとき、転送効率が低下しないように小さいデータサイズで送信を始めて徐々に転送速度を上げていきます。これを TCP スロースタートと言います。

## HTTP/2 によるネットワーク処理の効率化

HTTP/1 では、1 つの TCP コネクションにつき 1 組のリクエストとレスポンスしか同時に扱うことができませんでした。HTTP/2 からは、1 つの TCP コネクション内に複数の独立したストリームを生成して多重化し、HTTP リクエストとレスポンスを並列で実行できるようになりました

### 通信の多重化と並行リクエスト

HTTP/1 では単一のドメインに対する TCP の同時接続数が、大抵のブラウザで最大 6 に制限されていたので、複数の TCP コネクションを持つ（異なるドメインにリクエストする）ことで並行性を確保していました。HTTP/2 では 1 つの TCP コネクション内で作れるストリームが無制限で、同時接続数という概念はなくなり、HTTP/1 より高い並列性を持って実行できます。

HTTP/2 が 1 つの TCP コネクションで**複数のストリームを生成できることによって、HTTP/1 で同時接続数を増やすために行っていた配信ドメインの分散（ドメインシャーディング）も不要**になりました。ドメインシャーディングは TCP コネクションや DNS ルックアップなどの処理をドメインごとに発生させてしまうぶん、不要なオーバーヘッドを発生させていました。

### HPACK によるヘッダ圧縮

HTTP/1 のリクエストヘッダとレスポンスヘッダはテキスト形式で、リクエストが多いほどそのオーバーヘッドの影響は大きくなります。

HTTP/2 では、リクエストやレスポンスのヘッダを HPACK というアルゴリズムで圧縮してヘッダのサイズを小さくしています。 同一ドメインの静的なリソースなど、**共通のヘッダが多いほど効率的に圧縮される**ことになり、ヘッダが小さくなります。

### 取得リソースの優先度制御

HTTP/2 ではクライアントの定義する優先度に応じて配信を制御します。優先度はリソースどうしの依存関係と重みによって定義されます。ページの構成に必須の HTML、CSS、JavaScript などのリソースはブラウザによって優先度が高く設定され、いち早く配信されるようになっています。表示上クリティカルにならない画像や非同期にロードされる JavaScript などは優先度が低く扱われます。

### サーバプッシュによる高度なリソース配信

HTTP/2のサーバプッシュは、サーバが必要なリソースを先読みして、リクエストを待たずにリソースを送信する機能です。 

HTMLをダウンロードするまではブラウザにとって依存関係がわからないのでリソースをリクエストできませんが、例えば二度目のアクセス以降、サーバでHTMLの内容がわかっていれば、重要なリソースを先行して配信するように最適化ができます。
