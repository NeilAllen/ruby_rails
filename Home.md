rbenv is a tool for simple Ruby version management.

To install rbenv, please refer to the [Readme][install].

## Troubleshooting / FAQ

### How is this better than RVM?

See [[Why rbenv?]]

### How to verify that I have set up rbenv correctly?

1.  Check that `rbenv` is in your PATH:

        command which rbenv

2.  Check that rbenv's shims directory is in PATH:

    ```sh
    echo $PATH | grep --color=auto "$(rbenv root)/shims"
    ```

    If not, see the [`rbenv init` step][init] in installation instructions.

### Which shell startup file do I put rbenv config in?

Typically it's one of the following:

* bash: `~/.bash_profile`
* zsh: `~/.zshrc`
* other: `~/.profile`

With bash on Ubuntu, you probably already have a `~/.profile`. In that case you
should add rbenv config there instead of creating a `~/.bash_profile`. However,
since this file is read only once per desktop login, you may achieve quicker
results by adding rbenv to `~/.bashrc` instead.

See [[Unix shell initialization]] for more info about how config files get
loaded.

### Rubinius 2.0 in Ruby 1.9 mode

Rubinius in 1.9 mode uses a separate bin directory for executable binstubs. To
compensate for that, use the [rbx 2.0 dev fix plugin][rbx].


  [install]: https://github.com/sstephenson/rbenv#installation
  [init]: https://github.com/sstephenson/rbenv#basic-github-checkout
  [ruby-build]: https://github.com/sstephenson/ruby-build#readme
  [rbx]: https://github.com/collinschaafsma/rbenv-rbx_2.0.0-dev_fix#readme
