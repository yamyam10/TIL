# GitHub メモ

## 基本コマンド

### ローカルリポジトリの作成

初期化して、現在あるファイルを追加して、コミットすれば OK  
ファイルがなければ`git init`のみで OK

```
git init
git add .
git commit -m "initial commit"
```

---

### リモートリポジトリからプロジェクトをコピー

ターミナルでローカルリポジトリに移動して以下のコマンド

```
cd <ローカルリポジトリのパス>
git clone <リモートリポジトリパス> (例： https://github.com/jquery/jquery.git)
```

---

### ファイル更新までの基本手順

ざっくりは以下の様な流れ

- ファイルを追加
- ファイルをコミット
- ファイルを更新

```
git add <ファイル名> //追加
git commit -a -m "任意のコメント"  //コミット (-aオプションは変更を自動検出してくれる)
git push origin main  //mainを更新
```

---

### git add の使用例

```
git add . //すべてのファイル・ディレクトリ
git add *.css //すべてのCSSファイル
git add -n //追加されるファイルを調べる
git add -u //変更されたファイルを追加する
git rm --cached //addしてしまったファイルを除外
```

---

### git commit の使用例

```
git commit -a //変更のあったファイルすべて
git commit -m "coment" //コメントを含めてコミット
git commit --amend //直前のコミットを取り消す
git commit -v //変更点を表示してコミット
```

---

### コミットの取り消し

```
git reset --soft HEAD~2 // 最新のコミットから2件分をワークディレクトリの内容を保持し取り消す
git reset --hard HEAD~2 // 最新のコミットから2件分のワークディレクトリの内容とコミットを取り消す
```

---

### コミットメッセージの修正

```
git rebase -i HEAD~2 // HEADから2件のコミットメッセージ
```

上記のコマンドを実行すると Vim が起動し、最新から過去 2 件のコミットが表示されます。

```
pick {commit_id} {commit_meessage} // 2件目
pick {commit_id} {commit_meessage} // 1件目(最新コミット)
```

`pick`の部分を`edit`もしくは`e`に変更後ファイルを保存し、
修正が完了したら`--amend`オプションを付けてコミットする。

```
git commit --amend
```

最後に下記のコマンドを実行し完了。

```
git rebase --continue
```

---

### ブランチの作成/移動/削除/変更/一覧/

ブランチは変更履歴を記録できる。

```
git branch <branch_name>  //ブランチの作成
git checkout <branch_name>  //ブランチの移動
git branch -d <branch_name>  //ブランチの削除
git branch -m <branch_name>  //現在のブランチ名の変更
git branch // ローカルブランチの一覧
git branch -a //リモートとローカルのブランチの一覧
git branch -r //リモートブランチの一覧
git checkout -b branch_name origin/branch_name //リモートブランチへチェックアウト
```

Git ブランチ操作 (git switch を利用した最新版)
ブランチは、プロジェクトの変更履歴を記録できる非常に便利な機能です。Git 2.23 以降では、ブランチの操作に特化した**git switch**コマンドが導入され、より直感的に操作できるようになりました。

```
git switch -c <branch_name>  // ブランチの作成と同時にそのブランチへ移動
git switch <branch_name>  // 既存のブランチへ移動
git branch -d <branch_name>  // ブランチの削除 (マージ済みのみ)
git branch -D <branch_name>  // ブランチの強制削除 (未マージでも可能)
git branch -m <new_branch_name>  // 現在のブランチ名を変更
git branch  // ローカルブランチの一覧
git branch -a  // リモートとローカルのブランチの一覧
git branch -r  // リモートブランチの一覧
git switch --track origin/<branch_name>  // リモートブランチを追跡するローカルブランチを作成し、チェックアウト
```

---

### ファイルの名前変更

```
git mv <変更前のファイル名> <変更後のファイル名>
git commit -a -m "[rename] ファイルの名前変更"
git push origin main
```

---

### 特定ファイルを特定のコミットに戻す

特定のコミットに戻して main に反映したい場合は以下のコマンドで。

```
git checkout <commit_id> <file_name>  //特定ファイルの指定
git checkout abcd1234 test.txt

git checkout <commit_id> <directory_path>  //特定ディレクトリの指定
git checkout abcd1234 dir/

git commit -m "[revert] changes to <file> in <commit>" //戻した内容をコミット
git push origin main //変更をプッシュ
```

---

### 今やってる作業を一時退避する

```
git stash
git stash pop //戻す場合
git stash list //退避の一覧
git stash clear //退避の消去
```

---

### ファイルの削除

```
git rm <name>  //特定のファイルorディレクトリの削除
git rm *  //全ファイルorディレクトリ
git commit -a -m "[remove] <file>"  //削除をコミット
git push origin main  //削除を反映
```

---

### add の取り消し

間違えて`git add`してしまった場合は`reset`でキャンセルできる。

```
git reset HEAD
git reset HEAD {file_name}
```

---
