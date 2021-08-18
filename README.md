# devcontainers

Devcontainers I have customized for my use

## Quickest way to add to existing project

Inside your project root directory (example uses `javascript-nodejs` devcontainer):

1. `mkdir .devcontainer`
2. `cd .devcontainer`
3. `npx -y degit https://github.com/mikesprague/devcontainers.git/javascript-nodejs/.devcontainer`

Add the new folder to your repo and push the changes to GitHub. 

You can now start the customized devcontainer from your repo or VS Code.

## Devcontainer contents

Look at README files in each sub folder for more information and alternate install instructions

### Common to each of my devcontainers

The following are included in each devcontainer:

- Zsh installed and set as default shell
- [Oh My Zsh](https://ohmyz.sh/) installed
  - Autocomplete and Autosuggest plugins installed and enabled
- [Starship](https://starship.rs/) prompt installed and enabled
