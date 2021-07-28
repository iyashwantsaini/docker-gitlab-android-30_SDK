FROM gradle:6.8-jdk8

WORKDIR /opt/android-sdk-linux

ENV ANDROID_COMPILE_SDK "30"
ENV ANDROID_BUILD_TOOLS "30.0.2"
ENV ANDROID_SDK_TOOLS   "6609375"

ENV ANDROID_HOME      /opt/android-sdk-linux
ENV ANDROID_SDK_HOME  ${ANDROID_HOME}
ENV ANDROID_SDK_ROOT  ${ANDROID_HOME}
ENV ANDROID_SDK       ${ANDROID_HOME}
ENV PATH "${PATH}:${ANDROID_HOME}/tools/latest/bin"
ENV PATH "${PATH}:${ANDROID_HOME}/tools/tools/bin"
ENV PATH "${PATH}:${ANDROID_HOME}/tools/bin"
ENV PATH "${PATH}:${ANDROID_HOME}/build-tools/30.0.2"
ENV PATH "${PATH}:${ANDROID_HOME}/platform-tools"
ENV PATH "${PATH}:${ANDROID_HOME}/emulator"
ENV PATH "${PATH}:${ANDROID_HOME}/bin"

RUN apt-get --quiet update --yes
RUN apt-get --quiet install --yes wget tar unzip lib32stdc++6 lib32z1


## Downloading SDK and tools from google using sdk-manager -
# RUN wget --quiet --output-document=android-sdk.zip https://dl.google.com/android/repository/commandlinetools-linux-${ANDROID_SDK_TOOLS}_latest.zip
# RUN echo y | android-sdk-linux/tools/bin/sdkmanager --sdk_root=android-sdk-linux "platforms;android-${ANDROID_COMPILE_SDK}" >/dev/null
# RUN echo y | android-sdk-linux/tools/bin/sdkmanager --sdk_root=android-sdk-linux "platform-tools" >/dev/null
# RUN echo y | android-sdk-linux/tools/bin/sdkmanager --sdk_root=android-sdk-linux "build-tools;${ANDROID_BUILD_TOOLS}" >/dev/null
# RUN yes | android-sdk-linux/tools/bin/sdkmanager --sdk_root=android-sdk-linux --licenses >/dev/null


## Downloading from nexus repos and structuring

RUN wget --quiet --output-document=android-cmdline.zip https://dl.google.com/android/repository/commandlinetools-linux-${ANDROID_SDK_TOOLS}_latest.zip
RUN unzip -d . android-cmdline.zip
RUN mkdir -p ./cmdline-tools/2.1
RUN mv ./tools ./cmdline-tools/2.1

RUN wget --quiet --output-document=android-platform-tools.zip https://dl.google.com/android/repository/platform-tools_r${ANDROID_BUILD_TOOLS}-linux.zip
RUN unzip -d . android-platform-tools.zip

RUN wget --quiet --output-document=android-platform.zip https://dl.google.com/android/repository/platform-30_r03.zip
RUN unzip -d ./platforms android-platform.zip
RUN mv ./platforms/android-11 ./platforms/android-30

RUN wget --quiet --output-document=android-build-tools.zip https://dl.google.com/android/repository/build-tools_r${ANDROID_BUILD_TOOLS}-linux.zip
RUN unzip -d ./build-tools android-build-tools.zip
RUN mv ./build-tools/android-11 ./build-tools/${ANDROID_BUILD_TOOLS}

# RUN wget --quiet --output-document=android-licenses.zip https://gitlab.com/yash2127/data-android/-/raw/master/licenses.zip

COPY android-licenses.zip ./
RUN unzip -d . android-licenses.zip

## Cleaning up downloaded zips

RUN rm ./android-cmdline.zip
RUN rm ./android-platform-tools.zip
RUN rm ./android-platform.zip
RUN rm ./android-build-tools.zip
RUN rm ./android-licenses.zip


## Adding a temp app for testing

# COPY ./android-build ${PWD}/android-build
# COPY certs/cacerts ${PWD}/etc/ssl/certs/java/
# COPY certs/ca-bundle.crt ${PWD}/etc/ssl/certs/
# COPY certs/ca-bundle.crt ${PWD}/etc/ssl/certs/ca-certificates.crt


## The Current directory structure of SDK in container
# - opt/
#    - android-sdk-linux/
#       - build-tools/30.0.2/ 
#       - cmdline-tools/2.1/ or tools/
#       - licenses/
#       - platform-tools/
#       - platforms/android-30/


## Official links for zips
# https://dl.google.com/android/repository/platform-tools_r30.0.2-linux.zip
# https://dl.google.com/android/repository/platform-S_r04.zip # may vary wrt app
# https://dl.google.com/android/repository/platform-30_r03.zip # may vary wrt app
# https://dl.google.com/android/repository/build-tools_r30.0.2-linux.zip
# put licences from docker container or from local SDK folder
# https://androidsdkmanager.azurewebsites.net/