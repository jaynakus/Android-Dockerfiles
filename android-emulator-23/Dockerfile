FROM dyhpoon/android

MAINTAINER Darren "dyhpoon@gmail.com"

# Resources of Android SDK
RUN echo y | android update sdk -a --no-ui --filter sys-img-armeabi-v7a-android-23 --force

# Set up and run emulator
RUN echo no | android create avd --force -n test -c 30M -t android-23
# Avoid emulator assumes HOME as '/'.
ENV HOME /root
ADD wait-for-emulator /usr/local/bin/
ADD start-emulator /usr/local/bin/

VOLUME /root/.gradle
VOLUME /workspace
WORKDIR /workspace

####################
# Gradle
####################

RUN apt-get update
RUN apt-get install -y zip unzip

# Install Gradle
RUN cd /usr/local/ && wget http://services.gradle.org/distributions/gradle-2.10-all.zip && unzip -o gradle-2.10-all.zip

# Set environment variables
ENV GRADLE_USER_HOME /usr/local/gradle-2.10
ENV PATH $PATH:$GRADLE_USER_HOME/bin

# Clean up
RUN rm -rf /usr/local/gradle-2.10-all.zip
