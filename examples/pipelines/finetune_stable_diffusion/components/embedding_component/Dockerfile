FROM --platform=linux/amd64 pytorch/pytorch:2.0.0-cuda11.7-cudnn8-runtime

## System dependencies
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install git curl -y

# Downloading gcloud package
RUN curl https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz > /tmp/google-cloud-sdk.tar.gz

# Installing the package
RUN mkdir -p /usr/local/gcloud \
&& tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz \
&& /usr/local/gcloud/google-cloud-sdk/install.sh

# Adding the package path to local
ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin

# install requirements
COPY requirements.txt /tmp/requirements.txt
RUN python3 -m pip install -r /tmp/requirements.txt

# Copy over src-files of the component
COPY src /src

# Set the working directory to the source folder
WORKDIR /src

ENTRYPOINT ["python", "main.py"]