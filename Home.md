rbenv is a tool for simple Ruby version management.

To install rbenv, please refer to the [Readme][install].

## Troubleshooting / FAQ

### How is this better than RVM?

See [[Why rbenv?]]

### What is allowed in a `.ruby-version` file?

The string read from a `.ruby-version` file must match the name of an existing
directory in `~/.rbenv/versions/`. You can see the list of installed Ruby
versions with `rbenv versions`.

If you're using [ruby-build][], typically this will be one of [its Ruby version
names][versions].

Other version managers might allow fuzzy version matching on the string read
from `.ruby-version` file, e.g. they might allow "1.9.3" (without patch suffix)
to match the latest Ruby 1.9.3 release. **rbenv will not support this**, because
such behavior is unpredictable and therefore harmful.

### How to verify that I have set up rbenv correctly?

1.  Check that `rbenv` is in your PATH:

    ```sh
    which rbenv
    ```

2.  Check that rbenv's shims directory is in PATH:

    ```sh
    echo $PATH | grep --color=auto "$(rbenv root)/shims"
    ```

    If not, see the [`rbenv init` step][init] in installation instructions.

### rbenv is installed but things just aren't working for me!

Please search [existing issues][issues] and open a new one if you can't find any answers. Here's a script that dumps information about your current environment; you can use [Gist][] to paste it online and share the URL to it in your bug report:

```sh
curl -s https://gist.githubusercontent.com/mislav/4728286/raw/rbenv-doctor.sh | bash -x 2>&1
```

### Which shell startup file do I put rbenv config in?

Typically it's one of the following:

* bash: `~/.bash_profile` (or `~/.bashrc` on Ubuntu Desktop)
* zsh: `~/.zshrc`
* fish: `~/.config/fish/config.fish`
* other: `~/.profile`

See [[Unix shell initialization]] for more info about how config files get
loaded.