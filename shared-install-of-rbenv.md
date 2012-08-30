# Shared install of rbenv

A shared system-wide install of rbenv is possible, although it's still a somewhat experimental feature with some rough spots. rbenv is simple enough that it works pretty well, but there are some issues around file permissions in the shared install.  Some people are using this type of install on production/deployment servers too. 

The point of a shared install is to allow multiple unix accounts to use rbenv without each having to install different ruby versions (and usually gems) seperately. 

The RBENV_ROOT environmental variable is mainly what makes this setup possible. Use a recent version of rbenv to make sure it includes the RBENV_ROOT feature, and any fixes to how that feature works. 

## Install rbenv to /usr/local/rbenv

Or another location of your choice, but this one is what many have done. Instead of the rbenv install being at each user's `~/.rbenv`, there will be a single one at /usr/local/rbenv


(probably as sudo)

1. $ cd /usr/local
2. $ git clone git://github.com/sstephenson/rbenv.git rbenv
3. $ chgrp -R staff rbenv
4. $ chmod -R g+rwxXs rbenv

*Is setting the setgid bit here really a good idea? It seems safe but it cripples your Ruby pretty badly. For instance, I'm getting errors like "Insecure operation - exist?" when I try to do basically anything. Also, not EVERYTHING needs to be group-executable, just group-writable.* --@mcmire

## user environment for shared rbenv install

The additional RBENV_ROOT env variable needs to be added to the usual rbenv shell ENV setup for users who are to use it. 

In each user's `~/.profile`, `~/.bash_profile`, or `~/.zshenv` (depending on shell environment) (and/or optionally in the `/etc/skel/.profile`  or `/etc/skel/.bash_profile` etc, the template files for subsequently created accounts):

    export RBENV_ROOT=/usr/local/rbenv
    # these next are as usual for rbenv
    export PATH="$RBENV_ROOT/bin:$PATH"
    eval "$(rbenv init -)"

Alternately, you can use the no-shell-magic version, which might be better for accounts on production machines that won't be used for interactive shells. Again, this is just like any other rbenv except for the RBENV_ROOT. 

    export RBENV_ROOT=/usr/local/rbenv
    export PATH="$RBENV_ROOT/shims:$RBENV_ROOT/bin:$PATH"

Individual accounts on the machine can still 'opt out' and install and use account-specific rbenv installs simply by omitting the RBENV_ROOT for that account. 

## Optionally, install ruby-build as an rbenv plugin to this location

There are other ways to build ruby manually, but many find ruby-build convenient, it can be installed in this shared rbenv too, no problem. 

(probably as sudo)

1. mkdir /usr/local/rbenv/plugins
2. cd /usr/local/rbenv/plugins
3. git clone git://github.com/sstephenson/ruby-build.git
4. $ chgrp -R staff ruby-build
5. $ chmod -R g+rwxs ruby-build

## Use rbenv as normal

From an account that has the shell ENV set properly, you can use rbenv pretty much as normal, including using ruby-build as a plugin to install rubies. 

    $ rbenv install 1.9.3-p125
    $ rbenv rehash

Just like any rbenv install. One difference is that when you set the rbenv 'default' ruby, with eg `rbenv global 1.9.2-p125`, this global setting will apply to all users using this shared rbenv install, not just the current user. 

There's no way from the command line to set a default for just the current user. However, you can still use project-specific .rbenv directors, the RBENV_VERSION shell variable, or the `rbenv shell` command as ordinarily. A user could manually add an `export RBENV_VERSION=1.9.3-p125` to their .profile or other shell startup file to have their preferred ruby set for interactive shells on login. 

## <a name="permission-issues"></a>Note on permissions issues

This is the main not entirely solved pain point of this kind of shared rbenv install. 

The trick here is that we need everything in the `/usr/local/rbenv` to be *readable* and *executable* by any accounts that should be able to use the shared rbenv install; and *writeable* by any accounts that should be able to install new ruby versions, or install ruby gems to the system location. 

This is easy enough to set up on first install, with `chown` and `chgrp`. In the above instructions, the `chgrp -R staff` is meant with the idea that you have a `staff` group composed of everyone who should be able to use rbenv and install rubies and gems. 

However, it can be difficult to maintain when people install rubies or gems. If a certain user account installs a new ruby or even just a gem, it will usually end up with file ownership belonging to that user. You can wind up with a mishmash of ownership in that directory, which is messy. And files can end up not readable or writeable by everyone they should be, after ruby and gem installs.  In the instructions above, we tried setting the "setgid bit" in our chmod to ameliorate this, but experience shows that alone isn't really reliable. 

New rubies are installed relatively infrequently, so can maybe cleaned up manually after install. But gems are the real issue. 

Note however that on a server used only for production/deployment with modern bundler-based ruby apps, very few gems actually need to be installed in the system gem locations. You need `bundler`, and `passenger`, and possibly a few other things for the web/app server for nginx/thin/etc installs. But the contemporary standard deploy method of using `bundle install --deployment` on your production server will *not* install app-specific gems to the system location, they'll only be installed locally in the app's own directory. So this can ameliorate the problem. 

You could try to set up permissions such that only root can install new rubies and gems, but everyone can use them. (*Instructions from someone who has verified this?*)

Some have tried a shared install, letting each user account setup separate gem directories using the GEM_HOME and GEM path env variables.  BUT a problem arises: different rubies will store their gems in the same GEM_HOME directory - making this approach untenable.  An alternative approach is to use the [rbenv-usergems](https://github.com/andyl/rbenv-usergems) plugin.

## passenger

Just make sure your desired ruby is the current rbenv ruby (run `rbenv which` or `rbenv version` to see, as usual) when installing the passenger gem and running the passenger webserver install commands. That will then be the ruby passenger runs. 

It is not neccesary to set up the rbenv ENV variables in the `apache` account. It shouldn't be neccesary to set them up in the user account passenger will run apps under either (for bundler-based apps), although it doesn't hurt and can make debugging and troubleshooting less confusing to do so. 

## capistrano

You can tell capistrano to use the system-wide rbenv install very easily. In your deploy.rb:

    set :default_environment, {
      'RBENV_ROOT' => '/usr/local/rbenv',
      'PATH' => "/usr/local/rbenv/shims:/usr/local/rbenv/bin:$PATH"
    }

Cap will use now the system global/default rbenv ruby on each production machine. If you want to tell it to use a specific rbenv ruby when doing it's business, you could just include an `RBENV_VERSION` in there too.  You should probably even be able to have a project-specific `.rbenv` in your release source, and capistrano will end up using it as long as RBENV_ROOT and PATH are set appropriately -- but I find explicitly including an RBENV_VERSION to be more transparent. 

You can also tell capistrano to have bundler install it's 'binstubs' in such a way that they're pointing to the rbenv ruby specifically:

    set :bundle_flags, "--deployment --quiet --binstubs --shebang ruby-local-exec"

An account executing these binstubs would still need to have it's ENV variables set up for rbenv though. (Question: Since this is true, is the --shebang neccesary at all? If the account needs rbenv ENV set up anyway, it probably doesn't need the custom shebang? Try without it if you like and let us know)

## cronjob rake tasks

You want to run a rake task under a certain rb-env controlled ruby, in a cronjob?  The best way to run rake tasks in cronjobs in a bundler world is with bundler's binstubs (make sure you did bundle install with `--binstubs`). But you also need to make sure the rbenv ENV variables are set. 

If the cronjob is running under a user which has it's `.bash_profile` set up right to set rbenv ENV variables, here's one easy way:

* * * * * /bin/bash -l -c 'cd /path/to/app && ./bin/rake task'

(you may or may not have needed to generate bundler binstubs with `--shebang ruby-local-exec`, see above. 