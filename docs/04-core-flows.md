# コアフロー詳細

## 1. 新規助成金発見

Scheduler
→ Source Collector
→ 取得
→ 内容ハッシュ比較
→ 新規/更新判定
→ Parser
→ Normalizer
→ Validation
→ FundingOpportunity保存
→ Candidate Matching

同じ情報を再取得しても二重登録しない。

## 2. マッチング

### Step 1: ルール判定
法人格、地域、締切、明示された対象分野など機械判定できる条件を処理する。

### Step 2: AI判定
活動内容と募集趣旨など意味理解が必要な条件を分析する。

AI出力は構造化し、fit、confidence、matched_conditions、unmatched_conditions、uncertain_conditions、evidenceを持つ。

### Step 3: 人間向け説明
「なぜ通知されたか」を表示し、根拠資料へリンクする。

## 3. 通知

対象:
- 高適合の新規案件
- 締切7日前
- 締切3日前
- 募集要項更新
- 申請タスク期限

同一案件の重複通知を防ぐ。

## 4. 応募開始

NPOが「応募したい」
→ Application作成
→ 必要資料確認
→ 不足情報列挙
→ AIドラフト
→ NPOレビュー
→ 修正
→ 最終確認
→ 提出

## 5. 申請書生成

AIにゼロから作文させず、
募集要項 + 団体プロフィール + 過去事業 + 今回事業 + 予算
を根拠データとして渡す。

生成物は可能な限り根拠データへの参照を保持する。

## 6. 結果登録

採択・不採択・辞退等を登録する。不採択理由も可能な範囲で保存し、次回の申請改善に利用する。
