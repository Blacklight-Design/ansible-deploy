# Standard Deploy

Brought to you by [Blacklight](http://www.blacklight.co.za).

Deployment role for standard apps. Deployment can be done via Git, SVN, Mercurial, and Rsync. Tries to imitate a similar
structure to what you would see with other deployment tools such as [Capistrano](http://capistranorb.com/). The final
directory structure will look something like this:

```
project
    releases
        // All releases will be going here
    shared
        app
            storage
                logs
                sessions
        public
            uploads
    current // This will be a symlink to the latest release
```

The role also has error checking in place. If any of the steps fail the role will delete the newly created release folder
and stop execution. If the deploy was successful the role will remove old releases.

Other Deployment Roles
---------------------

Symfony: [symfony-deploy](https://galaxy.ansible.com/list#/roles/2111)

Laravel5: [laravel5-deploy](https://galaxy.ansible.com/list#/roles/2145)

Requirements
------------

The only requirement is Ansbile >= 1.2.

Installation
------------

```
ansible-galaxy install blacklight.standard-deploy
```

Role Variables
--------------

### deploy_root_dir (Required)

The root directory of the project.

### deploy_repo (Required)

The URL to the repo containing the application code.

### deploy_branch (Defaults: master)

The branch that you would like to deploy.

### deploy_strategy (Defaults: git)

The deployment strategy to use. Available options: git, svb, mercurial, rsync

### deploy_local_root (Defaults: /)

This option is only used when deploying via Rsync. It defines the path to the local folder to upload to the server.

*Important Note!* The path is relative to your playbook file.

### deploy_releases (Defaults: 5)

The amount of releases to keep in the releases directory.

Example Playbook
----------------

```yml
---
- hosts: web
  vars:
    deploy_root_dir: /var/www/example
    deploy_repo: git@github.com/example/example-project.git
    ansible_ssh_user: root

  roles:
    - blacklight.standard-deploy
```

License
-------

MIT
