# Xonsh ドキュメント日本語翻訳ガイド

## 貢献方法

通常のGithubでPull Requestを送る手順に従ってください。具体的には以下のとおりです。

1. このプロジェクトをForkします。
1. ForkしたプロジェクトをPullし、`git checkout -b make-changes`のようにブランチを切り替えます。
1. 変更を加え、コミットします。
1. Pushし、Pull Requestを作成します。
1. 現在のメンテナである [virusbb001](https://github.com/virusbb001) がレビューを行うので、その間しばらくお待ち下さい。
	+ もしPull Requestを作成後、直したい箇所があったり、あるいは訳が不安な箇所は都度コメントを付けてください。
		+ もし直したいと宣言があれば、そこを除いてレビューを行います。修正が行われるまでマージいたしません。
		+ 不安な箇所は重点的に確認いたします。
	+ virusbb001自身も翻訳の知識があまりないため、行われるレビューはシンタックスのミスやリンクのミスの確認が多いです。翻訳の知識があるメンテナを募集しています。
1. 翻訳を行っていただいた箇所の中で修正をお願いすることがあります。その時は修正をお願いいたします。
	+ rebaseするか否かは特に指定を行いません。
1. 問題がなければマージされます。 masterにマージされたものは [virusbb001/xonsh-docs-ja](https://virusbb001.github.io/xonsh-docs-ja/) へ反映されます。

## 表示確認手順

ドキュメントのビルドに、 [xonsh](https://github.com/xonsh/xonsh)リポジトリのファイルを使用します。

1. Python 3.4以上をインストールします。
1. [xonsh](https://github.com/xonsh/xonsh) をクローン/チェックアウトします。
	+ 対応しているリビジョンをチェックアウトしてください。 `git submodule status xonsh` で確認できます。
1. このリポジトリの[patches/add\_i18n\_conf.patch](patches/add_i18n_conf.patch)を適用します。
	1. `xonsh` のリポジトリに移動します
	1. `git apply PATH_TO_THIS_REPO/patches/add_i18n_conf.patch` のようにしてパッチを適用します。
		+ `PATH_TO_THIS_REPO` のところにはこのリポジトリをクローンした場所に置き換えてください。
1. `requirements-docs.txt`に記載されたパッケージ と `sphinx-intl` 及び `xonsh` をインストールします。
	+ 仮想環境を作成して行うことをおすすめします。  
		```sh
		pip install -r xonsh/requirements-docs.txt
		pip install sphinx-intl xonsh
		```
	+ xonshをソースからインストールする場合は、 `pip install -e .` を行うことをおすすめします。
		+ これはバージョン番号に `dev` が付加されるのを避ける効果もあります。
1. このリポジトリの `LC_MESSAGES` を `xonsh/docs/locale/ja` にコピーします
	+ このリポジトリを `xonsh/docs/locale/ja` でクローンすると便利です
	+ サブモジュールとしてチェックアウトして `ln ../../../ ja` のようにしてしまうと再帰的に処理されるため避けてください。
1. `xonsh/docs` 内で `make -e SPHINXOPTS="-D language='ja'" html` を実行して日本語訳を適用させたファイルを生成します。
	+ `make` コマンドがない場合は以下のコマンドで代用できます。  
		`sphinx-build -b html -d _build/doctrees . -D language='ja' _build/html`
1. `_build/html` の中身を確認します。
