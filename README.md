# generator-spfx-conventionalcommits

Add changelog generation based on [conventional commits](https://conventionalcommits.org/) convention to your rush monorepos.
See the [Rush and Conventional Commits Series](https://dev.to/kkazala/series/17133) for detailed description.

## Prerequisites

Project managed with rush. Run:

- `rush init`
- `rush update`

## Rush configuration

### autoinstallers

- **rush-commitlint**: rush autoinstaller installing `@commitlint/cli` and `@commitlint/config-conventional`
- **rush-changemanager**: rush autoinstaller installing `@microsoft/rush-lib`, `@rushstack/node-core-library`, `gitlog` and `recommended-bump`

### custom commands

- **commitlint** runs `commitlint` on the commit messages; used by the commit-msg Git hook.
- **changefiles** executes the custom `rush-changefiles.js` script to create rush change files, if necessary

### git-hooks

- **commit-msg** invokes `rush commitlint` custom command to ensure the commit message has correct format
- **post-commit** invokes `rush changefiles` custom command to generate rush change files, if necessary
- **pre-push** (optional) invokes `rush change -v` to verify change files are generated for changed projects

### scripts

- **scripts/rush-changefiles.js** this is where the magic happens. Invoked by `rush changefiles` during `post-commit`, parses the commit message and based on the conventional commits specification, decides whether a new change file should be created.
Types `fix:`, `feat:` or `BREAKING CHANGE:` will cause generation of a new change file, if the commit message has not been used just before.

> **Important**: If you want to generate change files for other commit messages types, install the `pre-push` hook. It will remind you to generate change files before `git push`, if none exist for the project.
