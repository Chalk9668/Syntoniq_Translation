+++
title = "キーボードを使う"
weight = 30
sort_by = "weight"
+++

実行ファイル、`syntoniq-kbd`はsyntoniqでキーボードを使う為に使います。キーボードの入力は主に**Syntoniq Scale**としてコンソール上に出力されます（動画見るとわかりやすい）。殊に、**キーボード用の機能は他の機能と独立した実行ファイルとして存在**します。概念対置する実行ファイルとして、`Syonitoniq langage compiler`（楽譜変換するやつ）がありますが、両者は互いに独立おり、依存関係はございませんので、どちらか一方の機能を使い続けて問題ありません。

# 機能
実行ファイルは次の機能を備えています。

* **同型鍵盤をサポート**
  * 六角キーボードや四角キーボードがご利用いただけます
  * 決めた配置を規則的に自動で敷き詰められます
  * おなじキーボード内で同時に複数の調律や音階を使えます。`region`という単位でキーボードを分割します
  * 複数の調律や音階には複数のキーボードレイアウトがご利用可能です。こちらもおなじキーボード内で同時に使えます
* **サスティンモード**
  * キーを押すとサスティンします
* **トランスポーズとキーボートレイアウトシフト**
  * キーボートの移調もキーボートの楽音をシフト移動するのも可能です
* **入力をコンソール上に出力**
  * Syntoniq Scale として出力されます
* **鍵盤のレイアウトとその詳細を表示**
  * ブラウザ上で各々の鍵盤の楽音や機能、又その詳細を表示します

# ハードウェア

FUTURE: update after next HexBoard firmware after v1.2 is released

Syntoniqで動かせるキーボードハードウェアは予め用意されたものだと次のとおりです。
* [Novation Launchpad MK3 Pro](https://novationmusic.com/products/launchpad-pro-mk3)
* [HexBoard MIDI Controller](https://shapingthesilence.com/tech/hexboard-midi-controller/) with custom firmware (as of version 1.2)

この場においては、**使用するキーボードは上に示すようなハードウェアを強く推奨**します。Syntoniqでキーボードを使うには、ハードウェアがlight eventsを送れ、button eventsを受けれる必要があります。そういったものにきちんと基づいたものであれば、自作のハードウェアキーボードを使用することも、ご自分のコンピュータにソフトウェアキーボードを作って使用することも可能です。

FUTURE: Update if the interactive chord builder is added

将来的には、キーボードが無くても、CLIに入力した音をMIDIや[Csound](https://csound.com/)からインラクティブに鳴らせる、**interactive chord builder**を作ろうと考えています。Syntoniq [generated scales](../../microtonality/generated-scales/)の性能を誰でも、ハードウェアキーボードやソフトウェアキーボードを持たない人でもフルに使えるようにします。

Syntoniq Keyboardについては、もっと詳しい説明は[こちら](../../keyboard/)からお願いします。

# 補足
同型鍵盤という用語が普通に登場しましたが、いわゆる[Isomorphic keyboard](https://en.wikipedia.org/wiki/Isomorphic_keyboard)のことです。日本だと[テルプストラキーボード](http://terpstrakeyboard.com/web-app/keys.htm?fundamental=415.305&right=4&upright=3&size=83&rotation=0&instrument=piano&enum=false&equivSteps=31&spectrum_colors=false&fundamental_color=55FF55&no_labels=false&scale=!24ET%0A%0A50.0%0A100.0%0A150.0%0A200.0%0A250.0%0A300.0%0A350.0%0A400.0%0A450.0%0A500.0%0A550.0%0A600.0%0A650.0%0A700.0%0A750.0%0A800.0%0A850.0%0A900.0%0A950.0%0A1000.0%0A1050.0%0A1100.0%0A1150.0%0A1200.0%0A&names=A%E2%99%AD%0AAd%0AA%0AA%EF%BD%B7%0AB%E2%99%AD%0ABd%0AB%0AB%EF%BD%B7%0AC%0AC%EF%BD%B7%0AC%23%0ADd%0AD%0AD%EF%BD%B7%0AD%23%0AEd%0AE%0AE%EF%BD%B7%0AF%0AF%EF%BD%B7%0AF%23%0AGd%0AG%0AG%EF%BD%B7&note_colors=3f3f3f%0A%234169e1%0Affffff%0A%23dc143c%0A3f3f3f%0A%234169e1%0Affffff%0A%2332cd32%0Affffff%0A%23dc143c%0A3f3f3f%0A%234169e1%0Affffff%0A%23dc143c%0A3f3f3f%0A%234169e1%0Affffff%0A%2332cd32%0Affffff%0A%23dc143c%0A3f3f3f%0A%234169e1%0Affffff%0A%23dc143c)（これは変拍子兄さんの二十四平均律キーボード）だとか[Lumatone Keybord](https://www.lumatone.io/)として有名な、**どこから音階を始めても音型が保たれるキーボードの奴ら**です。この日本語訳は、[めでたい](https://x.com/lapserazzle?s=20)さんのブログの記事、[流行れ！同型鍵盤 (Isomorphic Keyboard)](https://medeblogdayo.lprz.xyz/posts/isomorphic-keyboard/)から引用してきています。広めましょう。

どうでもいいんですが、**ボタン式アコーディオンのあれも同型鍵盤**です。