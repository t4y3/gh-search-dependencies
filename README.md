# gh-search-dependencies

GitHub組織内のリポジトリで特定のnpmパッケージの使用状況を検索するツールです。

## 概要

このツールは、GitHub Code Search APIを使用して、指定された組織（またはユーザー）のリポジトリ内のpackage.jsonファイルを検索し、特定のパッケージとそのバージョンを見つけます。

## インストール

```bash
gh extension install t4y3/gh-search-dependencies
```

## 前提条件

- `gh` (GitHub CLI) がインストールされていること
- `jq` がインストールされていること
- GitHub CLIで認証済みであること (`gh auth login`)

## 使用方法

```bash
# 基本的な使用方法（現在のリポジトリのownerで検索）
gh-search-dependencies PACKAGE_NAME

# 特定の組織/ユーザーで検索
gh-search-dependencies PACKAGE_NAME OWNER

# 進捗表示付き
gh-search-dependencies --progress PACKAGE_NAME

# 並列リクエスト数を指定
gh-search-dependencies --parallel 20 PACKAGE_NAME
```

## オプション

- `--progress`: 検索中の進捗を表示
- `--parallel N`: 並列リクエストの最大数を設定（デフォルト: 10）
- `-h, --help`: ヘルプメッセージを表示

## 環境変数

- `GH_SEARCH_MAX_PARALLEL`: デフォルトの並列リクエスト数を設定

## 出力形式

CSV形式で以下の情報を出力します：

```csv
repository,path,version
owner/repo1,package.json,1.0.0
owner/repo2,src/package.json,2.1.3
```

## 使用例

```bash
# reactパッケージを現在のリポジトリのownerで検索
gh-search-dependencies react

# my-org組織内でexpressパッケージを検索
gh-search-dependencies express my-org

# 進捗表示付きでtypescriptを検索
gh-search-dependencies --progress typescript

# CSVファイルに保存
gh-search-dependencies react > dependencies.csv
```

## 注意事項

- GitHub API のレート制限に注意してください
- 大規模な組織では検索に時間がかかる場合があります
- プライベートリポジトリへのアクセスには適切な権限が必要です