# まだ shrinkwrap で消耗してるの？

PLAID エンジニア/HUNTER  
山内 雅浩  
@algas

---

## Agenda

- 依存性解決できない問題
- dependency hell
- node パッケージの追加と削除
- shrinkwrap vs yarn
- 自作ツールの紹介

---

## 概要

- node.js (npm v3.x) で依存性解決する方法
- パッケージ管理を shrinkwrap から yarn (v0.18.1) へ移行した話

--

## 結論

shrinkwrap を捨てて yarn を使いましょう。  
ただし production に使うのはちょっと早いかも（後述）

---

## 依存性解決できない問題

--

### 理想

shrinkwrap を使えば node のパッケージのバージョンを  
固定できるので依存性問題なんて発生しない(はず)

--

### 現実

shrinkwrap を使ってるけど継続的な依存性解決できない  
＼(^o^)／

---

## Dependency Hell

リモートで依存性解決(しようと)する手順

1. package.json を更新する
1. npm-shrinkwrap.json を削除する
1. npm install or npm update --save を実行する
1. 依存性地獄との(果てしなく長い)闘い
1. npm shrinkwrap を実行する
1. 初めに戻る (goto 1)

---

## node パッケージの追加(削除)

package.json の手動更新でパッケージを追加しちゃダメ  
どうしても手動更新が必要であれば yarn を使って

--

## 1.Installing packages with npm commands

```
npm install --save new_package
npm shrinkwrap
npm ls
```

Not so bad

--

## 2.Installing packages from package.json with npm

```
(edit package.json)
npm update --save
npm shrinkwrap
npm ls
```

＿人人人人人人＿  
＞  突然の死  ＜  
￣Y^Y^Y^Y^Y^Y￣

--

## 3.Installing packages with yarn commands

```
yarn add new_package
yarn check
```

OK

--

## 4.Installing packages from package.json with yarn

```
(edit package.json)
yarn upgrade
yarn check
```

OK

---

## shrinkwrap vs yarn

|  | npm | yarn |
| --- | --- | --- |
| パッケージマネージャ | npm | yarn |
| パッケージファイル | package.json | package.json |
| パッケージ指定ファイル | npm-shrinkwrap.json | yarn.lock |

--

### PROS

- インストール処理が高速・安定
- 依存性解決の向上

### CONS

- yarn のインストールが必要
- yarn の不具合

--

## Yarn bugs

- production install できない
- postinstall を実行してない問題

---

## 自作ツールの紹介

npm-shrinkwrap.json から yarn.lock を生成するツールを作りました。  
https://github.com/algas/shrinkwrap2yarn  

yarn に緩やかに移行したい場合に使えます。

---

## まとめ

今すぐ shrinkwrap を捨てて yarn と旅に出よう！

株式会社プレイドでは私たちと一緒に node の依存性解決をしたりKARTEをいい感じに開発してくれるエンジニアを募集中です。

---

# おわり
