# keyhint
キーボードショートカットサービスの個人開発

# KeyHint 開発環境構築手順

## 1. プロジェクトディレクトリの作成(不要)

```bash
mkdir -p ~/privateDev/keyhint
cd ~/privateDev/keyhint
```

## 2. Git リポジトリの初期化

GitHub などでリモートリポジトリを作成し、以下を実行。

```bash
git init
# 例: git remote add origin https://github.com/yourname/keyhint.git
git remote add origin https://github.com/Shu-Anzai/keyhint.git
```

## 3. 必要なフォルダ構成の作成(不要)

```bash
mkdir -p frontend
mkdir -p docker/{minio,localstack,aws-ses-v2-local}
mkdir -p db/initdb.d/inital_data
```

## 4. docker-compose.yml の作成(不要)

`docker-compose.yml` ファイルをプロジェクト直下に作成し、サービス（db, phpmyadmin, frontend など）を定義。
※ `frontend` の volumes マウント先は `./frontend:/app` に設定すること。

## 5. Vue プロジェクトの初期化（frontend ディレクトリ内）

```bash
cd frontend
npm create vue@latest .
# TypeScript: Yes
# JSX support: No
# Vue Router: Yes/No（任意）
# Pinia: Yes/No（任意）
# ESLint, Prettier: Yes（推奨）
# Oxlint: No（安定性優先）
```

## 6. Docker コンテナの起動

プロジェクトルートに戻って以下を実行。

```bash
cd ~/privateDev/keyhint
docker compose up -d
```

## 7. フロントエンドの確認

ブラウザで以下にアクセス：

```
http://localhost:5173
```

## 8. Git コミット & Push

```bash
git add .
git commit -m "initial commit"
git push -u origin main  # またはブランチ名
```

## 9. 補足

* `frontend/package.json` が存在しないと `npm run dev` が失敗する。
* docker の `volumes` 設定ミス（例: `./keyhint:/app`）に注意。正しくは `./frontend:/app`。
* `aws-ses-v2-local` や `localstack` は今回のプロジェクトでは未使用であれば `docker-compose.yml` から削除して OK。
