# AI・エージェント設計

## 基本思想

AIエージェントがサービス全体を動かすのではなく、

「アプリケーションが仕事を定義し、AIがその仕事を実行する」

構造にする。

## Agent Roles

### Funding Analyst
公募内容を解析し、構造化・要約する。

### Matching Analyst
団体プロフィールと公募を比較する。

### Application Assistant
申請準備を支援する。

### Review Assistant
募集要項と申請内容の整合性を確認する。

### Research Agent
将来、情報源の探索や更新調査を支援する。

## エージェントに許可する操作

- DB読み取り
- 指定範囲の文書読み取り
- 分析結果保存
- ドラフト作成
- タスク提案

## MVPで禁止する操作

- 自動提出
- 契約締結
- 支払い
- 団体情報の無断変更
- 外部サイトへの自由な投稿
- 採択保証

## Dots等の自走型AI

将来的にResearch AgentやApplication Assistantの実行ランナーとして利用できる。

ただし、サービスのスケジュール制御、データ保存、通知制御はDots固有機能に依存させない。

## Human-in-the-loop

以下は人間確認必須:
- 応募意思
- 重要な団体情報変更
- 申請書最終版
- 予算最終版
- 提出
- 結果登録

## AI品質管理

AI実行ごとにprovider、model、prompt/version、input data version、output、token/cost、latency、statusを記録する。
