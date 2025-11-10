This repository is a multi-week course site with many example projects. The following notes give focused, actionable guidance for an AI coding agent to be productive here.

- Project layout
  - `site/` is the primary web app: an Angular 1.x single-page app with source in `site/src/`, build tasks in `site/gulp_tasks/`, and configs in `site/conf/`.
  - Course materials and example projects live under `week*/` folders. Treat these as mostly standalone examples (do not change broadly unless requested).

- Quick commands (run from repository root)
  - Install and run the dev site:
    - npm install (run in `site/` if you only work on the web app)
    - npm run serve (defined in `site/package.json` -> runs `gulp serve`)
  - Build production bundle: `npm run build` (calls `gulp`, which uses `webpack:dist` via `site/gulp_tasks/webpack.js`).
  - Tests: `npm test` (maps to `gulp test`, uses Karma configs in `site/conf/`)

- Build & dev details
  - Gulp orchestrates tasks (`site/gulpfile.js`); task implementations live in `site/gulp_tasks/*.js` (notably `webpack.js` for bundling and `browsersync.js` for live reload).
  - Webpack configs are in `site/conf/webpack.conf.js` and `site/conf/webpack-dist.conf.js`.
  - `site/conf/gulp.conf.js` contains path helpers and shared error handling; reference it when adding gulp tasks.

- Architecture & important patterns
  - The web app is an Angular 1.x app assembled in `site/src/index.js`. It registers components located under `site/src/app/` and uses `angular-ui-router` for routing (`site/src/routes.js`).
  - CSS is imported in `site/src/index.js` (see `require('./index.css')`) and goes through webpack loaders defined in the webpack config.
  - Many weekly examples are static or small p5.js sketches (look under `week*/`); they may not follow the same build pipeline as `site/`.

- Conventions and code patterns to follow
  - Minimal, focused changes for examples: modify only files within a given `week*` example unless the task explicitly targets `site/`.
  - When changing web app behavior, update the corresponding Angular component under `site/src/app/` and the route in `site/src/routes.js`.
  - Use existing gulp tasks where possible. Add tasks in `site/gulp_tasks/` and wire them in `site/gulpfile.js`.

- Tests and CI hints
  - Karma configs live in `site/conf/` (`karma.conf.js`, `karma-auto.conf.js`); the gulp task `karma:single-run` is used for `npm test`.
  - Unit tests for site components live alongside source as `*.spec.js` (e.g. `site/src/index.spec.js`).

- Integration and external deps
  - Dependencies are declared in `site/package.json`. The site uses legacy Angular 1.x and several gulp/webpack plugins pinned to older versions—avoid upgrading major versions without running the build/tests.
  - Browser sync is used in development for live reload (`browsersync.js` and `conf/browsersync.conf.js`).

- Files to inspect first for new tasks
  - `site/src/index.js` — app bootstrap and component registration.
  - `site/gulpfile.js` and `site/gulp_tasks/webpack.js` — dev / build flow.
  - `site/conf/webpack*.js` and `site/conf/gulp.conf.js` — path helpers, loaders, and env differences.
  - `site/package.json` — scripts and dependency pins.

- Examples to include when describing code changes
  - If modifying routing or components, show the diff touching `site/src/routes.js` and `site/src/app/<component>/`.
  - For build changes, reference `site/gulp_tasks/webpack.js` and `site/conf/webpack-dist.conf.js`.

- Safety and scope rules for the agent
  - Do not refactor or modernize Angular 1.x across the repo unless explicitly requested. This repo contains many historical examples; broad changes can break examples and the build.
  - Prefer small, isolated edits (single component or single example directory) and run the local dev build/test to validate.

If any area is unclear — for example which `week*` example should be used for a change, or if the task targets the `site/` app vs. a standalone example — ask a short clarifying question before making wide changes.

Please review and tell me which sections to expand or any examples you'd like included.
