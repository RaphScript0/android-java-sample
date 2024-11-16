# Use a base image with Java pre-installed
FROM mcr.microsoft.com/vscode/devcontainers/java:17

# Install required dependencies for Android development
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    openjdk-17-jdk \
    wget \
    unzip \
    curl \
    git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set environment variables
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH
ENV ANDROID_HOME=/opt/android-sdk
ENV PATH=$PATH:$ANDROID_HOME/emulator:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools

# Download and set up Android SDK
RUN mkdir -p $ANDROID_HOME && \
    curl -o /tmp/sdk-tools.zip https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip && \
    unzip /tmp/sdk-tools.zip -d $ANDROID_HOME && \
    rm /tmp/sdk-tools.zip && \
    yes | $ANDROID_HOME/cmdline-tools/bin/sdkmanager --licenses

# Install Gradle
RUN wget https://services.gradle.org/distributions/gradle-7.5-bin.zip -P /tmp && \
    unzip /tmp/gradle-7.5-bin.zip -d /opt && \
    rm /tmp/gradle-7.5-bin.zip && \
    ln -s /opt/gradle-7.5/bin/gradle /usr/bin/gradle

# Set the default working directory
WORKDIR /workspace

# Set default user
USER vscode
