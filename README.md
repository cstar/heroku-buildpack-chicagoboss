## Heroku buildpack: ChicagoBoss

This is a Heroku buildpack for applications written with the ChicagoBoss web framework (master branch or 0.9 when release).

To select the Chicago Boss version you want to deploy, select the correct revision in your rebar.config :

```erlang

{deps, [
  {boss, ".*", {git, "git://github.com/cstar/ChicagoBoss.git", "master"}}
]}.

```

The buildpack will automatically provision a dev database and configure your application to use it.


### Configure your app

    $ heroku config:add BUILDPACK_URL="https://github.com/cstar/heroku-buildpack-chicagoboss.git" -a YOUR_APP

or
    
    $ heroku create --buildpack "https://github.com/cstar/heroku-buildpack-chicagoboss.git"

### Connecting to your postgresql database

    $ heroku pg:psql

### Select an Erlang version

The Erlang/OTP release version that will be used to build and run your application is now sourced from a dotfile called `.preferred_otp_version`. It needs to be the branch or tag name from the http://github.com/erlang/otp repository, and further, needs to be one of the versions that precompiled binaries are available for.

Currently supported OTP versions:

* OTP_R16B01 (the default)
* OTP_R15B03-1
* OTP_R15B
* OTP_R15B01
* OTP_R15B02

To select the version for your app:

    $ echo OTP_R15B01 > .preferred_otp_version
    $ git commit "Select R15B01 as preferred OTP version" .preferred_otp_version

### Deploy your site

    $ git push heroku master

You may need to write a new commit and push if your code was already up to date.

### 

Forces use of heroku postgresql database.

IMPORTANT: All file uploads go to the transient file system, meaning that everything is destroyed on each deploys. These assets should go to S3 or similar.

Pull requests are very welcome.

### LIMITATIONS

Given the architecture of Heroku, it is not advisable to use the MQ with one or more dynos. They are isolated and each would have their own queue.

### THANKS

Geoff Cant for writing the base heroku-buildpack-erlang, the starting point of this buildpack. And the Chicago Boss and Heroku guys.

### LINKS

Chicago Boss: http://www.chicagoboss.org

Heroku: http://heroku.com

### AUTHOR

Eric Cestari

http://twitter.com/cstar

http://eric.cestari.info/
