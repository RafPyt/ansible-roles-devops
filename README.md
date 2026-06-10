# ansible-roles-devops

A collection of professional Ansible roles for automating infrastructure deployment on Linux systems.
Each role is self-contained, idempotent, and includes a pre-configured Molecule test suite for local development and CI/CD pipelines.

## 📦 Roles

### 🐳 [docker](roles/docker/README.md)
Automates the installation of Docker Engine and the Docker Compose plugin on Ubuntu systems.
Used as a dependency by other roles in this collection.

### 🔧 [jenkins](roles/jenkins/README.md)
Deploys a Jenkins server in a Docker container using Docker Compose.
Manages system user creation, SSH key generation, directory structure, and the full container lifecycle.
Automatically imports the `docker` role as a dependency.

## 🚀 Usage

Clone the repository and reference the roles by path in your playbook:



```yaml
- hosts: servers
  roles:
    - role: /path/to/ansible-roles/roles/jenkins
      vars:
        jenkins_http_port: 8081
        jenkins_image_tag: "lts"
```

## 🧪 Testing with Molecule

Both roles include a fully pre-configured Molecule test suite using the Docker driver with a systemd-enabled Ubuntu 24.04 image. The test scenarios are ready to use out of the box — if you want to modify a role and verify your changes.


## ⚙️ Requirements

- Ansible 2.15 or higher
- Ubuntu 22.04 (Jammy) or 24.04 (Noble)
- `sudo` privileges on the target host
- Molecule + Docker driver (for local testing only)

## 📄 License

MIT
