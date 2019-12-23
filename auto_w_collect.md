# タイトル
ポケモン剣盾の無限W回収を Aruduino UNO R3 + MacOS Mojave環境で自動周回する

## 目的
ポケモン剣盾の裏技の１つである、無限W回収を自動で行うための構築をMacで行いましたので、メモを残したいと思います。

## 無限W回収とは
ワイルドエリアでアイテム購入に使用できるエネルギー(ワット)を時間を進めることにより
何度も回収することのできる裏技です。この作業がとても虚無い。
→自動化するか！

## 参考
・「無限ワット」自動周回プログラムの導入方法[http://error-astray.hatenablog.com/entry/2019/12/17/012324]
・Splatoon2 イラスト投稿の自動ドット打ちをAruduino UNO R3 + macOS High Sierra環境でおこなう手順[https://qiita.com/knyrc/items/a39a7433857e83cf39a8]

## 結果
画像でOK
この状態で放置するだけでWが増えていきます。
ドックからUSBポートに刺すと電池切れの心配が無くなります。

#　ハードウェア環境
・Nintendo Switch + 付属のドック
・MacBook Pro（MacOS Mojave)
・[Arduino UNO R3](https://www.amazon.co.jp/ELEGOO-ATmega328P-ATMEGA16U2-USB%E3%82%B1%E3%83%BC%E3%83%96%E3%83%AB-Arduino%E7%94%A8/dp/B06Y5TBNQX/ref=sr_1_1?__mk_ja_JP=%E3%82%AB%E3%82%BF%E3%82%AB%E3%83%8A&keywords=arduino+uno+r3&qid=1576934258&s=videogames&sr=1-1-catcorr)
・[ジャンパーワイヤ（メス-メス）](https://www.amazon.co.jp/gp/product/B07P64GK35/ref=ppx_yo_dt_b_asin_title_o01_s00?ie=UTF8&psc=1)

#　ソフトウェア環境
・Python 3.6.８
・xcode-select：Xcodeのコマンドラインツール
・crosspack-avr：Arduino書き込み用ファイルのビルドツール
・dfu-programmer：Arduino書き込み用のコマンドラインツール
```
#terminal
brew install python3 # 入っていない場合のみ
xcode-select --install # 入っていない場合のみ
brew cask install crosspack-avr
export PATH=$PATH:/usr/local/CrossPack-AVR/bin/ # crosspack-avr にパスを通す
brew install dfu-programmer
```

# 手順
1.まずソフトウェアをダウンロードします
https://drive.google.com/file/d/1cmxYoadyxJma8MpBF6B14xdPXQip72Zg/view?usp=sharing

2.zipフォルダを展開し、ターミナルを開いて展開したフォルダ内に移動します。
```
rm Joystick.hex # 以前コンパイルしたファイルを削除
make
 [INFO]    : Finished building project "Joystick".
```

3.Arduino UNO R3への書き込み
## ArduinoをMacに接続する
Arduinoを一度綺麗にして、作ったコードを書き込みます。
```
# terminal
sudo dfu-programmer atmega16u2 erase
sudo dfu-programmer atmega16u2 flash Joystick.hex
sudo dfu-programmer atmega16u2 reset
```

# 注意
switch Pro controllerが起動していると失敗する