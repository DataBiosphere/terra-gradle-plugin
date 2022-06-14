# Extend base agent image with things needed for Terra tests

FROM gradle/gradle-enterprise-test-distribution-agent:1.6.9

# Switch to root user for installing packages
USER root

# Install docker. Needed for DataBiosphere/terra-cli tests.
RUN apt-get update && \
    apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common && \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
    apt-key fingerprint 0EBFCD88 && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
   apt-get update && \
   apt-get install -y docker-ce && \
   systemctl enable docker

# Install gcloud. Needed for DataBiosphere/terra-cli tests.
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - && apt-get update -y && apt-get install gnupg2 -y && apt-get install google-cloud-cli -y

# Switch back to application user
# USER gradle
