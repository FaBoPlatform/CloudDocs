# デバイスの登録 (Python)

## AWS IoTの設定
AWSマネジメントコンソールから設定していきます。

下記URLよりコンソールへサインインボタンをクリックしログインを行います。

AWS
https://aws.amazon.com/jp/


### Thingの作成
まず始めにThing(デバイス)の作成を行います。

HOME画面のIoTから「AWS IoT」を選択し、AWS IoTの画面に遷移します。

![](img/setup/python/001.png)

<br>

「Create a resource」ボタンを押すことでいくつかのアイコンが表示されます。

![](img/setup/python/002.png)

<br>

ここの一番左の「Create a Thing」をクリックし、表示されたNameの項目にThing名を入力して「Create」ボタンをクリックします。

![](img/setup/python/003.png)

これでThingが作成されました。

### Ruleの作成
次にThingに対するルールを作成します。

AWS IoTの画面から先ほど作成したThingを選択することで右側に詳細が表示されます。

その詳細の下にある「Create rule」ボタンを押します。

![](img/setup/python/004.png)

ルールの作成画面が表示されます。

ここではルール名やThingからの取得条件、取得後のアクションなどを設定していきます。
![](img/setup/python/005.png)

まずはルール名、取得条件を設定します。

![](img/setup/python/006.png)

SDKのサンプルコードでは「sdk/test/Python」というTopicをデータを送ってくるため、Topic filterにはこのように設定します。

<br>

各項目の説明と今回の設定内容

|項目|説明|設定値|
|:--|:--|:--|
|Name|ルール名|raspi1_rule|
|Description|ルールに対するコメント|未設定|
|SQL version|SQLのバージョン|2016-03-23-beta(変更なし)|
|Attribute|取得する項目|*|
|Topic filter|取得するTopic|sdk/test/Python|
|Condition|取得する条件|未設定|

<br>

画面を下にスクロールするとChoose an actionがあります。

ここは受け取ったデータに対してどうするかを決める箇所になります。
![](img/setup/python/007.png)

今回はS3にデータを作成するように設定します。

S3 bucketの右にあるCreate a new resourceからバケットを作成することができます。

Role nameについても同様にCreate a new roleから作成することが出来ます。

<br>

各項目の説明

|項目|説明|設定値|
|:--|:--|:--|
|choose an action|データ取得後のアクション|S3|

choose an action以下の項目はアクションに対する設定になります。

今回はアクションでS3を設定しているため、S3に関する設定になります。

|項目|説明|設定値|
|:--|:--|:--|
|S3 bucket|データを格納するバケット|fabo-iot-sdk-test1|
|Key|出力するオブジェクト名|sdk-test-python.txt|
|Role name|設定するロール|aws_iot_s3|

※今回の例では出力するオブジェクト名は毎回同じになるため、出力するたびに上書きされてしまいます。

設定が完了したら、「Add action」>「Create」とクリックすることで作成されます。

### デバイス接続認証設定

Thingに対して実際に接続するデバイスからの認証情報の設定を行います。

AWS IoTの画面からThingを選択し、表示された詳細から「Connect a device」をクリックします。

![](img/setup/python/008.png)

ここでは今回使用するPythonが存在しないので、代わりに「NodeJS」を選択します。

選択後、ボタンが表示されるので記述内容を確認し「Generate certificate and policy」をクリックします。
![](img/setup/python/009.png)

表示された下記の３つのリンクよりファイルをダウンロードします。

* Download publick key
* Download private key
* Download certificate

![](img/setup/python/010.png)

ダウンロードが完了したら「Confirm & start connecting」をクリックします。

<br>

次に表示されたテキストボックスの内容は接続時に使用するものになりますので、テキストボックスの内容をコピーして別ファイルに貼り付けて保存しておきます。

![](img/setup/python/011.png)

それが終わりましたらReturn to Thing Detailボタンを押します。

これでAWS側のデバイス登録の設定は完了となります。