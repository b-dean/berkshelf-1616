# How to reproduce [berkshelf/berkshelf#1616](https://github.com/berkshelf/berkshelf/issues/1616)

Do these things:

    rm -rf .berkshelf
    rvm use 2.3.1@berks-1616 --create
    gem install bundler
    bundle install
    BERKSHELF_PATH=.berkshelf bundle exec berks install

Which will produce output like this:

    Resolving cookbook dependencies...
    Fetching cookbook index from https://supermarket.chef.io...
    Installing nginx (2.7.6)
    Installing bluepill (2.4.3)
    Installing compat_resource (12.14.7)
    Installing 7-zip (1.0.2)
    Installing mercurial (2.0.4)
    Installing apt (2.9.2)
    Installing build-essential (2.4.0)
    Installing ohai (2.1.0)
    Installing packagecloud (0.2.5)
    Installing python (1.4.6)
    Installing rsyslog (4.0.1)
    Installing runit (1.8.0)
    Installing seven_zip (2.0.2)
    Installing windows (2.0.2)
    Installing yum (4.0.0)
    Installing yum-epel (0.7.1)

And then you can check the `Berksfile.lock` it created and see that it has `windows (< 2.0.0)` in the dependencies and `windows (2.0.2)` in the graph of installed cookbooks.

