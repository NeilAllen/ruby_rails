## Approved plugins

This list is edited by rbenv maintainers.

* [each](https://github.com/chriseppstein/rbenv-each) - execute the same command
  with each installed Ruby
* [gemset](https://github.com/jamis/rbenv-gemset) - basic gemset support
* [vars](https://github.com/sstephenson/rbenv-vars) - safely sets global and
  per-project environment variables
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
performance and overengineered state.

If you want to free yourself from having to always write `bundle exec <command>`
in a project, first generate Bundler's binstubs:

    bundle install --binstubs

Then add `./bin` to your PATH.

## Other plugins

Please add new plugins here. They might get promoted to the above list by rbenv
maintainers.

* [only](https://github.com/Rodreegez/rbenv-only) - execute the same command for
  specified rubies
* [man](https://github.com/mlafeldt/rbenv-man) - easily access man pages for
  current Ruby version
* [sudo](https://github.com/dcarley/rbenv-sudo) - run rbenv-provided rubies and
  gems from within a sudo session
* [usergems](https://github.com/andyl/rbenv-usergems) - store gems and shims in
  `~/.rbenv-usergems`
