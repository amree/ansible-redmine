# README

**ATTENTION: THIS REPOSITORY IS NOT ACTIVE ANYMORE**

## Features

- redmine v2.5.2
- rbenv v0.4.0
- ruby v2.1.2 
- Advance Git and Subversion integration with Redmine
- One authentication for everything (Redmine, Subversion and Git)
- Support for Slack
- Support for Microsoft Exchange Email
- Support for sendmail
- Support for repository creation through the web
- Only support MySQL
- Installed with Basecamp theme (waay better than the default theme)
- Only tested on Debian Wheezy

# Installation

## Pre Install

### Your Redmine (your target host)

- Set your hostname and domain e.g redmine.orgname
- Set a static IP
- Make sure it's added in your DNS record
- Three domains has been pointed to the Redmine (e.g: git.orgname, svn.orgname,
  redmine.orgname)
- Make sure you've set your timezone correctly

### Your workstation

- Install `ansible`
- Clone this repository
- Copy `hosts.example` to `hosts` and fill in the IP of your Redmine
- Copy `vars/all.example.yml` to `vars/all.yml` and fill in the values
- Check `site.yml` and comment out optional roles that you don't want by adding `#` in front of it
- Copy your ssh key into Redmine

## Install

```
ansible-playbook -K -i hosts site.yml
```

## Post Install

Make sure you can do these tasks (Step by step tutorial will be written in due time):

1. Open your Redmine URL
2. Login as admin, the default is `admin` for username and password
3. Make sure to change admin's email to a valid email
4. Create a project
5. Assign admin as a Manager or Developer for the project
6. Create two issues in the newly created project
7. Create a Git repository from the web interface
8. Clone/Checkout the project into your workstation
9. Create a file, put some contents
10. Push or commit your changes. Make sure you'll close the issue created just now using your commit message
11. Check the issue to make sure it's closed
12. Check repository tab to ensure your changes are available
13. Repeat step 5, but this time with Subversion repository
14. Check `/var/log/apache2/error.log` for any errors.

# Extra

##  Gotchas

1. First git commit won't be sent to Slack as there's no old revision, just
   new revision.
2. URL generated in Slack might not be accurate if you use different identifier
   for your repository or if you have multiple repository per project.

## Reminders

- You must be at least be a Developer or Manager for the project to gain access to the repository
- You have to edit some files manually if you changed the API key after the installation
- This ansible playbook is not idempotent! So, it should only work on the first run

# TODO

- [SSL Certificate](http://runssl.com/members/knowledgebase/9/SSL-Certificate-For-Private-Internal-IP-Address-or-Local-Intranet-Server-Name.html)

