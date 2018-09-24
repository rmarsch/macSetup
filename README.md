# macSetup
Useful things that are easy to forget when setting up my ideal mac os dev environment

## iTerm

How to setup my preferred way of moving forward and back characters as well as restoring page forward and back in vim
![image](https://user-images.githubusercontent.com/3334671/45964183-12502300-bff3-11e8-87d0-b2549c1db1df.png)

## Git setup in .bash_profile
Setup the prompt and also a shortcut for throwing a commit back into the prior commit (although it's better to just not commit the next bit and do the amend)

```
[ -f /usr/local/etc/bash_completion ] && . /usr/local/etc/bash_completion

GIT_PS1_SHOWDIRTYSTATE=true

alias git-push="git push -u origin HEAD"

git-squash-into-last() {
	git reset --soft HEAD~1
	git commit --amend --no-edit
}

gb() {
	echo -n ' [' && git branch 2>/dev/null | grep "^*" | colrm 1 2 | tr -d '\n' && echo -n ']'
}

git-branch() {
	gb | sed 's/ \[\]//'
}

PS1='\[\033[0;32m\]\[\033[0m\033[0;32m\]\u\[\033[0;36m\]@\w\[\033[0;32m\]$(git-branch)\[\033[0;32m\]\[\033[0m\033[0;32m\] \$\[\033[0m\033[0;32m\]\[\033[0m\] '
```
