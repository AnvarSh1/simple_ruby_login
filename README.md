This is Simple Ruby Login Page, allows SignUp/SignIn/SignOut operations, based on Devise, stores all user data in a MySQL DB.
Built and tested on Ubuntu 16.04
To install:

First, some dependencies needed:

```
sudo apt-get -y install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev nodejs
```

Then, use rbenv for ruby:

```
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
rbenv install 2.4.0
rbenv global 2.4.0
ruby -v
gem install bundler
rbenv rehash
```

Next, Rails:

```
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
gem install rails -v 5.1.1
rbenv rehash
```

Now, let's install our DB:

```
debconf-set-selections <<< 'mysql-server mysql-server/root_password password p' # this and next line put 'p' as DB root pswd
debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password p' # if changed, change config file too
apt-get install -y mysql-server
apt-get install -y mysql-client libmysqlclient-dev
```

Now, you are ready to clone this app:

```
mkdir ~/rails_apps
cd ~/rails_apps
git clone https://github.com/AnvarSh1/simple_ruby_login.git
cd simple_ruby_login
bundle install #installs all gem dependencies, including Devise
rake db:create
rake db:migrate
```


Server used for this app is Puma. To start it, run following command from app directory:

```
rails s
```
or
```
rails s &
```

to run in background.

Your website will be accessible at http://localhost:3000  (start with ` -p ` flag to use different port)

Sources used:

https://gorails.com/setup/ubuntu/16.04
https://www.digitalocean.com/community/tutorials/how-to-configure-devise-and-omniauth-for-your-rails-application#step-1-create-a-new-rails-application
