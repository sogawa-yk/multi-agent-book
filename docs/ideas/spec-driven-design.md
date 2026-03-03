# 書籍執筆用スペック駆動開発 ― 設計書

## 概要

Galleyリポジトリのスペック駆動開発の仕組みを書籍執筆に適用する。
ソフトウェア開発のパターンを執筆プロセスにマッピングし、
Claude Codeが章単位で自律的に執筆・レビュー・修正できる仕組みを構築する。

---

## Galleyとのマッピング

| Galley（ソフトウェア開発） | 書籍執筆版 |
|--------------------------|-----------|
| `CLAUDE.md` | `CLAUDE.md`（プロジェクトメモリ＋執筆ルール） |
| `docs/product-requirements.md` | `docs/book-plan.md`（書籍企画書） |
| `docs/functional-design.md` | `docs/chapter-specs/`（各章の仕様書） |
| `docs/architecture.md` | `docs/book-architecture.md`（書籍構成・依存関係） |
| `docs/glossary.md` | `docs/glossary.md`（用語集） |
| `docs/development-guidelines.md` | `docs/writing-guidelines.md`（執筆ガイドライン） |
| `docs/repository-structure.md` | `docs/repository-structure.md`（リポジトリ構造） |
| `.steering/YYYYMMDD-task/` | `.steering/YYYYMMDD-chNN-section/`（執筆作業単位） |
| `src/` | `manuscript/`（原稿本体） |
| `tests/` | `review/`（レビュー結果） |
| `.claude/commands/` | `.claude/commands/`（執筆用コマンド） |
| `.claude/skills/` | `.claude/skills/`（執筆用スキル） |

---

## ディレクトリ構造

```
book-multiagent-oci/
├── CLAUDE.md                          # プロジェクトメモリ
├── docs/                              # 永続ドキュメント（書籍の「北極星」）
│   ├── ideas/                         # 壁打ち・ブレインストーミング成果物
│   │   └── book-concept.md            # 書籍コンセプト（/setup-bookの入力）
│   ├── book-plan.md                   # 書籍企画書（≒PRD）
│   ├── book-architecture.md           # 書籍構成・章間依存関係
│   ├── writing-guidelines.md          # 執筆ガイドライン（文体・表記ルール）
│   ├── glossary.md                    # 用語集（日英対応、表記統一）
│   ├── repository-structure.md        # リポジトリ構造定義
│   ├── chapter-specs/                 # 各章の仕様書
│   │   ├── ch01-spec.md
│   │   ├── ch02-spec.md
│   │   ├── ...
│   │   └── ch15-spec.md
│   ├── figure-list.md                 # 図表一覧（全章横断）
│   └── feedbacks/                     # レビューフィードバック
│       └── .gitkeep
├── manuscript/                        # 原稿本体（≒src/）
│   ├── ch01/
│   │   ├── ch01.md                    # 本文
│   │   └── figures/                   # 章内の図表ソース
│   ├── ch02/
│   │   ├── ch02.md
│   │   └── figures/
│   ├── ...
│   └── appendix/
│       ├── appendix-a.md
│       └── appendix-b.md
├── review/                            # レビュー結果（≒tests/）
│   ├── consistency-check/             # 用語・表記の一貫性チェック
│   ├── cross-reference-check/         # 章間参照の整合性チェック
│   └── quality-check/                 # 内容品質チェック
├── .steering/                         # 作業単位のドキュメント
│   └── YYYYMMDD-chNN-section-name/
│       ├── requirements.md
│       ├── design.md
│       └── tasklist.md
├── .claude/
│   ├── commands/                      # スラッシュコマンド
│   │   ├── setup-book.md              # 初回セットアップ
│   │   ├── write-chapter.md           # 章の執筆
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
│       └── steering/                  # ステアリング管理（Galley流用）
└── build/                             # ビルド成果物
    └── .gitkeep
```

---

## CLAUDE.md（案）

```markdown
# プロジェクトメモリ

## プロジェクト概要

本プロジェクトは「AIエージェント開発入門 ― シングルからマルチへ」の執筆プロジェクトである。
Claude Codeによるスペック駆動開発で書籍を執筆する。

## スペック駆動開発の基本原則

### 基本フロー

1. **ドキュメント作成**: 永続ドキュメント(`docs/`)で「何を書くか」を定義
2. **作業計画**: ステアリングファイル(`.steering/`)で「今回何を書くか」を計画
3. **執筆**: tasklist.mdに従って執筆し、進捗を随時更新
4. **レビュー**: 品質チェック（用語統一、章間整合性、技術正確性）
5. **更新**: 必要に応じてドキュメント更新

### 重要なルール

#### 執筆前の確認

新しい章・節の執筆を始める前に、必ず以下を確認:

1. CLAUDE.mdを読む
2. `docs/book-plan.md`で書籍全体の方向性を確認
3. `docs/chapter-specs/chNN-spec.md`で該当章の仕様を確認
4. `docs/writing-guidelines.md`で文体・表記ルールを確認
5. `docs/glossary.md`で用語の統一基準を確認
6. 前後の章の原稿を読み、文脈の連続性を確認

#### ステアリングファイル管理

作業ごとに `.steering/[YYYYMMDD]-ch[NN]-[セクション名]/` を作成:

- `requirements.md`: 今回の執筆内容（どの節を書くか、含めるべきトピック）
- `design.md`: 執筆アプローチ（構成、図表計画、前後の章との接続方法）
- `tasklist.md`: 具体的なタスクリスト

#### ステアリングファイルの管理

**作業計画・執筆・レビュー時は`steering`スキルを使用してください。**

## ディレクトリ構造

### 永続的ドキュメント(`docs/`)

書籍全体の「何を書くか」「どう書くか」を定義:

#### 下書き・アイデア（`docs/ideas/`）
- 壁打ち・ブレインストーミングの成果物
- 書籍コンセプト、章構成案のメモ
- 自由形式（構造化は最小限）
- `/setup-book`実行時に自動的に読み込まれる

#### 正式版ドキュメント
- **book-plan.md** - 書籍企画書（対象読者、到達目標、全体構成）
- **book-architecture.md** - 書籍構成・章間依存関係図
- **writing-guidelines.md** - 執筆ガイドライン（文体、表記、図表ルール）
- **glossary.md** - 用語集（日英対応、表記統一）
- **chapter-specs/** - 各章の仕様書
- **figure-list.md** - 図表一覧
- **repository-structure.md** - リポジトリ構造

### 原稿（`manuscript/`）

実際の書籍本文:

- `chNN/chNN.md` - 各章の本文
- `chNN/figures/` - 章内の図表

### 作業単位のドキュメント(`.steering/`)

特定の執筆作業における「今回何を書くか」を定義

## 執筆プロセス

### 初回セットアップ

1. `/setup-book` で永続的ドキュメント作成
2. `/write-chapter [章番号]` で章の執筆開始

### 日常的な使い方

```bash
# 章の執筆
> /write-chapter 4

# 章のレビュー
> /review-chapter 4

# フィードバック修正
> /fix-feedback 2026-03-05-ch04-review.md

# 自由な編集
> ch04の4.3節を見直して、並列パターンの例をOKEの例に変更して
```

## 執筆ルール

### 文体

- 常体（である調）
- 技術用語は初出時に日本語（英語）の形式で記載
- 読者への語りかけは最小限

### 図表

- 各節に最低1つの図表を配置
- 図表はMermaid記法またはテキスト図で記述
- 図表番号は「図X.Y」形式（X=章番号、Y=章内連番）

### コード例

- 概念理解に必要な最小限のコードのみ
- 言語はPython（OCI SDK for Python）
- 疑似コードも可

### ページ配分

各章の目標ページ数は`docs/book-plan.md`を参照
```

---

## コマンド設計

### `/setup-book` — 初回セットアップ

Galleyの`/setup-project`に対応。以下を対話的に作成:

0. `docs/ideas/book-concept.md` を読み込み（事前に配置済み）
1. `docs/book-plan.md` ← book-planningスキル（book-concept.mdを元に詳細化）
2. `docs/book-architecture.md` ← 章構成と依存関係
3. `docs/writing-guidelines.md` ← writing-guidelinesスキル
4. `docs/glossary.md` ← glossary-creationスキル
5. `docs/repository-structure.md`
6. `docs/chapter-specs/ch01-spec.md` 〜 `ch15-spec.md` ← chapter-spec-writingスキル

**ポイント**: 
- `docs/ideas/book-concept.md`が全てのドキュメント生成の起点となる
- book-plan.mdのみユーザー承認を必須とし、
  それ以降は自動生成（Galleyの`setup-project`と同じパターン）。

### `/write-chapter [章番号]` — 章の執筆

Galleyの`/add-feature`に対応。完全自動実行モード:

1. **準備**: CLAUDE.md、関連ドキュメント、前後の章を読み込み
2. **計画**: ステアリングファイル作成（節ごとのタスク分解）
3. **執筆ループ**: tasklist.mdの全タスク完了まで自動実行
   - 節ごとに本文を執筆
   - 図表を設計・配置
   - 章末の理解度チェック問題を作成
4. **品質チェック**: サブエージェントでレビュー
   - 用語の統一チェック（glossary.mdとの照合）
   - 前後の章との整合性チェック
   - 技術的正確性チェック
5. **振り返り**: tasklist.mdに申し送り事項を記録

### `/review-chapter [章番号]` — 章のレビュー

Galleyの`/review-docs`に対応。サブエージェントを起動:

- 用語統一チェック
- 章間参照の整合性
- 図表の完全性
- 目標ページ数との乖離
- 技術的正確性

### `/fix-feedback [ファイル名]` — フィードバック修正

Galleyの`/fix-feedback`をそのまま書籍版に適用。
読了後のフィードバック（読んでわからなかった点、追記してほしい点）を
`docs/feedbacks/`に記録し、自動修正ワークフローを実行。

---

## スキル設計

### book-planning（書籍企画書）

Galleyの`prd-writing`に対応。

テンプレートの主要項目:
- 書籍タイトル・サブタイトル
- 対象読者・前提知識
- 到達目標（読了後にできるようになること）
- 全体構成（部・章・節の構成）
- ページ配分
- 執筆方針（図表ファースト、コード最小限、等）
- スコープ外

### chapter-spec-writing（章仕様書）

Galleyの`functional-design`に対応。

テンプレートの主要項目:
- 章のタイトル
- 章の目的（この章で読者が理解すべきこと）
- 前提知識（どの章を読んでいる必要があるか）
- 節の構成（各節のタイトルと概要）
- 図表リスト（各節で必要な図表の説明）
- コード例リスト（含める場合）
- 章末の理解度チェック問題（3〜5問）
- 前の章からの接続（前章の最後とどうつなぐか）
- 次の章への接続（次章の導入にどうつなぐか）
- 目標ページ数

### chapter-writing（章執筆）

ソフトウェア開発にはない、書籍固有のスキル。

ガイドの主要項目:
- 図表ファーストの執筆プロセス（先に図を設計し、本文は図の解説として書く）
- 節の構成パターン（導入→概念説明→具体例→まとめ）
- OCI Generative AI Serviceの例示パターン
- Mermaid図の記法ガイド
- 理解度チェック問題の作成パターン

### writing-guidelines（執筆ガイドライン）

Galleyの`development-guidelines`に対応。

テンプレートの主要項目:
- 文体ルール（常体、一人称、読者への語りかけ方）
- 表記ルール（技術用語の初出表記、数字の書き方、記号の使い方）
- 図表ルール（番号体系、キャプションの書き方、配置位置）
- コード例ルール（言語、インデント、コメントの付け方）
- 引用・参照ルール
- 禁止事項（曖昧な表現、主観的な評価、等）

### review（レビュー）

ソフトウェア開発のテストに対応。

チェック項目:
- **用語統一**: glossary.mdに定義された用語が正しく使われているか
- **章間整合性**: 前後の章で矛盾する記述がないか
- **図表完全性**: 本文で参照されている図表がすべて存在するか
- **技術正確性**: OCI Generative AI Service等の技術的記述が正確か
- **ページ配分**: 目標ページ数に対する乖離
- **読みやすさ**: 1文の長さ、段落の長さ、接続詞の使い方

---

## ワークフロー全体像

```
docs/ideas/book-concept.md（事前に配置）
  │
  ▼
/setup-book
  │
  ├── book-plan.md（book-concept.mdを元に作成、ユーザー承認必須）
  ├── book-architecture.md
  ├── writing-guidelines.md
  ├── glossary.md
  ├── repository-structure.md
  └── chapter-specs/ch01〜ch15-spec.md
          │
          ▼
/write-chapter 1
  │
  ├── .steering/YYYYMMDD-ch01-writing/
  │     ├── requirements.md
  │     ├── design.md
  │     └── tasklist.md
  │
  ├── manuscript/ch01/ch01.md（執筆）
  ├── manuscript/ch01/figures/（図表作成）
  │
  └── レビュー（サブエージェント）
        ├── 用語チェック
        ├── 整合性チェック
        └── 品質チェック
          │
          ▼
/write-chapter 2 ... （繰り返し）
          │
          ▼
読了後のフィードバック
  │
  ▼
/fix-feedback（修正）
```

---

## 次のステップ

この設計書の承認後、以下の順序で実装する:

1. **リポジトリのスキャフォールディング**: ディレクトリ構造とCLAUDE.mdの作成
2. **スキルの実装**: 各スキルのSKILL.md、guide.md、template.mdを作成
3. **コマンドの実装**: 4つのスラッシュコマンドを作成
4. **`/setup-book`の実行**: 永続ドキュメントの生成
5. **`/write-chapter 1`の実行**: 第1章の執筆で仕組みを検証
