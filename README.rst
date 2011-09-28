TurboGears2 on Red Hat's OpenShift Express
==========================================

This quickstart helps you get up and running with a fully-functional
TurboGears2 instance on OpenShift. It automatically handles creating a Python
virtualenv, populating a MySQL database, and deploying your application to the
cloud.

* Create an account at http://openshift.redhat.com/

Features
--------

* Completely free, thanks to Red Hat's OpenShift Express
* MySQL database automatically setup for your application
* Dynamic database configuration at runtime. No passwords stored in your configs.
* Your application's test suite is run after each push
* Automatic deployment upon git push
* No need to think about servers, let alone apache/mod_wsgi configuration

The fastest method
------------------

You can easily deploy a pre-configured TG2 + MySQL application to the OpenShift cloud with a single command, using my `openshift-quickstarter` tool: http://github.com/lmacken/openshift-quickstarter

::

    ./openshift-quickstarter EMAIL DOMAIN APPNAME turbogears2

That's it! You can now view your application at:

::

    http://APPNAME-DOMAIN.rhcloud.com

.. image:: http://lewk.org/img/turbogears2-quickstart.png


The manual method
-----------------

If you don't want to use the `openshift-quickstarter`, you can easily create a new OpenShift WSGI application and merge this quickstart into it manually:

::

    rhc-create-app -a tg2 -t wsgi-3.2 -l your@email.com
    rhc-ctl-app -a tg2 -e add-mysql-5.1 -l your@email.com
    cd tg2app
    git remote add upstream -m master git://github.com/lmacken/turbogears2-openshift-quickstart.git
    git pull -s recursive -X theirs upstream master
    git push

Monitoring your logs
--------------------

::

    rhc-tail-files -a tg2app -l your@email.com
