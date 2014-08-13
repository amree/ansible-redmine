
# ALERT

This playbook has only been tested in Virtual Machines (with positive results). Will be deployed in production in the coming weeks. Most of the scripts are done. however I really need to update the README to make sure it's more friendly for new people.

# Info

## Features

- redmine v2.5.2
- rbenv v0.4.0
- ruby v2.1.2 
- Advance Git integration with Redmine
- Advance Subversion integration with Redmine
- One authentication for everything (Redmine, Subversion and Git)
- Support for Slack
- Support for Microsoft Exchange Email
- Support for sendmail
- Support for repository creation through the web
- Only support MySQL
- Installed with Basecamp theme (waay better than the default theme)
- Only for Debian host

## Current Setup

- A normal user named `amree`
- `amree` can run `sudo`

# Installation

## Pre Install

### Your Redmine

- Set a hostname, for e.g: Redmine
- Set a static IP
- 3 domains has been pointed to the Redmine (e.g: git.orgname, svn.orgname,
  redmine.orgname)
- Create a copy and change all variables in `vars/all.yml`

### Your workstation

- Install `ansible`
- Copy `hosts.example` to `hosts` and fill in the values
- Copy `vars/all.example.yml` to `vars/all.yml` and fill in the values
- Copy your ssh key into Redmine

## Install

```
ansible-playbook -K -i hosts site.yml
```

## Post Install

Make sure you can do these tasks:

...

# Extra

## Creating Repository (Manually)

### Git

```
$ cd /opt/git
$ git init --bare reponame
$ chown root.www-data -R reponame
$ chmod 775 -R reponame
```

### Subversion

```
$ cd /opt/svn
$ svnadmin create reponame
$ chown root.www-data -R reponame
$ chmod 775 -R reponame
```

##  Gotchas

1. First git commit won't be sent to Slack since there's no oldrevision, just
   new revision.
2. URL generated in Slack might not be accurate if you use different identifier
   for your repository or if you have multiple repository per project.

## Reminders

- You must be at least a Developer or Manager for the project to gain access to the repository
- You have to edit some files manually if you changed the API key after the
  installation
- This ansible playbook is not idempotent! So, it should only work on the first
  try

