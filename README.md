# NaanoOrder — self-hosted trading automation

**Compatible with MetaTrader 5. Runs on your own server. No Windows machine.**

**Ready to deploy? → [Order on order.naanocorp.com](https://order.naanocorp.com)**

**API reference (Scalar) → [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)**
— served locally as soon as the stack is running.

NaanoOrder is a self-hosted module that runs the MetaTrader 5 terminal in
an isolated Docker container and exposes a small, authenticated HTTP API for
account, positions, orders, and position closing. You keep control of your
account, your broker, and your data.

This repository is the public front of the module. The module itself is
delivered after purchase.

---

## Simple by design

- **One command to start.** `docker compose up -d --build`, then
  `GET /health` returns `{"ok": true}`.
- **No Windows VM.** The terminal runs under Wine inside the container; no
  Python, Wine, or MetaTrader installation is needed on the host.
- **One configuration file.** Credentials, API token, broker installer URL,
  and RPyC server settings live in a single `.env`.
- **One small API.** Account, positions, order placement, and close — nothing
  to learn beyond a few endpoints.
- **Works with your broker.** The module installs the broker's own MT5
  installer and server list, so symbols and servers match your account.

## Reliable by default

- **Healthchecks on the terminal and the RPyC bridge.** The API only starts
  when the terminal is running and the bridge is listening.
- **Automatic recovery.** A maintenance loop reconnects and re-logs in after a
  terminal restart or a network drop.
- **Checked downloads.** The RPyC server binary is verified against a
  mandatory SHA-256; the broker installer checksum can be pinned too.
- **Persistent installation.** A Docker volume keeps the Wine prefix, the
  terminal, and the server list, so restarts do not reinstall MT5.
- **Bounded waits and clear logs.** Installation and startup never hang
  forever; failures point to the exact step and log file.
- **Version guard at startup.** The API logs the RPyC client/server versions
  and refuses to become healthy on a major mismatch.
- **Reference platform tested.** Linux x86_64 with Docker Engine and Compose
  v2.

## What you get

- Docker Compose stack: `mt5` (terminal under Wine + RPyC) and `mt5-api`
  (FastAPI).
- HTTP API for account, positions, orders, and position closing, with an
  interactive Scalar reference served locally at `/docs`.
- Documentation: installation, broker switching, operations, troubleshooting.
- Third-party licence inventory and notices.
- A documented upgrade path for the broker installer and the RPyC server.

## Requirements

- Linux x86_64 (the reference platform; Docker Desktop on Windows/macOS is
  not the reference setup).
- Docker Engine with Compose v2.
- An MT5 account — start with a **demo** account — and the exact broker
  server name.
- The direct download URL of your broker's MT5 installer.
- The RPyC server binary URL and its SHA-256 (documented in the module).

## Quick start

After purchase, from the delivered module directory:

```bash
cd mt5
cp .env.example .env
# Fill in MT5_LOGIN, MT5_PASSWORD, MT5_SERVER, MT5_TOKEN,
# MT5_BROKER_ID, MT5_SETUP_URL, MT5SERVER_URL, MT5SERVER_SHA256.
docker compose up -d --build
curl http://127.0.0.1:8000/health
```

Expected:

```json
{ "ok": true }
```

The first start downloads the broker installer and can take several minutes.
Later starts reuse the installed terminal from the Docker volume.

## API documentation

The interactive API reference ships with the module and is served locally —
no external service, no CDN:

- **Scalar UI:** [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
- **OpenAPI contract:** `mt5/mt5-api/openapi.yaml`
- **Authentication:** `x-api-key` or `x-token` with your `MT5_TOKEN`

It documents account, positions, order placement, and position closing, with
request and response schemas you can try directly from the browser. Start the
stack, then open the URL above; the reference is immediately available.

## What is not included

- The MetaTrader 5 terminal and the broker installer are **not
  redistributed**. They are downloaded at first start from the official
  sources, under the applicable MetaQuotes EULA and broker terms.
- No account credentials, no proprietary binaries, and no prebuilt image.
- No trading signals and no financial advice. The module executes the orders
  you send; trading decisions remain yours.

## Licensing and trademarks

This is a commercial, self-hosted module. The licence terms are provided at
purchase; the module and any image built from it are not licensed for
redistribution. Third-party components keep their own licences — see the
module's `THIRD_PARTY_NOTICES.md`.

"MetaTrader" and "MetaTrader 5" are trademarks of MetaQuotes Ltd. "FBS" is a
trademark of FBS Markets Inc. This product is not affiliated with, endorsed
by, or sponsored by MetaQuotes or any broker. It is compatible with
MetaTrader 5.

---

## Purchase and support

**Start here: [order.naanocorp.com](https://order.naanocorp.com)**

The website covers pricing, the purchase procedure, delivery, and support.
