# Buildkite Packages Publish Using OIDC Example

This repository is an example [Buildkite](https://buildkite.com/) pipeline for publishing packages using short term OIDC tokens for authentication. It builds a Debian package and publishes it to [this Buildkite Packages Registry](https://buildkite.com/organizations/buildkite/packages/registries/oidc-example).

👉 **See this example in action:** [buildkite/packages-publish-oidc-example](https://buildkite.com/buildkite/packages-publish-oidc-example/builds/latest)

See the full [Getting Started Guide](https://buildkite.com/docs/guides/getting-started) for step-by-step instructions on how to get this running, or try it yourself:

<!-- docs:start -->
## How it works

This example:

- Removes existing packages from the registry to avoid naming conflicts.
- Builds a simple Debian package called "Hello Buildkite".
- Pushes the package using the [publish-to-packages plugin](https://buildkite.com/resources/plugins/buildkite-plugins/publish-to-packages-buildkite-plugin/). This plugin uses OIDC tokens for authentication.
<!-- docs:end -->

## License

See [LICENSE.md](LICENSE.md) (MIT)
