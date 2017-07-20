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
