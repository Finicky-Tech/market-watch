# Handoff: auth-signup-signin-features-scaffold

## Phase

Cross-examination complete and approved (2 revision rounds) for
`market-watch-ui`'s auth signup/signin work. No implementation files exist
yet. Scope for this implementation pass is narrow: presentational-only
scaffolding of `feature-signup/` and `feature-signin/`. No `data/`, `ui/`,
or `utils/` files are in scope.

## Next action

Verify Angular 22 Signal Forms' root-level aggregate-validity accessor
(e.g. whether `form().valid()` is correct) against current angular.dev
docs — this gates submit-button logic in both forms and must be confirmed
before writing either component, not assumed. Then build, in order:

1. `feature-signup/` dumb form component
2. `feature-signup/` smart container component (stub submit handler)
3. `feature-signin/` dumb form component
4. `feature-signin/` smart container component (stub submit handler)

## Key decisions made

- Domain layers: `data/`, `features/`, `ui/`, `utils/` (plural). Both
  `feature-signup/` and `feature-signin/` (renamed from `feature-login`
  throughout — folders, component class/selector names, future route
  paths) nest inside `features/`.
- **This session builds ONLY inside `features/`.** `data/` (AuthStore,
  command/query services, DTOs, mappers) is fully deferred — do not create
  any file there. `ui/` is not created either — it's reserved for
  components proven reusable across 2+ unrelated consumers, never
  speculative; a single-consumer form doesn't qualify. `utils/` (guards,
  interceptor) is also deferred.
- Dumb/smart split is behavioral, not folder-based: the dumb form
  component and its smart page-level container both live co-located
  inside the same `feature-signup/`/`feature-signin/` folder — never
  split into a separate `ui/` or `ui-auth/` location. This was corrected
  twice across two prior sessions; do not reintroduce the split.
- Dumb form components: Signal Forms-based, take `submitting`/
  `serverError` inputs, emit a single form-value output, never inject
  `AuthStore` or `HttpClient`.
- Smart container components: wire the dumb form's output, but the
  submit handler is a stub/TODO this session (no `AuthStore` exists to
  call). Mark stubs clearly (comment or thrown "not implemented").
- `feature-signup`'s smart container also implements the inline
  "check your email" success-state UI now (replaces the form in place,
  not a route change) — registration never auto-authenticates, so this
  state is reachable/testable independent of the stub.
- `feature-signin`'s `serverError` input/signal is shaped to carry at
  least `name` and `message` (matches the error envelope below). The
  component renders whatever it's given — no hardcoded branching for
  "unverified email" vs. other failures baked into the component itself;
  that distinction is the future `AuthStore`'s responsibility, not this
  component's.
- Client-side validation on the signup form is UX-only, not a mirror of
  server rules (`IsStrongPassword`'s symbol requirement and
  `IsMobilePhone('en-NG')` are not fully replicated client-side).

## Open questions

- Signal Forms root-level aggregate-validity accessor API — flagged
  across two prior sessions as unconfirmed against angular.dev; must be
  verified before writing submit-gating logic (see Next action).
- Whether to set up `eslint-plugin-boundaries` now vs. once a second
  domain exists — raised in an earlier session, never decided, still
  open and unrelated to this implementation pass.
- Everything under the deferred `data/` layer (AuthStore's direct
  HTTP-calling design, `verifyUserStatus` consolidation, token storage)
  is a *decided* design, not open — but it is not this session's
  deliverable. See State reference.

## Source material

Exact API contracts the components must be built against — do not
re-derive or approximate these.

```typescript
// Request DTO (Market Watch API, IAM module)
export class RegisterNewUserRequestDto {
  readonly firstName!: string;       // required, 2-40 chars, trimmed
  readonly lastName!: string;        // required, 2-40 chars, trimmed
  readonly middleName!: string | undefined; // optional, 2-40 chars, trimmed
  readonly email!: string;           // required, trimmed+lowercased, IsEmail
  readonly phoneNumber!: string;     // required, trimmed+lowercased, IsMobilePhone('en-NG')
  readonly street!: string;          // required, trimmed
  readonly city!: string;            // required, trimmed
  readonly ward!: string;            // optional, trimmed
  readonly localGovernment!: string; // required, trimmed
  readonly state!: string;           // required, trimmed
  readonly zipCode!: string | null;  // optional, numeric string
  readonly country!: string;         // required, trimmed
  readonly password!: string;        // required, IsStrongPassword(minLength:8, minNumbers:1, minUppercase:1, minSymbols:1)
}

// Response DTO
export class RegisterNewUserResponseDto {
  id!: string;
  status!: string;
  createdAt!: string;
}

// Login request (assumed/confirmed shape, no formal DTO provided)
// { email: string; password: string }

// Login response
export interface LoginUserOutput {
  accessToken: string;
  refreshToken: string;
}

// verifyUserStatus response (role field to be added by backend; values confirmed: CONTRIBUTOR | ADMIN)
const verifiedUser: {
  id: string;
  status: UserStatus;
  role: 'CONTRIBUTOR' | 'ADMIN'; // pending backend update
} | null;

// Success envelope, wraps all of the above in `data`
export interface ApiResponse<T> {
  success: boolean;
  statusCode: number;
  message: string;
  data: T;
  timestamp: string;
  meta?: { path?: string; requestId?: string };
}

// Error envelope
// {
//   success: false,
//   statusCode: number,
//   message: string,
//   data: null,
//   timestamp: string,
//   error: { name: string, stack?: string }
// }
```

## State reference

The full approved cross-examination report — architecture rationale,
Intent/Context/Expectations, and the complete deferred-`data/`-layer
design (AuthStore's `verifyUserStatus()` owning JWT retrieval + header
attachment, token storage in `localStorage`, why `LoginUserOutput` stays
tokens-only, etc.) — is being supplied directly by the user alongside
this handoff, not attached here. If it is not present in the new
conversation, ask the user for it before making any `data/`-layer design
assumption; the condensed Key decisions above are sufficient to execute
*this session's* scope (features/ only) without it, but not sufficient to
correctly build `data/` later.

---

session = 2-round cross-examine (ice framework) for market-watch-ui auth
feature, culminating in this narrower implementation handoff. round 1
report wrongly scoped data/+features together — user corrected: data/
fully deferred, folder tree corrected to data/features/ui/utils (4
layers), feature-login->feature-signin rename, ui/ placement question
raised by user themselves (thought dumb components might belong there)
and resolved by re-citing prior session's own established rule (ui/ =
2+-consumer reuse proof only, dumb/smart is behavioral not foldering).
round 2 also locked: AuthStore.verifyUserStatus() itself does header
attach (not a separate query service) - relevant for data/ session later,
not this one. this session's actual deliverable = 4 files across 2
feature folders, in the order listed above, gated by 1 prerequisite
research check (signal forms validity accessor). nothing coded yet in
either round - purely planning/alignment, consistent with the original
(pre-cross-examine) handoff this whole thread descended from
(auth-domain-registration-signin_context_08-08-2026.md), which itself was
pure architecture tutoring w/ zero files created. resuming agent should
NOT reopen the data/-vs-features/ scope debate - that's settled, only
open items are the 2 explicitly listed above.
