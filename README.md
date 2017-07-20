# gitconfig.d
RefWorks specific git configuration files.

## Setup
Clone this directory to ~/.gitconfig.d
```bash
git clone git@github.com:proquest/gitconfig.d.git ~/.gitconfig.d
```

Include the aliases in your existing .gitconfig file
```bash
[include]
  path = .gitconfig.d/release-aliases 
  path = .gitconfig.d/general-aliases
```

It should look something like this:
```
# This is Git's per-user configuration file.
[user]
# Please adapt and uncomment the following lines:
  name = Michael Nishizawa
  email = michael.nishizawa@proquest.com

[include]
  path = .gitconfig.d/release-aliases
  path = .gitconfig.d/general-aliases
```

To validate that your setup is correct, the following command should show you the aliases that are recognized:
```
git config --get-regexp alias
```
