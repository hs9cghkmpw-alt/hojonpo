# Matching Algorithm

## 基本思想
AIだけで「合う/合わない」を決めない。Hard constraintsとSemantic fitを分離する。

## Stage 1: Hard Filter
募集要項から抽出した明示条件をDB上で判定。
- 法人格
- 所在地/活動地域
- 対象分野
- 対象者
- 予算規模など明示条件
- 募集期間

明確な必須条件に×がある候補は原則AI詳細分析へ送らない。

## Stage 2: Semantic Analysis
AIが募集趣旨、対象事業、活動内容、過去実績等を比較する。

出力はscoreだけにしない。
- fit: high/medium/low/unknown
- reasons
- matched_requirements
- unmet_requirements
- uncertain_points
- evidence_references

## Stage 3: Decision
例:
- 必須条件NG → 対象外
- 必須条件OK + AI不確実 → 要確認
- 必須条件OK + semantic fit高 → 高適合候補
- 必須条件OK + semantic fit中 → 検討候補

## 表示
「適合度92%」だけではなく、
「なぜそう判断したか」「どの原文を根拠にしたか」「何が未確認か」を表示する。

## 学習データ
採択/不採択の結果は将来の改善に利用できるが、結果だけで採択確率を断定しない。初期MVPではルール＋説明可能なAI分析を優先する。

## 評価指標
- Precision@K
- false positive率
- false negative率
- ユーザー保存率
- 応募開始率
- 人間レビュー修正率
