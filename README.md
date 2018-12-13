# bayespd
確率モデルをstanで実装する

開発環境には[Docker](https://www.docker.com/)を利用します

```
# イメージ作成(Dockerfileがあるディレクトリで実行)
$ docker build ./ -t bayespd

# コンテナ作成
$ docker run -v $PWD:/work -itd --name bayespd_01 bayespd

# Docker内でpython実行
$ docker exec -ti bayespd_01 python <hogehoge.py>

# テストを実行
$ docker exec -it bayespd_01 python -m unittest discover bayespd/tests

# コンテナをsshのように対話的に利用する
$ docker exec -ti bayespd_01 bash

# コンテナの停止
$ docker stop bayespd_01

# コンテナの開始
$ docker start bayespd_01
```

モジュールを追加する際には、requirements.txtに記載してください
```
# ファイルを編集
$ vim requirements.txt

# コンテナを再ビルド（Dockerfileでpipを実行しています）
# 必要に応じて、イメージとコンテナを削除
$ docker rm -f bayespd_01
$ docker build ./ -t bayespd
$ docker run -v $PWD:/work -itd --name bayespd_01 bayespd
$ docker exec -ti bayespd_01 pip list
```

ユニットテスト
```
# 個々のテストを実行
$ docker exec -it bayespd_01 python -m unittest bayespd/tests/test_hello.py

# ディレクトリ配下のテストを実行
# test_<hoge>.py が対象
$ docker exec -it bayespd_01 python -m unittest discover bayespd/tests

# 全てのテストを実行
$ docker exec -it bayespd_01 bash /work/run_test.sh
```
