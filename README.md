Quercus
=======

## hiroshi-cl/quercus

- roundrop/quercus を JDK8 でビルドできるように多少の修正を加えたものです
  - 単に `mvn compile` が通るようにしただけなのできちんと動作するかは知りません
  - `Optional` の名前被り解消
  - `Base64` の名前被り解消
  - リフレクション周りで抽象メソッドが増えたのをダミーを返すメソッド実装で対応
- 本家は 4.0.39 で更新が止まり、公式サイトも半壊している状態のようです
  - と思ったんだけど maven central repository に 4.0.45 が存在: https://search.maven.org/#artifactdetails%7Ccom.caucho%7Cquercus%7C4.0.45%7Cjar
  - また、Resin は 4.0.48 が最新なのでそちらにもっと新しいバージョンが含まれるかもしれない
- 以下丸コピ

# Quercusとは

PHPをJVM上で実行するためのミドルウェアです。詳しくは本家を参照ください。http://quercus.caucho.com/

# 改変内容
本家の Quercus 4.0.39 を JDK7 でビルドできるようにしたものです。
ライセンスは本家のGPLをそのまま継承しています。

# ビルド方法
## ビルド環境
- JDK7(JDK8ではビルドできません)
- Maven2以降

## ビルド方法

    $ mvn clean package

targetディレクトリにquercus-VERSION.jarが生成されます。

## デプロイ方法

    $ mvn clean deploy
    $ git add repos
    $ git commit repos -m '....'
    $ git push origin master

# サンプルプロジェクト

https://github.com/dwango/quercus-sample

# Mavenプロジェクトで利用する方法
pom.xmlに以下のようにリポジトリとjarへの依存関係を追加する。

    <repositories>
        // ...
        <repository>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
            <id>dwango-quercus-repos</id>
            <name>Dwango Quercus Repository</name>
            <url>https://raw.github.com/dwango/quercus/master/repos/</url>
        </repository>
        //...
    </repositories>
    // ...
    <dependencies>
        // ...
        <dependency>
            <groupId>com.caucho</groupId>
            <artifactId>quercus</artifactId>
            <version>4.0.39</version>
        </dependency>
        // ...
    </dependencies>
