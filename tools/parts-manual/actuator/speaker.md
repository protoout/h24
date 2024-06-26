# マニュアル: スピーカー（ブザー）

<img src="https://akizukidenshi.com/img/goods/L/104118.jpg" width="50">, 出典：[秋月電子通商](http://akizukidenshi.com/catalog/g/gP-04118/)
## 1. obnizでの配線

<details><summary>配線の仕方をクリックで開く</summary>
<a href="https://gyazo.com/081b807593f7bf2ab4725e5d44952a99"><img src="https://i.gyazo.com/081b807593f7bf2ab4725e5d44952a99.jpg" alt="Image from Gyazo" width="500"/></a>

★ 極性(+ -)なし


| 電子パーツの脚         | 接続先         |
|--------------|---------------|
| スピーカーの脚 |   5   |
| スピーカーの脚  |   6   |
</details>

## 2. 使うノードとつなぎ方

<details><summary>使うノードとつなぎ方をクリックで開く</summary>
- inject
- change
- obniz function
- debug

<a href="https://gyazo.com/86af5bb0ab066922e2c2ca830eb03244"><img src="https://i.gyazo.com/86af5bb0ab066922e2c2ca830eb03244.gif" alt="Image from Gyazo" width="1000"/></a>
</details>

## 3. 各ノードの設定方法

- change

msg.payloadを「数値」「500」（数字は任意で変更してください。単位はヘルツ。）

<a href="https://gyazo.com/cb0e5bf464ca48dd7ed5450fd7886c5e"><img src="https://i.gyazo.com/cb0e5bf464ca48dd7ed5450fd7886c5e.gif" alt="Image from Gyazo" width="500"/></a>


- obniz function

```javascript
obnizParts.Speaker.play(msg.payload); // msg.payloadで受け取った値（ヘルツ）の音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.Speaker.stop(); //止める
```


4. 初期化処理コードの編集

5番と6番に接続する例です。

```javascript
obnizParts.Speaker = obniz.wired("Speaker",{ signal:5, gnd:6 }); 
```


5. 結果

1000Hzの音が鳴り、1秒すると止まる。


■ 参考資料
[obnizの公式ドキュメント: ](https://docs.obniz.com/ja/sdk/parts/Speaker/README.md)

- 音階の表


| 音階 | 周波数[Hz] |
| ---- | ---------- |
| ド   | 523        |
| レ   | 587        |
| ミ   | 659        |
| ファ | 698        |
| ソ   | 784        |
| ラ   | 880        |
| シ   | 988        |
| ド   | 1046       |


ドレミを1秒ずつ鳴らすサンプル

```javascript

obnizParts.Speaker.play(523); // 1000Hz で音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.Speaker.play(587); // 1000Hz で音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.Speaker.play(659); // 1000Hz で音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.Speaker.stop(); 

```


