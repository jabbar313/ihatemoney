.. _configuration:

Configuration
=============

"ihatemoney" relies on a configuration file. If you run the application for the
first time, you will need to take a few moments to configure the application
properly.

The default values given here are those for the development mode.
To know defaults on your deployed instance, simply look at your
``ihatemoney.cfg`` file.

"Production values" are the recommended values for use in production.

`SQLALCHEMY_DATABASE_URI`
-------------------------

Specifies the type of backend to use and its location. More information on the
format used can be found on `the SQLAlchemy documentation`_.

- **Default value:** ``sqlite:///tmp/ihatemoney.db``
- **Production value:** Set it to some path on your disk. Typically
  ``sqlite:///home/ihatemoney/ihatemoney.db``. Do *not* store it under
  ``/tmp`` as this folder is cleared at each boot.

If you're using PostgreSQL, Your client must use utf8. Unfortunately,
PostgreSQL default is to use ASCII. Either change your client settings,
or specify the encoding by appending ``?client_encoding=utf8`` to the
connection string. This will look like::

    SQLALCHEMY_DATABASE_URI = 'postgresql://myuser:mypass@localhost/dbname?client_encoding=utf8'


`SECRET_KEY`
------------

The secret key used to encrypt the cookies.

- **Production value:** `ihatemoney conf-example ihatemoney.cfg` sets it to
  something random, which is good.

`MAIL_DEFAULT_SENDER`
---------------------

A python tuple describing the name and email address to use when sending
emails.

- **Default value:** ``("Budget manager", "budget@notmyidea.org")``
- **Production value:** Any tuple you want.

`ACTIVATE_DEMO_PROJECT`
-----------------------

If set to `True`, a demo project will be available on the frontpage.

- **Default value:** ``True``
- **Production value:** Usually, you will want to set it to ``False`` for a
  private instance.

`ADMIN_PASSWORD`
----------------

Hashed password to access protected endpoints. If left empty, all
administrative tasks are disabled.

- **Default value:** ``""`` (empty string)
- **Production value:** To generate the proper password HASH, use
  ``ihatemoney generate_password_hash`` and copy the output into the value of
  *ADMIN_PASSWORD*.

`ALLOW_PUBLIC_PROJECT_CREATION`
-------------------------------

If set to ``True``, everyone can create a project without entering the admin
password. If set to ``False``, the password needs to be entered (and as such,
defined in the settings).

- **Default value:** : ``True``.


`ACTIVATE_ADMIN_DASHBOARD`
--------------------------

If set to `True`, the dashboard will become accessible entering the admin
password, if set to `True`, a non empty ADMIN_PASSWORD needs to be set.

- **Default value**: ``False``

`APPLICATION_ROOT`
------------------

If empty, ihatemoney will be served at domain root (e.g: *http://domain.tld*),
if set to ``"somestring"``, it will be served from a "folder"
(e.g: *http://domain.tld/somestring*).

- **Default value:** ``""`` (empty string)

.. _the SQLAlchemy documentation: http://docs.sqlalchemy.org/en/latest/core/engines.html#database-urls

Configuring emails sending
--------------------------

By default, Ihatemoney sends emails using a local SMTP server, but it's
possible to configure it to act differently, thanks to the great
`Flask-Mail project <https://pythonhosted.org/flask-mail/#configuring-flask-mail>`_

* **MAIL_SERVER** : default **'localhost'**
* **MAIL_PORT** : default **25**
* **MAIL_USE_TLS** : default **False**
* **MAIL_USE_SSL** : default **False**
* **MAIL_DEBUG** : default **app.debug**
* **MAIL_USERNAME** : default **None**
* **MAIL_PASSWORD** : default **None**
* **DEFAULT_MAIL_SENDER** : default **None**

Using an alternate settings path
--------------------------------

You can put your settings file where you want, and pass its path to the
application using the ``IHATEMONEY_SETTINGS_FILE_PATH`` environment variable.

For instance ::

    export IHATEMONEY_SETTINGS_FILE_PATH="/path/to/your/conf/file.cfg"
