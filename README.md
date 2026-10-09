# Privacy policies

Published privacy policies for Endroid apps.

## Weekly sync

The **Sync privacy policies** GitHub Actions workflow runs every Monday at
07:17 UTC (08:17 in Amsterdam in winter, 09:17 in summer). It can also be run
manually from the Actions tab.

It copies every `apps/<game>/play/privacy-policy.html` on `endroid/android-dev`'s
`main` branch to `<game>.html` at this repository's root, preserving the file
contents. New and changed policies are proposed in one pull request on
`automation/sync-privacy-policies`; later runs update that same pull request.
No pull request is created when there are no changes. Policies without a
matching source are not deleted. Review and merge the pull request to publish.

### Required setup

1. Add an Actions repository secret named `ANDROID_DEV_READ_TOKEN` containing a
   fine-grained personal access token with **Contents: Read-only** access to the
   private `endroid/android-dev` repository. Approve the token in the organization
   if required. The workflow does not use this token to write to either repository.
2. In **Settings → Actions → General → Workflow permissions**, enable
   **Allow GitHub Actions to create and approve pull requests** (the organization
   must permit this). The workflow uses this repository's `GITHUB_TOKEN` with
   contents and pull-request write permissions to propose updates; it does not
   approve or merge them.
3. Merge the workflow pull request into `main` to enable the weekly schedule.
