# FAQ

## I installed gem &lt;xxx&gt; with a "bundle install" but after running "rbenv rehash" the &lt;xxx&gt; executable is not found.

Bundler does not create an executable in your path, by default you will need to use `bundle exec` to run your command (and that is a good habit anyway), if later you want to use this executable outside your current application you will need to reinstall it with a `gem install <xxx>` followed by a `rbenv rehash`.

## rbenv: command not found on Linux

This happens because ~/.bash_profile is read only at login. You would need to configure your ~/.bashrc file (If you don't have one, create one), which is read every time a shell is started. Put this in your ~/.bashrc

    if [ -n "$PS1" ]; then
      [ -f ~/.bash_profile ] && source ~/.bash_profile
    fi

