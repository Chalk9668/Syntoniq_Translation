+++
title = "キーボードを使う"
weight = 30
sort_by = "weight"
+++

実行ファイル、`syntoniq-kbd`はsyntoniqでキーボードを使う為に使います。キーボードの入力は主に**Syntoniq Scale**としてCLI上に出力されます（動画見るとわかりやすい）。殊に、**キーボード用の機能は他の機能と独立した実行ファイルとして存在**します。概念対置する実行ファイルとして、`Syonitoniq langage compiler`（楽譜変換するやつ）がありますが、両者は独立おり依存関係はありませんのでどちらか一方の機能を使い続けて問題ありません。

この実行ファイルは次の機能を提供します。
* Flexible layout engine that allows isomorphic and manual layouts
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

The Syntoniq Keyboard application is covered in depth in [SYNTONIQ KEYBOARD](../../keyboard/).
