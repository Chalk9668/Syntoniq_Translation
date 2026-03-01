+++
title = "導入"
weight = 10
sort_by = "weight"
+++

<!-- Note: the top-level README.md has a deep link to this section. Update it if the file is moved. -->

[こちら](https://github.com/jberkenbilt/syntoniq/releases)からダウンロードしてください。指示に従い、次から該当するコンピュータのものをダウンロードしてください。

* Linux amd64 (x86_64) and arm64 (aarch64) with and without Csound
* MacOS universal binaries (supporting both Intel and Apple Silicon) with and without Csound
* Windows x86_64 (64-bit only) with and without Csound

[Verifying Releases](#verifying-releases)は検証用/開発者用のリリースです。

このソフトウェアを利用するには、[Csound](https://csound.com/)を導入する必要があります。このリリースにおいては[Csound version 6.18.1](https://csound.com/download.html)をご利用ください。尚、Syntoniqがβ版を終えたら、予告無しに**Csound 7**に変更される可能性があります。お手数ですが、ご自分で定期的な確認をしていただきますようお願い申し上げます。

## Windows環境の方へ
Windows版はzipファイルで配布されています。Windows環境でSyntoniqをご利用になるには、Syntoniqのディレクトリ内に含まれる、`syntoniq-kbd`がMIDIコントローラとのインタフェースになります。インタフェースをマウントする為には、仮想MIDIポートをご自身のコンピュータに作成する必要があります。Syontoniqにおいては[LoopMIDI](https://forest.watch.impress.co.jp/docs/review/561423.html)を推奨しております。
 
* [ここ](https://forest.watch.impress.co.jp/docs/review/561423.html)から**LoopMIDI**をインストール
* 指示に従い、**loop port**を**syntoniq-loop**として作成

Csoundがパスに含まれていることを確認してください。インストール時にインストーラ上で設定可能です。尚、有効にする為に一度全てのPowerShellを再起動する必要があります。

## UNIX環境の方へ
LinuxおよびMac版は、圧縮tarball形式で配布されています。これらはsyntoniqとsyntoniq-kbdのバイナリのみを含みます。パス内のどこかに配置するか、直接実行するだけで利用可能です。Csoundバージョンについては、Csoundライブラリが参照可能であることを確認してください。通常にCsoundを導入していれば自動的に設定されている筈です。

## MacOS環境での注意点
MacOS環境だと、どうやらバイナリがおかしいと文句を言ってくるようです。その際は、下の一文をbashに入れていただければと思います。

```sh
xattr -d com.apple.quarantine syntoniq syntoniq-kbd
```

UI用いての導入も可能です。手続きは以下のとおりです。
* 実行ファイルを実行してください（ただし、以降は書く実行ファイルごとにここで示される操作を繰り返す必要があります）。
* 「syntoniq」（または「syntoniq-kbd」）が開かれていないというポップアップダイアログが表示されます。確認したら、左上にある「？」を押下してください
* 「isuue」を説明しているページが開きます。ダウンロード元を信頼し、「Open Privacy & Security settings for me」のリンクを探し、それを押下してください
* 下に「security」までスクロールし、「syntoniq」（または「syntoniq-kbd」）がMacを保護するためにブロックされた旨を確認してください
* 「Allow Anyway」を押下してください
* 今回使用した実行ファイルを再度実行します。今度は「Allow Anyway」が選択肢として表示されます。これをクリックすれば、バイナリを置き換えるまで問題なくご利用可能です

# ソースからビルド
[top-level README.md](https://github.com/jberkenbilt/syntoniq/blob/main/README.md)からお願いいたします。

# 検証用・開発者用のリソース
`syntoniq-<version>.sha256`ファイルには、すべてのリリース資産のSHA-256チェックサムが含まれています。そのファイルは、この鍵を用いてGPGによりクリア署名もされています（フィンガープリントは以下の通りです）。

 `C2C96B10011FE009E6D1DF828A75D10998012C7E` 
 
**Consign**によるデジタル署名が提供されています（認証は以下のとおりです）。
```
cosign verify-blob syntoniq-x.y.z.sha256 --bundle syntoniq-x.y.z.sha256.sigstore \
   --certificate-identity=ejb@ql.org \
   --certificate-oidc-issuer=https://github.com/login/oauth
```