# monkeyrepo
Find packages with the pattern *-LATEST.deb recursivly and create a repo.  
Automatically creates 'Packages' file

Can be used to create a local offline repo, or to create, sign and publish your repo to GIT or any other server.

Tested on Debian 11

### How to use
For help run  
`monkeyrepo -h`

List all uncommited git repos in all subfolders.  
`monkeyrepo-git-status <FOLDER>`

### Add your repo to APT
`REPO="http://yourrepo.url"`  
`KEY="your.gpg.mail@example.org"`  
`KEY_DES="/usr/share/keyrings/$KEY"`  
`SRC_LIST="/etc/apt/sources.list"`  
`wget -q -O- "$REPO/KEY.gpg" | gpg --dearmor | tee "$KEY_DES" >/dev/null`  
`grep -q "$REPO" "$SRC_LIST" ||`  
`echo "deb [signed-by=$KEY_DES] $REPO ./" >>$SRC_LIST`

### Tips
If you constantly create new packages and also want to install these packages, add these short commands to your .bash_aliases file:

```
# Build all packages locally (replace 'my_projekts' with your folder)  
alias repo-make='sudo monkeyrepo $HOME/my_projekts'  

# Build and sign all packages before uploading to your webserver  
alias repo-publish='monkeyrepo $HOME/my_projekts $HOME/my_www_root your.gpg.mail@example.org'  
```