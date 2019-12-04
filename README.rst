====================
Django Skinny Deploy
====================

Simple, single file deploy a Django project to an Ubuntu
host. Full-automatic, copy-paste Nginx/Gunicorn/Let's Encrypt HTTPS
set up in minutes. Tested on Ubuntu 18.04 LTS/19.10 and Debian 10
images

.. raw:: html

    <a href="https://letsencrypt.org"><img src="https://letsencrypt.org/images/letsencrypt-logo-horizontal.svg" height="60px"></a>&nbsp;&nbsp;&nbsp;&nbsp;
    <a href="http://docs.gunicorn.org"><img src="http://docs.gunicorn.org/en/latest/_images/gunicorn.png" height="50px"></a>&nbsp;&nbsp;&nbsp;&nbsp;
    <a href="https://nginx.org"><img src="https://nginx.org/nginx.png" height="50px"></a>&nbsp;&nbsp;&nbsp;&nbsp;

 https://medium.com/p/afde190f9e80/

    
Why?
====

Because I didn't find any drop-and-run solution without overburden with a lot of files for a simple project.

Prerequisites
=============

- Get your Virtual Private Server running (Digital Ocean, Linode, Vultr or on any other provider)
- Buy and set up your domain (GoDaddy, Gandi, ...)
- Pipenv tool installed on your machine
- django-environ enabled settings for the django project

Would would happen next?
========================

- Postgresql/Nginx/Gunicorn installed and configured on the server
- All code from a local directory synced to /srv/yourdomain.com on the server
- yourdomain-com user and youdomain-com database would be created on the Postgresql
- Let's encrypt certificates requested, systemd timer installed for automatic renewal

https://yourdomain.com - became ready to serve for you.

  
Quick start
===========

The repository contains quick django project template. It's just raw
django 3.0 startproject template with Pipenv and django-environ
enabled. No extra heady sugar added.

.. code:: bash

     python3 -m pip install --user django
     django-admin.py startproject --template=https://github.com/viewflow/django-skinny-deploy/archive/template.zip mysite

For an existing project, you need to install pipenv, and modify
project settings to use django-environ.  Detailed instructions
available in the article - https://medium.com/p/afde190f9e80/

Deploy
======

.. code:: bash

    pipenv -d install ansible

.. code:: bash

     pipenv run ansible-playbook -i yourdomain.com, -u root deploy.yml

Please note the command after the domain name. It's required and tell
ansible that we have provided a domain name, instead of an inventory
file name.

Update existing deployment
==========================

.. code:: bash

    pipenv run ansible-playbook -i yourdomain.com, -u root deploy.yml -tags=update

Trobleshooting
==============

Run ansible-playbook with -vvv flag:

Check service status on the server consile:

.. code:: bash

    $ service nginx status
    $ service gunicorn_mysite_com status

Check logs at:

.. code:: python

    /var/nginx/logs

Contributing
============

Have an idea how to make this script smarter, smaller and cleaner? Pull requests are welcome!


License
=======
Zero Clause BSD

Copyright (C) 2019 by Mikhail Podgurskiy <kmmbvnr@gmail.com>

Permission to use, copy, modify, and/or distribute this software for
any purpose with or without fee is hereby granted.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL
WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE
AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL
DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR
PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER
TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR
PERFORMANCE OF THIS SOFTWARE.
