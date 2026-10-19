# OmniWrap Java API

<!-- omniwrap-api-reference eyJjb250cmFjdF9maW5nZXJwcmludCI6IjU2ZDRmMDhmN2FkMzg0ZTI0NzZmMTMxY2MzY2I2YzlkYTFkMjk0NTg2NWI0Y2QzODJlZWNhMzMwY2NkYTg4MDgiLCJvcGVyYXRpb25fY291bnQiOjE2LCJyZW5kZXJlciI6ImphdmEiLCJ2ZXJzaW9uIjoiMS40LjAifQ -->

This generated index is tied to Semantic IR `1.14.0` and contract fingerprint `56d4f08f7ad384e2476f131cc3cb6c9da1d2945865b4cd382eeca330ccda8808`. Every operation below is rendered from the same semantic contract and artifact-attested public member allocation as the SDK.

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

## Resource `artifacts`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJnZXRBcnRpZmFjdCIsIm1ldGhvZCI6IkdFVCIsIm9wZXJhdGlvbl9pZCI6ImdldEFydGlmYWN0IiwicGF0aCI6Ii92MS9wcm9qZWN0cy97cHJvamVjdElkfS9hcnRpZmFjdHMve2FydGlmYWN0SWR9IiwicmVzb3VyY2UiOiJhcnRpZmFjdHMiLCJzZWN0aW9uX3NoYTI1NiI6IjBkZDA4NTNhNTNkOWUzZmRmM2IyOWYxY2RkZThhNmQ1YzkyY2ExMzAyNjRhMmU3YWM4ODUwYzA2YTVkOTZkZGQiLCJzaWduYXR1cmVfc2hhMjU2IjoiM2JjNDgyZWMyZDJkMzE3MDFhMDdhNWVlMTUyMDBlOWRjN2EwMWExNDNmZjcyYzUwNTQ3OTE0ODQ2NDBjMjFlMiJ9 -->
### `client.getArtifact`

Operation ID: `getArtifact`  
Route: `GET` `/v1/projects/{projectId}/artifacts/{artifactId}`  

#### Signature

```java
public Artifact getArtifact(OpaqueId projectId, OpaqueId artifactId)
public ApiResponse<Artifact> getArtifactWithResponse(OpaqueId projectId, OpaqueId artifactId)
public CompletableFuture<ApiResponse<Artifact>> getArtifactWithResponseAsync(OpaqueId projectId, OpaqueId artifactId)
public CompletableFuture<Artifact> getArtifactAsync(OpaqueId projectId, OpaqueId artifactId)
public Artifact getArtifact(OpaqueId projectId, OpaqueId artifactId, RequestOptions requestOptions)
public CompletableFuture<Artifact> getArtifactAsync(OpaqueId projectId, OpaqueId artifactId, RequestOptions requestOptions)
public ApiResponse<Artifact> getArtifactWithResponse(OpaqueId projectId, OpaqueId artifactId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<Artifact>> getArtifactWithResponseAsync(OpaqueId projectId, OpaqueId artifactId, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRBcnRpZmFjdCJ9 -->

## Resource `configurations`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJjcmVhdGVDb25maWd1cmF0aW9uUmV2aXNpb24iLCJtZXRob2QiOiJQT1NUIiwib3BlcmF0aW9uX2lkIjoiY3JlYXRlQ29uZmlndXJhdGlvblJldmlzaW9uIiwicGF0aCI6Ii92MS9wcm9qZWN0cy97cHJvamVjdElkfS9jb25maWd1cmF0aW9uLXJldmlzaW9ucyIsInJlc291cmNlIjoiY29uZmlndXJhdGlvbnMiLCJzZWN0aW9uX3NoYTI1NiI6IjIyNjFjZDhiMGU0Mzk4Zjc4ZmZlMmVlNGRkZjBkNjEzMDc4MzU4YWRhM2NhMzA5YThmYjM3ZjlhYmZiNjM0ZTgiLCJzaWduYXR1cmVfc2hhMjU2IjoiNzkyMDI4YThhNzNkZGY0YTExNTI2YmI3ZDg3YWYwZmJlNzllYWRhMmFjNzIyZmRlODE5ZWRjNjgxZGI4N2RmYyJ9 -->
### `client.createConfigurationRevision`

Operation ID: `createConfigurationRevision`  
Route: `POST` `/v1/projects/{projectId}/configuration-revisions`  

#### Signature

```java
public ConfigurationRevision createConfigurationRevision(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body)
public ApiResponse<ConfigurationRevision> createConfigurationRevisionWithResponse(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body)
public CompletableFuture<ApiResponse<ConfigurationRevision>> createConfigurationRevisionWithResponseAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body)
public CompletableFuture<ConfigurationRevision> createConfigurationRevisionAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body)
public ConfigurationRevision createConfigurationRevision(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body, RequestOptions requestOptions)
public CompletableFuture<ConfigurationRevision> createConfigurationRevisionAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body, RequestOptions requestOptions)
public ApiResponse<ConfigurationRevision> createConfigurationRevisionWithResponse(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<ConfigurationRevision>> createConfigurationRevisionWithResponseAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, ConfigurationRequest body, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJjcmVhdGVDb25maWd1cmF0aW9uUmV2aXNpb24ifQ -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJnZXRDb25maWd1cmF0aW9uUmV2aXNpb24iLCJtZXRob2QiOiJHRVQiLCJvcGVyYXRpb25faWQiOiJnZXRDb25maWd1cmF0aW9uUmV2aXNpb24iLCJwYXRoIjoiL3YxL3Byb2plY3RzL3twcm9qZWN0SWR9L2NvbmZpZ3VyYXRpb24tcmV2aXNpb25zL3tyZXZpc2lvbklkfSIsInJlc291cmNlIjoiY29uZmlndXJhdGlvbnMiLCJzZWN0aW9uX3NoYTI1NiI6IjlhYTdmM2YzYjE3ZGYwMzgzNmViMWU3ODdmOTIwNzM4ODJjYjcyNzU0ZjNkNWNjNzI0YmVjYzRlZTBlYWVlNzEiLCJzaWduYXR1cmVfc2hhMjU2IjoiNzRlZjdkNWM3NzI0YjE1NDI3MjBlMDljODg0NzVmYmY4ODhmMjg4NjU3ZWJlMjFjOGE4YTYyNTcxNDFjYTkxMiJ9 -->
### `client.getConfigurationRevision`

Operation ID: `getConfigurationRevision`  
Route: `GET` `/v1/projects/{projectId}/configuration-revisions/{revisionId}`  

#### Signature

```java
public ConfigurationRevision getConfigurationRevision(OpaqueId projectId, OpaqueId revisionId)
public ApiResponse<ConfigurationRevision> getConfigurationRevisionWithResponse(OpaqueId projectId, OpaqueId revisionId)
public CompletableFuture<ApiResponse<ConfigurationRevision>> getConfigurationRevisionWithResponseAsync(OpaqueId projectId, OpaqueId revisionId)
public CompletableFuture<ConfigurationRevision> getConfigurationRevisionAsync(OpaqueId projectId, OpaqueId revisionId)
public ConfigurationRevision getConfigurationRevision(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public CompletableFuture<ConfigurationRevision> getConfigurationRevisionAsync(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public ApiResponse<ConfigurationRevision> getConfigurationRevisionWithResponse(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<ConfigurationRevision>> getConfigurationRevisionWithResponseAsync(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRDb25maWd1cmF0aW9uUmV2aXNpb24ifQ -->

## Resource `context`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJnZXRVc2VyQ29udGV4dCIsIm1ldGhvZCI6IkdFVCIsIm9wZXJhdGlvbl9pZCI6ImdldFVzZXJDb250ZXh0IiwicGF0aCI6Ii92MS9tZS9jb250ZXh0IiwicmVzb3VyY2UiOiJjb250ZXh0Iiwic2VjdGlvbl9zaGEyNTYiOiIxYWJlODliMDk1ZGQyMmJjNjFhYTgwNTI2NmFhMTRhNjZmYWY4MTE2MDlhYzcyNWFkZjU5OTFhNWNhNmQwYzc4Iiwic2lnbmF0dXJlX3NoYTI1NiI6IjM2ZTg5OGIwNGY1ZGY2ZDVmMGExNzU5ODA5NWIzMjliZTRiN2NmY2I0NTQxODU2NjI5ZDkwNmViNTlkMDI1NDkifQ -->
### `client.getUserContext`

Operation ID: `getUserContext`  
Route: `GET` `/v1/me/context`  

#### Signature

```java
public UserContext getUserContext()
public ApiResponse<UserContext> getUserContextWithResponse()
public CompletableFuture<ApiResponse<UserContext>> getUserContextWithResponseAsync()
public CompletableFuture<UserContext> getUserContextAsync()
public UserContext getUserContext(RequestOptions requestOptions)
public CompletableFuture<UserContext> getUserContextAsync(RequestOptions requestOptions)
public ApiResponse<UserContext> getUserContextWithResponse(RequestOptions requestOptions)
public CompletableFuture<ApiResponse<UserContext>> getUserContextWithResponseAsync(RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRVc2VyQ29udGV4dCJ9 -->

## Resource `evidence`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJnZXRFdmlkZW5jZSIsIm1ldGhvZCI6IkdFVCIsIm9wZXJhdGlvbl9pZCI6ImdldEV2aWRlbmNlIiwicGF0aCI6Ii92MS9wcm9qZWN0cy97cHJvamVjdElkfS9ldmlkZW5jZS97ZXZpZGVuY2VJZH0iLCJyZXNvdXJjZSI6ImV2aWRlbmNlIiwic2VjdGlvbl9zaGEyNTYiOiI0MDlhMjI5MTZhZDI0ZTA4MDM0ZTU0Y2ZhYTMzMDg5OWRkZDkwYTUwOWI4MWM3YjU5MjJkYzMwNDIwOGU1MDA3Iiwic2lnbmF0dXJlX3NoYTI1NiI6Ijk3Y2M5MDY3ZDRiMTUxNzYzMzAzNzNlZjZlM2I4YTBkZGY5YjA5N2U0MDM2NzU4ZWY1MjZhOWRlY2VjOTNjZmUifQ -->
### `client.getEvidence`

Operation ID: `getEvidence`  
Route: `GET` `/v1/projects/{projectId}/evidence/{evidenceId}`  

#### Signature

```java
public Evidence getEvidence(OpaqueId projectId, OpaqueId evidenceId)
public ApiResponse<Evidence> getEvidenceWithResponse(OpaqueId projectId, OpaqueId evidenceId)
public CompletableFuture<ApiResponse<Evidence>> getEvidenceWithResponseAsync(OpaqueId projectId, OpaqueId evidenceId)
public CompletableFuture<Evidence> getEvidenceAsync(OpaqueId projectId, OpaqueId evidenceId)
public Evidence getEvidence(OpaqueId projectId, OpaqueId evidenceId, RequestOptions requestOptions)
public CompletableFuture<Evidence> getEvidenceAsync(OpaqueId projectId, OpaqueId evidenceId, RequestOptions requestOptions)
public ApiResponse<Evidence> getEvidenceWithResponse(OpaqueId projectId, OpaqueId evidenceId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<Evidence>> getEvidenceWithResponseAsync(OpaqueId projectId, OpaqueId evidenceId, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRFdmlkZW5jZSJ9 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJsaXN0UHJldmlld0V2aWRlbmNlIiwibWV0aG9kIjoiR0VUIiwib3BlcmF0aW9uX2lkIjoibGlzdFByZXZpZXdFdmlkZW5jZSIsInBhdGgiOiIvdjEvcHJvamVjdHMve3Byb2plY3RJZH0vcHJldmlld3Mve3ByZXZpZXdJZH0vZXZpZGVuY2UiLCJyZXNvdXJjZSI6ImV2aWRlbmNlIiwic2VjdGlvbl9zaGEyNTYiOiJmM2EzMzgyMmRhZjY1MjY1ODkyM2QxOGE2OTA1ODg5Mjk0NDM3ZGZmYWExNTdiNTgwOTI0YWU1MGY4OGI2MDg1Iiwic2lnbmF0dXJlX3NoYTI1NiI6IjY3ZDMxYTcyNDAzZDVjODg5OGExM2I0YWQ3ZWIwNDc0NThjNDY3ZGY4MTVjYmU0Y2Q2YTk5ZDU0OTBiNTUyY2UifQ -->
### `client.listPreviewEvidence`

Operation ID: `listPreviewEvidence`  
Route: `GET` `/v1/projects/{projectId}/previews/{previewId}/evidence`  

#### Signature

```java
public EvidencePage listPreviewEvidence(OpaqueId projectId, OpaqueId previewId)
public ApiResponse<EvidencePage> listPreviewEvidenceWithResponse(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<ApiResponse<EvidencePage>> listPreviewEvidenceWithResponseAsync(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<EvidencePage> listPreviewEvidenceAsync(OpaqueId projectId, OpaqueId previewId)
public EvidencePage listPreviewEvidence(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public ApiResponse<EvidencePage> listPreviewEvidenceWithResponse(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<EvidencePage>> listPreviewEvidenceWithResponseAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<EvidencePage> listPreviewEvidenceAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public EvidencePage listPreviewEvidence(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability)
public ApiResponse<EvidencePage> listPreviewEvidenceWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability)
public CompletableFuture<ApiResponse<EvidencePage>> listPreviewEvidenceWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability)
public CompletableFuture<EvidencePage> listPreviewEvidenceAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability)
public EvidencePage listPreviewEvidence(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability, RequestOptions requestOptions)
public CompletableFuture<EvidencePage> listPreviewEvidenceAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability, RequestOptions requestOptions)
public ApiResponse<EvidencePage> listPreviewEvidenceWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<EvidencePage>> listPreviewEvidenceWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String gateId, String availability, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJsaXN0UHJldmlld0V2aWRlbmNlIn0 -->

## Resource `previews`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJjYW5jZWxQcmV2aWV3IiwibWV0aG9kIjoiUE9TVCIsIm9wZXJhdGlvbl9pZCI6ImNhbmNlbFByZXZpZXciLCJwYXRoIjoiL3YxL3Byb2plY3RzL3twcm9qZWN0SWR9L3ByZXZpZXdzL3twcmV2aWV3SWR9L2NhbmNlbCIsInJlc291cmNlIjoicHJldmlld3MiLCJzZWN0aW9uX3NoYTI1NiI6ImQ2MzE1MDEwNjNlZDk3YTA5YmQxYzgxNWRhNmY4OGI1OGM2NjAxZGM0NTI4MWRiMTEwMWJmZjI4YTBlNDc5YjkiLCJzaWduYXR1cmVfc2hhMjU2IjoiMjA3OTY3OWQyMmUwOGRlYTUwYzI2OTcxYjJmZjdkNDQ3MWE2Mjk3MDNiNmMzMjM1YzI3OGM2ZWY1YWM0MWEzNiJ9 -->
### `client.cancelPreview`

Operation ID: `cancelPreview`  
Route: `POST` `/v1/projects/{projectId}/previews/{previewId}/cancel`  

#### Signature

```java
public CancellationReceipt cancelPreview(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body)
public ApiResponse<CancellationReceipt> cancelPreviewWithResponse(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body)
public CompletableFuture<ApiResponse<CancellationReceipt>> cancelPreviewWithResponseAsync(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body)
public CompletableFuture<CancellationReceipt> cancelPreviewAsync(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body)
public CancellationReceipt cancelPreview(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body, RequestOptions requestOptions)
public CompletableFuture<CancellationReceipt> cancelPreviewAsync(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body, RequestOptions requestOptions)
public ApiResponse<CancellationReceipt> cancelPreviewWithResponse(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<CancellationReceipt>> cancelPreviewWithResponseAsync(OpaqueId projectId, OpaqueId previewId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, CancelRequest body, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJjYW5jZWxQcmV2aWV3In0 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJjcmVhdGVQcmV2aWV3IiwibWV0aG9kIjoiUE9TVCIsIm9wZXJhdGlvbl9pZCI6ImNyZWF0ZVByZXZpZXciLCJwYXRoIjoiL3YxL3Byb2plY3RzL3twcm9qZWN0SWR9L3ByZXZpZXdzIiwicmVzb3VyY2UiOiJwcmV2aWV3cyIsInNlY3Rpb25fc2hhMjU2IjoiZmI5OTcxN2E4ZTJmNzM0YmVjN2MzMjRkZTNiZTBlYWVkMjgzMTVhYjAxZmIzN2Q0NzlmNTNjMTExZGI5NjgyMyIsInNpZ25hdHVyZV9zaGEyNTYiOiI1ZThjOWVhNGM5ZWQ0ZTY1NTQxMmFkYjcyNGMwZjAzNjI2ZDA3ODFjYjEyMDk5MGNiNjMzNmY1OWU2NjM0ZGVkIn0 -->
### `client.createPreview`

Operation ID: `createPreview`  
Route: `POST` `/v1/projects/{projectId}/previews`  

#### Signature

```java
public Preview createPreview(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body)
public ApiResponse<Preview> createPreviewWithResponse(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body)
public CompletableFuture<ApiResponse<Preview>> createPreviewWithResponseAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body)
public CompletableFuture<Preview> createPreviewAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body)
public Preview createPreview(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body, RequestOptions requestOptions)
public CompletableFuture<Preview> createPreviewAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body, RequestOptions requestOptions)
public ApiResponse<Preview> createPreviewWithResponse(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<Preview>> createPreviewWithResponseAsync(OpaqueId projectId, StrongEtag ifMatch, String idempotencyKey, String xCSRFToken, PreviewRequest body, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJjcmVhdGVQcmV2aWV3In0 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJnZXRQcmV2aWV3IiwibWV0aG9kIjoiR0VUIiwib3BlcmF0aW9uX2lkIjoiZ2V0UHJldmlldyIsInBhdGgiOiIvdjEvcHJvamVjdHMve3Byb2plY3RJZH0vcHJldmlld3Mve3ByZXZpZXdJZH0iLCJyZXNvdXJjZSI6InByZXZpZXdzIiwic2VjdGlvbl9zaGEyNTYiOiI3NGNiZDNkNDY0ZDBjY2MwMzYxYWZkNjM5N2E1NWM0OTgyMTI2MmE1NDRlOGEyZTg0Nzk4OTU4YzhmYTg1NDFiIiwic2lnbmF0dXJlX3NoYTI1NiI6Ijc2MzYzZDBjMjUzNTYyNGQ4OWQxNzRhY2I2M2UxZjg5OTAxNzRkOTZjNTEyNTJmOGU0ODEzZDA4ZDQyZjhmMjcifQ -->
### `client.getPreview`

Operation ID: `getPreview`  
Route: `GET` `/v1/projects/{projectId}/previews/{previewId}`  

#### Signature

```java
public Preview getPreview(OpaqueId projectId, OpaqueId previewId)
public ApiResponse<Preview> getPreviewWithResponse(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<ApiResponse<Preview>> getPreviewWithResponseAsync(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<Preview> getPreviewAsync(OpaqueId projectId, OpaqueId previewId)
public Preview getPreview(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<Preview> getPreviewAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public ApiResponse<Preview> getPreviewWithResponse(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<Preview>> getPreviewWithResponseAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRQcmV2aWV3In0 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJnZXRQcmV2aWV3RXZlbnRzIiwibWV0aG9kIjoiR0VUIiwib3BlcmF0aW9uX2lkIjoiZ2V0UHJldmlld0V2ZW50cyIsInBhdGgiOiIvdjEvcHJvamVjdHMve3Byb2plY3RJZH0vcHJldmlld3Mve3ByZXZpZXdJZH0vZXZlbnRzIiwicmVzb3VyY2UiOiJwcmV2aWV3cyIsInNlY3Rpb25fc2hhMjU2IjoiZTU5ZDc0YWMwODNiYzRiYmIyODQyNGU4ZGMxODg4N2ZhYmI4MzJkNGIyZmM1YTRlYWIwZmRkMjQzYjg5OWNkZSIsInNpZ25hdHVyZV9zaGEyNTYiOiIzZDg0NzhlMTdiMWU3ZWU2NjQ2ODY5YTgyMjVmNTRlZjJlMWIzY2Q4ZDZiZTI2ZjU3NmI0MGFmZjg3YTNkM2Q3In0 -->
### `client.getPreviewEvents`

Operation ID: `getPreviewEvents`  
Route: `GET` `/v1/projects/{projectId}/previews/{previewId}/events`  

#### Signature

```java
public EventPage getPreviewEvents(OpaqueId projectId, OpaqueId previewId)
public ApiResponse<EventPage> getPreviewEventsWithResponse(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<ApiResponse<EventPage>> getPreviewEventsWithResponseAsync(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<EventPage> getPreviewEventsAsync(OpaqueId projectId, OpaqueId previewId)
public EventPage getPreviewEvents(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public ApiResponse<EventPage> getPreviewEventsWithResponse(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<EventPage>> getPreviewEventsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<EventPage> getPreviewEventsAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public EventPage getPreviewEvents(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID)
public ApiResponse<EventPage> getPreviewEventsWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID)
public CompletableFuture<ApiResponse<EventPage>> getPreviewEventsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID)
public CompletableFuture<EventPage> getPreviewEventsAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID)
public EventPage getPreviewEvents(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID, RequestOptions requestOptions)
public CompletableFuture<EventPage> getPreviewEventsAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID, RequestOptions requestOptions)
public ApiResponse<EventPage> getPreviewEventsWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<EventPage>> getPreviewEventsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, Cursor lastEventID, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRQcmV2aWV3RXZlbnRzIn0 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJnZXRQcmV2aWV3TG9ncyIsIm1ldGhvZCI6IkdFVCIsIm9wZXJhdGlvbl9pZCI6ImdldFByZXZpZXdMb2dzIiwicGF0aCI6Ii92MS9wcm9qZWN0cy97cHJvamVjdElkfS9wcmV2aWV3cy97cHJldmlld0lkfS9sb2dzIiwicmVzb3VyY2UiOiJwcmV2aWV3cyIsInNlY3Rpb25fc2hhMjU2IjoiZDEwNjMyNGUyY2VkNjcxYTA3Yzk5OGU0NzUzZTBhZTcwYjMzMWJiODg1MGU2YmNjMTgyYjJjNjEyZTEwOTJiYSIsInNpZ25hdHVyZV9zaGEyNTYiOiI4NjgwOTk3ZGRjMWVmN2I3NTlkNTUwNDNkNmE3ZWE3Y2Q3YWU1NDY1MDI3ZTk1NjM5OTg3NDg5NzAwYjc4NjhhIn0 -->
### `client.getPreviewLogs`

Operation ID: `getPreviewLogs`  
Route: `GET` `/v1/projects/{projectId}/previews/{previewId}/logs`  

#### Signature

```java
public LogPage getPreviewLogs(OpaqueId projectId, OpaqueId previewId)
public ApiResponse<LogPage> getPreviewLogsWithResponse(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<ApiResponse<LogPage>> getPreviewLogsWithResponseAsync(OpaqueId projectId, OpaqueId previewId)
public CompletableFuture<LogPage> getPreviewLogsAsync(OpaqueId projectId, OpaqueId previewId)
public LogPage getPreviewLogs(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public ApiResponse<LogPage> getPreviewLogsWithResponse(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<LogPage>> getPreviewLogsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public CompletableFuture<LogPage> getPreviewLogsAsync(OpaqueId projectId, OpaqueId previewId, RequestOptions requestOptions)
public LogPage getPreviewLogs(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId)
public ApiResponse<LogPage> getPreviewLogsWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId)
public CompletableFuture<ApiResponse<LogPage>> getPreviewLogsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId)
public CompletableFuture<LogPage> getPreviewLogsAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId)
public LogPage getPreviewLogs(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId, RequestOptions requestOptions)
public CompletableFuture<LogPage> getPreviewLogsAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId, RequestOptions requestOptions)
public ApiResponse<LogPage> getPreviewLogsWithResponse(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<LogPage>> getPreviewLogsWithResponseAsync(OpaqueId projectId, OpaqueId previewId, Cursor cursor, Long limit, String level, OpaqueId phaseId, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRQcmV2aWV3TG9ncyJ9 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJsaXN0UHJldmlld3MiLCJtZXRob2QiOiJHRVQiLCJvcGVyYXRpb25faWQiOiJsaXN0UHJldmlld3MiLCJwYXRoIjoiL3YxL3Byb2plY3RzL3twcm9qZWN0SWR9L3ByZXZpZXdzIiwicmVzb3VyY2UiOiJwcmV2aWV3cyIsInNlY3Rpb25fc2hhMjU2IjoiMTYyZGNjODA3Y2JkMWQ5MjBmOTYxNGExYWJjODcwNDgwZDNjOWY4NzM0MDQwMTMyOThmMGM1NThmNWUxYzQxNiIsInNpZ25hdHVyZV9zaGEyNTYiOiIwOWVkNTAyNWFlMWE1MzBlNmVkOTNiOTIyZGYwNjIzOGVjYjMyOGU3ODI1ZGM2ZjQzZmY0Y2YyNWRjNjM4YWM2In0 -->
### `client.listPreviews`

Operation ID: `listPreviews`  
Route: `GET` `/v1/projects/{projectId}/previews`  

#### Signature

```java
public PreviewPage listPreviews(OpaqueId projectId)
public ApiResponse<PreviewPage> listPreviewsWithResponse(OpaqueId projectId)
public CompletableFuture<ApiResponse<PreviewPage>> listPreviewsWithResponseAsync(OpaqueId projectId)
public CompletableFuture<PreviewPage> listPreviewsAsync(OpaqueId projectId)
public PreviewPage listPreviews(OpaqueId projectId, RequestOptions requestOptions)
public ApiResponse<PreviewPage> listPreviewsWithResponse(OpaqueId projectId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<PreviewPage>> listPreviewsWithResponseAsync(OpaqueId projectId, RequestOptions requestOptions)
public CompletableFuture<PreviewPage> listPreviewsAsync(OpaqueId projectId, RequestOptions requestOptions)
public PreviewPage listPreviews(OpaqueId projectId, Cursor cursor, Long limit)
public ApiResponse<PreviewPage> listPreviewsWithResponse(OpaqueId projectId, Cursor cursor, Long limit)
public CompletableFuture<ApiResponse<PreviewPage>> listPreviewsWithResponseAsync(OpaqueId projectId, Cursor cursor, Long limit)
public CompletableFuture<PreviewPage> listPreviewsAsync(OpaqueId projectId, Cursor cursor, Long limit)
public PreviewPage listPreviews(OpaqueId projectId, Cursor cursor, Long limit, RequestOptions requestOptions)
public CompletableFuture<PreviewPage> listPreviewsAsync(OpaqueId projectId, Cursor cursor, Long limit, RequestOptions requestOptions)
public ApiResponse<PreviewPage> listPreviewsWithResponse(OpaqueId projectId, Cursor cursor, Long limit, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<PreviewPage>> listPreviewsWithResponseAsync(OpaqueId projectId, Cursor cursor, Long limit, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJsaXN0UHJldmlld3MifQ -->

## Resource `projects`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJnZXRQcm9qZWN0IiwibWV0aG9kIjoiR0VUIiwib3BlcmF0aW9uX2lkIjoiZ2V0UHJvamVjdCIsInBhdGgiOiIvdjEvcHJvamVjdHMve3Byb2plY3RJZH0iLCJyZXNvdXJjZSI6InByb2plY3RzIiwic2VjdGlvbl9zaGEyNTYiOiJmNDNiYmFhZjhiN2EyZGEzNTk0ZGY2YTNiMTVkMzBmZmU2NTlhOWNlY2VjZTJmOTFlZGE3ZjcxOTIwM2JkNjA0Iiwic2lnbmF0dXJlX3NoYTI1NiI6Ijk3YmI0ZjJkZWU0ZTljNDEyYzc2ZTVhNDMyZTVjYzVmNzQ2OGUxNzU5NjI2YjViMDUxMGE1M2UwYzZlYjJhYWQifQ -->
### `client.getProject`

Operation ID: `getProject`  
Route: `GET` `/v1/projects/{projectId}`  

#### Signature

```java
public Project getProject(OpaqueId projectId)
public ApiResponse<Project> getProjectWithResponse(OpaqueId projectId)
public CompletableFuture<ApiResponse<Project>> getProjectWithResponseAsync(OpaqueId projectId)
public CompletableFuture<Project> getProjectAsync(OpaqueId projectId)
public Project getProject(OpaqueId projectId, RequestOptions requestOptions)
public CompletableFuture<Project> getProjectAsync(OpaqueId projectId, RequestOptions requestOptions)
public ApiResponse<Project> getProjectWithResponse(OpaqueId projectId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<Project>> getProjectWithResponseAsync(OpaqueId projectId, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRQcm9qZWN0In0 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJsaXN0UHJvamVjdHMiLCJtZXRob2QiOiJHRVQiLCJvcGVyYXRpb25faWQiOiJsaXN0UHJvamVjdHMiLCJwYXRoIjoiL3YxL3Byb2plY3RzIiwicmVzb3VyY2UiOiJwcm9qZWN0cyIsInNlY3Rpb25fc2hhMjU2IjoiZjI4YjgzYTRiZjk5ZjVhMDc4ZWU3MTEyMjgzMDU1ZmY2MWU5YWYzZGQ5ZGJhZGJlZjllZjBlYzY1MWNkNGJlMiIsInNpZ25hdHVyZV9zaGEyNTYiOiIwZjY2N2RkNGY5YjRmMDkxNWFiMjI3NjY1MDdiNjIyNDA0ZjRhOTVhNWRkNTQ1MWUyOWVjYWE1Yjg4OWJmY2E5In0 -->
### `client.listProjects`

Operation ID: `listProjects`  
Route: `GET` `/v1/projects`  

#### Signature

```java
public ProjectPage listProjects()
public ApiResponse<ProjectPage> listProjectsWithResponse()
public CompletableFuture<ApiResponse<ProjectPage>> listProjectsWithResponseAsync()
public CompletableFuture<ProjectPage> listProjectsAsync()
public ProjectPage listProjects(RequestOptions requestOptions)
public ApiResponse<ProjectPage> listProjectsWithResponse(RequestOptions requestOptions)
public CompletableFuture<ApiResponse<ProjectPage>> listProjectsWithResponseAsync(RequestOptions requestOptions)
public CompletableFuture<ProjectPage> listProjectsAsync(RequestOptions requestOptions)
public ProjectPage listProjects(Cursor cursor, Long limit, String queryValue)
public ApiResponse<ProjectPage> listProjectsWithResponse(Cursor cursor, Long limit, String queryValue)
public CompletableFuture<ApiResponse<ProjectPage>> listProjectsWithResponseAsync(Cursor cursor, Long limit, String queryValue)
public CompletableFuture<ProjectPage> listProjectsAsync(Cursor cursor, Long limit, String queryValue)
public ProjectPage listProjects(Cursor cursor, Long limit, String queryValue, RequestOptions requestOptions)
public CompletableFuture<ProjectPage> listProjectsAsync(Cursor cursor, Long limit, String queryValue, RequestOptions requestOptions)
public ApiResponse<ProjectPage> listProjectsWithResponse(Cursor cursor, Long limit, String queryValue, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<ProjectPage>> listProjectsWithResponseAsync(Cursor cursor, Long limit, String queryValue, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJsaXN0UHJvamVjdHMifQ -->

## Resource `sources`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJjcmVhdGVTb3VyY2VSZXZpc2lvbiIsIm1ldGhvZCI6IlBPU1QiLCJvcGVyYXRpb25faWQiOiJjcmVhdGVTb3VyY2VSZXZpc2lvbiIsInBhdGgiOiIvdjEvcHJvamVjdHMve3Byb2plY3RJZH0vc291cmNlLXJldmlzaW9ucyIsInJlc291cmNlIjoic291cmNlcyIsInNlY3Rpb25fc2hhMjU2IjoiMTRkOTEyZWNlYzAwMDIxYTk2MzVjZWM2NjNkZDg0M2I5M2JmN2Y5NTgzZGZkODVjM2ZhOWVjOTNjZjMzYTdlNyIsInNpZ25hdHVyZV9zaGEyNTYiOiJjOGY4MWI1MTNkMmE1NDUzMmI2OWMxYjQ3NDE3Y2I0ODQwOTg4YmYwYzdkNTlhMWJlNzBlMTFjZmY2ZWJhNjY4In0 -->
### `client.createSourceRevision`

Operation ID: `createSourceRevision`  
Route: `POST` `/v1/projects/{projectId}/source-revisions`  

#### Signature

```java
public SourceRevision createSourceRevision(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body)
public ApiResponse<SourceRevision> createSourceRevisionWithResponse(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body)
public CompletableFuture<ApiResponse<SourceRevision>> createSourceRevisionWithResponseAsync(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body)
public CompletableFuture<SourceRevision> createSourceRevisionAsync(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body)
public SourceRevision createSourceRevision(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body, RequestOptions requestOptions)
public CompletableFuture<SourceRevision> createSourceRevisionAsync(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body, RequestOptions requestOptions)
public ApiResponse<SourceRevision> createSourceRevisionWithResponse(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<SourceRevision>> createSourceRevisionWithResponseAsync(OpaqueId projectId, String idempotencyKey, String xCSRFToken, String displayName, Object body, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJjcmVhdGVTb3VyY2VSZXZpc2lvbiJ9 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6Imxhbmd1YWdlLWV4YW1wbGUtbm90LWdlbmVyYXRlZCIsImV4YW1wbGVfc3RhdHVzIjoidW5zdXBwb3J0ZWQiLCJtZW1iZXIiOiJnZXRTb3VyY2VSZXZpc2lvbiIsIm1ldGhvZCI6IkdFVCIsIm9wZXJhdGlvbl9pZCI6ImdldFNvdXJjZVJldmlzaW9uIiwicGF0aCI6Ii92MS9wcm9qZWN0cy97cHJvamVjdElkfS9zb3VyY2UtcmV2aXNpb25zL3tyZXZpc2lvbklkfSIsInJlc291cmNlIjoic291cmNlcyIsInNlY3Rpb25fc2hhMjU2IjoiMjc0M2VlODI5MTY2NmUwNTUzMGI1MzAzYTEwOTdjZWUwMTZiZmFmOGNmMmUzZWQ4ZjcyZWE2Yjk5ZjQxNmRlNCIsInNpZ25hdHVyZV9zaGEyNTYiOiI0Y2I1NTRhMzg3NWJmOWU2ZTNlMzRlZWQzMzU5ZTQzMGQzMDk1ZjBhODRjMGY0ZTJiMTIwZDBlYjMxMTU2OTdhIn0 -->
### `client.getSourceRevision`

Operation ID: `getSourceRevision`  
Route: `GET` `/v1/projects/{projectId}/source-revisions/{revisionId}`  

#### Signature

```java
public SourceRevision getSourceRevision(OpaqueId projectId, OpaqueId revisionId)
public ApiResponse<SourceRevision> getSourceRevisionWithResponse(OpaqueId projectId, OpaqueId revisionId)
public CompletableFuture<ApiResponse<SourceRevision>> getSourceRevisionWithResponseAsync(OpaqueId projectId, OpaqueId revisionId)
public CompletableFuture<SourceRevision> getSourceRevisionAsync(OpaqueId projectId, OpaqueId revisionId)
public SourceRevision getSourceRevision(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public CompletableFuture<SourceRevision> getSourceRevisionAsync(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public ApiResponse<SourceRevision> getSourceRevisionWithResponse(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
public CompletableFuture<ApiResponse<SourceRevision>> getSourceRevisionWithResponseAsync(OpaqueId projectId, OpaqueId revisionId, RequestOptions requestOptions)
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

Example status: `unsupported`  
Unsupported reason: `language-example-not-generated`

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRTb3VyY2VSZXZpc2lvbiJ9 -->

