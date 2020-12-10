# practice-CPP

c++の練習用
http://cpp-lang.sevendays-study.com/
↑ 参考サイト

https://github.com/google/googletest/releases/tag/release-1.10.0 ↑Google Test
C++ Framework のダウンロード先。

## google test 展開、ビルド手順

```
tar zxvf googletest-release-1.10.0.tar.gz
cd googletest-release-1.10.0/googletest/
mkdir build
cd build/
cmake ..
make
```

このままだとテスト用の実行ファイルを作るのに下記のコマンドを毎回実行しないといけ
ない

```
$ g++ sample.cpp -I/path/to/googletest-release-1.8.1/googletest/include -L/path/to/googletest-release-1.8.1/googletest/build -lpthread -lgtest_main -lgtest
```

上記のコマンドを毎回入力するのは避けたい（コピペも）なのでシステム全体で利用でき
るようにビルドした成果物の移動とリンク作成

```
sudo mv googletest-release-1.10.0 /usr/local/
sudo chown -R root: /usr/local/googletest-release-1.10.0/

sudo ln -s /usr/local/googletest-release-1.8.1/googletest/include/gtest /usr/local/include/gtest
sudo ln -s /usr/local/googletest-release-1.8.1/googletest/build/libgtest_main.a /usr/lib/libgtest_main.a
sudo ln -s /usr/local/googletest-release-1.8.1/googletest/build/libgtest.a /usr/lib/libgtest.a
sudo ln -s /usr/local/googletest-release-1.8.1/googletest/build/libgtest_main.so /usr/lib/libgtest_main.so
sudo ln -s /usr/local/googletest-release-1.8.1/googletest/build/libgtest.so /usr/lib/libgtest.so
```

以上の操作でライブラリのリンクオプション(-I)とヘッダーファイルのディレクトリ指定
オプション(-L)を省略できるから。テスト用の実行ファイルを作成するコマンドが以下の
ように短くなる。

```
$ g++ sample.cpp -lpthread -lgtest_main -lgtest
```
