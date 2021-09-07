# version-autobump-action

Automatically bump android project version when merging to production

This Action bumps the version in build.gradle and pushes it back to the repo. It is meant to be used on every successful merge to master but you'll need to configured that workflow yourself.

**Attention**

Make sure you use the `actions/checkout@v2` action!

### Workflow

* Based on the commit messages, increment the version from the latest release.
    * If the string "BREAKING CHANGE", "major" or the Attention pattern `refactor!: drop support for Node 6` is found
      anywhere in any of the commit messages or descriptions the major version will be incremented.
    * If a commit message begins with the string "feat" or includes "minor" then the minor version will be increased.
      This works for most common commit metadata for feature additions: `"feat: new API"` and `"feature: new API"`.
    * If a commit message contains the word "pre-alpha" or "pre-beta" or "pre-rc" then the pre-release version will be
      increased (for example specifying pre-alpha: 1.6.0-alpha.1 -> 1.6.0-alpha.2 or, specifying pre-beta: 1.6.0-alpha.1
      -> 1.6.0-beta.0)
    * All other changes will increment the patch version.
* Push the bumped version in build.gradle back into the repo.
* Push a tag for the new version back into the repo.