# 職場コミュニケーション練習アプリ

このアプリケーションは、職場でのコミュニケーションスキルを安全に練習できる環境を提供します。AIとの対話を通じて、実際の職場で役立つコミュニケーション能力の向上を支援します。

## 🌟 主な機能

### 1. シナリオロールプレイ
- 30種類以上の実践的な職場シナリオを収録
- シナリオの難易度別分類（初級〜上級）
- AIと対話形式でリアルな状況を練習
- 会話終了後に詳細なフィードバックを取得
- 練習履歴の記録と振り返り

### 2. 雑談練習モード
- 職場での適切な雑談スキルを向上
- 相手（同僚・先輩・上司など）や状況に応じた会話練習
- 会話スキルに関する具体的なフィードバック
- 実践的なアドバイスの提供

### 3. 会話観戦モード
- 2つのAIモデル間の会話をリアルタイムで観察
- 会話の進行をステップバイステップで確認
- 自然な会話の流れと職場での適切なコミュニケーションを学習
- 異なるAIモデルの組み合わせで多様な会話パターンを観察

### 4. 学習記録・分析機能
- 練習した会話の履歴を保存
- シナリオごとの進捗状況を記録
- 練習時間の自動計測
- 学習の振り返りと改善点の分析

## 🧠 対応AIモデル

### クラウドAIモデル
- **OpenAI**
  - GPT-4
  - GPT-4-turbo
  - GPT-4o-mini
  - GPT-3.5-turbo
- **Google Gemini**
  - Gemini-1.5-pro
  - Gemini-1.5-flash

### ローカルAIモデル (Ollama経由)
- Llama2
- その他Ollamaでサポートされているモデル

## 💻 動作環境

- Python 3.8以上
- Flask 2.0以上
- インターネット接続（クラウドAIモデル使用時）
- [Ollama](https://ollama.ai/)（ローカルモデル使用時）

## 🚀 セットアップ

1. リポジトリのクローン
```bash
git clone https://github.com/CaCC-Lab/roleplay-chatbot-wepapp.git
cd roleplay-chatbot-wepapp
```

2. 仮想環境の作成と有効化
```bash
python -m venv venv
source venv/bin/activate  # Unix系
venv\Scripts\activate     # Windows
```

3. 依存パッケージのインストール
```bash
pip install -r requirements.txt
```

4. 環境変数の設定
```bash
cp .env.example .env
# .envファイルを編集してAPIキーを設定
```

5. アプリケーションの起動
```bash
python roleplay-chatbot-wepapp-main.py
```

6. ブラウザで以下のURLにアクセス
```
http://localhost:5001
```

## 📝 環境変数の設定例

```
# 基本設定
FLASK_SECRET_KEY=your_secret_key_here
OPENAI_API_KEY=sk-...  # OpenAI APIキー（オプション）
GOOGLE_API_KEY=AI...   # Google APIキー（オプション）

# セッション設定
SESSION_TYPE=filesystem
# SESSION_FILE_DIR=./flask_session  # セッションファイルの保存場所（オプション）

# Redisセッション（オプション、高負荷環境向け）
# SESSION_TYPE=redis
# REDIS_HOST=localhost
# REDIS_PORT=6379
# REDIS_PASSWORD=your_password
# REDIS_DB=0
```

## 🔧 ローカルLLM（Ollama）のセットアップ

1. [Ollama](https://ollama.ai/)をインストール
2. Ollamaサーバーを起動
```bash
ollama serve
```
3. 使用したいモデルをダウンロード（例：Llama2）
```bash
ollama pull llama2
```

## 📚 機能詳細

### シナリオロールプレイ機能
- 初級：基本的なコミュニケーションスキル向け
- 中級：より複雑な状況や対人関係向け
- 上級：難しい交渉や緊張状況向け

### フィードバック機能
- 話し方の適切さの評価
- 質問や確認の的確さの分析
- 改善点の具体的な提案
- 次回練習時の注目ポイント提示

### マルチモデル対応
- APIキーが設定されていない場合は自動的にローカルモデルにフォールバック
- 複数のAIプロバイダー間でのシームレスな切り替え
- 各モデルの特性を活かした会話練習

## 🛠 開発者向け情報

### ディレクトリ構成
```
/
├── static/                       # 静的ファイル
│   ├── css/                      # CSSファイル
│   └── js/                       # JavaScriptファイル
│       ├── chat.js               # 雑談モード用JS
│       ├── journal.js            # 学習記録用JS
│       ├── model-selection.js    # モデル選択用JS
│       ├── scenario.js           # シナリオモード用JS
│       ├── scenarios_list.js     # シナリオ一覧用JS
│       └── watch.js              # 観戦モード用JS
├── templates/                    # Flaskテンプレート
│   ├── chat.html                 # 雑談モードページ
│   ├── index.html                # トップページ
│   ├── journal.html              # 学習記録ページ
│   ├── scenario.html             # シナリオページ
│   ├── scenarios_list.html       # シナリオ一覧ページ
│   └── watch.html                # 観戦モードページ
├── scenarios/                    # シナリオ関連
│   ├── __init__.py               # シナリオロード処理
│   └── data/                     # シナリオデータ（YAMLファイル）
├── flask_session/                # セッションデータ保存場所
├── roleplay-chatbot-wepapp-main.py # メインアプリケーション
├── requirements.txt              # 依存パッケージ
├── requirements-dev.txt          # 開発用依存パッケージ
└── azure-webapp-settings.md      # Azureデプロイガイド
```

### 開発用依存パッケージ
```bash
pip install -r requirements-dev.txt
```

以下の開発ツールが導入されます：
- pytest: テスト実行
- black: コードフォーマッタ
- flake8: リンター
- isort: インポート順整理
- mypy: 型チェッカー

### シナリオの追加方法
1. `scenarios/data/` ディレクトリに新しいYAMLファイルを作成（例：`scenarioXX.yaml`）
2. 以下の形式でシナリオ情報を記述：
```yaml
title: シナリオのタイトル
description: シナリオの詳細説明
difficulty: 初級/中級/上級
tags:
  - タグ1
  - タグ2
role_info: AIは〇〇役、あなたは××
character_setting:
  personality: キャラクターの性格
  speaking_style: 話し方の特徴
  situation: 現在の状況
  initial_approach: 最初の声かけ
learning_points:
  - 学習ポイント1
  - 学習ポイント2
feedback_points:
  - フィードバックの観点1
  - フィードバックの観点2
```

## 🚀 Azureへのデプロイ

Azure Web Appへのデプロイ方法については、`azure-webapp-settings.md`を参照してください。主な設定内容：

1. 必要な環境変数の設定
2. セッションの保存方法（ファイルシステムまたはRedis）
3. アプリケーション設定の構成方法

## 🔒 プライバシーとセキュリティ

- OpenAI/Google APIを使用する場合、会話データは各サービスに送信されます
- ローカルLLM（Ollama）使用時は、すべてのデータがローカルで処理されます
- セッションデータは一時的にサーバーに保存され、セッション終了後に自動削除されます
- APIキーは環境変数で管理し、ソースコードには含まれません

## 📄 ライセンス

[MITライセンス](LICENSE)

## 📝 注意事項

- このアプリケーションは学習・練習用途を想定しています
- AIの応答は参考程度にお考えください
- 実際の職場での行動指針は、所属組織の方針に従ってください
- セキュリティの観点から、本番環境では適切なセッション管理（Redis推奨）を行ってください

## 🔒 セッション設定

アプリケーションはデフォルトでローカルファイルシステムにセッションデータを保存します。環境変数で設定を変更できます：

### ファイルシステムセッション（デフォルト）
```
SESSION_TYPE=filesystem
SESSION_FILE_DIR=/path/to/session/files  # オプション
```

### Redisセッション（スケーラブルな環境向け）
```
SESSION_TYPE=redis
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=your_password  # 必要な場合
REDIS_DB=0
```

## Azure Web Appへのデプロイ

Azure Web Appにデプロイする場合は、`azure-webapp-settings.md`を参照してください。

