# Lab 2 (First in person)

## SSH into RON via VScode
1. Open VScode
2. cmd + shift + P 
3. Connect current window to host
4. Click ron
5. Clone forked repos onto Ron
```
git clone https://github.com/<username>/<repo>
```
6. Open folder 
7. Save workspace to file (the same folder as your repo)


Bonus: Use terminal to generate ssh key so that you no longer need to enter password at login

        cd ~/.ssh
        ssh-keygen -t ed25519 -b 4096
        chmod 400 ~/.ssh/id_ed25519

- Next, share the public key with the Ron server

        ssh-copy-id username@ron.sr.unh.edu


## Make a lab notebook in your GitHub

