A simple learning project to understand the basics of setting up a Docker-based
app and deploy it to the cloud.

1. Clone the repo
2. Run `docker-compose up -d` to start the docker container and let it run in the background.
3. Visit `http://localhost:5000` to see the app running.

## What it does.

The Docker Compose file defines a single service, which is an Apache container
serving a static index.html file.

There is a github workflow that connects to an EC2 instance via SSH and installs
various packages needed to run the site.

The following environment variables are set as secrets in the github repo:

- `AWS_EC2_PEM`: The private key that can be used to connect to the EC2 instance with SSH.
- `AWS_EC2_PUBLIC_USER`: The username to use when connecting to the EC2 instance via SSH.
- `AWS_EC2_PUBLIC_DNS`: The public DNS of the EC2 instance.
