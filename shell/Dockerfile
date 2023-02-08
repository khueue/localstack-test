FROM python:3.11.1-bullseye

RUN apt update

# Terraform.
ENV TF_VERSION=1.3.7
RUN curl --location https://releases.hashicorp.com/terraform/${TF_VERSION}/terraform_${TF_VERSION}_linux_amd64.zip \
		--output ./terraform.zip \
	&& unzip ./terraform.zip \
	&& mv ./terraform /usr/local/bin/ \
	&& rm -rf ./terraform.zip

# For AWS CLI.
RUN apt install -y \
	groff \
	less

# AWS CLI.
ENV AWSCLI_VERSION=2.9.21
RUN curl --location https://awscli.amazonaws.com/awscli-exe-linux-x86_64-${AWSCLI_VERSION}.zip \
		--output ./awscli.zip \
	&& unzip ./awscli.zip \
	&& ./aws/install \
	&& rm -rf ./awscli.zip ./aws/

# Localstack AWS CLI wrapper.
RUN pip install awscli-local
ENV LOCALSTACK_HOST=localstack
