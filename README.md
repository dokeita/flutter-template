# Flutter × Kiro テンプレート

Flutter アプリを **Kiro** で開発するためのテンプレートリポジトリです。
**Spec-Driven Development (スペック駆動開発)** と **Flutter MCP** を組み合わせた AI アシスト開発ワークフローを提供します。

## 特徴

- 🤖 **Flutter MCP サーバー対応** - Kiro が Flutter の静的解析・テスト・Widget ツリー確認・パッケージ検索を直接実行できる
- 📋 **Spec-Driven Development** - 実装前にスペック (要件・設計・タスク) を定義するワークフロー
- 🔄 **Agent Hooks** - ファイル保存時の自動解析・フォーマット・テスト更新
- 📝 **Steering ドキュメント** - プロダクト・技術スタック・コーディング規約を AI が常に参照
- 🧠 **Agent Skills** - 要件定義 → アーキテクチャ決定 → 設計・実装 を対話形式で推進する専用スキル

## 前提条件

| ツール | バージョン |
|--------|-----------|
| [Kiro IDE](https://kiro.dev/) | 最新版 |
| [Flutter](https://flutter.dev/) | stable チャンネル (3.x 以降) |
| Dart SDK | Flutter に付属 |

> Flutter MCP サーバーは `dart mcp-server` コマンドで起動します。Dart SDK 3.9 / Flutter 3.35 以降が必要です。

## セットアップ手順

### 1. リポジトリをテンプレートとして使用

```bash
# このリポジトリをクローン
git clone <this-repo-url> your-app-name
cd your-app-name

# git 履歴をリセット
rm -rf .git
git init
git add .
git commit -m "chore: initialize from flutter-kiro-template"
```

次に GitHub 上にリモートリポジトリを作成して push します。

**GitHub CLI を使う場合 (推奨)**

```bash
# リモートリポジトリを作成して push (gh コマンド)
gh repo create your-app-name --private --source=. --remote=origin --push
```

**GitHub CLI を使わない場合**

1. [github.com/new](https://github.com/new) でリポジトリを作成する（README の自動生成は **オフ** にする）
2. 表示された URL をリモートに登録して push する

```bash
# リモートを登録して push
git remote add origin https://github.com/<your-username>/your-app-name.git
git push -u origin main
```

### 2. Flutter プロジェクトの作成

```bash
# Flutter プロジェクトを作成 (このリポジトリのルートに作成する場合)
flutter create . --org com.yourcompany --project-name your_app_name

# または既存の Flutter プロジェクトに .kiro ディレクトリをコピー
cp -r /path/to/this-template/.kiro /path/to/your-flutter-project/
```

### 3. Kiro で開く

```bash
# Kiro でプロジェクトを開く
kiro .
```

### 4. ステアリングドキュメントのカスタマイズ

`.kiro/steering/` 配下のファイルをプロジェクトに合わせて更新してください:

| ファイル | 更新すべき内容 |
|---------|--------------|
| `product.md` | ターゲットプラットフォーム・ユーザー・主要機能 |
| `tech-stack.md` | 状態管理・アーキテクチャ・使用パッケージ |
| `structure.md` | プロジェクト固有のディレクトリ構造 |
| `flutter-best-practices.md` | チーム固有のコーディング規約 |

### 5. MCP サーバーの確認

Kiro のコマンドパレット (`Cmd+Shift+P` / `Ctrl+Shift+P`) で `MCP` を検索し、`dart-flutter` サーバーが接続されていることを確認してください。

## ディレクトリ構成

```
.kiro/
├── settings/
│   └── mcp.json                          # Flutter MCP 設定
├── steering/                             # AI が常に参照するガイドライン
│   ├── conventions.md                   # AI の振る舞い規約 (日本語応答など)
│   ├── development-workflow.md          # 3フェーズ開発ワークフロー定義
│   ├── product.md                        # プロダクト概要
│   ├── tech-stack.md                     # 技術スタック
│   ├── structure.md                      # プロジェクト構造
│   └── flutter-best-practices.md        # コーディング規約
├── skills/                               # Agent Skills (フェーズ別専門スキル)
│   ├── requirements-definition/
│   │   └── SKILL.md                     # 要件定義スキル
│   ├── architecture-decision/
│   │   └── SKILL.md                     # アーキテクチャ決定スキル
│   └── flutter-design-impl/
│       └── SKILL.md                     # 設計・実装スキル
├── hooks/                                # エージェントフック
│   ├── flutter-analyze-on-save.kiro.hook    # 保存時: 静的解析 (有効)
│   ├── format-on-save.kiro.hook             # 保存時: フォーマット (有効)
│   ├── update-tests-on-save.kiro.hook       # 保存時: テスト更新 (有効)
│   ├── check-runtime-errors.kiro.hook       # 手動: ランタイムエラー確認 (無効)
│   ├── run-tests.kiro.hook                  # 手動: テスト実行 (無効)
│   └── pubspec-check-on-change.kiro.hook   # pubspec 変更時: 依存確認 (無効)
└── specs/                                # スペック格納場所 (Skills が自動生成)
    └── <feature-name>/
        ├── requirements.md              # Phase 1: 要件定義
        ├── design.md                    # Phase 2: アーキテクチャ設計
        └── tasks.md                     # Phase 3: 実装タスクリスト
```

## 使い方

### 3 フェーズ開発ワークフロー (Agent Skills)

Kiro のチャットに話しかけるだけで、対応するスキルが自動起動してフェーズを推進します。

#### Phase 1: 要件定義

```
「ToDoリストアプリを作りたい」
「ユーザーが旅行の計画を管理できるアプリを作りたい」
```
→ `requirements-definition` スキルが起動し、ヒアリング形式で要件を整理して
　`.kiro/specs/<feature>/requirements.md` を生成します。

#### Phase 2: アーキテクチャ決定

```
「アーキテクチャを決めたい」
「技術選定をしてほしい」
（または Phase 1 完了後に「次へ進む」）
```
→ `architecture-decision` スキルが起動し、状態管理・ルーティング・パッケージを
　選択肢形式で提示して合意し、`design.md` と `tech-stack.md` を更新します。

#### Phase 3: 設計・実装

```
「実装を始めたい」
「コードを書いてほしい」
（または Phase 2 完了後に「次へ進む」）
```
→ `flutter-design-impl` スキルが起動し、タスク分解 → 実装 → MCP 検証の
　サイクルを回しながら `tasks.md` を消化していきます。

### 新機能の開発 (Kiro Spec パネルから)

1. **Kiro のスペックパネルから `+` を押す** か、チャットで `Spec` モードを選択する
2. 機能の概要を自然言語で説明する
3. Kiro が `requirements.md` → `design.md` → `tasks.md` の順に作成するのをレビューする
4. `tasks.md` のタスクを実行して実装を進める

### Flutter MCP を使った開発

Kiro のチャットで以下のように指示するだけで MCP ツールが自動的に使われます:

```
「静的解析のエラーを確認して修正してください」
→ MCP の analyze ツールが起動してエラーを取得・修正

「チャートを表示するのに適したパッケージを探してください」
→ MCP の pub_dev_search でパッケージを検索・追加

「実行中アプリのレイアウトエラーを修正してください」
→ get_runtime_errors + get_widget_tree でウィジェットツリーを診断・修正
```

### フックの有効化/無効化

`.kiro/hooks/*.kiro.hook` ファイルの `enabled` フィールドを変更するか、Kiro の Agent Hooks パネルで切り替えてください。

```json
{
  "enabled": true,  // ← true / false で切り替え
  "name": "..."
}
```

> **注意**: フックの変更を有効にするには Kiro の再起動またはプロジェクトの再オープンが必要です。

## Flutter MCP で使えるツール一覧

| ツール | 説明 |
|--------|------|
| `analyze` | 静的解析の実行 |
| `test` | テストの実行 |
| `pub_dev_search` | pub.dev でパッケージを検索 |
| `add_dependencies` | `pubspec.yaml` に依存関係を追加 |
| `remove_dependencies` | `pubspec.yaml` から依存関係を削除 |
| `flutter_run` | アプリを起動 |
| `flutter_stop` | アプリを停止 |
| `hot_reload` | ホットリロード |
| `hot_restart` | ホットリスタート |
| `get_widget_tree` | 実行中アプリの Widget ツリーを取得 |
| `get_runtime_errors` | ランタイムエラーを取得 |
| `format` | コードフォーマット |

詳細は [Flutter MCP 公式ドキュメント](https://docs.flutter.dev/ai/mcp-server) を参照してください。

## ライセンス

MIT
