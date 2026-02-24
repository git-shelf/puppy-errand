# 子犬のおつかい — Git小説 指示書

## コンセプト

GitHubリポジトリ上で展開される短編小説。
本文（Markdownファイル）が「子犬の世界」、コミット履歴が「上位存在の操作ログ」として機能する。
読者は本文を読んだあとコミット履歴を遡ることで、もう一つの物語を発見する。

## ルール

- コミッター名: `fate` / メール: `fate@unknown`
- コミットメッセージは英語・小文字・淡々と（感情を出さない）
- 1コミット = 1操作。余計なファイルを混ぜない
- `git rebase` や `git commit --amend` は禁止（履歴改変不可）
- 本文の文体: ひらがな多め、絵本調、子犬の一人称「ぼく」

## リポジトリ初期構造

```
puppy-errand/
├── README.md          ← 「これは子犬のおつかいの記録です」とだけ書く
├── shopping-list.txt  ← 空ファイル（最後まで空のまま）
├── story.md           ← 本編
└── .gitignore         ← 空ファイル
```

---

## コミット手順（この順番で実行）

### 第1幕：出発

**commit 1**
- 操作: リポジトリ初期化、上記4ファイルを作成
- story.md の内容:

```
# おつかい

おかあさんが言った。
「おつかいに行ってきてくれる？」

ぼくはしっぽをふった。
まかせて。ぼくはもう おおきいんだから。

かいものリストを くびわにはさんで、ぼくは いえをでた。
```

- commit message: `init: create world`

---

### 第2幕：晴れた道

**commit 2**
- 操作: story.md に追記
- 追記内容:

```

おひさまが ぽかぽかしてる。
しってる みちだ。まっすぐ いけば おみせにつく。

たんぽぽが さいていた。
くんくん。いいにおい。
```

- commit message: `add: sunlight and path`

---

### 第3幕：雨が降る

**commit 3**
- 操作: `weather.md` を新規作成

```
# てんき

あめ。
```

- commit message: `add: weather system`

**commit 4**
- 操作: story.md に追記

```

とつぜん、そらが くらくなった。
ぽつ。ぽつぽつ。ざあざあ。

ぼくは はしった。
でも あしが どろだらけになって、くびわの かみが ぬれてきた。
```

- commit message: `apply: rain to subject`

---

### 第4幕：迷子（ブランチ分岐）

**commit 5**
- 操作: `git checkout -b lost` で新ブランチ作成
- story.md に追記:

```

あめがやんだ。
でも、ここ どこだろう。

みたことない おうちがならんでる。
しらない においがする。

ぼく、まいごに なっちゃった。
```

- commit message: `branch: subject lost direction`

**commit 6**
- 操作: lost ブランチのまま story.md に追記:

```

おおきな ねこが いた。
「きみ、まいご？」
ぼくは うなずいた。
「おみせなら あっちだよ」
ねこは しっぽで みちを さした。
```

- commit message: `add: npc guide (cat)`

**commit 7**
- 操作: main ブランチに戻り、lost ブランチを merge
- commit message: `merge: resolve lost state`

---

### 第5幕：誘惑

**commit 8**
- 操作: `distractions.md` を新規作成

```
# ゆうわく

- ちょうちょ
- ほかの いぬ
- おいしそうな においのする ごみばこ
```

- commit message: `add: distraction elements`

**commit 9**
- 操作: `.gitignore` に `distractions.md` を追記
- commit message: `ignore: distractions`

**commit 10**
- 操作: story.md に追記:

```

いろんなものが きになったけど、
ぼくは まえをむいて あるいた。

おみせが みえてきた。
```

- commit message: `update: subject resists distractions`

---

### 第6幕：到着、しかし

**commit 11**
- 操作: story.md に追記:

```

おみせについた！

ぼくは くびわに はさんだ かみを だそうとした。

ない。

あめで ながれちゃったんだ。

ぼくは すわった。
なにを かうんだっけ。

おかあさん、なんて いってたっけ。
```

- commit message: `error: shopping list data lost`

---

### 第7幕：帰還と仕掛け

**commit 12**
- 操作: story.md に追記（最終段落）:

```

ぼくは からっぽのまま いえに かえった。

おかあさんは わらった。
「おかえり。がんばったね」

おかあさんは あたらしい かみに なにかを かいて、
れいぞうこに はった。

「つぎは これを もっていってね」
```

- commit message: `return: subject home`

**commit 13（最終コミット）**
- 操作: `shopping-list.txt` に内容を書き込む:

```
ぎゅうにゅう
たまご
にんじん

だいすきな ぼくへ
わすれても いいよ。またいけばいいんだから。
            ——おかあさん
```

- commit message: `write: shopping list`

---

## 読者体験の設計

| レイヤー | 読むもの | 体験 |
|---------|---------|------|
| 第1層 | story.md | 子犬のほのぼのおつかい話 |
| 第2層 | コミット履歴 | 無機質な上位存在が世界を操作していた事実 |
| 第3層 | shopping-list.txt | 最後に初めて内容が書かれる。おかあさんのメッセージ |
| 第4層 | .gitignore | 上位存在が意図的に「誘惑」を子犬に見えなくしていた |
| 第5層 | ブランチ履歴 | 迷子は「分岐した世界線」として処理されていた |

## 補足

- weather.md, distractions.md は本編に直接参照されないメタファイル
- 読者が `git log --oneline --graph --all` で全体像を見たとき、上位存在の設計図が浮かび上がる
- shopping-list.txt が最初から最後の1コミット前まで空である事実が、物語の核

## Claude Code への実行指示

上記のコミット手順を、commit 1 から commit 13 まで順番通りに実行してください。
各コミットの前に必ず `git config user.name "fate"` と `git config user.email "fate@unknown"` を設定してください。
ブランチ操作は手順に従い、merge 時は `--no-ff` オプションを使用してください（マージコミットを残すため）。
