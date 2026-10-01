# API Specification

## 方針
REST APIを基本とし、非同期処理はJob APIとイベントで扱う。外部AI APIをクライアントへ直接公開しない。

## Organization
- POST /api/v1/organizations
- GET /api/v1/organizations/me
- PATCH /api/v1/organizations/me
- POST /api/v1/organizations/me/documents

## Grants
- GET /api/v1/grants
- GET /api/v1/grants/{grant_id}
- GET /api/v1/grants/{grant_id}/source
- POST /api/v1/grants/{grant_id}/watch

## Matches
- GET /api/v1/matches
- GET /api/v1/matches/{match_id}
- POST /api/v1/matches/{match_id}/dismiss
- POST /api/v1/matches/{match_id}/save

## Applications
- POST /api/v1/applications
- GET /api/v1/applications
- GET /api/v1/applications/{application_id}
- POST /api/v1/applications/{application_id}/tasks
- PATCH /api/v1/applications/{application_id}/tasks/{task_id}

## Notifications
- GET /api/v1/notifications
- POST /api/v1/notifications/{id}/read

## AI jobs
内部API。一般ユーザーから直接provider/modelを指定させない。
- POST /internal/ai/jobs
- GET /internal/ai/jobs/{job_id}

## 非同期ジョブ
重い処理は202 Accepted + job_idを返す。再試行しても二重登録・二重通知にならないidempotency keyを利用する。

## エラー方針
- 4xx: ユーザー入力/権限
- 404: リソース不存在
- 409: 状態競合
- 422: 業務ルール違反
- 429: レート制限
- 5xx: システム/外部依存障害

## 出典
Grant APIのレスポンスにはsource_urlとofficial_document_urlを可能な限り含める。
