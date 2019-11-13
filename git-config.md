### Your Identity
The first thing you should do when you install Git is to set your user name and email address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you start creating:
```git
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```
### Git Pull
By default, `git pull` first runs `git fetch` that downloads content from the specified remote repository, then a `git merge` is executed that merges the remote content refs and heads into a new local merge commit.

We want to change this, so that by default `git pull` runs `git fetch` followed by `git rebase`, instead of `git merge`. A must read on [git rebase](https://git-scm.com/book/en/v2/Git-Branching-Rebasing).
```git
git config --global pull.rebase true
```

### Git Config Levels and Files
The order of priority for configuration levels is: local, global, system. This means when looking for a configuration value, Git will start at the local level and bubble up to the system level.
- --local\
  By default, `git config` will write to a local level if no configuration option is passed. Local level configuration is applied to the context repository `git config` gets invoked in. Local configuration values are stored in a file that can be found in the **repo's .git directory**: `.git/config`
- --global\
  Global level configuration is user-specific, meaning it is applied to an operating system user. Global configuration values are stored in a file that is located in a user's home directory. `~/.gitconfig` on unix systems and `C:\Users\<username>\.gitconfig` on windows
- --system\
  System-level configuration is applied across an entire machine. This covers all users on an operating system and all repos. The system level configuration file lives in a `gitconfig` file off the system root path. `$(prefix)/etc/gitconfig` on unix systems. On windows this file can be found at `C:\Documents and Settings\All Users\Application Data\Git\config` on Windows XP, and in `C:\ProgramData\Git\config` on Windows Vista and newer.