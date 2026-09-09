# BATO Exchange

A locally runnable customer request portal for crypto deposit/withdrawal requests. It includes account registration/login, persistent request storage, a read-only viewer, and a direct WhatsApp handoff.

## Requirements

- Node.js 20 or newer
- npm

## Run locally

1. Open a terminal inside the `BATO-Exchange` folder.
2. Install dependencies:

   ```bash
   npm run install:all
   ```

3. Copy `.env.example` to `.env` and change `ADMIN_PASSWORD`.
4. Start both frontend and API:

   ```bash
   npm run dev
   ```

5. Open <http://localhost:5173>.

The API runs at <http://localhost:5000>. Data is created automatically in `server/data/database.json`.

## Administrator

Default local credentials are only for first startup:

- Email: `admin@bato.local`
- Password: `ChangeMe123!`

Change them in `.env` before the first run. The administrator can log in and open Viewer Portal to see unredacted customer contact details. Public viewer access is redacted.

## Production-style local run

```bash
npm start
```

Then open <http://localhost:5000>.

## Verify

```bash
npm test
```

Read `PROJECT-AUDIT.md` for what was wrong in the original archive, what was connected, and what remains before production.
