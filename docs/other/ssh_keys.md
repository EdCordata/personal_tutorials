# SSH Keys

###### Generate:
```bash
ssh-keygen -t rsa -b 4096 -N '' -C "example@gmail.com" -f ~/.ssh/id_rsa
ssh-keygen -t rsa -b 4096 -N '' -C "example@gmail.com" -f ~/.ssh/github_rsa

touch ~/.ssh/authorized_keys
touch ~/.ssh/known_hosts
touch ~/.ssh/config
```

###### Enable SSH Keys
```bash
ssh-agent bash
ssh-add ~/.ssh/id_rsa
ssh-add ~/.ssh/github_rsa
```

###### Set correct permissions:
```bash
sudo chmod 700 ~/.ssh
sudo chmod 644 ~/.ssh/authorized_keys
sudo chmod 644 ~/.ssh/known_hosts
sudo chmod 644 ~/.ssh/config
sudo chmod 600 ~/.ssh/id_rsa
sudo chmod 644 ~/.ssh/id_rsa.pub
sudo chmod 600 ~/.ssh/github_rsa
sudo chmod 644 ~/.ssh/github_rsa.pub
```

###### Add Domains
```bash
ssh-keyscan -t rsa github.com    >> ~/.ssh/known_hosts
ssh-keyscan -t rsa gitlab.com    >> ~/.ssh/known_hosts
ssh-keyscan -t rsa bitbucket.com >> ~/.ssh/known_hosts
```
