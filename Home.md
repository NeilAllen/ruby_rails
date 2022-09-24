rbenv is a tool for simple Ruby version management.

To install rbenv, please refer to the [Readme][install].

## Troubleshooting / FAQ

### How to verify that I have set up rbenv correctly?

1.  Check that `rbenv` is in your PATH:

    ```sh
    which -a rbenv
    ```

2.  Check that rbenv shims directory is in PATH:

    ```sh
    echo $PATH | grep --color=auto "$(rbenv root)/shims"
    ```

    If not, see the [`rbenv init` step][init] in installation instructions.

### What is allowed in a `.ruby-version` file?

The string read from a `.ruby-version` file must match the name of an existing
directory in `~/.rbenv/versions/`. You can see the list of installed Ruby
versions with `rbenv versions`.

Other version managers might allow fuzzy version matching on the string read from `.ruby-version` file, e.g. they might allow "3.1" to activate the latest Ruby 3.1.x release. **rbenv will not support this** since such behavior is non-deterministic and therefore considered harmful.

### “You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory”

This error can happen on a fresh installation where no Ruby version was configured yet as "global":
```
$ gem install bundler
ERROR: While executing gem ... (Gem::FilePermissionError)
You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory.
```
It's likely that rbenv is still set to use the "system" Ruby, which is the default:
```
$ rbenv versions
* system
```
With the system Ruby, the `gem install` operation will try to write into system directories which usually aren't user-writeable, and the user will get a permissions error.

The way to solve this is to install a Ruby version with rbenv (typically via `rbenv install`) and then **select that Ruby version as a "global" version**:
```
rbenv install 3.1.2
rbenv global 3.1.2
```
As long as you move away from "system", you should have no permission restrictions while installing gems because other Ruby versions under rbenv are user-writeable.

### rbenv is installed but things just aren't working for me!

The [rbenv-doctor script](https://github.com/rbenv/rbenv-installer#readme) analyzes your system setup for common problems. It's likely that you just missed a required installation step or have mis-configured your shell startup files.

### Which shell startup file do I put rbenv config in?

Typically it's one of the following:

* bash: `~/.bash_profile` (or `~/.bashrc` on Ubuntu Desktop)
* zsh: `~/.zshrc`
* fish: `~/.config/fish/config.fish`
* other: `~/.profile`

See [[Unix shell initialization]] for more info about how config files get
loaded.


  [install]: https://github.com/rbenv/rbenv#installation
  [init]: https://github.com/rbenv/rbenv#basic-git-checkout
