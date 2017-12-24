FROM openshift/jenkins-slave-base-centos7

MAINTAINER Petter Abrahamsson <petter@redhat.com>

ENV PYTHON_VERSION=3.6.3 \
    SONAR_SCANNER_VERSION=3.0.3.778 \
    BASH_ENV=/usr/local/bin/scl_enable \
    ENV=/usr/local/bin/scl_enable \
    PROMPT_COMMAND=". /usr/local/bin/scl_enable"

COPY contrib/bin/scl_enable /usr/local/bin/scl_enable

USER 0
# install python
RUN yum install -y centos-release-scl-rh && \
    INSTALL_PKGS="rh-python36-python rh-python36-python-virtualenv" && \
    yum install -y --setopt=tsflags=nodocs $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y && \
    curl -Lo /tmp/sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip http://central.maven.org/maven2/org/sonarsource/scanner/cli/sonar-scanner-cli/${SONAR_SCANNER_VERSION}/sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip && \
    unzip -d /opt /tmp/sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip && \
    ln -s /opt/sonar-scanner-${SONAR_SCANNER_VERSION}-linux /opt/sonar-scanner && \
    rm -f /tmp/sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001
ENV PATH=$PATH:/opt/sonar-scanner/bin
