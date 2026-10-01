# Database Schema

## 設計原則
- テナント（NPO）単位でデータを分離
- 原文とAI生成結果を分離
- すべての重要判断に出典・バージョン・履歴を残す
- 削除ではなく履歴管理を優先

## 主なテーブル

### organizations
NPO基本情報。
- id
- name
- legal_form
- address_region
- activity_regions
- fields
- founded_at
- budget_range
- staff_count
- profile_status

### organization_documents
- id
- organization_id
- document_type
- storage_key
- version
- extracted_text
- uploaded_at
- checksum

### grants
助成金の正規化された現在状態。
- id
- title
- provider
- source_id
- source_url
- official_document_url
- deadline
- status
- conditions_json
- amount_json
- current_version_id

### grant_versions
募集情報の変更履歴。
- id
- grant_id
- version
- raw_document_id
- normalized_json
- content_hash
- detected_at

### sources
情報源の監視設定。

### matches
NPOと助成金の候補関係。
- organization_id
- grant_id
- rule_result_json
- ai_result_json
- confidence
- status
- created_at
- updated_at

### notifications
- organization_id
- match_id
- channel
- priority
- sent_at
- read_at

### applications
申請案件。
- organization_id
- grant_id
- status
- deadline
- owner
- started_at
- submitted_at

### application_tasks
申請作業。
- application_id
- task_type
- status
- due_at
- evidence_required
- human_approval_required

### ai_runs
AI実行監査。
- provider
- model
- task_type
- input_reference
- output_reference
- status
- latency_ms
- token_usage
- cost_estimate
- created_at

## テナント境界
organization_idを主要な業務データに付与し、API/DB双方でアクセス制御する。
