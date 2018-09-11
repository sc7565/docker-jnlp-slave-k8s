FROM jenkinsci/jnlp-slave:3.23-1

USER root

WORKDIR /opt

# Add docker client
# The version number is the docker version you want to move to
ENV DOCKER_VERION 17.09.0-ce
RUN curl -fsSL get.docker.com -o get-docker.sh
RUN sh get-docker.sh
RUN usermod -aG docker jenkins
RUN usermod -aG docker root

# Add kubectl client
#    ENV KUBECTL_VERSION 1.11.1
#RUN wget https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl
#RUN chmod +x kubectl
#RUN mv kubectl /usr/bin/

#RUN apt-get update

# Change /home/jenkins ownership to root
RUN chown -R root:root /home/jenkins
RUN chmod -R 777 /home/jenkins
RUN mkdir -p /usr/lib/node_modules
RUN chmod -R 777 /usr/lib/node_modules

# Add python virtualenv and libs
#RUN apt-get install -y python-pip python-dev libxml2-dev libxslt1-dev zlib1g-dev
#RUN pip install virtualenv

# node.js
# versions: https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs
RUN apt-get install -y npm xvfb libgtk2.0-0 libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2
RUN npm install -g jasmine-node
RUN CYPRESS_CACHE_FOLDER=. npm install cypress

# install junit
#RUN apt-get install -y junit

# install bc - math expressions
#RUN apt-get install -y bc

# install apt-utils
#RUN apt-get install -y apt-utils

# Installing envsubst for file variable substitution
#RUN apt-get install -y gettext-base

# Installing zip
#RUN apt-get install -y zip

# Versions: https://pypi.python.org/pypi/awscli#downloads
#ENV AWS_CLI_VERSION 1.11.185
#RUN apt-get install -y python-pip python-dev build-essential
#RUN pip --no-cache-dir install awscli==${AWS_CLI_VERSION}

# Installing helm
# versions: https://github.com/kubernetes/helm#install
#ENV HELM_VERSION 2.9.1
#RUN wget https://kubernetes-helm.storage.googleapis.com/helm-v${HELM_VERSION}-linux-amd64.tar.gz
#RUN tar -zxvf helm-v${HELM_VERSION}-linux-amd64.tar.gz
#RUN cp linux-amd64/helm /usr/bin/
#RUN rm -rf /opt/helm*

#==========
# Maven
#==========
ENV MAVEN_VERSION 3.2.3

RUN curl -fsSL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar xzf - -C /usr/share \
  && mv /usr/share/apache-maven-$MAVEN_VERSION /usr/share/maven \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME /usr/share/maven

#==========
# Gradle
#==========
#ENV GRADLE_VERSION 2.2.1

#RUN wget https://services.gradle.org/distributions/gradle-$GRADLE_VERSION-bin.zip \
#    && unzip -d /usr/share gradle-$GRADLE_VERSION-bin.zip \
#    && mv /usr/share/gradle-$GRADLE_VERSION /usr/share/gradle \
#    && ln -s /usr/share/gradle/bin/gradle /usr/bin/gradle

#ENV GRADLE_HOME /usr/share/gradle

#==========
# Gcloud
#==========
#ENV CLOUD_SDK_VERSION 209.0.0
#
#RUN apt-get -qqy update && apt-get install -qqy \
#        curl \
#        gcc \
#        python-dev \
#        python-setuptools \
#        apt-transport-https \
#        lsb-release \
#        openssh-client \
#        git \
#    && easy_install -U pip && \
#    pip install -U crcmod   && \
#    export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
#    echo "deb https://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" > /etc/apt/sources.list.d/google-cloud-sdk.list && \
#    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
#    apt-get update && \
#    apt-get install -y google-cloud-sdk=${CLOUD_SDK_VERSION}-0 \
#        google-cloud-sdk-app-engine-python=${CLOUD_SDK_VERSION}-0 \
#        google-cloud-sdk-app-engine-python-extras=${CLOUD_SDK_VERSION}-0 \
#        google-cloud-sdk-app-engine-java=${CLOUD_SDK_VERSION}-0 \
#        google-cloud-sdk-app-engine-go=${CLOUD_SDK_VERSION}-0 \
#        google-cloud-sdk-datalab=${CLOUD_SDK_VERSION}-0 \
#        google-cloud-sdk-datastore-emulator=${CLOUD_SDK_VERSION}-0 \
#        google-cloud-sdk-pubsub-emulator=${CLOUD_SDK_VERSION}-0 \
#        google-cloud-sdk-bigtable-emulator=${CLOUD_SDK_VERSION}-0 \
#        google-cloud-sdk-cbt=${CLOUD_SDK_VERSION}-0 \
#        kubectl && \
#    gcloud config set core/disable_usage_reporting true && \
#    gcloud config set component_manager/disable_update_check true && \
#    gcloud config set metrics/environment github_docker_image && \
#    gcloud --version && \
#    mvn --version && \
#    gradle --version && \
#    java -version && \
#    kubectl version --client && \
#    npm --version

ENTRYPOINT ["jenkins-slave"]
