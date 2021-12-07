ARG NODEJS_VERSION

FROM node:${NODEJS_VERSION}

# Set Environment Variables
ENV DEBIAN_FRONTEND noninteractive

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

###########################################################################
# FINAL TOUCH:
###########################################################################
COPY ./locale.gen /etc/locale.gen

# Clean up
RUN locale-gen && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/log/lastlog /var/log/faillog

VOLUME /app

WORKDIR /app