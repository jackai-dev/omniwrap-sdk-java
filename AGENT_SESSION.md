# Native Java SDK sessions

Install the exact JAR and independently verify its SHA-256. Import
`dev.omniwrap.omniwrap.sdk.ApiClient.AgentSession` and its nested `Provider`, `Proposal`, `Call`, `Usage`, `Options`,
`Checkpoint` and `Cancellation` types. The two renderer editions have different
entrypoints; this installed guide and `agent-session.json` name the actual one.
The module calls the application's configured native SDK client in process.

Implement `Provider.identity()`, `version()` (`omniwrap.agent-provider/v1`),
`propose(context, remaining, cancellation)` and `close(cancellation)`. Proposal
factories are `Proposal.calls(usage, calls)` and `Proposal.done(usage, jsonValue)`;
the latter accepts an explicit JSON null. `discovery()` and `agent-session.json`
map operation IDs to native methods, schemas and typed `propose*` helpers.

The application supplies the verified archive hash, allowed operation IDs,
configured client, provider, checkpoint path, external key of at least 32 bytes,
result projection and write approval. For example, using the imported types:

```java
Map<String, Double> limits = Map.of(
    "turns", 8d, "model_calls", 8d, "tool_calls", 20d, "tokens", 8000d,
    "cost", 1d, "elapsed_seconds", 60d, "concurrency", 2d,
    "input_bytes", 1048576d, "output_bytes", 1048576d);
var options = new Options(archiveSha256, allowedOperationIds, limits,
    new Checkpoint(checkpointPath, externalKey), projectResult, approveWrite);
var session = new AgentSession(configuredClient, provider, options);
Object result = session.run(jsonInput, new Cancellation());
```

Use the session class name recorded above if a model collision required another
name. `projectResult` is `BiFunction<String, Object, Object>` and must return plain
JSON after removing application-known secrets. `approveWrite` returns a
`CompletableFuture<Boolean>` for an operation ID, argument SHA-256 and cancellation
token. Approve only specifically authorized writes, including declared effects
on a GET operation. No automatic arbitrary secret detection is claimed.

`runAsync(input, cancellation)` returns a `CompletableFuture<Object>`; cancelling
it signals the session token. Providers/callbacks must cooperate and are not
sandboxed. Native HTTP cancellation is best effort; request timeouts never exceed
the remaining session deadline or the configured client timeout. Native retries
are disabled and native response collectors enforce the smaller of the caller's
bound and remaining output budget, capped at 64 MiB per call. Concurrent buffers
can reach concurrency times that bound. Cleanup timeout remains visible.

Whole batches validate before any SDK effect or write approval. All nine budgets
are mandatory and positive. Plain finite JSON uses safe integers, at most 64
levels and valid Unicode strings. Schema graph qualification follows references,
optional properties and all composition branches before instance validation.
Unqualified constraints/formats, regex, model-owned header/cookie arguments and
stream/upload operations are refused. Provider usage is self-reported.

Checkpoints authenticate source, registry, archive, provider, allowlist and limits,
use exclusive locks/revision checks, hash-chain projected receipts, and persist a
wall deadline. Keep the checkpoint and permanent `.started` guard together. The
filesystem must support atomic replacement; unsupported replacement fails closed.
Power loss, hostile filesystems and complete directory loss are not qualified.
Recover an abandoned `.lock` only after proving its writer stopped.

Completed sessions resume without HTTP. Any unresolved batch requires explicit
reconciliation; an interrupted mutation raises `SessionException` with code
`agent_session_in_doubt` and `retryable=false`, retaining the native cause.
Ordinary refusals use `agent_session_refused`. Inspect the external system, then
call `session.reconcile(callId, knownResult)` for each verified outcome. This
records the projected result without replaying the SDK call. Failed checkpoint
writes poison the instance: inspect storage, reload and reconcile explicitly.

Exercise actual API calls, native failures, budgets, malformed batches, failed
storage, cancellation and process-kill recovery before connecting a live model.
