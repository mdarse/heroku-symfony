Symfony2 on Heroku example
==========================

The [Heroku toolbelt](https://toolbelt.heroku.com) is required for next steps.

To deploy to Heroku, create an application:
```
$ heroku apps:create --addons cleardb:ignite --region eu
```

Optionnaly, you can specify an application name:
```
$ heroku apps:create --addons cleardb:ignite --region eu awesome-app
```
This will make your app available from `http://awesome-app.herokuapp.com`.


For the application to work in the right environment (ie. "prod"), add an
environment variable in the Heroku application:
```
$ heroku config:set SYMFONY_ENV=prod
```

For the application to be able to access the MySQL database, we need to copy the
`CLEARDDB_DATABASE_URL` to the `DATABASE_URL` environment variable:
```
$ heroku config:set `heroku config --shell | grep CLEARDB_DATABASE_URL | sed -e 's/^CLEARDB_//'`
```

Then you just need to push your code on Heroku:
```
$ git push heroku master
```
You should have some output like this:
```
Counting objects: 4, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 543 bytes | 0 bytes/s, done.
Total 4 (delta 1), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote: 
remote: -----> PHP app detected
remote: -----> Resolved composer.lock requirement for PHP to version 5.6.4.
remote: -----> Installing system packages...
remote:        - PHP 5.6.4
remote:        - Apache 2.4.10
remote:        - Nginx 1.6.0
remote: -----> Installing PHP extensions...
remote:        - zend-opcache (automatic; bundled)
remote: -----> Installing dependencies...
remote:        Composer version 1.0.0-alpha9 2014-12-07 17:15:20
remote:        Loading composer repositories with package information
remote:        Installing dependencies from lock file
remote:          - ...

remote:        Generating optimized autoload files
remote:        Creating the "app/config/parameters.yml" file
remote:        Clearing the cache for the prod environment with debug false
remote:        Trying to install assets as symbolic links.
remote:        Installing assets for Symfony\Bundle\FrameworkBundle into web/bundles/framework
remote:        The assets were installed using symbolic links.
remote: -----> Preparing runtime environment...
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote: 
remote: -----> Compressing... done, 77.5MB
remote: -----> Launching... done, v8
remote:        https://gentle-earth-5510.herokuapp.com/ deployed to Heroku
remote: 
remote: Verifying deploy... done.
To https://git.heroku.com/gentle-earth-5510.git
 * [new branch]      master -> master

```

Your app sould be available :)
