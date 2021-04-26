# FluxCD

## Prerequisites

Flux is installed in a GitOps way and its manifest will be pushed to the repository. Export your GitHub personal access token and username:
```
export GITHUB_TOKEN=<your-token>
export GITHUB_USER=<your-username>
```


## Installation

Install the fluxcd cli tool. MacOS users could install with homebrew:
```
Install the Flux CLI
```
Or install flux by downloading precompiled binaries using a Bash script:
```
curl -s https://toolkit.fluxcd.io/install.sh | sudo bash
```