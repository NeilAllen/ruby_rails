If bash is installed, adding rbenv to your `PATH` is all that's necessary for rbenv's shims to work in fish.

    set PATH $HOME/.rbenv/bin $PATH
    set PATH $HOME/.rbenv/shims $PATH
    rbenv rehash >/dev/null ^&1

Patches that add fish compatibility to `rbenv init` so that you don't need to manually construct the paths will be accepted.