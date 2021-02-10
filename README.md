# FHIR-ePMA-Implementation

Implementation guidance for the use of the FHIR medicationRequest resource for the use case of electronic hospital patient medicines administration (ePMA) systems interoperability with hospital pharmacy / stock control systems. The medicationRequest acts as a medication order request to the pharmacy for a given patient under case on the ward.

This guidance will be applicable to both STU3 and R4 implementations of th FHIR standard. It will highlight differences between the STU3 and R4 medicationRequest resource and provide guidance on how to future proof an STU3 implementation if an uplift to R4 is expected.

Current approved version published on [https://developer.nhs.uk/apis/epma-implementation-1.0.1-alpha/index.html](https://developer.nhs.uk/apis/epma-implementation-1.0.1-alpha/index.html)

## Installation requirements

- Ruby (latest)
- Jekyll

**Note** It's advisable that you delete the `Gemfile.lock` file before running `bundle exec jekyll serve`; however, please ensure that you do not commit your version of the `Gemfile.lock` file that will be created when running within your environment.

## Contribution guidance

To contribute to the repository, please ensure you update your local repository so it is inline with the latest changes with the origin e.g. `git fetch` and `git pull`.

### Branching strategy

This repository uses [GitHub Flow](https://guides.github.com/introduction/flow/) for the branching strategy.

#### Branches

- master (default)
- feature/\[my-new-feature\] (feature branches with pending changes)

#### Making a contribution

Please do not commit to the `master` branch directly. Instead, please create a feature branch with an appropriate name - for example:

`git checkout -b feature/my-new-feature`

##### Commit messages

Please ensure your commit messages are relevant to the feature you're creating - for example:

`git commit -m "Fixed spelling mistake in README.md"`

#### Making a Pull / Merge request

Please create a pull/merge request to merge into the `master` branch upon successful review by the [contributors](https://github.com/nhsconnect/Dose-Syntax-Implementation/graphs/contributors) of this repository.

#### GitHub pages

Merges `master` branch will automatically be pushed to [GitHub page.](https://nhsconnect.github.io/FHIR-ePMA-Implementation/)

**Please note:** The approved guidance by [IOPS](https://architecture.digital.nhs.uk/trg/iccc) is hosted [on the NHS developer platform](https://developer.nhs.uk/apis/epma-implementation-1.0.1-alpha/index.html).

The GitHub pages version of the Dose Syntax Implementation guidance may differ from the official version.
