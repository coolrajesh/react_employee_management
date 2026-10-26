# Agent Instructions — Employee Management React Client

## Mission

Build a reliable React frontend for the existing Employee Management REST API. The backend is the source of truth for routes, data shapes, validation, authentication, and business rules.

## Mandatory first step

Before changing code:
1. Inspect the repository tree, package files, existing frontend conventions, and available scripts.
2. Locate and inspect the Express backend routes/controllers/services/validators and relevant documentation.
3. Identify the actual API base URL, endpoints, methods, request/response schemas, error format, CORS setup, and authentication requirements.
4. Summarize findings and propose a small implementation plan.
5. Call out any unknowns. Do not guess API fields or endpoints.

If the backend is in another directory or is not available in the workspace, ask the user for its location or API documentation. Do not pretend to have inspected it.

## Source-of-truth rules

- `prd.md` defines the product requirements.
- The existing backend implementation defines the API contract.
- Existing repository conventions take precedence over adding a new framework or tool.
- If PRD assumptions conflict with the actual API, explain the conflict and propose the smallest safe resolution.
- Do not change backend behavior unless explicitly requested.

## Engineering rules

- Prefer React + TypeScript and the repository's existing build setup.
- Use Tailwind CSS only if it is already installed or the user approves adding it; otherwise propose it before setup.
- Keep API calls in a dedicated API module, not scattered across components.
- Define types from the actual backend contract. Do not use speculative fields.
- Avoid `any`; use `unknown` and narrow types when appropriate.
- Do not add dependencies without a clear reason.
- Do not introduce Redux or another global state library for simple CRUD needs.
- Use reusable components where they reduce duplication; avoid premature abstraction.
- Keep components readable and focused.
- Use semantic HTML, accessible labels, keyboard support, and visible focus styles.
- Handle loading, empty, validation, network, and server-error states.
- Disable submit controls while requests are in progress and prevent accidental duplicate submissions.
- Confirm destructive actions before sending delete requests.
- Never show success or remove a row until the server confirms success.
- Never hard-code secrets. Browser-exposed environment variables are not secret.
- Do not log credentials, tokens, or sensitive employee data.
- Do not store tokens in localStorage unless the existing security design explicitly requires it and the trade-off is documented.
- Respect the backend's auth mechanism; do not invent a login/JWT contract.
- Avoid unsafe HTML rendering and unsafe SQL-like assumptions in frontend filtering/sorting.
- Do not replace real API integration with mock data except for explicitly isolated tests or a user-approved temporary prototype.

## API and environment configuration

- Read the API URL from an environment variable appropriate to the toolchain (for Vite, typically `VITE_API_BASE_URL`).
- Provide an `.env.example` with non-secret sample values.
- Ensure `.env` and secrets are ignored by Git.
- Normalize error handling in one place where practical.
- Check CORS and credential requirements against the backend configuration.

## Workflow for each task

1. State the intended change and files likely to be affected.
2. Make the smallest coherent implementation.
3. Run relevant lint, type-check, tests, and build commands available in the repository.
4. Fix issues caused by the change.
5. Review the diff for accidental changes, hard-coded URLs, secrets, dead code, and unsupported assumptions.
6. Report:
   - What changed
   - Files changed
   - Commands/checks actually run and their results
   - Remaining issues or assumptions

## Testing expectations

- Test API success and failure paths.
- Test form validation and duplicate-submit prevention.
- Test empty and loading states where practical.
- Test delete cancellation and failure behavior.
- Use existing test tools first. If none exist, recommend a minimal testing setup before adding it.
- Never claim tests or builds passed unless the command was executed and passed.

## Git and scope safety

- Do not delete or rewrite unrelated files.
- Do not overwrite user changes.
- Do not run destructive commands or modify production data.
- Do not commit or push unless explicitly asked.
- Keep each task small enough to review.
- If a requirement is ambiguous or a decision affects API compatibility/security, ask before proceeding.

## Completion definition

A task is complete only when the implementation matches the agreed acceptance criteria, relevant checks have been run, documentation is updated, and any unresolved limitations are clearly reported.
