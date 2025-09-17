---
title: "Igor ProのコマンドウィンドウでQuineを作ってみた"
emoji: "📉"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Igor Pro","quine"]
published: true
---
# Igor ProでQuineを作る

先行事例が無いようだったので作ってみました。
### Igor Proとは
WaveMetrics社が開発した、グラフ作成、データ解析、プログラミングを統合したソフトウェアです。私はIgor Pro 8を使っており、今回のコードが他のバージョンで動くかは未検証です。

### Quineとは
自身のソースコードと同じ文字列を出力するプログラムのことです。例えば以下のC言語で書かれたコードはQuineです^[遠藤 侑介, 『あなたの知らない超絶技巧プログラミングの世界』, 技術評論社, 2015年 より引用]。
```C
char s[]="char s[]=%c%s%c;int main(){printf(s,34,s,34);}";int main(){printf(s,34,s,34);}
```

# 作成過程
先ほどのC言語Quineを改造しながら進めます。
`char s[]`は`string s`にして、`int main()`や不要な波括弧を消すと次のようになります。
```C
string s = "string s = %c%s%c;printf s,34,s,34;";printf s,34,s,34;
```
問題ないように見えますが、Igor Proでは変数名に`s`を使えないためこのコードは動きません。別の変数名にします。
```C
string str = "string str = %c%s%c;printf str,34,str,34;";printf str,34,str,34;
```
上記のコードの出力結果は
```C
string str = "string str = %c%s%c;printf str,34,str,34;";printf str,34,str,34;
```
であり、Quineになっています。しかし、このコードをもう一度実行しようとすると「name already exists as a variable」というエラーが出ます。
これは、一度目の実行で`str`という変数がすでに宣言されているため、二度目の実行時に再び宣言しようとするとエラーになるからです。せっかくQuineを作るなら何度でも実行できる方が芸術点が高いと思うので、さらに改良します。
```C
string str = "string str = %c%s%c;printf str,34,str,34; killstrings str;";printf str,34,str,34; killstrings str;
```
最後に`killstrings`を追加することで、`str`という変数を毎回消去することができます。これで何度でも実行できるようになりました。
見栄えが良くなるよう、出力の末尾に改行を入れれば完成です。
```C
string str = "string str = %c%s%c; printf str,34,str,34,10; killstrings str;%c"; printf str,34,str,34,10; killstrings str;
```