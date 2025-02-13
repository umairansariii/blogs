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
