{{cookiecutter.project_name}}
==============================

{{cookiecutter.description}}


LICENSE: Apache-2.0

Settings
------------

{{cookiecutter.project_name}} relies extensively on environment settings which **will not work with Apache/mod_wsgi setups**. It has been deployed successfully with both Gunicorn/Nginx and even uWSGI/Nginx.

For configuration purposes, the following table maps the '{{cookiecutter.project_name}}' environment variables to their Django setting:

======================================= =========================== ============================================== ======================================================================
Environment Variable                    Django Setting              Development Default                            Production Default
======================================= =========================== ============================================== ======================================================================
DJANGO_CACHES                           CACHES (default)            locmem                                         redis
DJANGO_DATABASES                        DATABASES (default)         See code                                       See code
DJANGO_DEBUG                            DEBUG                       True                                           False
DJANGO_SECRET_KEY                       SECRET_KEY                  CHANGEME!!!                                    raises error
DJANGO_SECURE_BROWSER_XSS_FILTER        SECURE_BROWSER_XSS_FILTER   n/a                                            True
DJANGO_SECURE_SSL_REDIRECT              SECURE_SSL_REDIRECT         n/a                                            True
DJANGO_SECURE_CONTENT_TYPE_NOSNIFF      SECURE_CONTENT_TYPE_NOSNIFF n/a                                            True
DJANGO_SECURE_FRAME_DENY                SECURE_FRAME_DENY           n/a                                            True
DJANGO_SECURE_HSTS_INCLUDE_SUBDOMAINS   HSTS_INCLUDE_SUBDOMAINS     n/a                                            True
DJANGO_SESSION_COOKIE_HTTPONLY          SESSION_COOKIE_HTTPONLY     n/a                                            True
DJANGO_SESSION_COOKIE_SECURE            SESSION_COOKIE_SECURE       n/a                                            False
DJANGO_DEFAULT_FROM_EMAIL               DEFAULT_FROM_EMAIL          n/a                                            "{{cookiecutter.project_name}} <noreply@{{cookiecutter.domain_name}}>"
DJANGO_SERVER_EMAIL                     SERVER_EMAIL                n/a                                            "{{cookiecutter.project_name}} <noreply@{{cookiecutter.domain_name}}>"
DJANGO_EMAIL_SUBJECT_PREFIX             EMAIL_SUBJECT_PREFIX        n/a                                            "[{{cookiecutter.project_name}}] "
======================================= =========================== ============================================== ======================================================================

The following table lists settings and their defaults for third-party applications:

======================================= =========================== ============================================== ======================================================================
Environment Variable                    Django Setting              Development Default                            Production Default
======================================= =========================== ============================================== ======================================================================
DJANGO_AWS_ACCESS_KEY_ID                AWS_ACCESS_KEY_ID           n/a                                            raises error
DJANGO_AWS_SECRET_ACCESS_KEY            AWS_SECRET_ACCESS_KEY       n/a                                            raises error
DJANGO_AWS_STORAGE_BUCKET_NAME          AWS_STORAGE_BUCKET_NAME     n/a                                            raises error
======================================= =========================== ============================================== ======================================================================

Getting up and running
----------------------

Basics
^^^^^^

The steps below will get you up and running with a local development environment. We assume you have the following installed:

* pip
* virtualenv
* PostgreSQL

First make sure to create and activate a virtualenv_, then open a terminal at the project root and install the requirements for local development::

    $ pip install -r requirements/local.txt

.. _virtualenv: http://docs.python-guide.org/en/latest/dev/virtualenvs/

Create a local PostgreSQL database::

    $ createdb {{ cookiecutter.repo_name }}

Run ``migrate`` on your new database::

    $ python manage.py migrate

You can now run the ``runserver_plus`` command::

    $ python manage.py runserver_plus

Open up your browser to http://127.0.0.1:8000/ to see the site running locally.

Setting Up Your Users
^^^^^^^^^^^^^^^^^^^^^

To create an **superuser account**, use this command::

    $ python manage.py createsuperuser

Test coverage
^^^^^^^^^^^^^

To run the tests, check your test coverage, and generate an HTML coverage report::

    $ coverage run manage.py test
    $ coverage html
    $ open htmlcov/index.html

{% if cookiecutter.use_celery == "y" %}
Celery
^^^^^^
This app comes with Celery.

To run a celery worker:

.. code-block:: bash

    cd {{cookiecutter.repo_name}}
    celery -A {{cookiecutter.repo_name}} worker -l info

Please note: For Celerys import magic to work, it is important *where* the celery commands are run. If you are in the same folder with *manage.py*, you should be right.
{% endif %}
{% if cookiecutter.use_maildump == "y" %}
Email Server
^^^^^^^^^^^^

In development, it is often nice to be able to see emails that are being sent from your application. For this purpose,
a Grunt task exists to start an instance of `maildump`_ which is a local SMTP server with an online interface.

.. _maildump: https://github.com/ThiefMaster/maildump

Make sure you have nodejs installed, and then type the following::

    $ grunt start-email-server

This will start an email server. The project is setup to deliver to the email server by default. To view messages
that are sent by your application, open your browser to http://127.0.0.1:1080

To stop the email server::

    $ grunt stop-email-server

The email server listens on 127.0.0.1:1025
{% endif %}

It's time to write the code!!!
