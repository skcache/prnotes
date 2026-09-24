# Behavior-preserving refactor

## What changed

Refactors request retry policy construction into a single module without intended runtime behavior changes.

The previous implementation duplicated retry limits and backoff selection across three call sites. The new module owns policy construction while preserving the existing retry contract.

### Implementation

- All call sites now request a policy from `retry-policy.ts`.
- Retry count, backoff schedule, and retryable status codes are unchanged.
- Callers still own cancellation and timeout behavior.

### Verification

- [x] Existing retry behavior tests pass unchanged.
- [x] Snapshot coverage confirms the same policy for each previous call site.
- [x] Cancellation and timeout tests remain green.
