Setting up rbenv on a production server is exactly the same as in development.
Some considerations for a hypothetical deployment strategy:

* It is suggested that there is a single user for deployment, e.g. an "app" user.
* `RBENV_ROOT` is at the default location: `~app/.rbenv`.
* Ruby versions are either installed under or symlinked to `~app/.rbenv/versions`.

Chef and Puppet users may find these projects useful:

* [chef-rbenv][], [chef-ruby_build][]
* [puppet-rbenv][]

## Ensure consistent PATH for processes

Interactive and non-interactive shells, cron jobs, and similar processes for the
"app" user all must ensure that [[rbenv shims are prepended to PATH|How to edit path]]:

    export PATH=~/.rbenv/shims:"$PATH"

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
2. The Unicorn version in the project's bundle is used.

## Containers and rbenv

Applications deployed via a containerized architecture (e.g. Docker) should generally **not use rbenv**.

Originally, rbenv was designed to achieve isolation between projects running on the same host system. Containerized runtimes are a more sophisticated mechanism for isolation and thus do not benefit from rbenv. Instead, just base the container for your Ruby-based app on one of the publicly available [base images for Ruby](https://hub.docker.com/_/ruby).

The bottom line is: if you see rbenv used in a Dockerfile, they blew it.


  [chef-ruby_build]: https://github.com/fnichol/chef-ruby_build#readme
  [chef-rbenv]: https://github.com/fnichol/chef-rbenv#readme
  [puppet-rbenv]: https://github.com/alup/puppet-rbenv#readme
