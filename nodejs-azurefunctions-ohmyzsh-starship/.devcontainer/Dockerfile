# Find the Dockerfile for mcr.microsoft.com/azure-functions/node at the following URLs:
# Node 10: https://github.com/Azure/azure-functions-docker/blob/dev/host/3.0/buster/amd64/node/node10/node10-core-tools.Dockerfile
# Node 12: https://github.com/Azure/azure-functions-docker/blob/dev/host/3.0/buster/amd64/node/node12/node12-core-tools.Dockerfile
# Node 14: https://github.com/Azure/azure-functions-docker/blob/dev/host/3.0/buster/amd64/node/node14/node14-core-tools.Dockerfile
ARG VARIANT=14
FROM mcr.microsoft.com/azure-functions/node:3.0-node${VARIANT}-core-tools

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
  && apt-get -y install --no-install-recommends zsh vim curl wget zip unzip

RUN su node -c "npm install -g npm"

RUN rm -rf /root/.oh-my-zsh \
  && sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended \
  && chsh -s /bin/zsh \
  && git clone --quiet https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions \
  && git clone --quiet https://github.com/zsh-users/zsh-completions ~/.oh-my-zsh/custom/plugins/zsh-completions \
  && sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="refined"/g' ~/.zshrc \
  && sed -i 's/# HYPHEN_INSENSITIVE=/HYPHEN_INSENSITIVE=/g' ~/.zshrc \
  && sed -i 's/plugins=(git)/plugins=(git zsh-completions zsh-autosuggestions)/g' ~/.zshrc \
  && sed -i '/plugins=(git zsh-completions zsh-autosuggestions)/a autoload -U compinit && compinit' ~/.zshrc

RUN sh -c "$(curl -fsSL https://starship.rs/install.sh)" -- --yes \
  && echo '\neval "$(starship init zsh)"\n' >> ~/.zshrc
