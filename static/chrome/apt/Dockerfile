FROM base_image:latest

ARG VERSION
ARG PACKAGE=google-chrome-stable
ARG INSTALL_DIR=chrome

LABEL browser=$PACKAGE:$VERSION

RUN \
        curl -s https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
        if [ `uname -m` = "aarch64" ] ; then \
                   echo 'deb [arch=arm64] https://dl.google.com/linux/chrome/deb/ stable main' > /etc/apt/sources.list.d/google.list && \
                   apt-get update && \
                   apt-get -y --no-install-recommends install iproute2 && \
                   apt-get install chromium-browser $$ \
                   chromium-browser --version; \
                else \
                   echo 'deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main' > /etc/apt/sources.list.d/google.list && \
                   apt-get update && \
                   apt-get -y --no-install-recommends install iproute2 $PACKAGE=$VERSION && \
                   chown root:root /opt/google/$INSTALL_DIR/chrome-sandbox && \
                   chmod 4755 /opt/google/$INSTALL_DIR/chrome-sandbox && \
                   google-chrome --version; \
                fi && \
        rm -Rf /tmp/* && rm -Rf /var/lib/apt/lists/*
