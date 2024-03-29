# android build environment

FROM ubuntu:18.04
USER root
# Never ask for confirmations
ENV DEBIAN_FRONTEND noninteractive
ENV ANDROID_NDK_HOME /opt/android-ndk
ENV ANDROID_NDK_VERSION r21b

# Update apt-get & Install packages
RUN apt update && \
    apt install -y openjdk-8-jdk  bash wget unzip make file && \
	apt clean

# ------------------------------------------------------
# --- Android NDK

# download
RUN mkdir /opt/android-ndk-tmp && \
    cd /opt/android-ndk-tmp && \
    wget -q https://dl.google.com/android/repository/android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip && \
# uncompress
    unzip -q android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip && \
# move to its final location
    mv ./android-ndk-${ANDROID_NDK_VERSION} ${ANDROID_NDK_HOME} && \
# remove temp dir
    cd ${ANDROID_NDK_HOME} && \
    rm -rf /opt/android-ndk-tmp



# Export JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV PATH $PATH:$JAVA_HOME/bin

# Install Android SDK
RUN wget -q --no-check-certificate https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip && \
    unzip -q sdk-tools-linux-3859397.zip -d /usr/local/android-sdk && \
    rm sdk-tools-linux-3859397.zip && \ 
    mkdir /root/.android && touch /root/.android/repositories.cfg

# Export ANDROID_HOME variable
ENV ANDROID_HOME /usr/local/android-sdk
ENV PATH $PATH:$ANDROID_HOME/tools
ENV PATH $PATH:$ANDROID_HOME/tools/bin
ENV PATH $PATH:$ANDROID_HOME/platform-tools
ENV PATH $PATH:$ANDROID_HOME/build-tools/29.0.3

RUN echo yes | sdkmanager  \
    "platforms;android-29"  \
    "build-tools;29.0.3"  \
    "extras;android;m2repository" \
    "extras;google;m2repository" \
    "platform-tools" \
    "extras;google;google_play_services"

RUN echo "sdk.dir=$ANDROID_HOME" > local.properties
