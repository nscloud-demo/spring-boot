FROM docker.io/buildkite/hosted-agent-base:ubuntu-v1.0.1@sha256:f1378abd34fccb2b7b661aaf3b06394509a4f7b5bb8c2f8ad431e7eaa1cabc9c

ARG DEBIAN_FRONTEND=noninteractive
ENV CI=1
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en

# Set environment variables
ENV JAVA_VERSION=17
ENV GRADLE_VERSION=8.11.1
ENV GRADLE_HOME=/opt/gradle
ENV JAVA_HOME=/usr/lib/jvm/java-${JAVA_VERSION}-openjdk-amd64
ENV PATH=${GRADLE_HOME}/bin:${JAVA_HOME}/bin:${PATH}

# Install OpenJDK and necessary tools
RUN apt-get update && \
    apt-get install -y \
    openjdk-${JAVA_VERSION}-jdk \
    curl \
    unzip \
    && rm -rf /var/lib/apt/lists/*

# Download and install Gradle
RUN curl -L https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -o gradle.zip && \
    mkdir -p ${GRADLE_HOME} && \
    unzip gradle.zip && \
    mv gradle-${GRADLE_VERSION}/* ${GRADLE_HOME}/ && \
    rm gradle.zip

# Verify installation
RUN java -version && \
    gradle -version