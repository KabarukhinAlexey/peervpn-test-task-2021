peervpn-role
=========

Ansible-роль предназначена для сборки, выкладки и установки пакета peervpn для Ubuntu Bionic

Role Variables
--------------

vars/main.yml
- packages_list_for_build - список пакетов, необходимых для сборки peervpn
- peervpn_deb_package_version - версия бинарного исполняемого deb пакета
- peervpn_deb_package_architecture - архитектура исполняемого deb пакета
- repo_base_path - путь, по которому располагаются пакеты репозитория. Значением переменной является "DocumentRoot Apache2 сервера" + "/debs"
- repo_host - хост с репозиторием. По умолчанию - localhost

Tasks execution
--------------
Файл tasks/main.yml включает в себя 2 таски include_tasks с тегами build и install, которые логически соответствуют 2-м частям задания:
- build нужен для сборки и выкладки deb пакета
- install нужен для проверки выполнения задания путем установки из репозтория собранного пакета 

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
