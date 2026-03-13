+++
title = "クイックスタート Syntoniq言語を学ぶ "
weight = 20
sort_by = "weight"
+++

このセクションでは、Syntoniq内で用いる記述、**Syntoniq言語**について説明し、デフォルトな（つまり、ごく普通の12EDOで、音名も驚くほど普通な）音楽での記譜を始めます。この後のセクションでは微分音音楽について説明します。だんだん詳しく説明されます。

**完全なSyntoniq言語の説明は簡易なものです。全ての仕様については[こちら](../../reference/language-reference/)からお願いします。**

このSyntoniq言語の文法は[Csound](https://csound.com)と[LilyPond](https://lilypond.org/)から強い影響を受けており、似ていますが、異なるものです。

こちらはSytoniq言語で記述された簡単な楽譜です。

<!-- generate include=hello.stq checksum=f7c2a15b5a54491b3b9f9e1c471b01ed442e3f2f5d1f75691ebc9e8c9bd4631e -->
```syntoniq
syntoniq(version=1)

; これはカデンツだよ。Enjoy your Syntoniq!
[p1.0]  1:g a    b  c'
[p1.1]  1:e f    g  g
[p1.2]  2:c    1:f  e
[p1.3]  2:~    1:d  d
[p1.4]  1:~ a,   g, c,
  [p1] 64@0<    127@4
```
<!-- generate-end -->

{{ audio(src="hello-csound.mp3", caption="Audio Created with Csound") }}

この例はカデンツ第二型をハ長調で鳴らしたものです。順番に各行の説明をします。
### 一行目
一番最初に書かれている```syntoniq(version=1)```は**おまじない**です。大まかに言うと、楽譜だと認識させる為の命令ブロックです。これは**楽譜の最初に書く**必要があります。
### 三行目
次の行の頭、`;`は**コメント**です。`;`で始まるすべての行はコメントになり、命令として読み込まれません。UTF-8でエンコードできるものはだいたいいけます。
### 記譜セクション
4~8行目にかけての`[p1.0~4]`は**Part**（後述）という単位で表される、楽器の具体的な動きを示すものです。尚、今後この領域を**記譜セクション**と呼ぶこととします。

今は仮の説明ですが、この後の段でより詳しく、詳細な操作を可能にする記法を説明します。

FUTURE: Update this section when the reformatter is done.

# Syntoniqファイルの構造

Syntoniqファイル（この場ではSyntoniqの為に使われるファイルという意）はタイムラインを軸に記述されます。

Syntoniqでは、楽器ではなく、**Part**という単位で音符やそのダイナミクスが管理・表現され、その各Partは一つの楽器に割り当てられます。Partには和音など同時に複数の音を入れられます。又Partは**Tuning**という物を一つのPartずつ独自に持っており、これはBase pitchとScaleにより構成され、調律を決定します。このTuningは曲中のどこでも変更可能です。

音楽はScore blockという単位により表現されます。これにはNote lineという楽音を記述する領域と、Dynamic lineというダイナミクスを表現する領域に別れます。

加えて、Syntoniqファイルは、キーボードを使用される場合に、Scale definitionで音階をキーボードに定義でき、又Layout definitionでキーボード上の楽音のレイアウトを定義できます。

# 基本文法

完全な説明は[こちら](../../reference/language-reference/)からお願いします。飽くまでも、ここでの説明は簡易的な説明となります。

Syntoniqファイルは通常、拡張子`.stq`を使用しますが、必須ではありません。**推奨**する程度です。

Syntoniqファイルは次の要素から成り、各々は次に示すような機能を持ちます、

* コメント要素 `;`
コメントです。命令として解釈されません。
* Directive要素
実際の音楽となる楽音や調律の定義などを除いた、Syntoniqの指令です。現状ロジックは記述できませんが、関数呼び出しのような見た目になっています。
* Scale definitions要素
スケールをファイル内で定義します、[generated scale](../../microtonality/generated-scales/)にある、既に定義されたスケールを使うこともできますが、自分でピッチと音名を定義し使用することも可能です。尚、定義しない場合はデフォルトの12EDOが自動的に定義されます。
* Layout definitions要素
キーボードを使う際に定義するものです。キーボード上の音の配置を定義します。[Syntoniq keyboard](../../keyboard/)から既に定義されたものを使うこともできますが、自分で定義することも可能です。
* Score blocks要素
楽音とダイナミクスを表現します。note lineとdynamic lineから成り、note lineはScale definitions要素で定義された楽音を、dynamic lineは楽音のダイナミクスを表します。

Syntoniqにおいては、音符は`音価（拍数）+音名+詳細`という3つの情報を基に表現されます。便宜上今後は音価と書きますが、本来Syntoniqにおいては音の長さは西洋記譜法的な四分音符や八分音符といった、定義された拍に絶対な値ではなく、Syntoniqファイル内で定義される拍数により表現されます。前述した通り、Syntoniqは[Csound](https://csound.com)から強い影響を受けており、非常に文法が似ており、音価を記号ではなく純粋な値で指定するという点において類似しています。一方[LilyPond](https://lilypond.org/index.ja.html)的な、西洋記譜法の音価体系をそのまま使う表現方法からは遠いです。

**音名は必ず大文字小文字のアルファベットで始まる**必要がありますが、その後に続く文字はUTF-8がエンコードしうる範囲ならほとんど自由です。例としては、
```sh
G
Aｷ
C第三
```
といったものは使えますが、
```
ド
ｒｅ#
(C)*
```
といったものはアルファベットから始まらない為、使えません。

絶対音程も表現できます。音名の末尾に更に、`'`か`,`の二つの記号を付け加えられ、それぞれ`'`が1オクターブ上、`,`1オクターブ下を表します。この裏に更に半角数字を付け加えることにより、何オクターブ変位するかを表せます。例えば、
```sh
C'
D,
```
でCが1オクターブ上に、Dが1オクターブ下に変位したことが表現されています。又
```sh
F''
F'2
```
も同じ意味で、Fが2オクターブ上に変位したことが豹変されています。この場においては、半角数字でのオクターブ指定を推奨します。

**尚オクターブの限りではありません。この場では便宜上、オクターブと書きましたが、ノンオクターブチューニングでの表現も可能です。**

この記号、`~` は*hold*と呼ばれます。命令の裏に付けるとhold命令になります。これは「出された命令を続ける」という意味と、「ノートをサスティンする」という二つの意味を持ちます。詳しくは後述します。

## ちなみに…
この例では音符の修飾子、トリルだとかフェルマータなどの記号は使っていません。将来的にそういった機能をもつ記号や命令を追加したいとは思っていますが、その量は最小限にとどめます。何故ならば、**Syntoniqは音高と音価と抑揚を正確に記述するツール**であるからです。クラシック楽譜的な大量の記号体系を作る気はありません（てか疲れるし）。そういった仕事はDAWでやるようにしましょう。（でも翻訳者のチョークは最初**SyntoniqはDAW**と書いたくそマヌケ）

# Syntoniqファイルを演奏・変換・保存する
音楽へと変換するには、`syntoniq`をコマンドラインツールで使います。又`syntoniq --help`によりツールのヘルプと可能なオプションを出力します。

例えば、次は`hello.stq`Csound、MIDI形式に出力するものです。
```sh
syntoniq generate --score=hello.stq \
   --csound=hello.csd \
   --midi=hello.midi \
   --json=hello.json
```

そうしたら、次のような表示があります。
```
syntoniq score 'hello.stq' is valid
JSON output written to hello.json
MIDI output written to hello.midi
Csound output written to hello.csd
```

通常、変換には`--score`オプションを使用します。この引数に
```
syntoniq  generate --score=hoge.stq
```
の様に、**変換したいファイルの名称若しくはパスを入れる**ことにより変換が実行されます。他の方法もありますが、基本はこれを使うという認識でいてください。

## 各ファイルの説明
`hello.csd` は[Csound](https://csound.com)形式のファイルです。`csound hello.csd`を実行することにより、実際に音を聞くことができますが、かなりしょぼい音になってしまいます。[ここ](https://csound.com)から[Csound](https://csound.com)を導入することにより、独自に音を設定することができます。頑張って音作りしてください。

{{ audio(src="hello-csound.mp3", caption="音作りするとマシになる") }}

`hello.json`には生成の結果、生成中のステータスなどの全ての変換についてのデータが書かれています。CsoundとMIDIの演奏に使う全てのデータはここに.jsonとして納められています。他のソフトウェアとの連携や、ご自身のログ、または研究用途などにお使いいただけます。

`hello.midi`は、標準でMPE(MIDI Polyphonic Exresion)で出力されています。MPEはただの.midファイルとは異なります。いまはただの12EDOなので、さほどですが、実際に微分音を鳴らすとなると非常に重要になってくる要素です。出力したMIDIファイルはそのままお好きなDAWに取り込んで演奏することができます。試しに[FluidSynth](https://www.fluidsynth.org/)で手元の.sf2音源を使って.wavファイルに変換してみました。

<!--
To generate
* fluidsynth -iq -F /tmp/a.wav /tmp/a.midi
* convert to mp3 using same lame as in static-src/Taskfile.yml
-->
{{ audio(src="introduction/hello-fluid.mp3", caption="FluidSynthによるレンダリング") }}

# 余談
実は[FluidSynth](https://www.fluidsynth.org/)には`interpolation`という機能があり、サウンドフォントのサンプル波形を任意の音楽に変換する際に発生するノイズを、恣意的な元データにない中間値を加えることにより、より高音質にするという技術を使えます。私の環境（Joyさんの方）だと`interp 7`というコマンドでいけました。このノイズは微分音音楽だともっと顕著かもしれません。

Linuxには別のレンダリング方法があります。Surge XTなどを使う方法です。`aplaymidi`というツールを導入し、次のようなコマンドを打つとレンダリングできるかもしれません。

```sh
# start Surge XT and set up audio
aplaymidi --port='Midi Through' hello.midi
```
例えここに書かれていないレンダリング方法を使用しても結果は同じです。お好きなDAWやMIDIプレイヤー、レンダに取り込んでください。

<!--
To generate
* Start Surge XT
* Select Luna -> Analog Brass
* Start sox `rec` command with input set to monitoring the output device of Surge XT
* Use `aplaymidi --port='Midi Through'`
* Stop `rec`
* Trim the with with audacity and convert to mp3 using same lame as in static-src/Taskfile.yml
-->
{{ audio(src="introduction/hello-surge.mp3", caption="Audio Created by Surge XT with Luna/Analog Brass") }}