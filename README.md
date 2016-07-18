## Heroku buildpack for running your task (php artisan commands) on deploy
This buildpack is intended for use after the regular [php-buildpack].

## Usage

If you are using the default buildpack, manually set your buildpack to Heroku's default PHP buidpack

```
heroku buildpacks:set https://github.com/heroku/heroku-buildpack-php --app nhub
```

Append the heroku-buildpack-laravel-deploy-tasks to your buildpack list:

```
heroku buildpacks:add https://github.com/dretnan/heroku-buildpack-laravel-deploy-tasks --app nhub
heroku buildpacks:add https://github.com/dretnan/heroku-buildpack-laravel-deploy-tasks
```


Configure DEPLOY_TASKS environment variable with anything in the build directory. This basically runs any command you supplied

```
heroku config:set DEPLOY_TASKS='true' --app nhub
heroku config:set DEPLOY_TASKS='php artisan migrate:reset && php artisan migrate --force' --app nhub
heroku config:set DEPLOY_TASKS='php artisan migrate:reset && php artisan migrate --force && php artisan db:seed' --app nhub
```

Set the MIGRATE_REFRESH environment to true to reset your app each time you deploy. This simply runs 'php artisan migrate:refresh and php artisan db:seed' on deploy:

```
heroku config:set MIGRATE_REFRESH='true' --app nhub
heroku config:set MIGRATE_REFRESH='true' --app
```

## License

MIT, see the LICENSE file.

[php-buildpack]:https://github.com/heroku/heroku-buildpack-php
