FROM quay.io/openshift/origin-jenkins-agent-base:v4.0
# Labels consumed by Red Hat build service
LABEL com.redhat.component="rh-dotnet31-jenkins-slave-docker" \
      name="dotnet/dotnet-31-jenkins-slave-centos7" \
      version="3.1" \
      architecture="x86_64" \
      release="1" \
      io.k8s.display-name="Jenkins Slave .NET Core 3.1" \
      io.k8s.description="The jenkins slave dotnet image has the dotnet tools on top of the jenkins slave base image." \
      io.openshift.tags="openshift,jenkins,slave,dotnet,dotnet31"


ENV HOME=/opt/app-root \
    PATH=/opt/app-root/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    DOTNET_APP_PATH=/opt/app-root/app \
    DOTNET_DATA_PATH=/opt/app-root/data \
    DOTNET_DEFAULT_CMD=default-cmd.sh \
    DOTNET_CORE_VERSION=3.1 \
    DOTNET_FRAMEWORK=netcoreapp3.1 \
    DOTNET_RUNNING_IN_CONTAINER=true \
    DOTNET_SSL_CERT_DIR=/opt/app-root/ssl_dir

# Install
RUN yum install -y centos-release-dotnet centos-release-scl-rh && \
    INSTALL_PKGS="rh-nodejs10-npm rh-nodejs10-nodejs-nodemon rh-dotnet31-dotnet-sdk-3.1 rsync" && \
    yum install -y --setopt=tsflags=nodocs $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y && \
# yum cache files may still exist (and quite large in size)
    rm -rf /var/cache/yum/*

# RUN rm -rf /var/cache/yum/*

# Trigger first time actions.
# RUN scl enable rh-dotnet31 'dotnet help'

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001
