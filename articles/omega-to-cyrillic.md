---
title: "ChatGPTがΩのことをиだと言っている"
emoji: "🇬🇷"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---
# 要約

Yu Gothic UI SemiboldのU+03A9 (Greek Capital Letter Omega) にиが登録されていました。
なぜこうなっているかは分かりませんでした。ご存知の方がいれば教えてください...。

# はじめに

![](/images/omega-to-cyrillic/image1.png)

ChatGPTがこんなことを言っていました。иの部分は本来抵抗の単位なのでΩが正しいのですが、ChatGPTはиと言っています。なぜこうなるのか不思議に思ったので調べました。

# 考察

## 観察

とりあえずChatGPTに色々出力させて挙動を観察します。まずは、ギリシャ文字を全て出力してみましょう。

![](/images/omega-to-cyrillic/greek.png)

おや、Ωが正しく出力されています。他の文字も良さそうです。
冒頭の画像では太字で出力されていたので、太字で全ての文字を出力してみます。

![](/images/omega-to-cyrillic/greek-bold.png)

今度はΩがиになりました。この現象が起こるのは太字の場合のみのようです。また、他の文字は特に問題ないことも分かりました。

## ソースコードの確認

デベロッパーツールを使ってこのページのソースコードを見てみました。

![](/images/omega-to-cyrillic/dev.png)

これが該当部分です。иではなくΩになっているため、この部分は問題なさそうです。

## フォントの確認

次にフォントの確認をしました。

```css
font-family: ui-sans-serif, -apple-system, system-ui, Segoe UI, Helvetica, Apple Color Emoji, Arial, sans-serif, Segoe UI Emoji, Segoe UI Symbol;
```

これが該当部分です。とりあえず各フォントでΩを表示してみます。

<details><summary>html(やや長いので折り畳み)</summary>

```html
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="utf-8" />
<style>
  body{padding:20px;}
  .row{display:flex;align-items:center;gap:20px;margin:12px 0}
  .font-name{width:260px;font-size:14px;color:#333}
  .glyph{font-size:72px}
</style>
</head>
<body>
  <div class="row"><div class="font-name">ui-sans-serif</div><div class="glyph" style="font-family: ui-sans-serif;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">-apple-system</div><div class="glyph" style="font-family: -apple-system;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">system-ui</div><div class="glyph" style="font-family: system-ui;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">'Segoe UI'</div><div class="glyph" style="font-family: 'Segoe UI';">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">Helvetica</div><div class="glyph" style="font-family: Helvetica;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">'Apple Color Emoji'</div><div class="glyph" style="font-family: 'Apple Color Emoji';">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">Arial</div><div class="glyph" style="font-family: Arial;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">sans-serif</div><div class="glyph" style="font-family: sans-serif;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">'Segoe UI Emoji'</div><div class="glyph" style="font-family: 'Segoe UI Emoji';">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">'Segoe UI Symbol'</div><div class="glyph" style="font-family: 'Segoe UI Symbol';">Ω <strong>Ω</strong></div></div>
</body>
</html>
```
</details>

すると、以下のようにsystem-uiを太字にした場合のみΩがиになりました。長いので上3つだけ載せましたが、system-ui以外は正しく表示されました。
![](/images/omega-to-cyrillic/omega.png)

system-uiはOSで標準的に使用されているシステムフォントを指定するもので、私の使用しているWindows 11ではYu Gothic UIが使用されているそうです（[ソース](https://tenshoku.mynavi.jp/engineer/guide/articles/ZGXbwxEAACgAC-r4)）。

Yu Gothic UIを指定して同様にΩの太字を表示すると、確かにиになりました。

<details><summary>html(先程のコードの末尾にYu Gothic UIを追加)</summary>

```html
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="utf-8" />
<style>
  body{padding:20px;}
  .row{display:flex;align-items:center;gap:20px;margin:12px 0}
  .font-name{width:260px;font-size:14px;color:#333}
  .glyph{font-size:72px}
</style>
</head>
<body>
  <div class="row"><div class="font-name">ui-sans-serif</div><div class="glyph" style="font-family: ui-sans-serif;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">-apple-system</div><div class="glyph" style="font-family: -apple-system;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">system-ui</div><div class="glyph" style="font-family: system-ui;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">'Segoe UI'</div><div class="glyph" style="font-family: 'Segoe UI';">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">Helvetica</div><div class="glyph" style="font-family: Helvetica;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">'Apple Color Emoji'</div><div class="glyph" style="font-family: 'Apple Color Emoji';">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">Arial</div><div class="glyph" style="font-family: Arial;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">sans-serif</div><div class="glyph" style="font-family: sans-serif;">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">'Segoe UI Emoji'</div><div class="glyph" style="font-family: 'Segoe UI Emoji';">Ω <strong>Ω</strong></div></div>
  <div class="row"><div class="font-name">'Segoe UI Symbol'</div><div class="glyph" style="font-family: 'Segoe UI Symbol';">Ω <strong>Ω</strong></div></div>
</body>
</html>
```
</details>

![](/images/omega-to-cyrillic/Yu-Gothic-UI.png)

Yu Gothic UIが原因のようです。

## Yu Gothic UIの確認

charmap.exeを使ってYu Gothic UIを確認してみます。
すると、Yu Gothic UIのU+03A9 (Greek Capital Letter Omega) にはΩが登録されていますが、Yu Gothic UI SemiboldのU+03A9 (Greek Capital Letter Omega) にはиが登録されていました。

![](/images/omega-to-cyrillic/normal.png)
*Yu Gothic UI*

![](/images/omega-to-cyrillic/semibold.png)
*Yu Gothic UI Semibold*

これが全ての原因のようです。

なぜこのようになっているかは調べても分かりませんでした。
単なるミスなのか、何か意図があってこうなっているのか気になります。ご存知の方がいれば教えていただけると幸いです。

## 感想

謎解きみたいで楽しかったです。

