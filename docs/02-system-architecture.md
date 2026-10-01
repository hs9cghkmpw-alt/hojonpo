# システムアーキテクチャ

## 全体

Web UI
→ API/Auth
→ Application API
→ PostgreSQL
→ Job Queue / Scheduler

Job Workerは以下を担当する。

- Source Collector
- Parser / Normalizer
- Matching
- Notification
- AI Worker

## 重要な分離

### Collection Layer
Web、RSS、API、PDF等から公募情報を取得する。

### Normalization Layer
取得データを共通スキーマへ変換する。

### Matching Layer
まずコードで明確な条件を判定し、その後AIで曖昧な意味条件を判定する。

### AI Layer
要約、マッチング理由、申請書ドラフト、レビュー等を担当する。

### Notification Layer
メール・Web通知等を担当する。AIから直接通知を送らせない。

### Workflow Layer
応募、準備、レビュー、提出、結果を状態機械として管理する。

## スケール設計

「全NPO × 全公募」を毎回AI処理しない。

全データ
→ DB/ルールで安価に絞る
→ 候補集合
→ AI詳細判定
→ 通知

AI呼び出しは候補集合に限定する。

## AI Provider Adapter

アプリケーションからAIを抽象化する。

想定インターフェース:
- classifyEligibility
- explainMatch
- summarizeCall
- draftApplication
- reviewApplication

Provider:
- OpenAI
- Gemini
- Claude
- 将来Local LLM

定期実行・イベント発火は自社Scheduler/Queueが制御する。AIの自走機能をサービスの時計にしない。
