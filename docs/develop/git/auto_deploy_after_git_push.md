---
title: Auto deploy after git push
description: Auto deploy after git push
created: 2022-02-01
tags:
  - 'Git'
---

## How to

To enable the ```post-receive``` hook script, put a file in the hooks subdirectory of your .git directory that is same named (without any extension) and make it executable:

```shell
touch GIT_PATH.git/hooks/post-receive
chmod u+x GIT_PATH.git/hooks/post-receive
```

And here is the sample of ```post-receive``` file  
```shell
#!/bin/sh
cd /home/radio/scripts/django_opt
sudo -u radio git pull
sudo systemctl restart gunicorn
```

When there is sudo command, you need to adding ```sudoers``` file to auth the command without entering password by:

`sudo visudo -f /etc/sudoers.d/whatevername`
```shell
git ALL=(radio) NOPASSWD: /usr/bin/git
git ALL=(ALL) NOPASSWD: /bin/systemctl restart gunicorn
```

After all, the commands inside `post-receive`  will run when you doing `git push`


## References

[Using Hook post-receive](https://www.digitalocean.com/community/tutorials/how-to-set-up-automatic-deployment-with-git-with-a-vps)

[Running as different user](https://superuser.com/questions/745762/how-to-execute-commands-as-root-in-git-post-receive-hook)