# Mezzanine on Heroku

A quick way to deploy a Mezzanine site to Heroku. Inspired by blog posts by [Ben
Havilland][2] and [Josh Finnie][3]

This is just for testing. In particular, uploaded media files may vanish because
of how static files are served (see below).

## Deploy to Heroku

    git clone https://github.com/lorin/mezzanine-heroku
    cd mezzanine-heroku
    heroku login
    heroku create
    git push heroku master
    heroku run python mezzanine_heroku/manage.py createdb

You will be prompted to specify admin credentials as well as asked about
generating some default content (I answer "y" to all of these).

You will also be prompted to input a site record. Specify the hostname that Heroku assigned your app (e.g. `secret-peak-9874.herokuapp.com`).




## Run locally

The default database is Postgres. On Mac OS X, simplest thing to do is install
[Postgres.app][1]

    mkvirtualenv mezzanine_heroku
    pip install -r requirements.txt
    createdb mezzanine
    python mezzanine_heroku/manage.py createdb
    python mezzanine_heroku/manage.py collectstatic
    gunicorn mezzanine_heroku.wsgi

Serves at http://localhost:800

On subsequent runs, you can just do `gunicorn mezzanine_heroku.wsgi`.

## Issues

### Email

Not currently configured for email

### Static files

This serves static files from the local filesystem. This simplifies the
configuration, but it means we need to check some additional static files into
the repo (the static directory), and it also means that uploaded media files can
vanish.

For a production deployment, use django storages and store static and media
assets on a backend like S3.


[1]: http://postgresapp.com
[2]: http://www.benhavilland.com/blog/deploying-mezzanine-on-heroku/
[3]: https://gist.github.com/joshfinnie/4046138
