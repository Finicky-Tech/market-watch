# Cross-Examination Report: Auth Signup/Signin Implementation (Revised)

## Intent

Scaffold the presentational layer of signup and signin inside
`domains/shared/auth/features/` in `market-watch-ui` — `feature-signup/`
and `feature-signin/` — as fully-formed dumb form + smart container pairs,
with no live API wiring, since the `data/` layer (`AuthStore`, command/
query services, DTOs, mappers) is deferred to a future session in its
entirety.

This is a narrower session than originally scoped. The earlier draft of
this report assumed `data/` would be built alongside the components; that
assumption was corrected. The value of this session is producing
components whose contracts (inputs/outputs, error-display shape, submit
sequencing) are already correct and won't need reshaping once `AuthStore`
exists — not producing a working end-to-end auth flow.

## Context

**Folder structure, corrected.** The domain's four layers are `data/`,
`features/`, `ui/`, and `utils/` (plural — not `util/`). Both
`feature-signup/` and `feature-signin/` (renamed from `feature-login`
throughout — folders, component class/selector names, and eventual route
paths) live nested inside `features/`, not flat at the domain root as the
original handoff's tree showed. `data/` and `utils/` are not created this
session (no files belong there yet). `ui/` is also not created this
session — its absence isn't an oversight; per the handoff's original
rule, `ui/` is reserved for components proven reusable across two or more
unrelated consumers with zero feature-specific knowledge, created only on
real reuse pressure. A signup or signin form used by exactly one feature
doesn't clear that bar. This was raised and re-confirmed during this
revision: the dumb/smart split in this codebase is a *behavioral*
boundary (whether a component injects `AuthStore`/`HttpClient` directly),
not a *folder* boundary — dumb form components stay co-located inside
their own `feature-*/` folder, matching Manfred's screenshot pattern the
original handoff session settled on twice already.

**What gets built.** Each of `feature-signup/` and `feature-signin/`
gets two components:

- A **dumb form component** — Signal Forms-based, takes `submitting`/
  `serverError` inputs, emits a form-value output, never injects
  `AuthStore` or `HttpClient`.
- A **smart page-level container component** — wires the dumb form's
  output, but its submit handler is a stub/TODO, since there is no
  `AuthStore` to call yet.

No routes, guards, or interceptor are touched this session (already
deferred from the prior revision), and now `data/` is deferred alongside
them.

**Design decisions carried forward for the deferred `data/` session.**
These were resolved through discussion in this session and must not be
re-litigated or lost when `data/` is actually built — they are recorded
here as forward context, not as this session's deliverable:

- Both tokens (`accessToken`, `refreshToken`) arrive in the JSON response
  body and are persisted to `localStorage` by `AuthStore`.
- `LoginUserOutput` stays tokens-only (`{ accessToken, refreshToken }`).
  Identity is deliberately not added to it — padding it with `userId`/
  `email` was considered and rejected, since the frontend has no way to
  trust client-supplied identity for authorization regardless, and a
  post-login dashboard would need more than an ID anyway.
- Instead, `AuthStore.login()` stores the tokens, then calls
  `verifyUserStatus` to resolve `currentUser` (`id`, `status`, and a new
  `role` field: `CONTRIBUTOR` | `ADMIN`) before `login()` itself resolves.
  `verifyUserStatus` is deliberately being consolidated into the single
  "who is this token for, and are they allowed" endpoint — used
  server-side during login (to gate unverified accounts) and client-side
  by `AuthStore` (and later `adminGuard`) with the JWT in the header.
- **`AuthStore`'s own implementation of `verifyUserStatus()`** — not a
  separate query service — is responsible for retrieving the JWT from
  storage and attaching the `Authorization` header. This was corrected
  explicitly: the header-attachment logic belongs inside `AuthStore`
  itself, not delegated to a stand-alone data-access service, since the
  general HTTP interceptor is also deferred and this keeps the
  interceptor's eventual introduction a clean deletion rather than a
  rewrite.
- Registration does not authenticate the user — `RegisterNewUserResponseDto`
  returns no token because the API dispatches an email verification link
  instead. The signup form's success state must be an inline
  "check your email" message replacing the form, not a route change or
  auto-login.
- Login itself (not a separate pre-check) determines verification
  gating — the `/login` endpoint checks status and responds accordingly.
  `LoginComponent`'s error display reads from a signal populated by the
  API error response's `name`/`message` fields; it does not hard-code a
  branch on a guessed status code.
- Both response envelopes are fixed and verbatim:

  ```typescript
  // Success response shape
  interface ApiResponse<T> {
    success: boolean;
    statusCode: number;
    message: string;
    data: T;
    timestamp: string;
    meta?: { path?: string; requestId?: string };
  }
  ```

  ```typescript
  // Error response shape
  interface ApiErrorResponse {
    success: false,
    statusCode: number,
    message: string,
    data: null,
    timestamp: string, 
    error: { name, stack? }
  }
  ```

**Why building the dumb/smart shells now still has value despite no
`data/` layer existing.** The components' *contracts* — what inputs they
take, what they emit, how they display loading/error states — are fully
determined by the decisions above, even though nothing calls the real API
yet. Building them now against the final contract avoids a rewrite when
`AuthStore` lands; building them against a guessed contract would risk
exactly that rewrite.

## Expectations

**E1.** `feature-signup/`'s dumb form component collects the full
`RegisterNewUserRequestDto` field set (matching the verbatim DTO from the
handoff), performs UX-only client-side validation (not a mirror of
`class-validator` rules — e.g. `IsStrongPassword`'s symbol requirement and
`IsMobilePhone('en-NG')` are not fully replicated client-side), and emits
a single form-value output on submit. It never imports `AuthStore` or
`HttpClient`.

**E2.** `feature-signup/`'s smart container wires that output to a
stubbed/TODO submit handler (clearly marked, e.g. a comment or thrown
"not implemented" pending `AuthStore`), and separately implements the
inline "check your email" success-state UI so that once the real handler
is wired in, only the API call itself needs to be added — the success
path's presentation is already correct and testable.

**E3.** `feature-signin/`'s dumb form component takes `{ email, password }`
per `LoginUserInput`, plus `submitting` and `serverError` inputs where
`serverError` is shaped to carry at least `name` and `message` (matching
the error envelope above) so the future `AuthStore` wiring can populate it
directly without changing the component's input contract.

**E4.** `feature-signin/`'s smart container has a stubbed/TODO submit
handler and renders whatever `serverError` it's given without any
special-casing logic for "unverified" vs. other failures baked into the
component — that distinction lives in whatever populates the signal
later, not in this component.

**E5.** No file is created under `data/`, `ui/`, or `utils/` this
session. If, while building the form components, a genuinely
cross-feature-reusable piece becomes obvious (not just theoretically
possible), it is flagged to the user rather than silently placed in a
speculative `ui/` folder.

**E6.** The Signal Forms root-validity-accessor question flagged in the
original handoff as unconfirmed is verified against current Angular 22
docs before being used to gate either form's submit button — not carried
forward as an unverified assumption into working code.

**Failure scenarios to avoid:**

- Any file resembling `AuthStore`, a command/query service, or a DTO gets
  created this session — that work is fully deferred.
- The dumb form components end up injecting `AuthStore` or `HttpClient`
  "temporarily" to make the stub handler feel more complete — the stub
  must stay a stub.
- `feature-signin`'s dumb component hard-codes an "unverified email"
  message or branch, preempting the signal-based design decided above.
- A `ui/` folder gets created speculatively "since we're here," rather
  than left absent until real reuse pressure exists.
