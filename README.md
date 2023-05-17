## Test Assignment
Create an updatable repository for Ubuntu Bionic

Initial data:
Project https://github.com/peervpn/peervpn

- Task:
Build the project from the source for Ubuntu Bionic
Package the resulting binary executable file into a deb package, the file should be installed in /usr/local/bin/
Publish the deb package in an HTTP repository (GPG encryption is not required)

- Expected result:
A set of scripts (programs, Ansible playbooks, etc.) that allow you to build and package the binary file into a deb package and publish it to the repository for Ubuntu Bionic

- Verification of the result:
The obtained repository is connected to Ubuntu Bionic and does not give errors when calling apt update (errors due to the absence of a GPG signature are allowed)
The compiled deb package is installed from the repository, the binary file is placed in /usr/local/bin

## Instructions for running the playbooks
Running the playbook with tags for building and publishing the built package to the local repository.
```
ansible-playbook play.yml --tags build
```
Running the playbook to test the application installation according to the task statement.
```
ansible-playbook play.yml --tags install
```

## Comments

 The source code of the peervpn project is written for the use of the libssl library version 1.0, which is already outdated. For successful package compilation, it is necessary
 - either to fork the peervpn project and adjust the code for using libssl 1.1, as it is done, for example, in the repository https://github.com/BugMaster510945/peervpn
 - or install libssl version 1.0 before building (the source code remains unchanged)
 
The task statement says "build the project from sources for ubuntu bionic", which rather does not imply editing the source code, however, if it were necessary to edit the source code, I would additionally add a file to it to run the peervpn service and a standard peervpn config file.

Additional comments on the written ansible role can be found in its README file inside the peervpn-role directory.

## Assumptions
- The server with the deb package repository is the same server on which the assembly takes place. If a separate server was used for the repository, the code would be slightly different.
- Apache2 web server is installed during the execution of the playbook and has default settings, including the default DocumentRoot: "/var/www/html", which is partially set within the "repo_base_path" variable. Firewall and selinux settings are not affected.
- Files generated during the execution of the playbook in the repository directory have the mask "peervpn_*", which is accounted for in the gitignore file.
 
