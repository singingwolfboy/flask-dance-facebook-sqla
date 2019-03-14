Flask-Dance Example App: Facebook SQLAlchemy Edition
====================================================

This repository provides an example of how to use `Flask-Dance`_ with
a SQLAlchemy storage. This particular repository uses Facebook as an
OAuth provider, and it wires together the following Flask extensions:

* `Flask-Dance`_
* `Flask-SQLAlchemy`_
* `Flask-Login`_

You can run this code locally, or deploy it to Heroku_ to test it out.

|heroku-deploy|

Local Installation
``````````````````

Step 1: Get OAuth credentials from Facebook
-------------------------------------------
Visit https://developers.facebook.com/apps to register an
app on Facebook. You must set the application's authorization
callback URL to ``http://127.0.0.1:5000/login/facebook/authorized``.

Once you've registered your application on Facebook, Facebook will give you an
app ID and app secret, which we'll use in step 4.

Step 2: Install code and dependencies
-------------------------------------
Run the following commands on your computer::

    git clone https://github.com/singingwolfboy/flask-dance-facebook-sqla.git
    cd flask-dance-facebook-sqla
    python3 -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt

These commands will clone this git repository onto your computer,
create a `virtual environment`_ for this project, activate it, and install
the dependencies listed in ``requirements.txt``.

Also note that if you have trouble installing ``psycopg2``, it's OK to
skip it. That dependency is only needed if you are using PostgreSQL
for your database, and if you're running locally, then you can use
SQLite instead, which is simpler. SQLite is also the default option,
so you don't need to reconfigure anything.

Step 3: Create the database
---------------------------
Since we're storing OAuth data in the SQLAlchemy storage, we need to
create the database to hold that data. Fortunately, this project includes
basic command line support, so doing so is pretty straightforward.
Run this code::

    flask createdb

If it worked, you should see the message "Database tables created".

Step 4: Set environment variables
---------------------------------
Many applications use `environment variables`_ for configuration, and
Flask-Dance is no exception. You'll need to set the following environment
variables:

* ``FACEBOOK_OAUTH_CLIENT_ID``: set this to the client ID
  you got from Facebook.
* ``FACEBOOK_OAUTH_CLIENT_SECRET``: set this to the client secret
  you got from Facebook.
* ``OAUTHLIB_INSECURE_TRANSPORT``: set this to ``true``. This indicates that
  you're doing local testing, and it's OK to use HTTP instead of HTTPS for
  OAuth. You should only do this for local testing.
  Do **not** set this in production! [`oauthlib docs`_]

How you set these variables depends on your operating system.
For Mac/Linux, you can use the `export`_ command.
For Windows, you can use the `SET`_ command.
If you don't want to worry about this, you can create a ``.env`` file with
your environment variables, and use `foreman`_ to run your app. This repository
has a ``.env.example`` file that you can copy.

Step 5: Run your app and login with Facebook!
---------------------------------------------
If you're setting environment variables manually, run your app using the
``flask`` command::

    flask run

If you're using a ``.env`` file for your environment variables,
install `foreman`_ and use that to run your app::

    foreman start

Then, go to http://localhost:5000/ to visit your app and log in with Facebook!

.. _Flask: http://flask.pocoo.org/docs/
.. _Flask-Dance: http://flask-dance.readthedocs.org/
.. _Flask-SQLAlchemy: http://flask-sqlalchemy.pocoo.org/
.. _Flask-Login: https://flask-login.readthedocs.io
.. _Facebook: https://facebook.com/
.. _Heroku: https://www.heroku.com/
.. _environment variables: https://en.wikipedia.org/wiki/Environment_variable
.. _oauthlib docs: http://oauthlib.readthedocs.org/en/latest/oauth2/security.html#envvar-OAUTHLIB_INSECURE_TRANSPORT
.. _export: http://ss64.com/bash/export.html
.. _SET: http://ss64.com/nt/set.html
.. _foreman: https://github.com/ddollar/foreman
.. _virtual environment: https://docs.python.org/3.7/library/venv.html
.. _Fork this GitHub repo: https://help.github.com/articles/fork-a-repo/

.. |heroku-deploy| image:: https://www.herokucdn.com/deploy/button.png
   :target: https://heroku.com/deploy
   :alt: Deploy to Heroku
