---
inclusion: always
---

# プロジェクト構造

## ディレクトリ構成

```
<project_root>/
├── .kiro/                        # Kiro 設定ディレクトリ
│   ├── settings/
│   │   └── mcp.json              # MCP サーバー設定 (Flutter MCP)
│   ├── steering/                 # ステアリングドキュメント (常に参照される)
│   │   ├── product.md            # プロダクト概要・目的
│   │   ├── tech-stack.md         # 技術スタック
│   │   ├── structure.md          # このファイル: プロジェクト構造
│   │   └── flutter-best-practices.md  # Flutter コーディング規約
│   ├── hooks/                    # エージェントフック (ファイル変更トリガーの自動化)
│   │   ├── flutter-analyze-on-save.kiro.hook   # 保存時に静的解析
│   │   ├── update-tests-on-save.kiro.hook      # 保存時にテスト更新
│   │   └── format-on-save.kiro.hook            # 保存時にフォーマット
│   └── specs/                    # スペック駆動開発のドキュメント
│       └── <feature-name>/
│           ├── requirements.md   # 要件定義
│           ├── design.md         # 設計
│           └── tasks.md          # タスクリスト
│
├── lib/                          # Flutter アプリ本体
│   ├── main.dart                 # エントリーポイント
│   ├── app.dart                  # アプリのルートウィジェット
│   ├── core/                     # アプリ全体で共通のコード
│   │   ├── constants/            # 定数
│   │   ├── theme/                # テーマ設定
│   │   ├── router/               # ルーティング
│   │   └── utils/                # ユーティリティ
│   └── features/                 # 機能単位のディレクトリ (Feature-First)
│       └── <feature_name>/
│           ├── data/             # データ層 (API・DB)
│           ├── domain/           # ドメイン層 (ビジネスロジック)
│           └── presentation/     # プレゼンテーション層 (UI)
│
├── test/                         # テストコード
│   ├── unit/                     # ユニットテスト
│   ├── widget/                   # ウィジェットテスト
│   └── integration_test/         # インテグレーションテスト
│
├── assets/                       # 静的アセット
│   ├── images/
│   ├── fonts/
│   └── translations/             # i18n (使用する場合)
│
├── pubspec.yaml                  # パッケージ依存関係
├── pubspec.lock                  # ロックファイル (バージョン管理に含める)
├── analysis_options.yaml         # 静的解析設定
└── README.md                     # プロジェクト説明
```

## 命名規則

| 対象 | 規則 | 例 |
|------|------|----|
| ファイル名 | `snake_case` | `user_profile_page.dart` |
| クラス名 | `PascalCase` | `UserProfilePage` |
| 変数・関数名 | `camelCase` | `getUserProfile()` |
| 定数 | `camelCase` (Dart 標準) | `kMaxRetryCount` または `maxRetryCount` |
| ディレクトリ名 | `snake_case` | `user_profile/` |

## スペックの格納場所

新機能の開発を始める前に、必ず `.kiro/specs/<feature-name>/` 以下にスペックファイルを作成してください。

```
.kiro/specs/
└── user-authentication/       # 機能名 (kebab-case)
    ├── requirements.md        # EARS 記法で要件を定義
    ├── design.md              # 技術的な設計・アーキテクチャ
    └── tasks.md               # 実装タスクのチェックリスト
```

## テストファイルの配置

テストファイルは `lib/` のディレクトリ構造を `test/` に反映させて配置します。

```
lib/features/auth/domain/auth_repository.dart
    ↓ 対応するテスト
test/unit/features/auth/domain/auth_repository_test.dart
```
