See [[Authoring plugins]] for instructions on how to write new commands for
rbenv or hook into its functionality.

A plugin can be installed by dropping it in as a sub-directory of
`$RBENV_ROOT/plugins`, or it can be located elsewhere on the system as long as
`rbenv-*` executables are placed in the `$PATH` and hooks are installed
accordingly somewhere in `$RBENV_HOOK_PATH`.

## Approved plugins

This list is edited by rbenv maintainers.

* [ruby-build](https://github.com/sstephenson/ruby-build) - compile and install Ruby
* [ctags](https://github.com/tpope/rbenv-ctags) - automatically generate ctags for rbenv Ruby stdlibs
* [vars](https://github.com/sstephenson/rbenv-vars) - safely sets global and
  per-project environment variables
* [gem-rehash](https://github.com/sstephenson/rbenv-gem-rehash) - Automatically run
  `rbenv rehash` every time you install a new gem
* [default-gems](https://github.com/sstephenson/rbenv-default-gems) - automatically
  install gems every time you install a new version of Ruby
* [communal-gems](https://github.com/tpope/rbenv-communal-gems) - share gems across multiple Ruby installs
* [each](https://github.com/chriseppstein/rbenv-each) - execute the same command
  with each installed Ruby
* [gemset](https://github.com/jf/rbenv-gemset) - basic gemset support
* [update](https://github.com/rkh/rbenv-update) - update rbenv and installed
  plugins
* [use](https://github.com/rkh/rbenv-use) - rvm-style use command
* [whatis](https://github.com/rkh/rbenv-whatis) - resolving abbreviations to
  full Ruby identifiers (useful for other plugins)
* [aliases](https://github.com/tpope/rbenv-aliases) - Create aliases for rbenv Ruby versions

## Bundler integration

There is [rbenv-bundler](https://github.com/carsomyr/rbenv-bundler) which
adjusts rbenv's shims and `rbenv which` command with respect to the current
project's bundle. However,
[its usage is not recommended](https://github.com/carsomyr/rbenv-bundler/issues/32)
because of poor performance and being bug-ridden.

If you want to free yourself from having to always write `bundle exec <command>`
in a project, you can generate Bundler's binstubs:

    bundle install --binstubs

Now you can run `bin/rake` instead of `bundle exec rake`.

If you want to be able to just type `rake`, you have two options from here:

1. You can add `./bin` to your `$PATH`. See [[Understanding binstubs]] for more info.
2. You can install the [rbenv-binstubs](https://github.com/ianheggie/rbenv-binstubs#readme) plugin and run `rbenv rehash` from your project.

## Other plugins (alpha-order)

Please add new plugins here. They might get promoted to the above list by rbenv
maintainers.

* [bundle-exec](https://github.com/maljub01/rbenv-bundle-exec) - Runs commands using `bundle exec` when invoked from a bundler-managed directory
* [bundler-ruby-version](https://github.com/aripollak/rbenv-bundler-ruby-version) - picks a ruby version from Gemfile
* [env](https://github.com/ianheggie/rbenv-env) - Adds rbenv env command to show relevant environment variables
* [git](https://github.com/znz/rbenv-git) - `rbenv git` command to run `git` in directories of rbenv and all installed plugins
* [install-remote](https://github.com/fgrehm/rbenv-install-remote) - support for installing rubies using a custom definition defined remotely (like a gist)
* [man](https://github.com/mlafeldt/rbenv-man) - easily access man pages for
  current Ruby version
* [only](https://github.com/Rodreegez/rbenv-only) - execute the same command for
  specified rubies
* [path](https://github.com/taqtiqa/rbenv-path) - manage contents of `$PATH`
  (likely of interest to plugin writers)
* [plug](https://github.com/znz/rbenv-plug) - easiest rbenv plugin installer
* [plugin](https://github.com/taqtiqa/rbenv-plugin) - manage rbenv plugins
* [rails](https://github.com/alfa-jpn/rbenv-rails) - create rails project with the version.
* [readline](https://github.com/tpope/rbenv-readline) - Automatically link rbenv Ruby installs to readline on OS X
* [sentience](https://github.com/tpope/rbenv-sentience) - Make rbenv self-aware - creates a `.ruby-version` file inside the root of the installation directory
* [sudo](https://github.com/dcarley/rbenv-sudo) - run rbenv-provided rubies and
  gems from within a sudo session
* [usergems](https://github.com/andyl/rbenv-usergems) - store gems and shims in
  `~/.rbenv-usergems`