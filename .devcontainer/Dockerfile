# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.241.1/containers/alpine/.devcontainer/base.Dockerfile

# [Choice] Alpine version: 3.15, 3.14, 3.13
ARG VARIANT="3.15"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-alpine-${VARIANT}

# ** [Optional] Uncomment this section to install additional packages. **
RUN apk update \
    && apk upgrade \
    && apk add --no-cache git python3 go zsh terraform vim py3-pip unzip tzdata ca-certificates jq cosign #rust

ARG OPA_VERSION="v0.43.0"
RUN curl -L -o opa https://openpolicyagent.org/downloads/${OPA_VERSION}/opa_linux_amd64_static
RUN chmod 755 opa
RUN mv opa /usr/local/bin/opa

ARG GCLOUD_CLI_VERSION="396.0.0"
RUN curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-${GCLOUD_CLI_VERSION}-linux-x86_64.tar.gz
RUN tar -xf google-cloud-cli-${GCLOUD_CLI_VERSION}-linux-x86_64.tar.gz
RUN ./google-cloud-sdk/install.sh

RUN pip install pre-commit

#RUN CONFTEST_LATEST_VERSION=$(wget -O - "https://api.github.com/repos/open-policy-agent/conftest/releases/latest" | grep '"tag_name":' | sed -E 's/.*"([^"]+)".*/\1/' | cut -c 2-) \
#    && curl -O https://github.com/open-policy-agent/conftest/releases/download/v${CONFTEST_LATEST_VERSION}/conftest_${LATEST_VERSION}_Linux_x86_64.tar.gz \
#    && tar xzf conftest_${CONFTEST_LATEST_VERSION}_Linux_x86_64.tar.gz \
#    && mv conftest /usr/local/bin

ARG HOVERFLY_VERSION="v1.3.5"
RUN curl -L -o hoverfly_bundle_linux_amd64.zip https://github.com/SpectoLabs/hoverfly/releases/download/${HOVERFLY_VERSION}/hoverfly_bundle_linux_amd64.zip
RUN unzip hoverfly_bundle_linux_amd64.zip
RUN mv hoverfly /usr/local/bin/
RUN mv hoverctl /usr/local/bin/

#ARG TERRAFORMER_PROVIDER={all,google,aws,kubernetes}
#RUN curl -LO https://github.com/GoogleCloudPlatform/terraformer/releases/download/$(curl -s https://api.github.com/repos/GoogleCloudPlatform/terraformer/releases/latest | grep tag_name | cut -d '"' -f 4)/terraformer-${PROVIDER}-linux-amd64
#RUN chmod +x terraformer-${PROVIDER}-linux-amd64
#RUN mv terraformer-${PROVIDER}-linux-amd64 /usr/local/bin/terraformer

ARG HADOLINT_VERSION="v2.10.0"
RUN wget -O /usr/local/bin/hadolint https://github.com/hadolint/hadolint/releases/download/${HADOLINT_VERSION}/hadolint-Linux-x86_64
RUN chmod +x /usr/local/bin/hadolint

ARG SHELLCHECK_VERSION="stable" # or "v0.4.7", or "latest"
RUN wget -qO- "https://github.com/koalaman/shellcheck/releases/download/${SHELLCHECK_VERSION}/shellcheck-${SHELLCHECK_VERSION}.linux.x86_64.tar.xz" | tar -xJv
RUN mv "shellcheck-${SHELLCHECK_VERSION}/shellcheck" /usr/local/bin/
#RUN shellcheck --version
