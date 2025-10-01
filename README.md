[![Test](https://github.com/cucumber/action-publish-mvn/actions/workflows/test.yaml/badge.svg)](https://github.com/cucumber/action-publish-mvn/actions/workflows/test.yaml)

# action-publish-mvn

Publishes a Java module to [Maven Central](https://search.maven.org/)

Needs Java to be installed first.

## Inputs

* `gpg-private-key`
* `gpg-passphrase`
* `nexus-username`
* `nexus-password`
* `server-id` (default: `ossrh`)
* `maven-goals` (default: `deploy`)
* `maven-profiles` (default: `sign-source-javadoc`)
* `working-directory` (default `.`)

## Example

```yaml
name: Publish

on:
  push:
    branches:
      - "release/*"

jobs:
  publish-ui:
    name: Publish UI package to mvn
    runs-on: ubuntu-latest
    environment: Release
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-java@v1
        with:
          java-version: '17'
      - name: Test the action
        uses: cucumber/action-publish-mvn@v1.0.0
        with:
          gpg-private-key: ${{ secrets.GPG_PRIVATE_KEY }}
          gpg-passphrase: ${{ secrets.GPG_PASSPHRASE }}
          nexus-username: ${{ secrets.SONATYPE_USERNAME }}
          nexus-password: ${{ secrets.SONATYPE_PASSWORD }}
          working-directory: "java"
```
