# Multiple Git Accounts Using SSH

### List SSH keys
List all existing or previously generated SSH keys.
```bash
ls -l ~/.ssh
```
- Private keys typically have no extension (`id_rsa`, `id_ed25519`).
- Public keys have a `.pub` extension (`id_rsa.pub`, `id_ed25519.pub`).

### List from SSH Agent
List all currently loaded keys from SSH agent.
```bash
ssh-add -l
```
- If you see this error `Could not open a connection to your authentication agent.`

It typically means the SSH agent is not running, run this command to launch SSH agent.
```bash
eval $(ssh-agent)
```
### Delete from SSH Agent
Remove all keys from SSH agent.
```bash
ssh-add -D
```
Remove a specific key from SSH agent.
```bash
ssh-add -d ~/.ssh/id_ed25519
```
### Delete SSH keys
Permanently delete SSH keys from your local machine.
```bash
rm ~/.ssh/id_ed25519
rm ~/.ssh/id_ed25519.pub
```
### Generate SSH keys
Generate new SSH keys for each account like `personal` or `work`.
```bash
cd ~/.ssh
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- When prompted for the file name, specify a unique name `id_ed25519_personal`.
- Set passphrase for SSH key for an extra layer of security.

### Add SSH keys
Start the SSH agent and add your key files.
```bash
eval $(ssh-agent)
ssh-add ~/.ssh/id_ed25519_personal
ssh-add ~/.ssh/id_ed25519_work
```
### Add SSH keys to GitHub
Copy the public keys and add them to the corresponding Git accounts.
```bash
cat ~/.ssh/id_ed25519_personal.pub
cat ~/.ssh/id_ed25519_work.pub
```
- Go to GitHub → Settings → SSH and GPG keys → New SSH key and add the keys.

### Configure SSH config
Update the SSH config file located at `~/.ssh/config`, if it doesn't exist, create it.
```bash
touch ~/.ssh/config
code ~/.ssh/config
```
Add configuration for each host.
```plain
# Personal GitHub Account
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal
    AddKeysToAgent yes
    IdentitiesOnly yes

# Work GitHub Account
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work
    AddKeysToAgent yes
    IdentitiesOnly yes
```
### Test SSH connection
Test the SSH connection using custom aliases.
```bash
ssh -T git@github-personal
ssh -T git@github-work
```
- If configured correctly, you should see `Hi username! You've successfully authenticated`.

### Setup Git remotes
You can now use the aliases when cloning repositories.
```bash
git clone git@github-personal:username/repo-name.git
```
Or update existing remotes.
```bash
git remote set-url origin git@github-work:username/repo-name.git
```
