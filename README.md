# Jekyll Blog Server
https://jekyllrb.com/
https://www.ansible.com/
https://www.vagrantup.com/

## Summary
This is a set of roles and playbooks to produce a Jekyll blog server on CentOS 7,
along with a small Vagrantfile to mimic the environment for local work.

## Vagrant Quick Start
```
vagrant up blog
# copy desired public key into ./files/ssh
# update vars/access.yml to include desired users and refer to correct files
ansible-playbook app.yml -i inventory/dev

cd /path/to/your/blog
git remote add vagrant ssh://web-app@10.19.90.90/srv/git/web-app/blog.git
git branch dev # if branch doesn't already exist
git push vagrant dev:dev # will push to Vagrant and auto-build site
```

### Use
_Developed with Ansible 2.6.5_
The playbooks were designed to set specific variables on a per-host (inventory)
basis, allowing the same playbook to be run against different hosts for different
purposes provided the variables were set. These variables were set up to allow
easy differentiation between dev, stage, and production environments.

#### Variables
- `bootstrap_user`
  - This is the user that is responsible for the initial ssh access and setting
  up further access for the other users. For example, for the AWS CentOS image
  this user would be `centos`, for the Vagrant environment it would be `vagrant`.
- `access_user`
  - This user is intended to be the primary ssh user for your personal access
  and maintenance.
- `app_user`
  - This is the user under which ruby and the necessary gems will be installed.
  This user also owns all Jekyll source and build files.
- `rebuild_branch`
  - This is the name of the branch that will be checked out upon push to the
  git repo on the server. For local environments this may be something like `dev`,
  for stage it may be `staging`, and `master` for production.
