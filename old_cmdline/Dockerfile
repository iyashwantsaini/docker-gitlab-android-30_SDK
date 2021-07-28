FROM openjdk:8-jdk
ENV ANDROID_COMPILE_SDK "30"
ENV ANDROID_BUILD_TOOLS "30.0.2"
ENV ANDROID_SDK_TOOLS   "6609375"
RUN apt-get --quiet update --yes
RUN apt-get --quiet install --yes wget tar unzip lib32stdc++6 lib32z1
RUN wget --quiet --output-document=android-sdk.zip https://dl.google.com/android/repository/commandlinetools-linux-${ANDROID_SDK_TOOLS}_latest.zip
RUN unzip -d android-sdk-linux android-sdk.zip
RUN echo y | android-sdk-linux/tools/bin/sdkmanager --sdk_root=android-sdk-linux "platforms;android-${ANDROID_COMPILE_SDK}" >/dev/null
RUN echo y | android-sdk-linux/tools/bin/sdkmanager --sdk_root=android-sdk-linux "platform-tools" >/dev/null
RUN echo y | android-sdk-linux/tools/bin/sdkmanager --sdk_root=android-sdk-linux "build-tools;${ANDROID_BUILD_TOOLS}" >/dev/null
ENV ANDROID_SDK_ROOT $PWD/android-sdk-linux
ENV PATH $PATH:$PWD/android-sdk-linux/platform-tools/
RUN yes | android-sdk-linux/tools/bin/sdkmanager --sdk_root=android-sdk-linux --licenses