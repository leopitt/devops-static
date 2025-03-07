# A DevOps learning project.

A simple learning project to understand the basics of setting up a Docker-based
app and deploy it to the cloud.

This is very much for my own learning, rather than a production-ready /
recommended / best practice setup.

1. Clone the repo
2. Run `docker-compose up -d` to start the docker container and let it run in the background.
3. Visit `http://localhost:5000` to see the app running.

## Pre-requisites

- An AWS EC2 Ubuntu instance.
- A key pair to connect to the instance.
- Security rules on the instance allowing:
  - Inbound SSH access using the key pair
  - Inbound HTTP access on port 80
  - All outbound requests

The following environment variables are requires as secrets in the github repo:

- `AWS_EC2_PEM`: The private key that can be used to connect to the EC2 instance with SSH.
- `AWS_EC2_PUBLIC_USER`: The username to use when connecting to the EC2 instance via SSH.
- `AWS_EC2_PUBLIC_DNS`: The public DNS of the EC2 instance.

## What it does.

The Docker Compose file defines a single service, which is an Apache container
serving a static index.html file.

There is a github workflow that:
- checks out the repo to the github action runner (an ubuntu machine).
- creates a private key to connect to an EC2 instance, from a secret stored in the github repo.
- connects to an EC2 instance via SSH and installs various packages needed to run the site.
- removes the previously checked out code from the EC2 instance.
- copies the freshly checked out code to the EC2 instance.
- connects the EC2 instance and stops/removes/restarts the docker containers.
