
## LED制御(Python）

次にMQTT ClientからLEDの点灯/消灯の制御を行います。


### Out/In ShieldとLEDの接続
RaspberryPIにOut/In Shieldを取り付けます。

Out/In ShieldのGPIO4コネクタに#101 LED Brickを接続します。

### 証明書ファイルの準備

温度センサの同期で準備したファイルをそのまま使用します。

#### ディレクトリ構成

```
aws/
  └ key/
      ├ xxxxxxxxxx-certificate.pem.crt (ダウンロードしたSSL証明書)
      ├ xxxxxxxxxx-private.pem.key     (プライベートキー)
      └ rootCA.pem                     (コマンドにて取得したルート証明書)
```

執筆中