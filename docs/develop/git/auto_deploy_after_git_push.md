---
title: Auto deploy after git push
date: 2022-01-01
hide:
    - tags
tags:
    - git
---

# Auto deploy after git push using post-receive file

## Configuration

To enable the ```post-receive``` hook script, put a file in the hooks subdirectory of your .git directory that is same named (without any extension) and make it executable:

```shell
touch GIT_PATH.git/hooks/post-receive
chmod u+x GIT_PATH.git/hooks/post-receive
```

And here is the sample of ```post-receive``` file deploying a django project
!!! Sample
    ```shell title="GIT_PATH.git/hooks/post-receive"
    #!/bin/sh
    cd /home/user/scripts/django
    sudo -u uesr git pull
    sudo systemctl restart gunicorn
    ```

When there is sudo command, you need to adding ```sudoers``` file to auth run command without entering password by:

`sudo visudo -f /etc/sudoers.d/whatevername`

!!! Sample
    ```shell title="/etc/sudoers.d/whatevername"
    git ALL=(radio) NOPASSWD: /usr/bin/git
    git ALL=(ALL) NOPASSWD: /bin/systemctl restart gunicorn
    ```


After all, the commands inside `post-receive`  will run when you doing `git push`


## References

[Using Hook post-receive](https://www.digitalocean.com/community/tutorials/how-to-set-up-automatic-deployment-with-git-with-a-vps)

[Running as different user](https://superuser.com/questions/745762/how-to-execute-commands-as-root-in-git-post-receive-hook)