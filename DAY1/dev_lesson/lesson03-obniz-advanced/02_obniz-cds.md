# 照度センサー（CdS）

### **新しいことをはじめる前に**  


[新しいことをはじめる前に](../before-start.md)この手順を行いましょう。


---

## 1.やってみよう

### 0. そもそもセンサーとはなにか？

環境の変化（明るさ、圧力、温度etc...）を検出し、他のシステムに出力するデバイスです。

物理現象をアナログ電圧や場合によってはデジタル信号に変換します。



<img src="https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/07ce0f24-6b93-47ed-b668-9153aae9769d.jpg" width="500">

CdSといい、センサー部分にあたる光の強さによって抵抗値が変化します。  
（**可変抵抗素子**といいます）

通常の抵抗器（**固定抵抗素子**）と組み合わせることで、この「抵抗値の変化」を「電圧値の変化」として取り出すことができます。
このセンサーはobnizのドキュメントにはありませんが、電子部品の発展編として実際に扱ってみます。



### 1. obnizとの接続

<img src="https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/909d0f27-cd78-4386-9c6a-913114b1ae4b.jpg" width="500">


- CdS:1個
- 抵抗10KΩ:1個
- ブレッドボード:1個
- ジャンパワイヤー赤:1本
- ジャンパワイヤー黒:1本
- ジャンパワイヤー白:1本

以上の6点の部品を準備してください。

<img src="https://i.gyazo.com/aea0f2684723de82e05699203291fb76.png" width="500">

> 抵抗の数値は、カラーコードという色の帯で表現されています。（この写真は330Ωです。330Ωは橙橙茶金となります。）
> 今回利用する10KΩは `茶黒橙金` となります。  
> このあたりは[抵抗値早見表](http://part.freelab.jp/s_regi_list.html)などを参考にしてみてください。


(🚨：火傷の危険があります。注意レベルを上げましょう。)  
下記の回路をよく見て、接続を間違えないようにしましょう。

> CdSセルや抵抗が**含まれない**回路（ショート、短絡とも言います）があると、大量の電流が流れ高温になり、ブレッドボードが溶けたり、火傷の恐れがあります。

<img src="https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/71cb5fbc-3f61-47e3-aaef-9da67ccc290e.jpg" width="500">

<img src="https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/cbd3510a-9c8f-47eb-84c8-b99edb9c8336.jpg" width="500">

まずブレッドボードを横向き（横長方向）にし、CdSと抵抗を配置します。  
極性はありませんので方向は気にしなくてよいです。


図と同じ様に接続した場合、
明るくなると抵抗値が低くなる（電気が通りやすい）→ 高めの値が出ます
暗くなると抵抗値が高くなる（電気が通りにくい） → 低めの値が出ます


次にジャンパワイヤ3本を写真のようにブレッドボードに挿し、さらに以下の通りにobnizと接続します。

- obniz 0 - ジャンパワイヤ赤
- obniz 1 - ジャンパワイヤ白
- obniz 2 - ジャンパワイヤ黒

<img src="https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/1b53f227-13cb-4f93-86bc-26d7673c834c.jpg" width="500">

### 2. 仕組み

<details>
<summary>どうして抵抗器をつなぐ必要があるのか？「分圧」について</summary>

電圧は高い方から低い方に流れます。

<a href="https://gyazo.com/9ec44fded0ed5822427b5d0c64302a38"><img src="https://i.gyazo.com/9ec44fded0ed5822427b5d0c64302a38.png" alt="Image from Gyazo" width="293"/></a>

同じ抵抗値の抵抗が2つついていると、真ん中の電圧は2.5Vとなります。

<a href="https://gyazo.com/e9b1457f4b341e49e4306c74ce1a7e19"><img src="https://i.gyazo.com/e9b1457f4b341e49e4306c74ce1a7e19.png" alt="Image from Gyazo" width="318"/></a>

抵抗値が異なる抵抗が2つあると、抵抗値の比率に応じた電圧の値となります。

これを分圧といいます。

適切な抵抗値の抵抗器を接続することで、CdSセルから明るさに応じた値を取得することができるようになります。


抵抗器をつけずにCdSセルをつなげると、値は0Vになってしまいます。つまり、明るさの値を取ることができません。

<a href="https://gyazo.com/2038b85f0a568a856cfff95634a0b710"><img src="https://i.gyazo.com/2038b85f0a568a856cfff95634a0b710.png" alt="Image from Gyazo" width="310"/></a>

</details>

<img src="https://i.gyazo.com/d8f564c5f77f0608a31384faae4f9781.jpg" width="500">

obnizの端子の機能を以下のように設定し、このうち1番端子の「電圧」を計測します。

- obniz 0 - 電圧出力（5V）
- obniz 1 - 電圧入力（CdSと抵抗の**分圧**）
- obniz 2 - 電圧出力（0V）

### 3. Node-REDで動かす

以下のフローを読み込んで動かしてみましょう。
デバッグにchanged to X.XXXX vと表示されているのを確認したら。
照度センサーに手をかざし、値が変わるか確認してみてください。

```json
[{"id":"c091614d.5861c","type":"obniz-repeat","z":"d9dba4a1.01f228","obniz":"","name":"","interval":"100","code":"var voltage = await obniz.ad1.getWait();\n\nobniz.display.print(voltage)\nmsg.payload = `changed to ${voltage} v`;\n\nreturn msg;","x":230,"y":240,"wires":[["d7cb4a9f.3a6168"]]},{"id":"d7cb4a9f.3a6168","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":450,"y":240,"wires":[]}]
```

■ 参考: obniz repeatの中身

```javascript

var voltage = await obniz.ad1.getWait();

obniz.display.print(voltage)
msg.payload = voltage;

return msg;

```

■ 初期化処理コード
```javascript
obniz.io0.output(true); //io0を5vに
obniz.io2.output(false); //io2をGNDに
```
<img src="https://i.gyazo.com/bd601bf2e7ad760a85064af9dc6ced4f.gif" width="500">

※ 写真に映っているコンソールはNode-REDでないため表示が異なります


ここで使っている関数はCdS専用のものではなく、端子にかかっている電圧を測定して数値で表現できるような、汎用的なものとなります。  


> 参考：[obnizとNode.jsでCdSセル(照度センサ)を使ってみる](https://zenn.dev/protoout/articles/01-obniz-nodejs-cds)

---

その他、obnizで公式に動作確認・サポートされているパーツは、[obnizパーツライブラリ](https://docs.obniz.com/ja/sdk/parts)から参照できます。

この中にないものを触ってみたい場合も動かせる可能性はありますが、まずはパーツライブラリから選ぶのが手っ取り早くてオススメです。

## 2.演習

### 2-1. 光センサーの値をダッシュボードに表示しよう

ダッシュボードを使い、光センサーの値を可視化してみよう


### 2-2. obnizのディスプレイの光センサーの表示を最新の値が1つだけでるようにしてみよう

サンプルコードのままだと、obnizの画面には光センサーの値がたくさん出てきて見づらいです。

最新の値が1つだけでるように変更してみましょう！

<a href="https://gyazo.com/f985b7e5e46ec1bcd7f26c17b022fed7"><img src="https://i.gyazo.com/f985b7e5e46ec1bcd7f26c17b022fed7.png" alt="Image from Gyazo" width="193"/></a>

ヒント：画面の消去 ... `display.clear()`

[ディスプレイについて公式ドキュメント](https://docs.obniz.com/ja/reference/common/display#%E6%8F%8F%E7%94%BB%E9%96%A2%E6%95%B0)


### 2-3.【応用】明るさに応じてスピーカーの音が変わるテルミンのような楽器を作ってみよう


<a href="https://www.canva.com/design/DAGEsbNx3zQ/cRoX0B8ZLrePf7bGKfsaJw/watch?utm_content=DAGEsbNx3zQ&utm_campaign=designshare&utm_medium=link&utm_source=editor"><img src="https://i.gyazo.com/c3e1716a364bdd83040d7c908f4e4fcd.jpg" alt="Image from Gyazo" width="802"/></a>

#### ヒント: 複数のパーツを同時に使うときのTips

<a href="https://gyazo.com/6403c17f9cdf46fd6fd57d09e6490eef"><img src="https://i.gyazo.com/6403c17f9cdf46fd6fd57d09e6490eef.jpg" alt="Image from Gyazo" width="300"/></a>

- obniz 0 - 電圧出力（5V）
- obniz 1 - 電圧入力（CdSと抵抗の**分圧**）
- obniz 2 - 電圧出力（0V）
- obniz 9 - スピーカー
- obniz 11 - スピーカー



初期化処理コードの書き方

```javascript
obniz.io0.output(true); //io0を5vに
obniz.io2.output(false); //io2をGNDに
obnizParts.Speaker = obniz.wired("Speaker",{ signal:9, gnd:11 });//9、11番をスピーカーに

```

obnizでは、何番のピンに何を割り当てるかを初期化処理にかいて設定します。




---

**[◀ 目次ページに戻る](../readme.md)**