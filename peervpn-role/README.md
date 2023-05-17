peervpn-role
=========

The Ansible role is designed for building, deploying, and installing the peervpn package for Ubuntu Bionic.

Role Variables
--------------

vars/main.yml
- packages_list_for_build - a list of packages needed to build peervpn
- peervpn_deb_package_version - version of the binary executable deb package
- peervpn_deb_package_architecture - architecture of the executable deb package
- repo_base_path - the path where the repository packages are located. The variable value is "DocumentRoot of Apache2 server" + "/debs"
- repo_host - repository host. By default - localhost

Tasks execution
--------------
The tasks/main.yml file includes 2 include_tasks with build and install tags, which logically correspond to the 2 parts of the task:
- build is necessary for building and deploying the deb package
- install is necessary to check the execution of the task by installing the compiled package from the repository

Handlers
--------------
This Ansible role has two handlers "Copy package to local repo" and "Run dpkg-scanpackages", which are called upon a new successful build of the deb package. The handlers copy the deb package to the local repository and update the repository with the dpkg-scanpackages command.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: localhost
      become_user: root
      roles:
        - role: peervpn-role

License
-------
GNU General Public License v3.0

Author Information
------------------

Aleksei Kabarukhin
