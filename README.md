# EHER.git
Ansible role to create bare git repositories with hooks.

## variables
- eher_git_path - Path to where the git repository will be created
- eher_git_hook_post_receive - Command to be executed at post-receive hook
- eher_git_hook_pre_receive - Command to be executed at pre-receive hook

## how it works?
You cand use the role as you want. The basic use is add to your site.yml and set some required variables.
```yml
---
roles:
  - role: EHER.git
    eher_git_path: /home/git/queroservoluntario.git
    eher_git_hook_post_receive: "make deploy"
```

Before run the role, make sure that you have your keys into files/authorized_keys. That keys are used to allow git connection.
```bash
cat ~/.ssh/id_rsa.pub >> files/authorized_keys
```

After run the role, you should have your own git repository with hook. Then you can add as a remote server.
```bash
git remote add production git@myserver:querservoluntario.git
```

Push the code and watch the hook output.
```bash
git push production master
```

That will push your master branch to server and then trigger the post-receive hook. The command "make deploy" will run. Your "make deploy" can do wharever you want, as install dependencies, run tests, update database, copy the project to web directory, etc.

## installation

```bash
ansible-galaxy install EHER.git
```
or 
```bash
ansible-galaxy install -p roles EHER.git
```
