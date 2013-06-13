---
layout: post
title: Running with Nginx
---


So I've decided to play with [Nginx](http://wiki.nginx.org/) on my server, leaving Apache behind. I must admit, I've had a lot of fun with it. It appears to be a good front end for funneling web requests to other services. At the moment, I have various things running on my server such as:


* Two sites running [Django](http://www.djangoproject.com/) with *Psycopg* connected to a [Postgresql](www.postgresql.org) database.
* A [Node.js](nodejs.org) install that talks to a [MongoDB](www.mongodb.org) database for a top secret project
* A [Mediawiki](http://www.mediawiki.org) setup that runs my own journal and ideas. Currently talks to mysql running with *php5-fpm*
* Several static pages as and when needed
* Python *uWSGI* serving for the [Denied](http://saito.section9.co.uk) application


So there is a fair bit going on that Nginx needs to take care of. Rather than use the stock Lucid install of Nginx I downloaded the source and built it with:

 sudo ./configure --prefix=/opt/nginx --user=www-data --group=www-data --with-http_ssl_module --with-ipv6

You can then hit make. There are lots of modules and other things you can build. At the moment, ssl and ipv6 are the most important to me right now.

Nginx config files are quite easy to understand and it's quite easy to get a site up and running. In the case of Django, I went with the [FastCGI](https://docs.djangoproject.com/en/dev/howto/deployment/fastcgi/) route which seemed the easiest at the time (uWSGI might be better). This means you need to run your Django in a seperate process. Using a Linux *screen* you can do something like this:

	su www-data -c './manage.py runfcgi method=prefork daemonize=false\ 
	socket=/tmp/section9.sock pidfile=django.pid maxrequests=100'

The *maxrequests* variable is very important. Without it, I noticed a lot of processes waiting for IO when I studied the site using *top*. So far, that little line has helped make things faster.


You can then setup Nginx with Django a little like this:

	server {
 		listen 80;
 		server_name www.anneblundell.com;
 		rewrite ^/(.*) http://anneblundell.com/$1 permanent;
 	}

 	server {
        server_name anneblundell.com;

        access_log  /srv/www/anneblundell.com/logs/nginx_access.log;
		error_log /srv/www/anneblundell.com/logs/nginx_error.log;

		location /media {
		root /srv/www/anneblundell.com/public_html/AnneBlundell/;
	}

	location / {
		root /srv/www/anneblundell.com/public_html/AnneBlundell;
		fastcgi_pass unix:/tmp/anneblundell.sock;

		fastcgi_param PATH_INFO $fastcgi_script_name;

		fastcgi_param REQUEST_METHOD $request_method;
        fastcgi_param CONTENT_TYPE $content_type;
       	fastcgi_param CONTENT_LENGTH $content_length;
		fastcgi_param QUERY_STRING $query_string;
		fastcgi_pass_header Authorization;
        fastcgi_param  SERVER_ADDR        $server_addr;
		fastcgi_param  SERVER_PORT        $server_port;
		fastcgi_param  SERVER_NAME        $server_name;
		fastcgi_param  SERVER_PROTOCOL 	  $server_protocol; 
		fastcgi_intercept_errors off;
	}	

So Django runs ok for now. You can write down all the *fastcgi_params* in an include file to make things a little easier.


But what about a simple Python Script? For Denied, I needed to query a text file, parse it, and present json on request. To do that, uWSGI came to mind. Use *pip* to install uwsi and then:

	sudo su -c "uwsgi --pythonpath /srv/www/section9.co.uk/public_html/python\
	 --uid www-data --module wsgi_configuration_module -s /tmp/uwsgi.sock"

This creates a socket for which we can use with Nginx to grab our data. [This Guide](http://kbeezie.com/view/circuits-nginx-uwsgi/) is quite good for setting up Nginx to talk to a process.


So Nginx takes care of a lot of things. One issue I have is dealing with Mediawiki. Annoyingly, there is quite a large slowdown in the move from Apache to Nginx and I've yet to find out the issue; likely it is my novice setup of php5-fpm. Quite annoying really. 

It's quite easy to setup static pages - simply copy the simple example config, soft link and you are done. I've yet to attempt a setup with *Ruby on Rails* yet as Im reading into [Unicorn](https://github.com/blog/517-unicorn) and other such deployment strategies. I'll let you know how it goes.