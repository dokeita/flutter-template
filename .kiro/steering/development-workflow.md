---
inclusion: always
---

# 開発ワークフロー

## フェーズ構成

このプロジェクトでは以下の 3 フェーズで開発を進める。
**各フェーズを順番に完了させてから次へ進むこと。**

```
Phase 1: 要件定義
  → .kiro/specs/<feature>/requirements.md を生成
  → スキル: requirements-definition

Phase 2: アーキテクチャ決定
  → .kiro/specs/<feature>/design.md を生成
  → .kiro/steering/tech-stack.md を更新
  → スキル: architecture-decision

Phase 3: 設計・実装
  → .kiro/specs/<feature>/tasks.md を生成・消化
  → Flutter MCP を使って実装・検証
  → スキル: flutter-design-impl
```

## スキルの起動方法

各フェーズは専用のスキルが自動的に起動する。
ユーザーが以下のような発言をした際に **対応するスキルを自動的にロード**すること。

| ユーザーの発言例 | 起動するスキル |
|----------------|--------------|
| 「要件定義したい」「アプリを作りたい」 | `requirements-definition` |
| 「アーキテクチャを決めたい」「技術選定したい」 | `architecture-decision` |
| 「実装したい」「コードを書いてほしい」「設計して」 | `flutter-design-impl` |

## フェーズ間の連携ルール

- **前フェーズの成果物が存在しない場合は実行しない**  
  例: `requirements.md` がない状態で `architecture-decision` は起動しない

- **各フェーズの完了時に次フェーズへの案内を行う**  
  例: 要件定義完了後「アーキテクチャ決定フェーズに進みますか？」と聞く

- **前フェーズへの差し戻しを積極的に行う**  
  実装中に要件の曖昧さが判明した場合は実装を止めて要件定義に戻る

## スペックファイルの命名規則

```
.kiro/specs/
└── <feature-name>/          ← kebab-case で機能名
    ├── requirements.md      ← Phase 1 成果物
    ├── design.md            ← Phase 2 成果物
    └── tasks.md             ← Phase 3 成果物（チェックリスト）
```

`<feature-name>` は機能単位で作成する。アプリ全体の場合は `main-app` などとする。

## 意思決定の記録

各フェーズで行った重要な意思決定は必ずドキュメントに記録する。

- 要件の取捨選択 → `requirements.md` の「スコープ外」セクションに記載
- 技術選定の理由 → `design.md` の「主要な設計判断」セクションに記載
- 実装上の判断 → コードコメントまたは `tasks.md` の備考に記載

## 手戻りを防ぐためのチェックポイント

各フェーズ終了時にユーザーと以下を確認してから次へ進む:

### Phase 1 → Phase 2 チェック
- [ ] ターゲットユーザーは具体的に定義されているか
- [ ] スコープ外が明示されているか
- [ ] 受け入れ基準がテスト可能な形で書かれているか

### Phase 2 → Phase 3 チェック
- [ ] 全ての要件がアーキテクチャで実現可能か
- [ ] 採用パッケージのライセンスに問題がないか
- [ ] チームの技術力でそのアーキテクチャを扱えるか
