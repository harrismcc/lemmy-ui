# [Choice] Node.js version (use -bullseye variants on local arm64/Apple Silicon): 18, 16, 14, 18-bullseye, 16-bullseye, 14-bullseye, 18-buster, 16-buster, 14-buster
ARG VARIANT=16-bullseye
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:0-${VARIANT}

USER root

# Set zsh as the main shell
RUN chsh -s /usr/bin/zsh

# Install binaries
RUN apt-get update && apt-get -y install --no-install-recommends \
    curl \
    yarn \
    python3 \
    gcc \
    wget \
    git
RUN curl -sf https://gobinaries.com/tj/node-prune | sh

# Preserve Shell history
RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.zsh_history" \
    && echo $SNIPPET >> "/root/.zshrc"

# Ensure the root folder referenced here is accessible to the user that will run the container
RUN sudo chown root -R /root

# WORKDIR /usr/src/app

# ENV npm_config_target_arch=x64
# ENV npm_config_target_platform=linux
# ENV npm_config_target_libc=musl

# # Cache deps
# COPY package.json yarn.lock ./
# RUN yarn --production --prefer-offline --pure-lockfile

# # Build
# COPY generate_translations.js \
#   tsconfig.json \
#   webpack.config.js \
#   .babelrc \
#   ./

# COPY lemmy-translations lemmy-translations
# COPY src src
# COPY .git .git

# # Set UI version 
# RUN echo "export const VERSION = '$(git describe --tag)';" > "src/shared/version.ts"

# RUN yarn --production --prefer-offline
# RUN NODE_OPTIONS="--max-old-space-size=8192" yarn build:prod

# # Prune the image
# RUN node-prune /usr/src/app/node_modules

# RUN rm -rf ./node_modules/import-sort-parser-typescript
# RUN rm -rf ./node_modules/typescript
# RUN rm -rf ./node_modules/npm

# RUN du -sh ./node_modules/* | sort -nr | grep '\dM.*'

# FROM node:alpine as runner
# COPY --from=builder /usr/src/app/dist /app/dist
# COPY --from=builder /usr/src/app/node_modules /app/node_modules

# EXPOSE 1234
# WORKDIR /app
# CMD node dist/js/server.js
