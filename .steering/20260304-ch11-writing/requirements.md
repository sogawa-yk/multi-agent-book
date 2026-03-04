# 第11章 要件定義

## 概要
OCI Generative AI Service以外のOCIサービス群をエージェントのツール・基盤として活用する設計パターンを体系的に整理する。

## 章仕様（ch11-spec.md準拠）
- 目標ページ数: 20p
- 7節構成: Resource Manager / OKE / Autonomous Database / Streaming・Queue / Logging・Monitoring / Vault / API Gateway
- 図表: 図11.1〜11.5 + 表11.1
- 章末に理解度チェック問題5問

## 前後の章との接続
- 前章（第10章）: マルチエージェントシステムの構築でOCIサービスを概要レベルで言及 → 本章で個別に深掘り
- 次章（第12章）: ケーススタディで本章のサービス群を統合利用 → 本章末で「次章でこれらを統合」と接続

## 過去の章からの申し送り
- Mermaidノード名は日本語のみ（英語補記なし）
- 文の長さは80文字以内。例示は別文に分離
- 略語は初出時に定義。すでに定義済みのもの: OKE, VCN, HCL, IAM, ADB, RAG, MCP, A2A, IaC
- Resource Manager, Autonomous Databaseは第8章の用語集で初出（第11章）と定義されているが、第9〜10章で言及済み
