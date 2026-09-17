# Handoff: auth-domain-registration-signin

## Phase

Folder structure for `domains/shared/auth/` in market-watch-ui is finalized
(went through 3 correction rounds against Manfred Steyer's NG-DE 2024
folder-tree screenshot). Route mapping for signup/login/account/admin-users
is defined. Nothing has been implemented yet — no store, no components, no
guards. This is a pure planning/architecture-alignment session; next
conversation starts cold on implementation.

## Next action

Implement `AuthStore` in `domains/shared/auth/data/auth.store.ts` first
(login, register, logout methods + currentUser/isAuthenticated signals,
providedIn:'root'), then wire `feature-signup/signup.component.ts` and
`feature-login/login.component.ts` using Angular 22 stable Signal Forms
against the source DTOs below.

## Key decisions made

- Top-level structure is `domains/<domain>/`, auth sits at `domains/shared/auth/`
  — flat like any other domain, "shared" is a domain-qualifier in the path,
  not a special wrapper folder. Other domains (markets, confirmations) will
  be siblings under `domains/` later.
- No `ui-auth/` layer for this domain. Corrected twice: first pass wrongly
  imported Nx multi-library thinking (`ui-x` as separate physical lib);
  final correction — each `feature-*` folder is a self-contained Angular
  component (`.ts`/`.html`/`.scss`/`.spec.ts` together), matching Manfred's
  screenshot exactly (`flight-search/` holds its own template+component+style,
  not split across folders).
- `ui/` folders are reserved for components proven reusable across 2+
  consumers with zero feature-specific knowledge (no store injection, no
  feature-shaped DTO as input type) — created on real reuse pressure only,
  never speculatively. Two scopes when it does appear: `domains/<domain>/ui/`
  (domain-specific-but-dumb, e.g. MarketCard) vs `domains/shared/ui-kit/`
  (zero domain vocabulary, e.g. buttons/inputs).
- `auth.store.ts` lives in `data/` (not `feature-*`) — it's the one store
  that must be importable by guards/components in *other* domains without
  pulling in login/signup UI. Global singleton, providedIn:'root'.
- `admin-users.store.ts` is co-located inside `feature-admin-users/` —
  page-scoped state (paginated user list), only one consumer, matches
  Manfred's `booking.store.ts` sitting next to `flight-search/`.
- Final folder tree for the domain:

  ```txt
  domains/shared/auth/
    data/
      auth.store.ts
      auth-commands.service.ts   (register, login, logout)
      user-queries.service.ts    (getUser, getUsers)
      dtos/ (register-user.dto.ts, login.dto.ts, user.dto.ts)
      mappers/user.mapper.ts
      index.ts
    feature-signup/  (signup.component.ts/.html/.scss/.spec.ts)
    feature-login/   (login.component.ts/.html/.scss)
    feature-account/ (account.component.ts/.html/.scss)
    feature-admin-users/
      admin-users.store.ts
      admin-users.component.ts/.html/.scss
    util/ (auth.guard.ts, admin.guard.ts, auth.interceptor.ts, index.ts)
    auth.routes.ts
    index.ts   (public barrel — only import path other domains use)
  ```

- Data-access services split by CQRS-style command/query, mirroring backend
  naming AND because Angular tooling differs: queries fit `httpResource()`
  (Angular 22, reactive/cacheable), commands fit one-shot `rxMethod` calls.
  Not just cosmetic symmetry with backend handlers.
- No `InjectionToken` port abstraction for data-access repos — unlike
  backend, FE has no real swap scenario (TestBed overrides concrete classes
  fine for mocking); ceremony without benefit by user's own YAGNI standard.
  Use concrete `AuthCommandsService`/`UserQueriesService` directly.
- Angular 22 (stable June 2026) Signal Forms is the chosen forms approach —
  signal-first, matches zoneless architecture. `form()`, `FormField`
  directive, `[formField]` binding, schema validators (`required`, `email`,
  `minLength`, `validate` for cross-field like password confirm).
- Dumb vs smart split: dumb form components (`SignupComponent`'s template
  layer conceptually, even though co-located per the folder correction)
  take `submitting`/`serverError` inputs, emit a form-value output; never
  inject `AuthStore` or `HttpClient` directly — only the smart/page-level
  orchestration does that.
- Client-side form validation is UX-only, not a mirror of server rules —
  server's class-validator DTO remains source of truth (e.g.
  `IsStrongPassword`'s symbol requirement, `IsMobilePhone('en-NG')` won't be
  fully replicated client-side).
- Routes: `/signup`, `/login` public; `/account` guarded by `authGuard`;
  `/admin/users` guarded by `adminGuard`. Guards are functional
  (`CanActivateFn`), read `AuthStore` signals, live in `util/`, referenced
  directly in `auth.routes.ts`.
- `eslint-plugin-boundaries` was recommended (folder-path equivalent of
  Sheriff's tags, since this is a single Angular CLI app not Nx) but not
  yet set up — flagged as worth doing before a second domain exists.

## Open questions

- Exact Signal Forms field-state accessor API at the *root* form level
  (e.g. whether `signupForm().valid()` is correct vs. a different
  aggregate-validity accessor) — the API only stabilized June 2026 in
  Angular 22, docs/tutorials still settling. Verify against angular.dev
  before finalizing the submit-gating logic.
- Whether to set up `eslint-plugin-boundaries` now vs. deferring until a
  second domain exists — raised, not decided.

## Source material

User-provided DTO the signup form/data-access layer must build against
(verbatim, from Market Watch API's IAM module):

```typescript
import { ApiProperty } from '@nestjs/swagger';
import { Transform } from 'class-transformer';
import {
  IsDefined,
  IsEmail,
  IsMobilePhone,
  IsNotEmpty,
  IsNumberString,
  IsOptional,
  IsString,
  IsStrongPassword,
  Length,
} from 'class-validator';
// Request DTO
export class RegisterNewUserRequestDto {
  @ApiProperty({
    example: 'Sadiq',
    description: "User's first name",
    required: true,
    minLength: 2,
    maxLength: 40,
  })
  @IsDefined()
  @Transform(({ value }) => (value as string).trim())
  @IsNotEmpty()
  @IsString()
  @Length(2, 40)
  readonly firstName!: string;
  @ApiProperty({
    example: 'Eze',
    description: "User's last name",
    required: true,
    minLength: 2,
    maxLength: 40,
  })
  @IsDefined()
  @Transform(({ value }) => (value as string).trim())
  @IsNotEmpty()
  @IsString()
  @Length(2, 40)
  readonly lastName!: string;
  @ApiProperty({
    example: 'Gbenga',
    description: "User's middle name",
    required: false,
    minLength: 2,
    maxLength: 40,
  })
  @IsOptional()
  @Transform(({ value }) => (value as string).trim())
  @IsString()
  @Length(2, 40)
  readonly middleName!: string | undefined;
  @ApiProperty({
    example: 'sadiz.eze@example.com',
    description: "User's email address",
    required: true,
  })
  @IsDefined()
  @Transform(({ value }) => (value as string).trim().toLowerCase())
  @IsEmail()
  readonly email!: string;
  @ApiProperty({
    example: '08012345678',
    description: "User's phone number",
    required: true,
  })
  @IsDefined()
  @Transform(({ value }) => (value as string).trim().toLowerCase())
  @IsMobilePhone('en-NG')
  readonly phoneNumber!: string;
  @ApiProperty({
    example: '123 Main Street',
    description: "Street section of user's address",
    required: true,
  })
  @IsDefined()
  @Transform(({ value }) => (value as string).trim())
  @IsNotEmpty()
  @IsString()
  readonly street!: string;
  @ApiProperty({
    example: 'Abuja',
    description: "User's city",
    required: true,
  })
  @IsDefined()
  @Transform(({ value }) => (value as string).trim())
  @IsNotEmpty()
  @IsString()
  readonly city!: string;
  @ApiProperty({
    example: 'Garki',
    description: "User's local government ward",
    required: false,
  })
  @IsOptional()
  @Transform(({ value }) => (value as string).trim())
  @IsNotEmpty()
  @IsString()
  readonly ward!: string;
  @ApiProperty({
    example: 'AMAC',
    description: "User's local government",
    required: true,
  })
  @IsDefined()
  @Transform(({ value }) => (value as string).trim())
  @IsNotEmpty()
  @IsString()
  readonly localGovernment!: string;
  @ApiProperty({
    example: 'FCT',
    description: "User's state of residence",
    required: true,
  })
  @IsDefined()
  @Transform(({ value }) => (value as string).trim())
  @IsNotEmpty()
  @IsString()
  readonly state!: string;
  @ApiProperty({
    example: '900100',
    description: "User's nearest ZIP code",
    required: false,
  })
  @IsOptional()
  @IsNumberString()
  readonly zipCode!: string | null;
  @ApiProperty({
    example: 'Nigeria',
    description: "User's country of residence",
    required: true,
  })
  @IsDefined()
  @Transform(({ value }) => (value as string).trim())
  @IsNotEmpty()
  @IsString()
  readonly country!: string;
  @ApiProperty({ example: 'SuperSecret123!', minLength: 8, required: true })
  @IsDefined()
  @Transform(({ value }) => (value as string).trim())
  @IsString()
  @IsStrongPassword({
    minLength: 8,
    minNumbers: 1,
    minUppercase: 1,
    minSymbols: 1,
  })
  readonly password!: string;
}
// Response DTO
export class RegisterNewUserResponseDto {
  id!: string;
  status!: string;
  createdAt!: string;
}
```

---

session = pure FE architecture tutoring, GDE-persona, tying everything to
user's known backend vocab (clean arch/DDD/CQRS-lite on NestJS+TypeORM).
progression: (1) mapped angular layers->ddd concepts generally (2) covered
lightweight-store concept via Manfred NG-DE2024 talk summary user pasted,
incl store=stateful read-model+command-surface, not just trigger (3) first
folder-tree attempt used shared/auth/{feature,ui,data-access,util} +
nested pages/ subfolders — WRONG per later screenshot, too Nx-flavored,
smart/dumb wrongly forced into separate top-level dirs (4) user posted
screenshot of Manfred's actual lightweight-state repo explorer
(apps/flights/src/app/domains/ticketing/{data,feature-booking/{flight-edit,
flight-edit-reactive,flight-search/(component.ts+html+scss co-located)},
booking.store.ts co-located next to flight-booking.component}) (5) first
correction pass: renamed to domains/ (not shared/) + feature-booking style
naming + store co-location — user pushed back AGAIN: correctly pointed out
auth should be domains/shared/auth (shared BECAUSE consumed across
components) and feature dirs should be feature-signup/feature-login (not
feature-auth/signup/) each containing full angular component set — this
was the correct reading, adopted. (6) user then asked standalone Q: what
belongs in ui/ generically (not auth-specific) — answered w/ test "multiple
features need it with zero knowledge of caller", examples given (buttons/
cards generic; MarketCard/PriceBadge domain-specific-dumb; AddressFields as
the concrete "extract on 2nd consumer" example), anti-examples (injects
store = feature component in disguise; shaped like one feature's DTO =
premature extraction). two ui/ scopes distinguished: domain-level vs
shared/ui-kit. (7) signal forms research done via websearch this session:
Angular 22 released 3 Jun 2026, Signal Forms + Resource API + Angular ARIA
all went stable, OnPush now default, zoneless default for new projects.
Signal Forms syntax confirmed via angular.dev docs: import {form, FormField,
required, email, ...} from '@angular/forms/signals'; form(modelSignal,
schemaFn) returns FieldTree; template binds [formField]="form.field"; schema
fn receives path param, validators attached via required(path.x) etc;
validateHttp for async. exact root-level .valid() aggregate accessor NOT
directly confirmed in search results — flagged open Q above, verify on
resume before writing submit-gating code. sample signup dumb-component code
already drafted in convo using this API (SignupFormComponent w/
SignupFormValue model incl clientside-only confirmPassword field, address
subobject) — NOTE this sample used the pre-correction ui/-separated
structure; on resume, same component logic applies but should be
co-located inside feature-signup/ per final structure, not a separate
ui-auth/signup-form/ folder. CQRS data-access split (AuthCommandsService
vs UserQueriesService) reasoned through in Q4 of the vertical-slicing
brainstorm turn — kept as decision, justified via httpResource() vs
rxMethod fit, not just naming mirroring. No code has actually been created
as files anywhere yet — everything is inline chat markdown/code blocks.
next convo should start writing real files under
projects/market-watch-ui/src/app/domains/shared/auth/ per tree in Key
Decisions.
