---
inclusion: always
---

# Flutter コーディング規約・ベストプラクティス

## 全般

- **Dart の公式スタイルガイド**に従う (`dart format` でフォーマット、`flutter analyze` でチェック)
- `analysis_options.yaml` で `flutter_lints` (または `very_good_analysis`) を有効にする
- ファイルの先頭に不要な `import` を残さない
- `print()` の代わりに適切なロギングライブラリを使用する
- `// TODO:` コメントはチケット番号を添える (例: `// TODO(#123): 後で修正`)

## Widget 設計

- **1 ファイル 1 クラス** を基本とする (小さなプライベート Widget は同ファイル可)
- `StatelessWidget` を優先し、状態が必要な場合のみ `StatefulWidget` / 状態管理ライブラリを使う
- Widget は小さく保ち、**単一責任の原則** に従う
- `const` コンストラクタを積極的に使用してリビルドを最小化する
- `BuildContext` をコールバック外や非同期処理をまたいで使用しない (`mounted` チェック必須)

```dart
// Good
onPressed: () async {
  await doSomething();
  if (!mounted) return;  // 非同期後は mounted を確認
  Navigator.of(context).pop();
},
```

## 状態管理

- **ビジネスロジックを Widget から分離する**
- UI 層では状態管理ライブラリ (Riverpod 等) のプロバイダー/ブロック経由でのみ状態を変更する
- グローバル変数・シングルトンの乱用を避ける

## 非同期処理

- `Future` / `Stream` を適切に処理し、エラーハンドリングを忘れない
- `unawaited()` が必要な場合は明示的に記述する
- `async`/`await` を優先し、`.then()` チェーンの過度な使用を避ける

## テスト

- **ユニットテスト**: ビジネスロジック・Repository・ViewModel / Provider を対象とする
- **ウィジェットテスト**: 個々の Widget の表示・インタラクションを対象とする
- **インテグレーションテスト**: 主要なユーザーフローをカバーする
- テストは `flutter test` で実行できるように保つ
- モックには `mockito` または `mocktail` を使用する

```dart
// テストファイルの命名: <対象ファイル名>_test.dart
// 例: user_repository_test.dart
```

## Flutter MCP の活用方法

AI アシスタントに以下のような指示を出すことで、MCP ツールが自動的に活用されます:

| やりたいこと | 指示の例 |
|-------------|---------|
| エラーを修正したい | 「静的解析のエラーを確認して修正してください」 |
| テストを実行したい | 「テストを実行して結果を確認してください」 |
| パッケージを探したい | 「HTTP クライアントに適したパッケージを探してください」 |
| レイアウトを確認したい | 「実行中アプリの Widget ツリーを確認してレイアウトの問題を修正してください」 |
| ランタイムエラーを確認 | 「現在発生しているランタイムエラーを確認して修正してください」 |
| フォーマットしたい | 「このファイルをフォーマットしてください」 |

## pubspec.yaml 管理

- 依存関係のバージョンは原則として **キャレット記法** (`^`) で指定する
- 不要なパッケージはこまめに削除する (`flutter pub remove`)
- `dev_dependencies` と `dependencies` を正しく使い分ける

## analysis_options.yaml

```yaml
include: package:flutter_lints/flutter.yaml

linter:
  rules:
    # 推奨ルール
    - prefer_const_constructors
    - prefer_const_literals_to_create_immutables
    - avoid_print
    - use_build_context_synchronously
```

## コミット規約

Conventional Commits に従う:

```
feat: 新機能の追加
fix: バグ修正
docs: ドキュメントの変更
style: フォーマット等の変更 (コードの動作に影響なし)
refactor: リファクタリング
test: テストの追加・修正
chore: ビルドプロセス・補助ツールの変更
```
