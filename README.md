# 個人開発の手順

## 1. リポジトリの作成
&nbsp; 1.1 GitHubの「Repositories」から「New」ボタンを押す。

&nbsp; 1.2 リポジトリ名はすべて小文字でハイフンで区切る（例：`my-dev-workflow`）。

&nbsp; 1.3 public/privateを選択する。

&nbsp; 1.4 README.mdファイルを追加する。

&nbsp; 1.5 必要な場合は.gitignoreファイルを追加する。

&nbsp; 1.6 ライセンスを付与する。ライセンスを明示しない場合は、他者が利用できないので注意。

## 2. ローカルにクローン
&nbsp; 2.1 作業フォルダに移動する。

&nbsp; 2.2 ローカルにクローンする。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git clone https://github.com/<ユーザー名>/<リポジトリ名>.git`

## 3. IssueとPull Requestのテンプレートを作成

&nbsp; 3.1 `.github/ISSUE_TEMPLATE/`フォルダにIssueのテンプレートを作成する。テンプレート例は[こちら](.github/ISSUE_TEMPLATE/)。

&nbsp; 3.2 `.github/PULL_REQUEST_TEMPLATE.md`ファイルにPull Requestのテンプレートを作成する。テンプレート例は[こちら](.github/PULL_REQUEST_TEMPLATE.md)。

&nbsp; 3.3 6.2~6.4を実行し、リモートリポジトリにプッシュする。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git add .`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git commit -m "chore: Add templates for issues and pull requests"`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git push origin main`

## 4. Issueの作成

&nbsp; 4.1 GitHubで該当リポジトリを開く。

&nbsp; 4.2 「Issues」から「New issue」ボタンを押す。

&nbsp; 4.3 テンプレートを選択し、新しいIssueを作成する。

&nbsp; 4.4 Issue番号を確認する（後でブランチ名やコミットメッセージに使用）。

## 5. 開発ブランチの作成

&nbsp; 5.1 新しく開発ブランチを作成する。開発ブランチの命名規則については[こちら](#開発ブランチの命名規則)。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git checkout -b <Issue番号>-<prefix>/<開発内容>`

&nbsp; 5.2 開発ブランチに切り替わっているかを確認する。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git branch`

## 6. 開発

&nbsp; 6.1 開発作業を進める。

&nbsp; 6.2 コミットしたいファイルをインデックスに追加する。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git add <file path>`

&nbsp; 6.3 インデックスに登録した内容をローカルリポジトリにコミットする。コミットメッセージの命名規則については[こちら](#コミットメッセージの命名規則)。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git commit -m "<prefix>: <開発内容> (#<Issue番号>)"`

&nbsp; 6.4 ローカルリポジトリの内容をリモートリポジトリにプッシュする。開発ブランチ名は現在いるブランチを指す`HEAD`で代用できる。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git push origin <開発ブランチ名>`

&nbsp; 6.5 必要に応じて6.1~6.4を繰り返す。

## 7. Pull Requestの作成

&nbsp; 7.1 GitHubで該当リポジトリを開く。

&nbsp; 7.2 「Pull requests」から「New pull request」ボタンを押す。

&nbsp; 7.3 新しいPull Requestを作成する。

&nbsp; 7.4 Pull requestの作成完了後、画面右下の「Development」に該当するIssueを追加する。追加したIssueは、このPull Requestのマージが成功後、自動的に閉じられる。

## 8. mainブランチへマージ

&nbsp; 8.1 GitHubで該当リポジトリを開く。

&nbsp; 8.2 GitHubのPull RequestsからマージしたいPull Requestを開く。

&nbsp; 8.3 「Merge pull request」ボタンを押す。

&nbsp; 8.4 「Confirm merge」ボタンを押し、マージする。

## 9. ローカルのmainブランチを更新

&nbsp; 9.1 mainブランチに切り替える。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git checkout main`

&nbsp; 9.2 ローカルのmainブランチを更新する。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git pull origin main`

## 10. マージされた開発ブランチの削除

&nbsp; 10.1 マージされたローカルの開発ブランチを削除する。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git branch --delete <開発ブランチ名>`

&nbsp; 10.2 マージされたリモートの開発ブランチを削除する。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git push origin --delete <開発ブランチ名>`

&nbsp; 10.3 念のため、リモートリポジトリから最新のブランチ情報を取得する。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `git fetch -p`

## 11. 4~10の繰り返し

---

# 開発Tips

## 開発ブランチの命名規則
`git checkout -b <Issue番号>-<prefix>/<開発内容>`
- Issue番号については、4.3で確認した番号を使う。
- prefixについては、以下の中から適するものを使う。
  - feature: 新しい機能の開発
  - fix: バグの修正
  - refactor: リファクタリング
  - chore: 雑務的な作業
- 開発内容については、すべて小文字でハイフンで区切る。

## コミットメッセージの命名規則
`git commit -m "<prefix>: <開発内容> (#<Issue番号>)"`
- prefixについては、以下の中から適するものを使う。
  - feat: 新しい機能の開発
  - fix: バグの修正
  - refactor: リファクタリング
  - perf: パフォーマンス向上のための変更
  - test: テストの追加や変更
  - chore: パッケージのインストールやビルドプロセスの変更など
  - docs: ドキュメントの追加や変更
  - style: コード自体には影響しない変更（空白、インデント、セミコロンなどのコーディングスタイル）
- 開発内容については、英語か日本語を使う。文末のピリオドや句点はいらない。
- Issue番号については、4.3で確認した番号を使う。

## より良いコードのために
- フォーマッターやリンターツールを導入し、コーディングスタイルを統一する。
- テストコードをしっかりと書き、保守性を上げる。
- 変数名や関数名は分かりやすくして、可読性を上げる。

## GitHub Actionsを使用したCI/CD
### CI（継続的インテグレーション）とは
- 「Continuous Integration」の略。
- コードの変更をリポジトリに統合するたびに自動でテストやビルドを行い、品質を保つ仕組みのこと。

### CD（継続的デリバリー／継続的デプロイ）とは
- 「Continuous Delivery」または「Continuous Deployment」の略。
- 継続的デリバリーは、テストやビルド後に本番環境へリリースできる状態を常に保つ仕組みのこと。
- 継続的デプロイは、テストやビルドが成功したら自動で本番環境にデプロイまで行う仕組みのこと。

### 基本的なセットアップ

1. `.github/workflows/`フォルダを作成する。

2. そのフォルダの中に、`.yml`ファイル形式でCIやCDの記述をする。詳しくはプロジェクトで使用している環境に合わせて調べてください。
