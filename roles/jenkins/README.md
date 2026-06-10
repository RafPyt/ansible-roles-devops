# Ansible Role: Jenkins Docker Compose

A professional Ansible role for deploying a Jenkins server in a Docker container using Docker Compose. The role automates system user configuration, directory structure setup, and container lifecycle management.

## 📋 Role Features

- **Dependency installation:** Automatically installs the Python packages required for Docker modules in Ansible.
- **User management:** Creates a dedicated system user along with a secure SSH key pair (Ed25519).
- **Molecule support:** Includes a built-in fix for the OverlayFS driver (switching to vfs), enabling seamless testing in nested Docker environments.
- **Data persistence:** Maps key Jenkins directories to the host, ensuring the durability of configuration and jobs.
- **Host DNS integration:** Mounts `/etc/hosts` in read-only mode, allowing Jenkins to resolve server names defined at the host system level.
- **Automatic refresh:** Uses the Handlers mechanism to restart the container only when its definition or directory structure changes.

## ⚙️ Default Variables (`defaults/main.yml`)

| Variable | Default Value | Description |
|---|---|---|
| `jenkins_user` | `jenkins` | System username on the host. |
| `jenkins_http_port` | `8080` | Port on which the web interface will be available. |
| `jenkins_jnlp_port` | `50000` | Port for communication with JNLP agents. |
| `jenkins_data_path` | `/var/jenkins` | Storage path for configuration, plugins, and jobs. |
| `jenkins_compose_path` | `/var/jenkins/dockercompose` | Location of the `docker-compose.yml` file. |
| `jenkins_image_tag` | `latest` | Image tag from DockerHub (`lts`, `latest`, or a specific version). |

## 📂 Directory Structure

The role creates the following structure on the server:

- `{{ jenkins_compose_path }}/` — Storage location for the deployment definition.
- `{{ jenkins_data_path }}/` — Jenkins home directory (mounted as a volume).
- `/home/{{ jenkins_user }}/.ssh/` — SSH keys for the system user.

## 🔄 Event Handling (Handlers)

The role includes a **"Restart Jenkins"** handler, which is triggered automatically when the following change:

- Permissions or locations of project directories.
- The contents of the `docker-compose.yml` file (generated from a template).

## 🚀 Quick Start (Manual Management)

After running the role via Ansible, you can manage the container directly from the server using standard commands:

```bash
# Navigate to the project directory
cd {{ jenkins_compose_path }}

# Check status
docker compose ps

# Retrieve the initial admin password
docker compose logs jenkins | grep -A 5 "initialAdminPassword"

# Manual restart
docker compose restart
```

## 🛠 Requirements

- Debian/Ubuntu-based operating system.
- External `docker` role (imported inside `tasks/main.yml`).
- `sudo` privileges on the target host.

## 📝 Usage Example (Playbook)

```yaml
- hosts: servers
  roles:
    - role: jenkins
      vars:
        jenkins_http_port: 8081
        jenkins_image_tag: "lts"
```
