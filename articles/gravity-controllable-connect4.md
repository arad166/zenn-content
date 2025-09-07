---
title: "重力操作可能なコネクト4のゲームAIを作る"
emoji: "🔴"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---
# 要約
コネクト4に重力操作を加えた自作ゲームと、そのゲーム用のAIを作成しました。

# ゲームの概要

コネクト4に重力操作を加えると面白いのでは？と思い、作ってみました。

## ルール
基本的なルールは通常のコネクト4と同じですが、1ターンで以下の**いずれか1つ**を選択できます：

- **コマを配置**: 空いている列にコマを入れる
- **重力の向きを変更**: 重力の向きを変更する（今の重力方向以外の3方向）

### 重力の仕組み
例えば重力を右向きに変更すると：
1. 盤上のすべてのコマが右向きに落下
2. 新しくコマを配置する際は、盤面の左端から入れる
3. コマは右向きの重力に従って右端に落ちる

### 勝敗の判定
- 4つ揃った方が勝利
- 同時に4つ揃った場合は引き分け

[こちら](https://arad166.github.io/gravity-controllable-connect4/)からプレイできるので、是非遊んでみてください。

# ゲームAIの作成

ここからが本題です。
始めに作ったのは人間vs人間のモードでしたが、せっかくなので人間vsCPUのモードも作ることにしました。
CPUのレベルは"Weak"、"Normal"、"Strong"の3段階として、それぞれ別の方法で実装しています。
尚、NormalとStrongの実装は下記の書籍を参考にしました。
>ゲームで学ぶ探索アルゴリズム実践入門～木探索とメタヒューリスティクス, 青木栄太, https://amzn.asia/d/hB4XHNZ

## 🐇Weak の実装

合法手からランダムに1つ選ぶだけです。

```typescript
// Weak CPU
export const chooseCpuActionWeak = (ctx: CpuContext): CpuAction | null => {

  // actions配列に現在の盤面で取りうる全ての合法手（コマを入れる or 重力を変える）を追加する処理
  // （具体的な実装は省略）

  // 合法手の中からランダムで選んで返す
  const choice = actions[Math.floor(Math.random() * actions.length)];
  return choice;
};
```

Weakは自滅するほど弱いですが、このゲームのルールに慣れてもらうための練習用CPUなのでこれで十分です。

## 🐑Normal の実装

原始モンテカルロ法を使います。

```typescript
// Normal CPU
export const chooseCpuActionNormal = (ctx: CpuContext): CpuAction | null => {

  // actions配列に現在の盤面で取りうる全ての合法手（コマを入れる or 重力を変える）を追加する処理
  // （具体的な実装は省略）

  const rolloutsPerAction = 50;
  let best: CpuAction | null = null;
  let bestScore = -Infinity;
  for (const action of mcCandidates) {
    let total = 0;

    //各合法手に対してrolloutsPerAction回のシミュレーションを行う
    //勝つなら1,負けるなら0,引き分けなら0.5をtotalに加算する
    //（具体的な実装は省略）

    const score = total / rolloutsPerAction;
    if (score > bestScore) {
      bestScore = score;
      best = action;
    }
  }
  return best;
};
```
<code>rolloutsPerAction</code>はシミュレーション回数で、<code>50</code>に設定しています。もう少し大きくすることもできるのですが、強くなりすぎても面白くないのでこの値にしています。

## 🦁Strong の実装

モンテカルロ木探索を使っています。実装はここでは省略します。
快適にプレイできる範囲でシミュレーション回数をできるだけ大きくしているので、かなり強いです。

## 🐇Weak vs 🐑Normal vs 🦁Strong

3つのAIの強さを検証するため、リーグ戦形式で各組み合わせ100回ずつ対戦させました。

### 対戦結果

| 対戦組み合わせ | 勝者 |
|---|---|
| 🐇Weak vs 🐑Normal | 🐑Normal（100勝0敗0分） |
| 🐇Weak vs 🦁Strong | 🦁Strong（100勝0敗0分） |
| 🐑Normal vs 🦁Strong | 🦁Strong（80勝11敗9分） |

良い塩梅で調整できていそうです。

# 感想

Strongが強すぎて私は全然勝てません。重力操作は人類には早すぎるのかもしれない。

また、今回始めてReactを使ってみました。結構面白かったです（実装はほぼ全て Cursor Pro に任せましたが）。