# ElectionAnalyzer

選挙時期の実データの分析のためのプロジェクト及びクラス．

基本的にほとんどのクラスがHadoopのMapReduce v1フレームワークを使用．MapReduce v1については各自で勉強して下さい．

Eclipse Luna(4.4.0)で作業を行ったプロジェクトです．Eclipse上で自動ビルドしながら作業するためには，少なくともHadoop-0.20.2の主要なライブラリをインポートするか,
あるいはHadoop-0.20.2の主要なライブラリをインポートしたプロジェクトをビルドパスに含めて下さい．（多分この方式がベターです．他のHadoopプロジェクトを作るときにも使えるので．）
もし準備が面倒であれば，私が作成したCDH3準拠のHadoopプロジェクトがあるので，これをGithubからPullしてインポートしてもよいでしょう．ただし，CDH3はかなり古いことは注意して下さい．
  
[松澤のHadoopEclipseProject](https://github.com/YuMatsuzawa/HadoopEclipseProject)

もっと言うと，2014年度に稼働した研究室クラスタはCDH5で，  Githubに行くとCDH5用のEclipseプラグインがあるようです．
これをインポートし，かつクラスタの管理者（松澤卒業後は前田さん）の方と相談して，クラスタの設置してあるネットワークのルータを設定し，ポートを大橋・鳥海研ネットワーク向けに開放しておくことで，
本番環境と折衝しながらデバッグするような準備も一応できるようですが，私はやったことがなく，どの程度のことができるのかもちょっと不明です．
やってみる場合は「CDH Eclipse」等で検索して出てくるブログやガイドなどを読みながら設定して下さい．

なんにせよ必要なクラスを提供するライブラリがきちんとビルドパスに含まれていれば，Eclipse上でビルドしながら作業はできます．

クラスタ上で実行するためには、jarファイルに固めてゲートウェイのホームフォルダにアップロードし、

``hadoop jar <path>/<jarfilename>.jar [argument]``

とします。argumentにはクラス内で規定した引数（MapReduceジョブ指定子）パターンを入力します。
本クラスではJOB_PROPテーブル内で有効なパターンが指定されています。
argumentを入力せずにコマンド実行することで、パターンリストが表示されます。
詳細な利用法は各Mapper/Reducerのソース内コメントあるいは以下のdocを参照して下さい。

新たなジョブのためのMapper/Reducerを作成した場合は、JOB_PROPテーブルにそのMapRを使用するためのジョブを登録して下さい。
JOB_PROP要素の書き方はdoc内に

コマンドライン引数argumentの個数はクラスごとに指定できます。



## AnalyzerMain

ドライバークラス（Hadoopに対するジョブの投入を行うクラス）です．main関数を含み，ElectionAnalyzerクラス全体としてのエントリポイントです．