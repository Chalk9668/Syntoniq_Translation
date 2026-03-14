+++
title = "キーボードを使う"
weight = 30
sort_by = "weight"
+++

実行ファイル、`syntoniq-kbd`はsyntoniqでキーボードを使う為に使います。キーボードの入力は主に**Syntoniq Scale**としてCLI上に出力されます（動画見るとわかりやすい）。殊に、**キーボード用の機能は他の機能と独立した実行ファイルとして存在**します。概念対置する実行ファイルとして、`Syonitoniq langage compiler`（楽譜変換するやつ）がありますが、両者は独立おり依存関係はありませんのでどちらか一方の機能を使い続けて問題ありません。

# 機能
実行ファイルは次の機能を備えています。

## 同型鍵盤
  * Isomorphic layouts have the property that the interval between notes is based only on the notes' relative positions. For keyboards arranged in rectangular or hexagonal grids, this means you can play in any key by just shifting your hand position.
  * Manual layouts allow you to place any note in any position. On the Syntoniq keyboard, manual layouts can automatically tile using specified rules.
  * The keyboard can be divided into regions to allow more than one scale to be used at the same time
  * Multiple layouts can be loaded, and you can switch between them and play notes from multiple layouts at the same time
* Sustain mode where pressing a key toggles the note on or off
* Flexible transposition and layout shift mode
* Console output that shows information about each note as it is played or, in sustain mode, shows the complete list of all notes that are sounding, making it a very useful transcription or harmony experimentation tool
* Read-only web UI that shows a view of the keyboard with labeled keys and other information

# ハードウェア

業務連絡: update after next HexBoard firmware after v1.2 is released

The Syntoniq Keyboard works on the following devices:
* [Novation Launchpad MK3 Pro](https://novationmusic.com/products/launchpad-pro-mk3)
* [HexBoard MIDI Controller](https://shapingthesilence.com/tech/hexboard-midi-controller/) with custom firmware (as of version 1.2)

Adding support for additional devices may be possible as the device support parts of the keyboard are isolated. To support Syntoniq Keyboard, the device must support some kind of external control where external software can receive button events and send light events. It would also be possible to create a software-based keyboard application based on an existing software programmable controller or on a custom tool. I highly recommend one of the hardware solutions. Both of the options above are affordable in comparison to many microtonal keyboard options. The HexBoard gives you 133 notes vs. the Launchpad's 64 and also works as a capable microtonal keyboard in its own right. The Launchpad is also an excellent device that has other uses, particularly as a controller for a digital audio workstation.

FUTURE: Update if the interactive chord builder is added

A future version of Syntoniq may support an interactive chord builder that uses the keyboard's output logic to send sounds to Csound or a MIDI device. This would allow you to type note names at a command-line prompt to build chords interactively. It could function in lieu of a keyboard if you don't have the hardware, or it could allow you to build scales using the full power of Syntoniq [generated scales](../../microtonality/generated-scales/).

# 補足
同型鍵盤という用語が普通に登場しましたが、いわゆる[
Isomorphic keyboard](https://en.wikipedia.org/wiki/Isomorphic_keyboard)のことです。日本だと[テルプストラキーボード(これは変拍子兄さんの二十四平均律キーボード)](http://terpstrakeyboard.com/web-app/keys.htm?fundamental=415.305&right=4&upright=3&size=83&rotation=0&instrument=piano&enum=false&equivSteps=31&spectrum_colors=false&fundamental_color=55FF55&no_labels=false&scale=!24ET%0A%0A50.0%0A100.0%0A150.0%0A200.0%0A250.0%0A300.0%0A350.0%0A400.0%0A450.0%0A500.0%0A550.0%0A600.0%0A650.0%0A700.0%0A750.0%0A800.0%0A850.0%0A900.0%0A950.0%0A1000.0%0A1050.0%0A1100.0%0A1150.0%0A1200.0%0A&names=A%E2%99%AD%0AAd%0AA%0AA%EF%BD%B7%0AB%E2%99%AD%0ABd%0AB%0AB%EF%BD%B7%0AC%0AC%EF%BD%B7%0AC%23%0ADd%0AD%0AD%EF%BD%B7%0AD%23%0AEd%0AE%0AE%EF%BD%B7%0AF%0AF%EF%BD%B7%0AF%23%0AGd%0AG%0AG%EF%BD%B7&note_colors=3f3f3f%0A%234169e1%0Affffff%0A%23dc143c%0A3f3f3f%0A%234169e1%0Affffff%0A%2332cd32%0Affffff%0A%23dc143c%0A3f3f3f%0A%234169e1%0Affffff%0A%23dc143c%0A3f3f3f%0A%234169e1%0Affffff%0A%2332cd32%0Affffff%0A%23dc143c%0A3f3f3f%0A%234169e1%0Affffff%0A%23dc143c)だとか[Lumatone Keybord](https://www.lumatone.io/)として有名な、**どこから音階を始めても音型が保たれるキーボードの奴ら**です。この日本語訳は、[めでたい](https://x.com/lapserazzle?s=20)さんのブログの記事、[流行れ！同型鍵盤 (Isomorphic Keyboard) ](https://medeblogdayo.lprz.xyz/posts/isomorphic-keyboard/)から引用してきています。広めましょう。

どうでもいいんですが**ボタン式アコーディオンのあれも同型鍵盤**です。

The Syntoniq Keyboard application is covered in depth in [SYNTONIQ KEYBOARD](../../keyboard/).
