# GitHub Actions deployment

This repository publishes Docker images with the `Docker Publish` workflow and
deploys the full frontend plus API stack with `Deploy Docker Host`.

The deploy workflow needs a Docker host reachable over SSH. Configure these
repository secrets:

- `DEPLOY_HOST`: host name or IP address.
- `DEPLOY_USER`: SSH user that can run `docker compose`.
- `DEPLOY_SSH_KEY`: private key for that user.

Configure these repository variables:

- `DEPLOY_URL`: public URL for the frontend, for example `https://shadowbroker.example.com`.
- `DEPLOY_PATH`: remote deploy directory. Defaults to `/opt/shadowbroker`.
- `DEPLOY_BIND`: bind address. Defaults to `0.0.0.0`.

Optional runtime secrets are passed through when present:

- `ADMIN_KEY`
- `AIS_API_KEY`
- `OPENSKY_CLIENT_ID`
- `OPENSKY_CLIENT_SECRET`
- `LTA_ACCOUNT_KEY`
- `FINNHUB_API_KEY`
- `MESH_PEER_PUSH_SECRET`
- `MESH_MQTT_PASS`

After the secrets and variables are set, run `Docker Publish` or manually run
`Deploy Docker Host` from the Actions tab. The deployed app is served from
`DEPLOY_URL`, and API requests are proxied by the Next.js frontend to the
backend container over Docker networking.
