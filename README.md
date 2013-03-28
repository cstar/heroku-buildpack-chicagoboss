## Heroku buildpack: Zotonic

This is a Heroku buildpack for Zotonic sites.
Use it for easy and free deployments of Zotonic sites.
The buildpack will automatically provision a dev database and configure your Zotonic site to use it.


### Configure your site

    $ heroku config:add BUILDPACK_URL="https://github.com/cstar/heroku-buildpack-zotonic.git" -a YOUR_APP

or
    
    $ heroku create --buildpack "https://github.com/cstar/heroku-buildpack-zotonic.git"

### Configure your Zotonic site

Set the following environment variables :

  ADMIN_PASSWORD (That's the admin password, obviously)

### Select an Erlang version

The Erlang/OTP release version that will be used to build and run your application is now sourced from a dotfile called `.preferred_otp_version`. It needs to be the branch or tag name from the http://github.com/erlang/otp repository, and further, needs to be one of the versions that precompiled binaries are available for.

Currently supported OTP versions:

* master (R15B02 pre)
* master-pu (R16B pre)
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

Select the Zotonic version to deploy. Currently fetches master.

Fetches deps and rebuilds all Zotonic on each deploys, should use the build cache to only recompile the necessary bits.

IMPORTANT: All file uploads go to the transient file system, meaning that everything is destroyed on each deploys. These assets should go to S3 or similar.

Pull requests are very welcome.

### THANKS

Geoff Cant for writing the base heroku-buildpack-erlang, the starting point of this buildpack. And the Zotonic and Heroky guys.

### AUTHOR

Eric Cestari

http://twitter.com/cstar

http://eric.cestari.info/
