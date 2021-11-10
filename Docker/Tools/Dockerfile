  
FROM amazonlinux:2 as installer
ARG EXE_FILENAME=awscli-exe-linux-x86_64.zip
# Based upon https://github.com/aws/aws-cli/blob/2.0.10/docker/Dockerfile
ARG TERRAFORM_VERSION=1.0.3
RUN yum update -y \
  && yum install -y unzip \
  && curl https://awscli.amazonaws.com/${EXE_FILENAME} -o ${EXE_FILENAME} \
  && unzip awscli-exe-linux-x86_64.zip \
  # The --bin-dir is specified so that we can copy the
  # entire bin directory from the installer stage into
  # into /usr/local/bin of the final stage without
  # accidentally copying over any other executables that
  # may be present in /usr/local/bin of the installer stage.
  && ./aws/install --bin-dir /aws-cli-bin/ \
  && curl "https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip" -o terraform.zip \
  && unzip terraform.zip

FROM amazonlinux:2
COPY --from=installer /usr/local/aws-cli/ /usr/local/aws-cli/
COPY --from=installer /aws-cli-bin/ /usr/local/bin/
COPY --from=installer terraform /usr/bin/
RUN yum update -y \
  && yum install -y less groff jq tar gzip unzip git go\
  && yum clean all

RUN amazon-linux-extras install -y docker
RUN curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

ENTRYPOINT ["/bin/sh"]