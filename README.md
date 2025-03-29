# ⚡ clinerules

このリポジトリは、Cline を使ってコードレビューやインフラ設計の支援を自動化・効率化する開発環境テンプレートです。

Cline は強力な LLM プロンプトルールとタスクランナーを備えた CLI ツールで、さまざまな AI プロバイダ（OpenAI, Azure OpenAI, Anthropic など）を自由に切り替えて活用できます。

## ✅ セットアップ手順

### 1. Cline のインストール

```bash
npm install -g cline
# または
brew install clinehq/cline/cline
```

### 2. 環境変数を `.env` に設定

```env
AZURE_OPENAI_RESOURCE=your-azure-openai-resource-name
AZURE_OPENAI_API_KEY=your-api-key
```

> `.env` は `.gitignore` で除外されており、個人設定を安全に管理できます。


### 3. `direnv` の導入と設定（推奨）

```bash
# macOS の場合
brew install direnv

direnv allow
```

`.envrc` の内容：
```bash
export $(cat .env | xargs)
```


### 4. Cline の動作確認

```bash
cline ask "このファイルの目的は？"
cline run path/to/file.go
cline run
```


## 📁 ディレクトリ構成

```
your-project/
├── .clinerules             # プロンプトとルールの定義（言語ごとに最適化）
├── .clineconfig.yaml       # 使用するプロバイダ・モデルの設定
├── .env                    # 認証キーなどの環境変数
├── .envrc                  # direnv 対応ファイル
├── .gitignore              # 機密ファイルの除外
└── README.md               # このファイル
```


## 🧠 Cline 活用のポイント

- 言語ごとのベストプラクティスに基づくアドバイス
- ファイルごとに異なる LLM モデル・プロファイルを設定可能
- `ask`, `run`, `write`, `generate`, `explain` など豊富なコマンド群
- タスクの自動化やドキュメント生成にも応用可能


## 🔌 プロバイダ設定例（`.clineconfig.yaml`）

```yaml
default_provider: azure

providers:
  azure:
    api_base: https://${AZURE_OPENAI_RESOURCE}.openai.azure.com/
    api_key: ${AZURE_OPENAI_API_KEY}
    api_version: 2024-02-15-preview
    deployments:
      gpt4o:
        model: gpt-4o
      o3mini:
        model: gpt-3.5-turbo

  openai:
    api_key: ${OPENAI_API_KEY}
    deployments:
      gpt4o:
        model: gpt-4o
      o3mini:
        model: gpt-3.5-turbo

  anthropic:
    api_key: ${ANTHROPIC_API_KEY}
    deployments:
      claude:
        model: claude-3-sonnet
```

> 必要に応じてプロバイダを増減可能です。


## 🔗 参考リンク

- [Cline 公式ドキュメント](https://docs.cline.dev/)
- [direnv 公式サイト](https://direnv.net/)
- [Azure OpenAI Service](https://learn.microsoft.com/ja-jp/azure/ai-services/openai/)
- [OpenAI API リファレンス](https://platform.openai.com/docs/)
- [Anthropic Claude API](https://docs.anthropic.com/claude)
