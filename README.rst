cookiecutter-django-1.8
=======================

 cookiecutter_ template for Django.

.. _cookiecutter: https://github.com/audreyr/cookiecutter

Features
---------

* For Django 1.8
* 12-Factor_ based settings via django-environ_
* Optimized development and production settings
* Media storage using Amazon S3
* Serve static files from Amazon S3 or Whitenoise_ (optional)
* Pre configured Celery_ (optional)
* Integration with Maildump_ for local email testing (optional)

.. _django-environ: https://github.com/joke2k/django-environ
.. _12-Factor: http://12factor.net/
.. _Whitenoise: https://whitenoise.readthedocs.org/
.. _Celery: http://www.celeryproject.org/
.. _Maildump: https://github.com/ThiefMaster/maildump


Constraints
-----------

* Only maintained 3rd party libraries are used.
* PostgreSQL everywhere (9.0+)
* Environment variables for configuration (This won't work with Apache/mod_wsgi).


Usage
------

Let's pretend you want to create a Django project called "redditclone". Rather than using `startproject`
and then editing the results to include your name, email, and various configuration issues that always get forgotten until the worst possible moment, get cookiecutter_ to do all the work.

First, get cookiecutter. Trust me, it's awesome::

    $ pip install cookiecutter

Now run it against this repo::

    $ cookiecutter https://github.com/rickydunlop/cookiecutter-django-1.8.git

You'll be prompted for some questions, answer them, then it will create a Django project for you.


**Warning**: After this point, change 'Your Name', 'email', etc to your own information.

It prompts you for questions. Answer them::

    Cloning into 'cookiecutter-django-1.8'...
    ...
    project_name (default is "project_name")? Reddit Clone
    repo_name (default is "Reddit_Clone")? reddit
    author_name (default is "Your Name")? Your Name
    email (default is "Your email")? email
    description (default is "A short description of the project.")? A reddit clone.
    domain_name (default is "example.com")? myreddit.com
    version (default is "0.1.0")? 0.0.1
    timezone (default is "UTC")?
    now (default is "2015/01/13")? 2015/08/04
    year (default is "2015")?
    use_whitenoise (default is "y")?


Enter the project and take a look around::

    $ cd redditclone/
    $ ls

Create a GitHub repo and push it there::

    $ git init
    $ git add .
    $ git commit -m "first awesome commit"
    $ git remote add origin git@github.com:<your repo>/redditclone.git
    $ git push -u origin master

Now take a look at your repo. Don't forget to carefully look at the generated README. Awesome, right?

Getting up and running
----------------------

The steps below will get you up and running with a local development environment. We assume you have the following installed:

* pip
* virtualenv
* PostgreSQL

First make sure to create and activate a virtualenv_, then open a terminal at the project root and install the requirements for local development::

    $ pip install -r requirements/local.txt

.. _virtualenv: http://docs.python-guide.org/en/latest/dev/virtualenvs/

Then, create a PostgreSQL database and add the database configuration using the  ``dj-database-url`` app pattern: ``postgres://db_owner:password@dbserver_ip:port/db_name`` either:

* in the ``config.settings.common.py`` setting file,
* or in the environment variable ``DATABASE_URL``


You can now run the usual Django ``migrate`` and ``runserver`` command::

    $ python manage.py migrate

    $ python manage.py runserver


It's time to write the code!!!


Not Exactly What You Want?
---------------------------

This is what I want. *It might not be what you want.* Don't worry, you have options:

Fork This
~~~~~~~~~~

If you have differences in your preferred setup, I encourage you to fork this to create your own version.
Once you have your fork working, let me know and I'll add it to a '*Similar Cookiecutter Templates*' list here.
It's up to you whether or not to rename your fork.

If you do rename your fork, I encourage you to submit it to the following places:

* cookiecutter_ so it gets listed in the README as a template.
* The cookiecutter grid_ on Django Packages.

.. _cookiecutter: https://github.com/audreyr/cookiecutter
.. _grid: https://www.djangopackages.com/grids/g/cookiecutters/

Or Submit a Pull Request
~~~~~~~~~~~~~~~~~~~~~~~~~

I also accept pull requests on this, if they're small, atomic, and if they make my own project development
experience better.
