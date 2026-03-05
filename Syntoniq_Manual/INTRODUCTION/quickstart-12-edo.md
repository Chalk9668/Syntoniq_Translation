+++
title = "クイックスタート Syntoniq言語を学ぶ "
weight = 20
sort_by = "weight"
+++

このセクションでは、Syntoniq内で用いる記述、**Syntoniq Language** **Syntoniq言語**について説明し、デフォルトな（つまり、ごく普通の12EDOで、音名も驚くほど普通な）音楽での記譜を始めます。この後のセクションでは微分音音楽について説明します。だんだん詳しく説明されます。

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
4~8行目にかけての`[p1.0~4]`は。尚、今後この領域を**記譜セクション**と呼ぶこととします。

今は仮の説明ですが、この後の段落でより詳しく、詳細な操作を可能にする記法を説明します。

FUTURE: Update this section when the reformatter is done.

# Syntoniqファイルの構造

Syntoniqファイル（この場ではSyntoniqの為に使われるファイルという意）はタイムラインを軸に記述されます。もっと詳しい言い方をするなら、タイムラインにより命令が入る余地が用意されるということです。このSyntoniqファイルの文法は[Csound](https://csound.com)と[LilyPond](https://lilypond.org/)から強い影響を受けており、似ていますが、異なるものです。

Syntoniqでは、楽器ではなく、**Part**という単位で音符やそのダイナミクスが管理・表現され、その各Partは一つの楽器に割り当てられます。Partには和音など同時に複数の音を入れられます。又Partは**Tuning**という物を一つのPartずつ独自に持っており、これはBase pitchとScaleにより構成され、調律を決定します。このTuningは曲中のどこでも変更可能です。

音楽はScore blockという単位により表現されます。これにはNote lineという楽音を記述する領域と、Dynamic lineというダイナミクスを表現する領域に別れます。

加えて、Syntoniqファイルは、キーボードを使用される場合に、Scale definitionで音階をキーボードに定義でき、又Layout definitionでキーボード上の楽音のレイアウトを定義できます。

# 余談
死ぬほど分かりにくいと思うので、ちゃんと図解します。

そもそも、このSyntoniq言語の文法を理解するにはこのアプリケーションの設計思想から理解しないといけない。私は設計者ではないけど、解説するよ。

## 設計思想
そもそも現代の微分音音楽の作曲に於ける最大の問題はなんだったか、それは**ありとあらゆるアプリケーションが12EDOの調律を前提としている**ということ。それを解決する為に、Syntoniqが名乗り出た訳です。元来のMIDIというのは、**一つの楽器に単一の調律**が結びついていた。これは12EDOだけでやるには十分だけど、複数の音律、例えばボレピだとか31EDO、スレンドロ音階をやりたい人にはあまりにもキツい。何故なら、MIDIは12EDOのオクターヴ分割法でしか楽音のデータを扱えないから。

Syntoniqはこれに鮮やかな解決法を見出した。それは**音楽を構造化ファイルの変数と看做す**ということ。言われてみれば、我々の音楽だって簡単に構造化できる。例えばかえるの歌を擬似言語でSyntoniqっぽく構造化してみよう。

```かえるの歌
;おまじない
Part1 (name = "かえるの歌_主旋律") {
    調律(スケール="十二平均律", A4=440)
    拍子="4/4"
    速さ="100"
    楽器="唄音ウタ(notes)"
    オプション="単音で発音（歌声合成）"
    }
    
Part2 (name = "かえるの歌_コード") {
    調律(スケール="十二平均律", A4=440)
    拍子="4/4"
    速さ="100"
    楽器="ピアノ"
    オプション="コード譜"
    }

;ここから主旋律
[p1]ド（か），レ（え），ミ（る），ファ（の）
[p1]ミ（う），レ（た），ド（が），~
[p1]ミ（き），ファ（こ），ソ（え），ラ（て）
[p1]ソ（く），ファ（る），ミ（よ），~
[p1]ド（くわ），ド（くわ），ド（くわ），ド（くわ）
[p1]ド（け）ド（ろ），レ（け）レ（ろ），ミ（け）ミ（ろ），ファ（け）ファ（ろ）
[p1]ミ（くわ），レ（くわ），ド（くわ）

;ここからコード
[p2]C *
[p2]G7
[p2]C
[p2]C
[p2]G7
[p2]C
```

ただのカエルの歌だけでも、構造化できるものは多い。

# Syntax Basics

Syntoniq files usually end with the `.stq` extension, but this is not a requirement.

A Syntoniq file consists of the following things:

* Comments: the `;` introduces a comment. Comments last until the end of the line.
* Directives: these look kind of like function calls and provide general instructions to Syntoniq.
* Scale definitions: these allow you to define custom scales. You can either use Syntoniq's [generated scale](../../microtonality/generated-scales/) feature, or you can create your own completely custom scale where you give the pitches and note names.
* Layout definitions: if you are using the [Syntoniq keyboard](../../keyboard/), you can create layouts to place the notes of your scales on the keyboard.
* Score blocks: the heart of the language. Score blocks contain *note lines*, which include the notes and rhythms, and *dynamic lines*, which specify dynamics.

For a complete description of the Syntoniq language, see the [Language Reference](../../reference/language-reference/). Here are a few basics so you know what you're looking at.

A note consists of up to three parts: `duration:name:modifiers`. The duration is a *number of beats*. If you use csound, this will be familiar. If you are used to LilyPond, it is different. In LilyPond, `4` is a quarter note, `2` is a half note, etc. In Syntoniq, `1` is a beat, `2` is two beats, etc. Syntoniq doesn't have any concept of quarter notes, etc., as it breaks free from the usual notational conventions of Western music. Durations in Syntoniq can be fractions of a beat, but we'll come back to that later.

The note name always starts with a letter and may contain a wide range of characters. A note name may end with `'` followed by an optional number or `,` followed by an optional number. These indicate the number of *cycles* to go up (`'`) or down (`,`). These are similar to octave marks in LilyPond with some differences. If you want to go up or down two octaves, use `'2` or `,2` rather than repeating the mark. Also, notice that we used the term *cycle*, not *octave*. The term *cycle* refers to the interval over which a scale repeats. The default cycle size is the octave, but you can use other intervals&mdash;more on that later!

The symbol `~` is a *hold*. It means "keep doing what you were doing." In this example, it indicates a rest, but it can also mean "keep sustaining a sustained note".

This example doesn't include any note modifiers. Syntoniq supports a handful of modifiers to change articulation and note length and to sustain notes. There is no intention to add a wide range of modifiers to Syntoniq. Syntoniq's goal is not to be a complete musical production system. Its goal is to create music with fully specified pitch and dynamics. For experimentation, study, and working out melodic and harmonic ideas, this is often all you need. For complete musical production, you can take the output that Syntoniq generates and add further refinements in Csound or the Digital Audio Workstation of your choice.

# Playing the File

Use the `syntoniq` command-line tool to convert a file to musical output. Run `syntoniq --help` to see the available options and subcommands.

Save the above example to a file called `hello.stq`. Then you can run
```sh
syntoniq generate --score=hello.stq \
   --csound=hello.csd \
   --midi=hello.midi \
   --json=hello.json
```

You should see
```
syntoniq score 'hello.stq' is valid
JSON output written to hello.json
MIDI output written to hello.midi
Csound output written to hello.csd
```

The `--score` option is required. If no other options are given, `syntoniq` will just validate the score and report any errors it finds. The other options all tell `syntoniq` to generate a certain type of output.

The file `hello.csd` contains [Csound](https://csound.com) output. If you want to use Csound, you can install it from its website. Then just run `csound hello.csd` to hear the file. You can create your own Csound instruments to use with Syntoniq. By default, it includes a simple instrument with a simple wave form that's good for clearly hearing pitches and intervals...but you probably wouldn't want to listen to a piece of music with it! *Please note: you can create much better audio with csound. This is a limitation of Syntoniq's default instrument, not csound itself!*

{{ audio(src="hello-csound.mp3", caption="Audio Created with Csound") }}

The file `hello.midi` is a standard MIDI file with MPE (Midi Polyphonic Expression) compatible pitch bend statements. In this example, which uses regular 12-tone pitches, there won't be any, but for microtonal music, these are essential. A file like this can be loaded into a Digital Audio Workstation (DAW) or consumed by other MIDI tools. You can play this with a MIDI player of your choice. You can also render it with [FluidSynth](https://www.fluidsynth.org). The command `fluidsynth -iq -F a.wav a.midi` converts `a.midi` to `a.wav`.

<!--
To generate
* fluidsynth -iq -F /tmp/a.wav /tmp/a.midi
* convert to mp3 using same lame as in static-src/Taskfile.yml
-->
{{ audio(src="introduction/hello-fluid.mp3", caption="Audio Created by FluidSynth") }}

For better quality with fluidsynth, you can run `fluidsynth` interactively and give it the `interp 7` command. Then you send MIDI files to its input port. See documentation for `fluidsynth` for more help.

Another way to hear this on Linux is to install a synth tool, such as Surge XT, and to send the file to it using a tool such as `aplaymidi`. For example:
```sh
# start Surge XT and set up audio
aplaymidi --port='Midi Through' hello.midi
```
On other platforms, you can just load this into your favorite DAW or MIDI player.

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

The file `hello.json` contains complete information about the timeline that `syntoniq` generated. You can use this for study, or it could be the basis for creating other ways to render the audio without modifying the Syntoniq software. All the information that the Csound and MIDI generators use is encoded in this JSON file.