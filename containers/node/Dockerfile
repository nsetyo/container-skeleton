ARG NODEJS_VERSION

FROM node:${NODEJS_VERSION}

# Set Environment Variables
ENV DEBIAN_FRONTEND noninteractive

RUN if [ -n "${http_proxy}" ]; then \
    apt update -y && apt install netcat \
    ;fi

# always run apt update when start and after add new source list, then clean up at end.
RUN apt update -y \
    && apt upgrade -y \
    && apt install -y --no-install-recommends \
    apt-transport-https \
    apt-utils \
    ca-certificates \
    curl \
    git \
    locales \
    unzip

RUN npm install -g npm

################################################################################
# ENABLE COREPACK:
################################################################################

ARG ENABLE_COREPACK=false

RUN if [ ${ENABLE_COREPACK} = true ]; then \
    corepack enable \
    && pnpm add -g pnpm \
    && pnpm config set store-dir /root/.pnpm-store \
    ;fi

################################################################################
# INSTALL BASH COMPLETION:
################################################################################

ARG INSTALL_BASH_COMPLETION=false

RUN if [ ${INSTALL_BASH_COMPLETION} = true ]; then \
    apt-get install -y --no-install-recommends bash-completion \
    ;fi

################################################################################
# INSTALL STARSHIPRS
################################################################################

ARG INSTALL_STARSHIPRS=false

RUN if [ ${INSTALL_STARSHIPRS} = true ]; then \
    curl -sS https://starship.rs/install.sh | sh -s -- --yes \
    ;fi

################################################################################
# FINAL TOUCH:
################################################################################
COPY ./locale.gen /etc/locale.gen

# Clean up
RUN locale-gen && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/log/lastlog /var/log/faillog

VOLUME /app

WORKDIR /app