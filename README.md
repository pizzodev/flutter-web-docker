# flutter-web-docker
Setup flutter build inside a Docker container.

# Content
```
# Pull git image
FROM bitnami/git:2.43.0

ARG FLUTTER_LOCAL_DIR=/usr/local/flutter
ARG FLUTTER_VERSION=3.13.9

# Install unzip dependency
RUN apt-get update
RUN apt-get install -y unzip

# Clone flutter
RUN git clone https://github.com/flutter/flutter.git $FLUTTER_LOCAL_DIR

# Change dir to current flutter folder and make a checkout to the specific version
RUN cd ${FLUTTER_LOCAL_DIR} && git fetch && git checkout $FLUTTER_VERSION

# Setup the flutter path as an enviromental variable
ENV PATH="${FLUTTER_LOCAL_DIR}bin:${FLUTTER_LOCAL_DIR}bin/cache/dart-sdk/bin:${PATH}"

# Doctor to see if all was installed ok
RUN flutter doctor -v
```

# About the Dockerfile
Some versions are hardcoded, please setup according to the needs.