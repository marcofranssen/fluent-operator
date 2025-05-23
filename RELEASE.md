# Releases

This page describes the release process and the currently planned schedule for upcoming releases as well as the respective release shepherd.

## Release schedule

| release series | date (year-month-day) | release shepherd                        |
| -------------- | --------------------- | --------------------------------------- |
| v0.1.0         | 2020-02-17            | Guangzhe Huang (GitHub: @huanggze)      |
| v0.2.0         | 2020-08-27            | Guangzhe Huang (GitHub: @huanggze)      |
| v0.3.0         | 2020-11-10            | Guangzhe Huang (GitHub: @huanggze)      |
| v0.4.0         | 2021-04-01            | Wanjun Lei (GitHub: @wanjunlei)         |
| v0.5.0         | 2021-04-14            | Wanjun Lei (GitHub: @wanjunlei)         |
| v0.6.0         | 2021-06-03            | Wanjun Lei (GitHub: @wanjunlei)         |
| v0.6.1         | 2021-06-11            | Benjamin Huo (GitHub: @benjaminhuo)     |
| v0.6.2         | 2021-06-11            | Benjamin Huo (GitHub: @benjaminhuo)     |
| v0.7.0         | 2021-06-29            | Wanjun Lei (GitHub: @wanjunlei)         |
| v0.7.1         | 2021-07-09            | Wanjun Lei (GitHub: @wanjunlei)         |
| v0.8.0         | 2021-07-23            | Wanjun Lei (GitHub: @wanjunlei)         |
| v0.9.0         | 2021-08-13            | Wanjun Lei (GitHub: @wanjunlei)         |
| v0.10.0        | 2021-08-20            | Wanjun Lei (GitHub: @wanjunlei)         |
| v0.11.0        | 2021-09-01            | Wanjun Lei (GitHub: @wanjunlei)         |
| v0.12.0        | 2021-09-13            | Wanjun Lei (GitHub: @wanjunlei)         |
| v0.13.0        | 2022-03-14            | Elon Cheng (GitHub: @wenchajun)         |
| v1.0.0         | 2022-03-25            | Elon Cheng (GitHub: @wenchajun)         |
| v1.0.1         | 2022-05-12            | Elon Cheng (GitHub: @wenchajun)         |
| v1.0.2         | 2022-05-17            | Elon Cheng (GitHub: @wenchajun)         |
| v1.1.0         | 2022-06-15            | Elon Cheng (GitHub: @wenchajun)         |
| v1.5.0         | 2022-09-24            | Elon Cheng (GitHub: @wenchajun)         |
| v1.5.1         | 2022-09-30            | Elon Cheng (GitHub: @wenchajun)         |
| v1.6.0         | 2022-10-25            | Elon Cheng (GitHub: @wenchajun)         |
| v1.6.1         | 2022-10-31            | Elon Cheng (GitHub: @wenchajun)         |
| v1.7.0         | 2022-11-23            | Elon Cheng (GitHub: @wenchajun)         |
| v2.0.0         | 2023-02-03            | Elon Cheng (GitHub: @wenchajun)         |
| v2.0.1         | 2023-02-08            | Elon Cheng (GitHub: @wenchajun)         |
| v2.1.0         | 2023-03-13            | Elon Cheng (GitHub: @wenchajun)         |
| v2.2.0         | 2023-04-07            | Elon Cheng (GitHub: @wenchajun)         |
| v2.3.0         | 2023-06-05            | Elon Cheng (GitHub: @wenchajun)         |
| v2.4.0         | 2023-07-19            | Elon Cheng (GitHub: @wenchajun)         |
| v2.5.0         | 2023-09-13            | Elon Cheng (GitHub: @wenchajun)         |
| v2.6.0         | 2023-11-22            | Elon Cheng (GitHub: @wenchajun)         |
| v2.7.0         | 2023-12-19            | Anthony Treuillier (GitHub: @antrema)   |
| v2.8.0         | 2024-04-22            | Zhang Peng (GitHub: @Gentleelephant)    |
| v2.9.0         | 2024-06-13            | Elon Cheng (GitHub: @wenchajun)         |
| v3.0.0         | 2024-07-09            | Elon Cheng (GitHub: @wenchajun)         |
| v3.1.0         | 2024-08-14            | Zhang Peng (GitHub: @Gentleelephant)    |
| v3.2.0         | 2024-09-21            | Chengwei Guo (GitHub: @cw-Guo)          |
| v3.3.0         | 2025-02-27            | Chengwei Guo (GitHub: @cw-Guo)          |
| v3.4.0         | 2025-05-08            | Marco Franssen (GitHub: @marcofranssen) |
| v3.5.0         | 2025-10-24            | Josh Baird (GitHub: @joshuabaird)       |

## Operator release process

This document describes the process of cutting a new release of Fluent Operator. It is intended for maintainers and contributors who are responsible for managing the release process. Releases use [semantic versioning](https://semver.org/). The actual release is published by a GitHub Actions workflow.

### Major/Minor releases

Releases are cut from the `master` branch of the repository. The release process involves the following steps:

1. Create a PR to prepare the release.

   ```shell
   git checkout master
   git pull upstream master
   git checkout -b release-X.Y master
   ```

   This PR should include the following changes:

    * Update the `version` field in the `Chart.yaml` file to the new version number.
    * Update the `appVersion` field in the `Chart.yaml` file to the new version number.
    * Update the `CHANGELOG.md` file with a summary of changes since the last release.
    * Update the `RELEASE.md` file with the new release date and shepherd information.

2. Once the PR is reviewed and approved, merge it into the `master` branch.

3. Create a new tag for the release. The tag should follow the format `vX.Y.Z`, where `X` is the major version, `Y` is the minor version, and `Z` is the patch version. For example, for version 1.0.0, the tag should be `v1.0.0`.

### Patch releases

Patch releases are created for bug fixes and minor improvements. They should not introduce any breaking changes. The process for creating a patch release is the same as for a major or minor release, but the version number should be incremented in the patch version (e.g., from `v1.0.0` to `v1.0.1`).

1. Create a PR to prepare the patch release.

   ```shell
   git checkout release-X.Y
   git pull upstream release-X.Y
   git checkout -b patch-X.Y.Z release-X.Y
   ```

   Now cherry-pick the commits from the `master` branch that you want to include in the patch release. You can use the `git cherry-pick` command to do this.

   ```shell
   git cherry-pick <commit-hash>
   ```

   Repeat this step for each commit you want to include in the patch release.

   This PR should include the following changes:

    * Update the `version` field in the `Chart.yaml` file to the new version number.
    * Update the `appVersion` field in the `Chart.yaml` file to the new version number.
    * Update the `CHANGELOG.md` file with a summary of changes since the last release.
    * Update the `RELEASE.md` file with the new release date and shepherd information.

## FluentBit release process

To publish a new fluent-bit image:

* Execute the [bump-fluent-bit-version](https://github.com/fluent/fluent-operator/actions/workflows/bump-fluent-bit-version.yaml) workflow dispatch to generate a PR to update fluent-bit version references in this repo
* Merge the PR generated by the [bump-fluent-bit-version](https://github.com/fluent/fluent-operator/actions/workflows/bump-fluent-bit-version.yaml) workflow. (This will [automatically trigger the release](https://github.com/fluent/fluent-operator/blob/master/.github/workflows/build-fluentbit-image.yaml#L4-L8) of
 the new fluent-bit image)

### Fluentd release process

To publish a new fluentd image:

* Open a PR to update all references of the image/tag in this repo with the new image tag (TODO: automate this like the fluent-bit release process) including the `cmd/fluent-watcher/fluentd/VERSION` file
* Merge the PR
* Execute the [publish-fluentd-image](https://github.com/fluent/fluent-operator/actions/workflows/publish-fluentd-image.yaml) workflow dispatch to build and publish the new image
