# loyaltydog/docker-autoheal

Fork of [willfarrell/docker-autoheal](https://github.com/willfarrell/docker-autoheal) so we control the autoheal sidecar source. Used across the LoyaltyDog DigitalOcean fleet to auto-restart Docker containers reporting `unhealthy` (paired with the `HEALTHCHECK` probes added in core_api PR #759).

## How we use it

- Image hosted in the LoyaltyDog DigitalOcean container registry: `registry.digitalocean.com/loyaltydog-app/autoheal:v0.7.0`
- Built and pushed manually from this fork on 2026-05-28. CI publishing is a follow-up.
- Deployed as a sidecar on every Docker-using droplet via the deploy actions in `loyaltydog/core_api` (PR pending).

## Why the fork

- Upstream is solid but hasn't been touched in years.
- Forking keeps the door open for customization (alerting hooks, structured logging, polling cadence) without forking later under fire.
- No code changes vs upstream as of this initial sync.

## Upstream CI disabled

The upstream `.github/workflows/github-build.yml` pushes to a Docker Hub account we don't control. It has been renamed to `.disabled` to prevent failing scheduled runs. Replace with a workflow that pushes to DigitalOcean container registry when we set up CI here.
