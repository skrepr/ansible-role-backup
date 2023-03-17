<a href="https://skrepr.com/">
  <p align="center">
    <img width="200" height="100" src="https://skrepr.com/wp-content/uploads/2021/10/skrepr_logo_liggend.svg" alt="skrepr" />
  </p>
</a>
<h1 align="center">Ansible Role Backup</h1>
<div align="center">
  <a href="https://github.com/skrepr/ansible-role-backup/releases"><img src="https://img.shields.io/github/release/skrepr/ansible-role-backup.svg" alt="Releases"/></a><a> </a>
  <a href="https://github.com/skrepr/ansible-role-backup/blob/main/LICENSE"><img src="https://img.shields.io/github/license/skrepr/ansible-role-backup" alt="LICENSE"/></a><a> </a>
  <a href="https://github.com/skrepr/ansible-role-backup/actions/workflows/ci.yml"><img src="https://github.com/skrepr/ansible-role-backup/actions/workflows/ci.yml/badge.svg" alt="CI"/></a><a> </a>
  <a href="https://github.com/skrepr/ansible-role-backup/issues"><img src="https://img.shields.io/github/issues/skrepr/ansible-role-backup.svg" alt="Issues"/></a><a> </a>
  <a href="https://github.com/skrepr/ansible-role-backup/pulls"><img src="https://img.shields.io/github/issues-pr/skrepr/ansible-role-backup.svg" alt="PR"/></a><a> </a>
  <a href="https://github.com/skrepr/ansible-role-backup/commits"><img src="https://img.shields.io/github/commit-activity/m/skrepr/ansible-role-backup" alt="Commits"/></a><a> </a>
  <a href="https://github.com/skrepr/ansible-role-backup/stars"><img src="https://img.shields.io/github/stars/skrepr/ansible-role-backup.svg" alt="Stars"/></a><a> </a>
  <a href="https://github.com/skrepr/ansible-role-backup/releases"><img src="https://img.shields.io/github/forks/skrepr/ansible-role-backup.svg" alt="Forks"/></a><a> </a>
</div>

# About

This Ansible role is used for deploying a backup script on a Debian server

[![Ansible Role](https://img.shields.io/ansible/role/56860)](https://galaxy.ansible.com/skrepr/backup)
[![Ansible Role](https://img.shields.io/ansible/role/d/56860)](https://galaxy.ansible.com/skrepr/backup)
[![Ansible Quality Score](https://img.shields.io/ansible/quality/56860)](https://galaxy.ansible.com/skrepr/backup)

## Requirements

- SSH access to the server
- aws-cli on your computer
- `pip3 install boto3`
- `ansible-galaxy collection install community.aws`
- `ansible-galaxy collection install amazon.aws`

## Role Variables

```yaml
---


customer: yourcustomer # used for naming resources
app: myapplication # Used for naming resources
jira_key: APP # Used for tagging resource in AWS

# S3 settings
aws_profile: default
s3_human_readable_sizes: true

# MySQL database backup options.
backup_mysql_user: backup
backup_mysql_password: y0urverys3curep4ss

# Script settings
deletetime: 30 days
directory: daily
minimal_backups: 5

# Backup cron job options.
backup_cron_job_state: present
backup_hour: "3"
backup_minute: "00"

# User under which backup jobs will run.
backup_user: root

# Path to where backups configuration will be stored.
backup_path: /{{ backup_user }}/backup
```

## Example Playbook

```yaml
#!/usr/bin/env ansible-playbook


- hosts: production
  name: Database backup to S3 script
  become: true
  become_user: root

  roles:
    - skrepr.backup

```

## License

MIT / BSD

## Author Information

This role was created in 2023 by [Jeroen van der Meulen](https://github.com/jeroenvandermeulen), commisioned by [Skrepr](https://skrepr.com)