# Pixelfed photo sharing

Photo sharing application powered by Laravel/PHP and ActivityPub federation, with a Vue frontend and media processing jobs.

This repository is a separately imported source snapshot of [pixelfed](https://github.com/pixelfed/pixelfed). Upstream contributors created the imported application; local work is recorded in the commits after the source import. See [Upstream source](UPSTREAM_SOURCE.md) for attribution.

## Read the history accurately

The local history starts with a source import on November 3, 2026. The parent year directory and the “Original project year” field do not establish a historical contribution date or a release tag. The imported upstream commit and release are not recorded in the available provenance file.

## Navigate the source

| Path | Responsibility |
| --- | --- |
| [app/](app/) | Application, federation, and media logic |
| [routes/](routes/) | HTTP and API routes |
| [resources/](resources/) | Frontend resources |
| [tests/](tests/) | PHP tests |
| [DOCKER_COMPOSE_SETUP.md](DOCKER_COMPOSE_SETUP.md) | Container setup guidance |

## Prepare development

Read `composer.json`, `package.json`, `.env.example`, and `DOCKER_COMPOSE_SETUP.md`. Match the declared PHP version and extensions. Configure the database, Redis, and media processing before running the application. `composer test` starts the test Compose stack; inspect `docker-compose.test.yml` before use.

The commands below are existing project entry points, to run after their toolchain, dependency, and service prerequisites are ready:

```sh
composer test:quick
composer lint:test
npm run production
```

## Validation scope

The documentation change was checked for local link targets, manifest command references, and whitespace errors. Application builds, dependency installation, and service-backed test suites were not run for this documentation change. These instructions do not establish deployment readiness.

## Preserve upstream licensing

Read [LICENSE](LICENSE) and the notices in individual source files. This documentation does not change the license of imported code.

## Install and run locally

Match the PHP version/extensions in `composer.json` and the Node.js version in `.node-version`. Prepare the environment and locked dependencies:

```sh
cp .env.example .env
composer install
npm ci
php artisan key:generate
npm run development
```

Set the database, Redis, public URL, and storage configuration in `.env`. Use `DOCKER_COMPOSE_SETUP.md` for the container setup, or a dedicated local database before initializing schema with `php artisan migrate`. Run the PHP application with `php artisan serve` for local development and configure the queue worker for background media processing.

## Plan a deployment

Review `Dockerfile`, `.env.docker.example`, and `DOCKER_COMPOSE_SETUP.md`. The Compose environment includes database and Redis services; use unique credentials, persistent storage, and a public HTTPS URL. Review backup, queue, scheduler, and media-processing requirements before exposing federation endpoints.
