## Heroku buildpack: ChicagoBoss

This is a Heroku buildpack for applications written with the ChicagoBoss web framework (version 0.8.5).

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

* OTP_R15B03-1 (the default)
* OTP_R15B
* OTP_R15B01
* OTP_R15B02

To select the version for your app:

    $ echo OTP_R15B01 > .preferred_otp_version
    $ git commit "Select R15B01 as preferred OTP version" .preferred_otp_version

### Deploy your site

    $ git push heroku master

You may need to write a new commit and push if your code was already up to date.

### TODO

Select the Chicago version to deploy. Currently fetches 0.8.5.

Forces use of heroku postgresql database.

IMPORTANT: All file uploads go to the transient file system, meaning that everything is destroyed on each deploys. These assets should go to S3 or similar.

Pull requests are very welcome.

### LIMITATIONS

Given the architecture of Heroku, it is not advisable to use the MQ with one or more dynos. They are isolated and each would have their own queue.

### BUG

For some reason, the routes extracted from the controller naming scheme are not used.
Add the following line to your routes :

    {"/(.*?)/(.*?)/(.*?)", [{controller, '$1'}, {action, '$2'}, {id, '$3'}]}.
    
Which is not always working. Will fix that in an ulterior release. In any case, you have to be explicit for the moment.

### THANKS

Geoff Cant for writing the base heroku-buildpack-erlang, the starting point of this buildpack. And the Chicago Boss and Heroku guys.

### LINKS

Chicago Boss: http://www.chicagoboss.org

Heroku: http://heroku.com

### AUTHOR

Eric Cestari

http://twitter.com/cstar

http://eric.cestari.info/
