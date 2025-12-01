# devin-practicw2 – OpenRouter Chat Demo（CDN 版 React）

## 概要

index.html をブラウザで直接開くだけで動作する AI チャットアプリです。React を CDN で読み込むためビルド不要で、右上の歯車アイコンから OpenRouter API キーを入力できます。API キーは sessionStorage に保存され、タブを閉じると自動的に削除されます。サーバーには送信されないため、安全に利用できます。

## 機能

- **AI チャット UI（ダークテーマ）**: ChatGPT 風のモダンなダークテーマ UI でチャットが可能
- **設定モーダルで API キー入力**: 右上の歯車アイコンをクリックして OpenRouter API キーを入力
- **sessionStorage による安全なキー管理**: API キーはブラウザの sessionStorage に保存され、タブを閉じると削除
- **OpenRouter API との通信処理**: openai/gpt-3.5-turbo モデルを使用した AI との対話
- **環境変数サポート**: `window.OPENROUTER_API_KEY` が設定されている場合は自動的に使用
- **アプリ内でのエラー処理**: 無効な API キーや API 制限エラーなどを適切に表示

## 動作方法

### 方法 1: ローカルサーバーを使用

```bash
cd /path/to/devin-practicw2
python3 -m http.server 8080
```

ブラウザで `http://localhost:8080/index.html` を開きます。

### 方法 2: 直接開く

`index.html` ファイルをブラウザで直接開いても動作します。

### 使い方

1. 右上の歯車アイコンをクリックして設定モーダルを開く
2. OpenRouter API キーを入力して「Save」をクリック
3. メッセージを入力して「Send」をクリック
4. AI からの返答を待つ

### 環境変数による API キー設定

デプロイ時に `window.OPENROUTER_API_KEY` をグローバル変数として設定することで、UI からの入力なしで API キーを使用できます。

```html
<script>
  window.OPENROUTER_API_KEY = 'your-openrouter-api-key';
</script>
```

## ファイル構成

```
devin-practicw2/
├── README.md      # このファイル
└── index.html     # アプリ本体（React + CSS + JavaScript）
```

## 開発環境（Devin 内部）

- **OS**: Ubuntu (Devin Box)
- **バージョン管理**: GitHub リポジトリとの連携
- **フレームワーク**: React 18（CDN 経由）
- **トランスパイラ**: Babel（CDN 経由、in-browser）

## 今後の改善案

- **UI の改善**: レスポンシブデザインの強化、アニメーションの追加
- **ログ保存機能**: チャット履歴の localStorage への保存・復元機能
- **SCSS 導入**: スタイルの管理を容易にするための SCSS 導入
- **モデル選択機能**: gpt-4 など他のモデルを選択できる機能
- **ストリーミング対応**: リアルタイムでの応答表示（Server-Sent Events）

## 変更履歴

### OpenRouter 対応（2025-12-01）

OpenAI API から OpenRouter API への移行を行いました。

**変更内容:**

| 項目 | 変更前 | 変更後 |
|------|--------|--------|
| API エンドポイント | `https://api.openai.com/v1/chat/completions` | `https://openrouter.ai/api/v1/chat/completions` |
| モデル名 | `gpt-3.5-turbo` | `openai/gpt-3.5-turbo` |
| sessionStorage キー | `openai_api_key` | `openrouter_api_key` |
| UI ラベル | OpenAI API Key | OpenRouter API Key |

**追加された HTTP ヘッダー:**

- `HTTP-Referer`: アプリの URL（`window.location.origin`）
- `X-Title`: `devin-practicw2 OpenRouter Chat Demo`

**新機能:**

- 環境変数 `window.OPENROUTER_API_KEY` による API キーの自動設定サポート

**修正ファイル:**

- `index.html`: API エンドポイント、ヘッダー、UI ラベル、sessionStorage キーの変更
- `README.md`: ドキュメントの更新

## ライセンス

このプロジェクトは自由に使用・改変できます。
