# Planka v1 (Node2Shell fix)

This is a fork of [Planka](https://github.com/plankanban/planka) at v1.26.3, kept alive for one reason: to ship a Docker image that runs on a Node.js release patched against **Node2Shell** ([CVE-2026-111497](https://www.sophos.com/blog/node2shell-cve-2026-111497-in-active-exploitation), a critical Brotli decoder bug).

Upstream v1 images run Node 18, which receives no fix. This fork changes the runtime to Node 22.23.4 and makes no other functional changes. For new features or v2, use [upstream](https://github.com/plankanban/planka).

![](demo.gif)

## Docker image

```
ghcr.io/chmac/planka-v1:latest
```

Images are built by GitHub Actions on every push to `main` and published to the GitHub Container Registry. Release tags are published as `<version>`, and every build gets a `sha-<commit>` tag you can pin to.

It is a drop-in replacement for the upstream v1 image. If you already have a compose file, change its `image:` line from `ghcr.io/plankanban/planka` to `ghcr.io/chmac/planka-v1`. The `docker-compose.yml` in this repo already does. Configuration is unchanged; see the [upstream docs](https://docs.planka.cloud/docs/category/configuration/).

## What changed from upstream v1

- Docker base images moved from `node:18-alpine` to `node:22.23.4-alpine` (and the client build stage to `node:22.23.4`).
- The Docker publishing workflow now runs on GitHub-hosted runners and pushes to this fork's registry. Other upstream release workflows are disabled (`*.yml.disabled`).
- README rewritten for the fork.

## Features

- Create projects, boards, lists, cards, labels and tasks
- Add card members, track time, set due dates, add attachments, write comments
- Markdown support in card description and comments
- Filter by members and labels
- Customize project backgrounds
- Real-time updates
- Internal notifications
- Multiple interface languages
- Single sign-on via OpenID Connect

## Tech stack

- React, Redux, Redux-Saga, Redux-ORM, Semantic UI React, react-beautiful-dnd
- Sails.js, Knex.js
- PostgreSQL

## Security

Report issues with this fork's image or Dockerfile via GitHub issues. For vulnerabilities in Planka itself, follow [upstream's policy](SECURITY.md).

## License

Planka is [AGPL-3.0 licensed](LICENSE). Copyright belongs to the original Planka authors.
