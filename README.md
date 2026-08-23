# devbase-samples

[devbase](https://github.com/devbasex/devbase) のサンプルプラグインレジストリです。初めてdevbaseを使うユーザーがすぐに試せるよう、汎用的な公開ツールを収録しています。

> **必要な devbase バージョン**: 3.0.0 以上。各プロジェクトの設定は `project.yml` 形式で書かれており、2.x では読み込めません。

## 収録プラグイン

| プラグイン | 説明 | コンテナ | リポジトリ (`repos[].owner/repo`) |
|-----------|------|---------|-----------------------------------|
| `adminer` | 軽量DB管理ツール | `php` | `vrana/adminer` |
| `ai-plugins` | Claude Code プラグインマーケットプレイス + devbase 本体（複数リポジトリ構成の例） | `general` | `devbasex/ai-plugins`, `devbasex/devbase` |
| `devbase` | devbase本体の開発環境 | `general` | `devbasex/devbase` |
| `github_work_time` | GitHubアクティビティから稼働時間を集計するツール | `general` | `takemi-ohama/github_work_time` |
| `md-specgen` | Markdown仕様書自動生成ツール | `general` | `takemi-ohama/md-specgen` |
| `tmllib` | 共通ライブラリ開発環境 | `general` | `takemi-ohama/tmllib` |

## 使い方

### 1. レジストリを登録

```bash
devbase plugin repo add https://github.com/devbasex/devbase-samples.git
```

GitHubショートハンドでも登録できます：

```bash
devbase plugin repo add devbasex/devbase-samples
```

### 2. プラグインをインストール

名前だけで指定可能：

```bash
devbase plugin install adminer
devbase plugin install ai-plugins
devbase plugin install devbase
```

全部まとめてインストール：

```bash
devbase plugin install devbasex/devbase-samples --all
```

### 3. プロジェクトを起動

```bash
cd ~/devbase/projects/adminer
devbase up
```

## プロジェクト設定 (`project.yml`)

devbase 3.0.0 から、プロジェクトの設定は `projects/<プロジェクト名>/project.yml` に書きます。1 プロジェクト = 1 コンテナ = **複数リポジトリ** という構成です。

収録プラグイン `adminer` の `projects/adminer/project.yml`:

```yaml
version: 1
scale: 1
open_editor: true
repos:
  - owner: vrana
    repo: adminer
```

`repos` に要素を足すだけで、1 つのプロジェクト（＝1 コンテナ）に複数のリポジトリを並べられます。

```yaml
version: 1
defaults:
  owner: devbasex
repos:
  - repo: my-app        # 先頭が primary（ログイン直後の作業ディレクトリ）
  - repo: my-app-docs
```

| 設定 | 意味 |
|------|------|
| `repos[].owner` / `repos[].repo` | クローンする GitHub リポジトリ。先頭の要素が primary |
| `defaults` | `repos[]` の各要素へ継承させる既定値（`host` / `owner` / `branch` / `init`） |
| `work_dir` | コンテナ内の作業ディレクトリ（既定値と同じなら省略可） |
| `scale` | 起動するコンテナ数 |
| `open_editor` | `devbase up` 後にエディタを開くか |

スキーマの詳細は [project.yml リファレンス](https://github.com/devbasex/devbase/blob/main/docs/user/project-yml.md) を参照してください。

同じディレクトリの `env` は「**コンテナへ渡す環境変数**」だけを持ちます。`GIT_USER` / `GIT_REPO` / `CONTAINER_SCALE` / `DEVBASE_OPEN_EDITOR` といった devbase 自身の設定は `project.yml` へ移動しました。

## リポジトリ構成

```
devbase-samples/
├── registry.yml            # レジストリ定義（プラグイン一覧）
├── adminer/
│   ├── plugin.yml          # プラグインメタ情報
│   └── projects/
│       └── adminer/
│           ├── compose.yml
│           ├── project.yml # プロジェクト設定（リポジトリ・scale・エディタ）
│           └── env         # コンテナへ渡す環境変数
├── ai-plugins/
│   └── ...
└── devbase/
    └── ...
```

## 独自プラグインの追加

独自のプラグインレジストリを作成する手順は [devbase Plugin開発ガイド](https://github.com/devbasex/devbase/blob/main/docs/plugin-dev/quickstart.md) を参照してください。

## Issue / Contribution

新しいサンプルプラグインの追加提案やバグ報告は [Issues](https://github.com/devbasex/devbase-samples/issues) へ。

## License

MIT License. Copyright 2026 takemi-ohama.
