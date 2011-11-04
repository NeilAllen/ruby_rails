# Shared install of rbenv

I was asked by another user to create this page describing how I set up rbenv for multiple users to avoid the duplication of installed ruby versions and gems. This may not be best practices and I welcome any comments and will tolerate any criticisms.
 
I wanted to use rbenv but I didn't want every user - there were 5 at the time - to have to install the different ruby versions and gems. Seemed a bit redundant. 

All I did was move the ~/.rbenv to /usr/local/rbenv. 

Here's the steps: (as sudo)

1. $ cd /usr/local
2. $ git clone git://github.com/sstephenson/rbenv.git rbenv
3. $ chgrp staff rbenv
4. $ chmod -R g+rwx rbenv

I also setup ruby-build

1. $ cd
2. $ git clone git://github.com/sstephenson/ruby-build.git
3. $ cd ruby-build
4. $ ./install.sh
 
I modified the /etc/skel/.profile to include:

- `export PATH="/usr/local/rbenv/bin:$PATH"`
- `eval "$(rbenv init -)"`

I also added the same two lines to all the existing user's ~/.profile 

Now any user can install ruby versions and gems into that central location. 