<a href="https://crontogo.com/"><img alt="Cron To Go logo" src="https://crontogo.com/images/logo.svg" height="80" /></a>

_Cron To Go Scheduler: Run scheduled tasks on your Heroku Apps_

*Cron To Go allows you to schedule virtually any job on your Heroku applications.*

Heroku buildpack: Heroku CLI plugin for Cron To Go
==================================================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) that allows one to run the
Heroku CLI plugin for [Cron To Go Scheduler Heroku add-on](https://elements.heroku.com/addons/crontogo) in a dyno alongside application code.

Usage
-----

Example usage:

    $ heroku config:set HEROKU_API_KEY=`heroku auth:token`

    $ heroku buildpacks:add heroku-buildpack-cli-plugin-cron

    $ git push heroku master
    ...

    remote: -----> heroku-cli-plugin-cron app detected
    remote: === Fetching and vendoring Heroku CLI into slug
    remote: === Installing Heroku CLI plugin for Cron To Go into slug
    remote: === Installing profile.d script
    remote: === Heroku CLI plugin for Cron To Go installation done
    ...

    $ heroku run 'heroku auth:token'
    Running `heroku auth:token` attached to terminal... up, run.3706
    abcdef0123456789abcdef0123456789abcdef01

    $ heroku run 'heroku cron -a myapp'
    Running `heroku cron:jobs:import manifest.yml -a myapp` attached to terminal... up, run.5231

    Importing jobs to Cron To Go organization... done. 3/3 jobs imported
    
The `heroku-buildpack-cli-plugin-cron` from the [Buildpack Registry](https://devcenter.heroku.com/articles/buildpack-registry) contains the latest stable version of the buildpack. To use the edge version of the buildpack (i.e. the source code in this repository) run this command instead:

    $ heroku buildpacks:add https://github.com/crazyantlabs/heroku-buildpack-cli-plugin-cron

Notes
-----

Instead of setting HEROKU_API_KEY directly on the app as shown above, a short lived token may be passed in at run time:

```
heroku run "HEROKU_API_KEY=`heroku authorizations:create --expires-in 600 --short` heroku cron:jobs:import manifest.yml -a myapp" -a myapp
```
