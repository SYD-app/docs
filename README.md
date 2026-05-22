# PDF URL Generator

PDFファイルをGitHubリポジトリにアップロードし、共有URLを発行するシンプルなWebアプリです。

公開URL: https://syd-app.github.io/docs/

## 特徴

- PDFをドラッグ＆ドロップでアップロード
- アップロード後すぐに共有URLを生成
- 元のファイル名を保持（一覧で表示）
- アップロード日時で時系列ソート（最新が上）
- 複数ファイルの一括アップロード対応
- 認証情報のローカル保存（次回自動ログイン）

## セットアップ

### 1. GitHub Personal Access Token を取得

1. GitHubにログイン
2. 右上アイコン → **Settings**
3. 左メニュー最下部 → **Developer settings**
4. **Personal access tokens** → **Tokens (classic)**
5. **Generate new token (classic)**
6. Note に「PDF Uploader」と入力
7. Expiration を設定（90 days推奨）
8. Scopes で **repo** にチェック
9. **Generate token** → トークンをコピー

### 2. アプリにログイン

1. https://syd-app.github.io/docs/ を開く
2. GitHub Username、Personal Access Token、Repository Name を入力
3. 「接続する」をクリック

## 使い方

1. ログイン後の画面でPDFをドラッグ＆ドロップ（または選択）
2. 「アップロード」ボタンをクリック
3. 生成されたURLをコピーして共有

## 内部仕様

- **保存先**: GitHubリポジトリのルート直下（例: `https://username.github.io/repo/xxxxxxxx.pdf`）
- **ファイル名**: 8文字のランダム英数字に自動リネーム
- **元のファイル名と日時**: `manifest.json` に記録（元の名前とアップロード時刻の対応表）
- **ファイル一覧取得**: Git Trees API（1回のAPIコールで全PDFを取得・10万件まで対応）

## セキュリティ上の注意

- Personal Access Token は **repo 権限** を持つため、第三者に漏らさないこと
- ブラウザのlocalStorageに保存する場合は、共有PCで使わないこと
- 公開リポジトリにアップロードしたPDFは誰でもURLを知っていれば閲覧可能

## 技術スタック

- フロントエンド: Vanilla JavaScript（フレームワーク不使用）
- ホスティング: GitHub Pages
- ストレージ: GitHub Contents API
