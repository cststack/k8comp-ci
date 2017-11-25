FROM jenkins/ssh-slave
ENV KUBE_VERSION v1.8.4
ENV OC_VERSION v3.6.1
ENV OC_TAG 008f2d5
ENV K8COMP_VERSION master
RUN apt-get update && \
    apt-get install rubygems ed jq -y && \
    gem install hiera hiera-eyaml && \
    wget -O kubectl https://storage.googleapis.com/kubernetes-release/release/${KUBE_VERSION}/bin/linux/amd64/kubectl && \
    mv ./kubectl /bin/kubectl && \
    curl -L  https://github.com/openshift/origin/releases/download/${OC_VERSION}/openshift-origin-client-tools-${OC_VERSION}-${OC_TAG}-linux-64bit.tar.gz | tar -xz && \
    mv openshift-origin-client-tools-${OC_VERSION}-${OC_TAG}-linux-64bit/oc /bin/oc && \
    curl -L https://raw.githubusercontent.com/cststack/k8comp/${K8COMP_VERSION}/bin/k8comp > /bin/k8comp && \
    chmod +x /bin/* && \
    rm -rf /var/cache/* && \
    echo "jenkins:jenkins" | chpasswd && \
    echo "root:jenkins" | chpasswd && \
    sed -i 's/PermitRootLogin.*/#PermitRootLogin/' /etc/ssh/sshd_config && \
    sed -i 's/PasswordAuthentication.*/#PasswordAuthentication/' /etc/ssh/sshd_config
