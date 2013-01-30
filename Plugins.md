See [[Authoring plugins]] for instructions on how to write new commands for
rbenv or hook into its functionality.

A plugin can be installed by dropping it in as a sub-directory of
`$RBENV_ROOT/plugins`, or it can be located elsewhere on the system as long as
`rbenv-*` executables are placed in the `$PATH` and hooks are installed
accordingly somewhere in `$RBENV_HOOK_PATH`.

## Approved plugins

This list is edited by rbenv maintainers.

* [ruby-build](https://github.com/sstephenson/ruby-build) - compile and install Ruby
* [vars](https://github.com/sstephenson/rbenv-vars) - safely sets global and
  per-project environment variables
* [gem-rehash](https://github.com/sstephenson/rbenv-gem-rehash) - Automatically run
  `rbenv rehash` every time you install a new gem
* [default-gems](https://github.com/sstephenson/rbenv-default-gems) - Automatically
  install gems every time you install a new version of Ruby
* [each](https://github.com/chriseppstein/rbenv-each) - execute the same command
  with each installed Ruby
* [gemset](https://github.com/jamis/rbenv-gemset) - basic gemset support
* [rbx_2.0.0-dev_fix](https://github.com/collinschaafsma/rbenv-rbx_2.0.0-dev_fix)
  rbenv plugin that fixes up your shims and sets `RBENV_COMMAND_PATH`
  properly for rbx-2.0.0-dev in 1.9 mode 
* [update](https://github.com/rkh/rbenv-update) - update rbenv and installed
  plugins
* [use](https://github.com/rkh/rbenv-use) - rvm-style use command
* [whatis](https://github.com/rkh/rbenv-whatis) - resolving abbreviations to
  full Ruby identifiers (useful for other plugins)

## Bundler integration

There is a [rbenv-bundler](https://github.com/carsomyr/rbenv-bundler) which
adjusts rbenv shims and `rbenv which` command with respect to the current
project's bundle. However, **its usage is not recommended** because of slow
performance and over-engineered state.

If you want to free yourself from having to always write `bundle exec <command>`
in a project, first generate Bundler's binstubs:

    bundle install --binstubs

See [[Understanding binstubs]] for more info.

## Other plugins (alpha-order)

Please add new plugins here. They might get promoted to the above list by rbenv
maintainers.

* [env](https://github.com/ianheggie/rbenv-env) - Adds rbenv env command to show relevant environment variables
* [man](https://github.com/mlafeldt/rbenv-man) - easily access man pages for
  current Ruby version
* [only](https://github.com/Rodreegez/rbenv-only) - execute the same command for
  specified rubies
* [path](https://github.com/taqtiqa/rbenv-path) - manage contents of PATH (likely of interest to plugin writers)
* [plugin](https://github.com/taqtiqa/rbenv-plugin) - manage rbenv plugins
* [sudo](https://github.com/dcarley/rbenv-sudo) - run rbenv-provided rubies and
  gems from within a sudo session
* [usergems](https://github.com/andyl/rbenv-usergems) - store gems and shims in
  `~/.rbenv-usergems`