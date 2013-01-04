### rbenv _does…_

* Provide support for specifying **application-specific Ruby versions**.
* Let you **change the global Ruby version** on a per-user basis.
* Allow you to **override the Ruby version** with an environment
  variable.

### In contrast with rvm, rbenv _does not…_

* **Need to be loaded into your shell.** Instead, rbenv's shim approach works by adding a directory to your `$PATH`.
* **Override shell commands like `cd` or require prompt hacks.** That's dangerous and error-prone.
* **Have a configuration file.** There's nothing to configure except which version of Ruby you want to use.
* **Install Ruby.** You can build and install Ruby yourself, or use [ruby-build](https://github.com/sstephenson/ruby-build) to automate the process.
* **Manage gemsets.** [Bundler](http://gembundler.com/) is a better way to manage application dependencies. If you have projects that are not yet using Bundler you can install the [rbenv-gemset](https://github.com/jamis/rbenv-gemset) plugin.
* **Require changes to Ruby libraries for compatibility.** The simplicity of rbenv means as long as it's in your `$PATH`, [nothing](https://rvm.io/integration/bundler/) [else](https://rvm.io/integration/capistrano/) needs to know about it.
* **Prompt you with warnings when you switch to a project.** Instead of executing arbitrary code, rbenv reads just the version name from each project. There's nothing to "trust."
