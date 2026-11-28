<h1 align="center">Steve</h1>

<p align="center">
  <em>The health agent that acts for you.</em>
</p>

<p align="center">
  <img src="docs/assets/steve-readme-call.png" alt="Steve on the phone in an armchair" width="200">
</p>

<p align="center">Steve guides and organizes your care pathway. He calls, books and reschedules for you.</p>

Built for [Alan x Qovery x AWS: AI Health Hack 2](https://luma.com/o1eopuwy), Paris, 28 November 2026.

## Run the app locally

Use Node 24, per `.nvmrc`.

Install pnpm 10.33.0. `package.json` sets `packageManager` to `pnpm@10.33.0`.

The dev server starts with no env file.

From the repo root, run:

```bash
pnpm install
pnpm --filter @steve/app dev
```

Open http://localhost:3000. `/` redirects to `/chat`.

Port 3000 is the Next.js default. To use another port, pass `-p` with the new port number.

```bash
pnpm --filter @steve/app dev -p 3001
```

The root `package.json` has no `dev` script. `app/package.json` sets `dev` to `next dev`.

Run `pnpm verify` to lint, typecheck, test, and build.

## Deploy on Qovery

The repository root contains the production `Dockerfile`. The container runs
the Next.js standalone server as a non-root user on port `3000`.

Configure the Qovery application with:

- repository root as the build context;
- `Dockerfile` as the Dockerfile path;
- public HTTP port `3000`;
- readiness and liveness probes on `GET /api/healthz` at port `3000`;
- `STEVE_CHAT_LIVE=1`;
- `HACKATHON_AI_BASE_URL` as a variable;
- `HACKATHON_AI_KEY` as a secret.

No database is required for the current demo implementation.

Pull requests targeting the deployment branch receive an isolated Qovery
preview URL for team validation.

Agent rules live in [AGENTS.md](./AGENTS.md).

## License

[Apache-2.0](LICENSE). Copyright 2026 Steve.
