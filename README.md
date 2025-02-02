[![Build Status](https://github.com/CycloneDX/cyclonedx-cocoapods/actions/workflows/ruby.yml/badge.svg)](https://github.com/CycloneDX/cyclonedx-cocoapods/actions/workflows/ruby.yml)
[![Gem Version](https://badge.fury.io/rb/cyclonedx-cocoapods.svg)](https://badge.fury.io/rb/cyclonedx-cocoapods)
[![License](https://img.shields.io/badge/license-Apache%202.0-brightgreen.svg)][License]
[![Website](https://img.shields.io/badge/https://-cyclonedx.org-blue.svg)](https://cyclonedx.org/)
[![Slack Invite](https://img.shields.io/badge/Slack-Join-blue?logo=slack&labelColor=393939)](https://cyclonedx.org/slack/invite)
[![Group Discussion](https://img.shields.io/badge/discussion-groups.io-blue.svg)](https://groups.io/g/CycloneDX)
[![Twitter](https://img.shields.io/twitter/url/http/shields.io.svg?style=social&label=Follow)](https://twitter.com/CycloneDX_Spec)


# CycloneDX CocoaPods (Objective-C/Swift)

The CycloneDX CocoaPods Gem creates a valid CycloneDX software bill-of-material document from all [CocoaPods](https://cocoapods.org/) project dependencies. CycloneDX is a lightweight BoM specification that is easily created, human readable, and simple to parse.

## Installation

### From RubyGems

```shell
% gem install cyclonedx-cocoapods
```

### From Source

First, clone/copy the source code from GitHub.  Then in the source code directory run these ommands:

```shell
gem build cyclonedx-cocoapods.gemspec
gem install cyclonedx-cocoapods-x.x.x.gem
```

Building from source requires Ruby 2.4.0 or newer.

## Compatibility

*cyclonedx-cocoapods* aims to produce SBOMs according to the latest CycloneDX specification, which currently is [1.4](https://cyclonedx.org/docs/1.4/).
You can use the [CycloneDX CLI](https://github.com/CycloneDX/cyclonedx-cli#convert-command) to convert between multiple BOM formats or specification versions.

## Usage
```
Generates a BOM with the given parameters. BOM component metadata is only generated if the component's name, version, and type are provided using the --name, --version, and --type parameters.
[version <version_number>]

USAGE
  cyclonedx-cocoapods [options]

OPTIONS
        --[no-]verbose               Show verbose debugging output
    -h, --help                       Show help message

  BOM Generation
    -p, --path path                  Path to CocoaPods project directory (default: current directory)
    -o, --output bom_file_path       Path to output the bom.xml file to (default: "bom.xml")
    -b, --bom-version bom_version    Version of the generated BOM (default: "1")
    -x, --exclude-test-targets       Eliminate Podfile targets whose name contains the word "test"

  Component Metadata
    -n, --name name                  (If specified version and type are also required) Name of the component for which the BOM is generated
    -v, --version version            Version of the component for which the BOM is generated
    -t, --type type                  Type of the component for which the BOM is generated (one of application|framework|library|container|operating-system|device|firmware|file)
    -g, --group group                Group of the component for which the BOM is generated
```

**Output:** BoM file at specified location, `./bom.xml` if not specified

### Example

```shell
% cyclonedx-cocoapods --path /path/to/cocoapods/project --output /path/to/bom.xml --version 6 
```

#### Specific example

This repo contains a file named `example_bom.xml` that was generated with this tool.

It represents the open source [PodsUpdater application](https://github.com/kizitonwose/PodsUpdater).  The PodsUpdater code was checked out,
then these two commands were run in the checked out code directory.

```shell
% pod install
% cyclonedx-cocoapods -n "kizitonwose/PodsUpdater" -v 1.0.3 -t application --output example_bom.xml
```

## Contributing

To set up for local development, make a fork of this repo, make a branch on your fork named after the issue or workflow you are improving, checkout your branch, then run `bundle install`.

### Right to Contribute

This project runs the [DCO](https://probot.github.io/apps/dco/) checker to validate that the code author has the right to submit the code they are
contributing to the project.  Please verify that you do have the right to contribute, then when running `git commit` add the `-s` flag to
automatically add the proper `Signed-off-by` line to the commit message.

### Pull requests

Before submitting your pull request, please do the following:

- Run `rake spec` and make sure all the tests pass. If you are adding new commands or features, they must include tests. If you are changing functionality, update the tests or add new tests as needed.
- Add a note to the CHANGELOG describing what you changed.
- Make your pull request. If it is related to an issue, add a link to the issue in the description.

## Copyright & License
Permission to modify and redistribute is granted under the terms of the Apache 2.0 license. See the [LICENSE] file for the full license.

[License]: https://github.com/CycloneDX/cyclonedx-cocoapods/blob/master/LICENSE
