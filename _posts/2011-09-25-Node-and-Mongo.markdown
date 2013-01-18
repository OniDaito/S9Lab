---
layout: post
title: Node and Mongo
---
##
Recently, I've been working with a good client on a project that requires network communication between two sites and provision for a history feature.One of the collaborators is a fan of [mongodb](http://www.mongodb.org/) and [nodejs](http://nodejs.org/) - two rather nifty projects that I've been meaning to work with for a while. I had no idea but dived in anyway.

####
Node appears to have a set of modules which you can install with [npm](http://npmjs.org/). These modules are placed within the directory in which you run npm which is presumably where your node script is. One useful modules is [express](http://expressjs.com/) which sets up basic handling for a website. You can then write code such as:

	var Express = require('express');
	var app = Express.createServer();

	app.get('/', function(req, res){
    	res.send('Hello World');
	});

	app.listen(3001);


Of course, post requests, paths and all the usual gubbins are supported.

####
Mongo has a set of drivers that work with node as well. I used the [Mongodb native driver](https://github.com/christkv/node-mongodb-native) which seemed pretty good, *except* for one important thing - the syntax is not quite the same as the examples given on the mongodb website. It took me sometime to realise why my queries weren't working.

	var Db = require('mongodb').Db;
	var Connection = require('mongodb').Connection;
	var Server = require('mongodb').Server;

	var client = new Db('testing', new Server("127.0.0.1", 27017, {})),
		test = function (err, collection) {
		var Figure = {id: 1, limbs : [ [1.0,5.0,10.0] , [-1,1,1]  ] };
		collection.insert( Figure , function(err, docs) {

        	// Locate all the entries using find
        	collection.find().toArray(function(err, results) {
				console.log(results);    
				// Let's close the db
				client.close();
        	});
		});
    };

	client.open(function(err, p_client) {
  		client.collection('test_insert', test);
	});

####
You can install mongodb with [homebrew](https://github.com/mxcl/homebrew) and run it locally on a mac with 

	sudo mongod run --config /usr/local/Cellar/mongodb/1.8.1-x86_64/mongod.conf

Fairly straight forward. Sadly, for use in this project, it turned out that using boost::asio with tcp::iostreams are superior. I still haven't managed to work with streams in nodejs yet, though they do exist.
