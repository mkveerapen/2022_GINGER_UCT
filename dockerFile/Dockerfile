# Pull base image
FROM ubuntu:18.04

LABEL maintainer="veerapen@broadinstitute.org"

# clean up apt get
RUN apt-get clean && apt-get update
RUN apt-get install -y curl
RUN apt-get install -y python


# Downloading gcloud package
RUN curl https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz > /tmp/google-cloud-sdk.tar.gz

# Installing the package
RUN mkdir -p /usr/local/gcloud \
  && tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz \
  && /usr/local/gcloud/google-cloud-sdk/install.sh

# Adding the package path to local
ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin

# Installation instructions: https://www.cog-genomics.org/plink2

# Environment variables
ENV PLINK_VERSION       150314
ENV PLINK_HOME          /usr/local/plink
ENV PATH                $PLINK_HOME:$PATH

RUN apt-get install -y unzip

RUN curl -LO 'https://s3.amazonaws.com/plink2-assets/plink2_linux_x86_64_20220328.zip' 

RUN unzip plink2_linux_x86_64_20220328.zip && rm plink2_linux_x86_64_20220328.zip 

RUN mv plink2 plink && \
    mv plink /usr/local/bin/
