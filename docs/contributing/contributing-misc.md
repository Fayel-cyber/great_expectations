---
title: Contributing Misc and CLA
---

## Contributor license agreement (CLA)
When you contribute code, you affirm that the contribution is your original work and that you license the work to the project under the project’s open source license. Whether or not you state this explicitly, by submitting any copyrighted material via pull request, email, or other means you agree to license the material under the project’s open source license and warrant that you have the legal authority to do so.

Please make sure you have signed our Contributor License Agreement (either Individual Contributor License Agreement v1.0 or Software Grant and Corporate Contributor License Agreement (“Agreement”) v1.0).

We are not asking you to assign copyright to us, but to give us the right to distribute your code without restriction. We ask this of all contributors in order to assure our users of the origin and continuing existence of the code. You only need to sign the CLA once.

## Release checklist
GE core team members use this checklist to ship releases.

If this is a major release (incrementing either the first or second version number) the manual acceptance testing must be completed.

This private google doc outlines the procedure. (Note this will be made public eventually)

Merge all approved PRs into develop.

Make a new branch from develop called something like release-prep-2020-06-01.

In this branch, update the version number in the great_expectations/deployment_version file.

Update the changelog.rst: move all things under the Develop heading under a new heading with the new release number. NOTE: You should remove the Develop heading for the released version, it will be replaced in step #12.

Verify that any changes to requirements are specifically identified in the changelog

Double check the grouping / order of changes matches [BREAKING], [FEATURE], [ENHANCEMENT], [BUGFIX], [DOCS], [MAINTENANCE] and that all changes since the last release are mentioned or summarized in a bullet.

Make sure to shout out community contributions in the changelog! E.g. after the change title add (thanks @<contributor_id>)

Submit this as a PR against develop

After successful checks, get it approved and merged.

Update your local branches and switch to main: git fetch --all; git checkout main; git pull.

Merge the now-updated develop branch into main and trigger the release: git merge origin/develop; git push

Wait for all the builds to complete. The builds should include several test jobs and a deploy job, which handles the actual publishing of code to pypi. You can watch the progress of these builds on Azure.

Check PyPI for the new release

Create an annotated git tag:

````console
Run git tag -a <<VERSION>> -m "<<VERSION>>" with the correct new version.

Push the tag up by running git push origin <<VERSION>> with the correct new version.

Merge main into develop so that the tagged commit becomes part of the history for develop: git checkout develop; git pull; git merge main
````

On develop, add a new “Develop” section header to changelog.rst, and push the updated file with message “Update changelog for develop”

Create the release on GitHub with the version number. Copy the changelog notes into the release notes, and update any rst-specific links to use github issue numbers.

The deploy step will automatically create a draft for the release.

Generally, we use the name of the tag (Ex: “0.11.2”) as the release title.

Notify kyle@superconductive.com about any community-contributed PRs that should be celebrated.

Socialize the release on GE slack by copying the changelog with an optional nice personal message (thank people if you can)

Review and merge the automatically-generated PR for conda-forge/great-expectations-feedstock, updating requirements as necessary and verifying the build status.

To list requirements changed since a previous version of GE, you can run git diff <<old_tag_e.g._0.12.6>>..<<new_tag_e.g._0.12.7>> -- requirements.txt. If there are differences, update the requirements section of recipe/meta.yaml. This is an important step as this is not done automatically when the PR is generated.

In most cases, the PR will change the SHA and version number. Check the commits for other changes, they may be maintenance changes from the Conda dev team which are OK to merge.

Review all items on the conda-forge CI system and PR checklist. The active conda-forge community frequently updates build processes and testing, and may help discover issues not observed in our pypi deployment process.

If you need to re-run a failing build and don’t have appropriate permissions or you don’t have permissions to merge please refer to the Account Permissions Overview on the superconductive internal wikiwiki for who to ask. Other conda-forge community partners are extremely responsive and may be able to help resolve issues quickly.

Check for open issues in the GE conda-forge repository. If there are open issues that do not have a corresponding issue in the main GE repo, please create an issue in the GE repo with a link to the corresponding conda issue (e.g. issue #2021). This allows us to internally triage and track the issue.

Celebrate! You have successfully released a new version of Great Expectations!!

## Beta Release Notes

To ship a beta release, follow the above checklist, but use the branch name v0.11.x as the equivalent of main and v0.11.x-develop as the equivalent of develop

Ship the release using beta version numbers when updating the great_expectations/deployment_version and when creating the annotated tag (e.g. 0.11.0b0)

## Issue Tags
We use stalebot to automatically tag issues without activity as stale, and close them if no response is received in one week. Adding the stalebot-exempt tag will prevent the bot from trying to close the issue.

Additionally, we try to add tags to indicate the status of key discussion elements:

help wanted covers issues where we have not prioritized the request, but believe the feature is useful and so we would welcome community contributors to help accelerate development.

enhacement and expectation-request indicate discussion of potential new features for Great Expectations

good first issue indicates a small-ish task that would be a good way to begin making contributions to Great Expectations


