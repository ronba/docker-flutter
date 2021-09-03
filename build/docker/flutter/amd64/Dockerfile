FROM ubuntu:latest

LABEL maintainer="ronba"

ARG DART_VERSION=latest
ARG FLUTTER_VERSION=stable

RUN apt-get update 
RUN apt-get install -y --no-install-recommends bash ca-certificates curl git xz-utils wget unzip zip protobuf-compiler  
RUN curl https://storage.googleapis.com/dart-archive/channels/stable/release/latest/sdk/dartsdk-linux-x64-release.zip -o /tmp/dart-sdk.zip 
RUN unzip /tmp/dart-sdk.zip -d /usr/lib && rm /tmp/dart-sdk.zip

ENV PATH=/usr/lib/dart-sdk/bin:$PATH
ENV PATH=/root/.pub-cache/bin:$PATH
ENV PATH=/root/fvm/default/bin:/home/$user/fvm/default/bin:$PATH

# Setup flutter
RUN dart pub global activate fvm --verbose && fvm config
RUN fvm doctor --verbose
RUN fvm install $FLUTTER_VERSION --verbose 
RUN fvm global $FLUTTER_VERSION
RUN fvm flutter config --enable-web --enable-android --verbose

# # Protocol Buffer setup.
RUN flutter pub global activate protoc_plugin 20.0.0

# Add symlinks to flutter/dart (otherwise they get removed in the github action)
RUN ln -s $(which flutter) /usr/local/bin/flutter
RUN ln -s $(which dart) /usr/local/bin/dart

