# Find the Dockerfile for mcr.microsoft.com/azure-functions/node at the following URLs:
# Node 10: https://github.com/Azure/azure-functions-docker/blob/dev/host/3.0/buster/amd64/node/node10/node10-core-tools.Dockerfile
# Node 12: https://github.com/Azure/azure-functions-docker/blob/dev/host/3.0/buster/amd64/node/node12/node12-core-tools.Dockerfile
# Node 14: https://github.com/Azure/azure-functions-docker/blob/dev/host/3.0/buster/amd64/node/node14/node14-core-tools.Dockerfile
ARG VARIANT=16
FROM mcr.microsoft.com/azure-functions/node:4.0-node${VARIANT}-core-tools

# install some common utils
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
  && apt-get -y install --no-install-recommends zsh git vim curl wget zip unzip

# install github cli
RUN export DEBIAN_FRONTEND=noninteractive \
  && curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo gpg --dearmor -o /usr/share/keyrings/githubcli-archive-keyring.gpg \
  && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
  && sudo apt-get update \
  && sudo apt-get -y install gh

# install some global npm dependencies
RUN npm install -g npm n gitmoji-cli npm-check-updates

# use n (node version manager) to make sure we're on latest v16 of nodejs
RUN n 16 && npm i -g npm

# install and customize oh-my-zsh
RUN rm -rf /root/.oh-my-zsh \
  && sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended \
  && chsh -s /bin/zsh \
  && git clone --quiet https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions \
  && git clone --quiet https://github.com/zsh-users/zsh-completions ~/.oh-my-zsh/custom/plugins/zsh-completions \
  && git clone --quiet https://github.com/sobolevn/wakatime-zsh-plugin.git ~/.oh-my-zsh/custom/plugins/wakatime \
  && sed -i 's/ZSH_THEME="robbyrussell"/# ZSH_THEME="robbyrussell"/g' ~/.zshrc \
  && sed -i 's/# HYPHEN_INSENSITIVE=/HYPHEN_INSENSITIVE=/g' ~/.zshrc \
  && sed -i 's/plugins=(git)/plugins=(git zsh-completions zsh-autosuggestions npm)/g' ~/.zshrc \
  && sed -i '/plugins=(git zsh-completions zsh-autosuggestions npm)/a autoload -U compinit && compinit' ~/.zshrc

# set some shell aliases and options and set some git aliases and options
RUN echo '\nalias la="ls -lah"\nalias cl="clear"\nalias npmgls="npm -g ls --depth=0"\n' >> ~/.zshrc \
  && echo '\nalias aptupdate="sudo apt update && sudo apt upgrade"\n' >> ~/.zshrc \
  && echo '\nalias alias ncud="ncu --dep dev -u && npm install"\nalias ncup="ncu --dep prod -u && npm install"\n' >> ~/.zshrc \
  && echo '\n\nexport LS_COLORS="su=00:sg=00:ca=00:ow=01;36;40"\n' >> ~/.zshrc \
  && echo '\nzstyle ":completion:*" list-colors "${(@s.:.)LS_COLORS}"\n' >> ~/.zshrc \
  && echo '\neval "$(gh completion --shell zsh)"\n' >> ~/.zshrc \
  && git config  --global --add alias.st status \
  && git config --global --add alias.lsd 'log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate' \
  && git config --global --add commit.gpgsign true \
  && git config --global --add tag.gpgsign true \
  && git config --global --add tag.tag.forcesignannotated true

# install starship shell promopt
RUN sh -c "$(curl -fsSL https://starship.rs/install.sh)" -- --yes \
  && echo '\neval "$(starship init zsh)"\n' >> ~/.zshrc

# add config file for starship prompt
COPY starship.toml  /root/.config/starship.toml
