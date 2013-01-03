Shell initialization files are ways to persist common shell configuration, such
as:

* `$PATH` and other environment variables
* shell prompt
* shell tab-completion
* aliases, functions
* key bindings


## Shell modes

Which initializtion files get sourced by the shell is dependent on the
combination of modes in which a particular shell process runs. There are two
main, non-exclusive modes:

* **login** - e.g. when user logs in to a system with non-graphical interface or
  via SSH;
* **interactive** - shell that has a prompt and whose standard input and error
  are both connected to terminals.

These modes can be manually activated with the following flags to bash/zsh:

* `-l`, `--login`
* `-i`

Here are some common operations and shell modes they result in:

* log in to a remote system via SSH:
  **login + interactive**
* execute a script remotely, e.g. `ssh user@host 'echo $PWD'`:
  **non-login,&nbsp;interactive**
* start a new shell process, e.g. `bash`:
  **non-login, interactive**
* run a script, `bash myscript.sh`:
  **non-login, non-interactive**
* run an executable with `#!/usr/bin/env bash` shebang:
  **non-login, non-interactive**
* open a new graphical terminal window/tab:
  * on Mac OS X: **login, interactive**
  * on Linux: **non-login, interactive**


## Shell init files

In order of activation:

### bash

1. **login** mode:
   1. `/etc/profile`
   2. `~/.bash_profile`, `~/.bash_login`, `~/.profile` (only first one that exists)
2. interactive **non-login**:
   1. `/etc/bash.bashrc` (some Linux; not on Mac OS X)
   2. `~/.bashrc`

### zsh

1. `/etc/zshenv`
2. `~/.zshenv`
3. **login** mode:
   1. `/etc/zprofile`
   2. `~/.zprofile`
4. **interactive**:
   1. `/etc/zshrc`
   2. `~/.zshrc`
5. **login** mode:
   1. `/etc/zlogin`
   2. `~/.zlogin`

### Practical guide to which files get sourced when

* Opening a new Terminal window/tab:
  * **bash**
     * OS X: `.bash_profile` or `.profile` (1st found)
     * Linux: `.profile` (Ubuntu, once per desktop login session) + `.bashrc`
  * **zsh**
     * OS X: `.zshenv` + `.zprofile` + `.zshrc`
     * Linux: `.profile` (Ubuntu, once per desktop login session) + `.zshenv` + `.zshrc`
* Logging into a system via SSH:
  * **bash**: `.bash_profile` or `.profile` (1st found)
  * **zsh**: `.zshenv` + `.zprofile` + `.zshrc`
* Executing a command remotely with `ssh`:
  * **bash**: `.bashrc`
  * **zsh**: `.zshenv` + `.zshrc`

## Misc. things that affect `$PATH`

* OS X:
  * [`~/.MacOSX/environment.plist`][plist] - affects **all** graphical programs
  * `/etc/launchd.conf`
  * `/etc/paths`, `/etc/paths.d/*`
* Linux:
  * `/etc/environment`

## Final notes

This guide was tested with:

* bash 4.2.37, 4.2.39
* zsh  4.3.11, 5.0

On these operating systems/apps:

* Mac OS X 10.8 (Mountain Lion): Terminal.app, iTerm2
* Ubuntu 12.10: Terminal

See also:

* [Environment Variables](https://help.ubuntu.com/community/EnvironmentVariables)
* path_helper(8)
* launchd.conf(5)
* pam_env(8)


  [plist]:
  http://developer.apple.com/library/mac/#documentation/MacOSX/Conceptual/BPRuntimeConfig/Articles/EnvironmentVars.html#//apple_ref/doc/uid/20002093-113982