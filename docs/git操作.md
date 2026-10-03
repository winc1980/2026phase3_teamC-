# issueに着手してからPRを出すまで
1. mainを最新にする
```bash
git switch main
git pull origin main
```
2. 作業用ブランチを切る（例: issue #12 なら `feature/12-login`）
```bash
git switch -c feature/12-login
```
> 💡 ブランチを切ると、mainを壊さずに試行錯誤でき、変更がissue単位でまとまるのでレビューもしやすくなります。

3. 作業して、区切りごとにコミット
```bash
git status                          # 変更したファイルを確認
git add .
git commit -m "ログイン画面を追加 #12"
```
4. リモートにpush（2回目以降は `git push` だけでOK）
```bash
git push -u origin feature/12-login
```
5. GitHubで「Compare & pull request」→ 説明欄に `closes #12` と書いてPRを作成（マージ時にissueが自動で閉じる）

# チームメンバーのPRをレビューするとき
1. 自分のブランチに作業途中の変更があれば、一時退避する
```bash
git stash -u                        # -u: 新規ファイルも含めて退避
```
2. レビュー対象のブランチを取得して切り替える
```bash
git fetch origin
git switch feature/15-signup
```
3. 動作確認し、GitHubの「Files changed」でコメント → Approve / Request changes
   - PR本文の「動作確認」に書かれた手順どおりに、手元で起動して動くか確かめる
   - 「何をしたか／なぜそう書いたか／自信がないところ」を読んで、分からないところがあれば質問する
   - 「自信がないところ」に書かれた箇所は、重点的に見る

> 💡 コードの良し悪しに自信がなくても大丈夫です。動かしてみて質問するだけで、立派なレビューです。質問に答えることは、PRを出した人にとっても自分のコードを説明する練習になります。
>
> 例：「動作確認しました。手順どおり動きました。1つだけ質問があります：〇〇の部分でXXの式を使っているのはなぜですか？この書き方は初めて見たのですが、OOの書き方と比べてどんなメリットがあるんですか？」

4. 自分のブランチに戻り、退避した変更を復元する
```bash
git switch feature/12-login
git stash pop
```
