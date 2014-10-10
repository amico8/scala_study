# Typesafe ActivatorでEclipse＋Scalaの開発を行う準備をする
2014/10/10(Fri)に行われた「怖くないScala勉強会」の準備のため、以下の手順で環境構築しました。  
[怖くないScala勉強会](http://www.zusaar.com/event/12567004)

## Scala IDE for Eclipseをダウンロード
[http://scala-ide.org/](http://scala-ide.org/)  
> Scala用IDE。いつもJava EE 一択だったので知らなかった。。

## Typesafe Activatorをダウンロード
[http://typesafe.com/activator](http://typesafe.com/activator)

> Typesafe Activatorを使うと、コマンドラインやブラウザからScalaやPlay等の雛形プロジェクトを生成することができる。便利！  
homebrewなどでsbtをインストールして構築せずとも、自動でsbtを落としてきて実行してくれる優れ物。

### sbtとは
> Scala用のビルドツール。  
コンパイルをはじめ、プロジェクトに必要なパッケージやライブラリの管理を行ってくれるツール。  
Scalaのソースファイルをコンパイルする際、「scalac」よりもsbtで実行する方が軽いらしい。  
sbtを利用するには、ディレクトリ構造がある程度決まっているらしいが、Activatorを使えばその辺も意識せずに簡単に作れる。  
ちゃんと構造とか理解したい場合はsbt使うんだろうなー　でも今回は準備編ということで・・・

## activator uiを起動
ダウンロードしたら解凍したフォルダに移動し、以下のコマンドを入力する
```
$ cd path/to/activator
$ ./activator ui
```
> なぜか一回エラーになり、再度実行したら成功した・・・謎・・・  
起動が完了するとブラウザが立ち上がり、ホーム画面が表示されます

## プロジェクトを作成
* 上記の画面にて「Hello Scala!」をクリックする
* プロジェクトの保存場所を入力するダイアログが出てくるので適当なディレクトリを入力して、クリエイトボタンを押す
* プロジェクトが作成され必要なjarが落とされる

> この辺は問題なく〜

## IDEでプロジェクトを取り込む(Eclipse)
### 失敗編
* ダウンロードしたプロジェクト直下にあるbuild.sbtに次の記述を追加する
```
addSbtPlugin("com.typesafe.sbteclipse" % "sbteclipse-plugin" % "2.5.0")
```
* 次のコマンドを入力する
```
> sbt
sbt > eclipse
```

> ここで３時間くらい詰まった・・・  
sbtコマンドがないから、「あれ、Activatorに入ってんじゃないの？仕方ない・・・入れるか！」ってhomebrew経由で入れたんだけど、コマンド実行するとずっと以下のエラーが出る。  
*sbt.ResolveException: unresolved dependency: com.typesafe.sbteclipse#sbteclipse;2.5.0: not found*  
build.sbtじゃなくて、projet/projects.sbt にaddSbtPlugin〜を追加してもダメ。  
よくよく考えてみたら、sbtコマンドじゃなくてさっき入れたativatorでやればいいんじゃ・・・？ということで、sbtをアンインストールしてaddSbtPlugin〜の記述も消して仕切り直し。

### 成功編
* 作成したプロジェクトフォルダへ移動し、以下のコマンドを入力する
```
./activator eclipse
```
* 実行すると、Eclipseで取り込みやすいよう設定ファイルが追加される
* Eclipseを開き、File＞ Import ＞ Existing Projects Into Workspace > 作成したプロジェクトファイルを選択

> すんなり成功しました・・・。orz  
activatorで実行する場合、build.sbtでのプラグイン指定もいらなかったです。  
Activatorのブラウザ画面からも、Eclipse用のプロジェクト変換できるぽいですね。  

## 準備完了
ひとまずこれで勉強会の準備が整いました！
