# Zerops x GitHub Runner

A [GitHub Runner](https://docs.github.com/runner/) running on [Zerops](https://zerops.io), using the built-in zCLI binary for deployments directly from your CI/CD pipelines.

<br/>

## Deploy on Zerops

You can manually copy the [import yaml](https://github.com/zeropsio/recipe-zcli-github-runner/blob/main/zerops-project-import.yml) into the import dialog in the Zerops app.

[//]: # (You can either click the deploy button to import the recipe directly, or manually copy the [import yaml]&#40;https://github.com/zeropsio/recipe-zcli-github-runner/blob/main/zerops-project-import.yml&#41; into the import dialog in the Zerops app.)

[//]: # ([![Deploy on Zerops]&#40;https://github.com/zeropsio/recipe-shared-assets/blob/main/deploy-button/green/deploy-button.svg&#41;]&#40;https://app.zerops.io/recipe/zcli-github-runner&#41;)

<br/>

## Recipe features

- **Ubuntu 26.04** base with GitHub Runner installed via official binary
- **zCLI** available out of the box for Zerops deployments from your pipelines
- **Shell executor** for full control over the build environment
- Fixed container count — runners shouldn't scale horizontally automatically (adjust as needed)
- **Health check** by checking the runner process

<br/>

## Configuring

Set the following environment variables in the [import yaml](https://github.com/zeropsio/recipe-zcli-github-runner/blob/main/zerops-project-import.yml) before importing:

| Variable        | Description                                              |
|-----------------|----------------------------------------------------------|
| `GITLAB_URL`    | URL of your GitHub instance (e.g. `https://github.com/`) |
| `GITLAB_TOKEN`  | Runner authentication token from GitHub                  |
| `GITHUB_REPO`   | Repository for which the GitHub Runner is registered     |
| `RUNNER_LABELS` | Custom labels to identify the runner                     |

> If your GitHub instance uses an IP blocklist, create the project first, allow its IP address in your GitHub settings, then import the `zclirunner` service.

To adjust capacity for production workloads, increase `minContainers`/`maxContainers` and allocate more CPU/RAM to the service.

<br/>

## Changes made over a default GitHub Runner installation

- [x] Add [zerops.yml](https://github.com/zeropsio/recipe-zcli-github-runner/blob/main/zerops.yml) to the repository
- [x] Install runner dependencies (`git`, `zip`, `gcc`, `bzr`, `make`, `jq`) in [`prepareCommands`](https://github.com/zeropsio/recipe-zcli-github-runner/blob/main/zerops.yml#L6)
- [x] Download and install the GitHub Runner binary in [`prepareCommands`](https://github.com/zeropsio/recipe-zcli-github-runner/blob/main/zerops.yml#L8)
- [x] Register the runner automatically on startup via [`initCommands`](https://github.com/zeropsio/recipe-zcli-github-runner/blob/main/zerops.yml#L12)
- [x] Configure a [health check](https://github.com/zeropsio/recipe-zcli-github-runner/blob/main/zerops.yml#L31) by checking the runner process status

<br/>

Need help setting your project up? Join [Zerops Discord community](https://discord.com/invite/WDvCZ54).
