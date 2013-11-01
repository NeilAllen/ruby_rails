Setting up rbenv on a production server is exactly the same as in development.
Some considerations for a hypothetical deployment strategy:

* It is suggested that there is a single user for deployment, e.g. "app" user
* `RBENV_ROOT` is at the default location: `~app/.rbenv`
* Ruby versions are either installed or symlinked to `~app/.rbenv/versions`
* rbenv version 0.4 or greater is recommended.

Users of Chef or Puppet may find these projects useful:

* [chef-rbenv][], [chef-ruby_build][]
* [puppet-rbenv][]

## Ensure consistent PATH for processes

Interactive, non-interactive shells, cron jobs, and similar processes for the
"app" user all must ensure that rbenv is present in the PATH:

    export PATH=~/.rbenv/shims:~/.rbenv/bin:"$PATH"

## App bundles and binstubs

The recommended way of using Bundler in production is like so:

    bundle install --deployment --binstubs

The `--binstubs` option generates executables in your application's `./bin`
directory for gems in the bundle.
[[Read more about binstubs|Understanding binstubs]].

Now tools that interact with the app should strictly use the executables in
`./bin`. For instance, to invoke Unicorn:

    /u/apps/myapp/current/bin/unicorn

Such invocation ensures that:

1. The Ruby version for the project is used,
2. The Unicorn version of the project's bundle is used.


  [chef-ruby_build]: https://github.com/fnichol/chef-ruby_build#readme
  [chef-rbenv]: https://github.com/fnichol/chef-rbenv#readme
  [puppet-rbenv]: https://github.com/alup/puppet-rbenv#readme
