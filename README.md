# Info

## Stacks

- redmine v2.5.2
- rbenv v0.4.0
- ruby v2.1.2

## Current Setup Info

- A normal user named `amree`
- `amree` can run `sudo`

# Installation

## Pre Install

### Your host

- Set a hostname for the host
- Set a static IP for the host
- 3 domains has been pointed to the host (git.orgname, svn.orgname,
  redmine.orgname)
- Copy your ssh key into the host
- Change the redmine address name in `hosts` file
- Create a copy and change all variables in `vars/all.yml`

### Your workstation

- Install `ansible`
- Copy `hosts.example` to `hosts`

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

