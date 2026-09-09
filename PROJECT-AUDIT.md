# Original project audit

The uploaded archive was not one connected application. It contained several overlapping experiments:

- `backend/`: actually a React/Vite frontend. This was selected as the main product because it already described a coherent BATO Exchange request workflow.
- `server/`: an Express/TypeScript hello-world only; it had none of the endpoints used by the frontend.
- `baato/`: a second Express hello-world API on another port.
- `database/`: disconnected Mongoose model examples and seed data. No server imported these models.
- `crypto/`: a separate browser-only prototype that stored users, plaintext passwords, balances, and transactions in `localStorage`.
- `cripto/`: another large prototype with most data held in global JavaScript variables; it called a missing `/api/card/withdraw` endpoint.
- `bato_exchange_app (1).html`: another standalone snapshot.

## Missing or broken in the upload

1. No implementation for `/api/auth/register`, `/api/auth/login`, `/api/messages/create`, or `/api/viewer/overview`.
2. Frontend and server ports disagreed (`3000`, `4000`, and `5000`).
3. No real authentication, password hashing, sessions, or server-side validation.
4. No persistent storage connected to the chosen frontend.
5. Duplicate and misspelled project folders (`crypto` and `cripto`) made ownership unclear.
6. Generated `dist` and `node_modules` folders were included while source/config files were scattered.
7. No root command started the whole application.
8. The viewer exposed personal information without access control.
9. No automated test checked the main user workflow.

## Arrangement made

The repaired project uses `client/` for React and `server/` for Express. Vite proxies `/api` to port 5000 during development, while the production server serves the built frontend itself. Users and requests persist in a local JSON file. Passwords are hashed with Node's `scrypt`; login sessions use random server-side tokens. Viewer data is privacy-redacted unless the logged-in viewer is the administrator.

The old prototypes were intentionally not merged line-by-line because they implement conflicting products and unsafe client-side storage. Their useful requirements were consolidated into this working version.

## Still needed before real production or real-money use

- Replace the JSON file with a managed database (PostgreSQL or MongoDB) and migrations/backups.
- Use secure HTTP-only cookies, token expiry, rate limiting, password reset, email/phone verification, and audit logs.
- Protect the viewer with explicit staff roles and permissions.
- Define the business workflow for approving/rejecting requests and reconciling payments.
- Replace placeholder wallet addresses and never automate crypto transfers until security/legal review is complete.
- Confirm the WhatsApp administrator number in `client/src/App.jsx`.
- Add deployment configuration, HTTPS, monitoring, and jurisdiction-specific compliance/KYC/AML controls.
