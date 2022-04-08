# How to send files for github

## generate key for connect on github
[https://jdblischak.github.io/2014-09-18-chicago/novice/git/05-sshkeys.html](https://jdblischak.github.io/2014-09-18-chicago/novice/git/05-sshkeys.html)

- list all keys
    $ ls ~/.ssh

- generate keys
    $ ssh-keygen -o -t rsa -C "your@email.com"

Generating public/private rsa key pair.
Enter file in which to save the key (/Users/username/.ssh/id_rsa): `write name of keys file`

Enter passphrase (empty for no passphrase): `write de pass`

- verify your key generate

    cat ~/.ssh/id_rsa.pub

- copy and paste in github keys
    pbcopy < ~/.ssh/id_rsa.pub

    [https://github.com/settings/keys](https://github.com/settings/keys)

# How to generate keys for gitlab

link [https://docs.gitlab.com/ee/ssh/index.html](https://docs.gitlab.com/ee/ssh/index.html)

    cd existing_repo

    git remote add origin https://gitlab.com/xalextrack/streamlit.git
    or 
    git remote add origin git@gitlab.com:xalextrack/streamlit.git
    remove: git remote remove origin

    git branch -M main
    git push -uf origin main
