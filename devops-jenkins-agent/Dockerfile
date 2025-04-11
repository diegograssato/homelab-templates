FROM docker:latest

LABEL maintainer="Diego Grassato <diego.grassato@gmail.com>"

ARG VCS_REF
ARG BUILD_DATE

# Metadata
LABEL org.opencontainers.image.title="https://github.com/diegograssato/devOpstools" \
      org.opencontainers.image.url="https://helm.sh/docs/"
LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/diegograssato/devOpstools" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.docker.dockerfile="/Dockerfile"

RUN apk add --update ca-certificates \
    && apk add -t deps \
    && apk add --update curl \
    && export ARCH="$(apk --print-arch)" && if [[ ${ARCH} == "x86_64" ]]; then export ARCH="amd64"; elif [[ ${ARCH} == "aarch64" ]]; then export ARCH="arm64"; fi && curl -L https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/${ARCH}/kubectl -o kubectl \
    && install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl \
    && curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | sh \
    && curl -sSL -o argocd-linux-${ARCH} https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-${ARCH} \
    && install -o root -g root -m 0755 argocd-linux-${ARCH} /usr/local/bin/argocd \
    && apk del --purge deps \
    && rm /var/cache/apk/*

ENTRYPOINT ["kubectl"]
CMD ["help"]