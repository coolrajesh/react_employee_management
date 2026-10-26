# Employee Management — React Client

React frontend for the existing Employee Management REST API.

> The Express API is the source of truth. Confirm its actual endpoints and schemas before implementing the client. This README should be updated with the verified API contract as the project is developed.

## Features planned

- Employee list
- Create, view, update, and delete employee records where supported by the backend
- Loading, empty, validation, and error states
- Configurable API base URL
- Responsive and accessible UI
- Optional pagination, filtering, and sorting only where supported by the API

## Tech stack

Preferred defaults:
- React
- Vite
- TypeScript
- Tailwind CSS

Use existing repository choices where they differ; avoid duplicate tooling.

## Prerequisites

- A supported Node.js LTS version
- npm
- Existing Employee Management Express API running locally or at an accessible development URL

Check the backend README/package scripts for the exact Node.js version and startup command.

## Setup

1. Install dependencies:

   ```bash
   npm install
   ```

2. Create a local environment file from the example:

   ```bash
   cp .env.example .env
   ```

   On Windows PowerShell, use:

   ```powershell
   Copy-Item .env.example .env
   ```

3. Set the API URL in `.env` using the variable expected by the chosen build tool. For Vite:

   ```env
   VITE_API_BASE_URL=http://localhost:3000/api
   ```

   **Important:** Confirm the backend's actual port and route prefix. The value above is only an example.

4. Start the backend using its own documented command.

5. Start the frontend:

   ```bash
   npm run dev
   ```

   Open the local URL printed by Vite.

## Available scripts

The exact scripts depend on `package.json`. Common Vite scripts are:

```bash
npm run dev
npm run build
npm run preview
npm run lint
npm run test
```

Only run scripts that are defined in the repository. Add or update this section after checking `package.json`.

## API contract

Document verified details here after inspecting the Express backend:

| Operation | Method and path | Status |
|---|---|---|
| List employees | To be confirmed | Not verified |
| Get employee by ID | To be confirmed | Not verified |
| Create employee | To be confirmed | Not verified |
| Update employee | To be confirmed | Not verified |
| Delete employee | To be confirmed | Not verified |
| Login/authentication | To be confirmed | Not verified |

Do not treat these rows as proof that every endpoint exists.

For each verified operation, document:
- Request parameters/body
- Successful response schema
- Validation/error response schema
- Authentication requirements
- Pagination/filter/sort behavior, if supported

## Environment variables

| Variable | Purpose | Example |
|---|---|---|
| `VITE_API_BASE_URL` | Base URL for the Express API | `http://localhost:3000/api` |

Vite variables prefixed with `VITE_` are exposed to browser code. Never put passwords, private API keys, JWT signing secrets, or database credentials in them.

## CORS and connectivity troubleshooting

If the browser reports a CORS error:
1. Confirm the backend is running and the URL is correct.
2. Inspect the Express CORS configuration.
3. Allow the exact frontend development origin on the backend.
4. If cookie credentials are used, configure frontend requests and backend CORS credentials consistently. Do not combine credentialed requests with a wildcard origin.

A CORS error is not fixed securely by disabling browser security.

## Project structure

Suggested structure; adapt to the actual repository:

```text
src/
  app/
  components/
    common/
    layout/
  features/
    employees/
      api/
      components/
      pages/
      types/
      validation/
  lib/
  config/
  main.tsx
```

## Quality checks

Before opening a PR or considering a feature complete:
- Run lint/type-check scripts if configured.
- Run relevant tests.
- Run the production build.
- Verify loading, empty, success, and error states.
- Confirm the app uses real API data.
- Check desktop and mobile layouts.
- Ensure no secrets or `.env` files are committed.

Record the actual command results; do not claim checks passed if they were not run.

## Security notes

- The browser must never connect directly to PostgreSQL.
- Client-side validation improves UX but does not replace backend validation.
- Do not expose secrets in frontend environment variables.
- Follow the backend's authentication mechanism and authorization rules.
- Avoid logging tokens or sensitive employee data.

## Development notes

Keep product decisions and requirements in `prd.md`, and coding-agent rules in `agents.md`. Update this README when commands, configuration, API endpoints, or project structure change.
