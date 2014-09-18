# Ruby Installation Instructions

These directions are for OS X Mavericks, Mountain Lion and Lion:

## Prequel

* Install XCode
    * Go to App Store.
    * Search XCode.
    * Install.
* Install Apple Command Line Tools
    * Go to App Store

    * Open XCode
    * Go to Preferences > Downloads
    * Click Command Line Tools and install
    * Do not direct-install Command Line Tools; not everything you
      need will be installed.
* Install Macports (http://www.macports.org/install.php)
    * Download the Mavericks .pkg installer
    * Run the installer.
* Install apple-gcc42:
    * In the terminal run `sudo port install apple-gcc42`.
* Install git:
    * In the terminal run `sudo port install git`.
* Install the readline library:
    * In the terminal, run `sudo port install readline`.

## rbenv and Ruby

In the terminal, run

    git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
    git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build

Now we want to tell the bash terminal to include our newly built
rbenv/ruby every time we open a new terminal session.  By default,
bash isn't smart enough to search every path on your computer for all
the software you may have hiding in your files. To explicitly tell
bash to include a certain path we can modify the `~/.bash_profile`
file with any text editor and add a reference to a path to
include. This `~/.bash_profile` is a script that runs every time a new
instance of the bash shell is opened. For this reason, it is necessary
to close and reopen the terminal to see changes made to the
`~/.bash_profile` actually take effect.

Open `~/.bash_profile` in a text editor and add the following lines:
(I might type `mate ~/.bash_profile` to edit the file with textmate.)

    export PATH="$HOME/.rbenv/bin:$PATH"
    eval "$(rbenv init -)"

To include these to changes to bash profile, it is necessary to close
the terminal and open a new instance. Do so now.

Next, in our closed and reopened terminal window, we install Ruby with
the following command:

    CC=/opt/local/bin/gcc-apple-4.2 CONFIGURE_OPTS="--disable-install-rdoc" RUBY_CONFIGURE_OPTS="--with-readline-dir=/opt/local --with-openssl-dir=/opt/local" rbenv install 2.1.2 -v

After installation completes, tell rbenv to use the newly installed
Ruby version as default:

    rbenv global 2.1.2

These commands tell rbenv to install Ruby using the GCC compiler (not
clang), to not generate unnecessary rdoc (this is super slow), and to
make sure to use the readline library (in preference to OS X's
inferior libedit).

Lastly, open a fresh terminal and make sure it worked with:

```ruby
~$ which ruby
/Users/ruggeri/.rbenv/shims/ruby
~$ which gem
/Users/ruggeri/.rbenv/shims/gem
```

You **don't** want to see `/usr/bin/ruby` or `/usr/bin/gem`.

Once you are using the right version of `gem`, **install bundler**:
`gem install bundler`. Verify you're using the right bundle, too:

```ruby
~$ which bundle
/Users/ruggeri/.rbenv/shims/bundle
```

## Versions of Ruby

Different versions of Ruby have subtly (or sometimes not-so-subtly)
different APIs. You can probably save yourself some time and
frustration by referring only to the documentation for the version
you're using.

You can verify your version in a shell with `ruby -v`.

The default version for this course is currently
[Ruby 2.1.2](http://ruby-doc.org/core-2.1.2/).
