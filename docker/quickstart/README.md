# Docker quickstart

The files in this folder provide a copy–pasteable way to run Copyparty locally with Docker or Podman.

## Run

1. From the repository root, start the stack:

   ```bash
   docker compose -f docker/quickstart/compose.yml up -d
   ```

   - On Podman: `podman compose -f docker/quickstart/compose.yml up -d`
   - The server listens on http://localhost:3923

2. Log in with the default account:
   - user: `admin`
   - password: `changeme`

## Customise

- Change the password (recommended) by setting an environment variable before starting:

  ```bash
  PRTY_ADMIN_PASSWORD="supersecret" docker compose -f docker/quickstart/compose.yml up -d
  ```

- Override the exposed port or image tag with `.env` values:

  ```ini
  COPYPARTY_PORT=8080
  COPYPARTY_IMAGE=copyparty/ac:latest
  ```

- Your shared files live in `docker/quickstart/data/` (mounted at `/w`).
- Config, search index, and thumbnails live in `docker/quickstart/cfg/` (mounted at `/cfg`).
- The volume flag in `compose.yml` is `-v /w::rw,admin` (note the double colon) which mounts `/w` as the site root, readable/writable by `admin`.

## Notes

- The compose file sets `--hist /cfg/hists` so the index/thumbnails stay alongside the config.
- The volume is secured: only the `admin` account can read or write. Add more accounts or volumes by extending the compose `command` with extra `-a` / `-v` flags (see `scripts/docker/README.md` for syntax).
