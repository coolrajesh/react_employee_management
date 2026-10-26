# PRD — Employee Management React Client

## 1. Overview

Build a responsive React client for the existing Employee Management REST API built with Express. The frontend lets authorized users view and manage employee records through the backend's existing endpoints.

**Important:** The backend already exists. Inspect its routes, request/response schemas, authentication mechanism, validation rules, and error format before implementing API integration. Do not invent endpoints or silently change the backend contract.

## 2. Goals

- Provide a clean, responsive interface for employee management.
- Integrate with the existing Express API.
- Support the employee CRUD operations that the backend actually exposes.
- Handle loading, empty, validation, network, and server-error states clearly.
- Keep API calls, UI components, and page-level state organized and maintainable.
- Make the app straightforward to run locally and configure for another API URL.

## 3. Out of scope

Unless the backend already supports them or they are explicitly approved:
- Rebuilding or modifying the Express API.
- Inventing authentication or authorization behavior.
- Adding payroll, attendance, performance reviews, or other HR modules.
- Adding a new database or direct database access from the browser.
- Adding fake production data or pretending unsupported operations succeeded.

## 4. Required discovery before coding

Inspect the existing backend and document:
1. How to start the API and its base URL.
2. Available employee endpoints and HTTP methods.
3. Employee fields, required fields, field types, and ID format.
4. List response shape (array or paginated object).
5. Create/update request and response shapes.
6. Delete behavior and response status.
7. Authentication requirements, if any.
8. Error and validation response format.
9. CORS configuration and any required headers.

Create a short API contract note in the project README or `docs/api-contract.md`. If something cannot be determined, ask the user or clearly document the assumption rather than guessing.

## 5. Users and primary journeys

### Employee list
- User opens the Employees page.
- App fetches employee data from the existing API.
- App shows a loading indicator while the request is in progress.
- App displays records, an empty state, or a useful error with a retry action.

### Create employee
- User opens the create form.
- Form fields are derived from the actual API contract.
- Client-side validation provides helpful feedback.
- On successful submission, show confirmation and refresh/navigate to the updated list.
- On failure, show a useful message and preserve entered values where practical.

### View employee details
- User selects a row/card and sees the employee details supported by the API.
- Handle invalid IDs and not-found responses.

### Edit employee
- Form loads the selected employee's existing values.
- User edits allowed fields and submits.
- On success, show confirmation and refresh the displayed data.
- On failure, show validation/API feedback.

### Delete employee
- Ask for confirmation before deletion.
- Send the request only after confirmation.
- Update the UI only after the API confirms success.
- Handle failed deletion without falsely removing the record.

Only implement journeys supported by existing backend endpoints.

## 6. Functional requirements

### FR-1: Application shell
- Provide a clear application title and navigation.
- Include an Employees section.
- Show a responsive layout for desktop, tablet, and mobile.
- Include a consistent loading and error presentation.

### FR-2: Employee listing
- Fetch data from the configured API.
- Display meaningful fields based on the actual employee schema.
- Include a clear empty state.
- If the API supports pagination, filtering, or sorting, expose those capabilities; otherwise do not simulate server-side support.
- Avoid rendering undefined or malformed fields as confusing UI text.

### FR-3: Employee form
- Reuse form components where appropriate for create and edit.
- Use suitable controls based on field types.
- Validate required fields and basic formats on the client, consistent with backend rules.
- Treat backend validation as authoritative.
- Prevent duplicate submissions while a request is in progress.

### FR-4: API integration
- Keep the API base URL in environment configuration.
- Centralize HTTP requests in a small API layer.
- Handle non-2xx responses and network failures.
- Do not hard-code secrets in frontend environment variables. Anything shipped to the browser is public.
- Do not make direct database calls from the client.

### FR-5: Authentication
- First inspect the backend to determine whether authentication is required.
- If supported, integrate using the backend's existing mechanism and follow its security requirements.
- Do not invent a login screen or JWT contract.
- Never log access tokens or credentials.
- If cookie-based auth is used, configure requests and backend CORS/credentials consistently.

### FR-6: Accessibility and usability
- Use semantic HTML and correctly associated form labels.
- Support keyboard navigation and visible focus.
- Use accessible names for icon-only buttons.
- Ensure errors are not communicated only through color.
- Provide confirmation before destructive actions.

## 7. Technical direction

Preferred defaults, unless the existing repository has established choices:
- React
- Vite
- TypeScript
- Tailwind CSS
- React Router only if multiple pages/routes are needed
- Native `fetch` or the repository's existing HTTP client
- A small, feature-oriented folder structure

Do not add a large state-management library unless there is a demonstrated need. Avoid unnecessary dependencies.

Suggested structure (adapt to the actual repository):

```text
src/
  app/
    App.tsx
    router.tsx
  components/
    common/
    layout/
  features/
    employees/
      api/
        employeeApi.ts
      components/
      pages/
      types/
      validation/
  lib/
    http.ts
  config/
    env.ts
  main.tsx
```

## 8. UI direction

Create a professional, restrained business application:
- Clear page title and primary action.
- Readable table on larger screens and a usable responsive layout on smaller screens.
- Consistent spacing, typography, buttons, inputs, and feedback states.
- Avoid excessive gradients, animations, decorative cards, or unnecessary dashboard charts.
- Do not add metrics or charts unless supported by real API data and useful to the employee workflow.

## 9. Quality requirements

- TypeScript strictness should follow the existing project configuration; avoid `any` unless justified.
- Keep components focused and reusable without overengineering.
- Separate API calls from presentational components.
- Handle loading, success, empty, validation, and error states.
- Add tests for important behavior using the project's existing test tooling. If no test tooling exists, propose a minimal setup before adding dependencies.
- Run lint, type-check, tests, and production build where scripts are available.
- Do not claim a check passed unless it was actually run.

## 10. Acceptance criteria

- [ ] Frontend starts locally using documented commands.
- [ ] API base URL is configurable.
- [ ] API contract has been inspected and documented.
- [ ] Employee list displays real backend data.
- [ ] Create/edit/delete work if the corresponding endpoints exist.
- [ ] Forms validate inputs and display backend errors.
- [ ] Loading, empty, and error states are implemented.
- [ ] Destructive actions require confirmation.
- [ ] Layout is usable on desktop and mobile.
- [ ] No secrets or backend credentials are committed.
- [ ] Relevant tests and production build pass, or any failures are documented.
- [ ] README explains setup, configuration, scripts, and API integration.

## 11. Implementation plan

1. Inspect the repository and backend API; report findings before coding.
2. Scaffold or adapt the React app using the chosen stack.
3. Configure environment variables and the shared HTTP layer.
4. Implement the employee list and its loading/empty/error states.
5. Implement create and edit forms using the real schema.
6. Implement details and delete flows if supported.
7. Add responsive styling, accessibility improvements, and tests.
8. Run checks, fix issues, and update documentation.

Work in small, verifiable increments. Do not implement every phase in one giant change.
