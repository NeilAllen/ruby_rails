## Textmate
1. Preferences → Variables
1. add this to the front of `PATH`: `$HOME/.rbenv/bin:$HOME/.rbenv/shims:`
2. set `TM_RUBY` to this: `$HOME/.rbenv/shims/ruby`
3. if you want to fix the ruby version Textmate uses to be something other than the globally-set version, populate `RBENV_VERSION`. example: `2.1.0-preview1`
4. (and make sure the checkboxes for each of those variables is selected)
