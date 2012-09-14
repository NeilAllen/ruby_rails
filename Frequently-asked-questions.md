# FAQ

## I installed gem &lt;xxx&gt; with a "bundle install" but after running "rbenv rehash" the &lt;xxx&gt; executable is not found.

Bundler does not create an executable in your path, by default you will need to use `bundle exec` to run your command (and that is a good habit anyway), if later you want to use this executable outside your current application you will need to reinstall it with a `gem install <xxx>` followed by a `rbenv rehash`.

## rbenv: command not found on Linux

This happens because ~/.bash_profile is read only at login. You would need to configure your ~/.bashrc file (If you don't have one, create one), which is read every time a shell is started. Put this in your ~/.bashrc

    if [ -n "$PS1" ]; then
      [ -f ~/.bash_profile ] && source ~/.bash_profile
    fi

## cronjobs and whenever

Gems are not available in cron unless you source .bashrc or .zshrc to load the environment paths.

If using [whenever](https://github.com/javan/whenever), one solution is to create a custom job_type:

    job_type :rbenv_gem, "/bin/zsh -c 'source ~/.zshrc && bundle exec :task'"
    every 1.day, :at => '5:00 am' do
      rbenv_gem 'backup perform --trigger appbackup --config_file /www/app/config/backup.rb"'
    end

The above will generate:

    /bin/zsh -c 'source ~/.zshrc && bundle exec backup perform --trigger appbackup --config_file "/www/app/config/backup.rb"'

## How to install Ruby with rbenv on Ubuntu 12.04

See: http://www.stehem.net/2012/05/08/how-to-install-ruby-with-rbenv-on-ubuntu-12-04.html