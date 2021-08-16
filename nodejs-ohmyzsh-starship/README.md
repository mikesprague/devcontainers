# nodejs-ohmyzsh-starship

## Basic Usage

- Copy `.devcontainer/` folder to the root of the project you want to add it to
- Local:
  - Reload VS Code and answser yes when prompted use the dev container
- Remote (GH Codespaces):
  - Open your project in GH Codespaces and it will create the environment based on this dev container

## Contents

- Node.js
- [Yarn](https://yarnpkg.com/) package manager
- Zsh (set as default shell)
- [Oh My Zsh](https://ohmyz.sh/) installed with autocomplete and autosuggest plugins installed/enabled
- [Starship](https://starship.rs/) prompt installed and enabled
- [n](https://github.com/tj/n) Node.js version manager installed (defaults to Node.js v16 with v14 also installed)

### VS Code Extensions installed on first use

- See the extensions section in [devcontainer.json](./.devcontainer/devcontainer.json)
- NOTE: WIP - lots of extensions can be removed/commented out

