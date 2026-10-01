# ドメインモデル

## Organization
NPO団体。

主属性:
id、name、legal_status、prefecture、municipalities、activity_areas、target_groups、budget_range、founded_at、profile_version

## OrganizationDocument
団体資料。

主属性:
id、organization_id、document_type、storage_key、extracted_text、version、uploaded_at

## FundingOpportunity
助成金・補助金等の公募。

主属性:
id、title、provider_name、source_url、source_document_url、published_at、application_start、application_deadline、amount_min、amount_max、eligible_legal_statuses、eligible_regions、eligible_fields、eligibility_text、status、source_fetched_at、normalized_at

## Match
団体と公募のマッチング結果。

主属性:
id、organization_id、funding_opportunity_id、rule_score、ai_score、confidence、matched_conditions、unmatched_conditions、uncertain_conditions、evidence、model、created_at

## Application
応募案件。

主属性:
id、organization_id、funding_opportunity_id、status、internal_deadline、submitted_at、result、result_reason

状態:
DISCOVERED → INTERESTED → PREPARING → REVIEW_REQUIRED → APPROVED → SUBMITTED → RESULT_PENDING → ADOPTED / REJECTED / WITHDRAWN

AIはSUBMITTEDへ直接変更できない。

## ApplicationTask
申請作業。

主属性:
id、application_id、task_type、title、status、due_at、requires_human_approval

## Notification
通知履歴。

主属性:
id、organization_id、type、reference_id、sent_at、delivery_status

## AIExecution
AI実行監査。

主属性:
id、provider、model、task_type、input_reference、output_reference、token_usage、latency_ms、status、created_at
