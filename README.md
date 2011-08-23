CakePHP on OpenShift Express
============================

This git repository helps you get up and running quickly w/ a CakePHP installation
on OpenShift Express.  The backend database is MySQL and the database name is 'cake'
which matches the application name 'cake'.  You can call your application by
whatever name you want (the name of the database will always match the application).


Running on OpenShift
----------------------------

Create an account at http://openshift.redhat.com/

Create a php-5.3 application (you can call your application whatever you want)

    rhc-create-app -a cake -t php-5.3

Add MySQL support to your application

    rhc-ctl-app -a cake -e add-mysql-5.1

Add this upstream seambooking repo

    cd cake
    git remote add upstream -m master git://github.com/openshift/cakephp-example.git
    git pull -s recursive -X theirs upstream master
    
Then push the repo upstream

    git push

That's it, you can now checkout your application at (default admin account is admin/admin):

    http://cake-$your_domain.rhcloud.com


NOTES:

GIT_ROOT/.openshift/action_hooks/build:
    This script is executed with every 'git push'.  Feel free to modify this script
    to learn how to use it to your advantage.  By default, this script will create
    the database tables that this example uses.

    If you need to modify the schema, you could create a file 
    GIT_ROOT/.openshift/action_hooks/alter.sql and then use
    GIT_ROOT/.openshift/action_hooks/build to execute that script (make susre to
    back up your application + database w/ rhc-snapshot first :) )

CakePHP Security:
    If you're doing more than just 'playing' be sure to edit app/config/core.php
    and modify Security.salt and Security.cipherSeed.