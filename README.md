#Churchill Docker CLI 
	
This is a binary release repos for the ``Churchill Docker CLI`` project. This project allows for auto-generation of ``docker-compose`` and `Dockerfile`` file based on Heroku-based Procfile and ``app.json``

Source Code will be released once it is more mature.

Installation:

	curl -L https://github.com/timchunght/churchill/releases/download/0.1.0/churchill-`uname -s`-`uname -m` > /usr/local/bin/churchill
	chmod +x /usr/local/bin/churchill

###How To Use It:

Currently, I have only tested on ``Rails+Postgres`` and ``Nodejs`` using my custom cedar image, ``timchunght/cedar`` built on top of ``convox/cedar``.

###Setup (Ruby on Rails Example):

app.json

	{
	  "name": "SampleRailsApp",
	  "description": "Sample Rails App",
	  "image": "timchunght/cedar",
	  "addons": [
	    "heroku-postgresql"
	  ]
	}

Currently, the ``addons`` names follow the conventions set by Heroku, however, we can change that later as more plugins are added.

Procfile

	web: bundle exec unicorn

This file is absolutely necessary. The CLI will translate this into ``commands`` and linked images in your ``docker-compose`` file. For example, ``web: bundle exec unicorn`` becomes,
	
	web:
	  build: .
	  command: 'bash -c ''bundle exec unicorn''

in the ``docker-compose.yml`` file.

That's it! Push your code and ssh into your VM that has ``docker`` and ``docker-compose`` installed.

 	docker-compose build

To run migration, 
	
	docker-compose run shell rake db:migrate

You can simply do ``docker-compose run shell`` to gain shell access.

###	Rebuild:

	docker-compose build

### Run the App

	docker-compose up web

Visit, your ip:8080 to see your app running

### Deploy

After making sure the app runs,

	docker-compose up web -d

This will run the containers in background

This is simply the most basic setup I can find other than ``git push heroku master``

TODOs or Good to Have:

	nginx load balancing/reverse proxy with caching
	Test other setups like Django, Go, Scala

I currently study and research at Columbia University on Docker and Robotics. I am also looking for internship in New York or Bay Area (that is where my family lives). Please contact me.


