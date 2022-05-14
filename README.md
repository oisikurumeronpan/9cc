# 9cc

## OverView

[こちら](https://www.sigbus.info/compilerbook#%E9%9B%BB%E5%8D%93%E3%83%AC%E3%83%99%E3%83%AB%E3%81%AE%E8%A8%80%E8%AA%9E%E3%81%AE%E4%BD%9C%E6%88%90)を参考に、コンパイラの勉強をしていく

## SetUp

当方M1 Macを利用しているため、Dockerを利用して環境構築をおこなった。

[この手順](https://www.sigbus.info/compilerbook#%E3%82%BB%E3%83%83%E3%83%88%E3%82%A2%E3%83%83%E3%83%97%E6%89%8B%E9%A0%86)を参考に環境を構築したが、アセンブリのタイミングで以下エラーに遭遇したため、ちょっと修正した。

```
docker run --rm -v $HOME/9cc:/9cc -w /9cc compilerbook cc -o tmp tmp.s
tmp.s: Assembler messages:
tmp.s:1: Error: unknown pseudo-op: `.intel_syntax'
tmp.s:4: Error: operand 1 must be an integer register -- `mov rax,123'
```

上記を解決するために、利用するubuntuのDockerイメージを`amd64/ubuntu`を利用するように変更しました。

```diff
- FROM ubuntu:latest
+ FROM amd64/ubuntu:latest
```

以下ビルド手順

```
$ git clone ...
$ cd 9cc
$ docker build -t compilerbook .
```

## How To Run Commands

[この手順](https://www.sigbus.info/compilerbook#%E3%82%BB%E3%83%83%E3%83%88%E3%82%A2%E3%83%83%E3%83%97%E6%89%8B%E9%A0%86)
でコマンドを実行するサンプルがいくつか紹介されていますが、`amd64/ubuntu`の利用に伴い`--platform linux/amd64`オプションを追加する必要があります。

例えば`ls`コマンドを実行する場合は、以下のように実行が可能です。

```
docker run --rm -v ~/9cc:/9cc -w /9cc --platform linux/amd64 compilerbook ls /
```
