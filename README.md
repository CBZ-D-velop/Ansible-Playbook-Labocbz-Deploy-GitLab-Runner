# Ansible playbook: labocbz.deploy_gitlab_runner

![Licence Status](https://img.shields.io/badge/licence-MIT-brightgreen)
![CI Status](https://img.shields.io/badge/CI-success-brightgreen)
![Testing Method](https://img.shields.io/badge/Testing%20Method-Ansible%20Molecule-blueviolet)
![Testing Driver](https://img.shields.io/badge/Testing%20Driver-docker-blueviolet)
![Language Status](https://img.shields.io/badge/language-Ansible-red)
![Compagny](https://img.shields.io/badge/Compagny-Labo--CBZ-blue)
![Author](https://img.shields.io/badge/Author-Lord%20Robin%20Crombez-blue)

## Description

![Tag: UNIX](https://img.shields.io/badge/Tech-UNIX-orange)

An Ansible playbook to install and configure Docker, docker-compose and deploy a GitLab runner on a server based on Debian/Ubuntu.

## Deployment diagramm

## Tests and simulations

### Basics

You have to run multiples tests. *tests with an # are mandatory*

```MARKDOWN
# lint
# syntax
# converge
# idempotence
# verify
side_effect
```

Executing theses test in this order is called a "scenario" and Molecule can handle them.

Molecule use Ansible and pre configured playbook to create containers, prepare them, converge (run the playbook) and verify its execution.
You can manage multiples scenario with multiples tests in order to get a 100% code coverage.

This playbook contains a ./tests folder. In this folder you can use the inventory or the tower folder to create a simualtion of a real inventory and a real AWX / Tower job execution.

### Command reminder

```SHELL
# Check your YAML syntax
yamllint -c ./.yamllint .

# Check your Ansible syntax and code security
ansible-lint --config=./.ansible-lint .

# Execute and test your playbook
molecule lint
molecule create
molecule list
molecule converge
molecule verify
molecule destroy

# Execute all previous task in one single command
molecule test
```

## Installation

To install this playbook, just copy/import this playbook or raw file into your fresh playbook repository or call it with the "include_playbook/import_playbook" module.

## Usage

### Vars

```YAML
# From inventory
---
all vars from to put/from your inventory

# Special for Docker cleaning (docker system prune)

inv_handle_docker_clean: true

inv_handle_docker_clean_cron_file: "ansible_docker_system_prune"
inv_handle_docker_clean_weekday: "*"
inv_handle_docker_clean_minute: "*"
inv_handle_docker_clean_hour: "*/6"

```

```YAML
# From AWX / Tower
---
all vars from to put/from AWX / Tower
```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-09-28: First Init

* First init of this playbook with the bootstrap_playbook playbook by Lord Robin Crombez

### 2023-10-06: New CICD, new Images

* New CI/CD scenario name
* Molecule now use remote Docker image by Lord Robin Crombez
* Molecule now use custom Docker image in CI/CD by env vars
* New CICD with needs and optimization

### 2023-12-02: Docker clean

* Playbook can create or remove crontab job to handler a complete docker system prune

### 2023-12-18: Docker certs

* Added the install Docker role, so Docker will be installed
* Handler certs for Docker / Portainers 

### 2024-02-24: Fix and CI

* Added support for new CI base
* Edit all vars with __
* Tested and validated on Docker DIND
* Removed docker socket
* Tested and validated on LOCAL with REAL Token, but removed for tests
* Removed handling for Portainer and docker, playbook is not about deploying Portainer
* Added SonarQube

## Authors

* Lord Robin Crombez

## Sources

* [Ansible playbook documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_playbooks.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
