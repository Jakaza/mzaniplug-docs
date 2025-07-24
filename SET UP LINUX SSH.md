### Generate SSH key
Use same email as GitHub account
Replace the email in the following command and run it
````
ssh-keygen -t ed25519 -C "jakaza@gmail.com"
````

- Proceed with empty filename, just press ENTER
- Add a passphrase that is easy to remember, you will type it often
- The ~/.ssh folder is created
- Run the following to see it
```
la ~/.ssh
```
### Add the public SSH key to GitHub account

- Check the contents of the public key generated in the last step
- Make sure it is the file with the
```
cat ~/.ssh/id_ed25519.pub
```
- Copy the whole file content
- Go to GitHub account: Settings -> SSH and GPG keys -> New SSH key
- Title = wsl (or other)
- Key type = Authentication Key
- Key = paste what you have copied from the last step
- Add SSH key
- Enter your GitHub password if prompted
- The public SSH key has been added

#### Test SSH connection to GitHub
- Run the following
```
ssh -T git@github.com
```
