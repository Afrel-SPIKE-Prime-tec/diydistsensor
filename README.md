# diydistsensor

![diydistsensor](https://user-images.githubusercontent.com/5597377/125673593-851458ac-01b9-4ab9-953b-776fc8dae487.jpg)
![m5stickc](https://user-images.githubusercontent.com/5597377/125725713-0e166bc3-a5ad-4e03-8664-7caa427dabba.jpg)

## 概要
LEGO(R) SPIKE Prime用のDistance Sensorとして認識される自作のセンサーです。
1～9のダミーデータを返します。

## 材料
・Seeeduino XIAO 、M5StickCのどちらか。

・SPIKE Hub用カードエッジコネクタ　https://github.com/Afrel-SPIKE-Prime-tec/spikeconnector

・ジャンパーワイヤー

## 組み立てと実行

以下の回路図の通りに接続します(USBから給電する場合)。Seeeduino XiaoかM5StickCかによって接続方法が違います。

![schematics](https://user-images.githubusercontent.com/5597377/125727769-7025dcfb-4826-4344-9406-95c480ccffe4.png)

・Arduino IDEを使って、ソースコードを開きます

・M5StickCの場合はソースコード内の「#define M5STICKC」の値を1に変更します。Seeeduino XIAOの場合、値は0です。

・ソースコードをコンパイル＆書き込みます。

## Movie

https://www.youtube.com/watch?v=j6FGpP5RkfA

## プロトコル
### (1)接続の開始
通信速度は2400bps。
20ms周期で、Hub→Sensorへ0xF0を送信。
受信するとセンサー側がHubの存在を確認。Sensor→Hubへ約500ms Low信号を送る。

### (2)センサー情報を送信
Sensor→Hubへセンサー情報を送信。

### (3)接続の完了待ち
Hub→Sensorに0x04が送信されたら、接続の成功。以後、ボーレートを115200bpsに変更する。
0x04が送信されない場合、(1)へ戻る。

### (4)コマンド受信＆レスポンス返信
Hub→Sensorにコマンド送信。Sensor→Hubへレスポンス返信。返信後、(4)を繰り返す。
一定時間コマンドが到着しない場合はエラーとして、(1)へ戻る。

## 参考資料
https://github.com/sonoisa/cheese/

https://github.com/ahmedjouirou/legopup_arduino

https://www.philohome.com/wedo2reverse/protocol.htm
