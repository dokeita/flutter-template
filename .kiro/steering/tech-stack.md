---
inclusion: always
---

# 技術スタック

## フレームワーク・言語

| 種別 | 技術 | 備考 |
|------|------|------|
| フレームワーク | Flutter | 最新安定版 (stable channel) |
| 言語 | Dart | Flutter に付属のバージョン |
| IDE | Kiro | Flutter/Dart 拡張機能 + Flutter MCP |

## Flutter MCP サーバー

このプロジェクトでは **Dart & Flutter MCP サーバー** (`dart mcp-server`) を使用します。

MCP サーバーが提供する主要な機能:
- `analyze` - コードの静的解析・エラー修正
- `test` - テストの実行・結果確認
- `pub_dev_search` - pub.dev でのパッケージ検索
- `add_dependencies` / `remove_dependencies` - `pubspec.yaml` の依存関係管理
- `flutter_run` / `flutter_stop` / `hot_reload` / `hot_restart` - アプリの起動・制御
- `get_widget_tree` - 実行中アプリの Widget ツリー取得
- `get_runtime_errors` - ランタイムエラーの取得
- `format` - コードフォーマット

## 状態管理

> **注意**: プロジェクトで採用する状態管理ライブラリを選択・記載してください。

（例: Riverpod / Bloc / Provider / GetX）

## アーキテクチャ

> **注意**: プロジェクトで採用するアーキテクチャを記載してください。

（例: Clean Architecture / MVVM / Feature-First）

## 主要パッケージ

> **注意**: プロジェクトで使用するパッケージを記載してください。

| パッケージ | 用途 |
|------------|------|
| （例: `go_router`） | （例: ルーティング） |
| （例: `freezed`） | （例: データクラスの自動生成） |
| （例: `dio`） | （例: HTTP クライアント） |

## 開発ツール

| ツール | 用途 |
|--------|------|
| `flutter analyze` | 静的解析 |
| `flutter test` | テスト実行 |
| `dart format` | コードフォーマット |
| `flutter pub run build_runner` | コード生成 |

## CI/CD

> **注意**: 使用する CI/CD ツールを記載してください。

（例: GitHub Actions / Codemagic / Bitrise）

## バージョン管理

- Dart / Flutter のバージョンは `pubspec.yaml` の `environment` セクション、または `fvm` で管理する
- `pubspec.lock` はバージョン管理に含める
