# 用語集 (Glossary)

**更新日**: 2026-03-03（第1章執筆後に「エージェントフレームワーク」を追加）

## 凡例

- **表記**: 本書での統一表記
- **英語**: 英語表記（初出時に併記）
- **定義**: 本書における定義
- **初出**: 最初に登場する章

---

## マルチエージェント関連

### エージェント (Agent)
**定義**: LLMを推論エンジンとし、ツール呼び出しとプランニング能力を持つ自律的なソフトウェアエンティティ。チャットボットとは異なり、自律的に判断しアクションを実行する。
**初出**: 第1章

### マルチエージェントシステム (Multi-Agent System)
**定義**: 複数のエージェントが協調してタスクを遂行するシステム。各エージェントが専門的な役割を持ち、通信・状態共有を通じて連携する。
**初出**: 第3章

### エージェントランタイム (Agent Runtime)
**定義**: エージェントの推論-行動ループを制御する実行基盤。ループ制御、エラーハンドリング、停止条件の管理を担う。
**初出**: 第1章

### シングルエージェント (Single Agent)
**定義**: 単一のエージェントが全てのタスクを処理する構成。マルチエージェントとの対比で使用する。
**初出**: 第1章

### エージェントフレームワーク (Agent Framework)
**定義**: エージェントの構成要素（LLM、ツール、メモリ等）とランタイムをパッケージとして提供するソフトウェアフレームワーク。LangChain、CrewAI、AutoGen等が該当する。
**初出**: 第1章

## 協調パターン

### 直列パイプライン (Sequential Pipeline)
**定義**: エージェントが順番に処理を行い、前のエージェントの出力を次のエージェントの入力とするパターン。
**初出**: 第4章

### 並列ファンアウト/ファンイン (Parallel Fan-out/Fan-in)
**定義**: 複数のエージェントに同時にタスクを分配（ファンアウト）し、結果を集約（ファンイン）するパターン。
**初出**: 第4章

### オーケストレーター (Orchestrator)
**定義**: 中央のエージェントがタスクを動的に分解し、サブエージェントに分配・統合するパターン。タスクの分解と結果の統合を担う。
**初出**: 第4章

### スーパーバイザー (Supervisor)
**定義**: 階層的な監督構造で、上位エージェントが下位エージェントに委任し、結果を監督するパターン。オーケストレーターとの違いは監督と委任にある。
**初出**: 第4章

### コレオグラフィ (Choreography)
**定義**: 中央制御なしにエージェントが自律的に協調するパターン。各エージェントがルールに基づいて他のエージェントと直接通信する。
**初出**: 第4章

### 評価者ループ (Evaluator Loop)
**定義**: 生成エージェントと評価エージェントが生成→評価→修正のサイクルを繰り返すパターン。品質保証に活用される。
**初出**: 第4章

## プロトコル・標準

### MCP (Model Context Protocol)
**定義**: LLMにツールやリソースを提供するための標準プロトコル。ツール定義、Transport層、ライフサイクル管理を規定する。
**初出**: 第2章

### A2A (Agent-to-Agent Protocol)
**定義**: エージェント間の通信を標準化するプロトコル。Agent Card、Task、Message、Artifactの概念を定義する。
**初出**: 第5章

### Function Calling
**定義**: LLMが外部ツールの呼び出しを判断・実行する仕組み。ツール定義（スキーマ）をLLMに提示し、適切なツールの選択と引数生成を行う。
**初出**: 第2章

## OCI関連

### OCI Generative AI Service
**定義**: Oracle Cloud Infrastructure上で提供される生成AIサービス。Cohere Command R+、Meta Llama等のモデルをAPI経由で利用できる。
**初出**: 第8章

### Resource Manager
**定義**: OCIが提供するTerraform実行のマネージドサービス。スタックの作成・計画・適用・破棄を管理する。
**初出**: 第11章

### OKE (Oracle Container Engine for Kubernetes)
**定義**: OCI上のマネージドKubernetesサービス。コンテナ化されたエージェントのホスティングに利用する。
**初出**: 第11章

### Autonomous Database
**定義**: OCI上の自律型データベースサービス。エージェントの知識ベースとしてVector Search、JSON、SQL機能を活用する。
**初出**: 第11章

### Resource Principal
**定義**: OCIリソースに付与されるIAMプリンシパル。エージェントがOCIサービスにアクセスする際の認証方式の一つ。
**初出**: 第9章

### Instance Principal
**定義**: コンピュートインスタンスに付与されるIAMプリンシパル。インスタンス上で動作するエージェントの認証に使用する。
**初出**: 第9章

## 一般技術用語

### ReActパターン (ReAct Pattern)
**定義**: Reasoning（推論）とActing（行動）を交互に繰り返すエージェントの動作パターン。思考→行動→観察のループで問題を解決する。
**初出**: 第1章

### コンテキストウィンドウ (Context Window)
**定義**: LLMが一度に処理できるトークンの最大数。エージェントの「記憶」の上限を決定する。
**初出**: 第1章

### コンテキストエンジニアリング (Context Engineering)
**定義**: LLMに渡すコンテキスト（入力情報）を設計する技法。何を含め、何を除外するかを戦略的に決定する。
**初出**: 第2章

### RAG (Retrieval-Augmented Generation)
**定義**: 外部知識ベースから関連情報を検索し、LLMの生成に組み込む手法。エージェントの長期記憶として活用される。
**初出**: 第1章

### Human-in-the-Loop (HITL)
**定義**: エージェントの処理フローに人間の判断・承認ポイントを組み込む設計パターン。重要な意思決定や安全性の確保に使用する。
**初出**: 第7章

### 冪等性 (Idempotency)
**定義**: 同じ操作を複数回実行しても結果が変わらない性質。インフラ操作における再実行可能性の設計に重要。
**初出**: 第7章

### チェックポイント (Checkpoint)
**定義**: エージェントの処理状態を特定の時点で保存する仕組み。障害からの復旧や再開に使用する。
**初出**: 第6章

### ブラックボード (Blackboard)
**定義**: 複数のエージェントが共有する中央の情報ストア。各エージェントが情報を読み書きして間接的に協調する。
**初出**: 第6章

### イベントソーシング (Event Sourcing)
**定義**: 状態の変更をイベントの列として記録する手法。エージェントの行動履歴の追跡と再現に活用する。
**初出**: 第6章

### Terraform
**定義**: Infrastructure as Code（IaC）ツール。HCL（HashiCorp Configuration Language）でインフラを定義し、宣言的にプロビジョニングする。
**初出**: 第11章

### トレーシング (Tracing)
**定義**: エージェントの処理フローを追跡・可視化する技術。分散システムにおけるリクエストの流れを把握する。
**初出**: 第13章

---

## 索引（五十音順）

### あ行
- [イベントソーシング](#イベントソーシング-event-sourcing)
- [エージェント](#エージェント-agent)
- [エージェントフレームワーク](#エージェントフレームワーク-agent-framework)
- [エージェントランタイム](#エージェントランタイム-agent-runtime)
- [オーケストレーター](#オーケストレーター-orchestrator)

### か行
- [コレオグラフィ](#コレオグラフィ-choreography)
- [コンテキストウィンドウ](#コンテキストウィンドウ-context-window)
- [コンテキストエンジニアリング](#コンテキストエンジニアリング-context-engineering)

### さ行
- [シングルエージェント](#シングルエージェント-single-agent)
- [スーパーバイザー](#スーパーバイザー-supervisor)

### た行
- [チェックポイント](#チェックポイント-checkpoint)
- [直列パイプライン](#直列パイプライン-sequential-pipeline)
- [トレーシング](#トレーシング-tracing)

### な行
- [並列ファンアウト/ファンイン](#並列ファンアウトファンイン-parallel-fan-outfan-in)

### は行
- [ブラックボード](#ブラックボード-blackboard)
- [冪等性](#冪等性-idempotency)
- [評価者ループ](#評価者ループ-evaluator-loop)

### ま行
- [マルチエージェントシステム](#マルチエージェントシステム-multi-agent-system)

### ら行

### A-Z
- [A2A](#a2a-agent-to-agent-protocol)
- [Autonomous Database](#autonomous-database)
- [Function Calling](#function-calling)
- [Human-in-the-Loop](#human-in-the-loop-hitl)
- [Instance Principal](#instance-principal)
- [MCP](#mcp-model-context-protocol)
- [OCI Generative AI Service](#oci-generative-ai-service)
- [OKE](#oke-oracle-container-engine-for-kubernetes)
- [RAG](#rag-retrieval-augmented-generation)
- [ReActパターン](#reactパターン-react-pattern)
- [Resource Manager](#resource-manager)
- [Resource Principal](#resource-principal)
- [Terraform](#terraform)
