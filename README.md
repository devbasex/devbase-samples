# devbase-samples

[devbase](https://github.com/devbasex/devbase) のサンプルプラグインレジストリです。初めてdevbaseを使うユーザーがすぐに試せるよう、汎用的な公開ツールを収録しています。

## 収録プラグイン

| プラグイン | 説明 | コンテナ | GIT_USER/GIT_REPO |
|-----------|------|---------|-------------------|
| `adminer` | 軽量DB管理ツール | `php` | `vrana/adminer` |
| `ai-plugins` | Claude Codeプラグインマーケットプレイス開発環境 | `general` | `devbasex/ai-plugins` |
| `devbase` | devbase本体の開発環境 | `general` | `devbasex/devbase` |

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

## リポジトリ構成

```
devbase-samples/
├── registry.yml            # レジストリ定義（プラグイン一覧）
├── adminer/
│   ├── plugin.yml          # プラグインメタ情報
│   └── projects/
│       └── adminer/
│           ├── compose.yml
│           └── env
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
