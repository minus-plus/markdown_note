
github
check existing SSH keys
ls -al ~/.ssh

check ssh-agent is running
eval $(ssh-agent -s)

Add your SSH private key to the ssh-agent
ssh-add ~/.ssh/id_rsa

copy ssh key to the clipboard
clip < ~/.ssh/id_rsa.pub

following the guide to add the copied key to you account


HOW TO GENERATE NEW KEY
=======================
Open Git Bash.

Paste the text below, substituting in your GitHub email address.

ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
This creates a new ssh key, using the provided email as a label.

Generating public/private rsa key pair.
When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.

Enter a file in which to save the key (/c/Users/you/.ssh/id_rsa):[Press enter]
At the prompt, type a secure passphrase. For more information, see "Working with SSH key passphrases".
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
