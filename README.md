# Setup Swift
<p>
  <a href="https://swift.org">
    <img src=".github/swift.svg" height="20" alt="Swift" />
  </a>
  <a href="https://github.com/features/actions">
    <img src="https://img.shields.io/badge/GitHub-Action-blue?logo=github" alt="GitHub Action" />
  </a>
  <a href="https://help.github.com/en/actions/automating-your-workflow-with-github-actions/virtual-environments-for-github-hosted-runners#supported-runners-and-hardware-resources">
    <img src="https://img.shields.io/badge/OS-macOS+Ubuntu-brightgreen" alt="Supports macOS and Ubuntu" />
  </a>
</p>

[GitHub Action](https://github.com/features/actions) that will setup a [Swift](https://swift.org) environment with a specific version. Works on both Ubuntu and macOS runners.

## Usage

To run the action with the latest swift version available, simply add the action as a step in your workflow:

```yaml
- uses: fwal/setup-swift@master
```

After the environment is configured you can run swift commands using the standard [`run`](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions#jobsjob_idstepsrun) step:
```yaml
- uses: fwal/setup-swift@master
- name: Get swift version
  run: swift --version # Swift 5.1.1
```

A specific Swift version can be set using the `swift-version` input:

```yaml
- uses: fwal/setup-swift@master
  with:
    swift-version: "5.1.0"
- name: Get swift version
  run: swift --version # Swift 5.1.0
```

Works perfect together with matrixes: 

```yaml
name: Swift ${{ matrix.swift }} on ${{ matrix.os }}
runs-on: ${{ matrix.os }}
strategy:
  matrix:
    os: [ubuntu-latest, macos-latest]
    swift: ["5.1.0", "4.2.4"]
steps:
- uses: fwal/setup-swift@master
  with:
    swift-version: ${{ matrix.swift }}
- name: Get swift version
  run: swift --version
```

## Note about versions

This project uses strict semantic versioning to determine what version of Swift to configure. This differs slightly from the official convention used by Swift.

For example, Swift is available as version `5.1` but this will be interpreted as a version _range_ of `5.1.X` where `X` is the latest patch version available for that major and minor version.


In other words specifying...
- `"5.1.0"` will resolve to version `5.1`
- `"5.1"` will resolve to latest patch version (aka `5.1.1`)
- `"5"` will resolve to latest minor and patch version (aka `5.1.1`)


## Legal
Uses MIT license. 
The Swift logo is a trademark of Apple Inc.
