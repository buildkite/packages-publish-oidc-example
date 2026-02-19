# Buildkite example template

A template for creating example repositories for [Buildkite](https://buildkite.com).

## How to create an example repository

### 1. Create a repository

[Use this template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) to create a new repository. The name should be in the format `<name>-example`.

Add a description, and tag it with the `example` topic.

Add the "Engineering" team as a collaborator with admin role.

#### Write the pipeline config

Add [pipeline config](https://buildkite.com/docs/pipelines/configure) for the example to `.buildkite/pipeline.yml`.

#### Add template config

Fill out `.buildkite/template.yml`, so the example can be used to create a pipeline with the "Add to Buildkite" button.


<details>
<p><summary><code>template.yml</code> structure</summary></p>

```yml
name: "<title> Example"
description: "An example pipeline that <short description of what this pipeline does>."
emoji: ":buildkite:"
color: "<hex>"
languages:
  - "<language>"
steps:
  - command: "buildkite-agent pipeline upload"
    label: ":pipeline:"
```

</details>

### 2. Create a public pipeline

Create a new pipeline for the example repository with the following settings:

<table>
<tr>
<td>Git repository</td>
<td>The example repository</td>
</tr>

<tr>
<td>Checkout using</td>
<td>HTTPS</td>
</tr>

<tr>
<td>Auto-create webhooks</td>
<td>✔</td>
</tr>

<tr>
<td>Name</td>
<td><code>&lt;name&gt;-example</code></td>
</tr>

<tr>
<td>Description</td>
<td>Copy from repository description</td>
</tr>

<tr>
<td>Cluster</td>
<td>Examples</td>
</tr>

<tr>
<td>Steps</td>
<td>

```yaml
steps:
  - label: ":pipeline:"
    command: "buildkite-agent pipeline upload"
```

</td>
</tr>

<tr>
<td>Teams</td>
<td>Examples</td>
</tr>
</table>

#### General settings

After creating, update its general settings:

<table>
<tr>
<td>Tags</td>
<td><code>example</code></td>
</tr>

<tr>
<td>Pipeline emoji</td>
<td>Copy from <code>.buildkite/template.yml</code></td>
</tr>

<tr>
<td>Pipeline management</td>
<td>✔ Make pipeline public</td>
</tr>
</table>

#### Schedules

Add a new schedule with the following settings:

<table>
<tr>
<td>Description</td>
<td>Weekly build on main</td>
</tr>

<tr>
<td>Cron interval</td>
<td><code>@weekly</code></td>
</tr>

<tr>
<td>Build message</td>
<td>Scheduled build</td>
</tr>

<tr>
<td>Build commit</td>
<td><code>HEAD</code></td>
</tr>

<tr>
<td>Build branch</td>
<td><code>main</code></td>
</tr>

<tr>
<td>Enabled</td>
<td>✔</td>
</tr>
</table>

#### Agent image (optional)

<details>
<p><summary>If you need to install additional tools on the agent, create an <a href="https://buildkite.com/docs/pipelines/hosted-agents/linux#agent-images">Agent image</a>.</summary></p>

The name of the image should be the same as your example (`<name>-example`).

Once you've created the image, create a new Queue in the _Examples_ cluster with the following settings:

<table>
<tr>
<td>Key</td>
<td><code>&lt;name&gt;-example</code></td>
</tr>

<tr>
<td>Agent infrastructure</td>
<td>Hosted</td>
</tr>

<tr>
<td>Machine type</td>
<td>Linux</td>
</tr>

<tr>
<td>Architecture</td>
<td>AMD64</td>
</tr>

<tr>
<td>Capacity</td>
<td>Small</td>
</tr>
</table>

Configure the Base image for the Queue to use the Agent image you created.

Update the Pipeline steps to use the Queue:

```yaml
steps:
  - label: ":pipeline:"
    command: "buildkite-agent pipeline upload"

agents:
  queue: "<name>-example"
```

</details>

### 3. Fill out the README

Fill out the template below, removing any sections that aren't needed, and then delete these instructions.

You can use uses `<!-- docs:start -->`/`<!-- docs:end -->` comments to denote sections of the README that will be included as documentation when the example is displayed on the Buildkite website and app.

Update the website field in repository details with the public pipeline URL.

#### Add a screenshot

Create a build on the public pipeline, then capture a screenshot of the build canvas.

Use the `capture-screenshot` script from [example-utils](https://github.com/buildkite/example-utils) to ensure the screenshot is consistent with other examples:

```sh
docker-compose run --rm utils bin/capture-screenshot https://buildkite.com/buildkite/my-example/builds/1/canvas
```

Add the screenshot to `.buildkite/screenshot.png`.

## Checklist

- [ ] Pipeline config (`pipeline.yml`)
- [ ] Template config (`template.yml`)
- [ ] Public pipeline
  - [ ] is public
  - [ ] is in Examples team
  - [ ] is in Examples cluster
  - [ ] has `example` tag
  - [ ] has weekly build schedule
- [ ] **Repository**
  - [ ] is public
  - [ ] name matches `<name>-example`
  - [ ] has `example` topic
  - [ ] has website with public pipeline URL
- [ ] **README**
  - [ ] includes a screenshot
  - [ ] has "Add to Buildkite" button
  - [ ] has build badge
  - [ ] uses `<!-- docs:start -->`/`<!-- docs:end -->` comments to denote documentation

<!-- TODO: delete this line and everything above -->

# Buildkite \<title\> Example

[![Build status](https://badge.buildkite.com/FIXME.svg?branch=main)](https://buildkite.com/buildkite/FIXME)
[![Add to Buildkite](https://img.shields.io/badge/Add%20to%20Buildkite-14CC80)](https://buildkite.com/new)

This repository is an example [Buildkite](https://buildkite.com/) pipeline for \<describe what this pipeline does\>.

👉 **See this example in action:** [buildkite/FIXME](https://buildkite.com/buildkite/FIXME/builds/latest)

See the full [Getting Started Guide](https://buildkite.com/docs/guides/getting-started) for step-by-step instructions on how to get this running, or try it yourself:

[![Add to Buildkite](https://buildkite.com/button.svg)](https://buildkite.com/new)

<a href="https://buildkite.com/buildkite/FIXME/builds/latest?branch=main">
  <img width="2400" alt="Screenshot of example pipeline build page" src=".buildkite/screenshot.png" />
</a>

<!-- docs:start -->
## How it works

Explain how the example pipeline works, e.g. what the steps do, how artifacts and logs are handled, etc.

<!-- TODO: remove this section if not needed -->
## Setup

Describe any prerequisites or setup instructions (e.g. agent hooks) required to run the example.

Keep it brief — the focus is on demonstrating the live pipeline, not walking users through a full project setup.
<!-- docs:end -->

## License

See [LICENSE](LICENSE) (MIT)
