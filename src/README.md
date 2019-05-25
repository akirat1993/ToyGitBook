[TOC]

# 公開用の簡易的なGitBookを作成する

## 方針

下記のディレクトリ構造のように,公開したいマークダウン形式ファイルを`src/`以下に配置し,それを基にホームページ`html`ファイル`docs/`を作成して`gitbook`で公開する

```
ToyGitBook/
	src/ #ホームページ(.html)を作るための元ファイルの配置場所
  	SUMMARY.md
  	README.md
  	md/ 
  		sample1.md
  		sample2.md
  	node_modules/ #gitbook installコマンドで作成されるディレクトリ
  docs/ #gitbookによって作成したhtmlがあるディレクトリ
```



## 作成詳細

1. 目次を`SUMMARY.md`で作成する.
   このサイトを作成場合は`SUMMARY.md`は以下のようになる.

   ```markdown
   # Summary
   
   * [このサイトの作り方](./README.md)
   * サンプル
   	* [サンプル1](./md/sample1.md)
   	* [サンプル2](./md/sample2.md)
   ```

   ※ファイルパスは`SUMMARY.md`から見た相対パスを表示

   ※`* [ホームページ上での表示](ファイルパス)`という風に階層的に記述

2. 必要なパッケージを`book.json`に記載

   ```json
   {
     "plugins": [
       "mathjax-commonhtml"
     ],
     "pluginsConfig": {
       "mathjax":{
           "forceSVG": true
       }
     }
   }
   ```

3. パッケージをインストール

   1. `book.json`があるディレクトリに移動

        `$cd ToyGitBook/src`

   2. パッケージをインストール

      `$gitbook install`

      →同じディレクトリ内にパッケージを含んでいる`node_modules`が作成される

4. ローカルにホームページ(`.html`ファイル)を作成+確認

   1. `$cd ToyGitBook`

   2. ホームページを作成+確認

      `$gitbook serve src docs`

      コマンドは`gitbook serve [SUMMARY.mdがあるディレクトリ] [ホームページの出力先]`

      →`Serving book on http://localhost:4000`と表示される

      →ブラウザ(Safariなど)を開いてURLに`http://localhost:4000`と打ち込むとホームページが表示される.(表示中に`src`以下のファイルをいじると表示がおかしくなる)

      →終了する場合はControl+Cなどで中断すれば良い.終了ごとに`docs`というディレクトリが作成されていることを確認

5. *GitHub*で共有

   1. *GitHub*で新規でpublicリポジトリを作成し`ToyGitBook`をその管理下におく.
   2. `Setting>GitHub Pages>Source`のところをNoneからmaster branch/docs folderに設定