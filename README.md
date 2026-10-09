# Privacy policies

Published privacy policies for Endroid apps.

## Weekly sync

The **Sync privacy policies** GitHub Actions workflow runs every Monday at
07:17 UTC (08:17 in Amsterdam in winter, 09:17 in summer). It can also be run
manually from the Actions tab.

It copies every `apps/<game>/play/privacy-policy.html` on `endroid/android-dev`'s
`main` branch to `<game>.html` at this repository's root, preserving the file
contents. New, changed, and removed policies are committed directly to `main`.
No commit is created when there are no changes. Root-level HTML policies
without a matching source are deleted; if the source checkout contains no
policies, all root-level HTML policies are removed. A failed source checkout
stops the job before syncing. Other files are left untouched.

### Required setup

1. Add an Actions repository secret named `ANDROID_DEV_READ_TOKEN` containing a
   fine-grained personal access token with **Contents: Read-only** access to the
   private `endroid/android-dev` repository.
2. Add an Actions repository secret named `PRIVACY_POLICY_WRITE_TOKEN` containing
   a fine-grained personal access token with **Contents: Read and write** access
   to `endroid/privacy-policy`. Its owner must be allowed to push to `main`.
   A personal access token is used instead of `GITHUB_TOKEN` because pushes with
   `GITHUB_TOKEN` do not trigger this repository's branch-based GitHub Pages build.
3. Approve both tokens in the organization if required. The workflow must be on
   `main` for the weekly schedule to run. No pull-request permissions are needed.
