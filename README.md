# generator-spfx-conventionalcommits

## Rush configuration

## Git hooks

- commit-msg: commitlint
- post-commit: generate rush change files in changes require semver increase
- pre-push (optional): to ensure rush change files created for all changed projects (in case only changes not causing semver increase were commited)