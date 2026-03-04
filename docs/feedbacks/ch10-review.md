# 第10章 レビュー結果

## 構成・文体レビュー

### 指摘事項（修正済み）

1. **80字超過の文（修正済み）**: 13行目、15行目等の長文を分割・箇条書きに変更
2. **Cache with Redis未言及（修正済み）**: 10.5節に一時状態のキャッシュに関する段落を追加
3. **第8章への接続（修正済み）**: 10.3節にGenAI Service使用の一文を追加
4. **メッセージフォーマット設計（修正済み）**: 10.4節にメッセージフォーマットの設計パラグラフを追加
5. **テスト可能な設計への言及（修正済み）**: まとめ節にテスト手法への言及を追加

### 用語関連（修正済み）
- OKE初出章: glossary.mdの初出を第11章→第9章に修正
- Autonomous Database初出章: glossary.mdの初出を第11章→第9章に修正

## 技術検証レビュー

### 要修正（4件、全て修正済み）

1. **Agent CardとMCPの混同**: MCPではlist_tools、A2AではAgent Cardを使う記述に修正
2. **OCI Functionsの課金モデル**: 「呼び出し回数課金」→「呼び出し回数 + 実行時間課金」に修正
3. **OCI Functionsの長時間実行**: 「非対応」→「制限あり（同期: 最大5分、非同期: 最大1時間）」に修正
4. **A2Aプロトコルの通信パターン分類**: 「同期・A2A / HTTP REST」→「同期/非同期・A2A / HTTP（JSON-RPC + SSE）」に修正

### 正確と確認された項目
- オーケストレーター型パターンの定義
- MCP Streamable HTTPトランスポート
- OCI Resource Manager、Autonomous Database、Object Storage、Queue、Streaming、NSGの記述
- OKEのHPA/VPA、Dedicated AI Cluster、API Gatewayの記述
- Container InstancesとOKEの課金モデル

---

## 対応結果
- **対応日**: 2026-03-04
- **修正内容**: 構成・文体5件、用語2件、技術検証4件の合計11件の指摘を修正
