# Automating AWS With Python
Learning the ins and outs of AWS automation 
Docker container:

```Dockerfile
FROM alpine:3.8

# Python3, pip and git
RUN apk add --no-cache \
    python3 \
    ca-certificates \
    bash \
    git \
    openssh \
    groff \
    less && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    rm -r /root/.cache

# AWS CLI
RUN pip3 --no-cache-dir install awscli && \
    rm -rf /var/cache/apk/*
# node adn NPM
RUN apk add --update nodejs nodejs-npm

# pipenv
RUN pip3 install pipenv

# serverless
RUN npm install -g serverless

# Copy in my ssh keys
RUN mkdir /root/.ssh
# COPY id_rsa id_rsa.pub /root/.ssh/ 
# eval `ssh-agent -s`

# start the container in the /data directory
WORKDIR /data
```

