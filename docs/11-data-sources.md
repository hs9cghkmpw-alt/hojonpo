# Data Source Design

## 目的
助成金・補助金情報の収集をサービス品質の中核として設計する。

## 情報源の優先順位
1. 助成主体の公式募集ページ
2. 助成主体が公開する募集要項PDF
3. 公的機関の公式データ/API/RSS
4. 信頼できる二次情報源（発見用。最終根拠にはしない）

## Source Registry
各情報源をDBで管理する。
- source_id
- name
- organization
- source_type
- URL
- crawl_method
- crawl_interval
- last_checked_at
- last_success_at
- status
- terms/robots確認状態
- parser_version

## 取得パイプライン
Source Registry
→ Scheduler
→ Collector
→ Raw Document Storage
→ Parser
→ Normalizer
→ Deduplicator
→ Validation
→ Grant DB

## Grant最低データ
- title
- provider
- source_url
- official_document_url
- published_at
- application_start
- application_deadline
- eligible_legal_forms
- eligible_regions
- eligible_fields
- target_beneficiaries
- amount_min/max
- eligible_expenses
- restrictions
- required_documents
- source_last_seen_at
- source_hash
- extraction_confidence

## 更新検知
URLだけでなく本文/PDFのハッシュを保存し、更新・変更・掲載終了を検知する。

## 出典原則
NPOへ表示する重要条件には必ず一次情報源への導線を持たせる。AIの要約は原文の代替ではなく、確認を容易にする補助情報とする。

## MVPの情報源
最初から全国全件を狙わず、北海道を含む少数の公式情報源で収集品質・更新検知・PDF解析を検証する。
