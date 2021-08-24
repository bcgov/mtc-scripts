FROM registry.access.redhat.com/ubi8/ubi:latest

ENV TINI_VERSION=v0.19.0
ENV KUBESEAL_VERSION=v0.16.0
ENV KUSTOMIZE_VERSION=v4.2.0

ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
ADD bin/entrypoint.sh /bin/entrypoint

RUN dnf install -y git hostname jq python3 python3-pip python3-pyyaml && \
  pip3 install --upgrade pip && \
  pip install ansible openshift kubernetes jq pyyaml pyjwt jmespath && \
  chmod +x /bin/tini /bin/entrypoint && \
  rm -rf /var/cache/dnf

RUN curl -LOJ https://github.com/bitnami-labs/sealed-secrets/releases/download/${KUBESEAL_VERSION}/kubeseal-linux-amd64 && \
  mv kubeseal-linux-amd64 /bin/kubeseal && \
  chmod +x /bin/kubeseal

RUN curl -LOJ https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize%2F${KUSTOMIZE_VERSION}/kustomize_${KUSTOMIZE_VERSION}_linux_amd64.tar.gz && \
  tar -xzf kustomize*.tar.gz && \
  mv kustomize /bin/kustomize && \
  rm -f kustomize*.tar.gz

ENV HOME=/ansible
RUN mkdir -p ${HOME} ${HOME}/.ansible/tmp
COPY . /ansible
RUN chmod -R g+w ${HOME} && chgrp -R root ${HOME}
WORKDIR /ansible

ENTRYPOINT ["entrypoint"]
CMD ["sleep", "infinity"]