# GitLab Runner with AWS EC2 Autoscaling

This repository contains the configuration and instructions for setting up GitLab Runners using AWS EC2 instances with autoscaling capabilities. This setup allows GitLab Runners to dynamically create and terminate EC2 instances based on the job load, optimizing resource usage and cost.

## Prerequisites

- AWS Account with IAM permissions to manage EC2 instances.
- GitLab account with a project where the runner will be registered.
- An EC2 instance for initial setup.
- Docker and Docker Machine installed on the setup EC2 instance.

## Step-by-Step Setup

### 1. Generate an SSH Key Pair

1. Open Terminal on your Mac (or SSH into your setup EC2 instance).
2. Generate the SSH key pair:
    ```bash
    ssh-keygen -t ed25519 -C "your_email@example.com"
    ```
3. Start the SSH agent and add the key:
    ```bash
    eval "$(ssh-agent -s)"
    ssh-add -K ~/.ssh/id_ed25519
    ```

### 2. Install Docker Machine

Install Docker Machine on your setup EC2 instance:

```bash
curl -L https://github.com/docker/machine/releases/download/v0.16.2/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine &&
sudo install /tmp/docker-machine /usr/local/bin/docker-machine
