# A reusable GHA workflow for Moodle plugins

This repo holds a reusable workflow file for testing Moodle plugins in the GHA CI pipeline.

It has been sourced and modified from the [template](https://github.com/moodlehq/moodle-plugin-ci/blob/main/gha.dist.yml) provided by [moodle-plugin-ci](https://moodlehq.github.io/moodle-plugin-ci/) project.

## Usage

In your Moodle plugin repository, create a `.gihub/workflows/ci.yml` file with the following contents

```yml
name: Moodle Plugin CI

on:
  push:
  pull_request:
  schedule:
    - cron: "33 2 * * 1" # weekly, on Monday morning

jobs:
  ci:
    uses: ucsf-education/moodle-plugin-ci-reusable-workflow/.github/workflows/gha.yml@MOODLE_501_STABLE
```

## Update to support new Moodle version

1. Check the "Server requirements" section for the targeted [Moodle release](https://moodledev.io/general/releases) we're moving to.
2. Check the [moodle-plugin-ci](https://github.com/moodlehq/moodle-plugin-ci) for any changes to the [workflow template](https://github.com/moodlehq/moodle-plugin-ci/blob/main/gha.dist.yml). Look for PHP, database, and OS changes in particular.
3. branch the current default branch with a name that reflects the target Moodle version. For example, if we're targeting Moodle 5.2, then the branch name should be `MOODLE_502_STABLE`. 
4. In the new branch, realign the workflow file with the template and server requirements. **Achtung!** Don't forget to update the value of the `moodle-branch` setting in the test matrix section to match the targeted Moodle version, for example: `moodle-branch: ['MOODLE_502_STABLE']`. Push the new branch up to the repo.
5. In your Moodle plugins that utilize the reusable workflow, as part of their version upgrade, update the target branch suffix in their workflow file. For example, change `ucsf-education/moodle-plugin-ci-reusable-workflow/.github/workflows/gha.yml@MOODLE_501_STABLE` to `ucsf-education/moodle-plugin-ci-reusable-workflow/.github/workflows/gha.yml@MOODLE_502_STABLE` if you're upgrading to Moodle 5.2.






