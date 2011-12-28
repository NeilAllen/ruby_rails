## Method 1: Installing everything into a deploy user

**Note:** Before installing anything make sure your server has `git` installed.

Run `rbenv-installer`:

    curl -L https://raw.github.com/fesplugas/rbenv-installer/master/bin/rbenv-installer | bash

Once it has been downloaded run add to your load path `rbenv`:

```
if [[ -d $HOME/.rbenv ]]; then
  export PATH="$HOME/.rbenv/bin:$PATH"
  eval "$(rbenv init - --no-rehash)"
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

### Deploying

If you are using `bundler` there's nothing you need to change on your deployment strategy as long as you run always your commands with `bundle exec`.