FROM docker.io/redhat/ubi9
# Terraform
RUN curl -L -o /etc/yum.repos.d/hashicorp.repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo 
# docker-cli
RUN curl -o /etc/yum.repos.d/docker.repo https://download.docker.com/linux/rhel/docker-ce.repo
# AZ
RUN dnf install https://packages.microsoft.com/config/rhel/9.0/packages-microsoft-prod.rpm -y
RUN dnf install libicu make terraform azure-cli docker-ce-cli -y 
# K8s
RUN curl -L "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" -o /bin/kubectl && chmod +x /bin/kubectl
# NodeJS
RUN dnf module disable nodejs -y && dnf module enable nodejs:22 -y && dnf install nodejs npm -y 
# Maven
RUN dnf install maven -y
# Go 
RUN curl -o go1.24.5.linux-amd64.tar.gz -L https://go.dev/dl/go1.24.5.linux-amd64.tar.gz &&  rm -rf /usr/local/go && tar -C /usr/local -xzf go1.24.5.linux-amd64.tar.gz && rm go1.24.5.linux-amd64.tar.gz
ENV PATH="/usr/local/go/bin:${PATH}"
# Helm
RUN curl -o helm-v3.0.0-linux-amd64.tar.gz -L https://get.helm.sh/helm-v3.0.0-linux-amd64.tar.gz && tar -xzf helm-v3.0.0-linux-amd64.tar.gz && mv linux-amd64/helm /usr/local/bin/helm && rm helm-v3.0.0-linux-amd64.tar.gz linux-amd64
#
RUN useradd github
USER github
WORKDIR /home/github
RUN curl -o actions-runner-linux-x64-2.326.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.326.0/actions-runner-linux-x64-2.326.0.tar.gz && tar xzf ./actions-runner-linux-x64-2.326.0.tar.gz
COPY run.sh /
ENTRYPOINT ["bash", "/run.sh"]