# Ansible Role: Docker Installation

An Ansible role designed to automate the installation of Docker Engine and Docker Compose plugin on supported Linux distributions. It includes a validation mechanism to prevent redundant installations if Docker is already present, and it features full Molecule testing support using Docker-in-Docker.


## Features

* **OS Validation:** Strictly ensures the role runs only on supported operating systems.
* **Idempotency Check:** Skips repository setup and installation tasks if Docker is already installed.
* **GPG Key Management:** Securely downloads and configures the official Docker GPG keyring.
* **Repository Configuration:** Automatically adds the official Docker stable repository tailored to the system's distribution release.
* **Component Installation:** Installs `docker-ce`, `docker-ce-cli`, `containerd.io`, `docker-buildx-plugin`, and `docker-compose-plugin`.
* **Service Management:** Ensures the Docker systemd service is enabled and actively running.


## Requirements

* **Ansible Version:** 2.10 or higher
* **Privileges:** Access to `become: true` (root privileges) is required for package installation and service management.


## Testing with Molecule

This role includes a fully pre-configured Molecule test suite using the Docker driver and a systemd-enabled Ubuntu 24.04 image.

To run the test suite, ensure you have Molecule and the Docker driver installed