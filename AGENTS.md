# Agent Instructions

This repository requires Node dependencies to run tests and the dev server.

- Run `npm install` followed by `npm run build` before executing tests or starting the server.
- `nyc` and other dev tools are included in `package.json`; they will be installed via `npm install`.
- In read-only environments, use a setup script (e.g. `.codex/setup.sh`) to install these dependencies before the repository becomes read-only.

## Testing

Run `npm test` after installation.

## Running the Simulator

After installing dependencies and building, start the server with `npm run start` and open the provided URL in a browser.
