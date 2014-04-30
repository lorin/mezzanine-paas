# Mezzanine on Heroku

A quick way to deploy a Mezzanine site to Heroku. Inspired by blog posts by [Ben
Havilland][2] and [Josh Finnie][3]

## Deploy to Heroku

    git clone https://github.com/lorin/mezzanine_heroku
    cd mezzanine_heroku
    heroku login
    heroku create
    git push heroku master
    heroku run python mezzanine_heroku/manage.py createdb


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

* Doesn't support email


[1]: http://postgresapp.com
[2]: http://www.benhavilland.com/blog/deploying-mezzanine-on-heroku/
[3]: https://gist.github.com/joshfinnie/4046138
