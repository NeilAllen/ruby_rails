The key strengths of rbenv are:

- **Transparent:** rbenv gets out of your way while you work. Install some Ruby versions, select the one you need, and you don't need to interact with rbenv anymore. Other tools that invoke Ruby on the same system don't even need to know that rbenv exists, [[as long as it's in PATH|How to edit PATH]].

- **Extensible:** rbenv does only the bare minimum and the rest it leaves up to its [[plugin ecosystem|Plugins]].

- **Portable:** rbenv works in any shell on every Unix-like system. Its only dependency is the bash interpreter, which comes standard with basically every system.

But, its mechanism also has some downsides:

- **Slow:** since rbenv intercepts every call to `ruby`, it can add an overhead of ~50ms to ruby execution time. This shouldn't be noticeable with most usages of Ruby, but can cause friction in times when speed is imperative.

- **Strict:** due to rbenv's strict version isolation between projects, [some users found it challenging](https://github.com/rbenv/rbenv/issues/187) to keep some “global” (system-level) Ruby tooling and invoke it from within their projects. Similarly, other users had discovered that they [can't trivially “shell out”](https://github.com/rbenv/rbenv/issues/121) from a project that uses one Ruby version to a script that uses another Ruby version.

- **Known limitation:** rbenv [cannot discover executables](https://github.com/rbenv/rbenv/pull/1436) of `--user-install`ed gems in some contexts, most notably when the currently active Ruby version is "system".

What follows is a short overview of some other Ruby version managers.

## chruby

[chruby][] is a minimal Ruby version manager that hooks into your shell.

It has no overhead on `ruby` execution time because it does the switching either on-demand or, optionally, whenever you `cd` into a project directory. Additionally, it offers robust support for running executables of `--user-install`ed gems.

Its downsides are that it is only available in bash and zsh shells, and that other tools that invoke Ruby need to either load a login shell to gain access to version-switching, or need to explicitly invoke `chruby-exec`.

## direnv

[direnv][] is a general-purpose tool for loading & unloading project-specific environment variables when you change directories in your shell. Even though it's not specifically designed to be a version manager, it can be easily used to modify the PATH environment variable (among others) in a way that [activates a specific Ruby version](https://direnv.net/docs/ruby.html) for each project.

This approach has basically the speed of chruby (there is no ruby execution overhead) and the functionality of [rbenv-vars][].

The downside is that the usage guide linked above requires some manual setup and does not support `.ruby-version` files out of the box.

## asdf

[asdf][] works like rbenv, but is able to manage not just Ruby versions, but also Node.js, Python, and many more via its plugin architecture. It's suitable for machines when you need to switch between many versions of different languages, but don't want to use a separate version manager for each language.

It's downside is that it's likely [slower than rbenv](http://stratus3d.com/blog/2022/08/11/asdf-performance/).

## frum

[frum][] is a pure Rust implementation that is an order of magnitude faster than rbenv.

The downside is that it doesn't support all rbenv features; for example, there seems to be no extensibility with plugins.

## RVM

RVM is the original version manager that rbenv was created to be an alternative to. RVM might seem user-friendly at first, but it's hard to grok how it works and, historically, it has left users in a state where they don't understand why their Ruby program breaks in a certain way, or how to fix it. Other than for the ease of installing Ruby versions in certain situations, I am not sure what the benefits of RVM are and I can't recommend its use.


  [chruby]: https://github.com/postmodern/chruby
  [direnv]: https://direnv.net/
  [rbenv-vars]: https://github.com/rbenv/rbenv-vars
  [asdf]: https://github.com/asdf-vm/asdf
  [frum]: https://github.com/TaKO8Ki/frum
