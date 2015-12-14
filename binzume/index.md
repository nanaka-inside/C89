
# Windows上でErlang開発するための諸々

　こんにちは， binzume です．ここ1年くらい仕事でErlang開発をしていたので，WindowsでErlang開発する話を．


Erlangを触ったことがない人でも読みながら試せるように気を付けていますが，入門的な内容ではないので，Erlangについて理解したい場合は別途，入門書を用意したほうが良いです．

「すごいErlangゆかいに学ぼう!」がお勧めです．

なんで Windows なのか？

宗教上の理由で林檎印のOSは使えない，根っからのWindowsユーザなので困難に立ち向かいWindows上で開発しています．
でも一番好きなOSは FreeBSD です．

- cygwinは甘え
- emacs使ったら負け
- vim？なにそれ


# 環境構築

最低限必要なもの

- Erlang/OTP 18
- Git
- rebar


## Erlangシェルの使い方とか

```
> erl
Eshell V7.1  (abort with ^G)
1> hoge.
hoge
2> Hoge = 1 + 1.
2
3> Hoge * 3.
6
4>
```


# アプリケーションを作る

rebarを使います．依存ライブラリの解決やコンパイル，テストなど一通りやってくれます．

## rebarの使い方とか

アプリケーションの雛形を作成．

``` bash
> mkdir testapp
> cd testapp
> rebar create-app appid=testapp
==> testapp (create-app)
Writing src/testapp.app.src
Writing src/testapp_app.erl
Writing src/testapp_sup.erl
```
いくつかのファイルが生成されたと思います．

コンパイル＆実行

```
> rebar compile
==> testapp (compile)
Compiled src/testapp_app.erl
Compiled src/testapp_sup.erl

> erl -pa ebin -eval "application:ensure_all_started(testapp)."
Eshell V7.1  (abort with ^G)
1>
```

この例では，実行は普通にerlコマンドで実行しています．
コンパイル済みの中間コードであるbeamディレクトリに出力されるので，それを指定してアプリケーションを起動する関数を呼んでいます．

ただ，なにも起きないですね．何も書いてないので．


テスト

``` bash
> rebar eunit skip_deps=true
==> testapp (eunit)
  There were no tests to run.
```

これもまだ何も起きないです．

## Hello, World!

生成された src/testapp_app.erl を編集します．

``` erlang
    io:format("Hello, World!"),
    ok.
```

先ほどと同じようにコンパイル＆実行すると Hello, World! と出力されます．

Erlang入門はこれで終わりです．



# 開発環境を整える(Sublime Text編)

　本来なら， notepad.exe を使いたいのですが，さすがに辛いので Erlang をサポートしている IDE を入れることにします．

- IntelliJ Idea
- Sublime Text 3

普段は Idea で開発していますが，今回は Sublime Text 3 を使います．

Sublime TextでErlang開発するためのパッケージはいくつかありますが，
Sublime Text 2専用だったり，Windowsで動かなかったりするので，適当なものに手を入れて使います．

色々手を入れたリポジトリがこちら： https://github.com/binzume/SublimErl

このリポジトリを Packages ディレクトリ下にgit cloneすれば，Windowsでも Erlang 開発できます．

```
cd "%APPDATA%\Sublime Text 3\Packages"
git clone https://github.com/binzume/SublimErl
```

後日やる気があれば，fork本にPR出したいところ．

## 設定

TODO: 色々．

## 開発してみる


TODO: サンプルプロジェクトのURL．


# 最後に

　もしも万が一，これからWindowsでErlang開発をしようとしている方がこれを読んで，少しでも助けになることがあったなら．とても嬉しいです．

