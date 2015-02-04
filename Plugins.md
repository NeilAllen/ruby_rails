See [[Authoring plugins]] for instructions on how to write new commands for
rbenv or hook into its functionality.

A plugin can be installed by dropping it in as a sub-directory of
`$RBENV_ROOT/plugins`, or it can be located elsewhere on the system as long as
`rbenv-*` executables are placed in the `$PATH` and hooks are installed
accordingly somewhere in `$RBENV_HOOK_PATH`.

## Approved plugins

This list is edited by rbenv maintainers.

* [ruby-build](https://github.com/sstephenson/ruby-build) - compile and **install Ruby**
* [ctags](https://github.com/tpope/rbenv-ctags) - automatically **generate ctags** for rbenv Ruby stdlibs
* [vars](https://github.com/sstephenson/rbenv-vars) - safely sets global and
  per-project **environment variables**
* [each](https://github.com/chriseppstein/rbenv-each) - execute the same command
  **with each** installed Ruby
* [update](https://github.com/rkh/rbenv-update) - **update rbenv** and installed
  plugins
* [use](https://github.com/rkh/rbenv-use) - **RVM-style** `use` command
* [whatis](https://github.com/rkh/rbenv-whatis) - **resolve abbreviations** to
  full Ruby identifiers (useful for other plugins)
* [aliases](https://github.com/tpope/rbenv-aliases) - **create aliases** for Ruby versions

RubyGems-related plugins:

* [gem-rehash](https://github.com/sstephenson/rbenv-gem-rehash) - **automatically run**
  `rbenv rehash` every time you install a new gem
* [default-gems](https://github.com/sstephenson/rbenv-default-gems) - **automatically
  install** specific gems after installing a new Ruby
* [communal-gems](https://github.com/tpope/rbenv-communal-gems) - **share gems** across multiple Ruby installs
* [user-gems](https://github.com/mislav/rbenv-user-gems) - **discover gems** installed under `~/.gem` or a custom `$GEM_HOME`
* [gemset](https://github.com/jf/rbenv-gemset) - basic **gemset support**

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

* [around-install](https://github.com/toy/rbenv-around-install) - run scripts before and after `rbenv install` (externalised ruby-build hooks)
* [bundle-exec](https://github.com/maljub01/rbenv-bundle-exec) - Runs commands using `bundle exec` when invoked from a bundler-managed directory
* [bundler-ruby-version](https://github.com/aripollak/rbenv-bundler-ruby-version) - picks a ruby version from Gemfile
* [ccache](https://github.com/yyuu/rbenv-ccache) - Make Ruby build faster, with using the leverage of `ccache`.
* [chefdk](https://github.com/docwhat/rbenv-chefdk) - Use [ChefDK](https://downloads.chef.io/chef-dk/) as if it where just another rbenv version.
* [env](https://github.com/ianheggie/rbenv-env) - Adds rbenv env command to show relevant environment variables
* [gem-update](https://github.com/nicknovitski/rbenv-gem-update) - automatically run `gem update --system` on `rbenv install`
* [gemdir](https://github.com/bachue/rbenv-gemdir) - Return the gem directory of the currently selected ruby
* [git](https://github.com/znz/rbenv-git) - `rbenv git` command to run `git` in directories of rbenv and all installed plugins
* [install-remote](https://github.com/fgrehm/rbenv-install-remote) - support for installing rubies using a custom definition defined remotely (like a gist)
* [jruby-mode](https://github.com/toy/rbenv-jruby-mode) - run jruby in different mode (1.8, 2.0) by adding suffix to version
* [man](https://github.com/mlafeldt/rbenv-man) - easily access man pages for
  current Ruby version
* [only](https://github.com/Rodreegez/rbenv-only) - execute the same command for
  specified rubies
* [path](https://github.com/taqtiqa/rbenv-path) - manage contents of `$PATH`
  (likely of interest to plugin writers)
* [plug](https://github.com/znz/rbenv-plug) - easiest rbenv plugin installer
* [plugin](https://github.com/taqtiqa/rbenv-plugin) - manage rbenv plugins
* [pluger](https://github.com/cao7113/rbenv-pluger) - rbenv plugin manager and booter
* [rails](https://github.com/alfa-jpn/rbenv-rails) - create rails project with the version.
* [readline](https://github.com/tpope/rbenv-readline) - Automatically link rbenv Ruby installs to readline on OS X
* [rbenv-clean](https://github.com/sableloki/rbenv-clean) - `gem clean` for rbenv
* [rvm-download](https://github.com/garnieretienne/rvm-download) - Download ruby binaries from RVM repository
* [sentience](https://github.com/tpope/rbenv-sentience) - Make rbenv self-aware - creates a `.ruby-version` file inside the root of the installation directory
* [sudo](https://github.com/dcarley/rbenv-sudo) - run rbenv-provided rubies and
  gems from within a sudo session
* [update-rubies](https://github.com/toy/rbenv-update-rubies) - install updated ruby versions (`1.9.3-p547` => `1.9.3-p550`, `2.1.0` => `2.1.4`)
* [usergems](https://github.com/andyl/rbenv-usergems) - store gems and shims in
  `~/.rbenv-usergems`