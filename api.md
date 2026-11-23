# OmniWrap Java API

<!-- omniwrap-api-reference eyJjb250cmFjdF9maW5nZXJwcmludCI6IjIyODliY2IwZDY2MWJkZWE2ZGQ0N2M3OTY3ZjM3YWFjZTdkM2ExNTJlMThlN2QyZjY0YzA4NTE0ZmI3M2U3OTUiLCJvcGVyYXRpb25fY291bnQiOjE2LCJyZW5kZXJlciI6ImphdmEiLCJ2ZXJzaW9uIjoiMS41LjAifQ -->

This generated index is tied to Semantic IR `1.14.0` and contract fingerprint `2289bcb0d661bdea6dd47c7967f37aace7d3a152e18e7d2f64c08514fb73e795`. Every operation below is rendered from the same semantic contract and artifact-attested public member allocation as the SDK.

SDK maturity: **experimental**  
Artifact evidence: [`omniwrap-artifact.json`](omniwrap-artifact.json) binds this file by SHA-256 and is revalidated by the package gate.

## Client hooks and tracing

`ClientOptions.builder().hooks(RequestHooks)` registers four callbacks. Every attempt starts with `beforeRequest` and ends with exactly one of `onRetry` (another attempt follows), `afterResponse` (the success the call returns) or `onError` (the failure the call reports). Each receives the operation id, the HTTP method, the URL, the request headers, the attempt number (from 1), the time elapsed since the call started and, once the server answered, the HTTP status. No context carries a credential: `Authorization`, `Proxy-Authorization`, `Cookie`, every API-key header and API-key query parameter, and any configured credential value read `[redacted]`. Every context is an immutable `HookContext` record: no hook can change the request.

`ClientOptions.builder().tracer(RequestTracer)` opens one span per call through the tracer interface this SDK defines, named after the operation id, with `http.request.method`, `http.response.status_code` and `http.request.resend_count`. It needs no tracing library; README.md maps it onto the OpenTelemetry API.

## Shared types

- `ApiError`
- `Artifact`
- `CancelRequest`
- `CancellationReceipt`
- `ConfigurationRequest`
- `ConfigurationRevision`
- `Cursor`
- `Diagnostic`
- `ErrorDetail`
- `EventPage`
- `Evidence`
- `EvidenceBinding`
- `EvidencePage`
- `ExecutionBinding`
- `GateReport`
- `GateStatus`
- `LogEntry`
- `LogPage`
- `ObservedPhase`
- `OpaqueId`
- `Preview`
- `PreviewEvent`
- `PreviewInputs`
- `PreviewPage`
- `PreviewRequest`
- `PreviewState`
- `PrimaryArtifacts`
- `ProfileId`
- `Project`
- `ProjectPage`
- `Sha256`
- `SourceRevision`
- `StrongEtag`
- `Timestamp`
- `UserContext`

## Resource `artifacts()`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJhcnRpZmFjdHMoKS5nZXQiLCJtZXRob2QiOiJHRVQiLCJvcGVyYXRpb25faWQiOiJnZXRBcnRpZmFjdCIsInBhdGgiOiIvdjEvcHJvamVjdHMve3Byb2plY3RJZH0vYXJ0aWZhY3RzL3thcnRpZmFjdElkfSIsInJlc291cmNlIjoiYXJ0aWZhY3RzKCkiLCJzZWN0aW9uX3NoYTI1NiI6IjA4MThiOTc4ZWRmZTVhOTM1YWRhNWM5OTRiMjI5MzFiYzMyNzhlYWNlYTQ5YTFjZjAzMjAxZWQ0MTU4YWZjYzAiLCJzaWduYXR1cmVfc2hhMjU2IjoiMDRlMjEzZWVkZWYwNDc0YjlhODc1MjlmMjg0Njc5NDhmMGQ1ODY4ZTZmZjMzNWFkY2ViNDQ5NzgwNTlkMmMzMCJ9 -->
### `client.artifacts().get`

Operation ID: `getArtifact`  
Route: `GET` `/v1/projects/{projectId}/artifacts/{artifactId}`  
Equivalent member: `client.getArtifact`  

#### Signature

```java
public Artifact get(OpaqueId projectId, OpaqueId artifactId)
public CompletableFuture<Artifact> getAsync(OpaqueId projectId, OpaqueId artifactId)
public ApiResponse<Artifact> getWithResponse(OpaqueId projectId, OpaqueId artifactId)
public CompletableFuture<ApiResponse<Artifact>> getWithResponseAsync(OpaqueId projectId, OpaqueId artifactId)
public Artifact get(OpaqueId projectId, OpaqueId artifactId, RequestOptions requestOptions)
public CompletableFuture<Artifact> getAsync(OpaqueId projectId, OpaqueId artifactId, RequestOptions requestOptions)
public ApiResponse<Artifact> getWithResponse(OpaqueId projectId, OpaqueId artifactId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<Artifact>> getWithResponseAsync(OpaqueId projectId, OpaqueId artifactId, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `artifactId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (Artifact) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "path",
      "name": "artifactId",
      "value": "example"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.artifacts().get(/* projectId */ "example", /* artifactId */ "example");
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRBcnRpZmFjdCJ9 -->

## Resource `configurations()`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJjb25maWd1cmF0aW9ucygpLmNyZWF0ZVJldmlzaW9uIiwibWV0aG9kIjoiUE9TVCIsIm9wZXJhdGlvbl9pZCI6ImNyZWF0ZUNvbmZpZ3VyYXRpb25SZXZpc2lvbiIsInBhdGgiOiIvdjEvcHJvamVjdHMve3Byb2plY3RJZH0vY29uZmlndXJhdGlvbi1yZXZpc2lvbnMiLCJyZXNvdXJjZSI6ImNvbmZpZ3VyYXRpb25zKCkiLCJzZWN0aW9uX3NoYTI1NiI6IjgyODY2NWFjZWE0N2U1OWI0M2YyNTgwYWI3YmFiY2E5ZDEwMDdlN2RkN2NkOGFmYzE0ZTE3OWJmMDkwM2ZhMzUiLCJzaWduYXR1cmVfc2hhMjU2IjoiNzdjZWVhNzU5MzEwOGVmODJmMDZhNzVjNmE1NmM2MGVjZWFmOGFmZDNhNmRkMDk1ZmNmM2U1MDk4OWUxNjc2MSJ9 -->
### `client.configurations().createRevision`

Operation ID: `createConfigurationRevision`  
Route: `POST` `/v1/projects/{projectId}/configuration-revisions`  
Equivalent member: `client.createConfigurationRevision`  

#### Signature

```java
public ConfigurationRevision createRevision(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body)
public CompletableFuture<ConfigurationRevision> createRevisionAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body)
public ApiResponse<ConfigurationRevision> createRevisionWithResponse(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body)
public CompletableFuture<ApiResponse<ConfigurationRevision>> createRevisionWithResponseAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body)
public ConfigurationRevision createRevision(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body, RequestOptions requestOptions)
public CompletableFuture<ConfigurationRevision> createRevisionAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body, RequestOptions requestOptions)
public ApiResponse<ConfigurationRevision> createRevisionWithResponse(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<ConfigurationRevision>> createRevisionWithResponseAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `If-Match` | `header` | yes | `StrongEtag` | Exactly one strong ETag. Configuration activation and preview creation compare the current Project ETag, including first activation. Cancellation compares the Preview ETag. Stale = 412; absent = 428. Wildcard, weak tags and lists are rejected. |
| `Idempotency-Key` | `header` | yes | `string` | Required on every mutation. Scope = organization + project + operation; fingerprint includes raw body bytes, media type, resource and If-Match. Same key/content replays the same receipt; changed content is 409. Retained for 86400 seconds; reconcile an ambiguous outcome within retention before retry, never silently allocate a new key. |
| `X-CSRF-Token` | `header` | yes | `string` | Session-bound synchronizer token from the trusted BFF bootstrap, independent of the unreadable session cookie. Validate same-origin Origin and CSRF before mutation. This contract does not implement or provision the session/CSRF exchange. |
| `body` | body | yes | `ConfigurationRequest` |  |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `201` | Created and atomically activated after admitted engine resolution; response ETag identifies the immutable configuration. Reload Project to obtain the new Project ETag. | application/json (ConfigurationRevision) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `409` | idempotency_conflict/reconcile_idempotency, binding_conflict/refresh_snapshot, or retry_requires_reconciliation/refresh_snapshot. No additional effect. | application/json (allOf&lt;ApiError, object&gt;) |
| `412` | precondition_failed; recovery=refresh_snapshot. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `413` | request_too_large; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `415` | unsupported_media_type; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `428` | precondition_required; recovery=refresh_snapshot. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "body": {
    "profileId": "openapi-typescript-preview/1",
    "sourceRevisionId": "example"
  },
  "content_type": "application/json",
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "header",
      "name": "If-Match",
      "value": "\"A\""
    },
    {
      "in": "header",
      "name": "Idempotency-Key",
      "value": "AAAAAAAAAAAAAAAA"
    },
    {
      "in": "header",
      "name": "X-CSRF-Token",
      "value": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.configurations().createRevision(/* projectId */ "example", /* If-Match */ "\"A\"", /* Idempotency-Key */ "AAAAAAAAAAAAAAAA", /* X-CSRF-Token */ "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA", /* body */ {"profileId": "openapi-typescript-preview/1", "sourceRevisionId": "example"});
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJjcmVhdGVDb25maWd1cmF0aW9uUmV2aXNpb24ifQ -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJjb25maWd1cmF0aW9ucygpLmdldFJldmlzaW9uIiwibWV0aG9kIjoiR0VUIiwib3BlcmF0aW9uX2lkIjoiZ2V0Q29uZmlndXJhdGlvblJldmlzaW9uIiwicGF0aCI6Ii92MS9wcm9qZWN0cy97cHJvamVjdElkfS9jb25maWd1cmF0aW9uLXJldmlzaW9ucy97cmV2aXNpb25JZH0iLCJyZXNvdXJjZSI6ImNvbmZpZ3VyYXRpb25zKCkiLCJzZWN0aW9uX3NoYTI1NiI6Ijc4ZmY4YjMyMGI2MTBlZmFhYTFlYmMwZDU0MmRmNmJlYjdhMDM3OGNlYzA0NDc5NWNkOWQ4NjgzODI5Y2NlMzYiLCJzaWduYXR1cmVfc2hhMjU2IjoiODhjZWY0NGUwNDZiMDA4NzI0YWU4ZjhjNDU2ZWVlNjhkMzgwNzI1OGMxOWUyZjg1ZjhlYzA3MTIzMTUwNTZiMiJ9 -->
### `client.configurations().getRevision`

Operation ID: `getConfigurationRevision`  
Route: `GET` `/v1/projects/{projectId}/configuration-revisions/{revisionId}`  
Equivalent member: `client.getConfigurationRevision`  

#### Signature

```java
public ConfigurationRevision getRevision(OpaqueId projectId, OpaqueId revisionId)
public CompletableFuture<ConfigurationRevision> getRevisionAsync(OpaqueId projectId, OpaqueId revisionId)
public ApiResponse<ConfigurationRevision> getRevisionWithResponse(OpaqueId projectId, OpaqueId revisionId)
public CompletableFuture<ApiResponse<ConfigurationRevision>> getRevisionWithResponseAsync(OpaqueId projectId, OpaqueId revisionId)
public ConfigurationRevision getRevision(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public CompletableFuture<ConfigurationRevision> getRevisionAsync(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public ApiResponse<ConfigurationRevision> getRevisionWithResponse(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<ConfigurationRevision>> getRevisionWithResponseAsync(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `revisionId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (ConfigurationRevision) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "path",
      "name": "revisionId",
      "value": "example"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.configurations().getRevision(/* projectId */ "example", /* revisionId */ "example");
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRDb25maWd1cmF0aW9uUmV2aXNpb24ifQ -->

## Resource `context()`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJjb250ZXh0KCkuZ2V0VXNlciIsIm1ldGhvZCI6IkdFVCIsIm9wZXJhdGlvbl9pZCI6ImdldFVzZXJDb250ZXh0IiwicGF0aCI6Ii92MS9tZS9jb250ZXh0IiwicmVzb3VyY2UiOiJjb250ZXh0KCkiLCJzZWN0aW9uX3NoYTI1NiI6ImRkYzM3N2QwNWNiNTg4ODlmYmU5YmYyNTAyNjU3YzljODk3OGM1YmIxY2EwNjFhZDBhMzFjMGMzZDdmZTY5NzMiLCJzaWduYXR1cmVfc2hhMjU2IjoiNmYzYjI4ZjFkNmViMmM4YTAyODc3NjM2YWExMDFmOGZjZjQ0ZTJmZjE4ZjA2ZTJlMDdmMWQzMzA5ZmNjNTM4NSJ9 -->
### `client.context().getUser`

Operation ID: `getUserContext`  
Route: `GET` `/v1/me/context`  
Equivalent member: `client.getUserContext`  

#### Signature

```java
public UserContext getUser()
public CompletableFuture<UserContext> getUserAsync()
public ApiResponse<UserContext> getUserWithResponse()
public CompletableFuture<ApiResponse<UserContext>> getUserWithResponseAsync()
public UserContext getUser(RequestOptions requestOptions)
public CompletableFuture<UserContext> getUserAsync(RequestOptions requestOptions)
public ApiResponse<UserContext> getUserWithResponse(RequestOptions requestOptions)
public CompletableFuture<ApiResponse<UserContext>> getUserWithResponseAsync(RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| _none_ | | | | |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (UserContext) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": []
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.context().getUser();
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRVc2VyQ29udGV4dCJ9 -->

## Resource `evidence()`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJldmlkZW5jZSgpLmdldCIsIm1ldGhvZCI6IkdFVCIsIm9wZXJhdGlvbl9pZCI6ImdldEV2aWRlbmNlIiwicGF0aCI6Ii92MS9wcm9qZWN0cy97cHJvamVjdElkfS9ldmlkZW5jZS97ZXZpZGVuY2VJZH0iLCJyZXNvdXJjZSI6ImV2aWRlbmNlKCkiLCJzZWN0aW9uX3NoYTI1NiI6ImNhNjU2MDQyMmZhMzQ2NDJlNjk1OWZiMDNkNjE1MmQ0YjYwZjIzN2VhNjk4MDUwYzA2ZmNjMGRlNWFlNDUzYzAiLCJzaWduYXR1cmVfc2hhMjU2IjoiNWJjMWNmNGVkN2ViMDZhYTI0ODgzM2QwZWIwZTBlNmE2MDI4OGE3NjM2NmUxMDUxZTZkMzFkNGUxNGM2NjhkOCJ9 -->
### `client.evidence().get`

Operation ID: `getEvidence`  
Route: `GET` `/v1/projects/{projectId}/evidence/{evidenceId}`  
Equivalent member: `client.getEvidence`  

#### Signature

```java
public Evidence get(OpaqueId projectId, OpaqueId evidenceId)
public CompletableFuture<Evidence> getAsync(OpaqueId projectId, OpaqueId evidenceId)
public ApiResponse<Evidence> getWithResponse(OpaqueId projectId, OpaqueId evidenceId)
public CompletableFuture<ApiResponse<Evidence>> getWithResponseAsync(OpaqueId projectId, OpaqueId evidenceId)
public Evidence get(OpaqueId projectId, OpaqueId evidenceId, RequestOptions requestOptions)
public CompletableFuture<Evidence> getAsync(OpaqueId projectId, OpaqueId evidenceId, RequestOptions requestOptions)
public ApiResponse<Evidence> getWithResponse(OpaqueId projectId, OpaqueId evidenceId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<Evidence>> getWithResponseAsync(OpaqueId projectId, OpaqueId evidenceId, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `evidenceId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (Evidence) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "path",
      "name": "evidenceId",
      "value": "example"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.evidence().get(/* projectId */ "example", /* evidenceId */ "example");
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRFdmlkZW5jZSJ9 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJldmlkZW5jZSgpLmxpc3RQcmV2aWV3IiwibWV0aG9kIjoiR0VUIiwib3BlcmF0aW9uX2lkIjoibGlzdFByZXZpZXdFdmlkZW5jZSIsInBhdGgiOiIvdjEvcHJvamVjdHMve3Byb2plY3RJZH0vcHJldmlld3Mve3ByZXZpZXdJZH0vZXZpZGVuY2UiLCJyZXNvdXJjZSI6ImV2aWRlbmNlKCkiLCJzZWN0aW9uX3NoYTI1NiI6IjMxYjllMGZmYjIwY2VhYWIyNmIzN2ZkZjVkYjFmZTg4M2NiM2EyMmUzODAzZDkyMWI2MTQyZmUyYWY3ZDgxOTciLCJzaWduYXR1cmVfc2hhMjU2IjoiN2Y2MWM4ODhhODdkYzQ5Yjk2ODc0NDBiNDYxMmNiYWVkMjdlY2Y4OWJmZTY4ZjI5YjU1M2UyMDQ4MWY3MjM0MyJ9 -->
### `client.evidence().listPreview`

Operation ID: `listPreviewEvidence`  
Route: `GET` `/v1/projects/{projectId}/previews/{previewId}/evidence`  
Equivalent member: `client.listPreviewEvidence`  

#### Signature

```java
public EvidencePage listPreview(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<EvidencePage> listPreviewAsync(OpaqueId projectId, OpaqueId previewId)
public ApiResponse<EvidencePage> listPreviewWithResponse(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<ApiResponse<EvidencePage>> listPreviewWithResponseAsync(OpaqueId projectId, OpaqueId previewId)
public EvidencePage listPreview(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<EvidencePage> listPreviewAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public ApiResponse<EvidencePage> listPreviewWithResponse(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<EvidencePage>> listPreviewWithResponseAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public EvidencePage listPreview(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability)
public CompletableFuture<EvidencePage> listPreviewAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability)
public ApiResponse<EvidencePage> listPreviewWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability)
public CompletableFuture<ApiResponse<EvidencePage>> listPreviewWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability)
public EvidencePage listPreview(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability, RequestOptions requestOptions)
public CompletableFuture<EvidencePage> listPreviewAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability, RequestOptions requestOptions)
public ApiResponse<EvidencePage> listPreviewWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<EvidencePage>> listPreviewWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `previewId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `cursor` | `query` | no | `Cursor` | Opaque scope-bound continuation, never an offset or authority token. Expired/gap = 410 refresh_snapshot; invalid/tampered/wrong filters = 422. Denied objects remain uniform404. |
| `limit` | `query` | no | `integer` | Maximum page size; default 50. |
| `gateId` | `query` | no | `string` |  |
| `availability` | `query` | no | `string` |  |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (EvidencePage) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `410` | cursor_expired; recovery=refresh_snapshot. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "path",
      "name": "previewId",
      "value": "example"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.evidence().listPreview(/* projectId */ "example", /* previewId */ "example", /* optional: cursor, limit, gateId, availability */);
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJsaXN0UHJldmlld0V2aWRlbmNlIn0 -->

## Resource `previews()`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJwcmV2aWV3cygpLmNhbmNlbCIsIm1ldGhvZCI6IlBPU1QiLCJvcGVyYXRpb25faWQiOiJjYW5jZWxQcmV2aWV3IiwicGF0aCI6Ii92MS9wcm9qZWN0cy97cHJvamVjdElkfS9wcmV2aWV3cy97cHJldmlld0lkfS9jYW5jZWwiLCJyZXNvdXJjZSI6InByZXZpZXdzKCkiLCJzZWN0aW9uX3NoYTI1NiI6ImJiZjUzMGU1YTkxZWQ2ZGRlMWUwNjM5OTQzNWY3M2I5N2RjMjBkZWY0YTlmMTU2MzhmOWVjMDI0YzQxN2QzMDYiLCJzaWduYXR1cmVfc2hhMjU2IjoiNzA4NjcxZjI3MDg0MTAzM2Y1ODZjZTIwZjMxNTRjNjg5ZjRjMzA2ZTI0ZmUwYmM0MDYzMmQ0YWY0YTExMjZlMCJ9 -->
### `client.previews().cancel`

Operation ID: `cancelPreview`  
Route: `POST` `/v1/projects/{projectId}/previews/{previewId}/cancel`  
Equivalent member: `client.cancelPreview`  

#### Signature

```java
public CancellationReceipt cancel(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body)
public CompletableFuture<CancellationReceipt> cancelAsync(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body)
public ApiResponse<CancellationReceipt> cancelWithResponse(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body)
public CompletableFuture<ApiResponse<CancellationReceipt>> cancelWithResponseAsync(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body)
public CancellationReceipt cancel(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body, RequestOptions requestOptions)
public CompletableFuture<CancellationReceipt> cancelAsync(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body, RequestOptions requestOptions)
public ApiResponse<CancellationReceipt> cancelWithResponse(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<CancellationReceipt>> cancelWithResponseAsync(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `previewId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `If-Match` | `header` | yes | `StrongEtag` | Exactly one strong ETag. Configuration activation and preview creation compare the current Project ETag, including first activation. Cancellation compares the Preview ETag. Stale = 412; absent = 428. Wildcard, weak tags and lists are rejected. |
| `Idempotency-Key` | `header` | yes | `string` | Required on every mutation. Scope = organization + project + operation; fingerprint includes raw body bytes, media type, resource and If-Match. Same key/content replays the same receipt; changed content is 409. Retained for 86400 seconds; reconcile an ambiguous outcome within retention before retry, never silently allocate a new key. |
| `X-CSRF-Token` | `header` | yes | `string` | Session-bound synchronizer token from the trusted BFF bootstrap, independent of the unreadable session cookie. Validate same-origin Origin and CSRF before mutation. This contract does not implement or provision the session/CSRF exchange. |
| `body` | body | yes | `CancelRequest` |  |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `202` | Accepted for asynchronous processing; not a completed effect. | application/json (CancellationReceipt) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `409` | idempotency_conflict/reconcile_idempotency, binding_conflict/refresh_snapshot, or retry_requires_reconciliation/refresh_snapshot. No additional effect. | application/json (allOf&lt;ApiError, object&gt;) |
| `412` | precondition_failed; recovery=refresh_snapshot. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `413` | request_too_large; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `415` | unsupported_media_type; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `428` | precondition_required; recovery=refresh_snapshot. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "body": {
    "reason": "user_requested"
  },
  "content_type": "application/json",
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "path",
      "name": "previewId",
      "value": "example"
    },
    {
      "in": "header",
      "name": "If-Match",
      "value": "\"A\""
    },
    {
      "in": "header",
      "name": "Idempotency-Key",
      "value": "AAAAAAAAAAAAAAAA"
    },
    {
      "in": "header",
      "name": "X-CSRF-Token",
      "value": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.previews().cancel(/* projectId */ "example", /* previewId */ "example", /* If-Match */ "\"A\"", /* Idempotency-Key */ "AAAAAAAAAAAAAAAA", /* X-CSRF-Token */ "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA", /* body */ {"reason": "user_requested"});
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJjYW5jZWxQcmV2aWV3In0 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJwcmV2aWV3cygpLmNyZWF0ZSIsIm1ldGhvZCI6IlBPU1QiLCJvcGVyYXRpb25faWQiOiJjcmVhdGVQcmV2aWV3IiwicGF0aCI6Ii92MS9wcm9qZWN0cy97cHJvamVjdElkfS9wcmV2aWV3cyIsInJlc291cmNlIjoicHJldmlld3MoKSIsInNlY3Rpb25fc2hhMjU2IjoiMmNiMWQxMGZiYWE5MGM3MDE3MDZjNTBhNTM3MjYxZGNhNWRkNmUxNzA2ODVjMDJhYTY1N2YwNmE3Njg5ODI3YyIsInNpZ25hdHVyZV9zaGEyNTYiOiJiNjc2ODcxNDE3NjdiOThlMjg2Y2JlYjdhOWRhN2E4ZjMxYzYwYzMyMjdmNDZiMmYzZWQ1OWY1YmMyMWMyMzNjIn0 -->
### `client.previews().create`

Operation ID: `createPreview`  
Route: `POST` `/v1/projects/{projectId}/previews`  
Equivalent member: `client.createPreview`  

#### Signature

```java
public Preview create(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body)
public CompletableFuture<Preview> createAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body)
public ApiResponse<Preview> createWithResponse(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body)
public CompletableFuture<ApiResponse<Preview>> createWithResponseAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body)
public Preview create(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body, RequestOptions requestOptions)
public CompletableFuture<Preview> createAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body, RequestOptions requestOptions)
public ApiResponse<Preview> createWithResponse(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<Preview>> createWithResponseAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `If-Match` | `header` | yes | `StrongEtag` | Exactly one strong ETag. Configuration activation and preview creation compare the current Project ETag, including first activation. Cancellation compares the Preview ETag. Stale = 412; absent = 428. Wildcard, weak tags and lists are rejected. |
| `Idempotency-Key` | `header` | yes | `string` | Required on every mutation. Scope = organization + project + operation; fingerprint includes raw body bytes, media type, resource and If-Match. Same key/content replays the same receipt; changed content is 409. Retained for 86400 seconds; reconcile an ambiguous outcome within retention before retry, never silently allocate a new key. |
| `X-CSRF-Token` | `header` | yes | `string` | Session-bound synchronizer token from the trusted BFF bootstrap, independent of the unreadable session cookie. Validate same-origin Origin and CSRF before mutation. This contract does not implement or provision the session/CSRF exchange. |
| `body` | body | yes | `PreviewRequest` |  |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `202` | Accepted for asynchronous processing; not a completed effect. | application/json (Preview) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `409` | idempotency_conflict/reconcile_idempotency, binding_conflict/refresh_snapshot, or retry_requires_reconciliation/refresh_snapshot. No additional effect. | application/json (allOf&lt;ApiError, object&gt;) |
| `412` | precondition_failed; recovery=refresh_snapshot. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `413` | request_too_large; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `415` | unsupported_media_type; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `428` | precondition_required; recovery=refresh_snapshot. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "body": {
    "configurationRevisionId": "example"
  },
  "content_type": "application/json",
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "header",
      "name": "If-Match",
      "value": "\"A\""
    },
    {
      "in": "header",
      "name": "Idempotency-Key",
      "value": "AAAAAAAAAAAAAAAA"
    },
    {
      "in": "header",
      "name": "X-CSRF-Token",
      "value": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.previews().create(/* projectId */ "example", /* If-Match */ "\"A\"", /* Idempotency-Key */ "AAAAAAAAAAAAAAAA", /* X-CSRF-Token */ "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA", /* body */ {"configurationRevisionId": "example"});
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJjcmVhdGVQcmV2aWV3In0 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJwcmV2aWV3cygpLmdldCIsIm1ldGhvZCI6IkdFVCIsIm9wZXJhdGlvbl9pZCI6ImdldFByZXZpZXciLCJwYXRoIjoiL3YxL3Byb2plY3RzL3twcm9qZWN0SWR9L3ByZXZpZXdzL3twcmV2aWV3SWR9IiwicmVzb3VyY2UiOiJwcmV2aWV3cygpIiwic2VjdGlvbl9zaGEyNTYiOiJmNGQ2NGU0YTRlNmYzYzY1YmNhMTk2NTJhYjBjNDkyNGIyZjc2N2JkZGFkYTU3MzJmYzczZjE3NjBmMzk1OTEyIiwic2lnbmF0dXJlX3NoYTI1NiI6IjhiZGU5NDRlNjA5ODExYjU2ZjQxN2I3NTNjZTdkNjEyNjI0MDEzN2VmM2IxOGViOWU1YjRmZDgwMGFhYmUwZjEifQ -->
### `client.previews().get`

Operation ID: `getPreview`  
Route: `GET` `/v1/projects/{projectId}/previews/{previewId}`  
Equivalent member: `client.getPreview`  

#### Signature

```java
public Preview get(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<Preview> getAsync(OpaqueId projectId, OpaqueId previewId)
public ApiResponse<Preview> getWithResponse(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<ApiResponse<Preview>> getWithResponseAsync(OpaqueId projectId, OpaqueId previewId)
public Preview get(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<Preview> getAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public ApiResponse<Preview> getWithResponse(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<Preview>> getWithResponseAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `previewId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (Preview) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "path",
      "name": "previewId",
      "value": "example"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.previews().get(/* projectId */ "example", /* previewId */ "example");
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRQcmV2aWV3In0 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJwcmV2aWV3cygpLmdldEV2ZW50cyIsIm1ldGhvZCI6IkdFVCIsIm9wZXJhdGlvbl9pZCI6ImdldFByZXZpZXdFdmVudHMiLCJwYXRoIjoiL3YxL3Byb2plY3RzL3twcm9qZWN0SWR9L3ByZXZpZXdzL3twcmV2aWV3SWR9L2V2ZW50cyIsInJlc291cmNlIjoicHJldmlld3MoKSIsInNlY3Rpb25fc2hhMjU2IjoiNDNlMDVhYjM1N2U4YmU0MGU0NzUxMjUyNzM3OTExYzAzZmNkMjliNjU0NDYzYmM3MjgxMDE4NmQ0OTY4YmZlYSIsInNpZ25hdHVyZV9zaGEyNTYiOiI0OWQ2YjlhZTI0MmEwNmM1MjJjNzZkMzMyMTlmMzYzNTIwMGRlNTAzYmQ4NDZiNjEzZDllN2RjZmNkY2RhM2RhIn0 -->
### `client.previews().getEvents`

Operation ID: `getPreviewEvents`  
Route: `GET` `/v1/projects/{projectId}/previews/{previewId}/events`  
Equivalent member: `client.getPreviewEvents`  

#### Signature

```java
public EventPage getEvents(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<EventPage> getEventsAsync(OpaqueId projectId, OpaqueId previewId)
public ApiResponse<EventPage> getEventsWithResponse(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<ApiResponse<EventPage>> getEventsWithResponseAsync(OpaqueId projectId, OpaqueId previewId)
public EventPage getEvents(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<EventPage> getEventsAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public ApiResponse<EventPage> getEventsWithResponse(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<EventPage>> getEventsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public EventPage getEvents(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID)
public CompletableFuture<EventPage> getEventsAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID)
public ApiResponse<EventPage> getEventsWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID)
public CompletableFuture<ApiResponse<EventPage>> getEventsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID)
public EventPage getEvents(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID, RequestOptions requestOptions)
public CompletableFuture<EventPage> getEventsAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID, RequestOptions requestOptions)
public ApiResponse<EventPage> getEventsWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<EventPage>> getEventsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `previewId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `cursor` | `query` | no | `Cursor` | Opaque scope-bound continuation, never an offset or authority token. Expired/gap = 410 refresh_snapshot; invalid/tampered/wrong filters = 422. Denied objects remain uniform404. |
| `limit` | `query` | no | `integer` | Maximum page size; default 50. |
| `Last-Event-ID` | `header` | no | `Cursor` | SSE resume cursor; replay begins strictly after it. If query cursor also occurs the two must match, otherwise 422. Reauthorization is mandatory on reconnect. |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (EventPage), text/event-stream (string) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `410` | cursor_expired; recovery=refresh_snapshot. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "path",
      "name": "previewId",
      "value": "example"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.previews().getEvents(/* projectId */ "example", /* previewId */ "example", /* optional: cursor, limit, Last-Event-ID */);
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRQcmV2aWV3RXZlbnRzIn0 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJwcmV2aWV3cygpLmdldExvZ3MiLCJtZXRob2QiOiJHRVQiLCJvcGVyYXRpb25faWQiOiJnZXRQcmV2aWV3TG9ncyIsInBhdGgiOiIvdjEvcHJvamVjdHMve3Byb2plY3RJZH0vcHJldmlld3Mve3ByZXZpZXdJZH0vbG9ncyIsInJlc291cmNlIjoicHJldmlld3MoKSIsInNlY3Rpb25fc2hhMjU2IjoiMTQxMjE5YWRhZjYxZjY5YzY2ODgwMGYwMWRlMmMyOTEzZDYwNTU4N2E2NGM1ZGQwODZkYTU4NDU0Mjk3OTk5NSIsInNpZ25hdHVyZV9zaGEyNTYiOiI2M2FjNzFjNWVmNDRkY2M4ODZiYTY5NzMzMjVlMzgyY2JhMjBkZWZjNzY0NGJkZWUxM2NhZjA2ZGMxNDQ3MDZkIn0 -->
### `client.previews().getLogs`

Operation ID: `getPreviewLogs`  
Route: `GET` `/v1/projects/{projectId}/previews/{previewId}/logs`  
Equivalent member: `client.getPreviewLogs`  

#### Signature

```java
public LogPage getLogs(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<LogPage> getLogsAsync(OpaqueId projectId, OpaqueId previewId)
public ApiResponse<LogPage> getLogsWithResponse(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<ApiResponse<LogPage>> getLogsWithResponseAsync(OpaqueId projectId, OpaqueId previewId)
public LogPage getLogs(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<LogPage> getLogsAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public ApiResponse<LogPage> getLogsWithResponse(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<LogPage>> getLogsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public LogPage getLogs(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId)
public CompletableFuture<LogPage> getLogsAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId)
public ApiResponse<LogPage> getLogsWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId)
public CompletableFuture<ApiResponse<LogPage>> getLogsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId)
public LogPage getLogs(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId, RequestOptions requestOptions)
public CompletableFuture<LogPage> getLogsAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId, RequestOptions requestOptions)
public ApiResponse<LogPage> getLogsWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<LogPage>> getLogsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `previewId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `cursor` | `query` | no | `Cursor` | Opaque scope-bound continuation, never an offset or authority token. Expired/gap = 410 refresh_snapshot; invalid/tampered/wrong filters = 422. Denied objects remain uniform404. |
| `limit` | `query` | no | `integer` | Maximum page size; default 50. |
| `level` | `query` | no | `string` |  |
| `phaseId` | `query` | no | `OpaqueId` |  |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (LogPage) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `410` | cursor_expired; recovery=refresh_snapshot. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "path",
      "name": "previewId",
      "value": "example"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.previews().getLogs(/* projectId */ "example", /* previewId */ "example", /* optional: cursor, limit, level, phaseId */);
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRQcmV2aWV3TG9ncyJ9 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJwcmV2aWV3cygpLmxpc3QiLCJtZXRob2QiOiJHRVQiLCJvcGVyYXRpb25faWQiOiJsaXN0UHJldmlld3MiLCJwYXRoIjoiL3YxL3Byb2plY3RzL3twcm9qZWN0SWR9L3ByZXZpZXdzIiwicmVzb3VyY2UiOiJwcmV2aWV3cygpIiwic2VjdGlvbl9zaGEyNTYiOiJlM2VjNjNjZDM5ODRlYmI0NGYxNzBiNTJkZjZiNGE1ODRhNTUyMDFjM2VjMTNmY2VhYTMwMjc4NDhhNDYzYjIwIiwic2lnbmF0dXJlX3NoYTI1NiI6IjQyOTNhYmRkNzk3MjRmZmQwYmZiMmQxNDJmZTI3Mzc4YmIxMjI0N2ZjZjdmMWFiNTZiMDAxZGRiZjY4NmZkNTcifQ -->
### `client.previews().list`

Operation ID: `listPreviews`  
Route: `GET` `/v1/projects/{projectId}/previews`  
Equivalent member: `client.listPreviews`  

#### Signature

```java
public PreviewPage list(OpaqueId projectId)
public CompletableFuture<PreviewPage> listAsync(OpaqueId projectId)
public ApiResponse<PreviewPage> listWithResponse(OpaqueId projectId)
public CompletableFuture<ApiResponse<PreviewPage>> listWithResponseAsync(OpaqueId projectId)
public PreviewPage list(OpaqueId projectId, RequestOptions requestOptions)
public CompletableFuture<PreviewPage> listAsync(OpaqueId projectId, RequestOptions requestOptions)
public ApiResponse<PreviewPage> listWithResponse(OpaqueId projectId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<PreviewPage>> listWithResponseAsync(OpaqueId projectId, RequestOptions requestOptions)
public PreviewPage list(OpaqueId projectId, Cursor cursor, Long limit)
public CompletableFuture<PreviewPage> listAsync(OpaqueId projectId, Cursor cursor, Long limit)
public ApiResponse<PreviewPage> listWithResponse(OpaqueId projectId, Cursor cursor, Long limit)
public CompletableFuture<ApiResponse<PreviewPage>> listWithResponseAsync(OpaqueId projectId, Cursor cursor, Long limit)
public PreviewPage list(OpaqueId projectId, Cursor cursor, Long limit, RequestOptions requestOptions)
public CompletableFuture<PreviewPage> listAsync(OpaqueId projectId, Cursor cursor, Long limit, RequestOptions requestOptions)
public ApiResponse<PreviewPage> listWithResponse(OpaqueId projectId, Cursor cursor, Long limit, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<PreviewPage>> listWithResponseAsync(OpaqueId projectId, Cursor cursor, Long limit, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `cursor` | `query` | no | `Cursor` | Opaque scope-bound continuation, never an offset or authority token. Expired/gap = 410 refresh_snapshot; invalid/tampered/wrong filters = 422. Denied objects remain uniform404. |
| `limit` | `query` | no | `integer` | Maximum page size; default 50. |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (PreviewPage) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `410` | cursor_expired; recovery=refresh_snapshot. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.previews().list(/* projectId */ "example", /* optional: cursor, limit */);
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJsaXN0UHJldmlld3MifQ -->

## Resource `projects()`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJwcm9qZWN0cygpLmdldCIsIm1ldGhvZCI6IkdFVCIsIm9wZXJhdGlvbl9pZCI6ImdldFByb2plY3QiLCJwYXRoIjoiL3YxL3Byb2plY3RzL3twcm9qZWN0SWR9IiwicmVzb3VyY2UiOiJwcm9qZWN0cygpIiwic2VjdGlvbl9zaGEyNTYiOiIyNDg1NDkyYjhhZmZmZGJmNzE3NzQ1YTEzM2Q0NWVkNTcxZWZlYmJmMjI2NGQyNDU1MjkzOTYzNjVkNjBhYzVhIiwic2lnbmF0dXJlX3NoYTI1NiI6ImQ3ZGViODA0OTk0ZjQ3Mjc0M2E5NjUwOGYzOTdlNTUwNTg5ODU2MDNhYjVkYTEzZDlmMWNmODgyY2M4Mjc4ZTYifQ -->
### `client.projects().get`

Operation ID: `getProject`  
Route: `GET` `/v1/projects/{projectId}`  
Equivalent member: `client.getProject`  

#### Signature

```java
public Project get(OpaqueId projectId)
public CompletableFuture<Project> getAsync(OpaqueId projectId)
public ApiResponse<Project> getWithResponse(OpaqueId projectId)
public CompletableFuture<ApiResponse<Project>> getWithResponseAsync(OpaqueId projectId)
public Project get(OpaqueId projectId, RequestOptions requestOptions)
public CompletableFuture<Project> getAsync(OpaqueId projectId, RequestOptions requestOptions)
public ApiResponse<Project> getWithResponse(OpaqueId projectId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<Project>> getWithResponseAsync(OpaqueId projectId, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (Project) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.projects().get(/* projectId */ "example");
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRQcm9qZWN0In0 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJwcm9qZWN0cygpLmxpc3QiLCJtZXRob2QiOiJHRVQiLCJvcGVyYXRpb25faWQiOiJsaXN0UHJvamVjdHMiLCJwYXRoIjoiL3YxL3Byb2plY3RzIiwicmVzb3VyY2UiOiJwcm9qZWN0cygpIiwic2VjdGlvbl9zaGEyNTYiOiJjNjU3NzhlNTY5NjRkZjZmM2QyMGFiN2Q4MTEzOGU5ODhhNTMzOWZlNGJkMmVhNzIxMzg3MjJmYjcyNWRjZmUzIiwic2lnbmF0dXJlX3NoYTI1NiI6IjcwYTBlZDM0MTg0YTlmN2Y1OWJjMjJiMWYwMTQ4NWFmMjMwYmYwOGQ4YTkwYjMwMDBjODdjMTRiOGNkZDEzY2UifQ -->
### `client.projects().list`

Operation ID: `listProjects`  
Route: `GET` `/v1/projects`  
Equivalent member: `client.listProjects`  

#### Signature

```java
public ProjectPage list()
public CompletableFuture<ProjectPage> listAsync()
public ApiResponse<ProjectPage> listWithResponse()
public CompletableFuture<ApiResponse<ProjectPage>> listWithResponseAsync()
public ProjectPage list(RequestOptions requestOptions)
public CompletableFuture<ProjectPage> listAsync(RequestOptions requestOptions)
public ApiResponse<ProjectPage> listWithResponse(RequestOptions requestOptions)
public CompletableFuture<ApiResponse<ProjectPage>> listWithResponseAsync(RequestOptions requestOptions)
public ProjectPage list(Cursor cursor, Long limit, String queryValue)
public CompletableFuture<ProjectPage> listAsync(Cursor cursor, Long limit, String queryValue)
public ApiResponse<ProjectPage> listWithResponse(Cursor cursor, Long limit, String queryValue)
public CompletableFuture<ApiResponse<ProjectPage>> listWithResponseAsync(Cursor cursor, Long limit, String queryValue)
public ProjectPage list(Cursor cursor, Long limit, String queryValue, RequestOptions requestOptions)
public CompletableFuture<ProjectPage> listAsync(Cursor cursor, Long limit, String queryValue, RequestOptions requestOptions)
public ApiResponse<ProjectPage> listWithResponse(Cursor cursor, Long limit, String queryValue, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<ProjectPage>> listWithResponseAsync(Cursor cursor, Long limit, String queryValue, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `cursor` | `query` | no | `Cursor` | Opaque scope-bound continuation, never an offset or authority token. Expired/gap = 410 refresh_snapshot; invalid/tampered/wrong filters = 422. Denied objects remain uniform404. |
| `limit` | `query` | no | `integer` | Maximum page size; default 50. |
| `query` | `query` | no | `string` | Display-name substring filter, case-insensitive Unicode NFC matching. Bound to pagination cursor. |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (ProjectPage) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `410` | cursor_expired; recovery=refresh_snapshot. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": []
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.projects().list(/* optional: cursor, limit, query */);
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJsaXN0UHJvamVjdHMifQ -->

## Resource `sources()`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJzb3VyY2VzKCkuY3JlYXRlUmV2aXNpb24iLCJtZXRob2QiOiJQT1NUIiwib3BlcmF0aW9uX2lkIjoiY3JlYXRlU291cmNlUmV2aXNpb24iLCJwYXRoIjoiL3YxL3Byb2plY3RzL3twcm9qZWN0SWR9L3NvdXJjZS1yZXZpc2lvbnMiLCJyZXNvdXJjZSI6InNvdXJjZXMoKSIsInNlY3Rpb25fc2hhMjU2IjoiOGVlNWY5N2ZhNzUyNTQ1ZTVhYzhkZDYzNDM3NTFiN2EyNDExYmNlNzdlNTJiZDEyYTVlN2U4NWU1NDJiZWE2YyIsInNpZ25hdHVyZV9zaGEyNTYiOiI4ODhlY2M0ZmFjMTE3OWIyYjgxZjU2MDE3NjRhZTkyZTc5Mzc2ZmU3ZGM3ZmM2NGIzY2M2NmE1YWEyOGIzMThmIn0 -->
### `client.sources().createRevision`

Operation ID: `createSourceRevision`  
Route: `POST` `/v1/projects/{projectId}/source-revisions`  
Equivalent member: `client.createSourceRevision`  

#### Signature

```java
public SourceRevision createRevision(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body)
public CompletableFuture<SourceRevision> createRevisionAsync(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body)
public ApiResponse<SourceRevision> createRevisionWithResponse(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body)
public CompletableFuture<ApiResponse<SourceRevision>> createRevisionWithResponseAsync(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body)
public SourceRevision createRevision(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body, RequestOptions requestOptions)
public CompletableFuture<SourceRevision> createRevisionAsync(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body, RequestOptions requestOptions)
public ApiResponse<SourceRevision> createRevisionWithResponse(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<SourceRevision>> createRevisionWithResponseAsync(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `Idempotency-Key` | `header` | yes | `string` | Required on every mutation. Scope = organization + project + operation; fingerprint includes raw body bytes, media type, resource and If-Match. Same key/content replays the same receipt; changed content is 409. Retained for 86400 seconds; reconcile an ambiguous outcome within retention before retry, never silently allocate a new key. |
| `X-CSRF-Token` | `header` | yes | `string` | Session-bound synchronizer token from the trusted BFF bootstrap, independent of the unreadable session cookie. Validate same-origin Origin and CSRF before mutation. This contract does not implement or provision the session/CSRF exchange. |
| `displayName` | `query` | yes | `string` | Escaped display text only, never used as a filename or storage key; included in idempotency fingerprint. |
| `body` | body | yes | `any` |  |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `202` | Accepted for asynchronous processing; not a completed effect. | application/json (SourceRevision) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `409` | idempotency_conflict/reconcile_idempotency, binding_conflict/refresh_snapshot, or retry_requires_reconciliation/refresh_snapshot. No additional effect. | application/json (allOf&lt;ApiError, object&gt;) |
| `413` | request_too_large; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `415` | unsupported_media_type; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "body": "example",
  "content_type": "application/json",
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "header",
      "name": "Idempotency-Key",
      "value": "AAAAAAAAAAAAAAAA"
    },
    {
      "in": "header",
      "name": "X-CSRF-Token",
      "value": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"
    },
    {
      "in": "query",
      "name": "displayName",
      "value": "example"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.sources().createRevision(/* projectId */ "example", /* Idempotency-Key */ "AAAAAAAAAAAAAAAA", /* X-CSRF-Token */ "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA", /* displayName */ "example", /* body */ "example");
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJjcmVhdGVTb3VyY2VSZXZpc2lvbiJ9 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJzb3VyY2VzKCkuZ2V0UmV2aXNpb24iLCJtZXRob2QiOiJHRVQiLCJvcGVyYXRpb25faWQiOiJnZXRTb3VyY2VSZXZpc2lvbiIsInBhdGgiOiIvdjEvcHJvamVjdHMve3Byb2plY3RJZH0vc291cmNlLXJldmlzaW9ucy97cmV2aXNpb25JZH0iLCJyZXNvdXJjZSI6InNvdXJjZXMoKSIsInNlY3Rpb25fc2hhMjU2IjoiMGI0MDZjMzRlN2YzYTg4ZTc0MGQzNTAyMzA3MDExZmY0MjllOTE3NWNlMjBjYzY1MjM5NGNlMTM2ZTMzMGY2MiIsInNpZ25hdHVyZV9zaGEyNTYiOiI2OGQwN2FkZmNjNTUwMGI0OWVlNDBhYmI3Y2FiYWYwMGM2MmM2NzNiYTNiMjgwMGNlMGRiOWFlZjJiMTFkM2E3In0 -->
### `client.sources().getRevision`

Operation ID: `getSourceRevision`  
Route: `GET` `/v1/projects/{projectId}/source-revisions/{revisionId}`  
Equivalent member: `client.getSourceRevision`  

#### Signature

```java
public SourceRevision getRevision(OpaqueId projectId, OpaqueId revisionId)
public CompletableFuture<SourceRevision> getRevisionAsync(OpaqueId projectId, OpaqueId revisionId)
public ApiResponse<SourceRevision> getRevisionWithResponse(OpaqueId projectId, OpaqueId revisionId)
public CompletableFuture<ApiResponse<SourceRevision>> getRevisionWithResponseAsync(OpaqueId projectId, OpaqueId revisionId)
public SourceRevision getRevision(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public CompletableFuture<SourceRevision> getRevisionAsync(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public ApiResponse<SourceRevision> getRevisionWithResponse(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<SourceRevision>> getRevisionWithResponseAsync(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| `projectId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |
| `revisionId` | `path` | yes | `OpaqueId` | Opaque identity; authorize organization/project and verify every parent relation before lookup or mutation. Knowledge of an ID grants no access. |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authorized resource snapshot. | application/json (SourceRevision) |
| `401` | unauthenticated; recovery=authenticate. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `403` | forbidden; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `404` | not_found; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `406` | not_acceptable; recovery=none. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `422` | invalid_request, source_not_valid or cursor_invalid; never reinterpret an invalid source as ready. | application/json (allOf&lt;ApiError, object&gt;) |
| `429` | rate_limited; recovery=retry_same_request. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `500` | internal_error; recovery=reconcile_idempotency. See the normative error mapping and operation retry policy. | application/json (allOf&lt;ApiError, object&gt;) |
| `503` | configuration_required/configure_authority when approved JackAI exchange or product configuration is absent; authority_unavailable/retry_same_request on outage/timeout. No fallback identity, cached authorization or synthetic data. | application/json (allOf&lt;ApiError, object&gt;) |

#### Canonical required-input example

```json
{
  "parameters": [
    {
      "in": "path",
      "name": "projectId",
      "value": "example"
    },
    {
      "in": "path",
      "name": "revisionId",
      "value": "example"
    }
  ]
}
```

#### SDK call example

Example status: `generated`  
```java
var result = client.sources().getRevision(/* projectId */ "example", /* revisionId */ "example");
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRTb3VyY2VSZXZpc2lvbiJ9 -->

