* [Method 1](#method1) Installing everything into a deploy user.
* [Method 2](#method2) Bootstrap Ruby+Chef into user root and use Chef cookbooks thereafter.
* Method 3 Use a [[Shared Install of rbenv]] (link to seperate wiki page)

## <a name="method1"></a>Method 1: Installing everything into a deploy user

**Note:** Before installing anything make sure your server has `git` installed.

Run `rbenv-installer`:

    curl -L https://raw.github.com/fesplugas/rbenv-installer/master/bin/rbenv-installer | bash

Once it has been downloaded run add to your load path `rbenv`:

```
if [[ -d $HOME/.rbenv ]]; then
  export PATH="$HOME/.rbenv/bin:$PATH"
  eval "$(rbenv init -)"
fi
```

The `rbenv-installer` will install `rbenv` and the following plugins:

- rbenv-vars
- ruby-build
- rbenv-installer

### Install Rubies

Make sure you have the required packages installed. If you are in `Ubuntu 10.04 LTS` or `Ubuntu 11.10` you can use the bootstrap scripts provided by `rbenv-installer`:

    rbenv bootstrap-ubuntu-10-04

Once the packages have been installed you can install the desired `rubies`:

    rbenv install 1.9.3-p0

And make them global:

    rbenv global 1.9.3-p0

Now all your applications will use this Ruby version unless they have a `.rbenv-version` file on the root of the project.

## <a name="method2"></a>Method 2: Chef managed system-wide and user installs of rbenv+rubies

To avoid hand-rolled ruby installations and distro-packaged ruby installations, but rather
manage rbenv user and system-wide installs using Chef-Solo and fnichol's [ruby_build] and [rbenv]
cookbooks, bootstrap an initial ruby (1.9.2-p290) + chef + bundler install:

    curl -L https://raw.github.com/hedgehog/rbenv-installer/sysinstall/bin/rbenv-bootstrap-chef-solo | sudo -i bash

After this your production installations of ruby can be managed by Chef/Chef-Solo and cookbooks.
Example: install a different Ruby system-wide and then remove this bootstrapped version :)

### Deploying

If you are using `bundler` there's nothing you need to change on your deployment strategy as long as you run always your commands with `bundle exec`.

## Guides

- [Using Rbenv To Manage Rubies](http://shapeshed.com/using-rbenv-to-manage-rubies/)

[ruby_build]: https://github.com/fnichol/chef-ruby_build
[rbenv]: https://github.com/fnichol/chef-rbenv