# 📦 Remix PNPM Monorepo

This template repo can be used as a base for a minimal PNPM monorepo that also handles Docker based deployments of the apps that it contains.

## Getting started

Clone this repo and start adjusting it to your needs.

## Included

- one example **package** (`packages/ui`) intended to be used as a starting place for a shareable component library.
- two example **apps** in (`apps/remix-app-1` and `apps/remix-app-2`) that can import components from the shared package using the `~ui` **TypeScript path alias**.
- `Dockerfiles` for **deployment** inside both app dirs and a handy `.github/workflows/deploy.yml` script.
- some useful **run scripts** in the root `package.json` for managing PNPM and Docker related tasks.

## Not Included (on purpose)

- **Turborepo** - this template is intended to be _MINIMAL_ and basic features of Turborepo, such as filtering app run scripts, are already available in PNPM.
- **build step** for the shared package - transpiling and bundling is offloaded to the consuming apps.
- **oppinionated deployment** step in the GitHub Actions file - it does everything up to and including building the Docker images; what you do with them is up to you.

## Acknowledgements

Special thanks to [PhilDL](https://twitter.com/_philDL) and the [Remix Gospel Stack](https://github.com/PhilDL/remix-gospel-stack) for the inspiration. If you need something more complex than this basic starter then definitively check out his project!
