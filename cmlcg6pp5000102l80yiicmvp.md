---
title: "git pull --autostashでstashとpopを自動化する"
datePublished: Sat Feb 07 2026 15:07:00 GMT+0000 (Coordinated Universal Time)
cuid: cmlcg6pp5000102l80yiicmvp
slug: git-pull-autostash
tags: git

---

## **結論**

* `--autostash`オプションをつけることで`pull`のときに`stash`と`pop`を自動化できます。
    
    ```bash
    git pull origin main --autostash
    ```
    

* `--autostash`オプションをつけると以下が自動で行われます
    
    1. `pull`の前にローカルに未コミットの変更があれば`stash`する
        
    2. `pull`が終わったら`stash`した変更を`pop`する
        
* グローバルに設定することもできます
    

```bash
git config --global pull.autostash true
```

※ `rebase`のときも同様に`--autostash`をつけることで`autostash`が有効になります。

## **はじめに**

ローカルに未コミットの変更がある状態で`pull`することはありませんか？そんなときは`stash`して`pull`して、`pull`が終わったら`pop`していました。これがなんとも面倒ですよね。  
そんなときに便利なオプションがありました。`autostash`です！  
この記事では`autostash`の使い方を紹介します。

## **autostash の使い方**

### **pull するとき**

`autostash`は`pull`のオプションなので、`pull`のときに`--autostash`をつけるだけでOKです。  
（※後述しますが`rebase`でも使えます）

```bash
git pull --autostash
```

### **rebase するとき**

`rebase`のときも同様に`--autostash`をつけるだけでOKです。

```bash
git rebase --autostash
```

## **グローバルに設定する**

`autostash`はデフォルトでは無効（`false`）になっています。なので、`pull`するときに毎回`--autostash`をつけなければなりません。毎回つけるのは面倒だ！というときは、グローバルに設定してしまいましょう。

```bash
# pull
git config --global pull.autostash true

# rebase
git config --global rebase.autoStash true
```

これで`pull`するときに`--autostash`をつけなくても`autostash`が有効になります。

### **autostash してほしくないとき**

グローバルに設定したけれど`autostash`してほしくないときもあるかと思います。そんなときは`--no-autostash`をつけることで無効にできます。

```bash
# pull
git pull --no-autostash

# rebase
git rebase --no-autostash
```

## **おまけ**

`autostash`を紹介しましたが、それでも手動で`pop`する機会はありますよね。`git stash list`で`stash`の一覧を確認して、`pop`したい`stash`の番号を探して、0番目を`pop`したいときは

```bash
git stash pop stash@{0}
```

としていましたが

```bash
git stash pop 0
```

とできることを最近知りました。`stash@{0}`を`0`に省略できるんですね！

## **参考**

* [https://git-scm.com/docs/git-pull#Documentation/git-pull.txt---autostash](https://git-scm.com/docs/git-pull#Documentation/git-pull.txt---autostash)
    
* [https://git-scm.com/docs/git-rebase#Documentation/git-rebase.txt---autostash](https://git-scm.com/docs/git-rebase#Documentation/git-rebase.txt---autostash)
    
* [https://git-scm.com/docs/git-config#Documentation/git-config.txt-rebaseautoStash](https://git-scm.com/docs/git-config#Documentation/git-config.txt-rebaseautoStash)