FROM node:14-buster

RUN apt-get update && apt-get install gettext-base

RUN npm_config_user=root npm install --no-progress --global \
    @angular/cli \
    @e11community/token-exporter \
    firebase-tools \
    rollbar-cli && \
    yarn global add typescript

RUN mkdir -p /opt && cd /opt && \
    curl -so gcp-sdk.tgz 'https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-343.0.0-linux-x86_64.tar.gz' && \
    tar xfz gcp-sdk.tgz && \
    cd google-cloud-sdk && \
    ./install.sh -q --path-update true && \
    cd - && rm gcp-sdk.tgz

ADD firebase.bash /usr/bin

RUN chmod +x /usr/bin/firebase.bash && \
    ln -s /opt/google-cloud-sdk/bin/gcloud /usr/local/bin && \
    echo -n 'node version: '     && node --version && \
    echo -n 'npm version: '      && npm --version && \
    echo -n 'firebase version: ' && firebase --version

ENTRYPOINT [ "/usr/bin/firebase.bash" ]

