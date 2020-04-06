# Creating and copying ssh key from Windows using Powershell
From https://www.techrepublic.com/blog/10-things/how-to-generate-ssh-keys-in-openssh-for-windows-10/

- Create key with `ssh-keygen`
- Create .ssh folder with `ssh username@address mkdir ~/.ssh`
- Copy the public key with `scp .\id_rsa.pub username@address:~/.ssh/authorized_keys`