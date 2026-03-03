# リポジトリ構造 (Repository Structure)

## ディレクトリ構造

```
multi-agent-book/
├── CLAUDE.md                          # プロジェクトメモリ（執筆ルール・設定）
├── docs/                              # 永続ドキュメント（書籍の「北極星」）
│   ├── ideas/                         # 壁打ち・ブレインストーミング成果物
│   │   ├── book-concept.md            # 書籍コンセプト（/setup-bookの入力）
│   │   └── spec-driven-design.md      # スペック駆動開発の設計書
│   ├── book-plan.md                   # 書籍企画書（対象読者、到達目標、全体構成）
│   ├── book-architecture.md           # 書籍構成・章間依存関係図
│   ├── writing-guidelines.md          # 執筆ガイドライン（文体・表記・図表ルール）
│   ├── glossary.md                    # 用語集（日英対応、表記統一）
│   ├── repository-structure.md        # 本ファイル
│   ├── figure-list.md                 # 図表一覧（全章横断）
│   ├── chapter-specs/                 # 各章の仕様書
│   │   ├── ch01-spec.md
│   │   ├── ch02-spec.md
│   │   ├── ...
│   │   └── ch15-spec.md
│   └── feedbacks/                     # 読了後のフィードバック
│       └── .gitkeep
├── manuscript/                        # 原稿本体
│   ├── ch01/
│   │   ├── ch01.md                    # 本文
│   │   └── figures/                   # 章内の図表ソース（Mermaidファイル等）
│   ├── ch02/
│   │   ├── ch02.md
│   │   └── figures/
│   ├── ...
│   ├── ch15/
│   │   ├── ch15.md
│   │   └── figures/
│   └── appendix/
│       ├── appendix-a.md
│       ├── appendix-b.md
│       ├── appendix-c.md
│       └── appendix-d.md
├── review/                            # レビュー結果
│   ├── consistency-check/             # 用語・表記の一貫性チェック
│   ├── cross-reference-check/         # 章間参照の整合性チェック
│   └── quality-check/                 # 内容品質チェック
├── .steering/                         # 作業単位のドキュメント
│   └── YYYYMMDD-chNN-section-name/
│       ├── requirements.md            # 今回の作業の要求内容
│       ├── design.md                  # 執筆アプローチ
│       └── tasklist.md                # タスクリスト
├── .claude/
│   ├── commands/                      # スラッシュコマンド
│   │   ├── setup-book.md              # 初回セットアップ
│   │   ├── write-chapter.md           # 章の執筆
│   │   ├── write-all.md               # 全章一括執筆
│   │   ├── review-chapter.md          # 章のレビュー
│   │   └── fix-feedback.md            # フィードバック修正
│   └── skills/                        # 執筆スキル
│       ├── book-planning/             # 書籍企画書作成
│       ├── chapter-spec-writing/      # 章仕様書作成
│       ├── chapter-writing/           # 章執筆
│       ├── writing-guidelines/        # 執筆ガイドライン
│       ├── glossary-creation/         # 用語集作成
│       ├── figure-design/             # 図表設計
│       ├── review/                    # レビュー
│       └── steering/                  # ステアリング管理
└── build/                             # ビルド成果物
    └── .gitkeep
```

## 各ディレクトリの役割

### `docs/` — 永続ドキュメント
書籍全体の「何を書くか」「どう書くか」を定義する設計書群。プロジェクトの「北極星」として機能する。頻繁には更新されない。

### `docs/ideas/` — 下書き・アイデア
壁打ちやブレインストーミングの成果物。`/setup-book` 実行時に入力として読み込まれる。

### `docs/chapter-specs/` — 章仕様書
各章の詳細設計。節構成、図表リスト、章間の接続方法を定義する。執筆時の参照先。

### `docs/feedbacks/` — フィードバック
読了後のフィードバックファイルを格納する。`/fix-feedback` で自動修正ワークフローを実行。

### `manuscript/` — 原稿本体
実際の書籍本文。各章は `chNN/` ディレクトリに分離し、本文（`chNN.md`）と図表ソース（`figures/`）を格納する。

### `review/` — レビュー結果
自動レビューの結果を格納する。用語統一、章間整合性、品質の3軸でチェック。

### `.steering/` — 作業単位のドキュメント
特定の執筆作業における計画・進捗を管理する。作業ごとに新規ディレクトリを作成し、履歴として保持する。

### `.claude/` — Claude Code設定
スラッシュコマンドとスキルの定義。執筆ワークフローの自動化を支える。

## ファイル命名規則

| 対象 | 形式 | 例 |
|------|------|-----|
| 章の原稿 | `chNN.md` | `ch04.md` |
| 章の仕様書 | `chNN-spec.md` | `ch04-spec.md` |
| ステアリングディレクトリ | `YYYYMMDD-chNN-section-name` | `20260305-ch04-coordination-patterns` |
| 図表ソース | 内容に基づく名前 | `orchestrator-architecture.mmd` |
| 付録 | `appendix-X.md` | `appendix-a.md` |
