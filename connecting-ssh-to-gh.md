# Generating new key pair and connecting to Github
## Generate new key
ssh-keygen -t rsa -b 4096 -C "vineet.sethi@hotmail.co.uk" to generate a new key pair 

## Linking onto Github with key
Settings in Github and SSH and GPG key
cat vineet-github-key.pub - to get the public key displayed

eval `ssh-agent -s`

ssh-add vineet-github-key

ssh -T git@github.com

create test repo

