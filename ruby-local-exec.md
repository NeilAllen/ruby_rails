The `ruby-local-exec` command is **deprecated** as of rbenv 0.4.0 and will be removed in the next major release.

## What is ruby-local-exec?

`ruby-local-exec` was introduced in rbenv 0.2.0 as a drop-in replacement for the standard Ruby shebang line:

    #!/usr/bin/env ruby-local-exec

With `ruby-local-exec` in place, scripts in an application with a `.ruby-version` or `.rbenv-version` file use the application-specific Ruby version, regardless of what directory they're run from. This is useful for running scripts in cron jobs without needing to `cd` into the application first.

## Why is it deprecated?

The functionality provided by `ruby-local-exec` has been rolled into the standard `ruby` shim provided by rbenv. 

Now, when you run scripts or binstubs in an application with a `.ruby-version` file, rbenv will automatically use the application's specified Ruby version, regardless of what directory they're run from.

To upgrade, first ensure your team and its servers are on rbenv 0.4.0 or later. Then adjust your shebangs back to:

    #!/usr/bin/env ruby

Then be sure to regenerate your shims with `rbenv rehash`.

## Can I silence the warning message?

Set `RBENV_SILENCE_WARNINGS=1` in your environment to silence the `ruby-local-exec` deprecation warning message.
