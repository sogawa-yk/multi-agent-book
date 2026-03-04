# 第9章 レビュー結果

## 構成・文体レビュー

### 指摘事項

1. **OKE英語注釈の欠落（修正済み）**: 70行目付近でOKEが初出するが英語注釈がなかった → `OKE（Oracle Container Engine for Kubernetes）`を追加
2. **Mermaidノード名（修正済み）**: 図9.1のホスティングオプション（Container Instances, OKE, Compute）に日本語補足を追加

### 良好な点
- 章全体の構成が仕様に忠実
- 図表が各節に配置され、視覚的に理解しやすい
- 前章（第8章）からの接続が自然

## 技術検証レビュー

### 要修正（2件）

1. **MCPトランスポートの数（修正済み）**: MCP仕様2025-03-26版では標準トランスポートは2つ（stdio, Streamable HTTP）。SSEは旧仕様のもので非推奨。「三つの方式がある」を修正し、SSEの非推奨化を明記。

2. **Workload IdentityとDynamic Groupの関係（修正済み）**: OKE Workload IdentityではDynamic Groupは不要。図9.4のWorkload Identityフローから`Dynamic Group`ノードへの接続を削除し、`ServiceAccount + IAMポリシー`に変更。本文も修正。

### 要確認（1件）

1. **コンテキストウィンドウサイズ（修正済み）**: 推奨モデルCommand Aは256Kトークンだが図9.6では128Kと記載。「128K〜256Kトークン」に修正。

### 正確と確認された項目
- Container Instances / OKE / Compute の特性と使い分け
- OCI SDK for Python API（VirtualNetworkClient、CreateVcnDetails、create_vcn等）
- Cohere Command A / R+のFunction Calling対応
- MCP各トランスポートの説明（stdio, SSE, Streamable HTTP）
- Instance Principal / Resource Principalの適用場面
- Dynamic GroupとIAMポリシーの説明
- Autonomous Database AI Vector SearchによるRAG
- GenAI Service Chat APIクライアント

---

## 対応結果
- **対応日**: 2026-03-04
- **修正内容**: 全5件の指摘を修正（OKE英語注釈追加、Mermaidノード名の日本語補足、MCPトランスポート記述の更新、Workload IdentityのDynamic Group不使用を反映、コンテキストウィンドウサイズの更新）
