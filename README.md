# diydistsensor

![diydistsensor](https://user-images.githubusercontent.com/5597377/125673593-851458ac-01b9-4ab9-953b-776fc8dae487.jpg)

## 概要
LEGO(R) Spike Prime用のDistance Sensorとして認識される自作のセンサーです。
1～9のダミーデータを返します。

## 材料
・Seeeduino Xiao

・SPIKE Hub用カードエッジコネクタ　https://github.com/Afrel-SPIKE-Prime-tec/spikeconnector

・ジャンパーワイヤー

回路図(USBから給電する場合)
![schematics](https://user-images.githubusercontent.com/5597377/125700218-60866e66-431d-4ab3-ae54-b6ac945de928.png)

## Movie

https://www.youtube.com/watch?v=j6FGpP5RkfA

## プロトコル
### (1)接続
通信速度は2400bps。
20ms周期で、Hub→Sensorへ0xF0を送信。
受信するとセンサー側がHubの存在を確認。Sensor→Hubへ約500ms Low信号を送る。

### (2)センサー情報を送信
Sensor→Hubへセンサー情報を送信。

### (3)完了待ち
Hub→Sensorに0x04が送信されたら、成功。以後、ボーレートを115200bpsに変更する。
0x04が送信されない場合、(1)へ戻る。

### (4)コマンド受信＆レスポンス返信
Hub→Sensorにコマンド送信。Sensor→Hubへレスポンス返信。返信後、(4)を繰り返す。
一定時間コマンドが到着しない場合はエラーとして、(1)へ戻る。

## 参考資料
https://github.com/sonoisa/cheese/

https://github.com/ahmedjouirou/legopup_arduino

https://www.philohome.com/wedo2reverse/protocol.htm
