# リポジトリ構造 (Repository Structure)

## ディレクトリ構成

```
multi-agent-book/
├── CLAUDE.md                          # プロジェクトメモリ（執筆ルール・構造定義）
├── docs/                              # 永続ドキュメント（書籍の「北極星」）
│   ├── ideas/                         # 壁打ち・ブレインストーミング成果物
│   │   ├── book-concept.md            # 書籍コンセプト（/setup-bookの入力）
│   │   └── spec-driven-design.md      # スペック駆動開発の設計書
│   ├── book-plan.md                   # 書籍企画書
│   ├── book-architecture.md           # 書籍構成・章間依存関係
│   ├── writing-guidelines.md          # 執筆ガイドライン（文体・表記ルール）
│   ├── glossary.md                    # 用語集（日英対応、表記統一）
│   ├── repository-structure.md        # リポジトリ構造定義（本ファイル）
│   ├── figure-list.md                 # 図表一覧（全章横断）
│   ├── chapter-specs/                 # 各章の仕様書
│   │   ├── ch01-spec.md
│   │   ├── ch02-spec.md
│   │   ├── ...
│   │   └── ch15-spec.md
│   └── feedbacks/                     # レビューフィードバック
│       └── .gitkeep
├── manuscript/                        # 原稿本体
│   ├── ch01/
│   │   ├── ch01.md                    # 第1章 本文
│   │   └── figures/                   # 章内の図表ソース（Mermaidファイル等）
│   ├── ch02/
│   │   ├── ch02.md
│   │   └── figures/
│   ├── ...
│   ├── ch15/
│   │   ├── ch15.md
│   │   └── figures/
│   └── appendix/                      # 付録
│       ├── appendix-a.md
│       ├── appendix-b.md
│       ├── appendix-c.md
│       └── appendix-d.md
├── .steering/                         # 作業単位のドキュメント
│   └── YYYYMMDD-chNN-section-name/
│       ├── requirements.md            # 今回の作業の要求内容
│       ├── design.md                  # 執筆アプローチ
│       └── tasklist.md                # タスクリスト
├── .claude/                           # Claude Code設定
│   ├── commands/                      # スラッシュコマンド
│   │   ├── setup-book.md
│   │   ├── write-chapter.md
│   │   ├── review-chapter.md
│   │   └── fix-feedback.md
│   └── skills/                        # 執筆スキル
│       ├── book-planning/
│       ├── chapter-spec-writing/
│       ├── chapter-writing/
│       ├── writing-guidelines/
│       ├── glossary-creation/
│       ├── figure-design/
│       ├── review/
│       └── steering/
└── build/                             # ビルド成果物
    └── .gitkeep
```

## 各ディレクトリの役割

### `docs/` — 永続ドキュメント
書籍全体の「何を書くか」「どう書くか」を定義する。プロジェクトの「北極星」として、全ての執筆作業の基準となる。頻繁には更新されない。

### `docs/ideas/` — 下書き・アイデア
壁打ちやブレインストーミングの成果物を格納する。自由形式で構造化は最小限。`/setup-book` 実行時に自動的に読み込まれる。

### `docs/chapter-specs/` — 章仕様書
各章の詳細仕様を定義する。章の目的、前提知識、節構成、図表リスト、理解度チェック問題の方針を含む。

### `docs/feedbacks/` — フィードバック
読了後のフィードバック（わからなかった点、追記してほしい点）を格納する。`/fix-feedback` で自動修正ワークフローを実行する。

### `manuscript/` — 原稿本体
実際の書籍本文を格納する。各章ごとにディレクトリを分け、本文とfiguresディレクトリを持つ。

### `.steering/` — 作業単位のドキュメント
特定の執筆作業における計画・進捗を管理する。作業ごとに `YYYYMMDD-chNN-section-name/` 形式のディレクトリを作成する。履歴として保持する。

### `.claude/` — Claude Code設定
スラッシュコマンドとスキルの定義を格納する。

## ファイル命名規則

| 種類 | 命名規則 | 例 |
|------|---------|-----|
| 章の原稿 | `chNN.md` | `ch04.md` |
| 章の仕様書 | `chNN-spec.md` | `ch04-spec.md` |
| 図表ソース | `figX-Y.mmd` | `fig4-1.mmd` |
| ステアリング | `YYYYMMDD-chNN-section/` | `20260305-ch04-coordination-patterns/` |
| 付録 | `appendix-X.md` | `appendix-a.md` |
