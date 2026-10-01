# Job System Design

## 目的
「自走型AIが動くから自動」ではなく、自社のジョブ基盤が継続運転する。

## 基本構成
Scheduler
→ Job Queue
→ Worker
→ DB
→ Event
→ 次ジョブ/通知

## Job Types
- SOURCE_CHECK
- SOURCE_FETCH
- DOCUMENT_PARSE
- GRANT_NORMALIZE
- GRANT_DEDUP
- GRANT_VALIDATE
- MATCH_RULE_FILTER
- MATCH_AI_ANALYSIS
- NOTIFICATION_SEND
- DEADLINE_REMINDER
- APPLICATION_DRAFT
- APPLICATION_REVIEW

## 優先度
P0: 締切直前・障害復旧
P1: 新規公募の収集/マッチング
P2: 更新チェック
P3: バックフィル・分析

## Retry
指数バックオフ。外部サービスの一時障害は再試行するが、恒久エラーはDead Letter Queueへ送る。

## Idempotency
job_id + logical_keyで重複実行を防ぐ。通知にはnotification_idを持たせ、同一イベントの二重送信を防ぐ。

## AI障害時
Collector、DB、既存通知、期限管理は継続。AI分析だけpendingへ戻し、復旧後に再処理する。

## スケール
NPO数ではなく「実行ジョブ数」と「AI呼び出し数」を監視する。ルールフィルタでAI対象を削減する。

## SLO候補
- 情報源チェック成功率
- 新規公募検知遅延
- マッチング完了遅延
- 通知送信成功率
- AIジョブ成功率
- 重複通知率

MVPでは具体値を計測してからSLOを確定する。
