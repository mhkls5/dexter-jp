Windows 初心者向けインストールガイド

Git もターミナルも触ったことない方向けの完全ガイドです
この手順通りに進めれば、誰でも Dexter JP を使えます！


 全体の流れ

1. Git をインストールする
2. Bun をインストールする
3. Dexter JP をダウンロードする
4. API キーを取得する
5. 設定ファイルを作成する
6. 起動する

所要時間：約 15〜20 分

 ステップ 1: Git をインストールする

Git は、GitHub からファイルをダウンロードするために必要です。

 手順

1. Git 公式サイトを開く
   - ブラウザで https://git-scm.com/download/win にアクセス
   - 自動的に Windows 版のインストーラーがダウンロードされます

2. インストーラーを実行
   - ダウンロードした `Git-xxx.exe` ファイルをダブルクリック
   - 「このアプリがデバイスに変更を加えることを許可しますか？」→ **「はい」**

3. インストール設定
   - 基本的にすべてデフォルトのまま「Next」をクリック
   - 以下の画面で少し注意：
     - Default Editor → そのまま Next
     - Branch naming → そのまま Next
     - PATH 設定 → 「Git を PATH から使用可能」を選択**（デフォルト）
     - SSH クライアント → そのまま Next
     - HTTPS 転送 → そのまま Next
     - 行末変換 → そのまま Next
     - ターミナル → そのまま Next
     - 追加オプション → デフォルトのまま Next

4. インストール完了
   - 「Installing...」→「Finish」をクリック
   - PC を再起動 してください（重要！）

 確認方法

1. スタートメニューで「**コマンドプロンプト**」を検索して開く
2. 以下を入力：
git --version
3. 【git version 2.xx.x】 と表示されれば OK！

---

 ステップ 2: Bun をインストールする

Bun は、Dexter JP を動かすために必要なプログラムです。

 手順

1. Bun 公式サイトを開く
- ブラウザで https://bun.sh/ にアクセス

2. Windows 版をダウンロード
- ページ右上の「Install」ボタンをクリック
- または https://bun.sh/install/windows に直接アクセス

3. インストーラーを実行
- ダウンロードしたファイルをダブルクリック
- 画面の指示に従ってインストール

4. または、PowerShell でインストール**（おすすめ）
- スタートメニューで「PowerShell」を検索
- 右クリック→「管理者として実行」を選択
- 以下を入力：
  powershell
  powershell -c "irm bun.sh/install.ps1 | iex"
  
- インストールが完了するまで待つ

 確認方法

コマンドプロンプトで以下を入力：
bun --version

バージョン番号が表示されれば OK！

---

 ステップ 3: Dexter JP をダウンロードする

 手順

1. コマンドプロンプトを開く
   - スタートメニューで「コマンドプロンプト」を検索して開く

2. ダウンロードしたいフォルダに移動
   - 例：デスクトップにダウンロードする場合以下を入力
   - 
     cd %USERPROFILE%\Desktop
     

3. Dexter JP をダウンロード
   - 以下を入力：
     
     git clone https://github.com/edinetdb/dexter-jp.git
     
    【dexter-jp】 フォルダが作成されます

4. フォルダに移動
cd dexter-jp


---

## ステップ 4: API キーを取得する

Dexter JP を使うには、API キーという「鍵」が必要です。

必須：EDINET DB の API キー

1. EDINET DB にアクセス**
- https://edinetdb.jp にアクセス

2. アカウント作成
- 「登録」または「Sign Up」をクリック
- メールアドレスとパスワードを登録

3. API キーを取得
- ログイン後、ダッシュボードまたは設定画面から API キーをコピー
- 【edb_xxxxxx】 のような形式です

必須：LLM の API キー（いずれか 1 つ）

以下のいずれかを選択：

OpenAI（GPT-4）を使う場合
1. https://platform.openai.com/ にアクセス
2. アカウント作成・ログイン
3. API Keys → 「Create new secret key」
4. キーをコピー（`sk-xxxxxxx` の形式）

Anthropic（Claude）を使う場合
1. https://console.anthropic.com/ にアクセス
2. アカウント作成・ログイン
3. API Keys → キーを作成
4. キーをコピー（`sk-ant-xxxxxxx` の形式）

Google（Gemini）を使う場合
1. https://aistudio.google.com/ にアクセス
2. API キーを取得

💰 無料枠について
- EDINET DB: 無料枠あり
- OpenAI: 新規登録で$5 分の無料クレジット
- Anthropic: 無料枠は少ないので要注意
- Google Gemini: 無料枠あり

オプション：J-Quants（株価データ）

1. https://jpx-jquants.com/ にアクセス
2. アカウント作成（無料）
3. API キーを取得


ステップ 5: 設定ファイルを作成する

 手順

1. Dexter JP フォルダを開く
- エクスプローラーで `dexter-jp` フォルダを開く

2. `.env` ファイルを作成
- フォルダ内の `env.example` ファイルをコピー
- 名前を `.env` に変更
- または、メモ帳で新規作成して `.env` という名前で保存

3. API キーを編集
- `.env` ファイルをメモ帳で開く
- 以下の行を編集：

bash

#必須
OPENAI_API_KEY=sk-あなたのキーをここに貼り付け
EDINETDB_API_KEY=edb_あなたのキーをここに貼り付け

# オプション（株価データを使う場合）
JQUANTS_API_KEY=あなたのキーをここに貼り付け

4. 保存
  • ファイル→保存（Ctrl+S）
  • 拡張子が .env であることを確認（.env.txt にならないように注意！）

⚠️ 注意点

• API キーは絶対に他人に見せないでください
• GitHub にアップロードしないでください

───

ステップ 6: 依存関係をインストールする
https://github.com/mhkls5/dexter-jp

1. コマンドプロンプトを開く
2. Dexter JP フォルダに移動（デスクトップ以外にダウンロードした場合はパスを変更）
cd %USERPROFILE%\Desktop\dexter-jp

3. 依存関係をインストール
bun install

  • 数分かかることがあります
  • 完了すると node_modules フォルダが作成されます

───

ステップ 7: Dexter JP を起動する

手順

1. 起動コマンドを実行
bun run start

2. 起動したら
  • > というプロンプトが表示されます
  • ここに質問を入力できます！
試してみる例

トヨタの財務状況を分析して
ソニーと任天堂を比較して
高配当銘柄をスクリーニングして


トラブルシューティング

❌ 「git は内部コマンドとして認識されません」

→ Git のインストール後、PC を再起動 してください
→ それでもダメなら、Git を再インストール

❌ 「bun が認識されません」

→ Bun のインストール後、コマンドプロンプトを閉じて開き直す
→ それでもダメなら、PC を再起動

❌ 「ENOENT: no such file or directory」

→ 正しいフォルダにいるか確認：
cd %USERPROFILE%\Desktop\dexter-jp

❌ 「API キーが無効です」

→ .env ファイルのキーを再確認
→ スペースや余分な文字が入っていないか確認
→ API キーが正しいか、各サービスのダッシュボードで確認

❌ 「メモリが足りません」

→ 他のアプリを閉じる
→ PC を再起動して再試行

❌ ファイアウォールの警告

→ 「アクセスを許可する」を選択
→ 問題が解決しない場合は、一時的にファイアウォールを無効化してテスト

───

よくある質問

Q. 料金はかかりますか？

A. 以下がかかります：

• EDINET DB: 無料枠あり
• LLM API: 使用するサービスによる（OpenAI は従量課金）
• J-Quants: 無料

Q. どの LLM がおすすめですか？

A. OpenAI（GPT-4o） がおすすめ：

• 精度が高い
• 日本語が得意
• 新規登録で無料クレジットあり

Q. API キーはどこに保存されますか？

A. .env ファイルに保存されます。このファイルは絶対に公開しないでください

Q. 更新するにはどうすればいいですか？

A. 以下を実行：
git pull
bun install

Q. 削除するにはどうすればいいですか？

A. dexter-jp フォルダを削除するだけです

───

サポート

問題が解決しない場合は：

1. GitHub の Issues を確認：https://github.com/edinetdb/dexter-jp/issues
2. 新しい Issue を作成（英語または日本語で）

───

お疲れ様でした！🎉

これで Dexter JP が使えるようになりました！
日本株の分析を始めてみましょう！


